---
title: Module 3.3.3 Survey Form Creation and Reference Observation Collection with Collect Earth Online
toc: true
colorlinks: blue
---

# Módulo 3.3.3 Creación de Forma de Encuesta y Colección de Observaciones de Referencia con Collect Earth Online

## 1 Contexto

Se requieren observaciones de referencia para calcular estimaciones de área e incertidumbre insesgadas a partir de un producto cartográfico. Las observaciones de referencia suelen ser un conjunto de datos etiquetados, derivado de un mapa de actividad (por ejemplo, mediante una muestra aleatoria estratificada) y etiquetado utilizando imágenes o datos de campo. Esto se compara con los estratos del mapa de un mapa de actividad para estimar la precisión del mapa y obtener estimaciones de área no sesgadas. Este tutorial demostrará cómo recopilar observaciones de referencia con etiquetas categóricas para generar estimaciones de incertidumbre y área no sesgadas utilizando Collect Earth Online. Los usuarios deben ajustar los distintos componentes para que coincidan con los objetivos de su proyecto. Aquí, el proceso se demuestra para el país de Colombia y para una leyenda de mapa simple que indica la presencia o ausencia de pérdida o degradación del bosque.


### 1.1 Collect Earth Online

Collect Earth Online es un sistema de interpretación y visualización de imágenes satelitales de código abierto y personalizado para recopilar datos para su uso en proyectos que requieren información de referencia sobre la cobertura del suelo y/o el uso del suelo. Collect Earth Online promueve la coherencia en la localización, interpretación y etiquetado de muestras para su uso en la clasificación y seguimiento del cambio de cobertura y uso de la tierra. La funcionalidad completa de Collect Earth Online, incluida la compilación colaborativa de bases de datos de puntos de referencia, se implementa en línea, por lo que no es necesario instalarlo en el escritorio. 

### 1.2 Objetivos de Aprendizaje

Al final de este ejercicio, podrá redactar, revisar y publicar un proyecto en Collect Earth Online. Esto incluye:

* Diseño de encuestas en Collect Earth Online.

* Selección de imágenes para ver para la interpretación de datos.

* Recopilar y exportar observaciones de referencia.

### 1.3 Prerrequisitos para este modulo

