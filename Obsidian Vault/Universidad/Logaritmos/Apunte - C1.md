# Cotas inferiores
Complejidad (superior) > Costo mejor algoritmo

- Algoritmos que toman tiempo O(Tn) son óptimos > No hay otros de complejidad menor que lo resuelvan
- Cota inferior (símbolo Omega) ajustada > no puede haber mejor cota inferior (más alta)
- Complejidad exacta > símbolo Theta
## Estrategia del Adversario

Cotas inferiores de **peor caso**.
Algoritmo paga el costo de preguntar (leer datos, comparar elementos, etc.) algo sobre el input, adversario decide qué responder.

Se requiere crear un modelo de lo que el algoritmo va aprendiendo acerca del input.
	Estado inicial > Algortimo no sabe nada del input
	Estados(s) final(es) > Algoritmo aprendió lo suficiente para responder.
	Cota inferior > Mínimo costo de llegar de i a f

### Búsqueda de un arreglo

1. Arreglo desordenado:
	Peor caso > input está en valor no examinado
2. Arreglo ordenado:
	Elemento en subarreglo A[i,j] 
	Si accede a un elemento A\[k]:
		1. A[k] no está en [i,j], no aprende nada
		2. A[k] es el elemento buscado, está en A[k,k]
		3. A[k] mayor, entonces está en [i, k-1]
		4. A[k] menor, entonces está en [k+1, j]
	Inicial: A[1,n]
	Final: A[k,k]
	log2(n)

### Máximo de un arreglo

- Algoritmo "torneo de tenis"
- Cota inferior:
	- Modelo 1:
		- Estado inicial grafo n nodos sin aristas
		- Estado final grafo conexo
		- Como se necesitan n-1 aristas, este es una cota inferior
	- Modelo 2:
		- a cardinal conjunto nunca comparados
		- b comparado alguna vez y han ganado todas sus comparaciones
		- c han perdido
		- Estado inicial: (n, 0, 0)
		- Estado final: (0, 1, n-1)
		- Observar que c crece a lo sumo de a uno y como pasa de 0 a n-1, se necesita al menos n-1 comparaciones.
	n-1

### Mínimo y máximo de un arreglo

Modelo:
- a es cardinal de elementos que nunca se han comparado
- b comparado alguna vez y han ganado todo
- c comparado alguna vez y perdido todo
- d ganado alguna vez y perdido alguna vez
- Estado inicial: (n, 0, 0, 0)
- Estado final: (0, 1, 1, n-2)
(3/2)\*n - 2
### Máximo y segundo máximo de un arreglo

- n-1 para el maximo
- log2(n) - 1 para el segundo maximo
- n + log2(n) - 2
- Al aplicar el modelo de la tabla, debemos tener cuidado en escoger bien el estado final.
- Podemos usar el modelo del grafo, luego de escoger el maximo, quitar el maximo y las aristas hacía y nuevamente buscar un grafo conexo.
- Equivalente a solo encontrar el segundo máximo.

### Mediana de un arreglo

- Arreglo impar > No se conoce el número exacto de comparaciones
- Mediana será z
- Comparacion crucial > Permite conocer la relación entre x y z
- Dibujamos arista entre x y z, roja si x > z, azul si x < z.
- Pintamos también a x de rojo o azul, respectivamente.
- Para todo nodo rojo, dibujamos aristas rojas para elementos y > x que aún no tengan color.
- Lo mismo para todo nodo azul pero para elementos y < x
- En ambos casos pintamos de rojo o azul y.
- Repetimos el proceso.
- Aristas pintadas corresponden a las comparaciones cruciales
- Si grafo pintado no resulta conexo, no se puede conocer la mediana.
- Se necesitan n-1 comparaciones cruciales
- (n-1)/2 comparaciones no cruciales
- Modelo para comparaciones no cruciales:
	- a cardinal de elementos que nunca han sido comparados
	- b elementos comparados alguna vez y se les asignó un valor mayor a z
	- c comparados alguna vez y asignado menor a z
