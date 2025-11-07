#programming_languages
#other
## Content table
> [[#Chapter 0 Getting Started]]
> [[#Chapter 1 C++ Basics]]
## Getting Started
- Para compilar
```bash
g++ main.cpp -o main
# Se le puede añadir:
# -std=c++17
# -Wall -Wextra
	# Para warnings
```
## Chapter 1: C++ Basics
```C++
int a = 5; // copy initialization
int b(6);  // direct initialization
int c{7};  // list initialization

#include <iostream>
std::cout << "texto" << std::endl;
std::cin >> variable;
```
copy: crea la variable y luego copia el valor
	permite conversiones implicitas
direct: 
### Qué hace

- Llama directamente al constructor o inicializador correspondiente.
    
- Es común en objetos o clases con constructores.
    

### 🔹 Características

- Similar a la anterior, pero más eficiente (no crea una copia intermedia).
    
- También permite conversiones implícitas

LIST
### Características

- **Prohíbe conversiones peligrosas**:
- Permite inicializar múltiples variables o estructuras:
- Funciona igual para variables simples, structs, clases o arreglos.


La inicialización con llaves `{}` es preferida porque **previene conversiones implícitas inseguras**:



Si declaras una variable sin asignarle valor inicial, su contenido es **indeterminado (basura de memoria)**:


Reglas:

- Empiezan con letra o `_`, no con número.
    
- No tienen espacios.
    
- Son sensibles a mayúsculas.
```C++
camelCase
snake_case
```

papomudas
Errores por sintaxis y por lógica
g++ -g main.cpp -o main
gdb ./main

	break main
	run
	next
	print x
	quit

|Concepto|Explicación|
|---|---|
|**Breakpoint (punto de ruptura)**|Marca una línea donde el programa se detiene al depurar.|
|**Usos**|Inspeccionar variables, verificar flujo, detectar errores antes de que ocurran.|
|**Run normal**|Ejecuta todo el código hasta que termine o ocurra un error.|
|**Run en modo debug**|Ejecuta bajo control del depurador, se detiene en breakpoints.|
## Explicación detallada

- `std::cin.fail()`  
    → Devuelve `true` si la última operación de entrada **falló** (por ejemplo, leer un string en lugar de un número).
    
- `std::cin.clear()`  
    → Limpia las **banderas de error** (`failbit`, `badbit`), dejando el flujo listo para usarse de nuevo.
    
- `std::cin.ignore(n, c)`  
    → Descarta caracteres que quedaron en el buffer de entrada.

## 2. Por qué `main()` **retorna 0**

La función `main()` es el **punto de entrada del programa**.  
Cuando termina, devuelve un **código de salida** al **sistema operativo**.

Por convención:

- `return 0;` → indica que el programa **terminó correctamente**.
    
- Cualquier otro valor → indica **algún tipo de error**.



`std::endl` imprime un salto de línea y **vacia el búfer** (útil pero más lento).  
También puedes usar `'\n'` (más rápido):

Forward declaration

Overloading:
C++ permite tener varias funciones **con el mismo nombre** siempre que sus **parámetros sean distintos**.

`#include` inserta el contenido de un archivo.  
`#define` crea macros o constantes simbólicas (aunque se prefieren `const` o `constexpr` hoy en día).

- Los `.h` contienen **declaraciones**.
    
- Los `.cpp` contienen **definiciones**.
    
- `#include` copia el contenido del `.h` en el archivo actual.

Header guards
#ifndef ADD_H   // Si no está definido
#define ADD_H   // Defínelo

int add(int a, int b);

#endif          // Fin del guardia


g++ -c main.cpp   # compila sin enlazar (genera main.o)
g++ -c add.cpp    # compila sin enlazar (genera add.o)
g++ main.o add.o -o programa  # enlaza los objetos

g++ main.cpp add.cpp -o programa

| Concepto                    | Explicación                                                                |
| --------------------------- | -------------------------------------------------------------------------- |
| **Lectura secuencial**      | El compilador lee el código de arriba a abajo.                             |
| **Declaración (prototipo)** | Informa al compilador que una función existe y cómo se usa.                |
| **Definición**              | Contiene el cuerpo real de la función.                                     |
| **Forward declaration**     | Permite usar funciones definidas más abajo en el código o en otro archivo. |
| **Linker**                  | Une las declaraciones con las definiciones reales al final.                |
Errores de compilacion
	de enlace
	de ejecucion
	lógicos

g++ -g main.cpp -o programa
-g incluye info de depuracion

mejor usar gdb

- `next` → ejecutar la siguiente línea de código (no entra en funciones).
    
- `step` → entra dentro de funciones llamadas para inspeccionarlas.

- `next` → ejecuta **la siguiente línea** y se detiene después, **sin entrar en funciones llamadas**.
    
- `step` → ejecuta **la siguiente línea**, pero **entra dentro de la función llamada** si hay alguna.


(gdb) next
# Ejecuta: int x = 5; se detiene antes de la línea int y = 10;

(gdb) next
# Ejecuta: int y = 10; se detiene antes de: int z = add(x, y);

(gdb) step
# Como ahora se llama add(x, y), entra dentro de la función add()
# Se detiene en la primera línea de add()

(gdb) next
# Ejecuta la línea return a + b; y vuelve a main

(gdb) continue
# Termina la ejecución del programa hasta el final

- `next` es “paso sobre”: útil para avanzar líneas sin entrar en funciones.
    
- `step` es “paso dentro”: útil para inspeccionar qué pasa dentro de funciones.


g++ -g -Wall -Wextra main.cpp -o programa


\#include <cassert>

int main() {
    int x = 5;
    assert(x > 0); // ✅ pasa
    assert(x < 0); //  falla y detiene el programa
}

C++ tiene ** tipos de datos fundamentales ** :

1. **Enteros (`int`)** → números sin decimales.
    
2. **Caracteres (`char`)** → un solo carácter (ASCII).
    
3. **Booleanos (`bool`)** → `true` o `false`.
    
4. **Punto flotante (`float`, `double`, `long double`)** → números con decimales.
    

Todos estos tipos se pueden **modificar con `signed`, `unsigned`, `short`, `long`** para ajustar el tamaño y rango.

int 4 bytes en sistemas modernos

unsigned int u = 3000000000; // permitido
int i = 3000000000;          // ❌ overflow

char c = 'A';
std::cout << c + 1; // 66 → 'B'

También existen:

- `signed char`
    
- `unsigned char`
    
- `wchar_t` (caracteres “grandes”, Unicode básico)

true=1 y false=0

|Tipo|Tamaño aproximado|Precisión|
|---|---|---|
|`float`|4 bytes|~7 dígitos|
|`double`|8 bytes|~15 dígitos|
|`long double`|16 bytes|~19 dígitos|

1.0      // double
1.0f     // float
1.0L     // long double
100U     // unsigned int
100LL    // long long


auto type specifier

int a = 5;
decltype(a) b = 10; // b es int

`sizeof` devuelve **cuántos bytes ocupa un tipo o variable**:

double d = 3.14;
int i = static_cast<int>(d); // 3

const int DAYS_IN_WEEK = 7;
DAYS_IN_WEEK = 8; // ❌ error: no se puede modificar

Convención: se usan **mayúsculas con guiones bajos** (`DAYS_IN_WEEK`) para constantes globales

`constexpr` indica que **el valor se puede evaluar en tiempo de compilación**:

char name[] = "Juan";

#include <string>
#include <iostream>

std::string name = "Juan";
std::cout << name << std::endl;

OPERATIONS WITH std::string
std::string a = "Hola";
std::string b = " Mundo";

std::string c = a + b;         // concatenación
std::cout << c.length() << '\n'; // longitud
std::cout << c[1] << '\n';    // acceso por índice (0-based)

|Función / operador|Descripción|Ejemplo|
|---|---|---|
|`+`|Concatenar strings|`s3 = s1 + s2;`|
|`+=`|Concatenación abreviada|`s1 += s2;`|
|`.length()` / `.size()`|Devuelve longitud|`s.length();`|
|`.empty()`|Verifica si está vacía|`s.empty();`|
|`.substr(pos, len)`|Substring|`s.substr(0,3);`|
|`.find(str)`|Buscar substring|`s.find("abc");`|
|`.replace(pos, len, str)`|Reemplazar parte|`s.replace(0,3,"xyz");`|
|`[i]`|Acceso a carácter|`s[0] = 'A';`|
|`.c_str()`|Devuelve `const char*`|`printf("%s", s.c_str());`|
|`.append(str)`|Agrega al final|`s.append("abc");`|
|`.erase(pos, len)`|Elimina parte|`s.erase(0,3);`|

const char* ptr = "Hola mundo";
std::cout << ptr << '\n';

- `std::cout` sabe **que ptr apunta a un C-string terminado en `\0`**.
    
- No imprime la dirección de memoria, sino **el contenido hasta el `\0`**.
    
- Si no hubiera `\0`, imprimiría basura o hasta crash.
    

> Resumen: `std::cout` **interpreta `char*` como string**, no como dirección

#include <cstring>
#include <iostream>

int main() {
    char name[10];
    strcpy(name, "Juan");  // Copia "Juan" + '\0' en name
    std::cout << name << '\n'; // imprime "Juan"
}

**Nota importante:**

- El array destino (`name`) debe ser **lo suficientemente grande**.
    
- `strcpy` **no comprueba límites**, así que si copias algo más grande que el array, crash seguro.


- **Aritméticos**: `+`, `-`, `*`, `/`, `%`
    
- **Asignación**: `=`, `+=`, `-=`, `*=`, `/=`, `%=`
    
- **Incremento/decremento**: `++`, `--`
    
- **Relacionales**: `==`, `!=`, `<`, `>`, `<=`, `>=`
    
- **Lógicos**: `&&`, `||`, `!`
- Evaluación **corta-circuito**: si el primer operando determina el resultado, el segundo no se evalúa.
    
- **Bit a bit (bitwise)**: `&`, `|`, `^`, `~`, `<<`, `>>`
- x       = 00000101  (5)
~x      = 11111010

Número negativo → tomar **complemento a dos** del positivo:

- Invertir todos los bits.
    
- Sumar 1.
Los números negativos se representan en **complemento a dos**, así que `~x` de un positivo `x` siempre será **-(x+1)**.

    
- **Condicional**: `?:` (ternario)
- Sintaxis: `condición ? valor_si_true : valor_si_false`
    
- **Coma**: `,` (evalúa y devuelve el último valor)
- int x = (1, 2, 3); 
std::cout << x << '\n'; // 3







