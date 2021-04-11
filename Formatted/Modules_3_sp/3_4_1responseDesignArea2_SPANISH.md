# Análisis de datos de muestra 

## 1. Contexto

En los tutoriales anteriores, diseñamos y extrajimos una muestra del país de Colombia, y observamos y registramos las condiciones de cobertura del suelo de referencia en las ubicaciones de las unidades de muestra. La recopilación de observaciones de referencia se denomina resultados o datos de la muestra, o clasificación de referencia. En este tutorial aplicaremos varios estimadores a los datos de la muestra para estimar las características de la población que muestreamos, es decir, características del país de Colombia, como el área de perturbación forestal. Un estimador es “La regla por la cual una estimación de alguna característica de la población [es decir, parámetro] *μ* se calcula a partir de los resultados de la muestra ”(Cochran, 1977, p. 11) [^ fn1]. Tenga en cuenta que un estimador no es lo mismo que una estimación, sino que "un estimador es una función de la muestra, mientras que una estimación es el valor realizado de un estimador (es decir, un número) que se obtiene cuando una muestra es realmente tomado ”(Casella & Berger, 2002, p. 312) [^ fn2]. Un estimador tiene dos propiedades importantes: varianza y sesgo. El sesgo de un estimador *μ ^* de un parámetro de población *μ* es la diferencia entre *μ* y el valor esperado de *μ ^* en todas las muestras posibles; es decir, ![](https://latex.codecogs.com/gif.latex?\inline&space;\textup{Bias}(\hat{\mu})&space;=&space;\textup{E}(\hat{\mu})&space;-&space;\mu) (Casella & Berger, 2002, p. 330)[^fn2]  Si  ![](https://latex.codecogs.com/gif.latex?\inline&space;\textup{Bias}(\hat{\mu})&space;=&space;\textup{E}(\hat{\mu})&space;-&space;\mu=0), entonces se considera que el estimador es insesgado. Tenga en cuenta que debido a que una estimación es un número, no tiene varianza ni sesgo y, por lo tanto, no puede ser insesgado.

