# Introducción

Minería de Datos: Extrae conocimiento a partir de datos.

Métodos automáticos o semiautomáticos.

Encontrar patrones y estructuras relevantes.


Ciencia de datos: Análisis de datos para extraer conocimiento. Genera entendimiento.
Aprendizaje automático: Algoritmos para predecir. Genera predicciones.
Inteligencia Artificial: Sistemas que puedan realizar tareas inteligentes de manera autonoma. Genera acciones.

Pandas:
	DataFrame: Tablas
	Series: Columnas.

Leer.
Filtrar, agrupar y transformar.
Crear resúmenes estadísticos.

Para cargar y preprocesar antes de ML.

Numpy
Matplotlib
Scikit-Learn
Pandas
Jupyter Notebook
Keras


Métodos:
	Clasificacón: Predecir etiquetas. Discretas
	Regresión: Predecir valor. Continuo.
	Clustering: Agrupar. Sin etiquetas.
	Reducción, detección, etc.

Clasificación:
	Reconocimientos de emociones en el habla.
	Clasificacion de especies animales.
	Deteccion de tumores en imagenes médicas.

Regresión:
	Reconocer intensidad de una emoción.
	Evaluar daños tras un terromoto.
	Medir la severidad de Alzheimer.

Clustering:
	Topic mining: Descubrir de qué hablan.
	Detección: De desinformación en redes.
	Segmentación: De clientes, según preferencias.

# Datos

Document -> Features vector -> Predictive Model -> Expected Label

Objetivo de muchos métodos de ML: Detectar estructuras o patrones.

Se necesita información en forma de vectores númericos.

Tendremos que extraer representaciones cifradas que describan lo más relevante posible de cada ejemplo.
	Trasnformar texto a vector de frecuencia de palabras.
	Medir histograma de colores de imagen
	Recopilar atributos de tabla

Aprendizaje supervisado:
	Necesitamos también etiquetas o valores de salida.
	Features: Lo que describe al ejemplo
	Etiqueta: Variable que se quiere predecir (Valor).
	Modelo: Aprenderá parámetros para predecir etiqueta a partir de features.

Cuantitativos: Numéricos. Precisos pero dificil interpretacion.
Cualitativos:  Mas interpretables pero menos detalle.
		Categóricos: Mediciones, contaje.
		Nominales(categóricos sin orden o valor cuantitativo entre ellas) u
		 Ordinales(datos catégoricos con jerarquía y diferencias no medibles.).

Estructurados: Tablas
No estructurados: Requieren vectorización(Texto, audio, imágenes). Para aplicar algoritmos de ML.

Podemos comparar similitudes y diferencias entre vectores:
	![[Pasted image 20250828185731.png]]

En cuanto a calidad, los datos reales están lejos de ser perfectos.

Ruido:  Irregularidad aleatoria en los datos, no explicadas por el modelo. Inevitable e imprevisibles.
	Errores: De medición o muestreo, que distorsionan.
	Residuos: Variación intrínseca no capturada.
	Representamos vectores finitos, aproximados a la realidad.
	Se queda componente de ruido que no podemos modelizar.

Outlier: Valor atípico.
	Ruidosos: Datos erróneos o, extremos por variabilidad natural.
	Distorsionan estimaciones estadísticas. (Media)
	Útiles: Responden a eventos raros que sí queremos detectas.
		Identificarlos:
			Visualización
			Métodos estadísticos
			Algoritmos ML
			Validación de Dominio: Comprobar si es auténtico.

Valores faltantes:
	Eliminar filas: Si son pocas
	Imputar valores (Sustituir)
	Modelos que los manejen

Datos duplicados:
	Puede generar sobrepresentación y con esto, un sesgo en el entrenamiento
	Mitigarlos:
		Comparar hashes o firmas
		Clustering de similitud de ejemplos
		Herramientas de deduplicación
	Es crucial deduplicar dataset grandes.

Use-case:LLM (Modelo de lenguaje grande)
	Datos de web:
		Ruido 

Limpieza y preprocesamiento:
Estandarizacion y normalizacion:
	Features en escalas comparables
	Estandarizacion: 
		Media cero y varianza uno
		Distribucion centrada en 0 y desviacion estandar 1 (En promedio los valores se alejan 1 unidad de la media)
	Normalización:
		Ajusta vector para que norma sea 1.
		Evaluar dirección
	Scaling:
		Se comprime con: ![[Pasted image 20250828192301.png]]
		Se aleja de forma gaussiana (mayoria datos concentran en valor medio y frecuencia baja a medida que se alejan del centro) y escala finita.

