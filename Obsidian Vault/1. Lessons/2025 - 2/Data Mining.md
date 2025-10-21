#university 
#data_science

# Tabla de contenidos



# Clustering
## Aprendizaje no supervisado

En **aprendizaje no supervisado**, no hay una variable objetivo $Y$ etiquetada que queramos predecir. El objetivo es **descubrir estructuras** en los datos, como **grupos (clusters)**, **patrones** o **regularidades**. Esto difiere del **aprendizaje supervisado**, donde sí conocemos las etiquetas $(X_i,Y_i)(Xi_​,Yi_​)$ y buscamos una función $f$ que prediga $Y$ a partir de $X$.
## Clustering

Conjunto de técnicas para encontrar subgrupos con objetos similares o relacionados entre sí y que sean diferentes o no relacionados a los objetos de otro subgrupo.

- Idea
Minimizar la distancia intra-cluster (entre elementos de un grupo) y maximizar distancias inter-cluster (entre grupos)

### K-means
- Centroide
Punto medio de los elementos de un cluster
- Separa los datos en **K** clusters
- Se puede medir la variabilidad intra-cluster como la suma de errores cuadrados (SSE): Distancia de cada punto en un cluster al centroide
- Algoritmo
	- Seleccionar K puntos como centroides iniciales (aleatorios)
	- Formar K clustgers asignando todos los puntos mas cercanos a estos centroides
	- Recomputar centroide de cada cluster
	- Repetir hasta que el centroide no cambie
- En sklearn
	- Convergencia se controla con `max_iter` (máximo número de iteraciones) y `tol` (diferencia entre centroides en dos pasadas consecutivas)
- Complejidad O(n * k * i * d)
	- n puntos
	- K centros
	- i iteraciones
	- d dimensiones

- Solución a centroides iniciales
	- Correr K-means varias veces variando la semilla aleatoria y quedarse con el de menor SSE (no garantiza óptimo)
### Clustering Jerárquico
### DEBSCAN

## Conclusiones
