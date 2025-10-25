
# 7.1
```C
/*
 calcula tiempo absoluto a esperar y decide si rearmar el temporizador real,
 guarda la funcion wake-up en la estructura thread y la pone en la cola
 de temporizadores ordenados.
 O bien, marca al thread inmediatamente como listo
*/

void nth_programTimer(long long nanos, void(*wakeUpFun)(nThread th)){
	nThread thisTh = nSelf();                 // thread que está ejecutando 
											  // esta función
											  
	if(nanos > 0){                            // si hay tiempo, entonces se
									          // programamos un temporizador
									          
		long long currTime = nGetTimeNanos(); // obtener el tiempo actual en
											  // nanosegundos
											  
		long long wakeTime = currTime+nanos;  // tiempo absoluto para despertar
		
		if( nth_emptyTimeQueue(nth_timeQueue) 
		|| wakeTime-nth_nextTime(nth_timeQueue)<0){ 
											  // si la cola está vacía o si nuevo
											  // wakeTime es el más temprano
											
			nth_setRealTimerAlarm(wakeTime-currTime); 
											  // armar timer
		}
		
		thisTh->wakeUpFun=wakeUpFun;          // guarda en estructura de thisTh el
											  // puntero a la función callback
											
		nth_putTimed(nth_timeQueue, thisTh, wakeTime); 
											  // insertar en cola de temporizadores
											  // con su wakeTime
	}
	else {
		setReady(thisTh);                     // no se espera, marcando como 
											  // listo/ready al thread
	}
}
```

```C
/*
	revisar la cola de threads que estaban esperando por tiempo,
	y despertar los que ya deben ejecutarse.
*/
void nth_wakeThreads(void) {
	long long currTime= nGetTimeNanos();
	while (!nth_emptyTimeQueue(nth_timeQueue) &&
		nth_nextTime(nth_timeQueue)<=currTime ){ 
											  /*
												  Mientras la cola no este vacía
												  y el próximo tiempo de despertar
												  sea menor o igual al tiempo
												  actual.
											  */
		nThread th= nth_getTimed(nth_timeQueue);
											  // extrae primer thread de cola
											  
		if(th->wakeUpFun!=NULL)               // si tiene asignada un wakeUp
			(*th->wakeUpFun)(th);
		setReady(th);                         // después de ejecutar wakeUpFun
											  // el hilo se marca como listo
	}
	nth_setRealTimerAlarm(                    // rearma el temporizador real
	nth_emptyTimeQueue(nth_timeQueue) ?
	0 : nth_nextTime(nth_timeQueue)-currTime );
											  // cola vacía -> ret 0, no hay mas
											  // alarmas programadas
											  // o calcula cuánto falta para el
											  // proximo evento
}
```

```C
/*
	cancela cualquier espera programada para un thread y actualiza el
	temporizador global si es necesario
*/
void nth_cancelThread(nThread th){
	nth_delTimed(nth_timeQueue, th);          // elimina el thread de la cola
											  // temporizadores. Es como decir,
											  // este thread ya no debe despertarse
											  // cuando llegue su tiempo
											  
	nth_wakeThreads();                        // revisa y reconfigura el
											  // temporizador real del sistema
}
```