Evitar que atributos dominen a otros
Favorecer convergencia de algoritmos de opotimizacion
Mejora calidad de metodos

Discretizacion:
Dividir atributos continuos en bins(clases).
Modelo más expresivo, manteniendo interpretabilidad.

Polynomial Features:
Para incrementar complejidad de un modelo.

Sampling(muestreo)
	Muestreo estratificado: Mantiene proporciones de clases o grupos.
	Aleatorio simple: Elegir instancias al azar.
	Sistemático: Tomar cada k-ésimo elemento, desde punto aleatorio.

Agregaciones de datos: Combinar valores en uno. (media diaria)
	Reduce ruido y variabilidad
	Simplifica conjuntos
	Resume grandes volumenes.

Dimensión: Cursa y reduccion: Muchas dispersión
	Reduccion de dimension
	Eliminar o fusionar atributos irrelevantes
	Acelerar procesamiento y mejorar interpretabilidad

Análisis Exploratorio de Datos:
Características más importantes.
Dos criterios:
	Estadísticas de resumen
	Visualización de datos

Categoricals: Variables categóricas en estadísticas. 
Estadísticas de resumen: Valores que explican propiedades. Icluyen frecuencias, medidas de tendencia central y dispersión.

Frecuencia: cantidad de veces que valor de atributo es observado.
Pandas:
	serie.value_counts()
	porcentual: (serie.value_counts(normalize=True) \*100).round(2)

Moda: Valor mas frecuente observado.
dataframe.mode()

Tendencia central: Resumir valores en un único valor asociado al valor localizado en el centro.
	Media (mean): Media aritmética
		Muy sensible a outliers
		Media truncada(trimmed mean): Eliminar fracción de valores extremos.
		scipy.stats.trim_mean(vec, 0.1): Descartamos 10% de valores extremos.
	Mediana(median): Posición central. Impar: Valor justo en centro; Par: Promedio valores centrales.
	Percentiles: k-esimo percentil: un valor tal que k% observaciones por debajo y 100-k% sobre.
	Cuantiles: fracciones en vez de porcentajes. Generalmete se usan estos.
		pandas: quantile(\[i/100 for i in range(101)])
	Cuartiles: Q1 k=25, Q2 k=50(mediana), Q3 k=75.
		 .quantile(\[0, 0.25, 0.5, 0.75, 1])
		 groupby: filas

Medidas de Dispersión:
	Qué tan distintas o similares respecto a un valor particular.
	Gralmente, valor particular es una medida de Tendencia central.
	Rango: Dif(max-min)
	Desviacion estandar(sd): Raiz cuadrada de la varianza (var(x)) que mide las diferencias cuadradas promedio de las observaciones con respecto a la media. (se divide por m-1)
	![[Pasted image 20250829000430.png]]
		Sensible a outliers.
		series.var()
		series.std()
	Más robustas se basan en la mediana.
	Desviación absoluta promedio (average absolute deviation AAD): promedio m valores de x con respecto a una m(x) medida de tendencia central.
	![[Pasted image 20250829000419.png]]
	Desviación mediana absoluta o median absolute deviation(MAD): b cte de escala \* mediana entre x y una medida de tendencia central
		scipy.stats.median_abs_deviation
	Rango intercuartil: Diferencia entre Q3 y Q1

E. de Resumen Multivariada: Comparar una variable cr a otra.
	Covarianza: Grado variación lineal de un par de variables.
	![[Pasted image 20250829001018.png]]
		series.cov(series2)
	Matriz covarianza
		dataframe.cov(): dataframe de variables númericas
		matriz simétrica
	Independencia => Covarianza igual a 0
	Correlación lineal, medida de relacion que no dependa de la escala de la variable.
	![[Pasted image 20250829135211.png]]
	Correlación entre 1 y -1:
		1:  Variable crece la otra también en proporción
		-1: Relacion inversa
		0: No implica que no hay relacion no lineal entre variables.
		pandas: series.corr(); dataframe.corr(): Matriz correlaciones

