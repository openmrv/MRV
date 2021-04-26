---
title: Diseño de respuesta en AREA2
summary: Este tutorial explicará cómo utilizar AREA2 para el diseño de respuestas y la recopilación de observaciones de referencia. AREA2, abreviatura de Area Estimation & Accuracy Assessment, es una aplicación de Google Earth Engine que brinda soporte integral para muestreo y estimación en un marco de inferencia basado en diseño. Para obtener más información sobre AREA2, consulte https://area2.readthedocs.io/en/latest/.
author: Pontus Olofsson
creation date: febrero 2021
language: español
publisher and license: Copyright 2021, World Bank. Este trabajo tiene licencia bajo un Creative Commons Attribution 3.0 IGO

tags:
- OpenMRV
- Teledetección
- GEE
- AREA2
- Serie de tiempo
- Diseño de respuesta
- Encuesta
- Diseño de encuesta 
- Datos de referencia
- Clasificación de referencia
- Observaciones de referencia
- Colombia

group:
- categoría: GEE
  etapa: Colección de datos de referencia
---

# Diseño de Respuesta en AREA2 

## 1 Contexto
En este tutorial, aprenderá a determinar las condiciones de referencia examinando un conjunto de datos de referencia en ubicaciones de las unidades de un conjunto de datos de muestra utilizando AREA2. Este conjunto de datos de muestra tendrá cuatro estratos: bosque, no bosque, perturbación del bosque y una zona de amortiguamiento alrededor de la perturbación del bosque. El objetivo es estimar el área de perturbación forestal; en consecuencia, aprenderá a recopilar observaciones de referencia de bosques, no bosques y perturbaciones forestales. También puede utilizar otras herramientas para lograr esto. Puede encontrar más tutoriales aquí sobre OpenMRV en "Recopilación de datos de muestra" y herramientas "CE" y "CEO".

AREA2, abreviatura de Area Estimation & Accuracy Assessment (Estimación de Area y de Precisión de Mapa), es una aplicación de Google Earth Engine que brinda soporte integral para muestreo y estimación en un marco de inferencia basado en diseño. Para obtener más información sobre AREA2, consulte https://area2.readthedocs.io/en/latest/. 

El diseño de respuesta define la "respuesta" de las unidades en una muestra. En el contexto de la inferencia basada en el diseño en un contexto geográfico, "el diseño de respuesta abarca todos los pasos del protocolo que conducen a una decisión sobre el acuerdo de las clasificaciones de referencia y mapa [y] la mejor clasificación disponible de [condiciones de la superficie terrestre] para cada unidad espacial muestreada "(Olofsson et al. 2014) [^ fn1]. De importancia los siguientes términos:

**Datos de referencia**

Datos que caracterizan la evaluación disponible más precisa de la condición real en la ubicación de la muestra (ejemplo: imágenes de satélite de resolución fina).

**Observaciones de referencia**

La evaluación disponible más precisa de la verdadera condición de una unidad de población.

**Clasificación de referencia**

La clasificación de referencia aplicada a la colección de todas las unidades de muestra.

**Diseño de Respuesta**

Definido por Stehman and Czaplewski, 1998[^fn1]: “La referencia o clasificación 'verdadera' se obtiene para cada unidad de muestreo en función de la interpretación de fotografías aéreas o videografías, una visita terrestre o una combinación de estas fuentes. Los métodos utilizados para determinar esta clasificación de referencia se denominan "diseño de respuesta". El diseño de respuesta incluye procedimientos para recopilar información relacionada con la determinación de la cobertura terrestre de referencia y reglas para asignar una o más [etiquetas] de referencia a cada unidad de muestreo ". Conocido como "plan de medición" por Särndal et al. (1992)[^fn2].

**Muestra**

Un subconjunto de unidades de población seleccionadas de la población.

**Diseño de Muestra**

Sinónimo de diseño de muestreo, que es el término preferido en la literatura fundamental (Cochran, 1977 [^ fn3], Särndal et al., 1992 [^ fn2]). El término aparece en Rice (1995) [^ fn4] que utiliza tanto "diseño de muestreo" como "diseño de muestra".

**Diseño de Muestreo**

"El diseño de muestreo es el protocolo mediante el cual se seleccionan las unidades de muestra de referencia". (Stehman y Czaplewski, 1998) [^ fn1]. El “diseño de muestreo” también es utilizado por Cochran (1977) [^ fn3] y Särndal et al. (1992) [^ fn2]- el primero también usa "plan de muestreo".

**Encuesta**

