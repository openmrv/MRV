---
title: Recopilación de Datos de Entrenamiento
summary: Este tutorial demostrará cómo recopilar datos de entrenamiento categóricos para la clasificación de la cobertura terrestre utilizando QGIS o Google Earth Engine. Los usuarios deben ajustar los distintos componentes para que coincidan con los objetivos de su proyecto. Aquí, el proceso se demuestra para los países de Colombia, Mozambique y Camboya, y para una leyenda simple de cuatro clases de cobertura terrestre - bosque, agua, herbáceo y desarrollado.
author:
- Eric Bullock
- Karis Tenneson
creation date: diciembre 2020
language: Español
publisher and license: Copyright 2020, World Bank. Este trabajo tiene licencia bajo un Creative Commons Attribution 3.0 IGO

tags:
- OpenMRV
- Landsat
- Sentinel 2
- Planet Labs
- MODIS
- QGIS
- GEE
- Cobertura de nube
- Sensores ópticos
- Resolución alta
- Teledetección
- Imagen compuesta
- Mosaico
- Mapeo de cobertura terrestre
- Mapeo de bosque 
- Muestra
- Diseño de muestra
- Diseño de muestreo
- Selección de muestras 
- Colombia
- Mozambique
- Camboya

group:
- categoría: Imagen compuesta (Mediana)
  etapa: Creación de imagen compuesta/Pre-procesar
- categoría: Landsat
  etapa: Insumos
- categoría: Sentinel-2
  etapa: Insumos
- categoría: MODIS
  etapa: Insumos
- categoría: QGIS
  etapa: Recopilación de datos de entrenamiento
- categoría: GEE
  etapa: Colección de datos de entrenamiento
---

# Recopilación de Datos de Entrenamiento

## 1 Contexto

Los datos de entrenamiento son fundamentales para la clasificación de imágenes supervisadas. El conjunto de datos de entrenamiento es un conjunto de datos etiquetado que se utiliza para informar o "entrenar" a un clasificador. Luego, el clasificador entrenado se puede aplicar a nuevos datos para crear una clasificación. Por ejemplo, los datos de entrenamiento de cobertura terrestre contendrán ejemplos de cada clase en la leyenda del estudio y, en base a estas etiquetas, el clasificador puede usarse para predecir la clase de cobertura terrestre más probable para cada píxel de una imagen. Este es un ejemplo de una clasificación categórica y, por lo tanto, las etiquetas de entrenamiento son categóricas. Por el contrario, una variable continua (por ejemplo, porcentaje de cobertura de árboles) se puede predecir utilizando etiquetas de entrenamiento continuo.

Este tutorial demostrará cómo recopilar datos de entrenamiento categóricos para la clasificación de la cobertura terrestre utilizando QGIS o Google Earth Engine. Los usuarios deben elegir la opción con la que estén más familiarizados (QGIS o Google Earth Engine) y deben ajustar los diversos componentes para que coincidan con los objetivos de su proyecto. Aquí, el proceso se demuestra para los países de Colombia, Mozambique y Camboya, y para una leyenda simple de cuatro clases de cobertura terrestre: bosque, agua, herbácea y desarrollada.

### 1.1 Tutoriales

* For training data collection using **QGIS** please refer to process "Training Data Collection" and tool "QGIS" here on OpenMRV
* For training data collection using **Google Earth Engine**, please refer to process "Training Data Collection" and tool "GEE" here on OpenMRV

-----

![](./figures/m1.1/cc.png)  

Este trabajo tiene licencia bajo un [Creative Commons Attribution 3.0 IGO](https://creativecommons.org/licenses/by/3.0/igo/).

Copyright 2020, World Bank

Este trabajo fue desarrollado por Eric Bullock y Karis Tenneson bajo contrato del World Bank con GRH Consulting, LLC para el desarrollo de recursos nuevos o existentes relacionados a la Medida, Reportaje, y Verificación para el apoyo de la implementación MRV en varios países.

Atribución
Bullock, E., Tenneson, K. 2020. Image mosaic/composite creation for Landsat and Sentinel-2 in Google Earth Engine. © World Bank. License: [Creative Commons Attribution license (CC BY 3.0 IGO)](http://creativecommons.org/licenses/by/3.0/igo/)



![](./figures/m1.1/wb_fcfc_gfoi.png)