Tablas de contingencia: Relación entre var. categóricas.
Valores son frecuencias de co-ocurriencia entre todos los pares.
pd.Categorical(Series)
	pd.crosstab(Series1, Series2)

Visualización
	Reconocer patrones o tendencia.
Para graficar: matplotlib.pyplot as plt
plot: línea; atributo 'g--': discontinua verde
	plt.figure(figsize(x,y))
	plt.title
	plt.xlabel
	plt.ylabel
	plt.show

scatter: puntos

Histogramas: Dist. de val de una var.
División por contenedores(bins), grafico de barra por cada bin.
	pls.hist

Densidad:
	Versión suavizada de histograma.
	gaussian_kde de scipy y luego se visualizan con plt
		from scipy import stats
		stats.gaussian_kde(val)

Grafico de torta:
	Participación proporcional a su frecuencia relativa
	Gralmente. en var. categóricas.
	No se recomienda, puede entregar info. engañosa.
	plt.pie

Boxplots
	Se construyen a partir de percentiles.
	Rectángulo entre el primer y tercer Cuartil
	Altura del rectangulo es el rango intercuartil
	Mediana divide el rectangulo.
	Recta inf: Q1-1.5\*RIC
	Reca sup: Q3+1.5\*RIC
	Valores más extremos que el largo de los brazos: atípicos
	Para ver la simetría de la distribución de los datos.
		Mediana no en el centro => Dist. no simétrica.
		Y valores atípicos u outliers
		plt.boxplot
	Un boxplot para cada valor cr a otra var. numérica
	Varios boxplot en un mismo gráfico.
		data_to_plot=\[a,a2,a3]
		plt.bloxplot(datatoplot, patch_artist=True) #patch_artist para poder decorar las cajas
	plotly:
		fig=go.Figure()
		fig.add_trace(go.Box(y=, name=, marker_color=))
		fig.update_layout(
			title=
			yaxis_title=
			boxmode='group' //agrupar juntar las cakas para los diferentes trazos.
		)

Plot: Gralmente. gráficos estáticos; Plotly: Interactivos y de internet.
Diagrama de dispersión
Dos var. numéricas.
Val atributos determinan posición de elementos.
	plt.scatter(x,y)
plotly:
	fig=px.scatter(dataframe, x=, y=)
Todos los pares de valores para cada especie (sgn color)
fig=px.scatter_matrix(df,
	dimensions=\[atributos],
	color='species',
	symbol='species',
	title=
)
scatterplot 3 dimensiones:
	importar mpl_toolkits.mplot3d
	for s, c, m in zip(especie, colors.value(), markers.value()):
		ax.scatter(x,y,z, c=c, marker=m, label=s)

Gráficos de Coordenadas paralelas:
	datos multidimensionales.
	en vez de xyz ocupamos varios ejes paralelos entre sí.
	atributo representado por un eje paralelo respectivo a sus atributos.
	valores escalados para eje misma altura.
	objetos similares se agrupan en líneas con trayectoria similar.
		parallel_coordinades en pandas.
		pd.plotting.parallel_coordinates(data, 'Species', colormap=plt.get_cmap("Set1"))
Gráfico de estrellas:
	Cada ejemplo como estrella
	Var. como eje que parte en el centro de la estrella.
	Valor de cada variable se representa mediante línea o segmento que conecnta el centro con el punto correspondiente en el eje.
		Tamaño línea refleja valor reescalado var.
	Para comparar objetos o detectar valores atípicos.


Intro aprendizaje supervisado
Modelo aprenderá sus propios parámetros utilizando ejemplos y etiquetas asociadas.

Generalidades:
	Doc a vectores, para optimización
	Aprende parametros sobre conjunto de entrenamiento
	Para predecir etiquetas de nuevos datos
	Doc puede ser: audio, texto, imagen, video, ...

Para entrenamiento:
	1. Tener datos etiquetados
		Conjunto de tamaño n: Dn={(Doc_i, Y_i)}, con Doc_i  es una muestra e Y las etiquetas.
	2. Extraer descriptores: Transf. documentos en vectores.
	3. Crear modelo matemático f_theta tal q f_theta(X) esté cerca de Y (para regresión)
		Theta es conjunto parámetros del modelo
	4. Implementar una función de costo (error) l a minimizar.
		Mientras más se equivoque el modelo, mayor costo
		Se desea tener costo pequeño
	5. Encontrar parametros Theta de manera que l(f(Xi), Yi) sea pequeño
	6. Probar f_theta (theta obtenido de 5) en nuevos datos.