Särndal y col. (1992) [^ fn2] define una encuesta como una “investigación parcial de una población finita”, y además que “los términos 'encuesta' y 'encuesta por muestreo' se utilizan para denotar investigaciones estadísticas con las siguientes características metodológicas: [. ..] plan de medición [...] de muestreo probabilístico [y] estimación."

**Diseño de Encuesta**

Un "diseño total de la encuesta" define los procedimientos para "obtener la posible precisión en las estimaciones de la encuesta mientras se logra un equilibrio entre los errores de muestreo y los no muestrales [...] El diseño de la encuesta da lugar a operaciones de encuesta" como la selección de la muestra (Särndal et al., 1992) [^ fn2]. Lohr (1999) [^ fn5] describe un diseño de encuesta total como "Una filosofía de diseño de encuesta para minimizar los errores de muestreo y de no muestreo". Además, en Lohr (1999) “diseño de encuestas” es sinónimo de diseño de muestreo.

En este tutorial, determinaremos las condiciones de referencia examinando un conjunto de datos de referencia en ubicaciones de las unidades de la muestra que extrajimos de Colombia en el tutorial anterior. Definimos cuatro estratos: bosque, no bosque, disturbio del bosque, y un amortiguador alrededor de la perturbación del bosque. El objetivo es estimar el área de disturbio forestal; en consecuencia, recopilaremos observaciones de referencia de *bosque, no bosque* y *disturbio del bosque*.

## 2 Objetivos de Aprendizaje

Al completar el tutorial, el usuario debería poder mostrar un conjunto de datos de referencia en ubicaciones de unidades de muestra diseñadas y extraídas de un área de estudio. El usuario debería poder determinar las condiciones de referencia en la superficie terrestre examinando series de tiempo de datos Landsat en combinación con datos de alta resolución en Google Earth.

* Mostrar un conjunto de datos de referencia en ubicaciones de unidades de muestra en GEE
* Determinar las condiciones de referencia en la superficie terrestre examinando series de tiempo de datos Landsat en combinación con datos de alta resolución en GEE

### 2.1 Prerrequisitos
* Comprensión general de la interpretación de imágenes. La interpretación de imágenes es el proceso de observar imágenes de resolución espacial moderada, alta o muy alta (de satélites o fotografías aéreas) y etiquetar los objetos de interés en las ubicaciones de las muestras. La interpretación de fotografías es la habilidad central necesaria para determinar de manera efectiva las condiciones de referencia en la superficie terrestre.

## 3 Tutorial: Diseño de respuesta en AREA2

### 3.1 Preparar datos de referencia
El primer paso es extraer series de tiempo de datos Landsat en ubicaciones de muestra. Hacemos esto usando el script Save Feature Timeseries: https://code.earthengine.google.com/f358347952e3c362f3bb930e3eda095d. Este script no tiene una GUI, pero todo lo que tenemos que hacer es apuntar el script al activo GEE que contiene la muestra. En la parte superior del script, simplemente agregue la siguiente línea especificando la ubicación de la muestra (aquí estamos demostrando el ejercicio usando un conjunto de datos de muestra generado en otro tutorial aquí en OpenMRV bajo el proceso "Selección de muestra" y las herramientas "AREA2" y "QGIS "):
 ```
 var sample = ee.FeatureCollection('users/olofsson76/Open_MRV/STR_sample_Col')
 ```
 También debe cambiar las fechas de inicio y de final en el script de acuerdo a su periodo de estudio. Haga clic en Run en la pestaña Tasks y guarde el resultado como un asset de GEE. Nómbrelo "[filename]_TS".


### 3.2 Examinar datos de referencia en ubicaciones de muestra

