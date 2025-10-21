# Tarea 1


**Hipótesis.** Sea ε∈(0,1)\varepsilon\in(0,1)ε∈(0,1) y suponemos que

∀ distribuciones sobre M, ∀m∈M, ∀c∈C:∣Pr⁡[M=m∣C=c]−Pr⁡[M=m]∣<ε.\forall\ \text{distribuciones sobre }\mathcal M,\ \forall m\in\mathcal M,\ \forall c\in\mathcal C:\quad \big|\Pr[M=m\mid C=c]-\Pr[M=m]\big|<\varepsilon.∀ distribuciones sobre M, ∀m∈M, ∀c∈C:​Pr[M=m∣C=c]−Pr[M=m]​<ε.

Queremos probar ∣K∣≥(1−ε)∣M∣|\mathcal K| \ge (1-\varepsilon)|\mathcal M|∣K∣≥(1−ε)∣M∣.

**Demostración (más fuerte).**

1. Procedemos por contradicción. Supongamos ∣K∣<(1−ε)∣M∣|\mathcal K| < (1-\varepsilon)|\mathcal M|∣K∣<(1−ε)∣M∣. (En particular ∣K∣<∣M∣|\mathcal K| < |\mathcal M|∣K∣<∣M∣.)
    
2. Fijo c∈Cc\in\mathcal Cc∈C. Define Mc={m∈M:∃k∈K, Ek(m)=c}\mathcal M_c=\{m\in\mathcal M:\exists k\in\mathcal K,\ E_k(m)=c\}Mc​={m∈M:∃k∈K, Ek​(m)=c}.  
    Como (en el modelo estándar) cada EkE_kEk​ es una permutación sobre M\mathcal MM, para cada clave kkk existe exactamente un mmm tal que Ek(m)=cE_k(m)=cEk​(m)=c; por tanto
    
    ∑m∈M#{k:Ek(m)=c}=∣K∣.\sum_{m\in\mathcal M} \#\{k: E_k(m)=c\}=|\mathcal K|.m∈M∑​#{k:Ek​(m)=c}=∣K∣.
    
    En particular ∣Mc∣≤∣K∣<∣M∣|\mathcal M_c|\le|\mathcal K|<|\mathcal M|∣Mc​∣≤∣K∣<∣M∣, así que existe al menos un mensaje m∗∈Mm^*\in\mathcal Mm∗∈M que **no** pertenece a Mc\mathcal M_cMc​ (es decir, m∗m^*m∗ no puede ser la desencriptación de ccc para **ninguna** clave).
    
3. Ahora usa la cuantificación “para toda distribución”: elige la prior que pone probabilidad 1 sobre m∗m^*m∗ (masa puntual en m∗m^*m∗). Para esa prior:
    
    - Pr⁡[M=m∗]=1\Pr[M=m^*]=1Pr[M=m∗]=1.
        
    - Pero como m∗∉Mcm^*\notin\mathcal M_cm∗∈/Mc​ se tiene Pr⁡[C=c∣M=m∗]=0\Pr[C=c\mid M=m^*]=0Pr[C=c∣M=m∗]=0, por lo que Pr⁡[M=m∗∣C=c]=0\Pr[M=m^*\mid C=c]=0Pr[M=m∗∣C=c]=0.
        
4. Entonces
    
    ∣Pr⁡[M=m∗∣C=c]−Pr⁡[M=m∗]∣=∣0−1∣=1.\big|\Pr[M=m^*\mid C=c]-\Pr[M=m^*]\big| = |0-1| = 1.​Pr[M=m∗∣C=c]−Pr[M=m∗]​=∣0−1∣=1.
    
    La hipótesis pide que esa diferencia sea <ε<\varepsilon<ε, pero ε<1\varepsilon<1ε<1. Contradicción.
    
