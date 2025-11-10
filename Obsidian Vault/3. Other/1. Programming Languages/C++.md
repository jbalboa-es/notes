#programming_languages
#other
## Content table
> [[#Capítulo 1]]
 >	- *statement* y comentarios
 >	- *variables*: inicialización y comportamiento indefinido
 >	- identificadores
 >	- `iostream`: `cin` y `cout`
 >	- literal, operador y expresiones
>[[#Capítulo 2]]
 >	- funciones
 >	- parámetros y scope
 >	- declaración y definición
 >	- separación en archivos: `.cpp` y `.h`
 >	- `namespaces` y `#pragma once`
>[[#Capítulo 3]]
 >	- tipos de errores
 >	- depuración básica
 >	- depurador
 >	- prevensiones
>[[#Capítulo 4]]
 >	- tipos de datos y `sizeof()`
 >	- enteros
 >	- decimales
 >	- lógica y texto
 >	- `if statements` y conversión de tipos
>[[#Capítulo 5]]
 >	- `const`
 >	- `constexpr`
 >	- `std::string`
 >	- `std::string_view`
>[[#Capítulo 6]]
 >	- aritmética y precedencia
 >	- (de/in)cremento
 >	- operadores de lógica
 >	- operador ternario

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

# Capítulo 7





