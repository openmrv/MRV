# Diseño de muestreo para la aproximación de la precisión de área y mapa  

## 1. Contexto

Un método de estimación basado en muestreo puede dividirse en tres componentes diferentes: diseño de muestreo, diseño de respuesta, y análisis (Stehman & Czaplewski, 1998) [^ fn1]. El primer componente, el diseño de muestreo, se ilustra en este tutorial. El diseño de muestreo define el protocolo para seleccionar el subconjunto de unidades, es decir, la muestra, de una población más grande. En nuestro caso, la población es el equivalente al área de estudio, y las características del área de estudio, como el área de una cobertura de suelo, se estiman mediante el análisis de la muestra. Los métodos basados en el muestreo en un contexto geográfico o de teledetección son necesarios porque nos permiten estimar el sesgo del área, la precisión del mapa, y la incertidumbre. Como se explica en el Documento de orientación y métodos de GFOI, simplemente contando píxeles en los mapas para la estimación de las áreas de cobertura terrestre y el cambio de cobertura terrestre producirá resultados erróneos debido a errores de clasificación (GFOI, 2016, p. 125)[^fn2]:

> Los métodos que producen estimaciones de datos de actividad como sumas de áreas de unidades de mapa asignadas a clases de mapa se caracterizan como recuento de píxeles y, en general, no contemplan los efectos de los errores de clasificación de mapas. Además, aunque las matrices de confusión o error y los índices de precisión del mapa pueden informar problemas de precisión y errores sistemáticos, no producen directamente la información necesaria para construir intervalos de confianza. Por lo tanto, los métodos de recuento de píxeles no garantizan que las estimaciones “no sean ni sobreestimadas ni subestimadas” o que “las incertidumbres se reduzcan en la medida de lo posible”. La función de los datos de referencia, también caracterizados como datos de evaluación de la precisión, es proporcionar dicha garantía ajustando los errores de clasificación sistemáticos estimados y estimando la incertidumbre, proporcionando así la información necesaria para la construcción de intervalos de confianza para el cumplimiento de la guía de buenas prácticas del IPCC.

Al elegir un diseño de muestreo, debemos considerar algunos importantes criterios de diseño. De primordial importancia es la adherencia al muestreo probabilístico. El muestreo probabilístico se define en términos de probabilidades de inclusión, donde una probabilidad de inclusión se relaciona con la probabilidad de que una unidad determinada se incluya en la muestra; la probabilidad de inclusión debe ser conocida para cada unidad seleccionada en la muestra y la probabilidad de inclusión debe ser mayor que cero para todas las unidades en el área de estudio (Stehman, 2009) [^ fn3]. Varios diseños de muestreo probabilístico son aplicables a la precisión y la estimación de áreas. Los diseños más comúnmente usados son aleatorios simple, aleatorio estratificado, y sistemático. El muestreo en dos fases (también llamado doble), en dos etapas y por conglomerados es aplicable pero más complicado.



## 2 Objetivos de Aprendizaje 

El objetivo de este tutorial es proporcionar al usuario una comprensión de las diversas decisiones clave involucradas en el diseño de un esfuerzo de estimación basado en muestreo. Es importante comprender la relación entre el tamaño de la muestra y la asignación de unidades de muestra a los estratos, y los objetivos críticos de estimación, como la precisión del objetivo. Una vez completado el tutorial, el usuario debe poder elegir un método de selección de la muestra (SYS, SRS o STR), determinar el tamaño de la muestra y asignar la muestra a los estratos, en función de los objetivos de estimación.

- Comprender las diversas decisiones clave involucradas en el diseño de un esfuerzo de estimación basado en muestreo
- Elija un método de selección de muestras: SYS, SRS o STR según los objetivos de estimación
- Determinar el tamaño de la muestra y asignar la muestra a los estratos, en función de los objetivos de estimación.

### 2.1 Prerrequisitos para este módulo

- Repaso de la terminología relevante para las técnicas de muestreo en el tutorial 3.1 Terminología
- Es altamente recomendado que tenga un entendimiento de los tutoriales previos en Módulos 1 y 2



## 2. Como escoger un diseño de muestreo?

La elección de un diseño de muestreo a menudo implica compensaciones entre diferentes criterios y prioridades. El deseo de proporcionar estimaciones para las subregiones o la necesidad de alcanzar objetivos de precisión deberá equilibrarse con los criterios de diseño de muestreo deseables, como la facilidad y practicidad de la implementación, la rentabilidad, y la facilidad para adaptarse a los cambios en el tamaño de la muestra. Stehman (2009) [^ fn3] proporciona un repaso detallado de las opciones, objetivos, y criterios de diseño de muestreo, pero la decisión generalmente se reduce a tres decisiones clave: si usar estratos, si usar conglomerados, y si implementar un sistema sistemático o un protocolo simple de selección aleatoria.

### 2.1 Usar estratos?