5. Por tanto la suposición ∣K∣<∣M∣|\mathcal K|<|\mathcal M|∣K∣<∣M∣ es imposible. Concluimos que necesariamente
    
    ∣K∣≥∣M∣.|\mathcal K|\ge |\mathcal M|.∣K∣≥∣M∣.
    
    En particular ∣K∣≥(1−ε)∣M∣|\mathcal K|\ge(1-\varepsilon)|\mathcal M|∣K∣≥(1−ε)∣M∣ (pues 1≥1−ε1\ge 1-\varepsilon1≥1−ε).
    

**Comentario:** esta prueba es **más fuerte** que la cota pedida: si la condición se exige para **toda** prior entonces ya sale ∣K∣≥∣M∣|\mathcal K|\ge|\mathcal M|∣K∣≥∣M∣. Así que tu afirmación objetivo ∣K∣≥(1−ε)∣M∣|\mathcal K|\ge(1-\varepsilon)|\mathcal M|∣K∣≥(1−ε)∣M∣ es cierta, pero se sigue inmediatamente de una conclusión aún más fuerte.
# Clase 2: Criptografía clásica

- Requisito de desincreptación
- Cifrador de transposición y sustitución
- Cifrador de Vigenére
	- Test de Kasiski
	- Índice de Coincidencia
- Rotores
- One-Time Pad
- Principio de Kerchkoffs: Seguridad sólo debe depender de la privacidad de la llave

# 2. Confidencialidad perfecta

El secreto perfecto requiere llaves verdaderamente aleatorias, y como la aleatoriedad perfecta no existe en la práctica, los sistemas deben recolectar entropía del entorno y procesarla bien; usar un mal generador destruye toda la seguridad.

## 2.1 Definitions

- **Perfect secrecy**: observar el ciphertext no cambia en nada tu creencia sobre el mensaje.Formas equivalentes:
    1. Probabilidades condicionadas: $Pr⁡[M=m∣C=c]=Pr⁡[M=m]\Pr[M=m \mid C=c] = \Pr[M=m]Pr[M=m∣C=c]=Pr[M=m]$
    2. Distribuciones idénticas:$Pr⁡[EncK(m)=c]\Pr[Enc_K(m)=c]Pr[EncK​(m)=c]$ es la misma para todos los mensajes.
    3. Indistinguibilidad: ningún atacante puede adivinar mejor que al azar entre dos mensajes.
- El One-Time Pad cumple estas condiciones; cifrados clásicos como César o Vigenère, no.

## 2.2 The One-Time-Pad

- El One-Time Pad es el único cifrado con **secreto perfecto**.
- Pero tiene problemas prácticos:
    - Claves tan largas como los mensajes.
    - No se puede reutilizar la clave jamás.
- Por eso casi no se usa hoy, salvo en casos muy especiales (líneas diplomáticas, uso militar muy controlado).

## 2.3 Limitaciones de la confidencialidad (secreto) perfecto

- Perfect secrecy = clave tan larga como el mensaje y usarla solo una vez.
- El One-Time Pad no es un error de diseño, sino el **único esquema posible con secreto perfecto**.

## 2.4 Teorema de Shannon

El teorema de Shannon dice que un esquema es perfectamente secreto **⇔**
1. Todas las claves son igual de probables.
2. Cada par (mensaje, cifrado) corresponde a una única clave.  
    Esto caracteriza de manera completa al One-Time Pad y demuestra que no hay alternativas mágicas con claves más cortas.


# Cifradores de Bloque

## 3.1 What is blockciphers?

Un blockcipher es un algoritmo de cifrado que, con una clave secreta, convierte mensajes de longitud fija en ciphertexts de la misma longitud, de manera reversible y eficiente. Lo esencial es que sea **una permutación para cada clave**, y que esté diseñado para que sin la clave sea prácticamente imposible descifrar.

## 3.2 Data Encryption Standart (DES)

DES es un **blockcipher clásico**:

- Bloques de 64 bits, clave de 56 bits.
- 16 rondas Feistel con función **f** (expansión, XOR con subclave, S-boxes, permutación).
- Aunque inseguro hoy por su corta clave, fue la base de casi toda la criptografía simétrica moderna y aún se enseña como “el ejemplo histórico”.

## 3.3 Key recovery attacks on Blockciphers

