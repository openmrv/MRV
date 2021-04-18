---
title: Cobertura Terrestre y Clasificación de Uso Terrestre en Google Earth Engine
summary: Este tutorial demostrará cómo realizar una clasificación de la cobertura y el uso del suelo en Google Earth Engine. Los usuarios aprenderán a aplicar métodos de clasificación supervisados y no supervisados, así como a manejar problemas de enmascaramiento y clasificaciones erróneas. El proceso se demuestra para los países de Colombia, Mozambique y Camboya. Los datos de muestra para la clasificación se basan en los tutoriales anteriores.
author: Robert E Kennedy
creation date:  diciembre 2020
language: Español
publisher and license: Copyright 2020, World Bank. Este trabajo tiene licencia bajo un Creative Commons Attribution 3.0 IGO

tags:
- OpenMRV
- Landsat
- Sentinel 2
- GEE
- Cobertura de nubes
- Sensores ópticos 
- Teledetección
- Imagen compuesta
- Mosaico
- Clasificación supervisada
- Clasificación no supervisada
- Mapeo de cobertura terrestre
- Mapeo de bosques
- Muestra
- Diseño de muestra 
- Diseño de muestreo 
- Selección de muestras
- Precisión
- Evaluación de precisión
- Sesgo
- Colombia
- Mozambique
- Camboya
- Random Forests
- Arbol de clasificación y regresión
- K-means

group:
- categoría: Imagen compuesta (Mediana)
  etapa: Creación de imagen compuesta/Pre-procesar
- categoría: Landsat
  etapa: Insumos
- categoría: Sentinel-2
  etapa: Insumos
- categoría: GEE
  etapa: Recopilación de datos de entrenamiento 
- categoría: Random Forest
  etapa: Clasificación

---

# Cobertura Terrestre y Clasificación de Uso Terrestre en Google Earth Engine

## 1 Contexto

### 1.1 Espacio de datos espectrales y clasificadores

Antes de comenzar un ejercicio de clasificación de imagen, es importante entender que es los que se está clasificando. 

Imágenes terrestres de detección remota responden a las propiedades físicas y químicas de la superficie. La reflectancia y absortancia variadas de la energía electromagnética se registra en diferentes bandas de un sensor, y los valores numéricos grabados en esas bandas definen un espacio espectral (o más generalmente, un espacio de datos de dimensión n). Todos los pixeles en una imagen están puestos en este espacio de datos por virtud de su reflectancia medida en cada banda espectral del sensor. 

![Schematic view of a 2-dimensional spectral data space defined by two spectral bands.  Each dot represents a single pixel in an image. The location in the 2-d space of each pixel is defined its reflectance values in the two bands.](./figures/m1.3/spectral_data_space.png){ width=50% }

La mayoría de algoritmos de clasificación operan enteramente en este espacio de datos. Clasificadores intentan separar este espacio en regiones con limites donde todos los pixeles pertenecen a una clase etiquetada. Algunos clasificadores consideran que los limites entre regiones son inflexibles, mientras que otros son menos rígidos y tratan con la membrecía de cada pixel en una clase como una probabilidad. 

![Classified spectral space. Each pixel from the prior figure has been labeled according to a classification scheme defined by the analyst.  In an ideal case such as that shown here, all of the pixels in each class can be grouped together into bounded regions.](C:\Users\vanes\Downloads\figures\m1.3\spectral_data_space_and_classes.png){ width=50% } 

Una vez que los límites de la clase hayan sido definidos en el espacio espectral, cualquier otro pixel en la imagen puede ser etiquetado de acuerdo al área en donde aterriza. 

![A pixel in the image with spectral values that place it at the location indicated by "Pixel D" lands within the bounds of Class 3, and thus would be labeled Class 3.](C:\Users\vanes\Downloads\figures\m1.3\spectral_space_classifier_new_pixel.png){ width=50% }


### 1.2 Cobertura Terrestre vs. Uso Terrestre 

Las propiedades físicas y químicas de la superficie están relacionadas a la cobertura terrestre. Cuando se están recopilando los datos de entrenamiento, entre más correspondan las definiciones de cobertura terrestre con las propiedades físicas de la superficie que controla el espacio de datos espectrales, más exitosa será la clasificación. 

"Uso terrestre"  se refiere a una definición humana superpuesta a la cobertura terrestre subyacente. El mismo terreno con cobertura herbácea puede tener varias designaciones diferentes de uso terrestre: césped en un área urbana puede definirse como "espacio abierto" o "parque", mientras que el mismo césped en un área agrícola puede considerarse "pastizal". Debe de haber cuidado durante el proceso de definición de las etiquetas de clasificación para estar alertos a las ambigüedades potenciales en las propiedades espectrales de las clases.   


### 1.3 Otros Recursos 

|               **Concept**o               |            Fuente            |                                                        Sitio |
| :--------------------------------------: | :--------------------------: | -----------------------------------------------------------: |
|    Conceptos Básicos de Teledetección    |   Natural Resources Canada   | https://www.nrcan.gc.ca/maps-tools-publications/satellite-imagery-air-photos/tutorial-fundamentals-remote-sensing/9309 |
| Conceptos Fundamentales de Teledetección | ARSET (NASA Applied Science) | https://appliedsciences.nasa.gov/join-mission/training/english/fundamentals-remote-sensing |


## 2 Objetivos de Aprendizaje 

Al final de este módulo, el usuario podrá:  

- Describir como espacio espectral o datos de espacio son usados en clasificación multivariante 
- Aplicar y comparar 3 algoritmos comunes de clasificación 
- Evaluar posible fuentes de error en el proceso de clasificación que surgen del pre-procesamiento, el sensor elegido, y el diseño de muestras de entrenamiento  


## 2.1 Prerrequisitos para este módulo

* Conceptos de Google Earth Engine (GEE) 
  * Conseguir una cuenta de usuario 
  * Manejo de imágenes en GEE
  * La sintaxis básica de funciones 
  * Procesamiento básico de imágenes en GEE, incluyendo selección de imágenes, filtrando nubes, creando mosaicos e imágenes compuestas 

> NOTA: Estos temas se explican en el Módulo 1.1: Creación de Imagen Compuesta/Mosaico de Landsat y Sentinel-2 en Google Earth Engine


* Conceptos básicos de teledetección 
  * El espectro electromagnético
  * Reflectancia espectral 
  * Registro de la reflectancia en las bandas


## 3 Clasificación Supervisada en Google Earth Engine

### 3.1 Descripción general del flujo de trabajo