Los estratos son “subpoblaciones que no se superponen y que juntas comprenden toda la población” (Cochran, 1977, p. 89) [^ fn4]. La estratificación del área de estudio antes de la selección de la muestra puede garantizar que se obtengan estimaciones de precisión y área para ciertas subregiones en el área de estudio, y da como resultado una mayor precisión de las estimaciones. En consecuencia, existen varias buenas razones para utilizar estratos. Incluso con un muestreo aleatorio simple, el uso de estratos después de seleccionar la muestra es una [buena idea](### markdown-header-3.1-Post-estratificación). El muestreo estratificado proporciona una ventaja obvia si estamos interesados en una proporción muy pequeña del área de estudio, como suele ser el caso de los MRV tropicales. Por ejemplo, el área de pérdida de bosques, incluso en países con una deforestación desenfrenada, a menudo es una proporción muy pequeña del país, especialmente en intervalos de tiempo cortos. El uso de un mapa de pérdida de bosques (y otras categorías) para estratificar el área de estudio en tales situaciones permite un muestreo específico en áreas de interés particular. No estratificar en tales situaciones requerirá un tamaño de muestra muy grande.  

### 2.2 Usar selección simple aleatoria o sistemática?

La selección sistemática implica seleccionar un punto de partida al azar con la misma probabilidad y luego muestrear con una distancia fija entre las ubicaciones de las muestras. En resumen, la selección aleatoria simple es preferible si se recopilan observaciones de referencia en datos satelitales, mientras que la selección sistemática es preferible si se visitan ubicaciones de muestreo in situ (Olofsson et al. 2014) [^ fn5]. El fundamento de esta recomendación es que las unidades seleccionadas sistemáticamente son más fáciles de ubicar en el campo, mientras que la selección aleatoria es más fácil de aumentar. Tenga en cuenta que los mismos estimadores se utilizan tanto con selección aleatoria simple como con selección sistemática. 

### 2.3 Usar conglomerado?

Un conglomerado es una unidad de muestreo que consta de una o más de las unidades de evaluación básicas especificadas por el diseño de respuesta. Por ejemplo, un grupo podría ser un bloque de 9 pixeles 3 × 3 o un grupo de 1 km × 1 km que contenga 100 unidades de evaluación de 1 ha. En el muestreo de conglomerados, se selecciona una muestra de conglomerados y, por lo tanto, las unidades espaciales dentro de cada conglomerado se seleccionan como un grupo en lugar de seleccionarse como entidades individuales. El muestreo en dos etapas es una forma de muestreo por conglomerados en el que se seleccionan grandes unidades primarias de muestreo (UPM) en la primera etapa. Las unidades de muestreo secundarias (SSU por sus siglas en ingles) más pequeñas se seleccionan dentro de cada UPM en la segunda etapa. Dichos diseños tienen la ventaja de requerir datos de referencia (es decir, los datos utilizados para recopilar observaciones de referencia) solo sobre las UPM en lugar de toda el área de estudio, como es el caso de los diseños mencionados anteriormente. Sin embargo, a menos que los ahorros de costos sean considerables, los diseños basados en conglomerados no se recomiendan ya que la correlación entre SSU a menudo reduce la precisión en relación con una muestra aleatoria simple de igual tamaño, y porque son diseños complicados que son difíciles de aumentar con resultados de muestra que son difícil de analizar.


## 3. Muestreo aleatorio simple/sistemático

Si las unidades (por ejemplo, pixeles) de una población/área de estudio están enumeradas de 1 a *N*, el muestreo aleatorio simple (SRS) es “Un método para seleccionar *n* unidades de *N* de tal manera que cada una de estos [los conjuntos de *n* unidades especificadas] tiene una probabilidad igual de ser seleccionado” (Cochran 1977, p. 18)[^fn4]. En un contexto geográfico, frecuentemente estamos interesados en estimar la proporción de una población/área de estudio de los datos de muestra, como la proporción de área de un tipo de cobertura de suelo o de cambio de cobertura. Usando las nociones de Cochran, las unidades de una población son ![](https://latex.codecogs.com/gif.latex?\inline&space;y_1&space;\ldots&space;y_N) de las cuales una muestra ![](https://latex.codecogs.com/gif.latex?\inline&space;y_1&space;\ldots&space;y_n) es seleccionada bajo SRS; lo grabamos ![](https://latex.codecogs.com/gif.latex?\inline&space;y_i=1) si la cobertura de suelo de interés es observada en unidad *i* y ![](https://latex.codecogs.com/gif.latex?\inline&space;y_i=0) de lo contrario. Una ventaja de SRS es que la media de las observaciones es un estimador insesgado de la proporción de población (*p*) de interés. (Cochran, 1977, Eq 3.3)[^fn4]:

![](https://latex.codecogs.com/svg.latex?\Large&space;\bar{y}=\frac{1}{n}\sum_{i=1}^{n}y_i=\hat{p})

y la varianza de la proporción estimada *p^* es estimada fácilmente como (Cochran, 1977, Eq 3.11)[^fn4]

![](https://latex.codecogs.com/svg.latex?\Large&space;\hat{V}(\hat{p})=\frac{\hat{p}(1-\hat{p})}{n-1})

Estos estimadores también son aplicables a datos de muestra recopilados mediante muestreo sistemático simple (SYS por sus siglas en ingles). El análisis sencillo de los datos de muestra recopilados con SRS / SYS y la capacidad de aumentar el tamaño de la muestra con facilidad (especialmente con SRS) hacen que estos diseños sean atractivos.

### 3.1 Posestratificación 

Otra ventaja importante de SRS / SYS es la capacidad de estratificar el área de estudio después de que se hayan recolectado los resultados de la muestra; la aplicación de una estratificación posterior al muestreo se denomina posestratificación (PSTR). Es probable que el PSTR aumente la precisión de las estimaciones, y rara vez hay razones para no post-estratificar utilizando mapas.

### 3.2 Tamaño de muestra

Determinar el tamaño de la muestra independientemente del diseño implica calcular el número de unidades en una muestra necesarias para alcanzar una cierta precisión objetivo de una estimación de un parámetro de población de interés. El cálculo se basa en resolver el estimador de varianza correspondiente al diseño para *n*. Si la varianza en el estimador de varianza anterior es la varianza deseada de una estimación, resolver *n* da (Cochran, 1977, Eq. 4.2)[^fn4] 

![](https://latex.codecogs.com/svg.latex?\Large&space;n=\frac{\hat{p}(1-\hat{p})}{\hat{V}(\hat{p})})

donde *p^* es un estimado de la proporción de unidades en la clase de interés en el área de estudio. Por ejemplo, supongamos que queremos estimar la precisión general (como en Olofsson et al., 2014, p. 53)[^fn5] con un margen de error (*MoE*) de 5%. Definiríamos *p* como la precisión general del mapa. Obviamente no conocemos la precisión general del mapa en este punto así que se requiere una conjetura educada. Si suponemos una precisión general de 80%, un margen de error de 5% se traduciría a una varianza de (la puntuación z de 1.96 en el nivel de confianza de 95% se redondea a 2)

![](https://latex.codecogs.com/svg.latex?\Large&space;MoE=\frac{2\sqrt{\hat{V}}(\hat{p})}{\hat{p}}\Leftrightarrow\hat{V}(\hat{p})=(\frac{MoE\times&space;\hat{p}}{2})^2=(\frac{0.05\times0.8}{2})^2=0.0004)

el cual nos da un tamaño de muestra de

![](https://latex.codecogs.com/svg.latex?\Large&space;n=\frac{\hat{p}(1-\hat{p})}{\hat{V}(\hat{p})}=\frac{0.8(1-0.8)}{0.0004}=400)

Aunque la estimación de la precisión general se ilustró en Olofsson et al. (2014) [^ fn5], especificar un margen de error de la precisión general del mapa no es intuitivo y rara vez constituye un objetivo de estimación. Un ejemplo más realista sería la estimación del área de deforestación o degradación forestal con cierta precisión. En el tutorial CODED, se creó un mapa de deforestación, degradación forestal, forestal y no forestal para Colombia; para simplificar el asunto, agrupemos la deforestación y la degradación forestal en una sola clase de perturbación forestal, que fue mapeada como 1.4% del país de 2010 a 2020. Note, para la estimación de datos de actividad dentro de REDD+ (y otras iniciativas), se recomienda estimar la deforestación y la degradación por separado y, por lo tanto, utilizar un estrato de deforestación y un estrato de degradación, en lugar de combinar las dos clases en una sola clase de perturbación forestal. Aquí, estamos usando una clase de perturbación combinada para facilitar la ilustración del flujo de trabajo y los cálculos. Supongamos que queremos estimar el área de perturbación del bosque (nuevamente, deforestación y degradación combinadas) con un margen de error del 25%. Tenga en cuenta que el 25% se utiliza aquí simplemente para ilustrar el flujo de trabajo; el error objetivo dependerá de las circunstancias del estudio. Primero, un margen de error de 25% es equivalente a una varianza de  

![](https://latex.codecogs.com/svg.latex?\Large&space;\hat{V}(\hat{p})=(\frac{MoE\times&space;\hat{p}}{2})^2=(\frac{0.25\times0.014}{2})^2=0.000003)

el cual nos da un tamaño de muestra de

![](https://latex.codecogs.com/svg.latex?\Large&space;n=\frac{\hat{p}(1-\hat{p})}{\hat{V}(p)}=\frac{0.014(1-0.014)}{0.000003}=4,600)

La recopilación de observaciones en casi cinco mil ubicaciones de muestra rara vez es posible para un estudio individual. El ejemplo ilustra uno de los inconvenientes de SRS / SYS: debido a que no estamos usando ninguna información sobre la ubicación de la deforestación, se requiere un tamaño de muestra muy grande para lograr una alta precisión. Otra forma más rápida de estimar la muestra en este caso es asumir que necesitamos al menos 30 unidades en áreas de deforestación, lo que requeriría un tamaño de muestra de 30 / 0.014 = 2,142 unidades que es más manejable pero aún grande, y no estamos muestreando para alcanzar un objetivo de precisión. (Baje a la sección **4.3 Asignación** para una explicación de porque 30 es el "numero mágico".)

## 4. Muestreo aleatorio estratificado

El ejemplo anterior ilustra el inconveniente de SRS / SYS: cuando intentamos estimar algo que es una pequeña proporción de la población, se requiere un tamaño de muestra muy grande bajo SRS / SYS. En tales situaciones, se recomienda el muestreo aleatorio estratificado (STR). STR es simplemente cuando “se toma un muestreo aleatorio simple en cada estrato” (Cochran 1977, p. 89) [^ fn4]. En consecuencia, dividimos la población en estratos y seleccionamos una muestra en cada estrato bajo SRS (o SYS). STR agrega otro nivel de complejidad y requiere que determinemos cómo asignar la unidad de muestra a los estratos, además de determinar el tamaño total de la muestra.

### 4.1 Tamaño de muestra

Al igual que con SRS / SYS, necesitamos especificar un objetivo de precisión y calcularlo utilizando el estimador de varianza STR y el tamaño total de la muestra (*n*) requerido para alcanzar la precisión objetivo. Resolver el estimador de varianza STR da (Olofsson et al., 2014, Eq. 13. modificado de Cochran, 1977, Eq 5.25)[^fn4]

![](https://latex.codecogs.com/svg.latex?\Large&space;n=\left&space;[\frac{\sum_{h}W_h\textup{SD}_h}{\text{SE}(p)}\right&space;]^2)

*Wh* es el peso del estrato *h*, que es simplemente el área del estrato expresada como una proporción del área total de estudio; SD *h* es la desviación estándar del estrato *h*, que se explica a continuación. El error estándar objetivo es SE (*p*). Ahora, volvamos al ejemplo de perturbación forestal de Colombia, pero ahora usemos el mapa que generamos en el tutorial CODED de perturbación, bosque estable y no bosque estable. El cálculo del tamaño de la muestra en STR es un poco más complicado, por lo que usaremos una hoja de cálculo de Google Sheets (o Microsoft Excel si lo prefiere). Se puede acceder a la hoja de cálculo utilizada en este tutorial aquí: https://docs.google.com/spreadsheets/d/1lmPt35SvR3X7txpn0cwd-xkgwC_4nRPL520OZZcRKX0/edit?usp=sharing  

#### Paso 1 

Primero necesitamos calcular el número de píxeles de cada estrato; esto se puede hacer usando GDAL, QGIS, Google Earth Engine, etc.; en el tutorial CODED, estas áreas están impresas en la *Consola* en Google Earth Engine. De lo contrario, o si tiene un activo GEE existente, cargue el activo utilizando el script de muestreo aleatorio estratificado AREA2 (https://code.earthengine.google.com/6a0f89221d40ee039362974d303ff5aa) para calcular los pesos de los estratos. Agregue estos números en la primera fila "Área [px]". En la segunda fila, exprese estas áreas como una proporción (en célula B3 escriba "=B2/sum($B2:$D2") y extiéndalo a E2). A estas proporciones se les refiere como los pesos de los estratos (*Wh*).


|      | A             | B               | C               | D              | E                 |
| ---- | :------------ | :-------------- | :-------------- | :------------- | :---------------- |
| 1    | Estrato (*h*) | Bosque (1)      | No-Bosque (2)   | For. Dist. (3) | Total             |
| 2    | Área [m2]     | 658,196,561,513 | 462,219,395,097 | 15,594,353,281 | 1,136,010,309,891 |
| 3    | *Wh*          | 0.579           | 0.407           | 0.0137         | 1                 |

#### Paso 2

Note que hemos calculado *Wh*, y necesitamos calcular las dos variables restantes en la ecuación: la deviación estándar de estrato *h* (SD*h*) y el error estándar objetivo (SE(*p*)). SD*h* es algo difícil de entender y requiere la mejor conjetura de la proporción de estrato *h* que es la clase objetiva (*qh*). 

![](https://latex.codecogs.com/svg.latex?\Large&space;\textup{SD}_h=\sqrt{q_h(1-q_h)})

En nuestro ejemplo, la proporción de disturbio en el área de estudio es el objetivo, lo cual significa que *qh* es la proporción de estrato *h* que es el disturbio -- si el mapa fuera perfecto (y no lo es!) entonces *q1* (bosque) = *q2* (no-bosque) = 0; *q3* (disturbio) = 1, pero no podemos suponer que este es el caso. Ningún mapa es perfecto y una suposición mas realística seria decir, por ejemplo, que el 80% del disturbio en el área de estudio es capturado en la clase de disturbio del mapa, y que fracciones pequeñas de los estratos de bosque y no-bosque son disturbios causados por error de clasificación. Si *q1* = 0.001, entonces supondríamos que 0.001 × 658,196,561,513/30^2^ = 0.7M pixeles de disturbio en el estrato de bosque. Ya que el estrato de no-bosque es un poco mas pequeño, si creemos que una cantidad similar de disturbio también esta presente en ese estrato, debemos suponer que *q2* = 0.002. En consecuencia,agreguemos estos números (0.001, 	0.002   and	0.8	 ) en la fila 4 y calculemos SD*h* en fila 5, célula B5 como "=sqrt(B4(1-B4))" y extenderlo a la célula D5. Luego calculemos el producto de *SDh* y *Wh* en la fila 6 de manera que la célula B6 = B3*B5 y extender eso a D5:

|      | A            | B               | C               | D               | E                 |
| ---- | :----------- | :-------------- | :-------------- | :-------------- | :---------------- |
| 1    | Estrato(*h*) | Bosque (1)      | No-Bosque (2)   | Dist. Bosq. (3) | Total             |
| 2    | Área [m2]    | 658,196,561,513 | 462,219,395,097 | 15,594,353,281  | 1,136,010,309,891 |
| 3    | *Wh*         | 0.579           | 0.407           | 0.0137          | 1                 |
| 4    | *qh*         | 0.001           | 0.002           | 0.8             |                   |
| 5    | SD*h*        | 0.0316          | 0.0447          | 0.4             |                   |
| 6    | SD*h* x *Wh* | 0.0183          | 0.01818         | 0.005491        |                   |

#### Paso 3

Ahora, vamos a establecer el objetivo del muestreo: el margen de error deseado de una área de disturbio. En la formula para estimar el tamaño de muestra, el objetivo se expresa como un error estándar. Si de nuevo queremos establecer un margen de error de 25%, entonces 

![](https://latex.codecogs.com/svg.latex?\Large&space;MoE=\frac{1.96\times\textup{SE}(\hat{p})}{\hat{p}}\Leftrightarrow\textup{SE}(\hat{p})=\frac{MoE\times&space;\hat{p}}{1.96}=\frac{0.1\times0.01}{1.96}=0.0005)

Aquí estamos usando una puntuación z de 1.96 la cual corresponde con el nivel de confianza de 95%. Si especificamos el margen de error en la célula D7, entonces podemos calcular el error estándar objetivo en la célula D8: "=(D7/100)*D3/2":

|      | A            | B               | C               | D               | E                 |
| ---- | :----------- | :-------------- | :-------------- | :-------------- | :---------------- |
| 1    | Estrato(*h*) | Bosque(1)       | No-Bosque(2)    | Dist. Bosq. (3) | Total             |
| 2    | Área [m2]    | 658,196,561,513 | 462,219,395,097 | 15,594,353,281  | 1,136,010,309,891 |
| 3    | *Wh*         | 0.579           | 0.407           | 0.0137          | 1                 |
| 4    | *qh*         | 0.001           | 0.002           | 0.8             |                   |
| 5    | SD*h*        | 0.0316          | 0.0447          | 0.4             |                   |
| 6    | SD*h* x *Wh* | 0.0183          | 0.01818         | 0.005491        |                   |
| 7    | MoE [%]      |                 |                 | 25              |                   |
| 8    | ES(*p^*)     |                 |                 | 0.0017          |                   |

#### Paso 4

Finalmente, ahora podemos fácilmente calcular el tamaño de muestra en la fila 8, celular E9 como: "=(sum(B6:D6)/B7)^2"

|      | A            | B               | C               | D               | E                 |
| ---- | :----------- | :-------------- | :-------------- | :-------------- | :---------------- |
| 1    | Estrato(*h*) | Bosque(1)       | No-Bosque (2)   | Dist. Bosq. (3) | Total             |
| 2    | Área [m2]    | 658,196,561,513 | 462,219,395,097 | 15,594,353,281  | 1,136,010,309,891 |
| 3    | *Wh*         | 0.579           | 0.407           | 0.0137          | 1                 |
| 4    | *qh*         | 0.001           | 0.002           | 0.8             |                   |
| 5    | SD*h*        | 0.0316          | 0.0447          | 0.4             |                   |
| 6    | SD*h* x *Wh* | 0.0183          | 0.01818         | 0.005491        |                   |
| 7    | MoE [%]      |                 |                 | 25              |                   |
| 8    | ES(*p^*)     |                 |                 | 0.00172         |                   |
| 9    | *n*          |                 |                 |                 | 599               |

lo cual nos da un tamaño de muestra de 599 -- o sea aproximadamente 1/8 del tamaño de muestra de 4,600 requerido bajo SRS para alcanzar el mismo nivel de precisión. Para cambiar el objetivo de precisión, ahora simplemente necesitamos ajustarlo en la célula D7. 

### 4.2 Estratos de amortiguamiento

Un problema potencial en la situación anterior es que las omisiones de perturbación presentes en el estrato de bosque tendrán un gran impacto en la precisión de las estimaciones. Dichos errores de omisión son unidades de muestra en el estrato de bosque que se observaron en los datos de referencia como perturbaciones. El problema se explica en detalle en Olofsson et al. (2020) [^ fn6] y aquí simplemente reconocemos que la "contribución a la incertidumbre" de los errores de omisión depende en gran medida del tamaño del estrato en el que ocurren. Por lo tanto, nos gustaría disminuir el tamaño del estrato de bosque que actualmente es el 83% del área de estudio. En particular, queremos crear pequeños sustratos donde es probable que ocurran omisiones de disturbios. Un enfoque explorado en la literatura es la creación de estratos de amortiguamiento alrededor de los estratos de cambio; la razón es que es probable que los errores ocurran cerca del cambio correctamente mapeado. En nuestro caso, dicho estrato de amortiguamiento podría definirse como los píxeles en el estrato del bosque adyacente al disturbio.

La creación de un amortiguamiento no se ilustra en los tutoriales anteriores, así que hagámoslo ahora. Haga clic en este enlace para encontrar un script para crear un amortiguamiento en la salida CODED que está disponible en AREA2:
https://code.earthengine.google.com/861290ef20f0d76e7639d430471c7eae 
Alternativamente,  puede usar este mapa de Colombia basado en CODED con un amortiguamiento: 
https://code.earthengine.google.com/?asset=users/olofsson76/Open_MRV/Open_MRV_Col_strat_buffer
Para obtener los pesos de estratos, abra el script en AREA2 para seleccionar una muestra con muestreo aleatorio estratificado:
https://code.earthengine.google.com/?accept_repo=users%2Fopenmrv%2FMRV&scriptPath=projects%2FAREA2%2Fpublic%3A1.%20Sampling%20Design%2FStratified%20Random%20Sampling y especifique la ruta al mapa de Colombia basado en CODED con un amortiguamiento bajo "Specify stratification/image to define study area" (Especifique estratificación/imagen para definir area de estudio); use los otros argumentos automáticos y haga clic en "Load image" lo cual visualizara las áreas de estratos en la Consola (NOTA:  esto tomará tiempo). Consiga las siguientes áreas de Bosque (0), No-bosque (1), Disturbio de Bosque (2) y un amortiguamiento de 2-pixeles (3) [m^2^]:

0: 625,597,113,080
1: 462,219,395,097
2: 15,594,353,281
3: 32,599,448,433

Vamos a agregar estos números en la segunda pestaña en la hoja de cálculo y calcular los pesos de estratos: 

|      | A            | B               | C               | D              | E              | F                 |
| ---- | :----------- | :-------------- | :-------------- | :------------- | :------------- | :---------------- |
| 1    | Estrato(*h*) | Bosque (1)      | No-Bosque (2)   | For. Dist. (3) | FD buf. (4)    | Total             |
| 2    | Área [m2]    | 625,597,113,080 | 462,219,395,097 | 15,594,353,281 | 32,599,448,433 | 1,136,010,309,891 |
| 3    | *Wh*         | 0.551           | 0.407           | 0.0137         | 0.0287         | 1                 |

Si creemos que el estrato de amortiguamiento es eficiente para capturar errores de omisión, podemos disminuir *qh* para el estrato de bosque - si asumimos que la mitad de los píxeles de disturbio en el estrato de bosque serán "capturados" por el estrato de amortiguamiento, entonces *q1* = 0.0005 y *q4* = 0.0075. Con un margen de error objetivo del 25%, el tamaño de la muestra se reduce a 502.
	

|      | A            | B               | C               | D               | E                   | F                 |
| ---- | :----------- | :-------------- | :-------------- | :-------------- | :------------------ | :---------------- |
| 1    | Estrato(*h*) | Bosque(1)       | No-bosque (2)   | Dist. Bosq. (3) | Amortiguamiento (4) | Total             |
| 2    | Área [m2]    | 625,597,113,080 | 462,219,395,097 | 15,594,353,281  | 32,599,448,433      | 1,136,010,309,891 |
| 3    | *Wh*         | 0.551           | 0.407           | 0.0137          | 0.0287              | 1                 |
| 4    | *qh*         | 0.0005          | 0.002           | 0.8             | 0.0075              |                   |
| 5    | SD*h*        | 0.0223          | 0.04468         | 0.4             | 0.086277            |                   |
| 6    | SD*h* x *Wh* | 0.0123          | 0.01818         | 0.005491        | 0.002475            |                   |
| 7    | *MoE* [%]    |                 |                 | 25              |                     |                   |
| 8    | ES(*p^*)     |                 |                 | 0.001716        |                     |                   |
| 9    | *n*          |                 |                 |                 |                     | 502               |

Un amortiguamiento de tres pixeles fue usado aquí solo como ejemplo. Para mas información acerca de como determinar el tamaño del estrato de amortiguamiento, por favor refiérase a Olofsson et al. (2020)[^fn6]. 

### 4.3 Asignación

Supongamos que nos conformamos con el margen de error del 15% con un estrato amortiguador y un tamaño de muestra de 958. Ahora debemos decidir cómo asignar la muestra a los estratos. En resumen, una asignación proporcional a los pesos de los estratos es eficiente para estimar parámetros que incluyen cálculos entre estratos; tales parámetros incluyen el área, la precisión general, y la precisión del productor. La estimación de la precisión del usuario se basa en cálculos dentro de los estratos que se benefician de una asignación equitativa. Lograr una alta precisión de la precisión del usuario rara vez es un objetivo de estimación, lo que sugiere que es preferible una asignación proporcional. Volviendo a la hoja de cálculo, calculemos en la fila 10 el tamaño de la muestra en cada estrato siguiendo una asignación proporcional: en la celda B10: "= B3 * $ F $ 9" y extender hasta E10.

|      | A            | B               | C               | D               | E                   | F                 |
| ---- | :----------- | :-------------- | :-------------- | :-------------- | :------------------ | :---------------- |
| 1    | Estrato(*h*) | Bosque (1)      | No-Bosque (2)   | Dist. Bosq. (3) | Amortiguamiento (4) | Total             |
| 2    | Área [m2]    | 625,597,113,080 | 462,219,395,097 | 15,594,353,281  | 32,599,448,433      | 1,136,010,309,891 |
| 3    | *Wh*         | 0.551           | 0.407           | 0.0137          | 0.0287              | 1                 |
| 4    | *qh*         | 0.0005          | 0.002           | 0.8             | 0.0075              |                   |
| 5    | SD*h*        | 0.0223          | 0.04468         | 0.4             | 0.086277            |                   |
| 6    | SD*h* x *Wh* | 0.0123          | 0.01818         | 0.005491        | 0.002475            |                   |
| 7    | *MoE* [%]    |                 |                 | 25              |                     |                   |
| 8    | ES(*p^*)     |                 |                 | 0.001716        |                     |                   |
| 9    | *n*          |                 |                 |                 |                     | 502               |

|10| *nh* (prop.) |277	|204	|7	|14|	502


Esto parece razonable, pero necesitamos al menos 30 unidades por estrato, por lo tanto, en la fila 11 aumentemos el tamaño de la muestra en el estrato de disturbio a 30 y redondeemos los tamaños de muestra en el estrato forestal a 275 y el estrato no forestal a 200. Eso nos da la asignación final.

|      | A             | B               | C               | D               | E                   | F                 |
| ---- | :------------ | :-------------- | :-------------- | :-------------- | :------------------ | :---------------- |
| 1    | Estrato (*h*) | Bosque (1)      | No-bosque (2)   | Dist. Bosq. (3) | Amortiguamiento (4) | Total             |
| 2    | Área [m2]     | 625,597,113,080 | 462,219,395,097 | 15,594,353,281  | 32,599,448,433      | 1,136,010,309,891 |
| 3    | *Wh*          | 0.551           | 0.407           | 0.0137          | 0.0287              | 1                 |
| 4    | *qh*          | 0.0005          | 0.002           | 0.8             | 0.0075              |                   |
| 5    | SD*h*         | 0.0223          | 0.04468         | 0.4             | 0.086277            |                   |
| 6    | SD*h* x *Wh*  | 0.0123          | 0.01818         | 0.005491        | 0.002475            |                   |
| 7    | *MoE* [%]     |                 |                 | 25              |                     |                   |
| 8    | ES(*p^*)      |                 |                 | 0.001716        |                     |                   |
| 9    | *n*           |                 |                 |                 |                     | 502               |
| 10   | *nh* (prop.)  | 277             | 204             | 7               | 14                  | 502               |
| 11   | *nh* (final)  | 275             | 200             | 30              | 30                  | 535               |

La razón por la cual 30 se considera el tamaño de muestra mínimo se describe mejor por Lohr (1999).[^fn8]: 

> El término impreciso "suficientemente grande" aparece en el teorema del límite central porque la adecuación de la aproximación normal depende de n y de cuán cerca se parece la población {yi, i = 1, ..., N} a una población generada a partir de la distribución normal . El "número mágico" de n = 30 [se] suele citar en los libros de introducción a la estadística como un tamaño de muestra que es "suficientemente grande" para que se aplique el teorema del límite central.

El teorema del límite central es importante porque establece que la suma de las variables aleatorias independientes se distribuye normalmente incluso si las variables en sí mismas no lo están. Por ejemplo, el teorema nos permite construir intervalos de confianza utilizando z-score comunes y un error estándar.

## 5. Muestreo en dos etapas/conglomerado

Debido a la complejidad asociada con el muestreo en dos etapas, hay muchos menos ejemplos de este tipo de diseños en la literatura en comparación con STR y SRS / SYS. Además, no existen reglas fijas para guiar el tamaño de la muestra y las unidades primarias de muestreo (UPM) más que para encontrar un compromiso entre el número total de observaciones y un nivel razonable de incertidumbre para las estimaciones dentro de la UPM (Sannier et al. , 2013) [^ fn9]. En lugar de crear ejemplos, revisaremos dos ejemplos en la literatura.

El primer ejemplo es Potapov et al. (2014) [^ fn7] quien estimó el área de pérdida forestal 2000-2011 en la Amazonía peruana en apoyo de REDD +. La principal fuente de datos de referencia fueron las imágenes comerciales de alta resolución. Se eligió un diseño de dos etapas para ahorrar costos, ya que el presupuesto permitía comprar solo 30 conjuntos de datos de alta resolución. En un diseño de dos etapas, los datos de referencia solo son necesarios para las UPM y no para toda el área de estudio. En consecuencia, el tamaño de la muestra de las 30 UPM se determinó sobre la base de razones presupuestarias y no especificando una precisión objetivo como en los ejemplos anteriores. Se eligió el tamaño de las unidades de suministro de energía de 12 × 12 km para alinearse con las imágenes de alta resolución. Los 5,532 bloques que cubren el área de estudio, cada uno de 12 × 12 km, se separaron en un estrato de cambio forestal alto (337 bloques) y bajo (5,195 bloques), de los cuales se seleccionaron 21 y 9 UPM bajo STR. Esta selección se guió por las reglas de asignación de muestra óptima de Cochran (1977) [^ fn4]. Dentro de cada una de las 30 UPM, se seleccionaron 100 unidades de muestreo secundarias (SSU) según el SRS en la segunda etapa del muestreo.

Un segundo ejemplo se proporciona en Sannier et al. (2013) [^ fn9] quien estimó la proporción de cobertura forestal y deforestación neta en Gabón utilizando un muestreo en dos etapas. Se eligió el muestreo en dos etapas porque representaba un compromiso entre la facilidad de recopilación de datos y la distribución geográfica. El área de estudio se dividió en 251 bloques de 20 × 20 km, cada uno de los cuales se dividió en 100 bloques de 2 × 2 km. En la primera etapa, se seleccionó una PSU de 2 × 2 km en cada uno de los 251 bloques de 20 x 20 km bajo SRS. En la segunda etapa, se seleccionaron 50 SSU correspondientes a un píxel Landsat bajo SRS.  

## 6. Software que permite la estimación de tamaño de muestra

SEPAL/CEO tiene apoyo integrado para estimar el tamaño de muestra como se explica en esta documentación siguiente (en la sección 14).  

Esta hoja de calculo es similar a SEPAL y fue desarrollada por el Banco Mundial. También calcula el tamaño de muestra requerido para obtener una precisión de exactitud general: https://onedrive.live.com/view.aspx?resid=9815683804F2F2C7!37340&ithint=file%2cxlsx&authkey=!ANcP-Xna7Knk_EE



## 7. Seleccionando la muestra

El paso final del diseño de muestreo es extraer físicamente la muestra del área de estudio, que se trata en el siguiente tutorial.



## 4 Preguntas Frecuentes

**No entiendo la variable *qh* que se usa para calcular el tamaño de la muestra en STR, ¿qué significa?**

La variable *qh* es necesaria para calcular la desviación estándar del estrato *h* y es la proporción del estrato *h* que es la clase objetivo. En el ejemplo anterior, tenemos tres estratos (antes de crear el estrato de amortiguamiento), *h* = 1 es bosque, *h* = 2 no es bosque, y *h* = 3 es perturbación del bosque, siendo este último el objetivo clase. En este caso, *qh* es la proporción de perturbación forestal en cada estrato. Si el mapa fuera perfecto, entonces toda la perturbación del bosque en el área de estudio estaría presente en el estrato de perturbación del bosque y, por lo tanto, *q3* = 1, mientras que *q1* y *q2* serían cero. Ningún mapa es perfecto y tendremos que asumir algún nivel de error de clasificación. Tenga en cuenta que esta información se desconoce en la etapa de diseño y es necesaria una conjetura educada. Por ejemplo, si *q3* = 0.8, entonces asumimos que el 80% de la perturbación del bosque en el estudio está presente en el estrato de perturbación del bosque. Si *q1* = 0.001, entonces asumimos que 0.1% del estrato forestal es perturbación forestal.

**No se como determinar valores de qh --¿qué debo hacer?**

La variable *qh* es, en esencia, una indicación de qué tan bien la estratificación captura la clase de interés. Debido a que los mapas se utilizan normalmente para estratificar el área de estudio, recomendaría revisar la precisión de los mapas anteriores de la misma área. Tenga en cuenta que *qh* para *h* = la clase de interés, es la precisión anticipada del usuario de la clase de interés.

**¿Cómo determino un error estándar objetivo?**

Ciertos programas especifican una precisión deseada o requerida; el Forest Carbon Partnership Facility (FCPF), por ejemplo, estipula un margen de error del 30% con un nivel de confianza del 95% para las estimaciones de superficie de los datos de actividad. El margen de error es 1,96 veces el error estándar dividido por el área estimada. Cuando no se especifican tales requisitos de precisión, es necesario determinar un error estándar objetivo en función de otros criterios. Tenga en cuenta que cuanto menor sea la proporción de área de la clase objetivo, mayor será la muestra necesaria para alcanzar un pequeño margen de error. En consecuencia, para proporciones de área pequeñas, la precisión del objetivo deberá relajarse para evitar tener que seleccionar una muestra muy grande.

**Si utilizo un estrato de búfer, ¿cuántos píxeles debería tener?**

Es difícil proporcionar recomendaciones ya que el tamaño del búfer dependerá de las situaciones. Un búfer más grande probablemente "capturará" más errores de omisión, pero tendrá un mayor peso de estrato. Se recomienda una zona de amortiguamiento más grande en situaciones de una clase de interés pequeña en presencia de un estrato estable grande (como un bosque estable). Los ejemplos en la literatura varían de 1 a 3 píxeles. Una exploración más detallada del impacto del tamaño de la zona de influencia se presenta en Olofsson et al. (2020).



## Licencia

Este trabajo tiene licencia bajo [Creative Commons Attribution 3.0 IGO](https://creativecommons.org/licenses/by/3.0/igo/) 

Copyright 2020, World Bank. Este trabajo fue desarrollado por Pontus Olofsson bajo contrato del World Bank con GRH Consulting, LLC para el desarrollo de recursos nuevos o existentes relacionadas a la Medida, Reportaje, y Verificación para el apoyo de implementación MRV en varios países. 

Material revisado por:
Ana Mirian Villalobos, El Salvador, Ministry of Environment and Natural Resources
Carole Andrianirina, Madagascar, National Coordination Bureau REDD+ (BNCCREDD)
Foster Mensah, Ghana, Center for Remote Sensing and Geographic Information Services (CERGIS)
Jennifer Juliana Escamilla Valdez, El Salvador, Ministry of Environment and Natural Resources
Paula Andrea Paz, Colombia, International Center for Tropical Agriculture (CIAT)
Phoebe Oduor, Kenya, Regional Centre For Mapping Of Resources For Development (RCMRD)
Rajesh Bahadur Thapa, Nepal, International Centre for Integrated Mountain Development (ICIMOD)
Tatiana Nana, Cameroon, REDD+ Technical Secretariat



Atribución: Olofsson, P. (2021). *Open MRV: Sampling Design*. World Bank. License: Creative Commons Attribution license (CC BY 3.0 IGO)

## Referencias

[^fn1]: Stehman, S. V., & Czaplewski, R. L. (1998). Design and analysis for thematic map accuracy assessment: fundamental principles. *Remote Sensing of Environment*, 64(3), 331-344.
[^fn2]: GFOI (2016). *Integration of remote-sensing and ground-based observations for estimation of emissions and removals of greenhouse gases in forests: Methods and guidance from the Global Forest Observations Initiative* (2nd ed.), Rome: UN Food and Agriculture Organization
[^fn3]: Stehman, S. V. (2009). Sampling designs for accuracy assessment of land cover. *International Journal of Remote Sensing*, 30, 5243-5272.
[^fn4]: Cochran, W. G. (1977). Sampling techniques (3rd ed.), New York: Wiley
[^fn5]: Olofsson, P., Foody, G. M., Herold, M., Stehman, S. V., Woodcock, C. E., & Wulder, M. A. (2014). Good practices for estimating area and assessing accuracy of land change. *Remote Sensing of Environment*, 148, 42-57.
[^fn6]: Olofsson, P., Arévalo, P., Espejo, A. B., Green, C., Lindquist, E., McRoberts, R. E., & Sanz, M. J. (2020). Mitigating the effects of omission errors on area and area change estimates. *Remote Sensing of Environment*, 236, 111492.   
[^fn7]: Potapov, P. V., Dempewolf, J., Talero, Y., Hansen, M. C., Stehman, S. V., Vargas, C., ... & Giudice, R. (2014). National satellite-based humid tropical forest change assessment in Peru in support of REDD+ implementation. *Environmental Research Letters*, 9, 124012.
[^fn8]: Lohr, S. L. (1999). *Sampling: Design and Analysis: Design And Analysis*. CRC Press.
[^fn9]: Sannier, C., McRoberts, R. E., Fichet, L. V., & Makaga, E. M. K. (2014). Using the regression estimator with Landsat data to estimate proportion forest cover and net proportion deforestation in Gabon. *Remote Sensing of Environment*, 151, 138-148.