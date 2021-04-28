---
title: Diseño de respuesta
summary: Este tutorial presenta el concepto de diseño de respuesta, enumera términos relevantes y destaca diferentes herramientas que se pueden utilizar para la recopilación de observaciones de referencia en el contexto de la estimación del área y la precisión del mapa. Se pueden encontrar más tutoriales aquí sobre OpenMRV en el proceso "Recolección de datos de muestra" y herramientas "GEE", "AREA2", "CE" y "CEO".
author: Pontus Olofsson
creation date: febrero 2021
language: español
publisher and license: Copyright 2021, World Bank. Este trabajo tiene licencia bajo un Creative Commons Attribution 3.0 IGO

tags:
- OpenMRV
- GEE
- AREA2
- CEO
- CE
- Estratificado
- Aleatorio Simple
- Sistemático
- Diseño de respuesta
- Encuesta
- Diseño de encuesta
- Datos de referencia
- Clasificación de referencia
- Observaciones de referencia

group:
- categoría: Collect Earth
  etapa: Recopilación de datos de referencia
- categoría: GEE
  etapa: Recopilación de datos de referencia
- categoría: Estratificado
  etapa: Estimación de Area/Evaluación de Precisión
---

# Diseño de Respuesta

## 1 Contexto

El diseño de respuesta define la "respuesta" de las unidades en una muestra. En el contexto de la inferencia basada en el diseño en un contexto geográfico, "el diseño de respuesta abarca todos los pasos del protocolo que conducen a una decisión sobre el acuerdo de las clasificaciones de referencia y mapa y la mejor clasificación disponible de las condiciones de la superficie terrestre para cada unidad espacial muestreada "(Olofsson et al. 2014). Son de importancia los siguientes términos:

**Datos de referencia:** 

Datos que caracterizan la evaluación disponible más precisa de la condición real en la ubicación de la muestra (ejemplo: imágenes de satélite de resolución fina).

**Observaciones de referencia:** 

La evaluación disponible más precisa de la verdadera condición de una unidad de población.

**Clasificación de referencia:** 

La clasificación de referencia aplicada a la colección de todas las unidades de muestra.

Se puede encontrar terminología adicional con respecto a las técnicas de muestreo a continuación en 1.2 Terminología adicional.

Aquí en OpenMRV, en "Recopilación de datos de muestra" y las herramientas "GEE", "AREA2", "CE" y "CEO", encontrará tutoriales en los que podrá aprender a determinar las condiciones de referencia examinando un conjunto de datos de referencia en ubicaciones del conjunto de datos de muestra. Este conjunto de datos tendrá cuatro estratos: bosque, no bosque, disturbio de bosque, y un amortiguador alrededor de la perturbación del bosque. El objetivo es estimar el área del disturbio forestal; en consecuencia, aprenderá a recopilar observaciones de referencia de *bosque, no bosque* y *disturbio del bosque*. Esto se demuestra en tres herramientas diferentes entre las que el usuario puede elegir: GEE/AREA2, Collect Earth Desktop y Collect Earth Online.

### 1.1 Tutoriales

- Para el diseño de respuesta utilizando **AREA2**, consulte el proceso "Recopilación de datos de muestra" y las herramientas "AREA2" y "GEE" aquí en OpenMRV.
- Para el diseño de respuesta utilizando **Collect Earth Desktop**, consulte el proceso "Recopilación de datos de muestra" y la herramienta "CE" aquí en OpenMRV.
- Para el diseño de respuesta utilizando **Collect Earth Online**, consulte el proceso "Recopilación de datos de muestra" y la herramienta "CEO" aquí en OpenMRV.

## 1.2 Terminología Adicional

**Diseño de Respuesta** (definiciones similares)

Definido por Stehman and Czaplewski, 1998: “La referencia o clasificación 'verdadera' se obtiene para cada unidad de muestreo en función de la interpretación de fotografías aéreas o videografías, una visita terrestre o una combinación de estas fuentes. Los métodos utilizados para determinar esta clasificación de referencia se denominan "diseño de respuesta". El diseño de respuesta incluye procedimientos para recopilar información relacionada con la determinación de la cobertura terrestre de referencia y reglas para asignar una o más [etiquetas] de referencia a cada unidad de muestreo ". Conocido como "plan de medición" por Särndal et al. (1992).

**Muestra**

Un subconjunto de unidades de población seleccionadas de la población.

**Diseño de Muestra**

Sinónimo de diseño de muestreo, que es el término preferido en la literatura fundamental (Cochran, 1977, Särndal et al., 1992). El término aparece en Rice (1995) que utiliza tanto "diseño de muestreo" como "diseño de muestra".

**Diseño de Muestreo**

"El diseño de muestreo es el protocolo mediante el cual se seleccionan las unidades de muestra de referencia". (Stehman y Czaplewski, 1998). El “diseño de muestreo” también es utilizado por Cochran (1977) y Särndal et al. (1992) - el primero también usa "plan de muestreo".

**Encuesta**

Särndal y col. (1992) define una encuesta como una “investigación parcial de una población finita”, y además que “los términos 'encuesta' y 'encuesta por muestreo' se utilizan para denotar investigaciones estadísticas con las siguientes características metodológicas: [. ..] plan de medición [...] de muestreo probabilístico [y] estimación."

**Diseño de Encuesta**

Un "diseño total de la encuesta" define los procedimientos para "obtener la posible precisión en las estimaciones de la encuesta mientras se logra un equilibrio entre los errores de muestreo y los no muestrales [...] El diseño de la encuesta da lugar a operaciones de encuesta" como la selección de la muestra (Särndal et al., 1992). Lohr (1999) describe un diseño de encuesta total como "Una filosofía de diseño de encuesta para minimizar los errores de muestreo y de no muestreo". Además, en Lohr (1999) “diseño de encuestas” es sinónimo de diseño de muestreo.

## 2 Referencias

Cochran, W.G., 1977. *Sampling Techniques*, John Wiley & Sons, New York, NY.

Lohr, S.L., 1999. *Sampling: Design And Analysis,* CRC Press.

Olofsson, P., Foody, G.M., Herold, M., Stehman, S.V., Woodcock, C.E. and Wulder, M.A., 2014. Good practices for estimating area and assessing accuracy of land change. Remote Sensing of Environment, 148, pp.42-57. https://doi.org/10.1016/j.rse.2014.02.015

Rice, J.A., 1995. *Mathematical Statistics and Data Analysis* (2nd ed.), Duxbury Press, Belmont, CA.

Särndal, C.E., Svensson, B.H., & Wretman, J.H., 1992. *Model assisted survey sampling*, Springer Science & Business Media, New York, NY.

Stehman, S.V., & Czaplewski, R.L., 1998. Design and analysis for thematic map accuracy assessment: fundamental principles. *Remote Sensing of Environment*, 64(3), 331-344. https://doi.org/10.1016/S0034-4257(98)00010-8

-----

![](figures/cc.png)  

Este trabajo tiene licencia bajo un [Creative Commons Attribution 3.0 IGO](https://creativecommons.org/licenses/by/3.0/igo/).

Copyright 2021, World Bank

Este trabajo fue desarrollado por Pontus Olofsson bajo contrato del World Bank con GRH Consulting, LLC para el desarrollo de recursos nuevos o existentes relacionados a la Medida, Reportaje, y Verificación para el apoyo de la implementación MRV en varios países.

Atribución  
Olofsson, P. 2021. Response Design. © World Bank. License: [Creative Commons Attribution license (CC BY 3.0 IGO)](http://creativecommons.org/licenses/by/3.0/igo/)

![](figures/wb_fcfc_gfoi.png)
