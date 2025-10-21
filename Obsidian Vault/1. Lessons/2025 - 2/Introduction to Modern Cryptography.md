#university 
#cryptography
#computation_theory



# Clase 08

- Modos de operación
Cómo convertir un cifrador de bloque en un esquema de encriptación (procesar mensajes de largo arbitrario)

## ECB
Electronic Codebook Mode

![[../../Pasted image 20251017151652.png]]
Requerimiento:
- Que $E_k$ sea un cifrador de bloque, por tanto invertible
Debilidad: 
- Determinismo -> Bloques repetidos de mensajes entregan bloques repetidos de bloques cifrados
Solución:
- Encriptación aleatorizada

## CBC$
Chipher block chaining (con IV aleatorio)

![[../../Pasted image 20251017152305.png]]

## CTR$
Counter Mode Random
Modo contador aleatorizado

![[../../Pasted image 20251017152932.png]]


No utiliza $E_k^{-1}$ por lo que $E_k$ puede no ser cifrador de bloque
Encriptación y desencriptación paralelizables

# Clase 09

Definición de seguridad, no obtener ninguna información completa ni parcial de los mensajes encriptados.
- Primer bit de M
- Si M1 = M2
- El XOR entre M1 y M2

- Qué buscamos:
El adversario, conociendo ambos mensajes y C, no logra adivinar cual de los dos mensajes es el encriptado.

Dejaremos que incluso escoja los mensajes

## Propiedad maestra

IND-CPA: indistinguibilidad ante ataque de texto plano escogido 

## Juego

![[../../Pasted image 20251017180853.png]]
![[../../Pasted image 20251017180913.png]]

**Requisito**: Mensajes mismo largo

Tiempo de ejecución t y mensajes preguntados (consultas) al oráculo

### Formulación alternativa

![[../../Pasted image 20251017193504.png]]