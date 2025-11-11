#programming_languages
#other
# Tabla de Contenidos

>[[#Capítulo 1]]
 >	- *statement* y comentarios
 >	- *variables*: inicialización y comportamiento indefinido
 >	- Identificadores
 >	- `iostream`: `cin` y `cout`
 >	- Literal, operador y expresiones
>[[#Capítulo 2]]
 >	- Funciones
 >	- Parámetros y scope
 >	- Declaración y definición
 >	- Separación en archivos: `.cpp` y `.h`
 >	- `namespaces` y `#pragma once`
>[[#Capítulo 3]]
 >	- Tipos de errores
 >	- Depuración básica
 >	- Depurador
 >	- Prevensiones
>[[#Capítulo 4]]
 >	- Tipos de datos y `sizeof()`
 >	- Enteros
 >	- Decimales
 >	- Lógica y texto
 >	- `if statements` y conversión de tipos
>[[#Capítulo 5]]
 >	- `const`
 >	- `constexpr`
 >	- `std::string`
 >	- `std::string_view`
>[[#Capítulo 6]]
 >	- Aritmética, precedencia, `std::pow()` y `<cmath>`
 >	- (de/in)cremento
 >	- Operadores de lógica
 >	- Operador ternario
>[[#Capítulo O]]
 >	- `std::bitset` y manipulación de bits
 >	- Operadores sobre bits
 >	- Máscara de bits
>[[#Capítulo 7]]
 >	- Scope, shadowing y namespaces
 >	- Duration; `static`
 >	- Linkage y `extern`
 >	- `inline` y `using`
>[[#Capítulo 8]]
 >	- `if` y `switch`
 >	- `while`, `do-while` y `for`
 >	- `break`, `continue` y `std::exit()`
 >	- random
>[[#Capítulo 9]]
 >	- Testing y Cobertura
 >	- Estrategia de Errores
 >	- Manejo de errores en `std::cin`
 >	- `assert` y `static_assert`
>[[#Capítulo 10]]
 >	- Promoción y Estrechamiento
 >	- Inicialización de Lista `{}`
 >	- `static_cast<TIPO_NUEVO>(variable)`
 >	- `using` y `auto`
>[[#Capítulo 11]]
 >	- Overloading
 >	- Templates
 >	- Templates (Múltiples tipos y No-Tipo)
 >	- Templates y archivos
>[[#Capítulo F]]
 >	- funciones `constexpr`
 >	- funciones `consteval`
 >	- `constexpr` vs. `consteval`
>[[#Capítulo 12]]
 >	- `lvalue` y `rvalue`
 >	- Referencias `lvalue`: `&`
 >	- Punteros `*` y `nullptr`
 >	- Dangling reference y `std::optional`
>[[#Capítulo 13]]
 >	- `enum class`
 >	- `struct`
 >	- Plantillas de `struct`
>[[#Capítulo 14]]
 >	- OOP
 >	- Constructores
 >	- Seguridad con `const`
 >	- Clases en tiempo de compilación
>[[#Capítulo 15]]
 >	- `this` y destructor
 >	- Organización en `.h` y en `.cpp`
 >	- Miembros `static`
 >	- `friend` y clases anidadas
>[[#Capítulo 16]]
 >	- `std::vector`
 >	- Crecer y decrecer
 >	- `for-each`
 >	- `&` en vectores
>[[#Capítulo 17]]
 >	- `std::array`
 >	- Array C-style
 >	- Decay

# Capítulo 1
### 1. El Esqueleto del Programa

- Todo programa de C++ se ejecuta comenzando por la función **`int main()`**.
- El "cuerpo" de una función está delimitado por llaves **`{ }`**.
- Una **declaración** (_statement_) es una instrucción individual y casi siempre termina con un punto y coma **`;`**.
- Los **comentarios** son notas para humanos que el compilador ignora. Hay dos tipos: `//` (una línea) y `/* ... */` (multilínea).

---

### 2. Variables (Guardando Datos)

- Una **variable** es un "cajón" con nombre para almacenar datos (ej: `int edad`).
- **Inicialización**: Es dar un valor a una variable _en el momento de crearla_. La forma moderna preferida es con llaves (ej: `int edad {30};`).
- **Asignación**: Es dar un valor a una variable _después_ de que ya ha sido creada, usando el operador `=` (ej: `edad = 31;`).
- **Comportamiento Indefinido**: Es el "monstruo" 👻 de C++. Ocurre si usas una variable que has declarado pero _nunca_ has inicializado. Contendrá un valor "basura" aleatorio y tu programa será impredecible. **¡Inicializa siempre tus variables!**

---

### 3. Reglas del Lenguaje

- **Identificadores**: Son los nombres que das a tus variables (ej: `edad`, `puntuacion_total`).
    - Son **sensibles a mayúsculas** (`edad` no es lo mismo que `Edad`).
    - No pueden empezar con números ni contener espacios (solo letras, números y `_`).
- **Keywords**: Son palabras reservadas (ej: `int`, `return`, `void`) que no puedes usar como nombres de variables.
- **Whitespace** (espacios, `TAB`, saltos de línea): El compilador (casi) los ignora. Se usan para formatear el código y hacerlo **legible para los humanos**.

---

### 4. Interactuando con el Programa

- Para poder usar la entrada y salida, debes incluir la biblioteca de flujos: **`#include <iostream>`**.
- **`std::cout`**: Se usa para **imprimir** en la pantalla (salida). Usa el operador de inserción `<<` (ej: `std::cout << "Hola";`).
- **`std::cin`**: Se usa para **leer** desde el teclado (entrada). Usa el operador de extracción `>>` (ej: `std::cin >> edad;`).
- **Saltos de línea**: `\n` (recomendado) y `std::endl` (que también vacía el búfer).

---
### 5. Expresiones y Operadores

- **Literal**: Es un valor fijo escrito en el código (ej: `5` o `"Hola"`).
- **Operador**: Es un símbolo que realiza una acción (ej: `+`, `-`, `*`, `/` para aritmética, o `<<`, `>>`, `=` que ya vimos).
- **Expresión**: Es cualquier trozo de código que **produce un valor** (ej: `5`, `edad`, o `5 + edad`).

---

A
# Capítulo 2

### 1. ¿Qué son las Funciones?

- Son **bloques de código reutilizables** (mini-recetas) que realizan una tarea específica (como `sumar` o `saludar`).
- Hacen el código más **legible** y fácil de mantener (principio **DRY**: "No te repitas").
- Hay dos tipos principales:
    - **Funciones `void`**: _Hacen_ algo (ej: `imprimirBienvenida()`) pero **no devuelven** un valor.
    - **Funciones con retorno de valor**: _Calculan_ algo y **devuelven** un resultado usando la palabra clave `return` (ej: `int sumar(...)`).

---
### 2. Parámetros y Scope

- **Parámetros** (ej: `int a, int b`): Son los "ingredientes" que una función necesita para trabajar. Se definen en la función.
- **Argumentos** (ej: `sumar(10, 20)`): Son los valores _reales_ que le pasas a la función cuando la llamas.
- **Scope Local**: Las variables creadas _dentro_ de una función (incluyendo sus parámetros) **nacen y mueren** dentro de esa función. Son invisibles para `main` y otras funciones.

---

### 3. Declaraciones vs. Definiciones

- **Definición**: Es el código completo de la función, con su cuerpo `{...}`.
- **Declaración (o "Promesa")**: Es solo la "firma" de la función (ej: `int sumar(int a, int b);`). Le dice al compilador que la función existe, aunque esté definida más abajo. Es vital para organizar el código.

---

### 4. Separación en Archivos

- ¡No pongas todo en `main.cpp`!
- **Archivos `.cpp` (Fuente)**: Contienen las _definiciones_ (el "cómo"). Es el código de trabajo.
- **Archivos `.h` (Cabecera/Header)**: Contienen las _declaraciones_ (las "promesas"). Son el "menú" que le dices a otros archivos qué funciones están disponibles.
- **`#include`**: Es la directiva del **preprocesador** que "copia y pega" el contenido de un archivo `.h` en tu archivo `.cpp` antes de compilar.

---

### 5. Namespaces y Header Guards

- **Namespaces (ej: `std::`)**: Son "apellidos" que le ponemos a nuestras funciones (ej: `Matematicas::sumar`) para evitar **colisiones de nombres** cuando dos funciones se llaman igual.
- **`#pragma once`**: Es un **Header Guard**. Se pone al inicio de _cada_ archivo `.h` para evitar que el preprocesador lo incluya dos veces por error, lo cual causaría un error de compilación.

---

# Capítulo 3

### 1. Conoce a tu Enemigo: Tipos de Errores

- **Errores de Sintaxis:** Son errores "gramaticales" (como olvidar un `;` o escribir mal `retun`). Tu código **no compila**. Son los "fáciles" porque el compilador te avisa dónde está el problema.
- **Errores Semánticos (de Lógica):** Tu código compila perfectamente, pero **hace lo incorrecto** (ej. sumas cuando querías restar, o calculas un promedio dividiendo por 3 en vez de por 2). Estos son los _bugs_ difíciles y el objetivo principal de la depuración.

---

### 2. Tácticas de Detective "Manuales"

Antes de usar herramientas complejas, usamos nuestro cerebro y técnicas simples:

- **El Proceso Mental:** 1. Reproduce el error, 2. Formula una hipótesis (ej. "creo que `b` es cero"), 3. Prueba la hipótesis, 4. Arréglalo y verifica.
- **Depuración con `std::cout`**: La técnica clásica. Pones "micrófonos" (`cout << "DEBUG: b = " << b;`) en tu código para imprimir los valores de tus variables y ver dónde se tuercen.
- **Aislar el Problema**: Usar `/* ... */` para "apagar" bloques de código. Si el error desaparece, el culpable está en el bloque que comentaste.

---

### 3. La Herramienta Profesional: El Depurador Integrado 🕵️‍♂️

Esta es la herramienta más potente de tu IDE (Visual Studio, VS Code, etc.). Te permite **pausar** tu programa en mitad de la ejecución y espiarlo "a cámara lenta".

- **Breakpoints (Puntos de Interrupción)**: Pones una señal de "STOP" 🛑 en una línea de código. El programa se ejecutará y se **congelará** justo antes de esa línea.
- **Stepping (Paso a Paso)**: Una vez congelado, usas `F10 (Step Over)` para avanzar línea por línea, viendo exactamente qué hace el programa.
- **Ventanas "Watch" (Inspección)**: Mientras avanzas "paso a paso", puedes ver cómo los **valores de tus variables cambian en tiempo real**. Aquí es donde "ves" el bug (ej. ves que `b` se convierte en `0`).
- **Call Stack (Pila de Llamadas)**: Es el "rastro de migas de pan" 🍞. Te muestra el historial de funciones (ej. `main()` llamó a `funcionA()` que llamó a `funcionB()`), para que sepas _cómo_ llegaste al código problemático.

---

### 4. Medicina Preventiva 🩺

La mejor forma de depurar es escribir código que sea difícil de romper.

- **¡Inicializa siempre tus variables!** (ej. `int x {0};` en lugar de `int x;`). Esto elimina los errores de "basura aleatoria".
- **Escribe código defensivo**: Desconfía de la entrada del usuario. Comprueba si un divisor es `0` _antes_ de intentar dividir.
- **Mantén tus funciones cortas** y que hagan una sola cosa. Es más fácil depurar una función de 5 líneas que una de 50.

---

# Capítulo 4

### 1. Qué es un Tipo (y cuánto ocupa)

- Un **tipo de dato** le dice al compilador qué tipo de valor guardar (`int`, `double`, `bool`, `char`...) y cuánta memoria reservar.
- Usamos el operador **`sizeof(tipo)`** para preguntar cuántos **bytes** ocupa un tipo en la memoria (ej. `sizeof(int)` suele ser 4).
- **`void`** es el "anti-tipo": significa "sin valor" y se usa para funciones que no devuelven nada.

---

### 2. La Familia de los Enteros (Números sin decimal)

- **`int`** es el tipo por defecto para números con signo (positivos y negativos).
- También existen `short` (más pequeño) y `long long` (más grande).
- **¡Peligro `unsigned`!** Los tipos `unsigned` (ej. `unsigned int`) solo guardan positivos. Son peligrosos porque si intentas restar y el resultado es negativo, sufren **subdesbordamiento** (_underflow_) y dan un número gigante (¡como viste en el cuestionario!). **Recomendación: Evitarlos.**
- **Forma Moderna:** Los enteros de ancho fijo (ej. **`std::int32_t`**) de `<cstdint>` te garantizan _exactamente_ cuántos bits ocupan (ej. 32 bits = 4 bytes), haciendo tu código más portable.

---
### 3. La Familia de los Decimales (Punto Flotante)

- **`float`**: 4 bytes, rápido, pero menos preciso (unas 7 cifras). Literal: `3.14f`.
- **`double`**: 8 bytes, más lento, pero mucho más preciso (unas 15 cifras). Es el **tipo por defecto** para decimales.
- **¡Peligro de Precisión!** Los `double` y `float` son **imprecisos** por naturaleza. Nunca pueden representar perfectamente algunos decimales (como `0.1`).
- **Regla de Oro:** **Nunca compares dos `double` con `==`**. (¡Como viste en el cuestionario!).

---

### 4. Lógica y Texto

- **`bool`**: El tipo más simple. Solo puede ser **`true`** o **`false`**. Es el combustible de la lógica. (Cuando se imprime, `true` es `1` y `false` es `0`).
- **`char`**: Guarda un **único carácter** (letra, número o símbolo). Usa **comillas simples** (ej. `'A'`, `'!'`, `'5'`). Internamente, es solo un `int` de 1 byte que se interpreta según la tabla **ASCII**.

---

### 5. Uso y Mezcla (¡Lo más importante!)

- **`if statements`**: ¡Tu primera herramienta de lógica! `if (condición)` ejecuta el código en `{...}` solo si la `condición` es `true`.
- **Conversión de Tipos**:
    - **El Bug:** La **división de enteros**. Si divides dos `int` (ej. `5 / 2`), C++ corta los decimales. El resultado es `2`, no `2.5`.
    - **La Solución:** La conversión explícita. Le decimos al compilador que trate un número como `double` _antes_ de la división.
    - **Forma Correcta:** **`static_cast<double>(variable)`**. (Ej: `double prom = static_cast<double>(5) / 2;` // da `2.5`).

---

# Capítulo 5

### 1. Constantes (`const`)

- **Evita los "Números Mágicos"**: No escribas `3.14159` en tu código. Es difícil de leer y de mantener.
- **Usa `const`**: Es el "candado" 🔒 para variables. `const double PI {3.14159};` le da un nombre (legibilidad) y se asegura de que **nunca cambie** (seguridad y mantenimiento).
- **`const` es una promesa de "solo lectura"** que se aplica una vez que la variable se inicializa (lo cual puede ocurrir en tiempo de ejecución, ej: `const int edad { variable_de_cin };`).

---

### 2. Constantes de Compilación (`constexpr`)

- **`constexpr`** es un "súper-candado" 🚀. Es una promesa más fuerte: el valor **debe** ser conocido en **tiempo de compilación** (antes de que el programa se ejecute).
- **Optimización**: `constexpr int SEGUNDOS_POR_DIA {60*60*24};` se calcula **UNA VEZ** por el compilador (en la "fábrica") y se "hornea" el resultado (`86400`) en el programa. El usuario final nunca tiene que calcularlo.
- **Regla Moderna:** Usa `constexpr` siempre que el valor pueda ser conocido en la compilación; usa `const` para todo lo demás que no deba cambiar.

---

### 3. Texto con `std::string`

- ¡La forma moderna de manejar texto! (Olvídate de `char` sueltos).
- Tienes que incluir el header: **`#include <string>`**.
- Es un "contenedor" que maneja toda la memoria por ti.
- Puedes **unir (concatenar) strings** con el operador **`+`**.
- Puedes leer texto del usuario con `std::cin >> mi_string;` (lee hasta el primer espacio) o **`std::getline(std::cin, mi_string);`** (lee la línea completa).

---

### 4. Vistas de Texto con `std::string_view`

- Tienes que incluir el header: **`#include <string_view>`**.
- **No es un string**. Es un "visor" o "tarjeta de biblioteca" 💳 súper ligero que **solo mira** a un `std::string` que ya existe.
- **Optimización Clave**: Pasa `std::string_view` a tus funciones para **evitar copias lentas**. Es ideal para parámetros de función que solo necesitan _leer_ el texto.
- **Regla Moderna:** Pasa `std::string_view` por defecto; solo pasa `std::string` si la función necesita _modificar_ o _guardar_ el texto.

---


# Capítulo 6
### 1. Aritmética y Precedencia

- **Precedencia:** Es el "orden de operaciones". C++ hace la multiplicación (`*`), división (`/`) y módulo (`%`) **antes** que la suma (`+`) y la resta (`-`).
- **Paréntesis `( )`:** Son tus mejores amigos. Tienen la precedencia más alta. **Usa siempre paréntesis** para que tu código sea claro y no tengas que memorizar el orden de las operaciones.
- **División de Enteros:** ¡Cuidado! Cuando divides dos `int`, C++ **corta los decimales**. `7 / 2` da como resultado `3`.
- **Operador Módulo (`%`):** Es el **resto** de una división de enteros. `7 % 3` es `1`. Su uso más común es saber si un número es par: `if (numero % 2 == 0)`.
- **Potencias:** C++ **NO** usa el símbolo `^` para potencias (¡ese es un operador binario!). Para potencias, usa `std::pow()` (de `<cmath>`) o multiplica a mano (ej. `x * x`).

---

### 2. Incremento y Efectos Secundarios (¡Peligro!)

- **`++x` (Pre-incremento):** Primero incrementa `x` en 1, y luego la expresión evalúa al _nuevo_ valor.
- **`x++` (Post-incremento):** Primero, la expresión evalúa al valor _original_ de `x`, y _después_ incrementa `x` en 1.
- **Efecto Secundario:** Es cuando un operador modifica el estado (ej. cambia el valor de una variable). `++` y `--` tienen efectos secundarios.
- **Regla VITAL (Comportamiento Indefinido 👻):** **Nunca** uses una variable que estás incrementando/decrementando más de una vez en la misma declaración (ej. `y = ++x + x;`). El orden es indefinido y tu programa será impredecible. ¡Sepáralo siempre en líneas distintas!

---

### 3. Lógica (Comparación y Conexión)

- **Operadores Relacionales:** Son las "preguntas". Devuelven `true` o `false`.
    - `==` (Igual a)
    - `!=` (No igual a / Distinto)
    - `<`, `>`, `<=`, `>=`
- **Peligro `double`:** **Nunca** uses `==` o `!=` para comparar `double` o `float`. Debido a la imprecisión decimal (ej. `0.1 + 0.1 + 0.1` no es `0.3`), estas comparaciones casi siempre fallan.
- **Operadores Lógicos:** Combinan múltiples `bool`s.
    - **`&&` (Y / AND):** `true` solo si **ambos** lados son `true`.
    - **`||` (O / OR):** `true` si **al menos uno** de los lados es `true`.
    - **`!` (NO / NOT):** Invierte el valor (`!true` es `false`).

---

### 4. El "Mini-If" (Operador Condicional)

- Es un atajo para un `if-else` simple que asigna un valor.
- Sintaxis: `(condición) ? (valor_si_true) : (valor_si_false)`.
- Ejemplo: `std::string tipo = (edad >= 18) ? "Adulto" : "Menor";`.
- **Uso:** Genial para asignaciones simples, pero no lo uses para lógica compleja (ahí usa un `if-else` normal por claridad).

---

# Capítulo O

### 1. El Camino Fácil: `std::bitset`

- Es la forma **moderna, fácil y segura** de manejar bits. (Necesitas `#include <bitset>`).
- Piensa en él como un "panel de interruptores" 💡 de tamaño fijo (ej. `std::bitset<8>`).
- Te da métodos claros para manipularlos:
    - `.set(n)`: Enciende el bit `n`.
    - `.reset(n)`: Apaga el bit `n`.
    - `.flip(n)`: Invierte el bit `n`.
    - **`.test(n)`**: Comprueba si el bit `n` está encendido (devuelve `true`/`false`).
- **Uso principal:** Para **"banderas"** (`bit flags`), es decir, guardar muchas opciones SÍ/NO (como `bool`s) en muy poco espacio.

---

### 2. Binario y Operadores "Raw"

- **Binario (Base 2):** Es el idioma de la computadora (0s y 1s). Cada columna es una potencia de 2 (..., 8, 4, 2, 1). `0b1010` es `8 + 2 = 10`.
- **Operadores Bitwise:** A diferencia de `&&` o `||` (que son para `bool`s), estos trabajan **directamente sobre los 0s y 1s** de los números:
    - **`&` (AND):** `1` solo si _ambos_ bits son `1`. (Útil para "apagar" o "comprobar").
    - **`|` (OR):** `1` si _al menos un_ bit es `1`. (Útil para "encender").
    - **`^` (XOR):** `1` solo si los bits son _diferentes_. (Útil para "invertir").
    - **`~` (NOT):** Invierte _todos_ los bits.
    - **`<<` (Shift Izq.):** Mueve los bits a la izquierda. `x << 1` es una forma rápida de **multiplicar por 2**.
    - **`>>` (Shift Der.):** Mueve los bits a la derecha. `x >> 1` es una forma rápida de **dividir por 2**.

---

### 3. El Camino Manual: Máscaras de Bits

- Es la técnica clásica para guardar "banderas" en un solo `int`.
- Se usa una **"máscara"** (un `int` con un `1` en la posición deseada, ej. `MASCARA = 1 << 3;`) para "apuntar" a un bit.
- **Encender un bit:** `opciones |= MASCARA;` (con `OR`)
- **Apagar un bit:** `opciones &= ~MASCARA;` (con `AND` y `NOT`)
- **Invertir un bit:** `opciones ^= MASCARA;` (con `XOR`)
- **Comprobar un bit:** `if ((opciones & MASCARA) != 0)` (con `AND` y `!=`)

---
# Capítulo 7

### 1. Scope (Ámbito): ¿Dónde es visible?

- **Bloque/Scope Local:** Es el espacio entre llaves `{...}`. Las variables declaradas aquí (**variables locales**) nacen y mueren dentro de este bloque. Son tus mejores amigas y debes usarlas siempre que puedas.
- **Scope Global:** Es el espacio _fuera_ de cualquier llave. Las variables globales son visibles en todo el archivo.
- **Shadowing (Ocultamiento):** Ocurre cuando una variable local "tapa" a una global con el mismo nombre. Es confuso y debes evitarlo.
- **Scope de Namespace:** Los `namespaces` (`std::`, `Matematicas::`) crean su propia "habitación" para evitar colisiones de nombres.

---
### 2. Duration (Duración): ¿Cuánto tiempo vive?

- **Duración Automática:** Es la de las variables locales. Se crean al entrar al bloque y se destruyen (mueren) al salir.
- **Duración Estática:** La variable vive durante **toda la ejecución del programa**. Esto aplica a:
    1. Variables Globales.
    2. Variables Locales `static` (¡La "Zombie" 🧟!).
- **`static` Local:** Es una variable local que **recuerda su valor** entre llamadas a la función. Es visible _solo_ dentro de su función, pero vive para siempre.

----
### 3. Linkage (Vinculación): ¿Qué otros archivos pueden verla?

- **Vinculación Externa (Pública):** Es el _defecto_ de las variables globales. El Enlazador permite que _otros_ archivos `.cpp` accedan a ella (usando `extern`).
- **Vinculación Interna (Privada):** La variable solo existe en su propio archivo `.cpp`.
    - _Forma Antigua:_ Usando `static` en una variable global (`static int g_privado;`).
    - _Forma Moderna:_ Poniéndola en un **namespace sin nombre** (`namespace { int g_privado; }`).

---
### 4. Buenas Prácticas (¡Lo más importante!)

- **¡Las Globales no-`const` son MALVADAS 👿!** Son la causa número 1 de _bugs_ difíciles de encontrar. ¡Evítalas siempre! Pasa valores usando parámetros de función.
- **`inline const`:** Es la forma **moderna (C++17)** de compartir constantes globales (que sí son buenas) en archivos `.h`.
- **`using namespace std;` es peligroso 👿:** "Contamina" tu scope global. Es mucho mejor ser explícito (`std::cout`) o, si debes, usar una declaración `using` _dentro_ de tu función (`using std::cout;`).

---

# Capítulo 8

### 1. Tomando Decisiones (`if` y `switch`)

- **Flujo de Control** es el orden en que se ejecutan las instrucciones. En lugar de ser solo de arriba hacia abajo, podemos "bifurcar" el camino.
- **`if`, `else if`, `else`** es la herramienta principal para tomar decisiones. Comprueba una condición (`bool`) y ejecuta un bloque `{...}` solo si es `true`.
- **¡Peligro!** El _bug_ más común es usar `=` (asignación) en lugar de `==` (comparación). `if (x = 10)` _siempre_ será `true` (y cambiará `x`).
- **`switch`** es una alternativa limpia a un `if` encadenado cuando comparas _una sola variable_ con múltiples valores enteros (ej. `case 1:`, `case 2:`).
- **`break`** es VITAL en un `switch`. Si lo olvidas, el código "cae" (_fallthrough_) y ejecuta los siguientes `case` por error.
- **`goto`** es una reliquia peligrosa. Te permite "saltar" a una etiqueta, pero crea "código espagueti" 🍝. Debes evitarlo.

---

### 2. Repitiendo Tareas (Bucles)

- **Bucles** nos permiten ejecutar un bloque de código múltiples veces.
- **`while (condicion)`**: El bucle básico. Comprueba la condición **antes** de cada vuelta. Si la condición es `false` al inicio, nunca se ejecuta.
- **`do-while`**: Una variante que comprueba la condición **después** de cada vuelta. Esto garantiza que el bloque se ejecute **al menos una vez**.
- **`for (init; cond; accion)`**: El bucle más común y organizado. `for (int i {0}; i < 5; ++i)` junta la inicialización, la condición y la acción de incremento en un solo lugar.
- **¡Peligro!** Si olvidas actualizar la variable de control (ej. olvidar `++i`), creas un **bucle infinito** ♾️.

---

### 3. Controlando el Flujo

- **`break`**: Es el "freno de emergencia". Se usa para **salir inmediatamente** del bucle (`for`/`while`) o `switch` más cercano.
- **`continue`**: Es el botón de "saltar". Termina la vuelta _actual_ del bucle y salta **directamente a la siguiente iteración**.
- **`std::exit()`**: Es el "botón rojo". Aborta el programa _entero_ inmediatamente.

`std::exit(1)` : 1 significa error.
`std::abort()`: cierra el programa de forma "anormal".

---

### 4. Números Aleatorios (Forma Moderna)

- **No uses `rand()`**. Es la forma "antigua" de C y es de baja calidad.
- Usa siempre la biblioteca moderna **`<random>`** de C++.
- El proceso requiere 3 pasos:
    1. **Semilla (Seed)**: `std::random_device` (para un inicio impredecible).
    2. **Motor (Engine)**: `std::mt19937` (el generador de la secuencia pseudoaleatoria).
    3. **Distribución (Distribution)**: `std::uniform_int_distribution<int>(min, max)` (para ajustar los números a tu rango, ej. 1 a 6 para un dado).

```C++
std::random_device rd;

std::mt19937 motor(rd());

std::uniform_int_distribution<int> distribucion(1, 6);

for (int i = 0; i < 5; ++i) 
{ 
std::cout << distribucion(motor) << " "; 
}
```

---

# Capítulo 9

### Testing y Cobertura

- **Probar (Testing) no es Depurar (Debugging):** Probar es el proceso _proactivo_ de verificar que tu código da el resultado correcto (control de calidad). Depurar es el proceso _reactivo_ de encontrar un _bug_ que ya sabes que existe.
- **Cobertura de Código (Code Coverage):** Es una métrica (%) que te dice qué cantidad de tu código (ej. qué ramas de un `if-else`) se ejecutaron durante tus pruebas. Te ayuda a encontrar "zonas oscuras" que nunca has probado.

---

### Estrategias de Errores

- **Errores Semánticos (de Lógica):** Son los _bugs_ que el compilador no ve (ej. `if (x = 10)` en lugar de `if (x == 10)`, o la división de enteros `5 / 2 = 2`).
- **Manejo de Errores:** Cuando detectas un error, tienes varias opciones:
    - **Detener el programa:** Con `std::exit()` o `std::abort()`. Se usa para errores fatales e irrecuperables (ej. no se encuentra un archivo vital).
    - **Reintentar:** Es la mejor opción para errores "recuperables", como una entrada de usuario incorrecta.

---

### El Villano: Validar `std::cin` (¡Clave!)

¡`std::cin` es frágil y se "rompe" fácilmente! Si le pides un `int` y el usuario escribe "hola", `std::cin` entra en un **estado de fallo** 🚩 y **deja la "basura" ("hola") en la tubería (el búfer)**.

Esto provoca bucles infinitos si no se maneja. La solución **robusta** siempre tiene 2 pasos:

1. **`std::cin.clear()`:** "Limpia la bandera" 🚩. Saca a `cin` de su estado de fallo para que acepte órdenes de nuevo.
2. **`std::cin.ignore(...)`:** "Vacía la tubería" 🪠. Descarta la entrada basura que se quedó atascada en el búfer, para que no la vuelva a leer en la siguiente vuelta del bucle.


```C++ 
// 1. si el 'cin' falló
if (std::cin.fail()) {
	// 2. Limpiar bandera fallida
	std::cin.clear();
	// 3. Ignoramos entrada basura:
	// 32767 caracteres o hasta un '\n'
	std::cin.ignore(std::numeric_limits<std::streamsize>::max(), '\n');
}
```

---

### Los Guardianes: `assert`

`assert` es una herramienta de depuración para **encontrar _tus_ errores**, no los del usuario.

- **`assert(condición);`** (de `<cassert>`): Es un "guardián" 💂 en tiempo de **ejecución**.
    - Le dices una condición que _sabes_ que debe ser `true` (ej. `assert(divisor != 0);`).
    - **En modo Debug:** Si la condición es `false`, el programa **crasha** 🛑 inmediatamente y te dice dónde falló tu lógica.
    - **En modo Release:** `assert` desaparece por completo (coste cero).
    
- **`static_assert(condición, "mensaje");`**: Es un "guardián" 🏭 en tiempo de **compilación**.
    - Comprueba si algo es `true` _antes_ de que el programa se cree (ej. `static_assert(sizeof(int) == 4);`).
    - Si es `false`, el programa **falla al compilar**, ahorrándote problemas en el futuro.

---

# Capítulo 10

### 1. Conversiones Implícitas (La "Magia" Automática)

C++ convierte tipos automáticamente para que las operaciones funcionen. Hay dos tipos:

- **Promoción (Buena):** Convertir un tipo "pequeño" a uno "grande" (ej. `int` $\to$ `double`) para _evitar_ perder datos. Esto ocurre en operaciones mixtas (ej. `5 + 3.14`).
- **Estrechamiento (Mala/Peligrosa ⚠️):** Convertir un tipo "grande" a uno "pequeño" (ej. `double` $\to$ `int`). Esto _pierde_ datos (ej. `3.14` se trunca a `3`).

---

### 2. ¡El Escudo `{}` al Rescate!

- La forma moderna de inicializar (`int x { 3.14 };`) **prohíbe las conversiones de estrechamiento**. Te da un **error de compilación**, salvándote de _bugs_ lógicos. ¡Úsala siempre!

---

### 3. Conversión Explícita (Tomar el Control)

- Cuando _sí_ queremos forzar una conversión (y decírselo al compilador), usamos **`static_cast`**.
- **Sintaxis:** `static_cast<TIPO_NUEVO>(variable)`
- **Uso Clave:** Arreglar la **división de enteros**.
    - `int {7} / int {2}` $\to$ `int {3}` (¡Mal!)
    - `static_cast<double>(7) / 2` $\to$ `double {3.5}` (¡Bien!)

---

### 4. C++ Moderno: `using` y `auto`

- **Alias de Tipo (`using`):** Nos permite crear "apodos" para tipos largos y hacer el código más legible.
    - `using entero_largo = std::int64_t;`
- **Deducción de Tipo (`auto`):** Le permite al compilador "deducir" el tipo de una variable basándose en su inicializador.
    - `auto x = 5;` (El compilador deduce `int`).
    - `auto y = 3.14;` (El compilador deduce `double`).
    - Es más corto, más limpio y a veces más correcto que escribir el tipo a mano.

---
# Capítulo 11

### 1. Sobrecarga de Funciones (La "Familia")

La **sobrecarga** (_overloading_) te permite crear **múltiples funciones con el mismo nombre**, siempre que tengan **parámetros distintos**.

- **Diferenciación:** C++ distingue las funciones sobrecargadas basándose en el **número** o **tipo** de sus parámetros (ej. `imprimir(int)` es distinta de `imprimir(double)`).
    - El _tipo de retorno_ (`void`, `int`, etc.) **no** se usa para diferenciar.
- **Resolución:** Cuando llamas a `imprimir(5.0)`, C++ busca la "mejor" coincidencia. Primero busca una coincidencia exacta (`imprimir(double)`), luego una por promoción (`imprimir(long double)`), y luego una por conversión (`imprimir(int)`).
- **Ambigüedad:** Si C++ encuentra dos coincidencias que son "igual de buenas", no puede decidir y te da un **error de compilación por ambigüedad**.
- **Argumentos por Defecto:** Es otra forma de flexibilidad (ej. `void f(int n = 1)`). Permite que llames a la función (`f()`) como si estuviera sobrecargada, usando un valor predefinido.

---

### 2. Plantillas de Función (La "Receta Genérica")

Las **plantillas** (_templates_) son la herramienta definitiva contra el código repetitivo. En lugar de escribir `max(int)`, `max(double)` y `max(char)`, escribes **una sola "receta" genérica**.

- **Sintaxis Clave:** `template <typename T>` (o `class T`).
- **¿Qué es `T`?** Es un **marcador de posición** para un tipo de dato. `T` no es un tipo real, solo un "espacio en blanco" que el compilador rellenará.
- **La Receta:** Escribes tu función usando `T` como si fuera un tipo normal:
```C++
template <typename T>
T max(T a, T b)
{
    return (a > b) ? a : b;
}
```
- **Instanciación:** Cuando llamas a `max(5, 10)`, el compilador "ve" que `T` debe ser `int`. Entonces, **"construye" (instancia) automáticamente** la versión `max(int, int)` por ti.

---
### 3. Plantillas Avanzadas

- **Múltiples Tipos:** Puedes tener tantos marcadores de posición como necesites, usando `T`, `U`, `V`, etc.
    - `template <typename T, typename U>` te permite escribir funciones que aceptan tipos diferentes, como `miFuncion(int, double)`.
- **Parámetros No-Tipo:** Las plantillas también pueden aceptar **valores constantes** (como un `int`) como parámetro, no solo tipos.
    - `template <int N, typename T>` te permite "hornear" un valor (`N`) en la función, como `multiplicarPor<5>(...)`.

---

### 4. Plantillas y Archivos (¡Regla Clave!)

- **¡Las plantillas deben ir en el `.h`!** A diferencia de las funciones normales, el compilador necesita la "receta" completa (el código `{...}`) en el mismo momento en que ve la llamada.
- Por lo tanto, debes poner **toda la plantilla** (declaración _y_ definición) en el **archivo `.h` (cabecera)** para que otros archivos puedan "construir" sus propias versiones.

---


# Capítulo F

### `constexpr`: La Función Híbrida

- **¿Qué es?** `constexpr` es una palabra clave que marca una función como un "híbrido".
- **Doble Naturaleza:**
    1. **Tiempo de Compilación (La "Fábrica" 🏭):** Si la llamas con valores constantes (ej. `factorial(4)`), el compilador "ejecuta" la función _antes_ de que el programa se cree. El resultado (`24`) se "hornea" ♨️ directamente en el `.exe`. Esto es súper rápido.
    2. **Tiempo de Ejecución (El "Cliente" 🧍‍♂️):** Si la llamas con una variable (ej. `factorial(x)`), el compilador "se rinde" y la trata como una función 100% normal que se ejecuta cuando el usuario corre el programa.
- **Uso:** Es ideal para funciones (como `factorial`) que quieres que sean súper rápidas para constantes, pero que sigan siendo flexibles para variables.
- **Reglas:** Para que una función sea `constexpr`, debe ser simple. No puede tener "memoria" (como `static local`) ni depender de variables globales (no-`const`).

---

### `consteval`: La Función Pura (C++20)

- **¿Qué es?** `consteval` (evaluación constante) es el primo "súper estricto" de `constexpr`.
- **Naturaleza Pura:** No es un híbrido. `consteval` **obliga** a que la función se ejecute _siempre_ en **tiempo de compilación**.
- **Sin Fallback:** Si intentas llamar a una función `consteval` con una variable de tiempo de ejecución (como `consteval_factorial(x)`), el programa **no compilará** 🛑.
- **Uso:** Se usa cuando quieres _garantizar_ que un cálculo (quizás uno muy pesado) _siempre_ se haga en la compilación y nunca ralentice el programa del usuario.

---
### `constexpr` vs. `consteval`

- **`constexpr`**: "Intenta compilar, pero el tiempo de ejecución está bien".
- **`consteval`**: "¡Debe ser en tiempo de compilación, o es un error!".

----
# Capítulo 12

### 1. La Teoría: `lvalues` vs. `rvalues`

Todo el capítulo se basa en esta diferencia clave:

- **`lvalue` (la "caja" 📦):** Es una expresión que tiene una **dirección de memoria** persistente. Es una "caja" con una etiqueta (como una variable `x` o `nombre`). Puedes asignarle un valor.
- **`rvalue` (el "vapor" 💨):** Es una expresión que representa un **valor temporal** sin dirección fija. Es el "vapor" que resulta de una operación (como el literal `5` o el resultado de `x + 2`). No puedes asignarle un valor.

---

### 2. Referencias Lvalue (`&`): El "Apodo" 🏷️

Una **referencia (`&`)** no es una variable nueva. Es un **"apodo"** (alias) para un `lvalue` (una "caja") que ya existe.

- **Regla:** `int& ref = valor;`. `ref` y `valor` son ahora dos nombres para **la misma "caja"**. Si modificas `ref`, `valor` cambia.
- **Uso Principal:** Pasar variables a funciones **sin copiarlas**.

Hay dos formas de pasar por referencia:

1. **`void func(int& x)` (Pasar por Referencia):**
    - **Rápido:** No se hace copia.
    - **Permite Modificar:** La función recibe un "apodo" de la variable original y **puede modificarla**.
2. **`void func(const std::string& s)` (Pasar por Referencia Constante):**
    
    - **¡LA REGLA DE ORO 🏆!** Esta es la forma moderna y preferida de pasar objetos "pesados" (`string`, `vector`, etc.).
    - **Rápido:** No se hace copia (usa `&`).
    - **Seguro:** Es un "apodo de solo lectura" (usa `const`). La función promete no modificar el original.

`const int* ptr`: Promesa de no cambiar valor. Referencia constante.
`int* const ptr`: Promesa de no cambiar de dirección a la que se apunta.

---

### 3. Punteros (`*`): La "Dirección" 📝

Un **puntero (`*`)** SÍ es una **variable nueva**. Es una "caja" especial cuyo único trabajo es **guardar la dirección de memoria** de otra variable.

- **La "Danza" de Símbolos:**
    - `int* ptr;` (Declaración): `ptr` es una variable que guarda una dirección a un `int`.
    - `&` (Operador de Dirección): `ptr = &casa;` ("Dame la dirección de `casa`").
    - `*` (Operador de Desreferencia): `*ptr = 20;` ("Ve a la dirección guardada y pon un `20` en la casa que está allí").
- **Seguridad (`nullptr`):** Los punteros son peligrosos porque pueden estar "vacíos" (no inicializados). Usa `nullptr` para darles un valor "nulo seguro". **Siempre** comprueba si un puntero es `!= nullptr` antes de usar `*` en él.
- **Uso:** Se usan (rara vez) cuando necesitas la flexibilidad de "re-apuntar" el puntero a otra dirección o cuando necesitas que pueda estar "vacío" (`nullptr`).

**En resumen:** Prefiere siempre las **Referencias (`&`)** porque son más seguras. Usa **Punteros (`*`)** solo cuando _realmente_ necesites su flexibilidad.

---

### 4. Peligros y Soluciones Modernas

- **Referencias/Punteros Colgantes 🧟 (Dangling):** ¡El _bug_ más mortal! Ocurre si devuelves una referencia (`&`) o un puntero (`*`) a una **variable local** de una función. La variable local "muere" al salir de la función, y tu referencia/puntero se queda "colgando", apuntando a memoria muerta. **¡Nunca devuelvas un puntero o referencia a una variable local!**
- **`std::optional` (La Solución Moderna):** En lugar de usar un puntero y devolver `nullptr` (peligroso) si no encuentras algo, C++17 ofrece `std::optional`. Es un "contenedor" seguro que **o tiene un valor o está vacío** (`std::nullopt`). Es la forma preferida de manejar valores "opcionales".
	- Ejemplo:
```C++
#include <optional>

// Esta función devuelve un "contenedor opcional"
std::optional<Usuario> encontrarUsuario(int id) {
    if (id == 1) return Usuario("Ana"); // Devuelve una "caja llena"
    return std::nullopt; // Devuelve una "caja vacía"
}

std::optional<Usuario> u = encontrarUsuario(2);

// ¡Seguro! Comprobamos si la caja tiene valor
if (u.has_value()) // o solo 'if (u)'
{
    // Usamos .value() (o *u) para acceder
    std::cout << u.value().nombre; 
} else {
    std::cout << "Usuario no encontrado.\n";
}
```

---

# Capítulo 13

### 1. `enum class`: Las "Categorías" Seguras

Aprendimos a crear nuestros propios "catálogos" de constantes con nombre.

- **Forma Antigua (`enum Color { ROJO }`):** Es **insegura**. Contamina el _scope_ ( `ROJO` se "escapa" al exterior) y se convierte implícitamente a `int`, lo que permite errores lógicos.
- **Forma Moderna (`enum class Color { Rojo }`):** Es la forma **preferida y segura** 🏆.
    - **Con Ámbito (Scoped):** No contamina. Debes usar el "apellido" (`Color::Rojo`).
    - **Segura (Type-safe):** No se convierte a `int` por accidente.

```C++
enum class Color {
	Rojo,
	Verde,
	Azul
};

Color miColor = Color::Rojo 
```

- No se puede usar std::cout con clase Color, entonces:
```C++
std::string colorAString(Color color) 
{ 
	switch (color) 
	{ 
		case Color::Rojo: return "Rojo";
		case Color::Verde: return "Verde"; 
		case Color::Azul: return "Azul"; 
		default: return "???"; 
	} 
}
```

---

### 2. `struct`: Los "Paquetes" de Datos

Aprendimos a agrupar múltiples variables en un solo "paquete" lógico.

- **Definición:** Un `struct` (ej. `struct Estudiante`) agrupa variables (llamadas **miembros**).
- **Inicialización:** La forma más fácil es la "inicialización agregada" usando llaves (ej. `Estudiante ana { "Ana", 20, 8.5 };`).
- **Acceso (Selección de Miembros):** Usamos dos operadores clave:
    - **`.` (Operador Punto):** Para acceder a miembros desde el objeto mismo o una referencia (ej. `ana.nombre`).
    - **`->` (Operador Flecha):** Es un atajo para acceder a miembros desde un **puntero** (ej. `ptrAna->nombre`).
- **Paso a Funciones:** Los `struct`s (que pueden ser "pesados") casi siempre deben pasarse por **referencia constante (`const&`)** para evitar copias lentas y garantizar seguridad.

```C++
struct Videojuego 
{ 
	std::string titulo {}; 
	int anioLanzamiento { 2000 }; // ¡Valor por defecto! 
	double calificacion { 5.0 }; // ¡Valor por defecto! 
};
``` 
---

### 3. Plantillas de `struct` (Clase): Los "Paquetes Genéricos"

Aprendimos a combinar `struct` (Hito 2) y `template` (Cap. 11) para crear "paquetes" genéricos.

- **Definición:** `template <typename T, typename U> struct Par { ... };` crea un "plano" para un `struct` que puede guardar cualquier tipo.
- **CTAD (C++17):** Es la "deducción de argumentos". Nos permite escribir `Par p { 1, 2.5 };` y el compilador deduce `T=int` y `U=double` por nosotros (como `auto`).
- **Alias (`using`):** Podemos crear "apodos" para plantillas (ej. `using MapaDeString = Par<std::string, T>;`) para hacer el código más legible.

```C++
template <typename T, typename U> 
struct Par 
{ 
	T primero {}; 
	U segundo {}; 
};
```

---

# Capítulo 14

### 1. La Filosofía: OOP y Encapsulación 🔒

- **OOP (Programación Orientada a Objetos):** Es un paradigma de programación que consiste en "empaquetar" datos y las funciones que actúan sobre esos datos en una sola unidad llamada **objeto** (definida por una **`class`**).
- **`class` vs. `struct`:** Son casi idénticos. La única diferencia es la visibilidad por defecto:
    - **`struct`**: Miembros **`public`** (abiertos) por defecto. Ideal para paquetes simples de datos.
    - **`class`**: Miembros **`private`** (ocultos) por defecto. Ideal para OOP.
- **Encapsulación (Ocultamiento de Datos):** Es la idea central de OOP. Consiste en:
    1. Hacer los datos (`miembros`) **`private`** (una "caja fuerte" 🔒) para que el código exterior no pueda corromperlos.
    2. Proveer "botones" (**funciones miembro `public`** 🔑) para que el código exterior pueda _interactuar_ de forma segura con el objeto.
- **Getters y Setters:** Son las funciones públicas más comunes. Los **Setters** (ej. `asignarNota(int)`) validan y establecen un valor. Los **Getters** (ej. `obtenerNota()`) leen y devuelven un valor.

---

### 2. El "Nacimiento": Constructores 🐣

Un **constructor** es una función miembro especial que se llama _automáticamente_ cuando se crea un objeto. Su único trabajo es **inicializar** el objeto.
- **Reglas:** Tiene el mismo nombre que la clase y **no tiene tipo de retorno** (ni `void`).
- **Lista de Inicializadores (`:`)**: Esta es la forma **correcta y eficiente** de inicializar miembros. Ocurre _antes_ de que se ejecute el cuerpo `{}` del constructor.

```C++
class Estudiante {
private:
    int m_nota;
public:
    // Constructor con lista de inicializadores
    Estudiante(int nota_inicial) : m_nota{ nota_inicial } 
    {
        // El cuerpo se usa para lógica, no para inicializar
    }
};
```

- **Constructor por Defecto:** Es un constructor que no toma argumentos (ej. `Estudiante()`). Se llama cuando creas un objeto vacío (`Estudiante e;`).
- **Constructor de Copia (El "Clon" 🐑):** Un constructor que toma una referencia `const` a su propia clase (ej. `Estudiante(const Estudiante& otro)`). Se llama automáticamente cuando "clonas" un objeto (ej. `Estudiante e2 = e1;`).

---

### 3. Seguridad y `const` 🛡️

- **Funciones Miembro `const`:** Si una función miembro (como un "getter") **no modifica** ningún dato de la clase, debes marcarla con la palabra clave **`const` al final**.

``` C++
int obtenerNota() const 
{ 
    // m_nota = 10; // ¡ERROR! No puedes modificar en una función const
    return m_nota; 
}
```
Esto permite que la función sea llamada por objetos `const`.

- **`explicit`**: Es un "guardián" 🛡️ que se pone en los constructores que toman un solo argumento (ej. `explicit Estudiante(int nota)`). **Prohíbe** que el compilador haga "conversiones mágicas" implícitas (ej. `Estudiante e = 90;`), previniendo _bugs_ sutiles.

---
### 4. Clases en Tiempo de Compilación 🏭 (`constexpr`)

Este es el punto que une todo el Capítulo 14 con los conceptos de optimización avanzada (`constexpr`).

- **`constexpr` Clases y `struct`s:** Podemos declarar los **constructores** y las **funciones miembro** (como los _getters_) de una clase con la palabra clave `constexpr`.
- **¿Qué permite esto?** Permite que el compilador "ejecute" esas funciones y **cree instancias de tus objetos** (ej. `Punto p {1.0, 2.0};`) _dentro_ de la "fábrica" (en **tiempo de compilación**).
- **Optimización Definitiva:** El compilador puede hacer cálculos usando tus `struct`s/`class`es y "hornear" ♨️ el resultado final directamente en el `.exe`. El usuario final nunca tiene que ejecutar ese código, ¡haciendo que el programa sea increíblemente rápido!

```C++
struct Punto 
{ 
	// 2. El constructor 'constexpr' 
	// (Podemos usarlo en la "fábrica") 
	constexpr Punto(double x_in, double y_in) 
		: x(x_in), y(y_in) {} 
	// 3. El "botón" (función miembro) 'constexpr' 
	// (Este getter promete que puede correr en la "fábrica") 
	constexpr double obtenerX() const { return x; } 
	// Los miembros no necesitan ser 'constexpr' 
	double x;
	double y; 
}; 

// 4. Una función 'constexpr' que *usa* nuestro struct 
constexpr Punto crearPunto() 
{ 
	// ¡Estamos creando un objeto 'Punto' 
	// DENTRO de la fábrica! 
	return Punto(1.0, 2.0); 
}
```

---

# Capítulo 15

### 1. El "Yo" y la "Muerte": `this` y `Destructor`

- **`this` (El Puntero Oculto):** En cualquier función miembro (que no sea `static`), existe un puntero oculto llamado `this`. Este puntero apunta a la dirección del **objeto actual** que está llamando a la función. Es la forma en que una función "sabe" a qué objeto pertenece. Es muy útil para evitar el _shadowing_ (ej. `this->m_nota = m_nota;`).
- **`~Destructor()` (La "Muerte" 💀):** Es lo opuesto al constructor. Es una función especial (ej. `~Estudiante()`) que se llama **automáticamente** cuando un objeto "muere" (se destruye al salir de su _scope_). Su único trabajo es la **limpieza** (liberar memoria, cerrar archivos, etc.).

---

### 2. Organización: `.h` vs. `.cpp`

La regla de oro para organizar el código en C++ es **separar la "declaración" de la "implementación"**.

- **Clases Normales:**
    - **`.h` (Archivo de Cabecera):** Contiene la _definición_ de la clase (`class MiClase { ... };`) y las _declaraciones_ (promesas) de sus funciones miembro.
    - **`.cpp` (Archivo Fuente):** Contiene la _implementación_ (el código `{...}`) de esas funciones. Usas el operador de ámbito `::` (ej. `void MiClase::miFuncion() { ... }`) para "conectarlas".
- **Clases Plantilla (`template`):**
    - ¡Rompen la regla! Como son "recetas" 📜, el compilador necesita ver la implementación completa (`{...}`) para poder "construir" las versiones (`<int>`, `<double>`, etc.).
    - Por lo tanto, toda la plantilla (declaración _y_ definición) **debe ir en el archivo `.h`**.

---

### 3. Miembros `static` (El "Equipo")

Los miembros `static` **pertenecen a la Clase ⏰, no a los objetos individuales**. Solo existe _una_ copia compartida por todos.
- **`static` (Variable Miembro):** Es una variable _compartida_ por todos los objetos de la clase (ej. `s_contadorDeEstudiantes`). Debe ser declarada `static` en el `.h` y definida (inicializada) una vez en el `.cpp` (ej. `int Estudiante::s_contador = 0;`).
- **`static` (Función Miembro):** Es una función que pertenece a la clase y se puede llamar sin un objeto (ej. `Estudiante::obtenerContador()`). **No tiene puntero `this`** y solo puede acceder a otros miembros `static`.

---

### 4. `friend` y Tipos Anidados

- **`friend` (Amigo) 🔑:** Es una "llave maestra". Es una palabra clave que pones _dentro_ de tu clase (ej. `friend void funcionExterna(MiClase&);`) para darle a esa función (o a otra clase) acceso total a tus miembros **`private`**. Rompe la encapsulación, por lo que debe usarse con moderación.
- **Tipos Anidados:** Puedes definir un `enum` o `struct` _dentro_ de una clase (ej. `Coche::Estado`). Esto es excelente para la organización, ya que el tipo "pertenece" lógicamente a la clase (ej. `Coche::Estado::Parado`).

---

# Capítulo 16

### 1. ¿Qué es `std::vector`?

Un `std::vector` es un **"array inteligente"** o **"array dinámico"**. A diferencia de los arrays fijos (`int miArray[5]`), un `vector` puede **crecer y encogerse** en tiempo de ejecución. Es la forma moderna y preferida de manejar "listas de cosas". Requiere `#include <vector>`.

---

### 2. La Magia: Crecer y Encoger

El `vector` maneja toda la memoria por ti.

- **`push_back(elemento)`:** 🪄 Esta es la función mágica. **Añade** un elemento al _final_ del `vector`, haciendo que "crezca" automáticamente.
- **`pop_back()`:** **Quita** el elemento del _final_ del `vector`.
- **`size()` vs. `capacity()`:** `push_back()` es (casi siempre) súper rápido. Esto es porque el `vector` reserva memoria "de sobra".
    - **`size()`** es cuántos elementos _tienes_ 🧑‍🤝‍🧑.

    - **`capacity()`** es cuántos elementos _caben_ 📦 antes de tener que pedir más memoria (un proceso lento llamado re-alojamiento).

---

### 3. Recorrer `vector`s (Bucles)

Hay dos formas de recorrer un `vector`, ¡una mucho más segura que la otra!

- **Forma Moderna (¡Segura! 🏆): El `for-each`** Esta es la forma **preferida**. Es imposible equivocarse.

```C++
std::vector<int> v { 1, 2, 3 };

// "Para cada elemento EN v..."
// (Usamos const& para evitar copias lentas)
for (const auto& elemento : v)
{
    std::cout << elemento; // 1, 2, 3
}
```

- **Forma Clásica (¡Peligrosa! 🐛): El `for` con `.size()`** El _bug_ más infame de `vector`: la función `.size()` **no** devuelve un `int`, devuelve un **`unsigned int`** (sin signo). Esto puede causar _bugs_ de "subdesbordamiento" (underflow) en bucles que cuentan hacia atrás, llevando a _crashes_. Debes tener mucho cuidado.
	- Solución en C++20 `std::ssize()`(signed size).

---

### 4. Pasar y Devolver `vector`s

¡Los `vector`s son "pesados"! Moverlos incorrectamente es lento.

- **Para PASAR un `vector` a una función:** Usa **`const&`** (referencia constante). Es **rápido** (sin copias) y **seguro** (no se puede modificar).

```C++
// ¡Perfecto! ⚡
void imprimir(const std::vector<int>& v);
```

- **Para DEVOLVER un `vector` de una función:** ¡Simplemente **devuélvelo por valor**!

```C++
std::vector<int> crearVector()
{
    std::vector<int> v { 1, 2, 3 };
    return v; // ¿¡Lento!?
}
```

No te preocupes por la lentitud. C++ moderno usa "magia" 🪄 (semántica de movimiento) para "mover" el `vector` sin copiarlo. Es súper rápido.

---


# Capítulo 17
### `std::array`: La Forma Moderna (¡Segura!)

`std::array` es la forma preferida de C++ para un array de tamaño fijo. Es un "contenedor" (como un `struct`) que envuelve un array. Requiere `#include <array>`.

- **Sintaxis:** El tamaño es parte del tipo: `std::array<int, 5> miArray;`
- **Seguridad:** ¡Es "inteligente"!
    - **Conoce su tamaño:** Puedes llamar a `miArray.size()`.
    - **Acceso seguro:** Tiene `.at(i)` que comprueba si el índice es válido (evitando _crashes_).
- **Paso a Funciones:** Se pasa como un objeto. Para evitar copias lentas, se debe pasar por **referencia constante (`const&`)**, igual que un `std::vector`.

```C++
// ¡Rápido y seguro! No "decae".
void imprimir(const std::array<int, 5>& arr);
```

- **Arrays 2D (Matrices):** Se crean anidando: `std::array<std::array<int, 4>, 3> matriz;` (requiere `{{...}}` para inicializar).

---

### Array C-style: La Forma Antigua (¡Peligrosa!)

Esta es la forma heredada de C (`int miArray[5];`). Es rápida pero muy insegura.

- **Es "Tonto":** El array en sí **no sabe su propio tamaño**. `miArray.size()` no existe.
- **El "Decaimiento" (Array Decay) 🧟:** ¡Este es el _bug_ 🐛 más importante! Cuando "usas" un array C-style (como pasarlo a una función), este **"olvida" su tamaño** y se convierte (decae) en un simple **puntero (`*`)** 📝 a su primer elemento (`int*`).
    - **Consecuencia:** La función que lo recibe (`void func(int* ptr)`) **no tiene idea** de qué tan grande es el array, lo que obliga a pasar el tamaño como un argumento separado (`void func(int* ptr, int tamano)`).

---

### CONSEQUENCIAS DEL "DECAIMIENTO"

- **Aritmética de Punteros:** Como un array "decae" a un puntero, puedes usar "matemáticas" con él. `*(ptr + 2)` accede al segundo elemento después de `ptr`.
- **`array[i]` es un Atajo:** El compilador _traduce_ `miArray[2]` exactamente a `*(miArray + 2)`. ¡Son lo mismo!
- **C-strings (`char[]`):** La forma antigua de texto. Son solo `char[]` que _deben_ terminar con un carácter especial "STOP" 🛑: el **terminador nulo (`\0`)**.
    - `char texto[] = "Hola";` // El compilador añade `\0` por ti.
    - **Peligro:** Si olvidas el `\0`, las funciones (como `std::cout`) seguirán leyendo memoria "basura" 🗑️ hasta que encuentren uno, causando _bugs_ de seguridad graves. (¡Usa siempre `std::string`!).

---

# asd




- forms.html y forms.css
- Tarea de logs

- Laboratorio de míneria
- Estudiar control software

- Avanzar certificados
- Laboratorio 09

- Control Logs
- Control SOS