- A con A: uno mayor y otro menor
- A con B:  A menor a z
- A con C: A mayor a z
- B con C: según valores ya asignados
- Cuando B(o C) llegan a (n-1)/2  adversario le asignara todo el resto a C.
- Como partimos de (n, 0, 0), son necesarias (n-1)/2 comparaciones
3(n-1)/2 comparaciones


## Teoría de la información

Estudia cantidad mínima de bits para representar un mensaje u objeto.
	Considerar numero de posibles resultados en comparación para obtener la base, y las posibles entradas de la busqueda para obtener el argumento.

Aproximación de Stirling:
![[Pasted image 20250907135816.png]]

Aplica exclusivamente a algoritmos que deban proceder por **comparaciones**.

Establece cotas inferiores tanto de **peor** caso como de caso **promedio**.

Cota inferior > Mejor cota para el mejor algoritmo posible

Asintóticamente: Cuando variables crecen mucho, me interesa cómo se comporta la función en ese límite, ignorando detalles pequeños o constantes.

- O(f(n)) = “a lo más del orden de f(n)” → cota superior.
    
- Ω(f(n)) = “al menos del orden de f(n)” → cota inferior.
    
- Θ(f(n)) = “exactamente del orden de f(n)” → ajustada.
    
- o(f(n)) = “estrictamente más pequeño que f(n)” → crece más lento.

### Cotas de caso promedio

Entropía del conjunto de probabilidades.
	![[Pasted image 20250906191545.png]]
	Ningún compresor puede, en promedio, utilizar menos que esto de bits para codificar un elemento de U.

Si la probabilidad de cada elemento de U es uniformemente distribuida, se obtiene que la entropía es log2(|U|), llegando a su valor máximo.

Como esto coincide con el valor del peor caso, cota ingerior de peor caso de un algoritmo también es la cota ingerior de caso promedio si los inputs se presentan con la misma probabilidad.

Si ciertos elementos se buscan con mayor probabilidad que otros, entonces podemos romper la cota de log2(n) comparaciones en promedio, y llegar a la entropía H.

### Árboles de búsqueda óptimos

La idea es buscar un árbol de búsqueda  de profundidad promedio H.

#### Algoritmo de Huffman
Encontrar árbol binario que minimice la suma de las probabilidades p_i por la profundidad de correspondiente l_i.

Estrategia:
1. Crear bosque con n árboles, cada uno consistente en un único nodo (u_i) de peso w=p_i.
2. Tomar los dos árboles T_1 y T_2 de menor peso (w1, w2) y colocarlos como hijos izquierdo y derecho de un nuevo nodo.
3. Sacar T_1 y T_2 del bosque y agregar el nuevo árbol, con peso w1+w2
4. Volver al punto 2 hasta que quede solo un árbol

Sin embargo, desordena las hojas, por lo cual no necesariamente entrega un árbol de búsqueda.

#### Algoritmo de Hu-Tacker

H+2 comparaciones, la más ajustada posible hasta el momento.

Costo promedio de busqueda de 2(1-2epsilon)+3epsilon.

Demasiado complicado para verlo.

#### Construcción algoritmo más costoso
*Suma telescópica*: Serie donde la mayoría de los términos se cancelan entre sí en las sumas parciales, de modo que la suma final solo conseva el primer y último elemento.

Complicao (revisar de nuevo de ser necesario).

## Reducciones

Encontrar solución a un problema desconocido mediante *reducirlo* a uno conocido. al revés? conocido a desconocido

Queremos establecer cota inferior de P
Conocemos Q y su cota inferior
Si podemos transformar un input de Q en uno de P en tiempo o(C(n))
Resolver P en el input transformado
Transformar el output de P en el de Q, también en tiempo O(C(n))
Entonces cota inferior de Q también es cota inferior de P.
De no ser así, las transformaciones nos darían una solución a Q con una cota inferior mejor, lo que es imposible.

Para **peor caso** y **caso promedio**. Generalmente, para establecer órdenes de magnitud y no exactas.

### Cápsula convexa

Dados n puntos en el plano, encontrar el menor polígono convexo que los contiene.

Vértices polígonos son puntos del input. Por lo cual, output se pide en la forma de la secuencia de puntos que se obtiene al recorrer el perímetro del polígono en sentido antihorario, partiendo desde algún punto.

