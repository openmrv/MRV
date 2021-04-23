---
title: Simple random/systematic sampling
summary: Sampling-based approaches in a remote sensing or geographical context are necessary because they allow us to estimate area bias, map accuracy and uncertainty. A sampling-based approach to estimation can be separated into three different components - sampling design, response design and analysis (Stehman & Czaplewski, 1998). The first component, sampling design, is illustrated in this tutorial for the case of simple random/systematic sampling design. Other tutorials here on OpenMRV under process "Sampling design" explore other sampling design approaches (e.g. Stratified Random Sampling).
author: Pontus Olofsson
creation date: February, 2021
language: English
publisher and license: Copyright 2021, World Bank. This work is licensed under a Creative Commons Attribution 3.0 IGO

tags:
- OpenMRV
- Landsat
- Sentinel 2
- Sentinel 1
- GEE
- QGIS
- AREA2
- Cloud cover
- Optical sensors
- Remote sensing
- Composite
- Mosaic
- Time series
- Change detection
- Land cover mapping
- Forest mapping
- Deforestation mapping
- Degradation mapping
- Forest degradation mapping
- Sampling design
- Sample design
- Sample selection
- Sample
- Sampling frame
- Stratified
- Simple Random
- Systematic
- Response design
- Survey
- Survey design
- Accuracy
- Accuracy assessment
- Area Estimation
- Reference data
- Reference classification
- Reference observations
- Colombia

group:
- category: Stratified
  stage: Sampling
- category: Simple Random
  stage: Sampling
- category: Cluster
  stage: Sampling
- category: Systematic
  stage: Sampling
- category: Stratified
  stage: Area Estimation/Accuracy assessment
- category: Expansion
  stage: Area Estimation/Accuracy assessment
- category: Model-assisted
  stage: Area Estimation/Accuracy assessment
- category: Ratio
  stage: Area Estimation/Accuracy assessment
---

# Simple random/systematic sampling

## 1 Contexto

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

## 3 Tutorial: Sampling design for estimation of area and map accuracy - Simple random/systematic sampling

### 3.1 Como escoger un diseño de muestreo?

La elección de un diseño de muestreo a menudo implica compensaciones entre diferentes criterios y prioridades. El deseo de proporcionar estimaciones para las subregiones o la necesidad de alcanzar objetivos de precisión deberá equilibrarse con los criterios de diseño de muestreo deseables, como la facilidad y practicidad de la implementación, la rentabilidad, y la facilidad para adaptarse a los cambios en el tamaño de la muestra. Stehman (2009) [^ fn3] proporciona un repaso detallado de las opciones, objetivos, y criterios de diseño de muestreo, pero la decisión generalmente se reduce a tres decisiones clave: si usar estratos, si usar conglomerados, y si implementar un sistema sistemático o un protocolo simple de selección aleatoria.

#### 3.1.1 Usar estratos?