Aprendizaje:
	Datos etiquetados
	Extraccion de características
	Modelo f_theta
	Funcion de costo
	Algoritmo de optimización
	Métrica de evaluación

Función de costo: 
Penaliza modelo cuando comete errores.
Queremos optimizar pesos del modelo para obtener valor minimo de este costo.
![[Pasted image 20250829150430.png]]
	Sobre el conjunto de entrenamiento.
Expresa error desde perspectiva numérica
Transmite algoritmo de aprendizaje
Debe ser convexa (q se pueda optimizar eficientemente). 

Complejidad de los modelos y sobre/soto-aprendizaje
R(fsg)-R(f)= R(fs\*)-R(f\*) + R(fsg)-(Rfs\*) = Error aproximación + Error de estimación
fsg=f_s gorrito = satisfactorio utilizando datos de entrenamiento
f\* = mejor solución; S: clase de funciones utilizadas como modelos.
Error aproximación grande si S no es adaptado y de estimación grande si modelo es complejo.

Soto-aprendizaje: Pocos parámetros, imposible estimar bien
Sobre-aprendizaje: Demasiados parámetros, memoriza el ruido de ensamble de entrenamiento.

Regularizacion y parsimonia:
	Para no generalización, permite agregar penalización en relación con la complejidad del modelo.
		Gralmente. se usa la norma de los pesos (valores numéricos de cómo las caract. de entrada influyen en los resultados) del modelo. Disminuyendo esta.
		AIC: no convexa, parsimoniosa(explicado de forma sencilla, no interpretado mediante explicaciones complejas), poco utilizada
		Ridge: Convexa, no parsimoniosa
		Lasso: Convexa, parsimoniosa
		Elastic Net: Convexa, parsimoniosa
Optimizacion, loss landscape:
	Converger parametros para encontrar los q den costo minimo de entrenamiento.
![[Pasted image 20250829152053.png]]
Valor costo empirico en un eje, parametros en otro: Loss landscape
Ollos significan parametros que dan error pequeño.

Gradiente descendiente:
Derivada en cada dimensión. Aproximación lineal de la función al nivel loca.
Luego de calculo de costo se calcula el gradiente de esta para actualizar parámetros.

Metricas
	Tipos de errores:
		Clasificador binario: TP, FP, FN, TN.
		Con esto se crea matriz de confusión: Etiquetas en un eje y predicciones en otra.
			Si da matriz diagonal, predicciones perfectas.
	Tipos de metricas y costos:
		Accuracy: (TP+TN)/(TP+FP+TN+FN)
		Recall: TP/(TP+FN) positivos reales se clasificaron como positivos
		Precision: TP/(TP+FP) predicciones positivas correctas
		F1 = 2TP/(2TP+FP+FN)
Agregación:
	A nivel de clase:
		Macro-averaging: Computar métrica para cada clase (especies) y luego promediar.
		Micro-averaging: Crear matriz de confusión para cada clase, combinarlas y luego evaluar.
		Weighted-averaging: Computar metrica para cada clase y luego promediar usando pesos.

ROC & AUC
Umbral de discriminación (T) superior a 0.5 clasificador bueno.
Receiver Operating Characteristics: Curva representando la performancia de un clasificador en varias situaciones. Para cada valor de umbral si calcula la matriz de confusión.

Area Under Curve único valor que representa calidad de curva. Mayor, mejor.

Regresion
	Evaluar las distancias y si el modelo representa bien la varianza de datos.
		Calculos de errores
		Coef. de determinacion representa proporcion de varianza explicada.

Técnicas de evaluación
Validacion cruzada (cross-validation):
	Mejor estimacion de perfomancias del modelo. V experiencias, cortando el dataset en V partes, entrenar sobre V-1 y testear sobre 1. 
	Para obtener hiperparametros óptimos antes de entrenamiento.

Conjunto validacion y prueba (Holdout)
Si es imposible cross-validation, crear set de entrenamiento, de validación y de test.

Tamaño de participación:
	Es interesante tener un modelo bueno usando pocos datos.
	Rendimiento mas variable y bajo con pocos datos.
	Evaluacion mas confiable con mas datos de set.


[[ Clase 5 ]]