Reducir problema de orden al de la cápsula convexa.

Ordenar A={a1, ..., an}
Calculamos n puntos {(a1, a1^2), ..., (an, an^2)}
	Puntos distribuidos en parábola. Todos formarán parte de capsula convexa.
Listado en sentido antihorario que parta del mínimo en sus primeras coordenadas, se obtiene conjunto X en orden de menor a mayor.

### Colas de prioridad
*heap* obtiene tiempos O(logn) para las operaciones de insertar y extraer el mínimo en una cola de prioridad. 

### 3SUM y puntos coliniales

Cotas inferiores que están en función de otras cotas inferiores que no son conocidas, pero sí muy estudiadas.

Multiplicación de matrices -> Estudiado
Si podemos reducir la multiplicacion (estudiado) a un cierto problema P (desconocido). 
Si podemos resolver P en menor tiempo, habremos encontrado un algoritmo para multiplicar matrices mejor que todos los conocidos, se dice entonces que P es multiplicación-de-matrices-hard. Cuán improbable se considera obtener un mejor resultado para resolver P.

3SUM: dado n numeros reales, encontrar tres que sumen cero (pueden repetirse numeros en la suma).

Ordenamos n en nlogn, luego tomaremos cada zi y buscaremos dos que sumen -zi. 
Progresaremos desde las dos puntas m<-z1 y M<-zn.
Si m+M+zi<0 avanza m.
Caso contrario, disminuye M.
En tiempo O(n) encontramos m y M adecuados, o los cursores se cruzan y debemos considerar otro numero zi. El tiempo total es O(n^2). 
Problema bastante estudiado.

Dados n puntos (xi, yi) encontrar tres puntos colineales, que no estén en una línea vertical. Esto último se pone por conveniencia para demostrar cota inferior.

Reduciremos 3SUM a este problema.

Dado n numeros (z1 a zn), generaremos 3 puntos para cada zi: (1, zi), (2, -zi/2) y (3,zi). Veremos que este conjunto tiene 3 puntos colineales no en vertical sii Z tiene 3 numeros que suman 0.

Dado los xi, estos 3 puntos son 1,a 2,b 3,c con b=(a+c)/2, como a zi, b es algun zj y c algun zk tal q (zi+zk)/2=-zj/2, por lo que zi+zj+zk=0. Como la conversión cuesta sólo O(n), problema es 3SUM-hard.

# Memoria Externa

## Modelo
Discos mágneticos divididos en pistas (anillos) y sectores (entre radios de círculo consecutivo). Intersección es un bloque o página.

Algunos discos varios platos que giran simultáneamente > Unión mismo bloque se trata como único.

Disco escribe a través de cabezal. Se mueve a la pista correcta (seek). Espera que el sector pase girando por debajo (tiempo de latencia). 
Si se leen bloques contiguos, no se vuelve a pagar tiempo de seek ni latencia. Para pistas contiguas lo mismo, solo tiempo mínimo adicional.

Mejor acceso secuencial que aleatorio.
SSD ambos accesos es lo mismo.

Bloques de tamaño B.
Se leen y escriben bloques completos. (I/Os)
Operaciones RAM y CPU despreciables.
**No se considera diferencia de leer bloques consecutivos o aleatorios.**
Memoria RAM de tamaño M. m=M/B en bloques.
Input tamaño N. En disco en forma contigua ocupando n=N/B bloques.
Lectura secuencial O(n). Acceso aleatorio O(N)

Buscar en conjuntos ordenados (Árboles) y sin orden (Hashing), para colas de prioridad y algoritmos de ordenamiento.

## Árboles B

Nodo se almacena en un bloque > Ensancha el nodo a tamaño B.

Nodos internos almacena (B-1)/2 elementos(claves), (B-1)/2 claves y (B-1)/2 +1 punteros.

k claves necesita k+1 punteros.

Claves replicadas en hojas (Árbol B+).
Hojas pueden almacenar hasta B elementos, pero suelen almacenar B/2 para poder incorporar puntero a datos asociados a cada clave.

Diremos que bloques tienen capacidad de almacenar hasta B claves tanto en nodo interno como en hoja.

