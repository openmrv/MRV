# Diseño de Respuesta en AREA2 

## 1. Contexto
El diseño de respuesta define la "respuesta" de las unidades en una muestra. En el contexto de la inferencia basada en el diseño en un contexto geográfico, "el diseño de respuesta abarca todos los pasos del protocolo que conducen a una decisión sobre el acuerdo de las clasificaciones de referencia y mapa [y] la mejor clasificación disponible de [condiciones de la superficie terrestre] para cada unidad espacial muestreada "(Olofsson et al. 2014) [^ fn1]. De importancia los siguientes términos:

**Datos de referencia**
Datos que caracterizan la evaluación disponible más precisa de la condición real en la ubicación de la muestra (ejemplo: imágenes de satélite de resolución fina).

**Observaciones de referencia**
La evaluación disponible más precisa de la verdadera condición de una unidad de población.

**Clasificación de referencia**
La clasificación de referencia aplicada a la colección de todas las unidades de muestra.

En este tutorial, determinaremos las condiciones de referencia examinando un conjunto de datos de referencia en ubicaciones de las unidades de la muestra que extrajimos de Colombia en el tutorial anterior. Definimos cuatro estratos: bosque, no bosque, disturbio del bosque, y un amortiguador alrededor de la perturbación del bosque. El objetivo es estimar el área de disturbio forestal; en consecuencia, recopilaremos observaciones de referencia de *bosque, no bosque* y *disturbio del bosque*.

## 2. Preparar datos de referencia
El primer paso es extraer series de tiempo de datos Landsat en ubicaciones de muestra. Hacemos esto usando el script Save Feature Timeseries: https://code.earthengine.google.com/?scriptPath=projects%2FGLANCE%3Aglance%2Fsubmit%2FprepareTS%2FextractTS_getRegion Este script no tiene una GUI pero todo lo que tenemos que hacer es dirigir el script al asset de GEE que contiene la muestra. En la parte superior del script, simplemente agregue la siguiente línea especificando la ubicación de la muestra seleccionada en el paso anterior:
 ```
 var sample = ee.FeatureCollection('users/olofsson76/Open_MRV/STR_sample_Col')
 ```
 También debe cambiar las fechas de inicio y de final en el script de acuerdo a su periodo de estudio. Haga clic en Run en la pestaña Tasks y guarde el resultado como un asset de GEE. Nómbrelo "[filename]_TS".


## 3. Examinar datos de referencia en ubicaciones de muestra

El colector de referencia esta ubicado [aquí.](https://code.earthengine.google.com/09964c3fbb9a7d9f8530ee687be8bb90) Una vez que se haya cargado, especifique una ruta para guardar su trabajo bajo "Inputs and Outputs" (Insumos y Resultados) y por "Link to FC" (Enlazar a FC), especifique la ubicación del asset que contiene la muestra después de ser procesado usando el script de "Save Feature Timeseries" como se describió previamente. Active "Load chart data from feature collection" (Cargar datos del grafico de la colección de objetos) y haga clic en "Load" (Cargar). Esto debería de visualizar el tamaño de la muestra -- en mi caso, estoy usando una muestra de 535 unidades que fue diseñada en el tutorial de diseño de muestreo. 

Para comenzar, en "Interpretación de la muestra", especifique "1" y presione enter; esto mostrará los datos de referencia para la primera unidad de la muestra. Son importantes los gráficos de series de tiempo en el centro de la interfaz: las series de tiempo se muestran para las bandas Landsat rojo, infrarrojo cercano (NIR) e infrarrojo de onda corta (SWIR1), y para las transformaciones Tasseled Cap (Kauth-Thomas) Brillo, Verdor y Humedad. Los primeros seis gráficos muestran datos de series de tiempo para el período de estudio especificado en la secuencia de comandos Save Features Timeseries anterior; puede hacer zoom en un cierto intervalo de tiempo y los gráficos se pueden abrir en una ventana separada haciendo clic en la flecha junto a cada gráfico. Los últimos seis gráficos son gráficos de series de tiempo anuales acumuladas, de modo que los datos de cada año se grafican "uno encima del otro". 

Encima de los datos de la serie temporal está el contorno de la unidad de muestra colocada encima de las imágenes de satélite GEE predeterminadas; haga clic en "KML" para mostrar datos de alta resolución en Google Earth en ubicaciones de muestra.

 [image: AREA2_ref_collector.png]

Por ahora, recomendamos al usuario que anote las etiquetas de referencia en una hoja de cálculo separada, ya que la implementación de guardar las etiquetas de referencia en una única colección de características está en curso. Aquí se proporcionan videos que ilustran cómo observar las condiciones de referencia mediante el examen de los datos de referencia (los videos son parte del proyecto de [NASA MEaSUREs GLanCE project en Boston University](http://sites.bu.edu/measures/)):  
https://drive.google.com/file/d/1Y_D49kE_oiXxGEJEcPGT8FavrzdMj2qh/view?usp=sharing
https://drive.google.com/file/d/1Md5NajZAngJsVWWiTCbgSdLiEyw7u6BE/view?usp=sharing

## Licencia
Este trabajo tiene licencia bajo un [Creative Commons Attribution 3.0 IGO](https://creativecommons.org/licenses/by/3.0/igo/) 

Copyright 2020, World Bank. Este trabajo fue desarrollado por Pontus Olofsson bajo contrato del World Bank con GRH Consulting, LLC para el desarrollo de recursos nuevos o existentes relacionadas a la Medida, Reportaje, y Verificación para el apoyo de implementación MRV en varios países. 

Atribución: Olofsson, P. (2021). *Open MRV: Response Design*. World Bank. License: Creative Commons Attribution license (CC BY 3.0 IGO)

## Referencias
[^fn1]: Olofsson, P., Foody, G. M., Herold, M., Stehman, S. V., Woodcock, C. E., & Wulder, M. A. (2014). Good practices for estimating area and assessing accuracy of land change. *Remote Sensing of Environment*, 148, 42-57.