El colector de referencia esta ubicado [aquí.](https://code.earthengine.google.com/bd82e0554cdca38a4cedb56600cdeaf0) Una vez que se haya cargado, especifique una ruta para guardar su trabajo bajo "Inputs and Outputs" (Insumos y Resultados) y por "Link to FC" (Enlazar a FC), especifique la ubicación del asset que contiene la muestra después de ser procesado usando el script de "Save Feature Timeseries" como se describió previamente. Active "Load chart data from feature collection" (Cargar datos del grafico de la colección de objetos) y haga clic en "Load" (Cargar). Esto debería de visualizar el tamaño de la muestra -- en mi caso, estoy usando una muestra de 535 unidades que fue diseñada en el tutorial de diseño de muestreo. 

Para comenzar, en "Interpretación de la muestra", especifique "1" y presione enter; esto mostrará los datos de referencia para la primera unidad de la muestra. Son importantes los gráficos de series de tiempo en el centro de la interfaz: las series de tiempo se muestran para las bandas Landsat rojo, infrarrojo cercano (NIR) e infrarrojo de onda corta (SWIR1), y para las transformaciones Tasseled Cap (Kauth-Thomas) Brillo, Verdor y Humedad. Los primeros seis gráficos muestran datos de series de tiempo para el período de estudio especificado en la secuencia de comandos Save Features Timeseries anterior; puede hacer zoom en un cierto intervalo de tiempo y los gráficos se pueden abrir en una ventana separada haciendo clic en la flecha junto a cada gráfico. Los últimos seis gráficos son gráficos de series de tiempo anuales acumuladas, de modo que los datos de cada año se grafican "uno encima del otro". 

Encima de los datos de la serie temporal está el contorno de la unidad de muestra colocada encima de las imágenes de satélite GEE predeterminadas; haga clic en "KML" para mostrar datos de alta resolución en Google Earth en ubicaciones de muestra.

![](./figures/AREA2_ref_collector.png)

Por ahora, recomendamos al usuario que anote las etiquetas de referencia en una hoja de cálculo separada, ya que la implementación de guardar las etiquetas de referencia en una única colección de características está en curso. Aquí se proporcionan videos que ilustran cómo observar las condiciones de referencia mediante el examen de los datos de referencia (los videos son parte del proyecto de [NASA MEaSUREs GLanCE project en Boston University](http://sites.bu.edu/measures/)):  
https://drive.google.com/file/d/1Y_D49kE_oiXxGEJEcPGT8FavrzdMj2qh/view?usp=sharing
https://drive.google.com/file/d/1Md5NajZAngJsVWWiTCbgSdLiEyw7u6BE/view?usp=sharing

## 4 Preguntas Frecuentes

**¿Si no puedo determinar las condiciones de referencia en la ubicación de la unidad de muestra, puedo descartar esa unidad de la muestra?**

Es imperativo que las observaciones de referencia representen condiciones de referencia; por lo tanto, es mejor descartar una unidad de muestra que adivinar. Al mismo tiempo, la eliminación de unidades porque la provisión de etiquetas de referencia es imposible viola las reglas del muestreo probabilístico. Por estas razones, es difícil proporcionar consejos acerca de cuántas unidades de muestra se pueden descartar. (Un colega de renombre me dijo una vez que es aceptable eliminar descarte hasta el 15% de las unidades de la muestra, pero no quería que se le cotizara, y no he encontrado ningún apoyo para esta cifra en la literatura).



## Referencias
Cochran, W.G., 1977. *Sampling Techniques*, John Wiley & Sons, New York, NY.

Lohr, S.L., 1999. *Sampling: Design And Analysis,* CRC Press.

Olofsson, P., Foody, G.M., Herold, M., Stehman, S.V., Woodcock, C.E. and Wulder, M.A., 2014. Good practices for estimating area and assessing accuracy of land change. Remote Sensing of Environment, 148, pp.42-57. https://doi.org/10.1016/j.rse.2014.02.015

Rice, J.A., 1995. *Mathematical Statistics and Data Analysis* (2nd ed.), Duxbury Press, Belmont, CA.

Särndal, C.E., Svensson, B.H., & Wretman, J.H., 1992. *Model assisted survey sampling*, Springer Science & Business Media, New York, NY.

Stehman, S.V., & Czaplewski, R.L., 1998. Design and analysis for thematic map accuracy assessment: fundamental principles. *Remote Sensing of Environment*, 64(3), 331-344. https://doi.org/10.1016/S0034-4257(98)00010-8

-----

![](figures/cc.png)  

Este trabajo tiene licencia bajo un [Creative Commons Attribution 3.0 IGO](https://creativecommons.org/licenses/by/3.0/igo/) 

Copyright 2021, World Bank. 

Este trabajo fue desarrollado por Pontus Olofsson bajo contrato del World Bank con GRH Consulting, LLC para el desarrollo de recursos nuevos o existentes relacionadas a la Medida, Reportaje, y Verificación para el apoyo de implementación MRV en varios países. 

Material revisado por:
Ana Mirian Villalobos, El Salvador, Ministry of Environment and Natural Resources
Carole Andrianirina, Madagascar, National Coordination Bureau REDD+ (BNCCREDD)
Jennifer Juliana Escamilla Valdez, El Salvador, Ministry of Environment and Natural Resources
Phoebe Oduor, Kenya, Regional Centre For Mapping Of Resources For Development (RCMRD)
Tatiana Nana, Cameroon, REDD+ Technical Secretariat

Atribución: 
Olofsson, P. 2021. Response Design in AREA2. © World Bank. License: [Creative Commons Attribution license (CC BY 3.0 IGO)](http://creativecommons.org/licenses/by/3.0/igo/)

![](figures/wb_fcfc_gfoi.png)