Clasificación supervisada se refiere al proceso de usar un conjunto de datos de entrenamiento con etiquetas conocidas para guiar un clasificador matemático en la tarea de etiquetar el espacio espectral. La característica clave es que el conjunto de datos de entrenamiento guían (o "supervisan") la etiquetación. 

Aunque los pasos específicos varían en base al clasificador, el [flujo de trabajo de clasificacion supervisada en GEE](https://developers.google.com/earth-engine/guides/classification) es similar en todos los variantes. 

- Conseguir una imagen
- Conseguir datos de entrenamiento
- Entrenar un clasificador o un "clusterer"
- Aplicar ese clasificador a la imagen 

Próximamente, los pasos se muestran de manera visual. 

![Workflow of classification](C:\Users\vanes\Downloads\figures\m1.3\WB_graphs_v2-03.png)

Esto crea un mapa. Luego necesitará evaluar la precisión del mapa. Este tema se desarrolla en un módulo siguiente acerca de la evaluación de precisión.

Haremos un ejemplo simple con los componentes siguientes, y luego ilustraremos otras variaciones. Estas instrucciones suponen que el usuario ya tiene cuenta de GEE, y que ya tiene familiarización con la configuración, los formatos de datos, y las funciones en GEE. Si necesita volver a repasar estos pasos, por favor regrese al Módulo 1.1. 


**Classification component**|**Item used here**|**Process on OpenMRV**|**Tool on OpenMRV**
:-----:|:-----:|:-----:|:-----:|
Image|Landsat 8 composite from a single year|Pre-processing|GEE
Training data|Point data|Training data collection|GEE
Classifier|CART|Classification (current tutorial)|GEE (current tutorial)

#### 3.1.1 Preparación:  Cargar el script

GEE trabaja con scripts. Como se notó arriba, asumimos que está familiarizado con el interfaz de GEE and trabajando con scripts. Todo el código en este tutorial esta capturado en un script. Dependiendo de su nivel de interés, simplemente puede ejecutar el código usted mismo, o puede extraer los fragmentos de código a un script separado. Un tutorial breve acerca de este paso esta disponible en este enlace:  https://youtu.be/jaz-tcwmNLQ

1. Ingrese a su editor de código Javascript de GEE en [code.earthengine.google.com](code.earthengine.google.com)
2. *Opcional* Prepare repositorio nuevo para su trabajo

![This is how you do it](C:\Users\vanes\Downloads\figures\m1.3\GEE_new_repo.png)

3. Si tiene acceso de "reader" en el grupo de openMRV, verá el script en "users/openmrv/MRV/LCLUC/cls_landsat_v2_colombia".  O puede navegar al script directamente usando este enlace al [GEE script](https://code.earthengine.google.com/549b29a5d53880813d9b8f07b839bbb5).
   1. Nos referiremos a este código como el Script Maestro, ya que ejecuta todos los pasos en este tutorial.
4. Guárdelo a su carpeta preferida. Puede usar el video mencionado previamente como guía. 

> Pista: Necesitará hacer una alteración al archivo para guardarlo bajo un nombre local. Agregue un espacio en alguna parte del script, y use la función "Save As".

![The Save As Function](C:\Users\vanes\Downloads\figures\m1.3\GEE_save_as.png)


## 3.2 Construir Imagen Compuesta

El primer fragmento de código se basa en el módulo anterior acerca de los métodos de crear imágenes compuestas. Construimos una colección de imágenes de Landsat 8 surface reflectance (reflectancia de superficie) del 2019, la filtramos basado en la cobertura de nubes, aplicamos un valor mediano, y redujimos todo a los limites de nuestro país de interés. 

> Nota:  Los detalles del proceso de crear imágenes compuestas se encuentran en el módulo 1.1. Si quiere más repaso, considere regresar a ese módulo. 

Si está copiando y pegando fragmentos de código desde el Script Maestro a un script nuevo, esta sección está etiquetada como Sección 3.2 en el Script Maestro. 

En lugar de replicar un script entero aquí, vamos a resaltar el fragmento central del código. El código siguiente del Módulo 1.1 le será familiar.

```javascript 
var l8compositeMasked = l8.filterBounds(country)
                .filterDate(startDate,endDate)
                .filterMetadata('CLOUD_COVER','less_than',50)
                .map(maskL8srClouds)
                .median()
                .clip(country);
```

Cuando ejecute este código, GEE lentamente construirá una imagen en la ventana de mapa. 

Abajo hay una imagen de una área pequeña de Colombia, en la región alrededor de Medellín. La combinación de colores usa las bandas de Infrarrojo de Onda Corta, Infrarrojo Cercano, y Rojo en las pestañas desplegables de Rojo, Verde, Azul en el monitor. Bosque aparece verde, y áreas desarrolladas aparecen de color magenta.  

Note que hay áreas grises para las cuales no se encontraron pixeles válidos -- estas son áreas de nubes persistentes.

![Image of landsat composite](C:\Users\vanes\Downloads\figures\m1.3\landsat8_composite.png)


## 3.3 Cargar datos de entrenamiento

Los datos de entrenamiento son las observaciones que usaremos para construir la clasificación. Como se mencionó previamente, las definiciones de las etiquetas de clase de estos datos deben ser definidas con consideración de las propiedades espectrales de la superficie. 

Si está copiando y pegando el código, agregue "Sección 3.3" en el Script Maestro al código en su script de entrenamiento existente. Para este primer ejemplo acerca de como agregar a un script existente, consulte este [video breve]( https://youtu.be/r2jJrSYgtA8 ).

Para este ejercicio, usaremos datos de entrenamiento recopilados con los métodos descritos en los módulos acerca de la colección de datos de referencia (módulo 1.2).  Como se había mencionado antes, en lugar de replicar todo el código aquí, nos enfocaremos en solo una parte central del código: 

```javascript
var training = ee.FeatureCollection(
'users/openmrv/MRV/colombia_training');
```

>Terminología:  En GEE, conjuntos de datos como estos puntos de entrenamiento se definen como un "FeatureCollection".  Para usuarios familiares con los conceptos de shapefiles u otras representaciones vectoriales similares de datos geoespaciales, ambos son prácticamente la misma cosa. En GEE, datos vectoriales tienen una "geometría", la cual contiene la posición geográfica de los puntos, las líneas, y los polígonos de un objeto vectorial, además de los atributos que registran la información acerca de esas geometrías. Juntos, estos forman un "Feature" (objeto) singular, como un punto o un polígono. Varios de estos "features" juntos son considerados un "FeatureCollection".  


Para dar referencia, definimos los códigos de clase y las etiquetas antes del módulo previo de la manera siguiente: 

| **Código de Clase** | **Etiqueta de Clase** |
| :-------------: | :---------------: |
|        1        |      Bosque       |
|        2        |       Agua        |
|        3        |     Herbáceo      |
|        4        |   Desarrollado    |

Otra pieza de código importante que se introduce aquí define los colores de las clases, ya que estos se usarán mas tarde durante la visualización del mapa:

```javascript 
var palette_landcover = ee.List([
  '25CF1C', // forest
  '2E3FAC', // water
  'EFF215',  // herbaceous
  'FE9D02' // Developed
]);
```

Los colores están en forma de código hexadecimal, el método estándar para definir códigos de color en monitores. Consulte cualquier sitio de web relacionado a códigos de HTML (por ejemplo, https://htmlcolorcodes.com) para seleccionar sus colores preferidos. 

> **Uso avanzado:**  Para interpretación posterior, es útil definir un color para cada clase. Mire el código para ver un método para asignarle un color a cada punto interpretado de acuerdo al esquema de color definido usando códigos hexadecimales.

![The training points from Module 1.2.1 displayed in the code editor of GEE.](C:\Users\vanes\Downloads\figures\m1.3\training_points_colombia.png){ width=50% }


### 3.4 Asociar puntos de entrenamiento con valores espectrales 

Ahora, los valores espectrales serán extraídos a las ubicaciones asociadas con los puntos de entrenamiento. Primero, las bandas espectrales de la imagen deben ser definidas, y luego la operación `.sampleRegions` se le aplica a la imagen.

Si está agregando a su propio script, copie y pegue la sección 3.4 del Script Maestro. 

De nuevo, solo nos enfocaremos en los pasos claves del código. Interpretaremos cada fragmento siguiente en la sección "Analizando el código". 

```javascript
// Para clasificación, usaremos las bandas visibles, infrarrojo cerano, e infrarrojo de onda corta 

var bands_to_use = ['B2', 'B3', 'B4', 'B5', 'B6', 'B7']


// Ahora vamos a hacer una superposición espacial de los puntos en la imagen, y extraer

var landcover_labels = 'landcover'

var training_extract = l8compositeMasked.select(bands_to_use).sampleRegions({
  collection: training_points, 
  properties: [landcover_labels],
  scale: 30
});
```

***Analizando el código:***  

```javascript
	var bands_to_use = ['B2', 'B3', 'B4', 'B5', 'B6', 'B7']
```

Los nombres de las bandas se pueden encontrar en la descripción de la fuente original de la imagen, la cual es Landsat 8 en este caso. Note que los nombres están especificados como una lista de valores de cadena. 


```javascript
var landcover_labels = 'landcover'
```

Esto especifica cual atributo en el FeatureCollection tiene los valores etiquetados.  Como se mencionó en el Módulo 1.2, esta etiqueta debe de ser un código numérico. 


```javascript
var training_extract = l8compositeMasked.select(bands_to_use).sampleRegions({
  collection: training_points, 
  properties: [landcover_labels],
  scale: 30
});
```

La función de `.sampleRegions` requiere información acerca de la colección de objetos que se usará, el atributo (o propiedad) que se extraerá, y la escala de pixel (en metros). 

Al final de este paso, el FeatureCollection `training_extract` contendrá los valores espectrales de `bands_to_use` y las etiquetas de los puntos de entrenamiento. 

Para confirmar que el objeto tiene estas propiedades, puede usar el comando `print(training_extract)` para ver las propiedades del objeto en la consola. Este es un ejemplo:  

![An example of attributes listed in the Console of GEE for a feature collection containing the extracted values from the training points](C:\Users\vanes\Downloads\figures\m1.3\feature_collection_with_loandcover_and_bands.png){ width=50% }

El FeatureCollection tiene la misma cantidad de objetos que los datos de entrenamiento originales, pero note que cada objeto ahora tiene atributos para las bandas espectrales que especificó usando la variable `bands_to_use`.  

También tome en cuenta que ahora este FeatureCollection se puede usar con cualquier clasificador de GEE.


### 3.5 Construir un clasificador a CART 

A continuación, usaremos un clasificador CART para encontrar el mejor método que aplique los valores espectrales para separar las etiquetas. Los clasificadores conocidos como Classification and Regression Trees ('Árboles de Clasificación y Regresión', o CART por sus siglas en ingles) dividen el espacio de datos espectrales en sucesivas divisiones binarias en forma de árbol. 

Árboles de clasificación identifican líneas que sucesivamente dividen el espacio de datos para separar los puntos de entrenamiento en sus clases respectivas. 

![An example of a classification tree approach to classification. The classifier identifies a value on one of the two axes that best separates the classes, with successive splits further isolating training points into classes.](C:\Users\vanes\Downloads\figures\m1.3\CART_classification_cartoon.png){ width=50% }

Si está agregando a su propio script, copie y pegue la sección 3.5 del Script Maestro. 

El pedazo central de código para un clasificador CART en GEE es este comando simple: 

```javascript
var trained_CART = ee.Classifier.smileCart()
  .train(training_extract, landcover_labels, bands_to_use);
```

La variable `trained_CART` es un clasificador que ahora se puede aplicar de nuevo a la imagen a la que se le aplicó la función de `.sampleRegion` (ver próxima sección). Esencialmente, el clasificador es una encapsulación de reglas matemáticas que conectan las bandas espectrales a las etiquetas.

Las características básicas del objeto se pueden confirmar mirando el objeto usando la función `print()` en GEE: 

![The view of the classified object as viewed in the Console of GEE](C:\Users\vanes\Downloads\figures\m1.3\classifier_console.png){ width=50% }

### 3.6 Aplicar el clasificador a la imagen

Una vez que se haya construido un clasificador, la aplicación de reglas matemáticas a la imagen original resulta en un mapa etiquetado. Cada pixel en la imagen espectral es evaluado contra reglas matemáticas en el clasificador, y una etiqueta se le asigna en base a esas reglas.   

La aplicación del clasificador en GEE es una sola línea de código para crear la imagen clasificada, y otra línea para agregarla al mapa:  


```javascript
var classified_CART = l8compositeMasked.select(bands_to_use).classify(trained_CART);

Map.addLayer(classified_CART, {min:1, max:4, 
  palette:['25CF1C', // bosque
  '2E3FAC', // agua
  'EFF215',  // herbáceo
  'FE9D02']}, // desarrollado
 
  'CART Classification'
)
```

***Analizando el código***

```javascript
var classified_CART = l8compositeMasked.select(bands_to_use).classify(trained_CART);
```

Este paso aplica el objeto de clasificador a la imagen -- tomando en cuenta que la imagen debe ser igual a la que se usó para crear el objeto `trained_CART`.  

El resultado de este proceso es una imagen. Abajo, agregamos la imagen al mapa, y especificamos la visualización de color para las clases.


```javascript
Map.addLayer(classified_CART, {min:1, max:4, 
  palette:['25CF1C', // bosque
  '2E3FAC', // agua
  'EFF215',  // herbáceo
  'FE9D02']}, // desarrollado
 
  'CART Classification'
)
```

Consejo:  Hay que llevar cuenta de los números de código de color para saber en que orden aplicar los colores. 

Ya aplicados al país de Colombia, el mapa aparece de la siguiente manera:

![Image of classified map for all of Colombia](C:\Users\vanes\Downloads\figures\m1.3\CART_classification_countrywide.png){ width=50% }

Vale la pena reiterar que los puntos de entrenamiento que se usaron para construir este mapa no se hicieron para crear mapas de alta calidad. Dado esto, el mapa creado aquí es simplemente un ejercicio, no hecho con la intención de servir como un mapa real de cobertura terrestre en Colombia. Sin embargo, lo usaremos para enseñar los pasos para evaluarlo y mejorarlo. 

### 3.7 Evaluando y mejorando mapas  

La precisión del mapa será evaluada usando una muestra basada en diseño con un proceso descrito en módulos posteriores. Sin embargo, frecuentemente vale la pena evaluar un mapa visualmente para encontrar errores graves y mejorar el mapa de forma iterativa antes de tomar el tiempo para crear una muestra de precisión robusta. [Proveemos un video breve para que comience]( https://youtu.be/A7TEZMi_0cc ) a evaluar resultados de la clasificación. 

Varios problemas son evidentes en el mapa CART mostrado aquí: 

![Examples of classification problems, including missing pixels and over-prediction of developed areas.](C:\Users\vanes\Downloads\figures\m1.3\classification_problems.png)

1. Pixeles ausentes, causado por nubes

   Como se mencionó arriba, la imagen compuesta para esta región en el 2019 tenia un área considerable donde la máscara de nubes resulto en pocos pixeles válidos para la imagen compuesta. Estas áreas no pueden ser clasificadas, ya que no tienen valores espectrales en los cuales se pueda aplicar el clasificador. 

2. Áreas geográficas grandes clasificadas como "Desarrollado"

   En el norte del país en la Península Guajira, toda el área esta clasificada como "desarrollado", cuando en realidad el área es muy seca y poco vegetada, y con muy poco desarrollo urbano

3. Áreas substanciales de la clase "desarrollado" intercaladas con praderas

   En los planos en el noreste del país, la clasificación herbácea esta intercalada con la clase de "desarrollado"

#### 3.7.1 Opciones para problemas con la máscara de nubes

Cuando se trabaja con datos ópticos pasivos, la abundancia de nubes es un problema común en muchas partes del mundo. A continuación, discutimos varias opciones para mejorar la disponibilidad de imágenes. 

##### 3.7.1.1 Ajustar umbrales para filtrar imágenes nubladas 

En nuestros ejemplos hasta ahora, hemos filtrado imágenes individuales de Landsat donde mas del 50% del terreno está bajo nube, de acuerdo a los metadatos. Esta filtración ocurre en el paso de creación de imágenes compuestas:  `.filterMetadata('CLOUD_COVER', 'less_than', 50)`.  Esto filtra adquisiciones enteras de imágenes de Landsat, aun cuando algunos de esos pixeles podrían ser útiles.

Frecuentemente se recomienda ser conservativo con la filtración de nubes, pero cuando lleva a vacios considerables en las imágenes como observamos en el mapa de Colombia, vale la pena omitir el filtro a la escala de imágenes enteras, y mejor depender en filtración por-pixel capturado en la función  `.map(maskL8srClouds)`. 

Para el propósito de un ejemplo, el flujo de trabajo entero es recreado en el script  `cls_landsat_v1` en la sección etiquetada 3.7.  

Si está copiando y pegando el código, quizás quiera comenzar un script nuevo aquí con la Sección 3.7, ya que estos pasos se pueden ejecutar independientemente. 

En la primera porción de la Sección 3.7 (y a través de 3.7.1.1 en el Script Maestro), simplemente volvemos a ejecutar la misma clasificación pero cambiando la máscara de nubes. 

- La omisión del filtro de metadatos de 50% cobertura de nubes resulta en el mapa siguiente: 


![Image of classification without 50% cloud cover threshold](C:\Users\vanes\Downloads\figures\m1.3\CART_image_after_removing_image_cloud_filter.png){ width=50% }


Esto mejoró la situación sustancialmente, pero no la resuelve completamente.

#### 3.7.1.2 Expandir el mosaico para incluir mas años de datos 

Mapas de cobertura terrestre están asociados con el año en el cual las imágenes fueron adquiridas. En los ejemplos hasta ahora, nos hemos enfocado en imágenes del año 2019. Puntos de entrenamiento también fueron adquiridos en el año 2019 para este ejercicio. 

A pesar de que limitar las imágenes y los datos de entrenamiento a un año singular es loable, mapas con valores ausentes son problemáticos. Dependiendo del objetivo del mapa, una opción para mejorar la cobertura del mapa es expandir la cantidad de años disponible para crear la imagen compuesta.

En nuestro script de GEE de ejemplo, `cls_landsat_v2_colombia`, hemos proveído un ejemplo de como años de imágenes adicionales pueden fusionarse a una colección de imágenes antes de crear el mosaico. El método de fuerza bruta es simplemente construir dos colecciones de imágenes y luego usar el método GEE  `.merge()` para combinarlas.  

Si está copiando y pegando a su propio script, agregue la sección 3.7.1.2 a su script ahora. 

Las piezas claves están aquí: 


```javascript
// Crear imagen compuesta del 2019.  
// Notar que usamos la coleccion "l8" ya identificada
// en la cima de este script.

var startDate = '2019-01-01';
var endDate = '2019-12-31';

var l8compositeMasked2019 = l8.filterBounds(country)
                .filterDate(startDate,endDate)
                .map(maskL8srClouds);

// Ahora agregar 2018

var startDate = '2018-01-01';
var endDate = '2018-12-31';

var l8compositeMasked2018 = l8.filterBounds(country)
                .filterDate(startDate,endDate)
                .map(maskL8srClouds);
          
// Ahora combinar y conseguir valor mediano con median()

var two_year_composite = l8compositeMasked2019
                .merge(l8compositeMasked2018)
                .median()
                .clip(country);
```

***Analizando el código***

En este código, primero estamos creando la imagen compuesta para el 2019 usando el mismo código que usamos antes.

```javascript
var l8compositeMasked2019 = l8.filterBounds(country)
                .filterDate(startDate,endDate)
                .map(maskL8srClouds);

```

Repetimos este proceso para el 2018. 

El nuevo paso clave es la combinación de ambas imágenes compuestas: 

```javascript
var two_year_composite = l8compositeMasked2019
                .merge(l8compositeMasked2018)
                .median()
                .clip(country);
```

La fusión de los conjuntos de datos comienza con un conjunto de datos (aquí,`l8compositeMasked2019`) y luego usa la función  `.merge` para agregar el segundo conjunto de datos.

La imagen resultante tiene menos vacios. 

![Image showing two-year composite](C:\Users\vanes\Downloads\figures\m1.3\comparing_two_year_composite.png)

Aun hay vacios cerca de las costas y en elevaciones altas. Puede que sea necesario agregar un tercer año, o considerar un método para traer otras fuentes de imágenes. 

#### 3.7.1.3 Ejecutar CART usando imagen compuesta de dos años

Para ejecutar el CART con estos datos nuevos, debemos volver a extraer los valores espectrales, y reconstruir el clasificador.  

Si está copiando y pegando código, use Sección 3.7.1.3 del Script Maestro. 

Los fragmentos de código son idénticos, pero usamos nuevos nombres de variables para asegurar que no editemos o borremos nuestros datos por accidente. Dado esto, usamos el `two_year_composite` como entrada en la extracción de datos, y le asignamos una variable de entrenamiento nueva `training_extract_v3`.  

```javascript
var training_extract_v3 = two_year_composite.select(bands_to_use).sampleRegions({
  collection: training_points, 
  properties: [landcover_labels],
  scale: 30
});
```

Actualizaciones similares ocurren cuando se construye y se aplica el clasificador -- no replicamos el código aquí para mantener la sección breve, pero referimos al usuario al Script Maestro en esta sección.

Usando la imagen compuesta de dos años y volviendo a ejecutar el clasificador CART, el patrón espacial de clases demuestra menos artefactos de imagen. 

![Classification with two-year composite](C:\Users\vanes\Downloads\figures\m1.3\cart_classifier_with_two_year_composite.png){ width=50% }


#### 3.7.2 Manejando errores de clasificación 

Como se notó previamente, la evaluación visual de la clasificación de CART original reveló áreas donde la clase "Desarrollado" fue etiquetada inapropiadamente. Después de agregar un segundo año a nuestra imagen compuesta, el problema continua: la inspección visual confirma que se le esta asignando la clase "desarrollado" a pixeles que pertenecen en "herbáceo" o tierra estéril. A pesar de que las muestras de entrenamiento no están destinadas para mapeo robusto, podemos usar este ejemplo de clasificación errónea para ilustrar como se puede manejar el problema.


![The false-color image (C:\Users\vanes\Downloads\figures\m1.3\figure_zoom_of_guajira.png) on the left shows areas of sparse herbaceous vegetation with substantial soil or sand visible as well. These bright areas occupy a similar portion of the spectral space as the developed class, resulting in a classification with an abundance of labels of developed.](./figures/m1.3/figure_zoom_of_guajira.png)

Similarmente, una evaluación cercana de las llanuras en el este y noreste del país cerca del Río Meta demuestra una clasificación exagerada de área "desarrollada", aparentemente causada por áreas con poca vegetación. 

![Overclassification of the "developed" class near the Meta River in Northeastern Colombia. Colors and interpretation as in prior figure](C:\Users\vanes\Downloads\figures\m1.3\figure_overclass_developed_plains.png)

#### 3.7.2.1. Opciones para manejar errores de clasificación errónea 

Para entender como arreglar la clasificación errónea, uno debe de tener una comprensión de la causa: La clasificación errónea ocurre cuando un pixel de una clase cae en el espacio de datos espectrales que el clasificador le ha asignado a otra clase. 

Usando esta ilustración simple mostrada previamente para el clasificador CART, podemos imaginar al menos dos casos donde esto pueda ocurrir. 

Caso 1:  Un pixel nuevo cae en la parte de espacio espectral que ya esta ocupado por miembros de una clase diferente. Esta situación puede ocurrir cuando las dos clases no tienen suficientes diferencias espectrales para ser distinguidas, o cuando la densidad de puntos de entrenamiento es tan dispersa que estos lóbulos diferentes de espacio espectral no están lo suficientemente delimitados. 

Caso 2: Un pixel nuevo se encuentra en una región de espacio espectral que no tiene muestras de entrenamiento, pero al que se le debe asignar una etiqueta a causa de las divisiones identificadas por las muestras que sí existían. 

![Two cases of misclassification. In Case 1, a new pixel (C:\Users\vanes\Downloads\figures\m1.3\misclassification.png) that should be labeled with the Orange class lands in the midst of representatives of the green class. In Case 2, a new pixel of the Orange class lands outside the domain of classes already defined, but because it is on the "Green side" of the first split, it gets labeled as green.](./figures/m1.3/misclassification.png){ width=50% }

Al menos tres remedios existen para el Caso 1: 

- Proveer mas dimensionalidad al espacio de datos espectrales. Puntos que no pueden ser separados por un plano 2-D tal vez se puedan separar a lo largo de un tercer eje, por ejemplo. Esto requiere agregar información espectral al principio del proceso de clasificación.  La oportunidad de éxito mejora si la nueva dimensión de datos captura alguna característica que un experto pueda identificar como algo que separe las clases confundidas. Por ejemplo, agregando un componente que captura la estacionalidad puede separar a dos tipos de bosques que se distingan por la condición de sus hojas y su temporalidad.  

- Obtener más puntos de entrenamiento en las condiciones que están causando la confusión. Agregando más puntos en las partas del espacio espectral donde ocurre la confusión ayuda a que el clasificador tenga mejor oportunidad de separar los puntos a las clases apropiadas. 

- Aplicar un clasificador mas flexible al mismo conjunto de datos. CART es un clasificador relativamente sencillo. Es posible que un clasificador mas avanzado pueda obtener mejores resultados con los mismos datos. Vea la Sección 3.8 para ver un ejemplo.

Caso 2 es un ejemplo clásico de extender el modelo estadístico fuera de los límites para los cuales se construyo. El mejor remedio para este caso es obtener mas puntos de entrenamiento en la región donde ocurre la confusión, con la meta de entender el dominio del entrenamiento. 


### 3.8 Aplicando un clasificador supervisado diferente: Random Forests

El algoritmo Random Forests (Breiman 2001:  "Random Forests". Machine Learning. 45 (1): 5–32) usa el mismo concept de árboles de decisiones, pero agrega estrategias para hacerlos mas poderosos. Aunque una explicación detallada de Random Forests (RF) está mas allá de la meta de este entrenamiento, una breve introducción se presenta aquí. 

El algoritmo RF genera muchos árboles de decisión (muchos "árboles " forman un "bosque"), cada uno con aleatorizaciones un poco diferentes en los datos de entrenamiento y los datos de predicción (en este caso, los datos espectrales). Cada división en un árbol de decisión se hace con un subconjunto de los datos de entrenamiento y los valores espectrales. Esto mejora la robustez hacia puntos de entrenamiento o variables  atípicos. Cuando se construyen y se aplican estos árboles de decisiones a la imagen, cada pixel recibe una etiqueta de cada uno de los árboles , y la etiqueta final es considerada la que ocurre en la mayoría de árboles para ese pixel. 

Dado que la extracción de los datos de entrenamiento es igual para todos los clasificadores en GEE, solo necesitamos construir el clasificador nuevo de los datos de entrenamiento previo, y luego aplicar eso a la imagen. Usaremos la imagen compuesta de dos años de la Sección 3.7. 

Si esta copiando código del Script Maestro, agregue la Sección 3.8 a su script. Ya que estamos usando la imagen compuesta de dos años de la Sección 3.7, asegúrese de que esta agregando a un script que incluye las imágenes compuestas de esa sección.

Primero, construimos el clasificador (note que `training_extract_v3` se definió previamente en el script como una extracción de la imagen compuesta de dos años) : 

```javascript
var trained_RF = ee.Classifier.smileRandomForest(250)
  .train(training_extract_v3, landcover_labels, bands_to_use);
```

El algoritmo `smileRandomForest` acepta el número de árboles construidos como argumento -- aquí escogimos 250. A pesar de que el número de árboles varía en cada situación, la experiencia sugiere que al menos 250 árboles son un buen objetivo. 

Luego, aplicamos el clasificador a la imagen de dos años: 

```javascript
var classified_RF = two_year_composite.select(bands_to_use).classify(trained_RF);

Map.addLayer(classified_RF, {min:1, max:4, 
  palette:['25CF1C', // bosque
  '2E3FAC', // agua
  'EFF215',  // herbáceo
  'FE9D02']}, // desarrollado
 
  'RF Classification'
)
```

Una inspección de algunas de las áreas notadas arriba sugiere que el algoritmo RF pueda ser más robusto hacia los problemas de clasificación errónea, pero que aun existen.

![The result of the random forests classifier applied to the two-year composite for the same area shown above.  Note the substantial reduction in areas classified as developed.](C:\Users\vanes\Downloads\figures\m1.3\randomforests_classifier.png)

El área en la Península Guajira en su mayoría aun sigue clasificada de manera errónea. Esto sugiere que los datos de entrenamiento no muestrean el espacio espectral de esta clase adecuadamente, y que más datos de entrenamiento en esta región serían beneficiosos. 

![The Random Forests classification of the Guajira peninsula, showing that the developed class remains overpredicted.](C:\Users\vanes\Downloads\figures\m1.3\guajira_rf.png)


## 4 Clasificación No Supervisada

Un desafío clave de la clasificación supervisada es definir clases que puedan ser adecuadamente separadas en el espacio espectral de las imágenes. Si las definiciones de las clases no necesitan estar estrictamente definidas con anticipación, es posible permitir que las imágenes encuentren agrupamientos en el espacio espectral, y luego intentar asignarles a estos grupos una etiqueta descriptiva. Ya que datos de entrenamiento etiquetados no se usan para guiar este proceso, se le refiere a este proceso como una clasificación no supervisada. 

### 4.1 El algoritmo *k*-means 

Algoritmos de agrupamiento son númerosos. El lector interesado puede consultar https://en.wikipedia.org/wiki/Cluster_analysis u otras introducciones genéricas. En teledetección, un método común es el agrupador (clusterer) *k*-means, implementado en GEE como la función `ee.Clusterer.wekaKMeans`.  

El método *k*-means utiliza una estrategia de reagrupación iterativa para identificar grupos de píxeles cercanos entre sí en el espacio espectral. El usuario proporciona el número deseado (*k*) de clusters, y el algoritmo distribuye ese número de puntos semilla al espacio espectral. Estas ubicaciones semilla son consideradas puntos de partida de las clases eventuales. La ubicación de estos puntos semilla se predetermina a una ubicación aleatoria en la implementación GEE del algoritmo. Una muestra grande de pixeles en la imagen es asignada a su punto semilla más cercano, y el valor espectral medio de esos pixeles es calculado. Ese valor medio es similar al centro de una masa de puntos, y se le conoce como el centroide. A menos que los puntos que estaban más cerca de un punto semilla estuvieran dispuestos simétricamente alrededor de él, este centroide calculado se moverá ligeramente desde donde comenzó. Todos los píxeles de la imagen ahora se vuelven a adjuntar a los centroides -- a menudo, algunos píxeles cambian de centroide debido al movimiento de los centroides. Cuando el nuevo grupo de píxeles se usa para la calculación del centroide, el nuevo centroide se moverá nuevamente. El proceso se repite hasta que los centroides permanecen relativamente estables y pocos píxeles cambian de una clase a otra en las iteraciones posteriores.

## 4.2 Aplicación de *k*-means en GEE

La aplicación en GEE sigue generalmente el mismo flujo de trabajo que el que se utilizó para la clasificación supervisada, excepto que las muestras de entrenamiento se generan al azar en lugar de tomarse de un conjunto de entrenamiento interpretado. Estos no son datos estrictamente de "entrenamiento", ya que no tienen etiquetas. Más bien, son simplemente una submuestra aleatoria del espacio de datos espectrales.

El código para la implementación esta en la Sección 4.0 del Script Maestro. Tomar en cuenta que este código depende de la imagen compuesta `two_year_composite` de la Sección 3.7, así que asegúrese que su script la incluya si esta copiando y pegando el código. 

Primero, las ubicaciones aleatorias son elegidas.

```javascript
var randomtraining = two_year_composite.sample({
    region: country,
    scale: 30,
    numPixels: 500,
    tileScale: 10
  });
```

Luego, el algoritmo *k*-means es aplicado a los puntos elegidos. 

```javascript
var numberOfClasses =10
var clusterer = ee.Clusterer.wekaKMeans(numberOfClasses).train(randomtraining);
```


Finalmente, el clusterer es aplicado a la imagen. 

```javascript
var unsup = two_year_composite.cluster(clusterer);
Map.addLayer(unsup.randomVisualizer(), {}, '10 Clusters')
```

Tenga en cuenta que los colores de las clases no están relacionados con una cantidad significativa, por lo que se utiliza un visualizador aleatorio. Los colores de las clases no son significativos, simplemente se utilizan para distinguir las clases.

![A classified output from the *k*-means unsupervised classification algorithm.  Note that the colors are randomly assigned, and thus have no inherent meaning.](C:\Users\vanes\Downloads\figures\m1.3\figure_kmeans_examples.png)

### 4.3 Evaluación

Una vez creada la imagen agrupada, un usuario experto puede evaluar si las opciones utilizadas son efectivas y puede comenzar a asignar etiquetas de cobertura terrestre a los grupos. Esta es necesariamente una estrategia más subjetiva que requiere la comprensión tanto del paisaje como del espacio de datos espectrales.

El primer criterio de evaluación es simplemente si el patrón espacial de los grupos (clusters) sigue los patrones espaciales de interés en las imágenes. Si hay muy pocos grupos, los límites entre zonas distintas en el paisaje estarán abarcadas por un solo grupo. A la inversa, si hay demasiados grupos, las zonas visualmente homogéneas se dividirán. 

El segundo criterio es si a los conglomerados se les pueden asignar etiquetas que sean consistentes con el conocimiento del paisaje de un experto.

Los remedios para demasiadas o muy pocas clases son simplemente ejecutar la clasificación nuevamente, o tomar pasos más avanzados de dividir la imagen en clases de componentes y volver a ejecutar el clasificador en el subconjunto.

### 4.4 Ventajas y desventajas

La clasificación supervisada supone qué clases son interesantes o relevantes, pero rara vez esas etiquetas de clase se construyen de acuerdo con lo bien que se capturarán en el espacio de datos espectrales. Por lo tanto, el enfoque supervisado puede intentar hacer que un espacio de datos espectrales separe clases que no sean separables.

La clasificación sin supervisión depende completamente de las imágenes y de la separabilidad de las clases. Por lo tanto, puede representar mejor patrones en el paisaje. Pero el etiquetado de esas clases puede no ser útil para el usuario. Además, el método depende completamente del espacio de datos y, por lo tanto, una repetición de los mismos pasos básicos en un conjunto diferente de imágenes para la misma ubicación podría conducir a un mapa diferente.

# 5 Aplicación a otros países de ejemplo

Aunque trabajar con scripts en GEE exige más de un usuario que una simple interfaz gráfica de usuario, es en la aplicación a nuevas situaciones donde se hace evidente el poder de la plataforma.

Suponiendo que tiene datos de entrenamiento para su nueva situación, pasar a una nueva situación puede ser tan simple como cambiar algunas variables en el script y volver a ejecutarlo. Por supuesto, queremos interpretar los resultados y adaptar algunas opciones clave a cada situación.

### 5.1 Mozambique

Para completar, hemos proporcionado una versión completa del Script Maestro adaptado a Mozambique. Se puede encontrar en el directorio OpenMRV bajo `cls_landsat_v2_mozambique`, o directamente de [este enlace](https://code.earthengine.google.com/b6c049e0f85da94a4ea392bce261d19c). 

#### 5.1.1 Ajustes al código

Solo fue necesario cambiar algunas piezas clave para proporcionar una clasificación inicial.

Primero, necesitamos especificar los límites espaciales apropiados. Debido a que el conjunto de datos que define los límites del país es global, podemos simplemente identificar la nueva región usando un cambio de nombre apropiado:

```javascript
var country = countries.filter(ee.Filter.eq('country_na', 'Mozambique'));
```

En segundo lugar, identificamos los datos de entrenamiento apropiados, aquí la versión desarrollada en el módulo anterior sobre datos de entrenamiento usando QGIS.

```javascript
var training_points = ee.FeatureCollection('users/openmrv/MRV/mozambique_training');
```

Para ejecutar el Script Maestro completo, estos dos cambios deben ocurrir tanto en la Sección 3.2 como en la Sección 3.7. Una muestra de mapas e imágenes de todo el país ilustra que se puede lograr la aplicación de los mismos métodos de clasificación (Figura M1).

![_fig_moz_initial_class](C:\Users\vanes\Downloads\figures\m1.3\_fig_moz_initial_class.png)

Figure M1.  Mapas de ejemplo generados por la simple transferencia de un script de clasificación de Colombia a Mozambique.

#### 5.1.2 Hallazgos

Al ejecutar todo el Script Maestro y evaluar los mapas, se destacan los siguientes hallazgos:

***La compensación por nubosidad no es tan crítica***

No es de extrañar que las nubes sean un desafío menor en Mozambique que en Colombia. De hecho, en la imagen de composición simple, no hay vacios en la cobertura en un solo año. Esto podría sugerir que evitemos el uso de las imágenes compuestas de dos años por completo, especialmente si los datos de entrenamiento se recopilaron de un año.

***La transición de Bosque-a-Pradera es un reto***

En un ambiente más seco, las especies leñosas en Mozambique presentan diferentes desafíos para la clasificación. Cada uno de los enfoques de clasificación difiere del otro en la cantidad y distribución de la clase "bosque": las imágenes compuestas simples difieren de las imágenes compuestas de dos años que usan el mismo clasificador, y los diferentes clasificadores también difieren. El desafío es particularmente evidente cuando los mapas se comparan a una escala fina (Figura M2). Aunque no hay intención de usar los datos de entrenamiento aquí para mapeo autorizado, esta variabilidad indica un problema importante. Las mejoras podrían incluir una resolución más precisa de las definiciones de clases de bosque o una mayor densidad de muestra de entrenamiento.

![_fig_m2_zoom](C:\Users\vanes\Downloads\figures\m1.3\_fig_m2_zoom.png)

Figura M2. Comparación de tres variantes de clasificación en el esquema de clasificación supervisado. Tenga en cuenta que la variabilidad en el patrón espacial de las etiquetas de los bosques entre los tres es más pronunciada en los niveles intermedios de cobertura forestal.

### 5.2 Camboya

Al igual que en Mozambique, hemos proporcionado una versión completa del Script Maestro adaptada a Camboya. Se puede encontrar en el directorio OpenMRV bajo  `cls_landsat_v2_Camboya`, o directamente de [este enlace](https://code.earthengine.google.com/1fcaac622c0e644bf3139c251657f777). 

#### 5.2.1 Ajustes al código 

En Camboya, como en Mozambique, solo se necesitan unos pocos cambios para aplicar la misma estructura de clasificación, nuevamente con la presunción de que existen datos de entrenamiento: cambiar la ruta a los datos de entrenamiento y el nombre del país utilizado para el análisis de límites.

#### 5.2.2  Hallazgos

Aunque Camboya no tiene las regiones semiáridas que tiene Mozambique, se ve menos afectada por las nubes que Colombia: el compuesto de un año que utiliza la detección de nubes a nivel de píxeles no muestra áreas importantes en las que falten datos. También como antes, la aplicación del modelo de RF disminuye la sobreclasificación de áreas urbanas en áreas herbáceas o con vegetación escasa, pero no elimina por completo el problema (Figura C1).

![fig_camb_fourmaps](C:\Users\vanes\Downloads\figures\m1.3\fig_camb_fourmaps.png)

# 6.0 Preguntas Frecuentes

**¿Qué sucede si hay algunas áreas que casi siempre están nubladas, sin importar cuántos años de imágenes tenga?** 

Hay varias opciones:

- Si las áreas ocupan un pequeño porcentaje del mapa general, y si el propósito del mapa es estimar el área total en diferentes clases de cobertura terrestre, entonces puede ser posible considerar estos píxeles como la clase "desconocida" y considerar esa clase explícitamente cuando se construyan las tablas de precisión y estimaciones de área más adelante. Estos simplemente agregarán incertidumbre a las estimaciones del área.
- Considere utilizar otra fuente de imágenes ópticas pasivas en lugar de o además de su imagen original. Por ejemplo, podría ser posible combinar imágenes de Sentinel-2 con imágenes de Landsat para mejorar las probabilidades de encontrar observaciones de píxeles sin nubes.
- Considere el uso de imágenes de sensores SAR (radar de apertura sintética) que pueden mapear la superficie terrestre incluso en presencia de nubes. Sin embargo, todos los tipos de sensores tienen sus propios problemas para considerar al construir mapas, y las imágenes de radar no son una excepción. Consulte el Manual de SAR para obtener una explicación a fondo de las imágenes de SAR.

**Una vez que construyo un clasificador para un año, ¿puedo aplicarlo a imágenes en otros años para hacer mapas anuales?**

La respuesta corta es que no se recomienda. El espacio de datos espectrales de sus imágenes de entrenamiento es particular para las condiciones bajo las cuales se registraron: los valores espectrales por píxel varían debido a los caprichos de cuando un píxel tuvo vistas claras, el grado de precisión de la corrección atmosférica, la estacionalidad de la vegetación en un año versus otro, etc. En una primera aproximación, esperamos que el vínculo general entre los datos espectrales y las condiciones del suelo sea sólido, pero en los márgenes de las clases, o en clases que tengan un alto grado de variabilidad entre los años, las diferencias pueden ser bastante dramáticas. Hay dos formas básicas de abordar esto: 1) crear nuevas clasificaciones cada año o 2) usar una herramienta para estabilizar los datos espectrales a lo largo del tiempo.

**Si trabajo para corregir errores de clasificación en una región, ¿qué hago si la solución causa nuevos problemas en otra región?** 

La mejor respuesta es recopilar más datos de entrenamiento en ambas regiones y ejecutar un clasificador que pueda usar diferentes partes del espacio de datos espectrales de una manera no paramétrica. Esto proporciona la mayor flexibilidad local en la clasificación. Además, es posible que desee incluir otras capas covariables en su algoritmo de clasificación: otras fuentes de imágenes o incluso otros tipos de datos, como datos de elevación, suelo o clima. Estos podrían ayudar a un algoritmo de clasificación a diferenciar sus áreas de interés.

Como último recurso, podría simplemente delinear los estratos en su país según algunos criterios defendibles, ejecutar ejercicios de clasificación separados en cada región y luego manejar estos diferentes estratos cuando haga su evaluación de precisión posterior.

**¿Cómo podemos manejar mejor los impactos del sombreado topográfico?**

Los impactos de la topografía montañosa sobre las características de la imagen a menudo pueden ser graves. El sombreado topográfico provoca tanto efectos obvios (reducción general de la reflectancia) como efectos menos obvios (reducción diferencial del brillo en diferentes bandas espectrales debido a la iluminación diferencial directa vs indirecta). Si bien existen métodos para compensar los impactos visuales de los efectos topográficos, el hecho desafortunado es que la señal en los aspectos sombreados de las montañas es simplemente diferente. En la práctica, un enfoque razonable para manejar estos efectos es: 1) garantizar que los datos de entrenamiento se distribuyan en todos los aspectos, 2) incluir variables topográficas en la pila de clasificación y 3) garantizar que el clasificador utilizado tenga la capacidad de asignar la misma etiqueta de clase a para porciones desunidas del espacio de datos.  

**Este ejemplo solo tiene cuatro clases, pero necesitamos muchas más. ¿Cómo nos ayuda esto?**

De hecho, los ejemplos utilizados en este tutorial se limitan a un conjunto muy simple y pequeño de etiquetas de clasificación. Sin embargo, los métodos utilizados aquí podrían aplicarse igualmente a un esquema de clasificación con tantas clases como se desee.

Sin embargo, al desarrollar esquemas de etiquetado de clases más complejos, es importante recordar que 1) para que un clasificador basado en datos espectrales distinga entre píxeles en diferentes clases, esas clases deben ser separables en alguna parte de su dominio de señal, y 2) en cuanto más fino se divida el espacio de datos en muchas clases, menos precisa se espera que sea una clase determinada.



