# Selección de Muestras 

## 1. Contexto

En el tutorial anterior, diseñamos una muestra eligiendo un protocolo de selección y determinando el tamaño y la asignación de la muestra. En este tutorial sacaremos físicamente de un área de estudio la muestra que diseñamos. La extracción de una muestra implica la creación de un *marco de muestreo* que es una lista de unidades de población que se pueden seleccionar para su inclusión en una muestra. Las unidades de población de la lista se denominan unidades de muestreo. En otras palabras, un marco es un dispositivo que proporciona acceso de observación a la población al asociar las unidades de población con las unidades de muestreo (Särndal et al., 1992, p. 9) [^ fn1]. En nuestro caso, el marco de muestreo es, por ejemplo, una lista de todos los píxeles que componen el área de estudio. Por lo tanto, podríamos simplemente exportar una lista de todos los píxeles del mapa con identificadores únicos de los que seleccionamos aleatoriamente *n* unidades. En un muestreo aleatorio estratificado, cada píxel, además del identificador, también tendría un código de estrato de modo que se seleccione una muestra aleatoria de cada estrato. Este enfoque puede resultar fácilmente impráctico ya que el número de unidades de población tiende a ser grande. En cambio, la selección de muestras es compatible con varias herramientas y software; aquí, ilustramos cómo dibujar una muestra en QGIS, Google Earth Engine / AREA2 y un script R.

## 2 Objetivos de Aprendizaje 

- Al completar el tutorial, el usuario debería poder muestrear un área de estudio arbitraria bajo SYS, SRS o STR. El usuario debería poder extraer una muestra en QGIS en SYS o SRS, y una muestra en GEE / AREA2 en STR.

  - Aprender como muestrear un área de estudio arbitraria usando SYS, SRS o STR
  - Dibujar una muestra en QGIS bajo SYS o SRS
  - Dibujar una muestra en GEE/AREA2 bajo STR

  ### 2.1 Prerrequisitos para este módulo 

  - Revisión de la terminología relevante para las técnicas de muestreo en el tutorial 3.1 Terminología y comprensión del tutorial 3.2 Diseño de muestreo para la estimación del área y la precisión del mapa
  - Se recomienda que comprenda los tutoriales anteriores de los Módulos 1 y 2

## 3

#### 3.1. Muestreo aleatorio simple y sistemático en QGIS

QGIS proporciona soporte para el muestreo de poblaciones definidas por datos vectoriales. Por lo tanto, si desea muestrear en estratos definidos por un ráster, primero deberá vectorizar los datos ráster. Esto se hace usando la herramienta Raster> Conversions> "Polygonize (Raster to Vector)". La vectorización de rásteres grandes llevará mucho tiempo y no se recomienda; en su lugar, use las alternativas a continuación. Para áreas de estudio más pequeñas o para diseños SYS y SRS, QGIS funciona bien; repasemos los pasos necesarios para extraer dos muestras bajo SRS y SYS del país de Colombia.
###### Muestreo aleatorio simple
1. Primero necesitamos un shapefile que delinea nuestra área de estudio. Baje el shapefile de la frontera de Colombia aquí: https://drive.google.com/file/d/1tXvczTra_5wrlXBhe00m_oKRpLK0GwwJ/view?usp=sharing
2. Visualice el archivo en QGIS: Layer > Add Layer > "Add Vector Layer" y seleccione colombiaborder.shp para dibujar el shapefile en el lienzo. 
3. Vector > Research Tools > "Random Points Inside Polygons"
4. Especifique que la frontera de Colombia es la capa de insumo, seleccione "Points count as sampling strategy and the total sample size under Point count"; deje la distancia mínima automática, y seleccione "Save to a file" y hacer clic en Run para dibujar la muestra.

[image: SRS_QGIS.png]

