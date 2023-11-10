# KNN (K-Nearest Neighbors)

### KNN

KNN en espanol k vecinos mas cercanos, es un clasificador de <strong>aprendizaje supervisado</strong> que utiliza la proximidad para hacer clasificaciones o predicciones sobre la agrupacion de un punto de datos individual.

A pesar de ser un algoritmo sencillo dado que es basado en instancias, se utiliza para darle solicion a multitud de problemas, como en sistemas de recomendacion, busqueda semantica y deteccion de anomalias.

El algoritmo de KNN funciona a grandes rasgos de la siguiente manera:

1.- Calcula la distancia entre el item a clasificar y el resto de items del dataset de entrenamiento

2.- Selecciona los k elementos mas cercanos (con distancia menor segun la que se use en el algoritmo)

3.- Realiza una votacion de mayoria entre los k puntos mas cercanos, ahi es donde se decidira a que clase pertence.

Se recomienda que k sea impar, esto para evitar empates al momento de hacer la votacion.

El algoritmo en SciKit-Learn por default usa la distancia de Minkowski para el calculo de vecinos cercanos, sin embargo se puede modificaro con el parametro metric (Revisar documentacion)

### Algoritmo

En este repositorio se realiza un ejercicio de clasificacion con el Dataset reviews_sentiments.csv con la finalidad de mostrar de manera sencilla una aplicacion del algoritmo de KNN. 

Reviews_sentiments.csv es un dataset de resenas de un producto de google en el cual el usuario escribe su resena y otorga un numero de estrellas al producto.

Se usaran unicamente las variables continuas, estas se encuentran en las columnas wordcount, sentimentValue y Star Rating.

Lo que se espera lograr es que con los valores de wordcount y sentimentValue predecir el Star Rating (numero de estrellas otorgadas por el usuario al producto) de la resena.

Como primer paso haremos AED para ver como se ditribuyen los datos en sus cuartiles y los estadisticos mostrados del Dataset.

![AED](https://raw.githubusercontent.com/danielgpalma/Reviews_KNN/main/AED.png)

Hacemos la division del dataset.

Se realiza una normalizacion con StandardScaler, esto debido a que en el analisis exploratorio de datos observamos que los datos se asemejan a la normalidad, si no hubiera sido asi hubieramos optado tal vez por un MinMaxScaler.

Creamos y aplicamos el modelo de KNN, declaramos k como 5 en el parametro n_neighbors (Se explica porque se usa 5 mas abajo)

### Eleccion de K

Para elegir el mejor valor de K iteraremos k de 1 a 20 para poder apreciar el accuracy de cada una de las opciones.

![K Seleccion](https://raw.githubusercontent.com/danielgpalma/Reviews_KNN/main/K_Seleccion.png)


Como se puede observar en la grafica del notebook, tenemos que cuando se alcanza el mejor accuracy es con k = [5, 7, 10], por lo que con lo que ya sabemos, optamos por usar k = 5, debido a que una menor k implica menor costo de memoria y una k impar siempre es mejor que una k par para evitar el empate entre clases. 

### Resultados

En los resultados se obtiene un Accuracy con los datos de prueba del 86.5%, bastante bueno si supieramos que tenemos un dataset balanceado, sin embargo en el analisis exploratorio de datos podemos ver que nuestros datos no estan tan balanceados, lo cual nos lleva a explorar mas metricas de evaluacion.

En el reporte de clasificacion observamos que para la etiqueta 2, la precision no es tan buena, ya que solo el 40% de las muestras clasificadas con la etiqueta 2 son realmente Verdaderos Positivos.

Sin embargo, la columna que mayor informacion nos puede dar es el F1-Score, en la cual vemos que para la etiqueta 2 no tenemos un buen score, esto junto con lo anterior quiere decir que el modelo posiblemente clasifique datos con la etiqueta 2 pero que puede ser que sean Falsos Positivos.

![Matriz de Confusion](https://raw.githubusercontent.com/danielgpalma/Reviews_KNN/main/confuion_matrix.png)

Observamos la matriz de confusion en la cual vemos muy bien expresado el problema con la etiqueta 2, en la cual vemos que clasifica mas datos con la etiqueta 2 que los que son.

Como prueba final, graficamos las resenas para observar donde se distribuyen dependiendo de su numero de estrellas, numero de palabras y valor del sentimiento.

![Distribucion de Resenas](https://raw.githubusercontent.com/danielgpalma/Reviews_KNN/main/resultado.png)

Al observar la grafica podemos notar como se agrupan las resenas segun su clasificacion, por lo que podemos deducir que una resena de 20 palabras y un valor del sentimiento de 1 nos daria una clasficiacion de 4 estrellas.

Se llevo a la practica y efectivamente nuestro modelo predijo que una resena de 20 palabras y valor del sentimiento de 1 corresponde a una resena en la que el usuario daria 4 estrellas.