```C
/*
	Decide qué hilo ejecutará cada core virtual
	Cambia de contexto entre hilos
	Usa una cola de listos
	Puede haber multiples cores simulados, por eso usa nth_corePark(),
	nth_allocCoreId()
*/

// static: funcion interna
static void nth_fcfsSchedule(void) {

	CHECK_CRITICAL("nth_fcfsSchedule") // vertificar region crítica

	nThread thisTh= nSelf();
	for (;;) { // hasta que encuentre un hilo que ejecutar
	
	// CASO 1: seguir en el mismo hilo actual
		// si ya habia un hilo y esta listo o corriendo
		if (thisTh!=NULL && (thisTh->status==READY || thisTh->status==RUN)) {
			// asigna core virtual al hilo actual
			// nth_allocCoreId(thisTh)<0 : no se le puede asignar uno
			if (nth_allocCoreId(thisTh)<0 && thisTh->status==READY)
				// y estado ready
				nth_delQueue(nth_fcfsReadyQueue, thisTh); // lo saca de la cola
			break; // sale del bucle y sigue ejecutando el mismo hilo
		}
	
	// CASO 2: buscar un nuevo hilo para ejecutar
		nThread nextTh= nth_getFront(nth_fcfsReadyQueue); 
					// primer hilo cola listos
					
		// si hay alguno listo para ejecutar
		if (nextTh!=NULL) {
			// codigo de depuracion
			DBG(
				// existe hilo actual
				if (thisTh!=NULL) {
					// no debería estar en estado RUN
					if (thisTh->status==RUN)
						nFatalError("schedule", "Thread should be READY\n");
					// si esta READY debe seguir en cola de listos
					if ( thisTh->status==READY &&
						!nth_queryThread(nth_fcfsReadyQueue, thisTh) )
						nFatalError("schedule", "Ready thread not in ready queue\n");
				}
			);
			
			// guarda contexto thisTh y cambia a nextTh
			// durante esto, nextTh comienza a ejecutarse
			// thisTh queda pausado
			// este método retorna más tarde, cuando otro hilo devuelve el core
			nth_changeContext(thisTh, nextTh);
			
			// tras un nuevo cambio de contexto, si el hilo quedo en estado
			// READY, sale del bluce
			if (thisTh->status==READY)
				break;
		}
		
		// si no hay hilos listos, el core actual se apaga o duerme temporalmente
		// espera señal
		nth_corePark();
	}
	// asegura que nSelf() siga apuntando al mismo hilo
	DBG(
		if (thisTh!=nSelf())
			nFatalError("nth_fcfsSchedule", "nSelf() inconsistency\n");
	);
	CHECK_STACK // verifica desbordamiento de pila
	thisTh->status= RUN; // cambia estado a RUN
	if (!nth_emptyQueue(nth_fcfsReadyQueue)) // si aun hay hilos esperando
		nth_reviewCores(); // revisa si hay otros cores libres,
						   // simulando paralelismo
}
```

`START_CRITICAL` y `END_CRITICAL` aseguran la exclusión mutua en sección crítica.
en `schedule()` con `CHECK_CRITICAL()` se verifica que el código que llamó al scheduler ya hubiera realizado un `START_CRITICAL`.

Por tanto, el orden correcto sería:

```C
void nth_RTimerHandler(...) {
    START_HANDLER
    nth_wakeThreads();
    nThread th = nSelf();
    if (!nth_coreIsIdle[nth_coreId()] && th != NULL)
        schedule();  // aquí se llama al scheduler
    END_HANDLER
}
```

```C
/*
	Se llama cada vez que un hilo pasa de un estado bloqueado o dormido a estar
	listo para ejecutarse otra vez
	Cuando usar:
	1. Cuando se cumple el tiempo de espera de un hilo dormido
	2. Cuando un hilo deja de estar bloqueado en un recurso
	3. Cuando se crea un hilo nuevo
	4. Cuando un hilo es desbloqueado manualmente (nth_cancelThread)
	Cuando NO usar:
	- hilo ya en RUN
	- hilo ya READY
	- o dentro de sección crítica, a menos que se sepa que el hilo se va a
	  pausar después
*/

// static: visibilidad archivo
static void nth_fcfsSetReady(nThread th) {
	CHECK_CRITICAL("nth_fcfsSetReady") 
		// verifica y exige que estemos dentro de sección crítica
	
	if (th->status==READY || th->status==RUN)
		nFatalError("nth_fcfsReady", "The thread was already in READY status\n");
	
	th->status= READY;
	if (nth_allocCoreId(th)<0) // no hay core disponible
		nth_putBack(nth_fcfsReadyQueue, th); 
					// encolamos al final de la cola de listos
	
	// si core asignado es distinto al core actual
		// nth_coreId() : devuelve id del core que se está ejecutando
	else if (nth_allocCoreId(th)!=nth_coreId()) { 
#if 0
	DBG(
		printf("wake core %d up from %d\n", nth_allocCoreId(th), nth_coreId());
	);
#endif
		nth_coreWakeUp(nth_allocCoreId(th)); // se despierta ese core
	}
	
	// si el core es el actual, no hace falta despertar a nadie
}
```