###### Muestreo sistemático 
Dibujar una muestra bajo SYS en QGIS tiene el inconveniente de que la población tiene que ser rectangular, lo que dificulta dibujar un número exacto de unidades para un área no rectangular. Simplemente podemos recortar las unidades de muestra para la frontera con Colombia, pero eso dará como resultado un tamaño de muestra más pequeño que el especificado. Una solución alternativa es establecer una distancia entre ellos según el tamaño del área de estudio. Por ejemplo, si el área de estudio es *x* km^2^, establecer un espacio entre unidades ax/100 daría como resultado una muestra de 100 unidades.  
1. Después de agregar el shapefile en la sección 2.1.2 arriba, vaya a Vector > Research Tools > "Regular Points"
2. Seleccione la frontera de Colombia como la extensión de insumo
3. Especifique el espacio de los puntos (Point spacing) o la cantidad de puntos (Point count) -- si usa el espacio, active la cajilla "Use point spacing" 
4. Guarde esto a un archivo y haga clic en Run para visualizar la muestra.

[image: SYS_QGIS.png]

#### 3.2 Muestreo aleatorio estratificado en Google Earth Engine/AREA2
En el script de diseño de muestreo, estimamos el tamaño de muestra requerido para alcanzar el margen de error de 25% de la aproximación de área de disturbio forestal, y asignamos la muestra en estrato para el propósito de estimar el área. Eso nos dio el tamaño de muestra siguiente: 

| | A             | B            | C              |D              |E             |F         |
|-|:--------------|:-------------|:---------------|:--------------|:-------------|:---------|
|1| Estrato (*h*) | Bosque(1) | No-bosque(2) |Dist. Bosq. (3) |Amortiguamiento (4)   |Total     |
|11| *nh* (final) |275      	|200	      |30	        |30              |535           |

Para seleccionar una muestra, vamos a usar AREA2 para seleccionar una muestra usando muestreo aleatorio estratificado: https://code.earthengine.google.com/?accept_repo=users%2Fopenmrv%2FMRV&scriptPath=projects%2FAREA2%2Fpublic%3A1.%20Sampling%20Design%2FStratified%20Random%20Sampling. 

