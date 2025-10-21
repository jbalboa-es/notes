# Utilidades
- 0 se considera false y cualquier otro valor true.
- for(;;) similar a while(true) = while(1)
# Pthreads

Pueden compartir memoria y son baratos de instanciar.
- Core: Núcleo de ejecución
- Parece que se ejectuan en paralelo pero no es así.
- Antes de implementar threads investigar si hay algoritmos más eficientes.


- \#include <pthread.h>
- int pthread_create(pthread_t \*thread, const pthread_attr \*attr, void \*(\*start_routine)(void\*), void \*arg);
	- retorna 0 si la creación del thread fue exitosa.
	- termina si start_routine retorna, o
	- con void pthread_exit(void \*return_value)
	- notar que start_routine debe recibir y retornar un puntero opaco.

- el thread que maneja la lógica coordinada debe encargarse de esperar el término de los threads creados con pthread_create, esto se hace al "enterrar" un pthread con:
	int pthread_join(pthread thread, void \*\*return_value)
	- retorna 0 en caso de éxito

- Para usar más argumentos:
	typedef struct {
		ulonglong x;
		uint i, j;
		uint res; *//almacenar resultados intermedios*
		} Args;
## Diseño

1. Analizar partes paralelizables
2. Crear Args
3. Programar thread (función a paralelizar), notar que su retorno debe ser de tipo void \*
## Lógica

4. Lanzar threads
5. Esperar
6. Enterrar y recolectar resultados

## Secciones críticas

Zonas donde están los recursos compartidos.
### Mutex: MUTual EXclusion

Garantiza la exclusión mutua, bloqueando acceso a zonas críticas.
- pthread_mutex_t mutex = PTHREAD_MUTEX_INITIALIZER;
	Inicialización global
- int pthread_mutex_init(phtread_mutex \*m, pthread_mutexattr_t \*a);
	Inicialización local
- int pthread_mutex_destroy(pthread_mutex_t \*m);
	Destruir y liberar memoria
- int pthread_mutex_lock(pthread_mutex_t \*m);
	Solicitar
- int pthread_mutex_unlock(pthread_mutex_t \*m);
	Liberar

## Condiciones

- pthread_cond_t cond =PTHREAD_COND_INITIALIZER;
	Inicialización global
- int pthread_cond_init(pthread_cond_t \*cond, pthread_condattr_t \*a);
	Creación local
- int pthread_cond_destroy(pthread_cond_t \*cond);
	Destruye y libera recursos
- int pthread_cond_wait(pthread_cond_t \* cond, pthread_mutex_t \*m);
	Espera hasta que se cumpla la condición
	Notar que libera el mutex y bloquea el hilo; al despertarse vuelve a adquirir el mutex antes de continuar.
- int pthread_cond_boradcast(pthread_cond_t \*cond);
	Despierta a todos
- int pthread_cond_signal(pthread_cond_t \*cond);
	Despierta a uno

#### Sobre cena de filosofos:

- Con la solución de mutex se genera una solución correcta pero no necesariamente justa, puesto que evita el deadlock pero aún así no todos comen al mismo tiempo.
### Uso correcto de wait

- Spurios wakeups, el wait se puede despertar aunque nadie haya hecho signal o broadcast. Con el while nos aseguramos que si esto sucede, se vuelva a chequear la condición.
- while bajo condición booleana, no suelta el core y lo mantiene ocupado. (sin pthread_cond_wait)

### Clasificación problemas:

- Paralelizable: No dependencia entre threads.
- Sincronización: Dependencia.
## Problemas

- datarace: variables se sobreescriben incorrectamente
- race conditions: orden incorrecto de ejecución
- starvation(hambruna): un thread no obtiene tiempo de ejecución
- deadlock: hambruna global
- busy waiting: core se queda permanentemente ocupado.

## Orden de atención

- pthread_mutex_lock y pthread_cond_wait se despiertan en cualquier orden.

### No especificado

```C
int ticket, display;
// problema: cambios de contextos innecesarios
```

### Por orden de llegada

Se utiliza Patrón *request*: Como solución a los cambios de contexto innecesarios.

Fijarse en condición para que despierte (orden de llegada, mas cercano, etc). junto a los átributos que requiere una vez despierte, para ver que agregar a la estructura.


```C
typedef struct {
	int ready;
	pthread_cond_t w;
} Request;

Queue *q;
void ocupar():
	if(!ocupado){ //si no está ocupado
		..
	} else {
		Request req={0,
			PTHREAD_COND_INITIALIZER};
		put(q, &req);
		while(!req.ready){
			pthread_con_wait(&req.w, &m)
		}
	}
}
unlock;
}

void desocupar():
if(emptyQueue(q))
	busy=0;
else {
	Request *preq=get(q);
	preq->ready=1;
	pthread_cond_signal(&preq->w)
}
```

Diferencia entre get() y peek() en una cola,
	get() obtiene y elimina el primer elemento
	peek() obtiene pero NO elimina el primer elemento
```C
Request dummy; //para marcar si se deben leer todos los lectores
void enqueue(Kind kind){
	//Si es un Writer: se encola
	//Si es un reader,
		//Si es el primer reader, se ubica dummy en cola de writer para dejar la marca
		//Si no, simplemente se encola
}

void wakeup(){
	Req *preq=get(wq); //se obtiene el primer valor de la cola de writer
	//Si el primer elemento de la cola es NULL, se retorna
	//Si el primer elemento es un writer, se deja que se ejecute (writer++; ready=1, signal;)
	//Si el elemento es dummy, se procesan todos los readers. (while(!empty(rq)) readers++; ready=1; signal;)
}
```