Los estratos son “subpoblaciones que no se superponen y que juntas comprenden toda la población” (Cochran, 1977, p. 89) [^ fn4]. La estratificación del área de estudio antes de la selección de la muestra puede garantizar que se obtengan estimaciones de precisión y área para ciertas subregiones en el área de estudio, y da como resultado una mayor precisión de las estimaciones. En consecuencia, existen varias buenas razones para utilizar estratos. Incluso con un muestreo aleatorio simple, el uso de estratos después de seleccionar la muestra es una [buena idea](### markdown-header-3.1-Post-estratificación). El muestreo estratificado proporciona una ventaja obvia si estamos interesados en una proporción muy pequeña del área de estudio, como suele ser el caso de los MRV tropicales. Por ejemplo, el área de pérdida de bosques, incluso en países con una deforestación desenfrenada, a menudo es una proporción muy pequeña del país, especialmente en intervalos de tiempo cortos. El uso de un mapa de pérdida de bosques (y otras categorías) para estratificar el área de estudio en tales situaciones permite un muestreo específico en áreas de interés particular. No estratificar en tales situaciones requerirá un tamaño de muestra muy grande.

#### 3.1.2 Usar selección simple aleatoria o sistemática?

La selección sistemática implica seleccionar un punto de partida al azar con la misma probabilidad y luego muestrear con una distancia fija entre las ubicaciones de las muestras. En resumen, la selección aleatoria simple es preferible si se recopilan observaciones de referencia en datos satelitales, mientras que la selección sistemática es preferible si se visitan ubicaciones de muestreo in situ (Olofsson et al. 2014) [^ fn5]. El fundamento de esta recomendación es que las unidades seleccionadas sistemáticamente son más fáciles de ubicar en el campo, mientras que la selección aleatoria es más fácil de aumentar. Tenga en cuenta que los mismos estimadores se utilizan tanto con selección aleatoria simple como con selección sistemática.

#### 3.1.3 Usar conglomerado?

Un conglomerado es una unidad de muestreo que consta de una o más de las unidades de evaluación básicas especificadas por el diseño de respuesta. Por ejemplo, un grupo podría ser un bloque de 9 pixeles 3 × 3 o un grupo de 1 km × 1 km que contenga 100 unidades de evaluación de 1 ha. En el muestreo de conglomerados, se selecciona una muestra de conglomerados y, por lo tanto, las unidades espaciales dentro de cada conglomerado se seleccionan como un grupo en lugar de seleccionarse como entidades individuales. El muestreo en dos etapas es una forma de muestreo por conglomerados en el que se seleccionan grandes unidades primarias de muestreo (UPM) en la primera etapa. Las unidades de muestreo secundarias (SSU por sus siglas en ingles) más pequeñas se seleccionan dentro de cada UPM en la segunda etapa. Dichos diseños tienen la ventaja de requerir datos de referencia (es decir, los datos utilizados para recopilar observaciones de referencia) solo sobre las UPM en lugar de toda el área de estudio, como es el caso de los diseños mencionados anteriormente. Sin embargo, a menos que los ahorros de costos sean considerables, los diseños basados en conglomerados no se recomiendan ya que la correlación entre SSU a menudo reduce la precisión en relación con una muestra aleatoria simple de igual tamaño, y porque son diseños complicados que son difíciles de aumentar con resultados de muestra que son difícil de analizar.

### 3.2 Muestreo aleatorio simple/sistemático

Si las unidades (por ejemplo, pixeles) de una población/área de estudio están enumeradas de 1 a *N*, el muestreo aleatorio simple (SRS) es “Un método para seleccionar *n* unidades de *N* de tal manera que cada una de estos [los conjuntos de *n* unidades especificadas] tiene una probabilidad igual de ser seleccionado” (Cochran 1977, p. 18)[^fn4]. En un contexto geográfico, frecuentemente estamos interesados en estimar la proporción de una población/área de estudio de los datos de muestra, como la proporción de área de un tipo de cobertura de suelo o de cambio de cobertura. Usando las nociones de Cochran, las unidades de una población son [![img](https://camo.githubusercontent.com/24075d79a1be7cdb61571f6a8ceb68d58a6c3c1399369df900c56d923f9316e1/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f6769662e6c617465783f253543696e6c696e652673706163653b795f312673706163653b2535436c646f74732673706163653b795f4e)](https://camo.githubusercontent.com/24075d79a1be7cdb61571f6a8ceb68d58a6c3c1399369df900c56d923f9316e1/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f6769662e6c617465783f253543696e6c696e652673706163653b795f312673706163653b2535436c646f74732673706163653b795f4e) de las cuales una muestra [![img](https://camo.githubusercontent.com/6e5cd92f578094ee5fda46b4e476e5661801cf207fe1ef9b903ed86f9a8457fa/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f6769662e6c617465783f253543696e6c696e652673706163653b795f312673706163653b2535436c646f74732673706163653b795f6e)](https://camo.githubusercontent.com/6e5cd92f578094ee5fda46b4e476e5661801cf207fe1ef9b903ed86f9a8457fa/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f6769662e6c617465783f253543696e6c696e652673706163653b795f312673706163653b2535436c646f74732673706163653b795f6e) es seleccionada bajo SRS; lo grabamos [![img](https://camo.githubusercontent.com/52cdecab550e057a3a14457e68aa90be99952930db7abe33da4b146e45764dd2/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f6769662e6c617465783f253543696e6c696e652673706163653b795f693d31)](https://camo.githubusercontent.com/52cdecab550e057a3a14457e68aa90be99952930db7abe33da4b146e45764dd2/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f6769662e6c617465783f253543696e6c696e652673706163653b795f693d31) si la cobertura de suelo de interés es observada en unidad *i* y [![img](https://camo.githubusercontent.com/bc6a9d36a69d8f67c256bb69384819538068971cc76bd8baefadec4e6b660d63/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f6769662e6c617465783f253543696e6c696e652673706163653b795f693d30)](https://camo.githubusercontent.com/bc6a9d36a69d8f67c256bb69384819538068971cc76bd8baefadec4e6b660d63/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f6769662e6c617465783f253543696e6c696e652673706163653b795f693d30) de lo contrario. Una ventaja de SRS es que la media de las observaciones es un estimador insesgado de la proporción de población (*p*) de interés. (Cochran, 1977, Eq 3.3)[^fn4]:

[![img](https://camo.githubusercontent.com/d0263fe4179fb434408059650a1044b68ed963d42042ed3798e19e482cd67abf/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f2535434c617267652673706163653b253543626172253742792537443d25354366726163253742312537442537426e25374425354373756d5f253742693d312537442535452537426e253744795f693d25354368617425374270253744)](https://camo.githubusercontent.com/d0263fe4179fb434408059650a1044b68ed963d42042ed3798e19e482cd67abf/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f2535434c617267652673706163653b253543626172253742792537443d25354366726163253742312537442537426e25374425354373756d5f253742693d312537442535452537426e253744795f693d25354368617425374270253744)

y la varianza de la proporción estimada *p^* es estimada fácilmente como (Cochran, 1977, Eq 3.11)[^fn4]

[![img](https://camo.githubusercontent.com/cbdc4c514304e3b0831a7282c5215208c0140f4212ac71575cc25e59420b497b/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f2535434c617267652673706163653b253543686174253742562537442825354368617425374270253744293d253543667261632537422535436861742537427025374428312d25354368617425374270253744292537442537426e2d31253744)](https://camo.githubusercontent.com/cbdc4c514304e3b0831a7282c5215208c0140f4212ac71575cc25e59420b497b/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f2535434c617267652673706163653b253543686174253742562537442825354368617425374270253744293d253543667261632537422535436861742537427025374428312d25354368617425374270253744292537442537426e2d31253744)

Estos estimadores también son aplicables a datos de muestra recopilados mediante muestreo sistemático simple (SYS por sus siglas en ingles). El análisis sencillo de los datos de muestra recopilados con SRS / SYS y la capacidad de aumentar el tamaño de la muestra con facilidad (especialmente con SRS) hacen que estos diseños sean atractivos.

#### 3.2.1 Posestratificación

Otra ventaja importante de SRS / SYS es la capacidad de estratificar el área de estudio después de que se hayan recolectado los resultados de la muestra; la aplicación de una estratificación posterior al muestreo se denomina posestratificación (PSTR). Es probable que el PSTR aumente la precisión de las estimaciones, y rara vez hay razones para no post-estratificar utilizando mapas.

#### 3.2.2 Tamaño de muestra

Determinar el tamaño de la muestra independientemente del diseño implica calcular el número de unidades en una muestra necesarias para alcanzar una cierta precisión objetivo de una estimación de un parámetro de población de interés. El cálculo se basa en resolver el estimador de varianza correspondiente al diseño para *n*. Si la varianza en el estimador de varianza anterior es la varianza deseada de una estimación, resolver *n* da (Cochran, 1977, Eq. 4.2)[^fn4]

[![img](https://camo.githubusercontent.com/fa88088c6a263ed7966ab90b95c8bfa702a0793df088e02f709989e3e096fb39/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f2535434c617267652673706163653b6e3d253543667261632537422535436861742537427025374428312d253543686174253742702537442925374425374225354368617425374256253744282535436861742537427025374429253744)](https://camo.githubusercontent.com/fa88088c6a263ed7966ab90b95c8bfa702a0793df088e02f709989e3e096fb39/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f2535434c617267652673706163653b6e3d253543667261632537422535436861742537427025374428312d253543686174253742702537442925374425374225354368617425374256253744282535436861742537427025374429253744)

donde *p^* es un estimado de la proporción de unidades en la clase de interés en el área de estudio. Por ejemplo, supongamos que queremos estimar la precisión general (como en Olofsson et al., 2014, p. 53)[^fn5] con un margen de error (*MoE*) de 5%. Definiríamos *p* como la precisión general del mapa. Obviamente no conocemos la precisión general del mapa en este punto así que se requiere una conjetura educada. Si suponemos una precisión general de 80%, un margen de error de 5% se traduciría a una varianza de (la puntuación z de 1.96 en el nivel de confianza de 95% se redondea a 2)

[![img](https://camo.githubusercontent.com/811c93d26457b9e49663479d0985118d502336c1979d048117088530dd7ce7d4/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f2535434c617267652673706163653b4d6f453d25354366726163253742322535437371727425374225354368617425374256253744253744282535436861742537427025374429253744253742253543686174253742702537442537442535434c65667472696768746172726f77253543686174253742562537442825354368617425374270253744293d28253543667261632537424d6f4525354374696d65732673706163653b253543686174253742702537442537442537423225374429253545323d2825354366726163253742302e303525354374696d6573302e382537442537423225374429253545323d302e30303034)](https://camo.githubusercontent.com/811c93d26457b9e49663479d0985118d502336c1979d048117088530dd7ce7d4/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f2535434c617267652673706163653b4d6f453d25354366726163253742322535437371727425374225354368617425374256253744253744282535436861742537427025374429253744253742253543686174253742702537442537442535434c65667472696768746172726f77253543686174253742562537442825354368617425374270253744293d28253543667261632537424d6f4525354374696d65732673706163653b253543686174253742702537442537442537423225374429253545323d2825354366726163253742302e303525354374696d6573302e382537442537423225374429253545323d302e30303034)

el cual nos da un tamaño de muestra de

[![img](https://camo.githubusercontent.com/0d228a3402fa0aa5b648553e40ddb50ade37829d771c90cd127f8adae4d5094b/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f2535434c617267652673706163653b6e3d253543667261632537422535436861742537427025374428312d2535436861742537427025374429253744253742253543686174253742562537442825354368617425374270253744292537443d25354366726163253742302e3828312d302e3829253744253742302e303030342537443d343030)](https://camo.githubusercontent.com/0d228a3402fa0aa5b648553e40ddb50ade37829d771c90cd127f8adae4d5094b/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f2535434c617267652673706163653b6e3d253543667261632537422535436861742537427025374428312d2535436861742537427025374429253744253742253543686174253742562537442825354368617425374270253744292537443d25354366726163253742302e3828312d302e3829253744253742302e303030342537443d343030)

Aunque la estimación de la precisión general se ilustró en Olofsson et al. (2014) [^ fn5], especificar un margen de error de la precisión general del mapa no es intuitivo y rara vez constituye un objetivo de estimación. Un ejemplo más realista sería la estimación del área de deforestación o degradación forestal con cierta precisión. En el tutorial CODED, se creó un mapa de deforestación, degradación forestal, forestal y no forestal para Colombia; para simplificar el asunto, agrupemos la deforestación y la degradación forestal en una sola clase de perturbación forestal, que fue mapeada como 1.4% del país de 2010 a 2020. Note, para la estimación de datos de actividad dentro de REDD+ (y otras iniciativas), se recomienda estimar la deforestación y la degradación por separado y, por lo tanto, utilizar un estrato de deforestación y un estrato de degradación, en lugar de combinar las dos clases en una sola clase de perturbación forestal. Aquí, estamos usando una clase de perturbación combinada para facilitar la ilustración del flujo de trabajo y los cálculos. Supongamos que queremos estimar el área de perturbación del bosque (nuevamente, deforestación y degradación combinadas) con un margen de error del 25%. Tenga en cuenta que el 25% se utiliza aquí simplemente para ilustrar el flujo de trabajo; el error objetivo dependerá de las circunstancias del estudio. Primero, un margen de error de 25% es equivalente a una varianza de

[![img](https://camo.githubusercontent.com/93e57726bc514bee06e8d0b73ecfc4cccf4373b8366d7a5064b9bb64aabfe0e3/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f2535434c617267652673706163653b253543686174253742562537442825354368617425374270253744293d28253543667261632537424d6f4525354374696d65732673706163653b253543686174253742702537442537442537423225374429253545323d2825354366726163253742302e323525354374696d6573302e3031342537442537423225374429253545323d302e303030303033)](https://camo.githubusercontent.com/93e57726bc514bee06e8d0b73ecfc4cccf4373b8366d7a5064b9bb64aabfe0e3/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f2535434c617267652673706163653b253543686174253742562537442825354368617425374270253744293d28253543667261632537424d6f4525354374696d65732673706163653b253543686174253742702537442537442537423225374429253545323d2825354366726163253742302e323525354374696d6573302e3031342537442537423225374429253545323d302e303030303033)

el cual nos da un tamaño de muestra de

[![img](https://camo.githubusercontent.com/dfce4941c2735664ba896945af7acca926fdf8bbd7781e284a6498244ee5e28d/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f2535434c617267652673706163653b6e3d253543667261632537422535436861742537427025374428312d2535436861742537427025374429253744253742253543686174253742562537442870292537443d25354366726163253742302e30313428312d302e30313429253744253742302e3030303030332537443d342c363030)](https://camo.githubusercontent.com/dfce4941c2735664ba896945af7acca926fdf8bbd7781e284a6498244ee5e28d/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f2535434c617267652673706163653b6e3d253543667261632537422535436861742537427025374428312d2535436861742537427025374429253744253742253543686174253742562537442870292537443d25354366726163253742302e30313428312d302e30313429253744253742302e3030303030332537443d342c363030)

La recopilación de observaciones en casi cinco mil ubicaciones de muestra rara vez es posible para un estudio individual. El ejemplo ilustra uno de los inconvenientes de SRS / SYS: debido a que no estamos usando ninguna información sobre la ubicación de la deforestación, se requiere un tamaño de muestra muy grande para lograr una alta precisión. Otra forma más rápida de estimar la muestra en este caso es asumir que necesitamos al menos 30 unidades en áreas de deforestación, lo que requeriría un tamaño de muestra de 30 / 0.014 = 2,142 unidades que es más manejable pero aún grande, y no estamos muestreando para alcanzar un objetivo de precisión. (Baje a la sección **4.3 Asignación** para una explicación de porque 30 es el "numero mágico".)


### 3.3 Software que permite la estimación de tamaño de muestra

SEPAL/CEO tiene apoyo integrado para estimar el tamaño de muestra como se explica en esta documentación siguiente (en la sección 14).

Esta hoja de calculo es similar a SEPAL y fue desarrollada por el Banco Mundial. También calcula el tamaño de muestra requerido para obtener una precisión de exactitud general: https://onedrive.live.com/view.aspx?resid=9815683804F2F2C7!37340&ithint=file%2cxlsx&authkey=!ANcP-Xna7Knk_EE

### 3.4 Seleccionando la muestra

El paso final del diseño de muestreo es extraer físicamente la muestra del área de estudio, que se trata en el siguiente tutorial.

## 4 Preguntas Frecuentes

**¿Cómo determino un error estándar objetivo?**

Ciertos programas especifican una precisión deseada o requerida; el Forest Carbon Partnership Facility (FCPF), por ejemplo, estipula un margen de error del 30% con un nivel de confianza del 95% para las estimaciones de superficie de los datos de actividad. El margen de error es 1,96 veces el error estándar dividido por el área estimada. Cuando no se especifican tales requisitos de precisión, es necesario determinar un error estándar objetivo en función de otros criterios. Tenga en cuenta que cuanto menor sea la proporción de área de la clase objetivo, mayor será la muestra necesaria para alcanzar un pequeño margen de error. En consecuencia, para proporciones de área pequeñas, la precisión del objetivo deberá relajarse para evitar tener que seleccionar una muestra muy grande.

**How do I know if I can use SRS or if I will need a more complex design such as STR?**

The easiest way to determine if simple designs such as SRS and SYS viable is to following the equations in this tutorial to determine the sample size required to reach a certain precision. If the sample size required is too large to be managable, then you might need have to use strata when sampling.


## 5 Terminología relevante para las técnicas de muestreo

Una lista de términos relevantes para las técnicas de muestreo e inferencia esta provista en la documentación de AREA2: https://area2.readthedocs.io/en/latest/definitions.html. Abajo hay algunos términos adicionales que no están incluidos en la documentación.

### 5.1 Diseño de Respuesta

Definido por Stehman and Czaplewski, 1998[^fn1]: “La referencia o clasificación 'verdadera' se obtiene para cada unidad de muestreo en función de la interpretación de fotografías aéreas o videografías, una visita terrestre o una combinación de estas fuentes. Los métodos utilizados para determinar esta clasificación de referencia se denominan "diseño de respuesta". El diseño de respuesta incluye procedimientos para recopilar información relacionada con la determinación de la cobertura terrestre de referencia y reglas para asignar una o más [etiquetas] de referencia a cada unidad de muestreo ". Conocido como "plan de medición" por Särndal et al. (1992)[^fn2].

### 5.2 Muestra

Un subconjunto de unidades de población seleccionadas de la población.

### 5.3 Diseño de Muestra

Sinónimo de diseño de muestreo, que es el término preferido en la literatura fundamental (Cochran, 1977 [^ fn3], Särndal et al., 1992 [^ fn2]). El término aparece en Rice (1995) [^ fn4] que utiliza tanto "diseño de muestreo" como "diseño de muestra".

### 5.4 Diseño de Muestreo

"El diseño de muestreo es el protocolo mediante el cual se seleccionan las unidades de muestra de referencia". (Stehman y Czaplewski, 1998) [^ fn1]. El “diseño de muestreo” también es utilizado por Cochran (1977) [^ fn3] y Särndal et al. (1992) [^ fn2]- el primero también usa "plan de muestreo".

### 5.5 Encuesta

Särndal y col. (1992) [^ fn2] define una encuesta como una “investigación parcial de una población finita”, y además que “los términos 'encuesta' y 'encuesta por muestreo' se utilizan para denotar investigaciones estadísticas con las siguientes características metodológicas: [. ..] plan de medición [...] de muestreo probabilístico [y] estimación."

### 5.6 Diseño de Encuesta

Un "diseño total de la encuesta" define los procedimientos para "obtener la posible precisión en las estimaciones de la encuesta mientras se logra un equilibrio entre los errores de muestreo y los no muestrales [...] El diseño de la encuesta da lugar a operaciones de encuesta" como la selección de la muestra (Särndal et al., 1992) [^ fn2]. Lohr (1999) [^ fn5] describe un diseño de encuesta total como "Una filosofía de diseño de encuesta para minimizar los errores de muestreo y de no muestreo". Además, en Lohr (1999) “diseño de encuestas” es sinónimo de diseño de muestreo.

## Referencias

Cochran, W.G., 1977. *Sampling Techniques*, John Wiley & Sons, New York, NY.

GFOI. 2016. *Integration of remote-sensing and ground-based observations for estimation of emissions and removals of greenhouse gases in forests: Methods and guidance from the Global Forest Observations Initiative* (2nd ed.), UN Food and Agriculture Organization, Rome.

Lohr, S.L., 1999. *Sampling: Design And Analysis,* CRC Press.

Olofsson, P., Arévalo, P., Espejo, A.B., Green, C., Lindquist, E., McRoberts, R.E. and Sanz, M.J., 2020. Mitigating the effects of omission errors on area and area change estimates. Remote Sensing of Environment, 236, p.111492. https://doi.org/10.1016/j.rse.2019.111492

Olofsson, P., Foody, G.M., Herold, M., Stehman, S.V., Woodcock, C.E. and Wulder, M.A., 2014. Good practices for estimating area and assessing accuracy of land change. Remote Sensing of Environment, 148, pp.42-57. https://doi.org/10.1016/j.rse.2014.02.015

Potapov, P.V., Dempewolf, J., Talero, Y., Hansen, M.C., Stehman, S.V., Vargas, C., Rojas, E.J., Castillo, D., Mendoza, E., Calderón, A. and Giudice, R., 2014. National satellite-based humid tropical forest change assessment in Peru in support of REDD+ implementation. Environmental Research Letters, 9(12), p.124012. https://doi.org/10.1088/1748-9326/9/12/124012

Rice, J.A., 1995. Mathematical Statistics and Data Analysis (2nd ed.), Duxbury Press, Belmont, CA.

Sannier, C., McRoberts, R.E., Fichet, L.V. and Makaga, E.M.K., 2014. Using the regression estimator with Landsat data to estimate proportion forest cover and net proportion deforestation in Gabon. Remote Sensing of Environment, 151, pp.138-148. https://doi.org/10.1016/j.rse.2013.09.015

Särndal, C.E., Svensson, B.H., & Wretman, J.H., 1992. Model assisted survey sampling, Springer Science & Business Media, New York, NY.

Stehman, S.V., 2009. Sampling designs for accuracy assessment of land cover. International Journal of Remote Sensing, 30(20), pp.5243-5272. https://doi.org/10.1080/01431160903131000

Stehman, S.V., & Czaplewski, R.L., 1998. Design and analysis for thematic map accuracy assessment: fundamental principles. *Remote Sensing of Environment*, 64(3), 331-344. https://doi.org/10.1016/S0034-4257(98)00010-8



-----

![](./figures/cc.png)  

Este trabajo tiene licencia bajo [Creative Commons Attribution 3.0 IGO](https://creativecommons.org/licenses/by/3.0/igo/)

Copyright 2020, World Bank. Este trabajo fue desarrollado por Pontus Olofsson bajo contrato del World Bank con GRH Consulting, LLC para el desarrollo de recursos nuevos o existentes relacionadas a la Medida, Reportaje, y Verificación para el apoyo de implementación MRV en varios países.

Material revisado por: Ana Mirian Villalobos, El Salvador, Ministry of Environment and Natural Resources Carole Andrianirina, Madagascar, National Coordination Bureau REDD+ (BNCCREDD) Foster Mensah, Ghana, Center for Remote Sensing and Geographic Information Services (CERGIS) Jennifer Juliana Escamilla Valdez, El Salvador, Ministry of Environment and Natural Resources Paula Andrea Paz, Colombia, International Center for Tropical Agriculture (CIAT) Phoebe Oduor, Kenya, Regional Centre For Mapping Of Resources For Development (RCMRD) Rajesh Bahadur Thapa, Nepal, International Centre for Integrated Mountain Development (ICIMOD) Tatiana Nana, Cameroon, REDD+ Technical Secretariat

Atribución: Olofsson, P. 2021. Simple random/systematic sampling. © World Bank. License: [Creative Commons Attribution license (CC BY 3.0 IGO)](http://creativecommons.org/licenses/by/3.0/igo/)

![](./figures/wb_fcfc_gfoi.png)