Especifiquemos una ruta al mapa de Colombia basado en CODED (https://code.earthengine.google.com/?asset=users/olofsson76/Open_MRV/Open_MRV_Col_strat_buffer) con un amortiguamiento bajo "Specify stratification/image to define study area" (especificar estratificación/imagen para definir área de estudio); usemos los otros argumentos automáticos y hagamos clic en "Load image" lo cual visualizará áreas de estratos en la Consola (NOTA: esto tomará tiempo). Seleccione "Arbitrary sample size" (Tamaño de muestra arbitrario) bajo "Determine sample size", y en la opción "Allocate sample size to strata" (Asignar tamaño de muestra a estratos), especifique lo siguiente: 275, 200, 30, 30. Haga clic en "Create sample" (Crear muestra), y note que solo debe hacer clic una vez. Aunque parece que GEE no reacciona, esta dibujando la muestra después de su clic. 

Hacerle clic a "Add to map" (Agregar al mapa) visualizará las unidades de muestra como puntos rojos en el mapa. El paso final es exportar la muestra: haga clic en pestaña Tasks (Tareas), y luego exporte la muestra en el Dialog – dos entradas nombradas “sample_asset” y "sample_CSV" pueden aparecer en tareas. Estas son idénticas pero una es para exportar la muestra como un archivo CSV, una para guardar como asset de GEE Asset para uso en Google Earth Engine. Haga clic en el botón "Run" junto a las entradas y guárdelas como un asset de GEE y CSV (el ultimo se guardará en su Google Drive). Use el nombre “STR_sample_Col” para el asset de GEE y el archivo CSV.  

[image: STR_AREA2.png]


## 4. Muestreo aleatorios estratificado en R

El Banco Mundial ha implementado los scripts siguientes que permiten que un usuario seleccione una muestra bajo STR usando una estratificación en formato ráster. Los comentarios en el código están principalmente en francés pero las instrucciones para ejecutar los scripts se proveen próximamente aquí. 

El primer script calcula los pesos de estratos y esta disponible para descarga aquí: https://drive.google.com/file/d/1b5kZD_Eb73MwKvWPpGIqokyJpQJZ0rZ1/view?usp=sharing
Hay algunas cosas que debemos especificar antes de poder ejecutar el script. Si esta utilizando RStudio, tendrá que instalar los siguientes paquetes: rgdal, raster, and stringr.  Una vez que haya abierto el script en RStudio, necesitara definir el directorio de trabajo. Abajo, el directorio de trabajo es C:/Users/olofsson/Desktop/STR_example/ en un sistema operativo Windows. Cambie esto al directorio donde ocurrirá su estratificación. Note que debe usar una barra inclinada "/" (conocida como un forward slash en ingles) aun cuando esta especificando un directorio de Windows.

```R
#########DEFINIR ENTRADAS###############################################
#establecer directorio de trabajo. Usar / en lugar de \
wd <- "C:/Users/olofsson/Desktop/STR_example/"
setwd(wd)
```
Segundo, especifique el nombre de la estratificación en formato ráster, la resolución espacial de la estratificación, y el nombre del archivo CSV de salida:

```R
# leer el raster 
Raster <- raster('Col_strat_buffer_subset.tif')
 
##Resolucion de la imagen utilizada
Res <- 30
 
##Archivo con areas por estrato
Output <- "Col_Strat_buffer_subset_Wh.csv"
```
Esto resultará en los pesos de estratos con los que podemos comenzar el diseño de muestreo. (Note que hay muchas otras maneras de computar las áreas de estratos incluyendo el comando "GDALINFO -hist".)

Ahora podemos seleccionar la muestra usando el segundo script, el cual se puede acceder aquí: https://drive.google.com/file/d/1NbfEUBzwsAToxAkFFho2ltowb3Par8iE/view?usp=sharing

De nuevo, hay algunos argumentos en el código que debemos especificar. Primero debe crear un archivo CSV con dos columnas, una llamada "map_value" con el valor de cada estrato, y la otra llamada "final" con el numero del tamaño de muestras en cada estrato. Debe poner el archivo en un directorio de trabajo. Después, en la: 
Línea 12: establecer el directorio de trabajo
Línea 19: punto a archivo que contiene la estratificación 
Línea 22: especificar la resolución
Línea 26: punto a archivo CSV que contiene el tamaño de muestras
Línea 29: especificar el nombre del archivo CSV de salida para uso en Collect Earth
Línea 35: especificar el nombre del shapefile de salida que contiene la muestra

## 4 Preguntas Frecuentes

**¿Debo usar las aplicaciones mencionadas en este tutorial para seleccionar una muestra?**

¡No, en absoluto! Estos son solo algunos ejemplos y hay muchas otras formas de muestrear un área de estudio. Las aplicaciones comunes incluyen R, ENVI y ArcGIS.

**¿Tengo que seleccionar píxeles? ¿Qué pasa si quiero seleccionar segmentos o bloques de píxeles?**

La unidad espacial de la muestra no tiene que ser un píxel, pero debe tener el mismo tamaño para satisfacer los criterios del muestreo probabilístico. Los píxeles se utilizan como unidades en estos tutoriales en aras de la simplicidad. Para un análisis en profundidad de las unidades espaciales, consulte Stehman y Wickham (2011).

# Terminología relevante para las técnicas de muestreo 

Una lista de términos relevantes para las técnicas de muestreo e inferencia esta provista en la documentación de AREA2: https://area2.readthedocs.io/en/latest/definitions.html. Abajo hay algunos términos adicionales que no están incluidos en la documentación. 

#### Diseño de Respuesta

Definido por Stehman and Czaplewski, 1998[^fn1]: “La referencia o clasificación 'verdadera' se obtiene para cada unidad de muestreo en función de la interpretación de fotografías aéreas o videografías, una visita terrestre o una combinación de estas fuentes. Los métodos utilizados para determinar esta clasificación de referencia se denominan "diseño de respuesta". El diseño de respuesta incluye procedimientos para recopilar información relacionada con la determinación de la cobertura terrestre de referencia y reglas para asignar una o más [etiquetas] de referencia a cada unidad de muestreo ". Conocido como "plan de medición" por Särndal et al. (1992)[^fn2].

#### Muestra

Un subconjunto de unidades de población seleccionadas de la población.

#### Diseño de Muestra 

Sinónimo de diseño de muestreo, que es el término preferido en la literatura fundamental (Cochran, 1977 [^ fn3], Särndal et al., 1992 [^ fn2]). El término aparece en Rice (1995) [^ fn4] que utiliza tanto "diseño de muestreo" como "diseño de muestra".

#### Diseño de Muestreo

"El diseño de muestreo es el protocolo mediante el cual se seleccionan las unidades de muestra de referencia". (Stehman y Czaplewski, 1998) [^ fn1]. El “diseño de muestreo” también es utilizado por Cochran (1977) [^ fn3] y Särndal et al. (1992) [^ fn2]- el primero también usa "plan de muestreo".

#### Encuesta

Särndal y col. (1992) [^ fn2] define una encuesta como una “investigación parcial de una población finita”, y además que “los términos 'encuesta' y 'encuesta por muestreo' se utilizan para denotar investigaciones estadísticas con las siguientes características metodológicas: [. ..] plan de medición [...] de muestreo probabilístico [y] estimación."


#### Diseño de Encuesta

Un "diseño total de la encuesta" define los procedimientos para "obtener la posible precisión en las estimaciones de la encuesta mientras se logra un equilibrio entre los errores de muestreo y los no muestrales [...] El diseño de la encuesta da lugar a operaciones de encuesta" como la selección de la muestra (Särndal et al., 1992) [^ fn2]. Lohr (1999) [^ fn5] describe un diseño de encuesta total como "Una filosofía de diseño de encuesta para minimizar los errores de muestreo y de no muestreo". Además, en Lohr (1999) “diseño de encuestas” es sinónimo de diseño de muestreo.



## Referencias

[^fn1]: Särndal, C. E., Svensson, B. H., & Wretman, J. H. (1992). *Model assisted survey sampling*. New York, NY: Springer

[^fn1]: Stehman, S. V., & Czaplewski, R. L. (1998). Design and analysis for thematic map accuracy assessment: fundamental principles. *Remote Sensing of Environment*, 64(3), 331-344.

[^fn2]: Särndal, C. E., Svensson, B. H., & Wretman, J. H. (1992). *Model assisted survey sampling.* New York, NY: Springer.

[^fn3]: Cochran, W. G. (1977). *Sampling Techniques*. New York, NY: Wiley.

[^fn4]: Rice, J. A. (1995). *Mathematical Statistics and Data Analysis* (2nd ed.). Belmont, CA: Duxbury Press.

[^fn5]: Lohr, S. L. (1999). *Sampling: Design And Analysis.* CRC Press.



## Licencia

Este trabajo tiene licencia bajo un [Creative Commons Attribution 3.0 IGO](https://creativecommons.org/licenses/by/3.0/igo/) 

Copyright 2020, World Bank.

 Este trabajo fue desarrollado por Pontus Olofsson bajo contrato del World Bank con GRH Consulting, LLC para el desarrollo de recursos nuevos o existentes relacionadas a la Medida, Reportaje, y Verificación para el apoyo de implementación MRV en varios países. 

Material revisado por:
Ana Mirian Villalobos, El Salvador, Ministry of Environment and Natural Resources
Carole Andrianirina, Madagascar, National Coordination Bureau REDD+ (BNCCREDD)
Foster Mensah, Ghana, Center for Remote Sensing and Geographic Information Services (CERGIS)
Jennifer Juliana Escamilla Valdez, El Salvador, Ministry of Environment and Natural Resources
Paula Andrea Paz, Colombia, International Center for Tropical Agriculture (CIAT)
Phoebe Oduor, Kenya, Regional Centre For Mapping Of Resources For Development (RCMRD)
Rajesh Bahadur Thapa, Nepal, International Centre for Integrated Mountain Development (ICIMOD)
Tatiana Nana, Cameroon, REDD+ Technical Secretariat

Atribución: Olofsson, P. (2021). *Open MRV: Sample Selection*. World Bank. License: Creative Commons Attribution license (CC BY 3.0 IGO)