* Comprender la terminología del Módulo 3.1 y tener un diseño de muestra establecido, que se describe en los Módulos 3.2 y 3.3.
* Comprensión general de la interpretación de imágenes. La interpretación de imágenes es el proceso de observar imágenes de resolución espacial moderada, alta o muy alta (de satélites o fotografías aéreas) y etiquetar los objetos de interés en las ubicaciones de las muestras. La interpretación de fotografías es la habilidad principal necesaria para ejecutar de manera efectiva cualquier proyecto de CEO.
* Para obtener más información, consulte el Manual de creación de proyectos e instituciones de Collect Earth Online, que se encuentra en [Collect Earth Online Support Pages](https://collect.earth/support)
* Se recomienda que comprenda los tutoriales anteriores de los Módulos 1 y 2


### 1.4 Registrarse para obtener una cuenta de Collect Earth Online

1. En su navegador de internet, navegue a [CEO](https://collect.earth/). CEO apoya a Google Chrome, Mozilla Firefox, y Microsoft Edge.

2. Haga clic en [Login/Register] en la parte superior a mano derecha.

3. Para configurar una cuenta nueva, haga clic en [Register] y siga las instrucciones. Recibirá una bienvenida si la registración fue exitosa. 

4. Cuando haya creado una cuenta, ingrese con su email y su contraseña.

5. Si se le olvido su contraseña, haga clic en [Forgot your password?] y siga las instrucciones.

### 1.5 Recursos de Collect Earth Online

Puede acceder las paginas de Home (Inicio), About (Acerca de), Support (Apoyo), y Account (Cuenta) desde el bar de menú en la parte superior. 

* La página Home incluye información sobre instituciones, proyectos publicados y un mapa que muestra la ubicación de los proyectos existentes.
* La página About resume la información sobre CEO.
* La página Support incluye manuales, tutoriales y una demostración de Collect Earth Online. Esta página también incluye enlaces para informes de errores y foros para pedir ayuda.
* La página Account enumera información como estadísticas de usuario y permite a los usuarios actualizar la configuración de su cuenta.
* Hay un signo de interrogación violeta en la esquina superior derecha de la pantalla. Al hacer clic en esto, aparecerá la interfaz de ayuda, que proporciona información sobre las funciones del CEO. Estas interfaces de ayuda están disponibles para la página de inicio, para la recopilación de datos y para la creación de proyectos.


## 2. Configurando Feeds de Imágenes en Collect Earth Online

Hay múltiples fuentes de imágenes públicas disponibles a todos los usuarios en Collect Earth Online. Estas incluyen Mapbox Satellite y los datos de Planet disponibles gracias a una colaboración con el International Climate and Forests Initiative (Planet NICFI) de Noruega. También puede agregar sus propias fuentes de imágenes privados a la página de su Institución. Recomendamos agregar Sentinel 1, Sentinel 2, y Bing, como se describe próximamente. Todas estas son opciones gratuitas. 

1. Vaya a la página de su institución en Collect Earth Online. Luego haga clic en la pestaña de Imagery. 

### 2.1 Agregar datos Sentinel 2 a la pagina de Institución

Imágenes de Sentinel 2 están disponibles desde junio 2015-presente. Después de ajustar las configuraciones usando las siguientes instrucciones, los datos Sentinel 2 data serán enviados de GEE a CEO para el uso de sus usuarios. 

1. Hacer clic en 'Add New Imagery' (agregar imágenes nuevas).

2. Del menú desplegable, seleccione 'Sentinel 2' como el tipo. 

3. Titulo: Este será el nombre mostrado de las imágenes. Escriba 'Sentinel 2'.

4. Año Predeterminado: El año predeterminado que será mostrado cuando se cargue el mapa. Escriba '2020'.

5. Mes Predeterminado: El mes predeterminado que será mostrado cuando se cargue el mapa. Usar formato de numero entero 1-12. Escriba 1 para cargar el mes de enero de forma predeterminada.

6. Combinación de Bandas: Seleccione una de las opciones disponibles, incluyendo True Color (color verdadero), False Color Infrared (infrarrojo de color falso), False Color Urban (urbano color falso), Agriculture (agricultura), Healthy Vegetation (vegetación saludable), y Short Wave Infrared (infrarrojo de onda corta). 

Para este ejercicio, seleccione 'False Color Infrared'. Este estiramiento nos ayuda a distinguir entre suelo/pavimento y la vegetación. Rojo oscuro corresponde con la vegetación, y los rojos mas profundos corresponden con vegetación mas densa. Suelo y pavimento aparecen como gris o marrón. 

7. Min: Valor mínimo para bandas que serán mapeadas a 0 para visualización. Esto debería de ser un solo numero. Valores aceptables para el mínimo de cada banda son los mismos que en el Geo-Dash y Sentinel disponible en GEE generalmente; ver [https://developers.google.com/earthengine/datasets/catalog/sentinel](https://developers.google.com/earthengine/datasets/catalog/sentinel).

Para este ejercicio, seleccione 0.

8. Max: Valor máximo para bandas que serán mapeadas a 255 para la visualización. Esto debería de ser un solo numero. Valores aceptables para el máximo de cada banda son los mismos que en el Geo-Dash y Sentinel disponible en GEE generalmente. Vea el enlace de arriba. Por ejemplo, valores de 2800-4000 son usados con frecuencia. 

Para este ejercicio, seleccione 3500. (Unidades son unidades de reflectancia * 10000)

9. Cloud Score: Cobertura de nube aceptable. Valores pueden ser de 0-100.

Para este ejercicio, seleccione 20.

10. Si quiere agregar esta fuente de imágenes a todos los proyectos de su institución, active la casilla junto a "Add Imagery to All Projects When Saving". 

Para este ejercicio, seleccione esta opción.

11. Cuando todos los campos estén llenos, haga clic en [Add New Imagery].

![](figures/AddS2.JPG)

### 2.2 Agregar datos de Sentinel 1 a pagina de Institución

Información de Sentinel 1 solo esta disponible de abril del 2014 hasta el presente (lanzamiento de Sentinel 1A). Después de ajustar las configuraciones usando las instrucciones siguientes, los datos de Sentinel 1 serán enviados de GEE a CEO para el uso de sus usuarios. 

1. Regrese a su pagina de Institución. Bajo la pestaña de Imagery, haga clic en 'Add New Imagery'.

2. Del menú desplegable, seleccione 'Sentinel 1' como el tipo. 

3. Título: Este será el nombre mostrado de las imágenes. Escriba 'Sentinel 1'.

4. Año predeterminado: El año predeterminado que será mostrado cuando se cargue el mapa. Escriba en '2020'.

5. Mes predeterminado: El mes predeterminado que será mostrado cuando se cargue el mapa. Usar formato de numero entero 1-12. Escribir '1' para cargar imágenes de enero de forma predeterminada. 

6. Combinación de Bandas: Combinaciones de bandas predeterminadas para la mayoría de usos. VH y VV son de polarización singular, VH/VV y HH/HV son polarización dual. Más información esta disponible aquí:
[Sentinel 1 User Guide, Acquisition Mode](https://sentinel.esa.int/web/sentinel/user-guides/sentinel-1-sar/acquisition-modes). 

Para este ejercicio, seleccione 'VH,VV, VH/VV'.

7. Min: Valor mínimo para bandas que serán mapeadas a 0 para visualización. Esto debería de ser un solo numero. Valores aceptables para el mínimo de cada banda son los mismos que en el Geo-Dash y Sentinel disponible en GEE generalmente; ver [https://developers.google.com/earthengine/datasets/catalog/sentinel](https://developers.google.com/earthengine/datasets/catalog/sentinel). Min puede ser tan bajo como -50, pero frecuentemente se usa 0.

Para este ejercicio, seleccione '0'.

8. Max: Valor máximo para bandas que serán mapeadas a 255 para la visualización. Esto debería de ser un solo numero. Valores aceptables para el máximo de cada banda son los mismos que en el Geo-Dash y Sentinel disponible en GEE generalmente. Vea el enlace de arriba. Por ejemplo, el valor de 1 se puede usar, pero .3 se usa con frecuencia.

Para este ejercicio, seleccione '0.4'. (Unidades de coeficientes de retrodispersión gamma cero).

9. Si desea agregar esta fuente de imágenes a todos los proyectos de su institución, marque la casilla junto a "Add Imagery to All Projects When Saving". Marque esta casilla para agregar la fuente a todos los proyectos existentes. 

10. Cuando todos los campos estén llenos, haga clic en [Add New Imagery].

![](figures/AddS1.JPG)

### 2.3 Agregar imágenes de Bing a la pagina de Institución 

Esto le permite agregar Bing Maps con su propia clave API. Las imágenes proporcionadas por Bing Maps son imágenes de satélite compuestas. Esto significa que cada mosaico de mapa se une a partir de imágenes adquiridas en varias fechas. No hay una sola fecha para un mosaico de imágenes. Algunos mosaicos de mapas contienen imágenes recopiladas durante una ventana de varios días, mientras que otros mosaicos contienen imágenes recopiladas durante una ventana de varios años. Como no hay una sola fecha para un mosaico de imágenes, el director ejecutivo no puede proporcionar la fecha exacta de las imágenes utilizadas. Si le interesa saber mas, la API de los Mapas Bing se puede encontrar aquí: [Bing Imagery-metadata](https://docs.microsoft.com/en-us/bingmaps/restservices/imagery/imagery-metadata). 

El sistema de mosaicos de Bing utiliza la proyección de Mercator y tiene 23 niveles de zoom (aunque no todos los niveles están disponibles en todas las ubicaciones). Por lo general, la resolución con el zoom máximo es de aproximadamente 0.3 m por píxel. Para más información, ver [Bing maps tile system](https://docs.microsoft.com/en-us/bingmaps/articles/bing-maps-tile-system).

#### 2.3.1 Direcciones para solicitar una llave de Bing maps:

1. Para usar imágenes de Bing Maps para sus proyectos, puede crear su propia clave de Bing Maps GRATIS para conectar los proyectos de su institución a su cuenta de Bing Maps. Las direcciones completas para crear una llave están aquí: [Get a Bing maps key](https://docs.microsoft.com/en-us/bingmaps/getting-started/bing-maps-devcenter-help/getting-a-bing-maps-key).

2. Visitar [Bing Maps Portal](https://www.bingmapsportal.com/) para solicitar una llave Bing o una copia de su llave existente.

a. Iniciar sesión en su cuenta. Necesitara una cuenta de Bing maps o una cuenta de Microsoft
[Account page](https://docs.microsoft.com/en-us/bingmaps/getting-started/bing-maps-dev-centerhelp/creating-a-bing-maps-account).

b. Una vez que haya ingresado, haga clic en My account, luego haga clic en My Keys (Mis llaves).

c. Si ya tiene una llave, haga clic en Show key (Mostrar llave) o Copy key (Copiar llave).

d. Si no tiene llave, haga clic en "Click here to create a new key" para crear una llave nueva.

e. Complete la información necesaria. El URL de aplicación es opcional, pero si lo quiere completar puede usar https://collect.earth como su URL. 

f. Creará un Basic key (una llave básica). Si necesita mas imágenes, necesitará hablar con Microsoft y solicitar un [Enterprise key](https://www.microsoft.com/en-us/maps/create-a-bingmaps-key#enterprise)

#### 2.3.2 Direcciones para conectar su llave de Bing maps key en Collect Earth Online:

1. Regrese a su página de Institución. Bajo la pestaña de Imagery, haga clic en 'Add New Imagery'.

2. Del menú desplegable, seleccione 'Bing Maps' como el tipo. 

3. Titulo: Este será el nombre mostrado de las imágenes. Escriba 'Bing Maps'.

4. Id de Imágenes: Solo se implementan Aerial y AerialWithLabels por el momento. Note que las imágenes AerialWithLables usan el servicio de legacy static tile (el servicio de teselas estáticas heredado), el cual es obsoleto, y los datos mas recientes no se actualizaran. Por esto, pueda que tenga imágenes más antiguas que el conjunto de datos de Bing Aerial dataset. Seleccione Aerial.

5. Token de Acceso: Escriba su llave de BingMaps. Para mas información o para obtener su propia llave, ver 2.3.1 arriba.

6. Si desea agregar esta fuente de imágenes a todos los proyectos de su institución, marque la casilla junto a Add Imagery to All Projects When Saving. Marque esta casilla para agregar la fuente a todos los proyectos existentes. 

7. Cuando todos los campos estén llenos, haga clic en [Add New Imagery].

### 2.4 Fuentes de Imágenes Adicionales

Consulte el Manual de creación de proyectos e instituciones de Collect Earth Online para obtener información sobre cómo agregar fuentes de imágenes adicionales, como recursos de imágenes de Google Earth Engine. Se puede acceder al manual aquí: [Collect Earth Online Support Pages](https://collect.earth/support).

## 3. Diseño de Respuesta

### 3.1 Resumen

El diseño de un proyecto es un proceso iterativo, y probablemente necesitará realizar varias ediciones en los proyectos en CEO a medida que prueba y refina sus objetivos, esquemas de clasificación de cobertura o uso de la tierra, fuentes de imágenes, etc. Estos cambios deben examinarse y realizarse para un proyecto antes de que se publique. Esto significa que, idealmente, puede dedicarle tiempo a poner a prueba un proyecto, recopilar datos de prueba con el cuestionario y revisarlo para adaptarlo a cualquier error o ineficiencia que encuentre antes de publicar el proyecto y comenzar los esfuerzos oficiales de recopilación de datos.

En la práctica, encontramos que la creación de un proyecto piloto y la recopilación de datos piloto es increíblemente útil para recopilar datos de alta calidad. El proceso con frecuencia se verá así:

1. Redacte su diseño de muestra y sus preguntas en consulta con los miembros clave del proyecto.
2. Cree un proyecto piloto en CEO utilizando su diseño de muestra y preguntas preliminares.
3. Pídale a los miembros clave de su equipo que recopilen algunos datos utilizando el proyecto piloto del CEO.
4. Revise las áreas de confusión en la redacción de las preguntas y la configuración del proyecto del CEO.
5. Revise las áreas de acuerdo y desacuerdo con la identificación de la cobertura terrestre. Por ejemplo, quizás el agua sea fácil de identificar para todos los miembros del equipo, pero las clases de bosques son difíciles.
2. Utilice la discusión sobre áreas de acuerdo y desacuerdo para crear una clave de cobertura terrestre. Este es un documento que contiene información de interpretación importante sobre diferentes clases de cobertura terrestre. Incluye varias imágenes de cada clase de cobertura terrestre, así como descripciones de cómo se ve cada clase. El documento ayuda a los intérpretes a identificar las clases de cobertura terrestre cuando recopilan datos y aumenta el acuerdo entre los diferentes intérpretes.
3. Utilizando los comentarios del proyecto piloto, cree proyectos para que los intérpretes recopilen los datos de "producción" o "finales". Se eliminarán todos los datos recopilados de las muestras interpretadas antes de la publicación.
4. Recopilar y analizar datos.

### 3.2 Crear un proyecto nuevo

Para comenzar, abra un navegador de web y navegue a [Collect Earth Online](https://collect.earth/). Navegue a la página de su institución. 

1. En la pestaña de Projects en la página de su institución, haga clic en [Create New Project]. Esto lo llevará al wizard (asistente) de creación de proyectos. El asistente consiste de 6 partes, cada una explicada próximamente. 

![](figures/Wizard.png)

#### 3.2.1 Resumen del Proyecto: 

Esta sección le permite agregar información general acerca del proyecto, incluyendo la selección de una plantilla (opcional), nombre de proyecto, descripción de proyecto, y opciones de proyecto. 

1. [Opcional] Use una plantilla de proyecto (project template): esta función se usa para copiar toda la información, incluida la información del proyecto, el área y el diseño de muestra, de un proyecto existente publicado a un proyecto nuevo. Esto es útil si tiene un proyecto existente que desea duplicar para otro año o ubicación, o si está iterando a través del diseño del proyecto. Para una plantilla, puede utilizar cualquier proyecto publicado o cerrado disponible de su institución. No puede utilizar proyectos eliminados. No puede usar el proyecto privado de otra institución (solo los miembros o administradores tienen acceso), pero puede usar el proyecto público de otra institución (cualquier visitante del sitio web o usuario del CEO). Para obtener más información sobre la configuración de privacidad del proyecto, consulte Visibilidad a continuación.

Para este ejercicio, practicará diseñar su propio proyecto comenzando de cero, así que puede saltarse esta sección, y deje la opción de [Select Project] puesta en el campo de "Select Template". 

Sin embargo, información acerca de como trabajar con una plantilla se incluye próximamente para su referencia. 

  i. Filtro de Plantilla (Nombre o ID): Escriba una palabra clave en el nombre de un proyecto existente o el Numero de ID de un proyecto. Este numero se puede encontrar si navega al proyecto que quiere copiar y mira el URL. 

  ii. Luego haga clic en el menú desplegable abajo de "Select Project" y hacer clic en el nombre del proyecto. 

![](figures/Template.png)

  iii. Haga clic en el nombre del proyecto, y luego haga clic en "Load" para cargar la información de la plantilla. 

  iv. Haga clic en "Clear" para borrar toda la información de la plantilla. 

  v. Cargar una plantilla creará dos casillas abajo de Copy Options: Copy Template Plots (Copiar parcelas de plantilla) y Samples and Copy Template Widgets (Widgets de Muestras y Copeo de Plantilla). Están activadas automáticamente. 

    * Si está activada la casilla de 'Copy Template Plots and Samples', las secciones de Plot Review and Sample Design (Repaso de Parcela y Diseño de Muestra) solo mostraran una vision general del numero de las parcelas, etc. Desactive esta casilla para cambiar esos parámetros. 
    
    * La casilla de 'Copy Template Widgets' se refiere a las opciones de Geo-Dash cubiertas en Parte 6: Implementación de Geo-Dash.

2. Llene el nombre y la descripción del proyecto. El Nombre debe de ser corto y será mostrado en la pagina de Inicio además de la pagina de Colección de Datos.

    i. Para este ejercicio, nómbrelo 'Example Project for Area Estimation' (Proyecto Ejemplo para Estimación de Área.)

**Consejos:**
Debe mantener la Descripción breve pero informativa. Los usuarios lo verán si hacen clic en el pin del proyecto en el mapa de la página de inicio. También verá esto cuando esté administrando su proyecto. Tenga en cuenta que si está utilizando una plantilla, el nombre y la descripción se completarán automáticamente. Asegúrese de cambiar esto para reflejar su nuevo proyecto.

3. Seleccione la visibilidad del proyecto. El botón de opción "Privacy Level" (Nivel de privacidad) cambia quién puede ver su proyecto, contribuir a la recopilación de datos y si los administradores de su institución u otras personas que crean nuevos proyectos pueden usar su proyecto como plantilla.

  * Public: All: Todos los usuarios pueden ver y contribuir datos a su proyecto. Administradores pueden usar su proyecto como plantilla. 

  * Users: Logged in Users: Cualquier usuario que este ingresado en CEO puede ver y contribuir a su proyecto. Administradores pueden usar su proyecto como plantilla. 

  * Institution: Group Members: Miembros de su institución pueden ver y contribuir a su proyecto. Administradores de otras instituciones no pueden usar su proyecto como plantilla. 

  * Private: Group Admins: Solo administradores de su institución pueden ver y contribuir a su proyecto.  Administradores de otras instituciones no pueden usar su proyecto como plantilla. 

Para este ejercicio, seleccione "Institution".

4. Seleccione "Project Options" (Opciones de proyecto).

i. La primera opción es "Show GEE Script Link on the Collection Page" (Mostrar enlace a Script de GEE en la Página de Colección). Esto permite que usuarios en Data Collection hagan clic en un botón etiquetado [Go to GEE Script to open a new tab with a series of Landsat and Sentinel time series images and charts] (ver siguiente imagen). El botón abrirá una pestaña nueva con una serie de tiempo de imágenes Landsat y Sentinel. Para este ejercicio, seleccione esta opción. 

I. La primera opción es 'Show GEE Script Link on the Collection Page' (Mostrar enlace al Script de GEE en la página de Colección). Esto permite que los usuarios en Data Collection hagan clic en un botón etiquetado [Ir a GEE Script para abrir una nueva pestaña con una serie de imágenes y gráficos de series de tiempo de Landsat y Sentinel] (ver imagen abajo). Para este ejercicio, seleccione esta opción.

![](figures/GEE_script.JPG)

En el ejemplo de imagen del script GEE hay tres paneles. En el extremo izquierdo, hay una composición de Sentinel 2 de los últimos 12 meses. Se colorea utilizando un compuesto de color infrarrojo (infrarrojo cercano, infrarrojo medio, rojo). En el centro están los mosaicos Landsat 8 y Landsat 7 Color Yearly, con un control deslizante para que pueda elegir entre años. A la derecha están los gráficos NDVI del gráfico de MODIS, Landsat 7/8 y Sentinel 2. Para los gráficos Landsat 7/8 y Sentinel, puede hacer clic en un punto de los gráficos para cargar imágenes específicas en los paneles izquierdo y central.

ii. La segunda opción es "Show Extra Plot Columns on Collection Page" (Mostrar Columnas de Parcela Extras en Pagina de Colección). Esta permite que seleccione información presente en los datos de sus ubicaciones de muestras (por ejemplo, el csv de un shapefile). Ejemplos comunes de información suplementaria que pueda incluir en su muestra son elevación o jurisdicción (por ejemplo, estado, provincia, distrito). Para este ejercicio, no seleccione esta opción. 

  * Esta opción solo es útil si esta usando archivos de .csv o .shp para definir su Diseño de Parcela. 

  * Si tiene columnas adicionales en sus archivos de .csv o .shp, como información de elevación o de cobertura de suelo, los recopiladores de datos podrán verlos en la página abajo de "Plot Information" (Información de Parcela).

iii. La tercera opción es 'Auto-launch Geo-Dash' (Lanzar Geo-Dash automáticamente). El Geo-Dash es otra pestaña que se puede diseñar para mostrar imágenes y gráficos de series de tiempo e imágenes. Esto automáticamente abrirá la interfaz de Geo-Dash en una ventana o pestaña nueva cuando el recopilador de datos navegue a una parcela nueva. Desactivar esta opción significa que recopiladores de datos tendrán que hacer clic en el icono de Geo-Dash abajo de "External Tools" (Herramientas Externas) en la interfaz de Colección de Datos.

Para este ejercicio, seleccione lanzamiento automático de Geo-Dash.

5. Su pantalla debería de verse similar a la imagen siguiente. Haga clic en "Next" para llegar al panel de selección de imágenes. 

![](figures/ProjectOverview.JPG)

#### 3.2.2 Selección de Imágenes 

En el panel de "Imagery Seleccion" (Selección de imágenes), puede cambiar las imágenes del mapa base predeterminado y los mapas base de imágenes que están disponibles para los usuarios durante la recopilación de datos.

1. La primera opción le permite especificar las imágenes predeterminadas que los usuarios verán cuando comiencen a recopilar datos para su proyecto. Sus usuarios pueden cambiar entre todas las capas de imágenes disponibles durante la colección de datos. 

Las opciones predeterminadas (publicas) de las cuales todos pueden escoger incluyen  MapBox Satellite, Mapbox Satellite con etiquetas, y Planet NICFI Public. También puede agregar sus propias fuentes de imágenes privadas en la pagina de su institución. Por favor refiérase al manual de Collect Earth Online Institution and Project Creation para aprender como. Lo puede acceder aquí: [Collect Earth Online Support Pages](https://collect.earth/support).

Puede elegir cualquiera de las opciones de imágenes disponibles para su institución. Para este ejercicio, seleccione Mapbox Satellite. Observe que, después de hacer la selección, la Vista previa de imágenes mostrará la selección actual.

**Nota:** Si tiene una licencia comercial para PlanetMonthly, PlanetDaily, y SecureWatch, ellos no permiten extracciones grandes de datos, así que estos no pueden servir somo su mapa de base automático (los usuarios verán una pantalla o caja en blanco). Si quiere trabajar con estas fuentes, le recomendamos que use un mapa de base automático diferente y que sus recopiladores de datos cambien a PlanetDaily una vez que se hayan acercado lo suficiente a una parcela para interpretarla. 

2. Public Imagery (Imágenes Publicas) son las imágenes que están disponibles para todas las instituciones. Si tiene un proyecto publico, todos los usuarios, incluyendo los que no se han ingresado a sus cuentas, pueden ver esas imágenes. Active la casilla a un lado de cada fuente de imágenes que quiere que este disponible para su proyecto. Para este ejercicio, selecciónelas todas.

3. Private Institution Imagery (Imágenes de institución privada) son imágenes que solo son visibles para los miembros de una institución, aun si tiene su proyecto puesto en publico.

Active la casilla a un lado de cada fuente de imágenes que quiere que este disponible para su proyecto. Previamente en el ejercicio, establecimos fuentes de Sentinel 1, Sentinel 2, y Bing maps. Seleccione los tres. 

4. Haga clic en "Next" cuando haya terminado.

![](figures/ImagerySelection.JPG)

#### 3.2.3 Especificación de Muestra: Diseño de Parcela

El sistema integrado de CEO permite que usuarios creen diseños de muestreo usando una interfaz fácil de usar. Hay dos partes claves, seleccionando el área de interés y la generación de parcelas.

##### 3.2.3.1 Seleccione su área de interés (AOI)

Para este ejercicio usaremos la selección de muestras creado anteriormente y exportado como archivo csv. Esto establecerá el área de interés (AOI por sus siglas en ingles) para el proyecto. CEO limita el AOI alrededor de las ubicaciones de parcela que usted suba. Por eso, salte las próximas instrucciones para dibujar el AOI manualmente. 

Estos pasos están incluidos próximamente para su referencia. 

i. La manera mas fácil de seleccionar el área de interés de su proyecto es dibujando una caja en la ventana de mapa en el panel a mano derecha (Collection Map Preview).

  * Ubique su área de interés haciendo zoom usando la rueda de desplazamiento de su mouse o las cajas +/- en su ventana de mapa. Puede arrastrar el mapa si lo mueve mientras sostiene el clic en la ventana de mapa.

  * Sostenga el botón CTRL (o 'command' en Mac) y dibuje una caja mientras mantiene el botón izquierda del mouse sostenido. 

  * Sostenga el botón SHIFT y dibuje una caja para acercarse a una área (hacer zoom). 

  * Las cajas de coordenadas se poblaran una vez que la caja este dibujada y suelte el botón del mouse. Las coordenadas se muestran en formato lat/long usando WGS84 EPSG:4326.

![](figures/AOI.png)

ii. Puede incluir manualmente las coordenadas de límites en las cajas provistas. 

![](figures/CoordBoundingBox.png)

##### 3.2.3.1 Diseño de Parcela 

En la sección "Plot Design" (Diseño de Parcelas), puede especificar el tipo y número de parcelas. Para este ejercicio usaremos la selección de muestra creada anteriormente y exportada como un csv. Hay otras tres opciones para ubicar parcelas: aleatoriamente, diseño cuadriculado y carga de un shapefile.

Para este ejercicio, siga las instrucciones para cargar el archivo csv. Luego, omita las siguientes instrucciones para trabajar con opciones aleatorias, cuadriculadas o shapefile. Estos pasos se incluyen a continuación para su referencia.

Notas adicionales acerca de trabajar con archivos de parcelas especificados por el usuario: Usando archivos .csv y .shp, el numero máximo de parcelas es 50,000 y el limite total de puntos de muestra es 350,000. Debe de usar el formato WGS84 EPSG:4326 para coordenadas en archivos .csv y .shp.

Primero debemos de ajustar el formato del archivo .csv. El archivo que suba para especificar los centros de parcelas debe de contener estas columnas, en este orden: LON, LAT, PLOTID.

i. En un software para el formato de hojas de calculo como Excel, abra el archivo de muestra aleatoria estratificada que creo en el ejercicio de selección de muestra (Modulo 3.2). 

![](figures/stratSmplRaw.JPG)

ii. Copiar y pegar las columnas alrededor para que la primera contenga las coordenadas de longitud, seguida por coordenadas de latitud, y luego el ID de la parcela.

iii. Cambiar los nombres de las columnas a: LON, LAT, PLOTID. Note, si hay distinción entre mayúsculas y minúsculas, así que asegúrese de usar mayúsculas. 

iv. Borre la columna llamada '.geo'.

v. Guarde los cambios a su .csv.

![](figures/stratSmplMod.JPG)

Nota: si no especifica los nombres de columnas correctamente (deletreando o en orden), recibirá el siguiente error: 

![](figures/csvError.png)

Longitud debe de estar entre -180 and 180, y latitud debe de estar entre -90 and 90. Si los confunde, puede obtener un error si su longitud es mas grande que 90 o menos que -90 (cuando esto se confunde con latitud, esta "por encima" del polo). Revise bien estos valores. 

Ahora subiremos el archivo a CEO.

1. En la pestaña de Plot Design abajo de Spatial Distribution (Distribución Espacial) seleccione ‘CSV file.’

2. Haga clic en 'Upload plot file' (Subir archivo de parcela).

3. Plot Shape (Figura de parcela) puede ser circulo o cuadrado. Seleccione 'Square'  (cuadrado). 

4. Necesitará especificar el diámetro en metros. Estos tamaños deberían de ser definidos por las necesidades de su proyecto. Para este ejercicio, escriba 30 metros para corresponder con la resolución de un pixel de Landsat.  

Nota: cuando las parcelas con pequeñas, sus usuarios necesitaran alejarse/hacer 'zoom out' considerablemente para ver la imagen de fondo relevante porque CEO automáticamente se centra y se acerca dentro de los limites de la parcela.

5. Haga clic en"Next" cuando haya terminado. 

##### Solo para referencia, instrucciones acerca de como trabajar con las otras opciones de diseño de parcela 

* En CEO, puede especificar un método de muestreo Random (aleatorio) o uno Gridded (cuadriculado, sistemático espacial). 

* Si seleccione Random, necesitara proveer el numero de parcelas para todo el proyecto.  

* Si selecciona Gridded, necesitará proveer el espacio entre los centros de las parcelas en metros.  

**Nota:** CEO proveerá un estimado de cuantas parcelas se generaran para su proyecto en base a su diseño de muestreo. Usando el muestreo de CEO, el numero máximo de parcelas para un proyecto es 5,000. Para el muestreo cuadriculado, pueda que necesite incrementar el espacio entre las parcelas para no exceder el máximo de 5,000 parcelas.

#### 3.2.4 Especificación de Muestra: Diseño de Muestra 

Aquí es donde especificara cuantos puntos de muestra están dentro de cada parcela, y si se crearon con un método aleatorio, cuadriculado, o una distribución personalizada.  

1. Bajo Spatial Distribution puede seleccionar "random", "gridded", "center", "csv", "shp" o "none". Para este ejercicio, selección "Center." Con Center, un punto de muestra será puesto en el centro de su parcela, y no necesita especificar otra cosa.
2. Para cualquiera de estas distribuciones espaciales, puede hacer clic en la casilla junto a [Allow users to draw their own samples to enable proactive sampling] (Permitir que usuarios dibujen sus propias muestras para activar muestreo proactivo). El muestreo proactivo permite que los recopiladores de datos dibujen líneas, puntos, y polígonos directamente en el mapa para crear sus propias muestras. El recopilador de datos luego tiene que responder algunas preguntas acerca de cada figura. Muestreo proactivo es útil para recopilar datos de entrenamiento para informar modelos de random forest y de autoaprendizaje.

Para este ejercicio, puede dejar esa opción sin activar.

![](figures/SmpDesign.JPG)

3. Haga clic en Next.

##### Solo para su referencia, instrucciones acerca de como trabajar con las otras opciones de diseño de muestra:

* Con el muestreo aleatorio, puntos de muestra será distribuidos aleatoriamente dentro de los limites de la parcela. También necesitara especificar el numero de muestras por parcela. 

* Con muestreo cuadriculado, puntos de muestra serán arreglados en una cuadricula dentro de los limites de la parcela. Necesitara especificar la distancia entre los puntos dentro de la parcela, bajo resolución de muestra (Sample Resolution) en metros. 

* Usando el muestreo de CEO, el numero máximo de puntos de muestra por parcela es 200.

* Usando el muestreo de CEO, el numero máximo total de puntos de muestra para el proyecto (numero de parcelas * numero de puntos/parcela) es 50,000.
Si necesita mas puntos o parcelas, por favor cree su diseño de muestreo en otro programa y súbalo a CEO usando el formato de archivo de .csv o .shp y las instrucciones en la próxima sección.

* Con "None" (Ninguno), no predefinirá muestras. Esto requiere que los usuarios dibujen sus propias muestras durante la recopilación. 

* Por favor refiérase al manual de [Collect Earth Online Institution and Project Creation Manual](https://collect.earth/support) para leer acerca de como trabajar con muestras especificadas con un csv o shapefile. 

#### 3.2.5 Preguntas de Tarjeta de Notas ('Notecard Questions')

Aquí es donde diseña las preguntas que sus recolectores de datos / intérpretes fotográficos responderán para cada una de sus parcelas. Cada pregunta crea una columna de datos. A partir de estos datos sin procesar, puede calcular métricas de área, etc.

Tarjetas de Pregunta con la unidad básica de organización. Cada tarjeta crea una página de preguntas en la interfaz de Colección de Datos. El flujo de trabajo básico es: 

i. Crear nueva pregunta de nivel-alto (nueva tarjeta de pregunta) y poblar respuestas 

ii. Crear preguntas y respuestas 'hijo' 

iii. Mover a la próxima pregunta de nivel-alto (nuevo tarjeta de pregunta) & repetir hasta que todas las preguntas hayan sido preguntadas.

Para la pestaña de "Survey Question" (Pregunta de Encuesta), el panel izquierdo permite que ingrese preguntas mientras que el panel derecho proporciona una vista previa de como estas preguntas le aparecerán a sus recopiladores de datos. Ahora entraremos en mas detalle acerca de como agregar una pregunta y respuestas, los tipos de preguntas que se pueden hacer, y cuando estas preguntas pueden ser útiles. 

##### 3.2.5.1. Como agregar preguntas y respuestas 

CEO provee una manera directa para hacer preguntas de opción múltiple. Ya que es el tipo de pregunta usado con mayor frecuencia, lo usaremos para este ejemplo. En CEO, estas preguntas se llaman "button text" o "texto de botón" ya que dentro de colección de datos, aparecen como un botón con texto. 

Las preguntas de este tipo son útiles para inventarios de uso del suelo y cobertura del suelo, o en cualquier lugar donde desee que el usuario elija entre un conjunto limitado de opciones mutuamente excluyentes.

1. Para comenzar, escriba su primera pregunta en la caja de New Question (Nueva Pregunta). Ya que es su primera pregunta, no puede asignar una Pregunta Padre o una Respuesta Padre. Mantenga la pregunta por debajo de 45 caracteres para que toda la pregunta sea visible durante la recolección de datos. 

Para este ejercicio, escriba 'Current Land Cover' (Cobertura de Suelo Actual).

2. Haga clic en [Add Survey Question] para crear su primera tarjeta de encuesta. 

3. Ahora puede agregar Respuestas a su pregunta. Las respuestas tienen dos partes, un color y una caja de texto. 

i. Haga clic en el rectángulo azul para que aparezca el Selecto de Color. Puede mover el punto o tipo de selector de color en los valores RGB (0-255). El color que escoja será asociado con la respuesta. Cuando un recolector de datos selecciona esa respuesta color, los puntos de muestra asignados a esa respuesta también tendrán ese color en el mapa. Para la primera respuesta, seleccione azul ya que eso será asociado con agua. 

ii. Ahora escriba su respuesta en la caja de texto. Trate de escribir respuestas con aproximadamente 15 caracteres o menos para que el nombre entero sea mostrado durante la recolección de datos. Escriba 'WATER'.

iii. Haga clic en el símbolo verde [+] para agregar la respuesta.

iv. Repita estos pasos para todas las clases siguientes: Nieve/hielo, Desarrollado, Desnudo, Arboles, Arbustos, Pastizales, Cultivos, y Otro. Continúe agregando respuestas hasta que todas las respuestas para su pregunta de encuesta hayan sido agregadas. 

4. Ahora preguntaremos si hubo un cambio. En el blanco de nuevas preguntas en la parte inferior de la pantalla, escriba 'Did land use change occur' (¿Ocurrió cambio de uso de suelo?). Luego agregue la pregunta a la encuesta, mantenga el botón de texto, no preguntas padres, y no respuestas padres como las configuraciones predeterminadas.  

5. Ahora agregue respuestas usando el método que se explico en paso 3 anteriormente para agregar una opción de "No Cambio" y una de "Cambio". 

6. Ahora que tiene preguntas de nivel-alto (o padre) con respuestas, puede agregar preguntas y respuestas hijo que aparecerán solo cuando respuestas especificas sean seleccionadas. Preguntas de padre e hijo, particularmente las preguntas hijo que tienen respuestas padre, son útiles cuando tienen categorías grandes y quiere refinar la respuesta dentro de la categoría. Puede haber preguntas adicionales dependiendo de la respuesta del usuario para refinar aun mas la información acerca de la parcela. Por ejemplo, si el usuario categoriza una parcela como bosque, puede preguntarle si es un bosque conífero o  caducifolio. 

Para este ejercicio, agregaremos una pregunta hijo acerca del año del cambio. 

i. Primera, mantenga el tipo de componente como botón de texto. 

ii. Luego, para crear una pregunta hijo, seleccione ‘¿Ocurrió cambio de uso de suelo?’ como su pregunta padre. 

iii. Luego puede asignar una respuesta padre con el menú desplegable. Cuando se seleccione una respuesta, la pregunta hijo aparecerá.  Si no quiere una respuesta padre, entonces ponga 'Any' (Cualquiera) en ese campo. Para este ejercicio, seleccione su respuesta ‘Change’ (Cambio).

iv. Ahora preguntaremos cuando ocurrió el cambio. En el blanco de Nueva Pregunta en la parte inferior de la pantalla, escriba 'Año del cambio mas reciente, si ocurrió uno'. Luego haga clic en Add Survey question, y mantenga la configuración de botón de texto.

v. Ahora agregue respuestas usando el método explicado en paso 3 arriba para agregar respuestas para cada año del 2009 al 2020. 

7. También agregaremos una pregunta hijo que aparece sin importar la respuesta que se seleccione para la pregunta de cambio. 

i. Agregaremos una pregunta acerca de confianza. En el blanco de nuevas preguntas, escriba  'Nivel de confianza'. Luego haga clic en "Add Survey question", use ‘Año de cambio mas reciente’ como su pregunta padre, y 'Any' para la respuesta padre.

ii. Ahora agregue respuestas como ‘Bajo,’ ‘Mediano,’ y ‘Alto’ como opciones.

8. Ahora agregaremos una pregunta acerca de la cobertura de suelo previa. 

i. En el campo de Nueva Pregunta, escriba 'Cobertura de suelo previa'. Luego haga clic en "Add Survey question", mantenga la configuración de botón de texto, use ‘Hubo cambio? ’ como su pregunta padre, y 'Cambio' como su respuesta padre. 

ii. Ahora agregue respuestas a la nueva pregunta hijo usando el método explicado en paso 3 arriba. Lo puede hacer usando las mismas categorías de cobertura de suelo que usamos en la primera pregunta: Agua, Hielo/nieve, desarrollado, desnudo, arboles, arbustos, pastizales, cultivos, y otro. 

![](figures/ChildQ.JPG)

8. Puede repetir este proceso para preguntar si hubo cambios antes del evento de cambio mas reciente. Agregue hasta tres opciones de eventos de cambios.

9. Una vez que haya escrito todas las preguntas, puede revisar y repasarlas haciendo clic en los números en el panel de vista previa de preguntas a mano derecha en la pantalla. 

10. Una vez que este satisfecho con la lista, haga clic en Next para proceder con el panel de reglas de encuestas. 

##### Notas, consejos, y trucos para crear preguntas en CEO

* Puede eliminar una pregunta haciendo clic en la [X] roja. Eliminar una pregunta padre con hijos también eliminará las preguntas hijos.
* Puede contraer una "Survey Card" (Tarjeta de encuesta) haciendo clic en el símbolo [-] en la esquina superior izquierda.
* Puede cambiar el orden de las tarjetas de encuesta haciendo clic en las flechas azules hacia arriba y hacia abajo en la parte superior derecha.

* Intente mantener su pregunta por debajo de los 45 caracteres.

* Otras opciones de Tipo de componente: Las opciones de Tipo de componente disponibles incluyen combinaciones de cuatro tipos de preguntas y tres tipos de datos.

Los cuatro tipos de preguntas son:

* Button: Esto crea botones fáciles de usar, lo cual permite que los usuarios seleccionen una de muchas respuestas para cada punto de muestra. 

* Input: Permite que usuarios ingresen respuestas en la caja provista. El texto de  respuesta provisto por el creador del proyecto se convierte en la respuesta predeterminada.

* Radiobutton: Esto crea botones de radio, lo cual permite que el usuario seleccione una de muchas respuestas para cada punto de muestra. 

* Dropdown: Permite que usuarios seleccionen de una lista de respuestas. 

Los tres tipos de datos permitidos son:

* Boolean: Use esto cuando tiene dos opciones para una pregunta (si/no).

* Text: Use esto cuando tiene múltiples opciones que son cadenas de texto. Pueden incluir números, letras, o símbolos. 

* Number: Use esto cuando tenga varias opciones que sean números, que no contengan letras ni símbolos.

#### 3.2.6 Reglas de Encuesta

Las reglas de la encuesta ayudan a garantizar que los usuarios recopilen respuestas lógicas y correctas. Si no desea agregar ninguna regla, simplemente haga clic en Siguiente.

Para este ejercicio, no agregaremos ninguna regla de encuesta. Sin embargo, si desea obtener más información sobre estas opciones, consulte el manual [Collect Earth Online Institution and Project Creation Manual](https://collect.earth/support).

Esto completa el conjunto de proyecto. Haga clic en [Review] en la esquina inferior a mano derecha.

##### Solo para referencia, tipos de reglas de encuesta:

Tipos de reglas incluyen:

* Text Regex Match: Esta regla se aplica solo a las preguntas de texto de entrada y sus respuestas. Le permite verificar si el valor ingresado se ajusta, usando expresiones regulares. Sin embargo, a menos que tenga una razón específica para usar el tipo de pregunta de texto de entrada, considere usar texto de botón o texto de botón de radio en su lugar. Estas opciones son más fáciles para los usuarios y siempre proporcionarán texto exacto. Esta regla usa la función JavaScript RegExp, documentación para escribir la expresión regular se puede encontrar [aqui](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions).

* Numeric Range: Esta regla se aplica a las preguntas de número de entrada y sus respuestas. Con esta regla, puede verificar que la entrada numérica se encuentre dentro de un rango predefinido. Por ejemplo, si pregunta sobre la proporción de puntos en la parcela que contienen árboles, podría restringir las respuestas entre 0 y 1.

* Sum of Answers: Esta regla se aplica a cualquier pregunta de tipo numérico y sus respuestas. Seleccione varias preguntas (2 o más) y especifique a qué deben sumar las preguntas. Por ejemplo, esto es útil si tiene varias preguntas sobre el porcentaje de cobertura terrestre, donde la suma debe ser del 100%.

* Matching sums: Esta regla se aplica a cualquier pregunta de tipo numérico y sus respuestas. Con esta regla, especifica dos conjuntos de preguntas múltiples (2 o más) que deben tener sumas iguales.

* Incompatible answers: Esta regla se puede aplicar a cualquier tipo de pregunta. Permite al usuario definir conjuntos de respuestas incompatibles. Por ejemplo, si la respuesta a una pregunta es cobertura terrestre = "Agua", la respuesta a otra pregunta no podría ser uso de la tierra = "Industrial".

#### 3.2.7 Repaso de Proyecto y Publicación

1. Ahora verá una descripción general de los detalles de su proyecto.
2. Desplácese para comprobar que todo esté correcto.

I. Si todo está correcto, haga clic en "Create Project" (Crear proyecto).

ii. Si nota un error, haga clic en "Continue Editing" (Continuar editando) para arreglarlo.

4. Después de hacer clic en Create Project, una ventana aparecerá con la pregunta  'Do you REALLY want to create this project?' (En realidad quiere crear este proyecto?)

5. Haga clic en OK.

6. Después de crear el proyecto, será llevada a un panel de información del proyecto. Puede manejar su proyecto usando este menú. 


#### 3.2.8 Configurando Geo-Dash

Geo-Dash es un tablero que se abre en una segunda ventana cuando los usuarios comienzan a analizar parcelas de muestra. GeoDash proporciona a los usuarios información adicional para ayudarlos a interpretar las imágenes y clasificar mejor los puntos de muestra y las gráficas. La pestaña Geo-Dash se puede personalizar para mostrar información como series de tiempo NDVI, imágenes adicionales y datos digitales de elevación.

1. Puede configurar su Geo-Dash haciendo clic en [Configure Geo-Dash] de la página de información de proyecto. Esto abrirá la pantalla de layout de Geo-Dash.

![](figures/geoDash.JPG)

2. [Copy Layout] le permitirá copiar el Geo-Dash de otro proyecto. Esto borrará otros widgets de Geo-Dash que posiblemente ya haya asociado con su proyecto.

![](figures/copygeodash.JPG)

3. Puede agregar widgets de Geo-Dash individuales con [Add Widget]. Para entender el propósito de cada widget, haga clic en [Geo-Dash Help] para abrir el Centro de Ayuda de  Geo-Dash. 

Para este ejercicio, solo agregaremos uno de los muchos widgets Geo-Dash disponibles. Sin embargo, si desea obtener más información sobre estas opciones, consulte el manual [Collect Earth Online Institution and Project Creation Manual](https://collect.earth/support).

![](figures/geodashHelp.JPG)

#### 3.2.8.1 Agregando Imágenes ChronoSequence al Geo-Dash, el Widget de Degradación Forestal

El widget Degradación proporciona información de series de tiempo sobre la degradación forestal por tala selectiva, incendios y otras perturbaciones grandes y pequeñas. El índice de fracción de diferencia normalizada (NDFI, por sus siglas en inglés) permite una mejor detección del daño al dosel forestal de múltiples fuentes, incluida la tala selectiva y los incendios forestales. Se calcula con la metodología encontrada en Souza et. al (2005).

1. Haga clic en [Add Widget] en la parte superior a mano derecha de la pantalla de Geo-Dash layout.

2. Seleccione 'Degradation Tool' (Herramienta de Degradación) en el desplegable de Tipo.

3. Escoja la fuente del mapa de fondo del menú desplegable. Este será el mapa de base para el widget y otros datos serán encimadas en este. Seleccione Mapbox Satellite.

4. Dele un titulo al widget. Escriba 'Time series viewer tool' (Herramienta de vista de serie de tiempo).

5. Escoja cual banda quiere trazar. Opciones disponibles incluyen SWIR1, NIR, Red, Green Blue, SWIR2, y NDFI. NDFI permite la detección mejorada de daño al dosel de bosque de múltiples fuentes, incluyendo la tala selectiva y los incendios forestales. Seleccione NDFI.

6. Seleccione el rango de fechas de interés. Esta herramienta puede usar Landsat 4 (julio 1982 - diciembre 1993), Landsat 5 (marzo 1984 - enero 2013), Landsat 7 (abril 1999 - presente), y Landsat 8 (febrero 2013 - presente) basado en el rango que define el usuario. Información de Sentinel solo esta disponible desde abril 2014 hasta la fecha. Seleccione el rango de 01/01/2005 a 01/01/2020.

7. Haga clic en 'Create'.

8. Reposicione y cambie el tamaño a su gusto. Esta herramienta tendrá dos paneles, así que asegúrese de darle un amplio espacio vertical.

9. Los widgets se pueden manipular en el editor de diseño de widgets de Geo-Dash de varias formas. Para ver un gif que ilustra estos movimientos, vea [video](https://collect.earth/geo-dash/geo-dash-help) y haga clic en 'To Move and Resize Widgets' (Para mover y cambiar el tamaño de widgets).

## 4 Colección de Datos

### 4.1 Resumen

Los usuarios de su equipo que ayudarán a recopilar las observaciones de referencia deberán registrarse para obtener una cuenta de Collect Earth Online. Las instrucciones para hacer esto se encuentran a continuación. Como administrador de la institución, usted será responsable de asegurarse de que los miembros del equipo hayan sido invitados a la institución del director ejecutivo de su agencia para completar la recopilación de datos.

#### 4.2 La pantalla de análisis 

Una vez que se han agregado miembros a la institución, puede compartir el enlace al proyecto con ellos. O pídales que naveguen a la página de su institución y seleccionen el proyecto en la página de inicio de la institución.

![](figures/FindProject.JPG)

1. Una vez en la página de recopilación de datos del proyecto, puede acceder a la ayuda para la pantalla de análisis en cualquier momento haciendo clic en el signo de interrogación púrpura en la esquina superior derecha de la pantalla. La función de ayuda señalará características importantes de la página de recopilación de datos.

![](figures/HelpButton.JPG)

2. Primero asegúrese de hacer clic en el botón [Go to first plot] (Ir a la primera parcela) en la esquina superior a mano derecha.

* Para algunos proyectos, la segunda página o pestaña se abrirá automáticamente cuando entre a su primera parcela. Esta es la interfaz de Geo-Dash. Varios elementos diferentes se pueden mostrar en esta interfaz, dependiendo en lo que haya configurado su institución. Haga clic en la pestaña a mano izquierda para regresar a la página de colección de datos. 

3. Familiarícese con la pantalla de análisis. A mano izquierda esta la ventana de mapa:

* Su parcela de muestra aparecerá como un circulo o cuadro amarillo en la ventana de mapa. La figura de muestra depende de como fue diseñado el proyecto. 

* Cada punto de muestra es identificado con un circulo negro hasta que se le asigna una etiqueta. Puede cambiar el color de los puntos de muestra no asignados de negro a blanco si selección el botón de color correspondiente junto a "Unanswered Color" (Color sin respuesta) en el panel a mano derecha. 

* Puede hacer zoom usando los botones azules + y - en la esquina superior a mano izquierda de la ventana de mapa, o usando la rueda deslizante de su mouse. 

* Información acerca de la fuente de imágenes es mostrada en la parte superior de la pantalla. 

4. A mano derecha están todas las opciones de navegación, imágenes, y encuesta.

5. Opciones de navegación están incluidas en un menú desplegable. Este le permite seleccionar varias opciones: 

* Unanalyzed Plots (Parcelas sin analizar): lo predeterminado. Esta opción le permite recopilar datos en parcelas sin analizar para contribuir a su proyecto. 

* My analyzed plots (Mis parcelas analizadas): repase las parcelas que analizo previamente.  Esta opción le permitirá corregir errores etc. 

* All analyzed plots (Todas las parcelas analizadas): Esta opción solo es disponible a los administradores de la institución. Si usted es un administrador, puede examinar las parcelas analizadas por cualquier usuario.  

6. Debajo de este menú desplegable esta el numero ID de parcela. Junto a este ID hay botones azules de avance y retroceso. Estos se pueden usar para navegar a diferentes parcelas, y también hay un campo de texto donde puede ingresar un ID de parcela y hacer clic en [Go to plot] para navegar a esa parcela especifica.

7. Opciones para Herramientas Externas incluyen las siguientes: 

* Haga clic en [Re-Zoom] para regresar su enfoque a la parcela de enfoque. 

* Haga clic en [Geodash] para abrir la ventana de Geo-Dash con información adicional acerca de la parcela. 

* Puede hacer clic en [Download Plot KML] para descargar un archivo KML con información de parcela. Descargar un KML le permite transferir la información de parcela a otro programa, como Google Earth, para acceder las imágenes históricas que contienen. La funcionalidad KML permite que usuarios determinen las coordenadas (latitud y longitud) donde están ubicados los puntos de interés. 

* El botón de [Go to GEE Script] puede si o no estar presente en su tablero, dependiendo de como el administrador de su proyecto configuro los detalles del proyecto. Si esta presente, lo llevara a un sitio de aplicaciones Earth Engine mostrando datos adicionales acerca de la parcela.

8. Opciones de Imágenes: Usando el menú desplegable abajo de Imagery Options, puede cambiar la imagen fondo si selecciona imágenes diferentes de esta lista. Imágenes diferentes pueden ser útiles para comparar puntos diferentes en el tiempo, o donde una fuente de imágenes no tiene suficiente detalle para responder a las preguntas de encuesta. Algunas opciones de imágenes también incluyen los nombre de pueblos, ciudades, etc. 

9. Preguntas de Encuesta: Esta es el área donde puede responder a las preguntas de encuesta del proyecto. 

* Cada proyecto tiene un conjunto diferente de preguntas de encuesta enumeradas (en el ejemplo siguiente solo hay "1" pregunta en el proyecto). 

* Puede navegar entre preguntas usando las flechas de avance y retroceso o los números. 

* El botón de 'Unanswered Color' cambia el color de los puntos de encuesta.

* El botón 'Save' guardara sus respuestas de encuesta y lo moverá al próximo punto (solo se hace activo cuando todos los puntos han sido interpretados). 

* [Flag Plot] (Marcar Parcela) se usa cuando la pregunta no se puede responder, por que las imágenes no son suficientes para etiquetar los atributos de la parcela con precisión (porque faltan, porque la resolución es baja, etc.) o por algún otro problema. Esto lo avanzara automáticamente a la próxima parcela. 

* 'Clear All' borra todas las respuestas y preguntas de encuesta para esta parcela. 

* 'Quit' lo regresará a la página de Inicio de CEO.

10. La ventana emergente Geo-Dash también se abrirá con información acerca de la parcela si ha sido configurada para el proyecto. La ventana contiene información para asistir a identificar atributos de cobertura y uso de suelo compilado de Google Earth Engine. Dependiendo del proyecto, Geo-Dash puede incluir parcelas de datos de series de tiempo (por ejemplo, como valores de NDVI han variado a través del tiempo), chips de imágenes Landsat, y mas. 

#### 4.2 Analizar Parcelas 

1. Ahora es tiempo de contribuir al proyecto. 

2. Lea la primera pregunta de encuesta y las respuestas posibles. Está preguntando cual es la cobertura de suelo actual. Para determinar esto, aléjese de la parcela con zoom hasta que las imágenes se vean mas claras. Esto le permitirá conseguir mas pistas de contexto del paisaje.

![](figures/Q1.JPG)

3. Use el menú desplegable de 'Imagery Options' para cargar fuentes de imágenes disponibles y determinar cual es la cobertura de suelo actual. 

4. En el ejemplo arriba, son arboles. Para responder a la primera pregunta, solo haga clic en la respuesta --Arboles-- sin la necesidad de seleccionar los puntos dentro de la parcela primero. 

* En este proyecto de ejemplo solo tenemos un punto de muestra por parcela, sin embargo  en CEO es posible incluir múltiples muestras por parcela en la fase de diseño del proyecto. Si esta trabajando en un proyecto con múltiples muestras, puede asignar clases diferentes o respuestas a puntos en la parcela si primero selecciona los puntos de muestra. Cuando se seleccionan puntos de muestra, se hacen azules. 

* Para seleccionar un punto de muestra singular, haga clic en ese punto con el botón izquierdo del mouse. 

* Para seleccionar varios puntos de muestra de una vez, haga clic en ellos mientras mantiene presionado el botón de Shift.

* Para seleccionar todos los puntos en la parcela o todos los puntos en el rectángulo, presione Ctrl, y luego haga clic, sosténgalo, y arrástrelo en la ventana de mapa para dibujar su rectángulo. 

* Cuando sus puntos de muestra están marcados en azul, puede asignarles un valor de muestra haciendo clic en el valor adecuado en la leyenda a la derecha de la ventana del mapa. A continuación, los puntos de muestra se marcan con el color de la clase de valor.

* Si comete un error y asigna un valor incorrecto a un punto o puntos, puede volver a seleccionar los puntos y cambiar la "respuesta".


![](figures/Q2pre.JPG)

5. A continuación, seleccione la segunda pregunta de la encuesta haciendo clic en "2" o presione la flecha hacia la derecha. Esta pregunta es preguntar si ha habido un cambio en la cobertura del suelo, en qué año ocurrió. Si hubo más de un cambio, indica que debe registrar el año del evento de cambio más reciente.

![](figures/Q2.JPG)

6. Para determinar el historial del paisaje en esta parcela, es útil revisar los datos en Google Earth Pro, GEE Script y en la pestaña Geo-Dash. Primero, abra la pestaña Geo-Dash (es probable que sea la pestaña inmediatamente a la derecha de la pestaña de recopilación de datos. Es posible que deba hacer clic en el botón Geo-Dash si la pestaña aún no está abierta.
7. Haga clic en Descargar Plot KML para descargar un archivo .kml y verlo en Google Earth. Google Earth tiene varias fuentes de imágenes históricas y actuales que pueden ayudar a identificar una trama. Necesitará tener Google Earth Pro instalado en su computadora. Puede hacer clic en el archivo .kml descargado para abrirlo en Google Earth o importarlo manualmente en Google Earth. Luego, haga clic en el control deslizante de la serie temporal para alternar entre las imágenes disponibles para diferentes fechas.
8. En este ejercicio, la página Geo-Dash se ha configurado con solo una herramienta de visualización de series de tiempo. Esto incluye un gráfico de series de tiempo de los valores mensuales (NDFI) de enero de 2005 a enero de 2020 calculados a partir de las colecciones de imágenes de Landsat. Busque cambios bruscos y graduales en el gráfico de series de tiempo NDFI, que se muestra en el panel inferior. Recuerde examinar el gráfico de series de tiempo en busca de patrones cíclicos (que indiquen cambios estacionales) antes de evaluar valores inesperados. Estos patrones estacionales están presentes en los bosques caducifolios, pero no indican un cambio en la cobertura del suelo. Busque cambios abruptos (generalmente desengrasados bruscos) o cambios graduales (generalmente aumentos graduales). Estos indican posibles eventos de degradación y recuperación.

![](figures/TimeSeries.JPG)

9. Si identifica lo que parece un cambio del valor esperado, puede hacer clic en un punto del gráfico para cargar esa imagen Landsat en la ventana del mapa. Haga clic en una fecha individual (círculo azul) en el gráfico para que aparezcan las imágenes de ese período de tiempo. Es posible que deba esperar a que se carguen las imágenes.

* Por ejemplo, en la imagen de abajo hay un par de puntos con un valor NDFI bajo en comparación con la mayoría de los valores en el rango de tiempo. Por ejemplo, en la imagen de abajo hay una caída en los valores de NDFI el 9 de noviembre de 2015. Si hace clic en el punto de la imagen antes de la caída, verá que el paisaje parece arbolado. Si luego hace clic en el punto con un valor bajo (el 9-11-2015), la imagen se carga y el paisaje todavía parece arbolado. Sin embargo, hay un borde de nube que se superpone a la trama. En este ejemplo, parece que el cambio en la serie temporal se debe al ruido atmosférico en lugar de a los cambios en la cobertura del suelo. Después de hacer clic en todos los valores bajos de NDFI y examinar la imagen Landsat asociada, parece que todas estas caídas se deben a la cobertura de nubes en esta ubicación de la parcela. Por lo tanto, para este gráfico de la pregunta 2, seleccionaríamos 'Sin cambios'.

![](figures/prechange.png)

![](figures/Change.png)

* Al hacer clic en los puntos del gráfico, las imágenes a veces tardan un momento en cargarse.

* Nota: en la herramienta de vista de serie de tiempo, el panel superior es el panel de imágenes. Imágenes será mostradas aquí sobre los datos de OpenStreetMap cuando selecciona una fecha especifica en el panel inferior. La barra deslizante le permite seleccionar el nivel de opacidad de sus imágenes. Bajo la combinación de bandas, 321 significa una compuesta true color (R,G,B) y 543 representa compuesta 'false color' (SWIR, NIR, R). Usando la palanca de 'Data', puede escoger entre datos Landsat o SAR. 

* Nota: en la herramienta de vista de serie de tiempo, el panel inferior muestra un grafico de serie de tiempo de NDFI (el mas común) y otro métrico. Valores de NDFI entre -1 y 0 generalmente indican áreas que han sido taladas (y probablemente quemadas). Valores de NDFI cerca de +1 indican bosque intacto. Cada punto representa un periodo de tiempo de mes por mes donde hay datos para su parcela de muestras. 

* Un declive fuerte de NDFI (frecuentemente acompañado por una recuperación pequeña) puede indicar tala selectiva. El panel a mano izquierda muestra el paisaje antes; a la derecha es el después. Podemos ver que en nuestra parcela de muestras, se ha construido una carretera. Esto se registraría como una degradación aun en el 2009 con una recuperación durando aproximadamente 2-3 años. 

![](figures/road.png)

10. Haga clic en diferentes fechas en y alrededor de su evento sospechado para confirmar visualmente que si ocurrió un evento. Si ocurrió un evento, indique en que año ocurrió. Si no hubo cambios, seleccione 'No Changes'. 

11. Si un evento ocurrió, después de indicar el año de actividad una segunda pregunta aparecerá por debajo de la pregunta acerca del año del cambio de cobertura de suelo. Esta pregunta nueva pregunta acerca de la cobertura de suelo previa. Examine las imágenes Landsat antes del cambio y determine que tipo de cobertura era. Luego seleccione esa respuesta en el panel de preguntas de encuesta. 

12. Una vez que todas las preguntas hayan sido asignadas un valor para todas las preguntas de la encuesta, haga clic en SAVE. 

* Recibirá un mensaje de error si no ha respondido a todas las preguntas.  

13. La próxima parcela para análisis aparece automáticamente.

14. En cualquier momento, puede saltar una parcela para analizarla mas tarde si hace clic en la flecha [Next Plot Arrow] en la pestaña de "Plot Navigation". Alternativamente, haga clic en [Previous Plot Arrow] para volver a visitar una parcela previa. Puede hacer clic en [Flag Plot] (Marcar Parcela) si las imágenes no son suficientes para etiquetar los atributos de la parcela con precisión (porque faltan, porque la resolución es baja, etc.). Automáticamente volverá a cargar la próxima parcela para su proyecto.

* [Flag Plot] borrará cualquier atributos que se le hayan asignado a los puntos/parcelas.  

* Usando "Navigate Through" (Navegar) puesto en "My Analyzed Plots" (Mis Parcelas Analizadas) puede regresar a la parcela marcada y volver a intentar responder las preguntas. El botón para marcar la parcela estará desactivado ya que solo se pueden marcar una vez. 

* Sus respuestas serán grabadas, y la parcela ya no estará marcada si selecciona "Save".

* Parcelas pueden can ser marcadas o guardadas por un usuario, pero no ambas cosas. 

* A veces las parcelas pueden ser difíciles, aun que buenas imágenes. Estas parcelas solo pueden ser clasificadas de manera precisa y confiable con el conocimiento de sistemas agrícolas locales, tipos de vegetación, y patrones de paisaje locales. Intente usar el paisaje de la parcela para obtener toda la información posible antes de hacer una conjetura educada. Si no se siente cómoda interpretando la parcela, márquela con [Flag Plot].

15. Si hace clic en el nombre del proyecto, mostrara el numero y el porcentaje de las parcelas que han sido completadas, el numero y porcentaje de las que están marcadas, el numero y porcentaje de las que se consideran malas, y el numero total de las parcelas. Pronto también estará disponible una puntuación de precisión basada en los datos de formación del proyecto.

16. Cuando se clasifican todas las parcelas, aparece una ventana emergente para informarle que se analizaron todas las parcelas de muestra de su proyecto.

#### Consejos de Interpretación de Imágenes

* Problemas de estacionalidad pueden ocurrir cuando diferentes coberturas y usos de suelo aparecen de formas diferentes entre estaciones. Por ejemplo, un pastizal puede aparecer muy verde en la primavera pero marrón en el verano. Si solo examina la imagen marrón, pueda pensar que el marrón es suelo desnudo y clasificar esa área de manera incorrecta. 

* Acercarse y alejarse a la imagen usando zoom para recopilar pistas de contexto del paisaje es importante para múltiples tipos de coberturas y usos de suelo. Por ejemplo: 

  * Agua en cuerpos grandes de agua frecuentemente aparece negra u oscura hasta que se aleja mas de la imagen. 

  * Plantaciones de arboles pueden parecer bosques naturales hasta que se aleja de la imagen y observa el patrón regular y sistemático de los arboles plantados. 

## 6 Exportar Datos
1. Cuando haya recopilado todos los datos de su proyecto, navegue a la pagina de su institución. 

2. Junto a su proyecto hay dos opciones de descarga: 'Download Plot Data' (Descargar Datos de Parcela), la cual descarga los datos de forma resumida por parcela, y 'Download Sample Data' (Descargar Datos de Muestra), la cual descarga sus datos brutos con información de cada punto dentro de cada parcela como su propia fila. La descarga de datos de parcela se indica con una P y la descarga de datos de muestra se indica con una S (por sus siglas en ingles). Ambos se descargan en forma de archivo csv, el cual se puede abrir en programas como Microsoft Excel o importados a un software de análisis de datos. 

3. Datos descargados de CEO estarán en formato WGS84 EPSG:4326.

4. Descargar y guardar datos de muestra.

Usara estos datos descargados en modelos futuros para ejecutar estimaciones de área. 



## 4 Preguntas Frecuentes

**¿Cuándo debería usar CEO? **

Utilice CEO si tendrá varios recopiladores de datos (CEO) y si desea una configuración más sencilla para las preguntas de la encuesta (CEO).

**¿Dónde puedo encontrar ayuda dentro del CEO? **

Hay un signo de interrogación violeta en la esquina superior derecha de la pantalla. Al hacer clic en esto, aparecerá la interfaz de ayuda, que proporciona información sobre las funciones del CEO. Estas interfaces de ayuda están disponibles para la página de inicio, para la recopilación de datos y para la creación de proyectos.

**¿Cuándo debería usar una plantilla de proyecto?**

Esta función se utiliza para copiar toda la información, incluida la información del proyecto, el área y el diseño de muestreo, de un proyecto publicado existente a un proyecto nuevo. Esto es útil si tiene un proyecto existente que desea duplicar para otro año o ubicación, o si está iterando a través del diseño del proyecto.

**¿Qué debo poner en la descripción del proyecto?**

Debe mantener la Descripción breve pero informativa. Los usuarios los verán si hacen clic en el pin del proyecto en el mapa de la página de inicio. También verá esto cuando esté administrando su proyecto.

**¿Hay algo a tener en cuenta para las fuentes de imágenes pagas?**

Si tiene una licencia comercial para PlanetMonthly, PlanetDaily y SecureWatch, no permiten extracciones de datos de gran área, por lo que no debería ser su mapa base predeterminado (los usuarios solo verán un cuadro blanco). Si desea trabajar con estos feeds, le recomendamos que establezca un mapa base predeterminado diferente y que sus recolectores de datos cambien a PlanetDaily una vez que hayan hecho zoom en un gráfico para interpretar.

**¿Cuántos gráficos y muestras se permiten con archivos .csv y .shp?**

Con archivos .csv y .shp, el número máximo de parcelas es 50.000 y el límite total de puntos de muestra es 350.000. Debe utilizar el formato WGS84 EPSG: 4326 para las coordenadas en archivos .csv y .shp.

**¿Cuántas parcelas y muestras se permiten con proyectos generados por el CEO?**

El CEO proporcionará una estimación de cuántas parcelas se generarán para su proyecto en función de su diseño de muestreo. Usando el muestreo del CEO, el número máximo de parcelas para un proyecto es 5,000. Para el muestreo cuadriculado, es posible que deba aumentar el espacio entre parcelas para evitar exceder las 5.000 parcelas.

**¿Cuáles son algunos consejos para crear preguntas de encuestas?**

A continuación se ofrecen algunos consejos:

- Puede eliminar una pregunta haciendo clic en la [X] roja. Eliminar una pregunta de los padres con hijos también eliminará las preguntas de los hijos.
- Puede contraer una tarjeta de encuesta haciendo clic en el símbolo [-] en la esquina superior izquierda.
- Puede cambiar el orden de las Tarjetas de encuesta haciendo clic en las flechas azules hacia arriba y hacia abajo en la parte superior derecha.
- Intente mantener su pregunta por debajo de los 45 caracteres.

**¿Dónde puedo encontrar más información sobre el CEO y la creación de proyectos de CEO?**

Consulte el [Manual de creación de proyectos e instituciones de Collect Earth Online](https://collect.earth/support).



## 7 Referencias

Souza, C. M., Roberts, D. A., & Cochrane, M. A. (2005). Combining spectral and spatial information to map canopy damage from selective logging and forest fires. Remote Sensing of Environment, 98(2), 329-343.



Este trabajo tiene licencia bajo un [Creative Commons Attribution 3.0 IGO](https://creativecommons.org/licenses/by/3.0/igo/) 

Copyright 2021, World Bank 

Este trabajo fue desarrollado por Karis Tenneson y Karen Dyson  bajo contrato del World Bank con GRH Consulting, LLC para el desarrollo de recursos nuevos o existentes relacionadas a la Medida, Reportaje, y Verificación para el apoyo de implementación MRV en varios países. 

Atribución
Tenneson, Karis and Dyson, Karen. 2021. Module 3.3.3 Survey Form Creation and Reference Observation Collection with Collect Earth Online.  World Bank. 

License: Creative Commons Attribution license (CC BY 3.0 IGO)

![](figures/WB_FCPF.png)
![](figures/GFOI.png)

