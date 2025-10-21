#cryptography 

Estudiante: Juan Balboa Espinoza
# P1

// Asumiendo que... donde definimos a este Adversario B del siguiente modo:
//

Para realizar esta demostración, supondremos que $SE$ no es IND-ROR seguro y con eso, demostraremos que tampoco es IND-CPA seguro.

Asumiendo que  no es IND-ROR seguro, existe un adversario B que gana el juego IND-ROR contra  con ventaja significativa.

Utilizaremos el poder de B para construir un adversario A contra SE en el juego IND-CPA. Definimos A de la siguiente forma:


```md
Adversario A^IND-CPA:
	b <-$ {0,1}
	K <-$ G
	M_b <-$ {0,1}^|M|
	B <- M_b
	Ejecutamos B^IND-ROR: // tiempo de B
		R <-$ {0,1}^|M|
		C <- Fn(M_b)      // Juega en IND-ROR -> Puede retornar E_k(M_b) o E_k(R)
					      // consulta 1
		B -> C
	if(E_k(M_b) == C):    // si efectivamente encriptó el mensaje M_b
						  //+ tiempo que le toma encriptar M_b a A 
		return 1
	return 0            
```

De lo anterior, es posible notar que dado que B posee una gran ventaja para acertar que está en el mundo Real, se tiene una correspondencia entre esto y la ventaja de que A acierte el mundo en el que se encuentra, en concreto, se tiene que:

$Adv_{IND-CPA}(A) = | Pr[Real_{B} => True] - Pr[Random_{B} => True] |$

Donde, dado que si B juega en el mundo Random, se tendría entonces que A retornaría 1 (True) en la misma medida en que $R$ sea justamente $M_b$ , entonces:

$Pr[Random_{A} => True] = 1/2^{|M|}$

Luego,

$Adv_{IND-CPA}(A) = | Pr[Real_{B} => True] - 1/2^{|M|} |$

Donde solo basta una consulta para A y su tiempo asociado corresponde al tiempo de ejecución de B sobre su oráculo para la consulta, más el tiempo de encriptación de A sobre $M_b$.

# P2

Similar al caso anterior, supondremos que $SE$ no es $REPCTXT$ seguro y con eso, demostraremos que tampoco es IND-CPA seguro.

Asumiendo que $SE$ no es $REPCTXT$ seguro, existe un adversario B que gana el juego $REPCTXT$ contra $SE$ con ventaja significativa.

Utilizaremos el poder de B para construir un adversario A contra $SE$ en el juego IND-CPA. Definimos A de la siguiente forma:

```md
Adversario A^IND-CPA:
	k <-$ G
	b <-$ {0,1}
	M_b <- {0,1}^|M|
	B <- M_b
	Ejecutamos B dos veces:
		S <- vacío
		C <- E_k(M_b)         // gran probabilidad de que C sea el mismo
		S <- S U {C}
		// cuando termine ambas consultas
		B -> b'
	if(b' == 1):             // cifrado C en ambas consultas, por tanto mismo mundo
		return 1             
	return 0
```

De lo anterior, se puede evidenciar que hay una correspondencia entre la ventaja de A para acertar en el mundo en el que está con la probabilidad de que B de que retorne 1 (True) , en concreto, se tiene que:

$Adv_{IND-CPA}(A) = Pr[REPCTXT_{B} => True]$

Que es equivalente a:

$Adv_{IND-CPA}(A) = Adv_{REPCTXT}(B)$

Donde, se realiza una consulta para A (pasa $M_b$) y dos para B (encripta dos veces $M_b$); y en cuanto al tiempo, ambos deben esperar a que B encripte el mensaje dos veces, por lo que $t_A =  2*t_B$.

# P3

## a

Para demostrar que $H$ no es resistente a colisiones, basta mostrar un par $(X', Y')$ distinto de $(X,Y)$ tal que $H_K(X'|| Y') = H_k(X || Y)$.

Para esto, nos aprovecharemos primeramente, de que en el constructor de $H$ se encuentra un cifrador de bloque PRF y por lo tanto, existe su desencriptador $D_k()$

De aquí, como en sí, necesitamos que:

$E_{X'}(Y) \oplus X' = E_X(Y) \oplus X$

Es conveniente primero notar que, para el lado izquierdo necesitaremos obtener un (a partir de $Y'$):

$Z = X' \oplus X$

De forma que $Z \oplus X' = X$

A sí mismo, necesitaremos que se obtenga un

$W = E_X(Y)$
 
- Nota: Es relevante percatarse que de cierta forma se "escoge" la clave, por lo que el hecho de que sea PRF no toma tanta relevancia, pues se debilita en el determinismo. (Dada una clave, si ingresamos un mismo mensaje siempre retornará el mismo cifrado)

De manera que:

$W \oplus Z \oplus X' = E_X(Y) \oplus X = H_k(X,Y)$

Por lo que, bastaría tomar el siguiente par:

$(X',  D_{X'}(W \oplus Z))$

para obtener una colisión, con,

$Y' = D_{X'}(W \oplus Z))$

Por tanto, se obtiene que $H$ no es resistente a colisiones. Donde se necesitó una encriptación de $E_X(Y)$ y una desencriptación $D_{X'}(Y')$.

## b

En este caso, lo que un adversario podría hacer es lo siguiente:

```md
Adversario A:
k <-$ {0,1}^k             // importante notar que se fija un k al comienzo del juego
m_0 <-$ {0,1}^(n-1)
m_1 <-$ {0,1}^(n-1)
m_2 <-$ {0,1}^(n-1)
m_3 <-$ {0,1}^(n-1)
Ejecutar el MAC para consulta de etiquetas:
	t_0 || t_1<- T_k(m_0 || m_1)
	t_2 || t_3<- T_k(m_2 || m_3)
	// Como esto nos entrega etiquetas válidas y el k está fijo para F_k:
A -> (m_0 || m_3), (t_0 || t_3)
```

Es decir, dado el determinismo de F para una clave fijada con anterioridad, un adversario A podría realizar dos consultas convenientes con dos mensajes formados por mitades distintas, para luego, a través de estos y las etiquetas entregadas, formar un par de un nuevo mensaje y una nueva etiqueta válida que le permitirá engañar al verificador y por tanto, hacer pasar su mensaje como auténtico.

Es importante notar que en este caso se explota la independencia de la ejecución de ambas mitades del mensaje en $F_k$, pues justo en ello recae la débilidad de esto, ya que nos permite hacer esta combinación de mitades tanto en los mensajes como en los tags.