------
![](figures/m1.1/cc.png)

Este trabajo tiene licencia bajo un [Creative Commons Attribution 3.0 IGO](https://creativecommons.org/licenses/by/3.0/igo/) 

Copyright 2020, World Bank 

Este trabajo fue desarrollado por Robert E Kennedy bajo contrato del World Bank con GRH Consulting, LLC para el desarrollo de recursos nuevos o existentes relacionadas a la Medida, Reportaje, y Verificación para el apoyo de implementación MRV en varios países. 

Material revisado por:
Kenset Rosales  & Sofia Garcia / Ministry of Environment and Natural Resources, Guatemala
Jennifer Juliana Escamilla Valdez / Minsterio de Medio Ambiente y Recursos Naturales, El Salvador
Raja Ram Aryal /  Ministry of Forests and Environment, Nepal
KONAN Yao Eric Landry / REDD+ Permanent Executive Secretariat, Cote d'Ivoire
Carole Andrianirina / BNCCREDD+, Madagascar
Phoebe Odour / RCMRD, Kenya

Atribución
Kennedy, Robert E . 2020. Land Cover and Land Use Classification in Google Earth Engine. © World Bank. License: [Creative Commons Attribution license (CC BY 3.0 IGO)](http://creativecommons.org/licenses/by/3.0/igo/)

![](figures/m1.1/wb_fcfc_gfoi.png) 