### Diseño

1. Diseñar estructura para hacer Request.
	a. Indicador de cuándo está lista la petición y herramienta para despertar el thread
	b. Debe incluir toda información necesaria para continuar
2. Escoger estructura que permita acceder las Request en el orden deseado.
3. Diseñar proceso para registrar una Request
4. Diseñar proceso para procesar Requests

// AUX 3

## Semáforos
- Representa un dispensador de fichas
- En el caso que un thread solicite un ticket y no haya tickets disponibles, deberá esperar
- Inicializar un semáforo: 
	- void sem_init(sem_t \*sem, int pshared, unsigned val);
		- sem_t \*sem: puntero a semáforo a inicializar. 
		- int pshared: Flag para indicar si semáforo será compartido entre threads (pshared = 0) o entre procesos (pshared = 1). 
		- unsigned int val: Cantidad de fichas iniciales.
- sem_t sem; sem_init(&sem, 0, 1);
- Extraer una ficha: void sem_wait(sem_t \*sem);
	- Depositar una ficha: void sem_post(sem_t \*sem);
### Operaciones
```C
// Inicializar
void sem_init(sem_t *sem, int pshared, unsigned val);
//sem: dir; pshared: 0=se comparte entre hilos mismo proceso; !0 = se puede compartir entre procesos distintos; value: 0=empieza cerrado, >0=empieza abierto con ese conteo de permisos
//Extraer
void sem_wait(sem_t *sem);
//Depositar
void sem_post(sem_t *sem);
//Destruir
void sem_destroy(sem_t *sem);
```

- Si no hay fichas disponibles > sem_wait espera hasta que otro thread deposite una ficha con sem_post.
- Si hay varios threads en espera, no se específica orden.
- Para garantizar exclusión mutua: se inicializa solo con una ficha.
- O suspender thread hasta que se cumpla condición: se inicializa con 0 fichas.

### Cena de filósofos
Se crean 5 direcciones de sem_t
Se genera una ficha para (for) cada uno.
Se garantiza exclusión mutua para palito j y k con sem_wait.
sem_post para unlockear.

### Productor/Consumidor
Productores ponen items y los consumidores los sacan.

La idea de reemplazo:
- Si alguien no puede continuar, deja un "semáforo personal" en la cola y se bloquea en él.
- Cuando alguien libera espacio o pone un item, busca en la cola correspondiente y "despierta" al que estaba esperando.
```C
sem_wait(&buf->mutex); //lock
//si buffer lleno
	sem_t w; //semaforo privado del hilo
	sem_init(&w, 0, 0); //empieza bloqueado
	//lo pongo en la cola
	sem_post(&buf->mutex); //unlock
	sem_wait(&w); //me duermo en MI semáforo
//si hay espacio, escribo
//chequeo si en los consumidores hay alguno esperando
//si no, unlock normal
//si si, despierto a uno
```
Cuando se despierta, se prosigue justo después del sem_wait.

|Aspecto|Productor–Consumidor|Lectores–Escritores|Cena de Filósofos|
|---|---|---|---|
|**Recurso**|Buffer finito (slots)|Recurso lógico (ej. BD, archivo)|Tenedores (recursos compartidos múltiples)|
|**Restricción**|No consumir de buffer vacío, no producir en buffer lleno|Lectores simultáneos, escritor exclusivo|Cada filósofo necesita 2 tenedores|
|**Control**|Cantidad (espacios disponibles)|Rol (lector vs escritor)|Acceso múltiple y simultáneo a varios recursos|
|**Objetivo**|Balancear flujo entre productores y consumidores|Equilibrar concurrencia justa entre lectores y escritores|Evitar deadlock e inanición entre procesos vecinos|
|**Sincronización**|Productores ↔ Consumidores|Lectores ↔ Escritores|Filósofos ↔ Recursos (tenedores)|
|**Problema extra**|Bloqueo si buffer lleno/vacío|Inanición si no se da prioridad justa|Deadlock y inanición|
|**Estructuras típicas**|Semáforos contadores + mutex|Mutex + contadores + colas de espera|Semáforos por tenedor + mutex global/políticas de orden|

Descomponer en subintervalo: en un ciclo en donde no hay dependencia entre iteraciones, se puede descomponer el intervalo del ciclo en NT subintervalos y cada thread se ocupa de un subintervalo. • Ejemplos: multiplicación de matrices, búsqueda de un factor • Divide y conquista en paralelo: en una función con 2 llamadas recursivas, la primera llamada se ejecuta en un nuevo thread y la segunda en el thread original. • Generar demasiados threads es ineficiente • Cuando se hayan completado nt threads se continúa secuencialmente con la recursividad

• El típico paralelismo que habíamos visto hasta el momento es del tipo AND: se necesita los resultados de todos los threads • La búsqueda de un factor en paralelo es del tipo OR: si uno de los threads encuentra un resultado, no se necesitan los resultados de los demás threads • El problema es detenerlos

• Alternativa: usar una variable booleana compartida que indica cuando se encontró un factor, pero eso significa un pequeño sobrecosto en consultar esa variable por cada división hecha • Esa variable se lee casi siempre, por lo que los cores la pueden mantener en sus propios cachés, ¡excepto si por mala suerte queda en la misma línea de una variable que los threads sí modifican!