Todas las hojas del árbol B están al mismo nivel, por lo que su altura es O(logB(N))

Busqueda:
Se lee el nodo raíz con sus claves, si esta entre yi y yi+1, busqueda continua en subarbol Ti. La busqueda requiere leer entonces O(logB(N)) páginas de disco.

Inserción:
Comienza con búsqueda, identificando hoja donde deberia estar.
Se agrega a la hoja
Si se pasa se corta en dos hojas y la mediana de las claves se inserta en el Padre.
Si ocurre en la raíz, se crea una nueva raíz con solo dos hijos y altura crece en 1.

Borrado:
Elimina elemento de hoja.
Si pasa a tener menos de B/2 elementos, se une con su anterior o siguiente hermana y la clave que las separa en el padre se elimina y baja.
Si se llega a la raíz y esta queda con 0 elementos, se elimina y el hijo pasa a ser la raíz, el arbol pierde altura.

Si al unir con su hermano, queda un nodo con mas de B elementos.
Se vuelve a cortar el nodo por su mediana.

Tanto inserción como borrado cuestan O(logB(N)) operaciones de I/O.

Si mantenemos los primeros O(logB(M)) niveles en memoria principal, la cantidad de I/Os se reduce a O(logB(N/M))

### Cota inferior

El costo logB(N/M) es óptimo si se busca mediante comparaciones.

Método del adversario: 
Partimos con M+1 zonas de N/(M+1) tamaño.
Algoritmo lee un bloque de B elementos de disco, lee hasta B nuevas claves con las que comparar.
Luego siguen con los B+1 subrangos, uno de los cuales pasa a ser el nuevo rango de busqueda.
Adversario escoge siempre el mayor de los rangos, de modo que el rango se reduce en un factor de a lo más B+1. Necesita leer al menos LogB+1(N/(M+1)) páginas de disco para reducir el tamaño a 1 y responder correctamente.

## Ordenamiento
Basado en MergeSort, dividir en 2 hasta que rango sea 1.
Detener recursion cuando subarreglos son de tamaño B.
Vuelta de recursión, unión de ambos subarreglos(de tamaño B).
Uniones de un nivel del árbol requieren leer el arreglo completo y reescribirlo, a costo O(N/B)=O(n). Cantidad de niveles log2(B) (hasta que llegan a tamaño B).
Esta variante requiere O((N/B) log(N/B))=O(nlogn)
Mejorar deteniendo recursion cuando subarreglo es de tamaño M. (O(nlog(n/m))) restar al anterior lo que cuesta en RAM.

Mejorar aun mas si se divide por más, sin exceder el tamaño de M/B - 1, para no exceder tamaño B del buffer de cada elemento que se une. Ahora costo es O(N/Blog(N/M)) = O(nlog(n/m)).

En la práctica solo aridad de decenas, puesto que si no aumenta mucho el costo del seek.

### Cota inferior
Procederemos por estrategia del adversario.
Estado inicial: S = N!
Estado final: S=1

Al leer B estos puedes venir en B! formas.
Si ya se habian leído B, se pueden guardar otros M-B en memoria principal,  que se insertan como M sobre B. En total, el algoritmo determina la configuracion correcta entre las M sobre B \* B! que eran posibles antes de leer el bloque.
Cada una de las S permutaciones que aún son posibles son compatibles con solo una de estas configuraciones. Por lo que se puede particionar S en M sobre B \* B! subconjuntos.
El adversario tomará el mayor que debe ser de al menos S/(M sobre B \* B!). Por tanto el adversario puede encargarse de reducir S en un factor de este.

Si el algoritmo lee t bloques, a lo sumo se puede reducir el tamaño en N!/((M sobre B)^t \* (B!)^t).

La cantidad de lecturas del algoritmo debe ser t>= n, pues debe leer todo el input. Donde solo las primeras n  son de bloques nunca vistos, entonces en realidad B! es elevado a n, no t.

Calculando t, nos da que es >= a nlogm(n)
Por tanto, todo algoritmo que ordene en memoria externa por comparaciones requiere nlogm(n) I/Os