La otra propiedad importante de un estimador es la varianza. La definición formal de la varianza proporciona “una medida del grado de extensión de una distribución alrededor de su media” (Casella y Berger, 2002, p. 59) [^ fn2]. Esta definición no es muy útil en nuestro contexto, en cambio, nos preocupan las situaciones en las que hemos muestreado un área de estudio para estimar un determinado parámetro de población (por ejemplo, el área de bosque o deforestación). Por ejemplo, si tenemos una población de la que se ha seleccionado una muestra de, la varianza de la muestra es *s^2^* y se calcula fácilmente para diseños de muestreo comunes. Pero la varianza de la muestra es menos interesante en comparación con la varianza de un estimador. Para diseños comunes, podemos probar fácilmente que la varianza muestral *s^2^* es un estimador insesgado de la varianza poblacional *S^2^* (Cochran, 1977, p. 22, 26) [^ fn1]. La varianza de un estimador  *u^*  es ![](https://latex.codecogs.com/gif.latex?\inline&space;\textup{V}(\hat{\mu})&space;=&space;S^2&space;\div&space;n) (asumiendo un tamaño de muestra pequeño, *n*, relativo al tamaño de las poblaciones, *N*); la varianza estimada de *u^* sustituye la varianza de la muestra *s^2^* por la varianza de la población *S^2^* para crear el estimador de varianza de *u^*   cuando![](https://latex.codecogs.com/gif.latex?\inline&space;\hat{V}(\hat{\mu})&space;=&space;s^2&space;\div&space;n) que es el estimador de varianza de mayor interés para nosotros, ya que nos permite cuantificar la incertidumbre en cosas como los datos de actividad u otros parámetros de interés.

A partir de aquí, podemos introducir dos medidas de propagación más importantes: el error estándar y el intervalo de confianza. El error estándar es la desviación estándar (es decir, raíz cuadrada de la varianza) de un estimador (Rice, 1995, p. 192)[^fn3] y por lo tanto tiene la misma unidad que la estimación. La desviación estándar de un estimador se conoce como su error estándar. Debido a que la varianza muestral es un estimador insesgado de la varianza poblacional, podemos estimar el error estándar usando la varianza muestral: ![](https://latex.codecogs.com/gif.latex?\inline&space;\textup{SE}(\hat{\mu})&space;=&space;\hat{V}(\hat{\mu})&space;\div&space;\sqrt{n}). Tenga en cuenta que debido a que un error estándar es una desviación estándar de un estimador, todos los errores estándar también son desviaciones estándar, pero no todas las desviaciones estándar son errores estándar. Esto a veces causa confusión a pesar de que las definiciones de error estándar y desviación estándar son consistentes. Normalmente, ni la varianza ni el error estándar se utilizan para expresar la incertidumbre en las estimaciones; en cambio, se suele utilizar un intervalo de confianza: "Un intervalo de confianza del 95% para *μ* es un intervalo aleatorio que contiene *μ* con probabilidad de 0,95; si tomáramos muchas muestras aleatorias [bajo el mismo diseño de muestreo] y formáramos un intervalo de confianza de cada una, aproximadamente el 95% de estos intervalos contendrían *μ* " (Rice, 1995, p. 217)[^fn3]. Intervalos de confianza frecuentemente están en la forma ![](https://latex.codecogs.com/gif.latex?\inline&space;\hat{\mu}&space;\pm&space;a\times\textup{SE}(\hat{\mu})) donde *a* es una estadística relacionada con el nivel de confianza deseado, denominado puntuación z (z-score) o puntuación estándar expresada como un porcentaje entre 0 y 100%. Para un cierto nivel de confianza *p*, el área bajo la función de densidad normal estándar de *-z* a *+ z* es *p* (Rice, 1995, p. 202)[^fn3]; por ejemplo, un intervalo de confianza en el nivel de confianza del 95% corresponde a una puntuación z de 1.96 (a menudo se redondea a 2). Una condición para utilizar una puntuación z para calcular un intervalo de confianza es que la distribución muestral sea aproximadamente una distribución normal, lo que podemos suponer para tamaños de muestra grandes. El intervalo de confianza dividido por la estimación se denomina margen de error (*MoE*) y, a menudo, se expresa como porcentaje.

Las dos propiedades, sesgo y varianza, son importantes porque podemos asegurarnos de que el estimador que utilizamos sea insesgado y podemos expresar la incertidumbre en estimaciones. Tampoco es posible cuando se utiliza el recuento de píxeles en mapas o cuando se toman muestras sin adherirse al muestreo probabilístico. Otro aspecto importante de un estimador es que es una función de la muestra, lo que significa que el estimador debe corresponder al diseño muestral. Por ejemplo, la media muestral es un estimador insesgado de la media poblacional para muestreo aleatorio simple; para el muestreo aleatorio estratificado, necesitamos utilizar un estimador estratificado que se expresa como la suma de las medias de las muestras aleatorias simples dentro de los estratos ponderados por los pesos de estrato.



## 2. Análisis de resultados de muestra recopilados bajo SRS/SYS 
Los resultados de la muestra recopilados con muestreo aleatorio simple son los más sencillos de analizar (se utilizan los mismos estimadores tanto para el muestreo aleatorio simple como para el sistemático). Debido a que no se utilizan mapas / estratificaciones y debido a que la media de la muestra es un estimador insesgado de la media de la población, el análisis de los resultados de la muestra de SRS / SYS se puede completar fácilmente en una hoja de cálculo. El muestreo aleatorio estratificado se ilustró en tutoriales anteriores, y aquí solo se proporcionan datos ficticios para ilustrar la construcción de estimadores SRS / SYS. Supongamos que los datos de esta hoja de cálculo son mapas y etiquetas de referencia en ubicaciones seleccionadas en SRS: https://docs.google.com/spreadsheets/d/1pcK-rlhUo5lvmYqibT4zIv-bR5tF4Uu8DqPwIG8mJWQ/edit?usp=sharing El tamaño de la muestra es *n* = 100, y una etiqueta de 1 es perturbación del bosque, 2 es bosque, y 3 es no bosque.        

Debido a que la media muestral es un estimador insesgado de la media poblacional, el cálculo de las proporciones del área es sencillo; defina *y_i* = 1 si se observó alteración del bosque en la ubicación de la muestra *i* y 0 en caso contrario; el área de perturbación del bosque viene dada por (Cochran, 1977, p. 22)[^fn1]:

![](https://latex.codecogs.com/svg.latex?\Large&space;\hat{y}=\frac{1}{n}\sum_{i=1}^{n}y_i)


En la hoja de calculo, escriba en la célula C1 "y_i" y en C2 "=if(B2=1,1,0)" y extiéndalo a la célula C101. Debería de ver: 

| | A             | B            | C  |D     |E   
|-|:--------------|:-------------|:------|:------|:---|
|1| Mapa     | Ref.          | y_i   |         |    |
|2| 2             |  2             | 0     |          |    |
|3| 2             |    2           | 0     |	      |    |
|4| 1             |    1           | 1     |          |    |
|5| 2             |    2           | 0     |          |    |

En célula D1, escriba *Area dist. bosque*, y en D2 "=sum(B2:B101)/100" para construir un estimador SRS y aplicarlo a los resultados de muestra. Debería de ver:

| | A             | B            | C     |D        |E   
|-|:--------------|:-----------|:------|:----------------------|:---|
|1| Map       | Ref.        | y_i  | Area para dist.  |    |
|2| 2             |  2           | 0     | 0.14                    |    |
|3| 2             |    2         | 0     |	                         |    |
|4| 1             |    1         | 1     |                             |    |
|5| 2             |    2         | 0     |                             |    |


Ahora calculemos el margen de error en el estimado de área. El estimador de varianza SRS es (Cochran, 1977, p. 26)[^fn1]

![](https://latex.codecogs.com/svg.latex?\Large&space;\hat{V}(\hat{y})=\frac{s^2}{n}&space;=&space;\frac{\sum&space;(y_i-\bar{y})^2}{n(n-1)})

Para aplicar el estimador de varianza a la hoja de calculo, escriba en célula D3 "Varianza", y en célula D4  "=sum(ArrayFormula((C4:C103-D24)^2))/(100 * 99)" para aplicar el estimador de varianza; debería de regresar 0.001414. Ahora escriba "Error Estándar" en D5, y en D6: "=sqrt(C4)"; escriba "95% CI" en D7 y en D8: "=1.96*D6". Finalmente escriba "Margen de error" en D9 y en D10 "=D8/D2":

| | A             | B            | C     |D        |E   
|-|:--------------|:-------------|:------|:--------|:---|
|1| Mapa     | Ref.        | y_i   |Área dist. bosque    |    |
|2| 2             |  2           | 0      | 0.14                        |    |
|3| 2             |    2         | 0      |Varianza	             |    |
|4| 1             |    1         | 1      | 0.001414               |    |
|5| 2             |    2         | 0      |Error Estándar      |    |
|6| 2             |    2         | 0      |  0.0376                  |    |
|7| 2             |    2         | 0      | 95% CI                   |    |
|8| 1             |    1         | 1      | 0.0737                   |    |
|9| 2             |    1         | 1      | Margen de error |    |
|10| 2            |    2        | 0      | 53%                       |    |

Ahora hemos estimado el área de perturbación forestal usando una muestra de 100 unidades recolectadas bajo SRS como 0.14 + - 0.074 correspondiente a un margen de error del 53%. Tenga en cuenta que no se utilizó la información del mapa de la columna A.

Por último, calculemos la precisión del mapa, comenzando con la precisión general: escriba "Prec. general". en la celda E1 y en E2 "= CONTAR.SI (A2: A101, B2: B101) / 100": esta expresión contará el número de instancias en las que el mapa y las etiquetas de referencia coinciden y se dividen por el tamaño de la muestra. La precisión general es la proporción total de área correctamente clasificada.

En célula F1 escriba "Prec. Usuario Dist." y en F2 "=countifs(A1:A101,"1",B1:B101,"1")/countif(A1:A101,1)"; la precisión de usuario de la clase de un mapa “es la probabilidad condicional de que un área clasificada como categoría i por el mapa sea clasificada como categoría i por los datos de referencia” (Stehman, 1997, p. 79):

Finalmente, en celula G1 type "Prec. Prod. Dist." y en G2 "=countifs(A1:A101,"1",B1:B101,"1")/countif(B1:B101,1)"; la precisión del productor de una clase de mapas "La probabilidad condicional de que un área clasificada como categoría j por los datos de referencia sea clasificada como categoría j por el mapa" (Stehman, 1997, p. 79).

| | A             | B            | C     |D        |E           |F             |G
|-|:--------------|:-------------|:------|:--------|:-----------|:-------------|:------------|
|1| Mapa      | Ref.        | y_i   | Area FD            |Prec. gen.|Prec. Usuario Dist.|Prec. Prod. Dist.|
|2| 2             |    2         | 0     |0.14                      | 0.65         |0.80                       |0.86                 |
|3| 2             |    2         | 0     |Varianza                |                  |                               |
|4| 1             |    1         | 1     |0.001414               |                  |                               |
|5| 2             |    2         | 0     |Error Estándar     |                  |                               |
|6| 2             |    2         | 0     |0.0376                   |                  |                               |
|7| 2             |    2         | 0     |95% CI                   |                  |                                |
|8| 1             |    1         | 1     |0.0737                   |                  |                                |
|9| 2             |    1         | 1     |Margen de error |                  |                                 |
|10| 2           |    2         | 0     |53%                       |                  |                                 |


## 3. Estimación estratificada 
Al analizar la muestra de SRS en el ejemplo anterior, no se utilizaron datos de mapas. Si bien un muestreo aleatorio simple facilita la selección y el análisis de la muestra, podemos obtener una ganancia en precisión en las estimaciones si estratificamos el área de estudio antes de extraer la muestra. En particular, si los estratos se definen para corresponder a subpoblaciones que son homogéneas, en el sentido de que las características de la población "varían poco de una unidad a otra, se pueden obtener estimaciones más precisas de la media de cualquier estrato a partir de una pequeña muestra en ese estrato" (Cochran, 1977, pág. 89) [^ fn1]. En el tutorial CODED, se produjo un mapa que categorizó el paisaje en perturbación forestal y bosque estable y no bosque. Si estamos interesados en una estimación del área de la perturbación del bosque, el uso del mapa que produjimos, siempre que sea preciso, debería permitirnos producir una estimación precisa a partir de una muestra relativamente pequeña en ese estrato.

Cuando se usa un mapa para estratificar la región de estudio bajo un muestreo aleatorio estratificado, es común y conveniente presentar los resultados de la muestra en una matriz de error (también llamada matriz de confusión o contingencia). Una matriz de error es una tabulación cruzada de las observaciones de referencia y las etiquetas del mapa en las ubicaciones de las muestras. Hay varias formas de crear una matriz de errores. Por ejemplo, considere la siguiente hoja de cálculo que se creó en el tutorial de selección de muestra; las etiquetas del mapa en las unidades de muestra están en la columna del mapa, y supongamos que hemos recopilado observaciones de referencia que se registran en la columna de referencia: https://docs.google.com/spreadsheets/d/1-Z2LmLmwfxlVHwezO9N74P7GjfN_y0gjxUblKTfmCc8/edit?usp=sharing 

Los códigos son 
1: bosque estable
2: estable no-bosque
3: disturbio del bosque
4: amortiguación en el bosque alrededor del disturbio del bosque

En filas 1 a 8 y columnas E a K, cree la siguiente matriz: 

| | A    | B   | C    |D |E      |F        |G         |H         |I        |J            |K     |L       |
|-|:-----|:----|:-----|:-|:------|:--------|:---------|:---------|:--------|:------------|:-----|:------|
|1| ID  | Mapa | Ref. |  |*Muestra*|*count* |*error*   |*matriz*  |         |             |       |      |
|2| 1    |  1  | 1    |  |      |          | R        |E         |F.       |             |       |      |
|3| 2    |  1  | 1    |  |      |          | Bosque | No-bosque |Dist. Bosque| Amortiguamiento |Total  |*Wh*  |
|4| 3    |  4  | 1    |  |  M   |Bosque    |          |          |         |             |       |      |
|5| 4    |  3  | 3    |  |  A   | No-bosque       |          |          |         |             |       |      |
|6| 5    |  1  | 1    |  | P    |Dist. Bosque |          |          |         |             |       |      |
|7| 6    |  2  | 2    |  |      |Amortiguamiento    |          |          |         |             |       |      |
|8| 7    |  1  | 1    |  |      |Total     |          |          |         |             |       |      |

Primero, agregue los pesos de los estratos del tutorial de diseño muestral (0.551, 0.407, 0.0137, 0.0287). En la celda G4, ahora queremos calcular la cantidad de unidades en la muestra que mapeamos como bosque y también observamos como bosque en los datos de referencia; lo hacemos con la siguiente expresión: "= countifs (B1: B536,"1", C1: C536,"1")". Rehaga el cálculo para no-bosque en la celda H5 pero cambie el "1" a "2"; y luego nuevamente en las celdas I6 y J7. En la celda H4, queremos calcular la cantidad de unidades de muestra que se mapearon como bosque pero se observaron como No-bosque en los datos de referencia; especifique en la celda H4 "= countifs (B1: B536,"1", C1: C536, "2") ". Rehaga el cálculo para todas las celdas restantes cambiando el código de acuerdo con la posición de la celda; y sumar los totales. Esto debería dar la siguiente matriz:


| | A    | B   | C    |D |E      |F        |G         |H         |I        |J       |K        |L      |
|-|:-----|:----|:-----|:-|:------|:--------|:---------|:---------|:--------|:-------|:--------|:------|
|1| ID  | Map  | Ref. |  |*Error*|*matriz* |          |          |         |        |         |       |
|2| 1    |  1  | 1    |  |*muestra*| *cuentas* | R       |E         |F.       |        |         |       |
|3| 2    |  1  | 1    |  |      |          | Bosque |No-Bosque|Dist. Bosque| Amortiguamiento |Total    |*Wh*   |
|4| 3    |  4  | 1    |  |  M   |Bosque    |271       | 3        | 1       |0       |275      |0.551  |
|5| 4    |  3  | 3    |  |  A   |No-Bosque| 6        |193       | 1       |0       |200      |0.407  |
|6| 5    |  1  | 1    |  | P    |Dist. Bosque | 2        |1         | 27      |0       |30       |0.0137 |
|7| 6    |  2  | 2    |  |      |Amortiguamiento    | 23       |0         | 7       |0       |30       |0.0287 |
|8| 7    |  1  | 1    |  |      |Total     | 302      |197       | 36      |0       |535      | 1     |

Algunas cosas interesantes a tener en cuenta aquí: no hay observaciones de referencia de Amortiguamiento porque obviamente no estamos observando unidades como "amortiguamiento". Es importante que ahora hemos estimado el número de errores en el mapa; tenemos un error de cada disturbio de bosque omitido en los estratos forestales y no forestales, y siete en el estrato de amortiguamiento. También tenemos dos errores más uno de disturbio de bosque cometido.

Debido a que muestreamos Colombia con un muestreo aleatorio estratificado, la media ya no es un estimador insesgado de la media de la población a menos que necesitemos tener en cuenta las ponderaciones de los estratos. Por lo tanto, es más útil expresar la matriz de errores como proporciones de área en lugar de conteos de muestras. Para hacer esto, copie la matriz de error en la fila 10 pero deje las celdas vacías:

| | A   | B  | C |D |E      |F        |G         |H         |I        |J       |K        |L      |
|-|:----|:---|:--|:-|:------|:--------|:---------|:---------|:--------|:-------|:--------|:------|
| 9|  8 |  2 | 2 |  |       |         |          |          |         |       |         |       |
|10|  9 |  2 | 2 |  |*Error*|*matriz* |          |          |         |       |         |       |
|11| 10 |  2 | 2 |  |área|*proporciones*| R     |E         |F.       |       |         |       |
|12| 11 |  3 | 3 |  |      |          | Bosque |No-bosque|Dist. Bosque| Amortiguamiento |Total    |*Wh*   |
|13| 12 |  1 | 1 |  |  M   |Bosque    |          |          |         |       |         |0.551  |
|14| 13 |  1 | 1 |  |  A   |No-bosque|          |          |         |       |         |0.407  |
|15| 14 |  1 | 1 |  | P    |Dist. Bosque |          |          |         |       |         |0.0137 |
|16| 15 |  2 | 2 |  |      |Amortiguamiento    |          |          |         |       |         |0.0287 |
|17| 16 |  3 | 3 |  |      |Total     |          |          |         |       |         | 1     |


Las proporciones de área estimadas de una celda perteneciente al estrato *h* y observada en los datos de referencia como *j* es (*h+* denota una suma entre columnas; por lo tanto, *n<sub>h + </sub>* significa el tamaño de la muestra asignado al estrato *h*)

![](https://latex.codecogs.com/gif.latex?\Large&space;\hat{p}_{hj}&space;=&space;W_h&space;\frac{n_{hj}}{n_{h&plus;}})

Para estimar las proporciones de área, escriba en G13: "=$L12*G4/$K4" y expándalo a J13. Rehaga la calculación para las filas, lo cual debería de dar la siguiente matriz:  

| | A   | B  | C |D |E      |F        |G         |H         |I        |J       |K        |L      |
|-|:----|:---|:--|:-|:------|:--------|:---------|:---------|:--------|:-------|:--------|:------|
| 9|  8 |  2 | 2 |  |       |         |          |          |         |       |         |       |
|10|  9 |  2 | 2 |  |*Error*|*matriz* |          |          |         |       |         |       |
|11| 10 |  2 | 2 |  |área|*proporciones*| R     |E         |F.       |       |         |       |
|12| 11 |  3 | 3 |  |      |          | Bosque |No-bosque| Dist. Bosque | Amortiguamiento |Total    |*Wh*   |
|13| 12 |  1 | 1 |  |  M   |Bosque    |0.54299|0.00601|0.00200|0|0.55100|0.551  |
|14| 13 |  1 | 1 |  |  A   |No-bosque| 0.01221|0.39276|0.00204|0|0.40700 |0.407  |
|15| 14 |  1 | 1 |  | P    | Dist. Bosque    | 0.00091|0.00046|0.01233|0|0.01370 |0.0137  |
|16| 15 |  2 | 2 |  |      |Amortiguamiento    |0.02200|0      |0.00670|0|0.02870 |0.0287  |
|17| 16 |  3 | 3 |  |      |Total     | 0.57811|0.39922|0.02307|0|1 |1  |

Si hicimos los cálculos correctamente, los totales de las filas deben ser iguales a los pesos de los estratos, ya que estos son las proporciones de área estimadas de los estratos. Con la matriz de error expresada en proporciones de área, podemos aplicar fácilmente un estimador estratificado para estimar el área de cada categoría (Cochran, 1977, Eq. 5.52)[^fn1] : 

![](https://latex.codecogs.com/gif.latex?\Large&space;\hat{\mu}_{j}=\hat{p}_{+j}&space;=&space;\sum_{h=1}^H&space;W_h&space;\frac{n_{hj}}{n_{h&plus;}})

En la matriz de error de proporciones de área estimadas, las estimaciones estratificadas son iguales a los totales de la columna. Por eso,

![](https://latex.codecogs.com/gif.latex?\Large&space;\hat{\mu}_{1}=0.578;\hat{\mu}_{2}=0.399;\hat{\mu}_{3}=0.231)

Ahora necesitamos aplicar un estimador de varianza estratificado para construir un intervalo de confianza del 95% alrededor de las estimaciones. El estimador de varianza estratificado es (Cochran, 1977, Eq. 5.57)

![](https://latex.codecogs.com/gif.latex?\Large&space;\hat{V}(\hat{\mu}_{j})=\sum_{h=1}^H&space;W_h^2&space;\frac{\frac{n_{hj}}{n_{h+}}(1-\frac{n_{hj}}{n_{h+}})}{n_{h+}-1}=\sum_{h=1}^H&space;\frac{W_h\hat{p}_{hj}-\hat{p}_{hj}^2}{n_{h+}-1})

Para aplicar el estimador de varianza a los resultados de la muestra en la matriz de error, escriba en célula F17 "V(*μ*)" and in G17 "=($L12*G12-G12^2)/($K4-1) + ($L13*G13-G13^2)/($K5-1) + ($L14*G14-G14^2)/($K6-1) + ($L15*G15-G15^2)/($K7-1)" y expándala a J18. 

Ahora escriba "ES(*μ*)" en célula F18 a calcular el error estándar; en la célula G18 escriba  "=sqrt(G17)" y expanda a J18. Luego escriba "±95% CI" en célula F19 y en célula G19 escriba "=G18*1.96" y expanda a J19. Finalmente, escriba "MoE [%]" en célula F20 y en célula G20 escriba "=G19/G16" y expanda a I20, y convierta a células G a I en fila 20 a porcentaje. Eso le debería de dar lo siguiente:


| | A   | B  | C |D |E      |F        |G         |H         |I          |J |K |L  |
|-|:----|:---|:--|:-|:------|:------|:----------|:----------|:----------|:-|:-|:--|
|16| 15 |  2 | 2 |  |      |Total   | 0.57811   |0.39922    |0.02307    |0 |1 |1  |
|17| 16 |  3 | 3 |  |      |V(μ)	|0.0000456	|0.0000403	|0.0000138	|0| ||
|18| 17 |  1 | 2 |  |      |ES(μ)	|0.0067520	|0.0063466	|0.0037174	|0| ||
|19| 18 |  2 | 2 |  |      |±95% CI	|0.0132339	|0.0124393	|0.0072862	|0| ||
|20| 19 |  4 | 1 |  |      |MoE [%]	|2.29%	    |3.12%	    |31.59%	    |0| ||

Eso concluye la estimación estratificada del área (estos son la proporción del área y deben multiplicarse por el área total de Colombia para expresar las estimaciones en unidades de área):

![](https://latex.codecogs.com/gif.latex?\Large&space;\hat{\mu}_{1}=0.578\pm0.0132)
![](https://latex.codecogs.com/gif.latex?\Large&space;\hat{\mu}_{2}=0.399\pm0.0124)
![](https://latex.codecogs.com/gif.latex?\Large&space;\hat{\mu}_{3}=0.231\pm0.0072)


Finalmente, vamos a calcular la precisión del mapa y las clases del mapa, comenzando con la precisión del usuario. En célula F21 escriba "Prec. Usuario" y en G21 "=G12/K12"; H21 "=H13/K13"; I21 "=I14/K14". Repita para la precisión del productor en fila 22 con células G22 "=G12/G16"; H22 "=H13/H16"; I22 "=I14/I16". Agregue la precisión general en la fila 23 como  "=sum(G12,H13,I14)". Eso le debería de dar lo siguiente:

| | A   | B  | C |D |E      |F        |G         |H         |I          |J |K |L  |
|-|:----|:---|:--|:-|:------|:------|:----------|:----------|:----------|:-|:-|:--|
|16| 15 |  2 | 2 |  |      |Total   | 0.57811   |0.39922    |0.02307    |0 |1 |1  |
|17| 16 |  3 | 3 |  |      |V(μ)	|0.0000456	|0.0000403	|0.0000138	|0| ||
|18| 17 |  1 | 2 |  |      |ES(μ)	|0.0067520	|0.0063466	|0.0037174	|0| ||
|19| 18 |  2 | 2 |  |      |±95% CI	|0.0132339	|0.0124393	|0.0072862	|0| ||
|20| 19 |  4 | 1 |  |      |MoE [%]	|2.29%	    |3.12%	    |31.59%	    |0| ||
|21| 20 |  3 | 3 |  |      |Prec. Usuario	|0.985	    |0.965	    |0.900	    |0| ||
|22| 21 |  3 | 3 |  |      |Prec. Prod.	|0.939	    |0.984	    |0.535	    |0| ||
|23| 22 |  2 | 2 |  |      |Prec. General	|0.948	    |    |	    || ||


## 4. Estimar la precisión de un mapa diferente de la estratificación original 

Cuando los resultados de la muestra se han recopilado utilizando una estratificación diferente al mapa que queremos utilizar para la evaluación de la precisión, no podemos aplicar los estimadores estratificados convencionales ilustrados anteriormente, ya que están sesgados cuando las filas de la matriz de error de la población no corresponden a los estratos utilizados para seleccionar la muestra. En cambio, necesitamos construir estimadores de razón usando funciones indicadoras (Stehman, 2014) [^ fn4]. Para simplificar, reduzcamos los resultados de nuestra muestra a dos clases de observaciones de referencia: *h* = 1 es disturbio del bosque y *h* = 2 es sin perturbación.

Para estimar la precisión general del nuevo mapa utilizando nuestros resultados de muestra existentes, defina la siguiente variable

![](https://latex.codecogs.com/gif.latex?y_u%5EO%20%3D%20%5Cbegin%7Bcases%7D%201%20%26%20%5Ctext%7Bif%20unit%20%5Ctextit%7Bu%7D%20is%20classified%20correctly%7D%5C%5C%200%20%26%20%5Ctext%7Bif%20unit%20%5Ctextit%7Bu%7D%20is%20classified%20incorrectly%7D%20%5Cend%7Bcases%7D)

La precisión general de la media de la población ![](https://latex.codecogs.com/gif.latex?%5Cinline%20%5Cdpi%7B100%7D%20%5Cbar%7BY%7D) basado en un censo de N píxeles en la región; ![](https://latex.codecogs.com/gif.latex?%5Cinline%20%5Cdpi%7B100%7D%20%5Cbar%7BY%7D) es equivalente a la proporción de píxeles clasificados correctamente, es decir, la precisión general. Un estimador insesgado de ![](https://latex.codecogs.com/gif.latex?%5Cinline%20%5Cdpi%7B100%7D%20%5Cbar%7BY%7D) es

![](https://latex.codecogs.com/gif.latex?%5Chat%7BO%7D%20%3D%20%5Chat%7B%5Cbar%7BY%7D%7D%20%3D%20%5Cfrac%7B%5Csum%20N_h%5E*%20%5Cbar%7By%7D_h%5EO%7D%7BN%7D%20%3D%20%5Cfrac%7BN_1%5E*%20%5Cbar%7By%7D_1%5EO%7D%7BN%7D%20&plus;%20%5Cfrac%7B%20N_2%5E*%20%5Cbar%7By%7D_2%5EO%7D%7BN%7D%20%3D%20%5Cfrac%7B1%7D%7BN%7D%20%28N_1%5E*%20%5Csum_%7Bu%20%5Cin%20h%3D1%7D%20%5Cfrac%7By_u%5EO%7D%7Bn_1%5E*%7D%20&plus;%20N_2%5E*%20%5Csum_%7Bu%20%5Cin%20h%3D2%7D%20%5Cfrac%7By_u%5EO%7D%7Bn_2%5E*%7D%29)

Para la precisión del usuario del mapa nuevo, defina las siguientes dos variables

![](https://latex.codecogs.com/gif.latex?y_u%5EU%20%3D%20%5Cbegin%7Bcases%7D%201%20%26%20%5Ctext%7Bif%20unit%20%5Ctextit%7Bu%7D%20is%20classified%20correctly%20and%20map%20class%20forest%20dist.%7D%5C%5C%200%20%26%20%5Ctext%7Botherwise%3B%7D%20%5Cend%7Bcases%7D%20)

![](https://latex.codecogs.com/gif.latex?x_u%5EU%20%3D%20%5Cbegin%7Bcases%7D%201%20%26%20%5Ctext%7Bif%20unit%20%5Ctextit%7Bu%7D%20is%20map%20class%20forest%20dist.%7D%5C%5C%200%20%26%20%5Ctext%7Botherwise.%7D%20%5Cend%7Bcases%7D)


y para la precisión del productor: 

![](https://latex.codecogs.com/gif.latex?y_u%5EP%20%3D%20%5Cbegin%7Bcases%7D%201%20%26%20%5Ctext%7Bif%20unit%20%24u%24%20is%20correctly%20classified%20and%20reference%20class%20forest%20dist.%7D%5C%5C%200%20%26%20%5Ctext%7Botherwise%3B%7D%20%5Cend%7Bcases%7D)

![](https://latex.codecogs.com/gif.latex?x_u%5EP%20%3D%20%5Cbegin%7Bcases%7D%201%20%26%20%5Ctext%7Bif%20unit%20%5Ctextit%7Bu%7D%20is%20reference%20class%20forest%20dist.%7D%5C%5C%200%20%26%20%5Ctext%7Botherwise.%7D%20%5Cend%7Bcases%7D)

Ahora podemos estimar la precisión del usuario y del productor de la clase de perturbación del bosque usando un estimador de razón con las medias específicas del estrato de *x* e *y*:

![](https://latex.codecogs.com/gif.latex?%5Chat%7BR%7D%20%3D%20%5Cfrac%7B%5Chat%7BY%7D%7D%7B%5Chat%7BX%7D%7D%20%3D%20%5Cfrac%7B%5Csum_%7Bh%3D1%7D%5EH%20N_h%5E*%20%5Cbar%7By%7D_h%7D%7B%5Csum_%7Bh%3D1%7D%5EH%20N_h%5E*%20%5Cbar%7Bx%7D_h%7D)

Note que ![](https://latex.codecogs.com/gif.latex?%5Cinline%20%5Cdpi%7B100%7D%20N_h%5E*) es el tamaño de la población y ![](https://latex.codecogs.com/gif.latex?%5Cinline%20%5Cdpi%7B100%7D%20n_h%5E*) es el tamaño de muestra en los resultados de muestra, a diferencia del tamaño de población ![](https://latex.codecogs.com/gif.latex?%5Cinline%20%5Cdpi%7B100%7D%20N_h) y tamaño de muestra ![](https://latex.codecogs.com/gif.latex?%5Cinline%20%5Cdpi%7B100%7D%20n_h) en el mapa nuevo.  Contando *x* e *y* en el nuevo mapa, calculamos los recuentos de muestra para completar la siguiente matriz de error:

![](https://latex.codecogs.com/gif.latex?%5Cdpi%7B120%7D%20%5Cbegin%7Btabular%7D%7B%20l%20c%20c%20c%20c%7D%20Stratum%20%26%20%24%5Cbar%7By%7D_u%5EU%24%20%26%20%24%5Cbar%7Bx%7D_u%5EU%24%20%26%20%24%5Cbar%7By%7D_u%5EP%24%20%26%20%24%5Cbar%7Bx%7D_u%5EP%24%20%5C%5C%20%5Chline%201.%20Forest%20Dist.%20%26%20%24%5Cfrac%7B%5Csum%20y_u%5EU%7D%7Bn_1%5E*%7D%24%20%26%20%24%5Cfrac%7B%5Csum%20x_u%5EU%7D%7Bn_1%5E*%7D%24%20%26%20%24%5Cfrac%7B%5Csum%20y_u%5EP%7D%7Bn_1%5E*%7D%24%20%26%20%24%5Cfrac%7B%5Csum%20x_u%5EP%7D%7Bn_1%5E*%7D%24%5C%5C%202.%20Non-Dist.%20%26%20%24%5Cfrac%7B%5Csum%20y_u%5EU%7D%7Bn_2%5E*%7D%24%20%26%20%24%5Cfrac%7B%5Csum%20x_u%5EU%7D%7Bn_2%5E*%7D%24%20%26%20%24%5Cfrac%7B%5Csum%20y_u%5EP%7D%7Bn_2%5E*%7D%24%20%26%20%24%5Cfrac%7B%5Csum%20x_u%5EP%7D%7Bn_2%5E*%7D%24%20%5Cend%7Btabular%7D)


lo cual nos permite fácilmente construir el estimador de razón para la estimación de la precisión de usuario y de productor del nuevo mapa de la clase de disturbio forestal (![](https://latex.codecogs.com/gif.latex?%5Cinline%20%5Cdpi%7B100%7D%20U_1) y ![](https://latex.codecogs.com/gif.latex?%5Cinline%20%5Cdpi%7B100%7D%20P_1)):

![](https://latex.codecogs.com/gif.latex?%5Cdpi%7B120%7D%20%5Chat%7BU%7D_1%20%3D%20%5Chat%7BR%7D%20%3D%20%5Cfrac%7B%5Cfrac%7BN_1%5E*%7D%7Bn_1%5E*%7D%20%5Csum_%7Bu%20%5Cin%20h%3D1%7D%20y_u%5EU%20&plus;%20%5Cfrac%7BN_2%5E*%7D%7Bn_2%5E*%7D%20%5Csum_%7Bu%20%5Cin%20h%3D2%7D%20y_u%5EU%7D%7B%5Cfrac%7BN_1%5E*%7D%7Bn_1%5E*%7D%20%5Csum_%7Bu%20%5Cin%20h%3D1%7D%20x_u%5EU%20&plus;%20%5Cfrac%7BN_2%5E*%7D%7Bn_2%5E*%7D%20%5Csum_%7Bu%20%5Cin%20h%3D2%7D%20x_u%5EU%7D)

![](https://latex.codecogs.com/gif.latex?%5Cdpi%7B120%7D%20%5Chat%7BP%7D_1%20%3D%20%5Chat%7BR%7D%20%3D%20%5Cfrac%7B%5Cfrac%7BN_1%5E*%7D%7Bn_1%5E*%7D%20%5Csum_%7Bu%20%5Cin%20h%3D1%7D%20y_u%5EP%20&plus;%20%5Cfrac%7BN_2%5E*%7D%7Bn_2%5E*%7D%20%5Csum_%7Bu%20%5Cin%20h%3D2%7D%20y_u%5EP%7D%7B%5Cfrac%7BN_1%5E*%7D%7Bn_1%5E*%7D%20%5Csum_%7Bu%20%5Cin%20h%3D1%7D%20x_u%5EP%20&plus;%20%5Cfrac%7BN_2%5E*%7D%7Bn_2%5E*%7D%20%5Csum_%7Bu%20%5Cin%20h%3D2%7D%20x_u%5EP%7D)

## 5. Posestratificación
Como se explica en el tutorial de diseño de muestreo, una ventaja importante de SRS / SYS es la capacidad de estratificar el área de estudio después de que se hayan recopilado los resultados de la muestra. La aplicación de una estratificación posterior al muestreo se conoce como posestratificación (PSTR), que probablemente aumentará la precisión de las estimaciones, y rara vez hay razones para no posestratificar siempre que existan mapas sobre el área de estudio. Otra ventaja es que el estimador estratificado ilustrado en la Sección 3, **Estimación estratificada** anterior, es directamente aplicable a los datos de la muestra SRS o SYS cuando se tabula en forma cruzada con las etiquetas de la posestratificación en una matriz de error (en este caso, el estimador estratificado se denomina estimador posestratificado pero la fórmula es exactamente la misma). Por lo tanto, para aplicar un estimador PSTR, simplemente siga los pasos descritos en la Sección 3, **Estimación estratificada** anterior.

Una diferencia importante entre estimación STR y PSTR es la formula para el estimador de varianza. De acuerdo a Lohr (1999, Eq. 4.22)[^fn5] si *Wh* se conoce y “*nh* es razonablemente grande (≥30 aprox.)” – o “razonablemente grande, por decir > 20 en cada estrato” (Cochran 1977, p. 134)[^fn1] – el estimador de varianza es

![](https://latex.codecogs.com/gif.latex?\Large&space;\hat{V}(\hat{\mu}_{PSTR})\approx\sum_{h=1}^H&space;W_h\frac{s_h^2}{n_{h}})

Para proporciones (Cochran, 1977, Eq. 3.5)[^fn1], la varianza de estrato *h* se puede expresar como

![](https://latex.codecogs.com/gif.latex?\Large&space;s_h^2=\frac{n_h}{n_{h}-1}p_h(1-p_h))

En una matriz de error tradicional, *p_h = n_hj ÷ n_h* donde *n_hj* es el conteo de muestra de clases de referencia *j* en estrato *h*. Combinando la aproximación de varianza de Lohr y la expresión de Cochran para varianza de estrato da un estimador de varianza posestratificada expresado usando elementos de una matriz de error: 

![](https://latex.codecogs.com/gif.latex?%5Chat%7BV%7D%28%5Chat%7B%5Cmu%7D_%7BPSTR%7D%29%5Capprox%5Csum_%7Bh%3D1%7D%5EH%26space%3BW_h%5Cfrac%7Bs_h%5E2%7D%7Bn_%7Bh%7D%7D%3D%5Cfrac%7B1%7D%7Bn%7D%5Csum_%7Bh%3D1%7D%5EHW_h%5Cfrac%7Bn_h%7D%7Bn_h-1%7Dp_h%281-p_h%29%3D%5Cfrac%7B1%7D%7Bn%7D%5Csum_%7Bh%3D1%7D%5EHW_h%5Cfrac%7Bn_%7Bhj%7D%281-%5Cfrac%7Bn_%7Bhj%7D%7D%7Bn_{h+}%7D%29%7D%7Bn_{h+}-1%7D)

Si compara esto con el estimador de varianza STR de Sección 3, **Estimación Estratificada** arriba, vera que el estimador de varianza PSTR es muy similar pero no idéntico.  


## 6. Software para automatizar el análisis de resultados de muestra 

### 6.1 AREA2
La aplicación AREA2 en Google Earth Engine tiene ecuaciones para todos los estimadores descritos en este tutorial. Note que en AREA2, se le refiere al estimador SRS por su nombre formal, estimador de expansión. AREA2 esta disponible aquí: https://code.earthengine.google.com/?accept_repo=projects/AREA2/public y mas documentación detallada aquí: https://area2.readthedocs.io/

### 6.2 SEPAL
Estimación estratificada es automatizada en SEPAL; la documentación esta disponible aquí: https://github.com/sig-gis/SEPAL-CEO  Baje a *Ejercicio 4.3: Estimación de área e incertidumbre* para una descripción de estimación estratificada. 

## Licencia
Esta trabajo tiene licencia bajo un [Creative Commons Attribution 3.0 IGO](https://creativecommons.org/licenses/by/3.0/igo/) 

Copyright 2020, World Bank. Este trabajo fue desarrollado por Pontus Olofsson bajo contrato del World Bank con GRH Consulting, LLC para el desarrollo de recursos nuevos o existentes relacionadas a la Medida, Reportaje, y Verificación para el apoyo de implementación MRV en varios países. 

Atribución: Olofsson, P. (2021). *Open MRV: Analysis of sample data*. World Bank. License: Creative Commons Attribution license (CC BY 3.0 IGO)



## Referencias
[^fn1]: Cochran, W. G. (1977). *Sampling Techniques*. New York, NY: Wiley

[^fn2]: Casella, G., & Berger, R. L. (2002). *Statistical Inference* (2nd ed.). Pacific Grove, CA: Duxbury Press

[^fn3]: Rice, J. A. (1995). *Mathematical Statistics and Data Analysis* (2nd ed.). Belmont, CA: Duxbury Press

[^fn4]: Stehman, S. V. (2014). Estimating area and map accuracy for stratified random sampling when the strata are different from the map classes. *International Journal of Remote Sensing*, 35(13), 4923-4939

[^fn5]: Lohr, S. L. (1999). *Sampling: Design and Analysis*. CRC Press




