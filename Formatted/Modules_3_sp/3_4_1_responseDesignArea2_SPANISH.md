---
title: Response design in AREA2
summary: This tutorial will go through how to use AREA2 for response design and collection of reference observations. AREA2, short for Area Estimation & Accuracy Assessment, is a Google Earth Engine application that provides comprehensive support for sampling and estimation in a design-based inference framework. For more information about AREA2 please refer to https://area2.readthedocs.io/en/latest/
author: Pontus Olofsson
creation date: February, 2021
language: English
publisher and license: Copyright 2021, World Bank. This work is licensed under a Creative Commons Attribution 3.0 IGO

tags:
- OpenMRV
- Remote sensing
- GEE
- AREA2
- Time series
- Response design
- Survey
- Survey design
- Reference data
- Reference classification
- Reference observations
- Colombia

group:
- category: GEE
  stage: Reference data collection
---

# Diseño de Respuesta en AREA2 

## 1 Contexto
AREA2, short for Area Estimation & Accuracy Assessment, is a Google Earth Engine application that provides comprehensive support for sampling and estimation in a design-based inference framework. For more information about AREA2 please refer to https://area2.readthedocs.io/en/latest/. 

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

## 2 Learning Objectives

Upon completion of the tutorial, the user should be able to display a set of reference data at locations of sample units designed and drawn from a study area. The user should be able to determine reference conditions at the land surface by examining time series of Landsat data in combination with high resolution data in Google Earth. 

* Display a set of reference data at locations of sample units in GEE
* Determine reference conditions at the land surface by examining time series of Landsat data in combination with high resolution data in GEE

### 2.1 Pre-requisites
* A general understanding of image interpretation. Image interpretation is the process of looking at moderate, high, or very high spatial resolution imagery (from satellites or aerial photography) and labeling the objects of interest in your sample locations. Photo interpretation is the core skill needed to effectively determine reference conditions at the land surface.

## 3 Tutorial: Response design in AREA2

### 3.1 Preparar datos de referencia
El primer paso es extraer series de tiempo de datos Landsat en ubicaciones de muestra. Hacemos esto usando el script Save Feature Timeseries: https://code.earthengine.google.com/?scriptPath=projects%2FGLANCE%3Aglance%2Fsubmit%2FprepareTS%2FextractTS_getRegion Este script no tiene una GUI pero todo lo que tenemos que hacer es dirigir el script al asset de GEE que contiene la muestra. En la parte superior del script, simplemente agregue la siguiente línea especificando la ubicación de la muestra seleccionada en el paso anterior:
 ```
 var sample = ee.FeatureCollection('users/olofsson76/Open_MRV/STR_sample_Col')
 ```
 También debe cambiar las fechas de inicio y de final en el script de acuerdo a su periodo de estudio. Haga clic en Run en la pestaña Tasks y guarde el resultado como un asset de GEE. Nómbrelo "[filename]_TS".


### 3.2 Examinar datos de referencia en ubicaciones de muestra

El colector de referencia esta ubicado [aquí.](https://code.earthengine.google.com/09964c3fbb9a7d9f8530ee687be8bb90) Una vez que se haya cargado, especifique una ruta para guardar su trabajo bajo "Inputs and Outputs" (Insumos y Resultados) y por "Link to FC" (Enlazar a FC), especifique la ubicación del asset que contiene la muestra después de ser procesado usando el script de "Save Feature Timeseries" como se describió previamente. Active "Load chart data from feature collection" (Cargar datos del grafico de la colección de objetos) y haga clic en "Load" (Cargar). Esto debería de visualizar el tamaño de la muestra -- en mi caso, estoy usando una muestra de 535 unidades que fue diseñada en el tutorial de diseño de muestreo. 

Para comenzar, en "Interpretación de la muestra", especifique "1" y presione enter; esto mostrará los datos de referencia para la primera unidad de la muestra. Son importantes los gráficos de series de tiempo en el centro de la interfaz: las series de tiempo se muestran para las bandas Landsat rojo, infrarrojo cercano (NIR) e infrarrojo de onda corta (SWIR1), y para las transformaciones Tasseled Cap (Kauth-Thomas) Brillo, Verdor y Humedad. Los primeros seis gráficos muestran datos de series de tiempo para el período de estudio especificado en la secuencia de comandos Save Features Timeseries anterior; puede hacer zoom en un cierto intervalo de tiempo y los gráficos se pueden abrir en una ventana separada haciendo clic en la flecha junto a cada gráfico. Los últimos seis gráficos son gráficos de series de tiempo anuales acumuladas, de modo que los datos de cada año se grafican "uno encima del otro". 

Encima de los datos de la serie temporal está el contorno de la unidad de muestra colocada encima de las imágenes de satélite GEE predeterminadas; haga clic en "KML" para mostrar datos de alta resolución en Google Earth en ubicaciones de muestra.

![](./figures/AREA2_ref_collector.png)

Por ahora, recomendamos al usuario que anote las etiquetas de referencia en una hoja de cálculo separada, ya que la implementación de guardar las etiquetas de referencia en una única colección de características está en curso. Aquí se proporcionan videos que ilustran cómo observar las condiciones de referencia mediante el examen de los datos de referencia (los videos son parte del proyecto de [NASA MEaSUREs GLanCE project en Boston University](http://sites.bu.edu/measures/)):  
https://drive.google.com/file/d/1Y_D49kE_oiXxGEJEcPGT8FavrzdMj2qh/view?usp=sharing
https://drive.google.com/file/d/1Md5NajZAngJsVWWiTCbgSdLiEyw7u6BE/view?usp=sharing

## 4 Frequently Asked Questions (FAQs)

**If I can't determine the reference conditions at the location of a sample unit, can I discard that unit from the sample?**

It is imperative that the reference observations represent reference conditions; therefore, it is better to discard a sample unit than guessing. At the same time, removing units because the provision of reference labels is impossible violates the rules of probability sampling. For these reasons, it is difficult to provide guidelines for how many sample units can be discarded. (A renowned colleague of mine once told me that it is acceptable to remove discard up to 15% of the units in sample but he didn't want to be quoted, and I have not found any support for this figure in the literature.)



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

Copyright 2020, World Bank. Este trabajo fue desarrollado por Pontus Olofsson bajo contrato del World Bank con GRH Consulting, LLC para el desarrollo de recursos nuevos o existentes relacionadas a la Medida, Reportaje, y Verificación para el apoyo de implementación MRV en varios países. 

Atribución: Olofsson, P. (2021). *Open MRV: Response Design*. World Bank. License: Creative Commons Attribution license (CC BY 3.0 IGO)
![](figures/wb_fcfc_gfoi.png)