### Sobre DES
- La **mejor técnica práctica conocida** sigue siendo **búsqueda exhaustiva**.
- Se puede hacer **en paralelo**, y con hardware especializado, puede reducirse de **decenas de años a horas**.
    - Ejemplo: máquina de la EFF encontró una clave DES en 56 horas (1990s).
- **Conclusión:** DES fue muy fuerte para su época, pero con avances en hardware, ya no es seguro.

### Más allá

- Un bloque cifrador seguro debe resistir más que solo **ataques de recuperación de clave**.
- **Limitación de DES:** tamaño del bloque 64 bits → vulnerable a ataques tipo “cumpleaños” con q≈232q \approx 2^{32}q≈232 pares.
- Por eso se diseñaron cifradores modernos como **AES**, con bloques de 128 bits y claves más largas.

## 3.4 Iterated-DES and DESX

### Limitaciones

- **Tamaño de bloque de DES = 64 bits** → vulnerable a ataques tipo “cumpleaños” con 2322^{32}232 pares de mensajes.
- Incluso DESX o 3DES con clave larga **siguen teniendo el mismo tamaño de bloque**, por lo que desde ese punto de vista no son mucho más seguros.
- Esto motivó el diseño de **AES**: mayor longitud de clave y **bloques de 128 bits** para evitar ataques de cumpleaños.

### Comparación

| Cifrado | Clave nominal | Operaciones para romper    | Velocidad relativa |
| ------- | ------------- | -------------------------- | ------------------ |
| DES     | 56 bits       | 2^56                       | 1x                 |
| 2DES    | 112 bits      | 2^57 (meet-in-the-middle)  | 2x lento           |
| 3DES2   | 112 bits      | 2^112                      | 3x lento           |
| 3DES3   | 168 bits      | 2^112 (meet-in-the-middle) | 3x lento           |
| DESX    | 184 bits      | 2^120                      | ~1x-1.5x lento     |

## 3.5 Advanced Encryption Standart (AES)
# Clase 4: Cifradores de Bloque
, DES y ataques
- Funciones
- Permutaciones
- Familia de Funciones (o Permutaciones)
- Cifrador de Bloque
	- Familia de funciones con
		- Mismo dominio y recorrido
		- Permutación
	- Largo del dominio (o recorrido) = Largo del bloque
- DES
	- Largo clave: 56
	- Largo bloque: 64
	- IP y IP^-1
	- Función f
		- Input: 32 bits de texto plano (mitad) y una subclave de 48 bits
		- XOR entre estos
		- Subdividir el retorno del XOR en 8 partes de 6 bits
		- Introducir a los round de Feistel. Cada caja retorna 4 bits.
		- Unir outputs de cajas para retornar
	- Caja S
		- 2 bits finales: índice fila
		- 4 bit iniciales: índice columna
	- KeySchedule
		- Extender bits de llave. Agregando 1 cada 8.
		- ... Escoger key
- Recuperación de Clave Objetivo (TKR)
- Juego TKR_E
- Ventaja del Adversario
- Fuerza Bruta o Búsqueda Exhaustiva de Claves EKS
- Clave Consistente
- Juego para Recuperación de Claves (KR)
- Proposición
- q > k/l : consultas > largo_llave/largo_bloque, se espera que la ventaja en TKR para Adversario de EKS sea cercana a 1.
- DES quebrado por EKS en paralelo
- DES sólido, no existe otro ataque que exploten su estructura.

# Clase 5: Cifradores de Bloque (Parte II)
- 2DES_(K1||K2): DES_K2(DES_K1(M))
- Ataque "Encontrarse en el medio" (Meet in the Middle)
	- Clave efectiva es de 57 bits
- 3DES
	- 3DES3_(K1||K2||K3): DES_K3(DES_K2 ^(-1)(DES_K1(M)))
	- 3DES2_(K1||K2): 3DES3 pero DES con K2 y DES^-1 con K1
- También ataque MITM para 3DES3
	- Clave efectiva 112 bits
- AES
	- Expand

# Clase 6: Funciones pseudoaleatorias (PRF)

- Dificultad para recuperar clave no es suficiente
- 