## Colas de prioridad
Si eventos se pueden manejar en cola simple, es facil manejarlos en disco a un costo de O(1/B) por inserción y borrado. Si en cambio, deben ser procesador en algun orden, se necesita de cola de prioridad en disco.

Se puede demostrar reduciendo Ordenamiento a esto.

### Cola de prioridad limitada
Reserva de M/2 de RAM para la cola de prioridad H.
Mientras cola caiga en RAM, insertar en H gratis. (no necesitamos leer/escribir del disco).
Si H está llena, se ordena completamente (en memoria; gratis) y se almacena en archivo en disco F1, lo que requiere de M/2B escrituras.

Inmediatamente, creamos buffer F1 de tamaño B en memoria, donde leeremos su primer bloque. H quedará vacía.

El mínimo se extrae de elegir entre el primer elemento del primer bloque de F1 y el mínimo de H. Una vez leímos todo el buffer de F1, lo volvemos a llenar leyendo el siguiente bloque de B elementos.

H sigue leyendo por lo que se pueden crear hasta Fk archivos. 

Luego para extraer el mínimo se requerirá una cola de prioridad (de k+1(k primeros elementos y el de H)) que mantenga los primeros elementos de cada Fi, y los reemplaza por el siguiente de su buffer cuando éstos son extraídos.

Como tenemos M/2 de memoria para los buffers, tenemos límite de k<=M/2B. Por lo cual se tiene un límite de O(M^2/B) elementos que pueden ser insertados.

Cada vez que un elemento pasa por el proceso desde inserción hasta extracción, tiene un costo de 1/B escrituras cuando se pasa al archivo. Luego puede ser leído de este archivo cobrandole 1/B lecturas. 

Muchas operaciones son gratis, entonces, solo se provoca un costo de O(M/B) para escribir un archivo.

Ordenar en O(N/B) siempre que N=O(M^2/B)

### Cola de prioridad general
Extensión ante no poder usar toda la RAM, mediante una secuencia creciente de *grupos* de archivos.

Se crean lo k archivos pero del grupo 1. Cuando se cree el k+1, se uniran todos en uno nuevo F1 del grupo 2, de tamaño máximo k*(M/2), asi sucesivamente, por ejemplo el grupo 3 será de tamaño k^2*(M/2)

Cada unión de archivos del grupo i cuesta O(tamaño del proximo grupo / B) = O(k^i/m), es decir O(1/B) por elemento unido. Si se construyen r grupos, el costo amortizado de una operacion es O(r/B) pues un elemento insertado puede ser escrito y luego unido r-1 veces, y finalmente leído.

Para poder crear el primer elemento del grupo r, debemos hacer insertado N= Sumatoria de i=0 hasta i=r-1 de k^i\*(M/2) = Oexacto(K^r\*M).

M/2 es el tamaño de los archivos.

#### Grupos:
Numero de grupos que podemos producir: r = logk((N/M))

#### Buffers y restricciones:
K\*r buffers, por lo que necesitamos M/2 > krB, por tanto, estamos limitados a 2kr<=m.

No más buffers de los que cae en RAM.

#### Como elegir k:

Para tener tiempo óptimo necesitamos r=O(logm(n/m)), es decir, logk=Oexacto(logm). Entonces podemos elegir k=Oexacto(m^alpha) para algún 0<alpha<1 cte.

Dada la limitación, debe cumplirse que m^alpha \* logm(n)=O(m), es decir, logn=O(m^(1-alpha)\* logm).

## Hashing
Buscar haciendo O(1) accesos al disco en promedio.
Tabla normal de hashing requiere conocer de antemano la cantidad de elementos que se almacenará, o bien, incrementar periódicamente el tamaño de tabla.
### Hashing Extendible
Funciona cuando se almacena N=O(MB) datos en total.

En memoria se genera un árbol trie.
Con k-1 nodos y k hojas, donde cada hoja almacena datos en una página de disco.

Búsqueda de una clave x parten por calcular h(x) y usan sus bits para recorrer el trie.

No hay ocupación mínima garantizada. No se puede garantizar que los nodos del trie es O(k)=O(N/B).

En promedio si h(y) es aleatorio las páginas estarán llenas a un 69%.

S