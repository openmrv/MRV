---
title: Análisis de datos de muestra recopilados bajo SRS/SYS
summary: En este tutorial aplicaremos varios estimadores a un conjunto de datos de muestra para estimar las características de la población muestreada, es decir, características del área de estudio, como el área de perturbación del bosque. Este tutorial se centra en los datos de muestra recopilados en SRS/SYS.
author: Pontus Olofsson
creation date: febrero 2021
language: español
publisher and license: Copyright 2021, World Bank. Este trabajo tiene licencia bajo un Creative Commons Attribution 3.0 IGO

tags:
- OpenMRV
- AREA2
- GEE
- Precision
- Evaluación de precisión 
- Estimación de Area
- Colombia

group:
- categoría: Estratificado
  etapa: Estimación de Area/Evaluación de Precisión
---

# Análisis de datos de muestra recopilados bajo SRS/SYS 

## 1 Contexto

En los tutoriales anteriores, diseñamos y extrajimos una muestra del país de Colombia, y observamos y registramos las condiciones de cobertura del suelo de referencia en las ubicaciones de las unidades de muestra. La recopilación de observaciones de referencia se denomina resultados o datos de la muestra, o clasificación de referencia. En este tutorial aplicaremos varios estimadores a los datos de la muestra para estimar las características de la población que muestreamos, es decir, características del país de Colombia, como el área de perturbación forestal. Un estimador es “La regla por la cual una estimación de alguna característica de la población [es decir, parámetro] *μ* se calcula a partir de los resultados de la muestra ”(Cochran, 1977, p. 11). Tenga en cuenta que un estimador no es lo mismo que una estimación, sino que "un estimador es una función de la muestra, mientras que una estimación es el valor realizado de un estimador (es decir, un número) que se obtiene cuando una muestra es realmente tomado ”(Casella & Berger, 2002, p. 312). Un estimador tiene dos propiedades importantes: varianza y sesgo. El sesgo de un estimador *μ ^* de un parámetro de población *μ* es la diferencia entre *μ* y el valor esperado de *μ ^* en todas las muestras posibles; es decir, [![img](https://camo.githubusercontent.com/0a124237fea316e5d657b6f75cfa463307793bdf49738b559fbb5426df5f67a9/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f6769662e6c617465783f253543696e6c696e652673706163653b25354374657874757025374242696173253744282535436861742537422535436d75253744292673706163653b3d2673706163653b25354374657874757025374245253744282535436861742537422535436d75253744292673706163653b2d2673706163653b2535436d75)](https://camo.githubusercontent.com/0a124237fea316e5d657b6f75cfa463307793bdf49738b559fbb5426df5f67a9/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f6769662e6c617465783f253543696e6c696e652673706163653b25354374657874757025374242696173253744282535436861742537422535436d75253744292673706163653b3d2673706163653b25354374657874757025374245253744282535436861742537422535436d75253744292673706163653b2d2673706163653b2535436d75) (Casella & Berger, 2002, p. 330) Si [![img](https://camo.githubusercontent.com/e5e04116142d61c833f0e7b6448aaf64d482b730db11cb20b4661a866906ec93/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f6769662e6c617465783f253543696e6c696e652673706163653b25354374657874757025374242696173253744282535436861742537422535436d75253744292673706163653b3d2673706163653b25354374657874757025374245253744282535436861742537422535436d75253744292673706163653b2d2673706163653b2535436d753d30)](https://camo.githubusercontent.com/e5e04116142d61c833f0e7b6448aaf64d482b730db11cb20b4661a866906ec93/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f6769662e6c617465783f253543696e6c696e652673706163653b25354374657874757025374242696173253744282535436861742537422535436d75253744292673706163653b3d2673706163653b25354374657874757025374245253744282535436861742537422535436d75253744292673706163653b2d2673706163653b2535436d753d30), entonces se considera que el estimador es insesgado. Tenga en cuenta que debido a que una estimación es un número, no tiene varianza ni sesgo y, por lo tanto, no puede ser insesgado.

La otra propiedad importante de un estimador es la varianza. La definición formal de la varianza proporciona “una medida del grado de extensión de una distribución alrededor de su media” (Casella y Berger, 2002, p. 59). Esta definición no es muy útil en nuestro contexto, en cambio, nos preocupan las situaciones en las que hemos muestreado un área de estudio para estimar un determinado parámetro de población (por ejemplo, el área de bosque o deforestación). Por ejemplo, si tenemos una población de la que se ha seleccionado una muestra de, la varianza de la muestra es *s^2^* y se calcula fácilmente para diseños de muestreo comunes. Pero la varianza de la muestra es menos interesante en comparación con la varianza de un estimador. Para diseños comunes, podemos probar fácilmente que la varianza muestral *s^2^* es un estimador insesgado de la varianza poblacional *S^2^* (Cochran, 1977, p. 22, 26). La varianza de un estimador *u^* es [![img](https://camo.githubusercontent.com/06f72d13b4ac52188eccb8cdf11aff5dd0eb293b7f548eb136c12607cb5e4fc5/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f6769662e6c617465783f253543696e6c696e652673706163653b25354374657874757025374256253744282535436861742537422535436d75253744292673706163653b3d2673706163653b53253545322673706163653b2535436469762673706163653b6e)](https://camo.githubusercontent.com/06f72d13b4ac52188eccb8cdf11aff5dd0eb293b7f548eb136c12607cb5e4fc5/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f6769662e6c617465783f253543696e6c696e652673706163653b25354374657874757025374256253744282535436861742537422535436d75253744292673706163653b3d2673706163653b53253545322673706163653b2535436469762673706163653b6e) (asumiendo un tamaño de muestra pequeño, *n*, relativo al tamaño de las poblaciones, *N*); la varianza estimada de *u^* sustituye la varianza de la muestra *s^2^* por la varianza de la población *S^2^* para crear el estimador de varianza de *u^* cuando[![img](https://camo.githubusercontent.com/70b5db5d67b6dc02868c46296e02cceea82eb2b361cb9f8c9e791d301a786b5b/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f6769662e6c617465783f253543696e6c696e652673706163653b25354368617425374256253744282535436861742537422535436d75253744292673706163653b3d2673706163653b73253545322673706163653b2535436469762673706163653b6e)](https://camo.githubusercontent.com/70b5db5d67b6dc02868c46296e02cceea82eb2b361cb9f8c9e791d301a786b5b/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f6769662e6c617465783f253543696e6c696e652673706163653b25354368617425374256253744282535436861742537422535436d75253744292673706163653b3d2673706163653b73253545322673706163653b2535436469762673706163653b6e) que es el estimador de varianza de mayor interés para nosotros, ya que nos permite cuantificar la incertidumbre en cosas como los datos de actividad u otros parámetros de interés.

A partir de aquí, podemos introducir dos medidas de propagación más importantes: el error estándar y el intervalo de confianza. El error estándar es la desviación estándar (es decir, raíz cuadrada de la varianza) de un estimador (Rice, 1995, p. 192) y por lo tanto tiene la misma unidad que la estimación. La desviación estándar de un estimador se conoce como su error estándar. Debido a que la varianza muestral es un estimador insesgado de la varianza poblacional, podemos estimar el error estándar usando la varianza muestral: [![img](https://camo.githubusercontent.com/0427c01f6a33aeee4b7a31db2a96dba1c23729b4939ed280ad82842e59e6bdfd/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f6769662e6c617465783f253543696e6c696e652673706163653b2535437465787475702537425345253744282535436861742537422535436d75253744292673706163653b3d2673706163653b25354368617425374256253744282535436861742537422535436d75253744292673706163653b2535436469762673706163653b253543737172742537426e253744)](https://camo.githubusercontent.com/0427c01f6a33aeee4b7a31db2a96dba1c23729b4939ed280ad82842e59e6bdfd/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f6769662e6c617465783f253543696e6c696e652673706163653b2535437465787475702537425345253744282535436861742537422535436d75253744292673706163653b3d2673706163653b25354368617425374256253744282535436861742537422535436d75253744292673706163653b2535436469762673706163653b253543737172742537426e253744). Tenga en cuenta que debido a que un error estándar es una desviación estándar de un estimador, todos los errores estándar también son desviaciones estándar, pero no todas las desviaciones estándar son errores estándar. Esto a veces causa confusión a pesar de que las definiciones de error estándar y desviación estándar son consistentes. Normalmente, ni la varianza ni el error estándar se utilizan para expresar la incertidumbre en las estimaciones; en cambio, se suele utilizar un intervalo de confianza: "Un intervalo de confianza del 95% para *μ* es un intervalo aleatorio que contiene *μ* con probabilidad de 0,95; si tomáramos muchas muestras aleatorias [bajo el mismo diseño de muestreo] y formáramos un intervalo de confianza de cada una, aproximadamente el 95% de estos intervalos contendrían *μ* " (Rice, 1995, p. 217). Intervalos de confianza frecuentemente están en la forma [![img](https://camo.githubusercontent.com/4524fcedf9dec9bd0a4882b9f787f1cd11ad363239b7a5b8a41e95135a65f3cf/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f6769662e6c617465783f253543696e6c696e652673706163653b2535436861742537422535436d752537442673706163653b253543706d2673706163653b6125354374696d65732535437465787475702537425345253744282535436861742537422535436d7525374429)](https://camo.githubusercontent.com/4524fcedf9dec9bd0a4882b9f787f1cd11ad363239b7a5b8a41e95135a65f3cf/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f6769662e6c617465783f253543696e6c696e652673706163653b2535436861742537422535436d752537442673706163653b253543706d2673706163653b6125354374696d65732535437465787475702537425345253744282535436861742537422535436d7525374429) donde *a* es una estadística relacionada con el nivel de confianza deseado, denominado puntuación z (z-score) o puntuación estándar expresada como un porcentaje entre 0 y 100%. Para un cierto nivel de confianza *p*, el área bajo la función de densidad normal estándar de *-z* a *+ z* es *p* (Rice, 1995, p. 202); por ejemplo, un intervalo de confianza en el nivel de confianza del 95% corresponde a una puntuación z de 1.96 (a menudo se redondea a 2). Una condición para utilizar una puntuación z para calcular un intervalo de confianza es que la distribución muestral sea aproximadamente una distribución normal, lo que podemos suponer para tamaños de muestra grandes. El intervalo de confianza dividido por la estimación se denomina margen de error (*MoE*) y, a menudo, se expresa como porcentaje.

Las dos propiedades, sesgo y varianza, son importantes porque podemos asegurarnos de que el estimador que utilizamos sea insesgado y podemos expresar la incertidumbre en estimaciones. Tampoco es posible cuando se utiliza el recuento de píxeles en mapas o cuando se toman muestras sin adherirse al muestreo probabilístico. Otro aspecto importante de un estimador es que es una función de la muestra, lo que significa que el estimador debe corresponder al diseño muestral. Por ejemplo, la media muestral es un estimador insesgado de la media poblacional para muestreo aleatorio simple; para el muestreo aleatorio estratificado, necesitamos utilizar un estimador estratificado que se expresa como la suma de las medias de las muestras aleatorias simples dentro de los estratos ponderados por los pesos de estrato.

## 2 Objetivos de aprendizaje

- Construir el estimador SRS/SYS y el estimador de varianza SRS/SYS
- Estimar la precisión general del productor del usuario de un mapa utilizando observaciones de referencia
- Estimar la precisión del mapa y la estimación del área.

### 2.1 Prerrequisitos

- La terminología relevante se encuentra al final de este documento.
- Puede encontrar más información sobre el diseño de muestreo y el diseño de respuesta aquí en OpenMRV en los procesos "Diseño de muestreo" y "Recopilación de datos de muestra".

## 3 Tutorial: Análisis de datos de muestra recopilados bajo SRS/SYS

### 3.1 Construcción de estimadores de SRS

Los resultados de la muestra recopilados con muestreo aleatorio simple son los más sencillos de analizar (se utilizan los mismos estimadores tanto para el muestreo aleatorio simple como para el sistemático). Debido a que no se utilizan mapas/estratificaciones y debido a que la media de la muestra es un estimador insesgado de la media de la población, el análisis de los resultados de la muestra de SRS/SYS se puede completar fácilmente en una hoja de cálculo. El muestreo aleatorio estratificado se ilustró en tutoriales anteriores, y aquí solo se proporcionan datos ficticios para ilustrar la construcción de estimadores SRS/SYS. Supongamos que los datos de esta hoja de cálculo son mapas y etiquetas de referencia en ubicaciones seleccionadas en SRS: https://drive.google.com/file/d/19MnbicvFpf-D5-if_Dry4MgHJyLAP-3U/view?usp=sharing El tamaño de la muestra es *n* = 100, y una etiqueta de 1 es perturbación del bosque, 2 es bosque, y 3 es no bosque.

Debido a que la media muestral es un estimador insesgado de la media poblacional, el cálculo de las proporciones del área es sencillo; defina *y_i* = 1 si se observó alteración del bosque en la ubicación de la muestra *i* y 0 en caso contrario; el área de perturbación del bosque viene dada por (Cochran, 1977, p. 22):

[![img](https://camo.githubusercontent.com/9526e607fa79beca79b6ebbbe348e578036eeddf4a888c049b87b895c7140593/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f2535434c617267652673706163653b253543686174253742792537443d25354366726163253742312537442537426e25374425354373756d5f253742693d312537442535452537426e253744795f69)](https://camo.githubusercontent.com/9526e607fa79beca79b6ebbbe348e578036eeddf4a888c049b87b895c7140593/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f2535434c617267652673706163653b253543686174253742792537443d25354366726163253742312537442537426e25374425354373756d5f253742693d312537442535452537426e253744795f69)

En la hoja de calculo, escriba en la célula C1 "y_i" y en C2 "=if(B2=1,1,0)" y extiéndalo a la célula C101. Debería de ver:

|      | A    | B    | C    | D    | E    |
| ---- | ---- | ---- | ---- | ---- | ---- |
| 1    | Mapa | Ref. | y_i  |      |      |
| 2    | 2    | 2    | 0    |      |      |
| 3    | 2    | 2    | 0    |      |      |
| 4    | 1    | 1    | 1    |      |      |
| 5    | 2    | 2    | 0    |      |      |

En célula D1, escriba *Area dist. bosque*, y en D2 "=sum(B2:B101)/100" para construir un estimador SRS y aplicarlo a los resultados de muestra. Debería de ver:

|      | A    | B    | C    | D               | E    |
| ---- | ---- | ---- | ---- | --------------- | ---- |
| 1    | Map  | Ref. | y_i  | Area para dist. |      |
| 2    | 2    | 2    | 0    | 0.14            |      |
| 3    | 2    | 2    | 0    |                 |      |
| 4    | 1    | 1    | 1    |                 |      |
| 5    | 2    | 2    | 0    |                 |      |

Ahora calculemos el margen de error en el estimado de área. El estimador de varianza SRS es (Cochran, 1977, p. 26)

[![img](https://camo.githubusercontent.com/c148de221fa80e31980ec517a407742cfff0cfbe41df7820357cbe822f64f340/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f2535434c617267652673706163653b253543686174253742562537442825354368617425374279253744293d2535436672616325374273253545322537442537426e2537442673706163653b3d2673706163653b2535436672616325374225354373756d2673706163653b28795f692d2535436261722537427925374429253545322537442537426e286e2d3129253744)](https://camo.githubusercontent.com/c148de221fa80e31980ec517a407742cfff0cfbe41df7820357cbe822f64f340/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f2535434c617267652673706163653b253543686174253742562537442825354368617425374279253744293d2535436672616325374273253545322537442537426e2537442673706163653b3d2673706163653b2535436672616325374225354373756d2673706163653b28795f692d2535436261722537427925374429253545322537442537426e286e2d3129253744)

Para aplicar el estimador de varianza a la hoja de calculo, escriba en célula D3 "Varianza", y en célula D4 "=sum(ArrayFormula((C4:C103-D24)^2))/(100 * 99)" para aplicar el estimador de varianza; debería de regresar 0.001414. Ahora escriba "Error Estándar" en D5, y en D6: "=sqrt(C4)"; escriba "95% CI" en D7 y en D8: "=1.96*D6". Finalmente escriba "Margen de error" en D9 y en D10 "=D8/D2":

|      | A    | B    | C    | D                 | E    |
| ---- | ---- | ---- | ---- | ----------------- | ---- |
| 1    | Mapa | Ref. | y_i  | Área dist. bosque |      |
| 2    | 2    | 2    | 0    | 0.14              |      |
| 3    | 2    | 2    | 0    | Varianza          |      |
| 4    | 1    | 1    | 1    | 0.001414          |      |
| 5    | 2    | 2    | 0    | Error Estándar    |      |
| 6    | 2    | 2    | 0    | 0.0376            |      |
| 7    | 2    | 2    | 0    | 95% CI            |      |
| 8    | 1    | 1    | 1    | 0.0737            |      |
| 9    | 2    | 1    | 1    | Margen de error   |      |
| 10   | 2    | 2    | 0    | 53%               |      |

Ahora hemos estimado el área de perturbación forestal usando una muestra de 100 unidades recolectadas bajo SRS como 0.14 + - 0.074 correspondiente a un margen de error del 53%. Tenga en cuenta que no se utilizó la información del mapa de la columna A.

Por último, calculemos la precisión del mapa, comenzando con la precisión general: escriba "Prec. general". en la celda E1 y en E2 "= CONTAR.SI (A2: A101, B2: B101) / 100": esta expresión contará el número de instancias en las que el mapa y las etiquetas de referencia coinciden y se dividen por el tamaño de la muestra. La precisión general es la proporción total de área correctamente clasificada.

En célula F1 escriba "Prec. Usuario Dist." y en F2 "=countifs(A1:A101,"1",B1:B101,"1")/countif(A1:A101,1)"; la precisión de usuario de la clase de un mapa “es la probabilidad condicional de que un área clasificada como categoría i por el mapa sea clasificada como categoría i por los datos de referencia” (Stehman, 1997, p. 79):

Finalmente, en celula G1 type "Prec. Prod. Dist." y en G2 "=countifs(A1:A101,"1",B1:B101,"1")/countif(B1:B101,1)"; la precisión del productor de una clase de mapas "La probabilidad condicional de que un área clasificada como categoría j por los datos de referencia sea clasificada como categoría j por el mapa" (Stehman, 1997, p. 79).

|      | A    | B    | C    | D               | E          | F                   | G                 |
| ---- | ---- | ---- | ---- | --------------- | ---------- | ------------------- | ----------------- |
| 1    | Mapa | Ref. | y_i  | Area FD         | Prec. gen. | Prec. Usuario Dist. | Prec. Prod. Dist. |
| 2    | 2    | 2    | 0    | 0.14            | 0.65       | 0.80                | 0.86              |
| 3    | 2    | 2    | 0    | Varianza        |            |                     |                   |
| 4    | 1    | 1    | 1    | 0.001414        |            |                     |                   |
| 5    | 2    | 2    | 0    | Error Estándar  |            |                     |                   |
| 6    | 2    | 2    | 0    | 0.0376          |            |                     |                   |
| 7    | 2    | 2    | 0    | 95% CI          |            |                     |                   |
| 8    | 1    | 1    | 1    | 0.0737          |            |                     |                   |
| 9    | 2    | 1    | 1    | Margen de error |            |                     |                   |
| 10   | 2    | 2    | 0    | 53%             |            |                     |                   |



### 3.2 Software para automatizar el análisis de resultados de muestra

#### AREA2

La aplicación AREA2 en Google Earth Engine tiene ecuaciones para todos los estimadores descritos en este tutorial. Note que en AREA2, se le refiere al estimador SRS por su nombre formal, estimador de expansión. AREA2 esta disponible aquí: https://code.earthengine.google.com/?accept_repo=projects/AREA2/public y mas documentación detallada aquí: https://area2.readthedocs.io/

## 4 Preguntas Frecuentes

**¿Son los estimadores anteriores la única opción que tengo cuando trabajo con resultados de muestra recopilados bajo SRS / SYS?**

¡No! Puede estratificar el área de estudio después de seleccionar la muestra, lo que le permitirá utilizar un estimador estratificado, que en este caso se denomina estimador posestratificado. También puede utilizar un estimador de regresión que a menudo funciona bien cuando el mapa y las observaciones de referencia se expresan como proporciones.

**¿El SRS/SYS dará como resultado estimaciones menos precisas en comparación con el muestreo aleatorio estratificado??**

Es difícil decir que un diseño muestral y una familia de estimadores sean más o menos precisos en general, ya que la precisión final dependerá de varios factores. Para lograr la misma precisión que en el diseño estratificado, normalmente necesitaría una muestra más grande en SRS/SYS. Esto es especialmente cierto si los parámetros de interés son pequeñas proporciones del área de estudio.

## 5 Terminología relevante para las técnicas de muestreo

Una lista de términos relevantes para las técnicas de muestreo e inferencia esta provista en la documentación de AREA2: https://area2.readthedocs.io/en/latest/definitions.html. Abajo hay algunos términos adicionales que no están incluidos en la documentación.

### 5.1 Diseño de Respuesta

Definido por Stehman and Czaplewski, 1998: “La referencia o clasificación 'verdadera' se obtiene para cada unidad de muestreo en función de la interpretación de fotografías aéreas o videografías, una visita terrestre o una combinación de estas fuentes. Los métodos utilizados para determinar esta clasificación de referencia se denominan "diseño de respuesta". El diseño de respuesta incluye procedimientos para recopilar información relacionada con la determinación de la cobertura terrestre de referencia y reglas para asignar una o más [etiquetas] de referencia a cada unidad de muestreo ". Conocido como "plan de medición" por Särndal et al. (1992).

### 5.2 Muestra

Un subconjunto de unidades de población seleccionadas de la población.

### 5.3 Diseño de Muestra

Sinónimo de diseño de muestreo, que es el término preferido en la literatura fundamental (Cochran, 1977, Särndal et al., 1992). El término aparece en Rice (1995) que utiliza tanto "diseño de muestreo" como "diseño de muestra".

### 5.4 Diseño de Muestreo

"El diseño de muestreo es el protocolo mediante el cual se seleccionan las unidades de muestra de referencia". (Stehman y Czaplewski, 1998). El “diseño de muestreo” también es utilizado por Cochran (1977) y Särndal et al. (1992) - el primero también usa "plan de muestreo".

### 5.5 Encuesta

Särndal y col. (1992) define una encuesta como una “investigación parcial de una población finita”, y además que “los términos 'encuesta' y 'encuesta por muestreo' se utilizan para denotar investigaciones estadísticas con las siguientes características metodológicas: [...] plan de medición [...] de muestreo probabilístico [y] estimación."

### 5.6 Diseño de Encuesta

Un "diseño total de la encuesta" define los procedimientos para "obtener la posible precisión en las estimaciones de la encuesta mientras se logra un equilibrio entre los errores de muestreo y los no muestrales [...] El diseño de la encuesta da lugar a operaciones de encuesta" como la selección de la muestra (Särndal et al., 1992). Lohr (1999) describe un diseño de encuesta total como "Una filosofía de diseño de encuesta para minimizar los errores de muestreo y de no muestreo". Además, en Lohr (1999) “diseño de encuestas” es sinónimo de diseño de muestreo

### 5.7 Datos de referencia 

Datos que caracterizan la evaluación disponible más precisa de la condición real en la ubicación de la muestra (ejemplo: imágenes de satélite de resolución fina).

### 5.8 Observaciones de referencia

La evaluación disponible más precisa de la verdadera condición de una unidad de población.

### 5.9 Clasificación de referencia 

La clasificación de referencia aplicada a la colección de todas las unidades de muestra.

## 6 Referencias

Cochran, W.G., 1977. *Sampling Techniques*, John Wiley & Sons, New York, NY.

Casella, G., & Berger, R. L., 2002. *Statistical Inference* (2nd ed.), Duxbury Press, Pacific Grove, CA.

Lohr, S.L., 1999. *Sampling: Design And Analysis,* CRC Press.

Rice, J.A., 1995. *Mathematical Statistics and Data Analysis* (2nd ed.), Duxbury Press, Belmont, CA.

Stehman, S.V., 2014. Estimating area and map accuracy for stratified random sampling when the strata are different from the map classes. *International Journal of Remote Sensing*, 35(13), 4923-4939.

-----

![](figures/cc.png)

Esta trabajo tiene licencia bajo un [Creative Commons Attribution 3.0 IGO](https://creativecommons.org/licenses/by/3.0/igo/)

Copyright 2021, World Bank. 

Este trabajo fue desarrollado por Pontus Olofsson bajo contrato del World Bank con GRH Consulting, LLC para el desarrollo de recursos nuevos o existentes relacionadas a la Medida, Reportaje, y Verificación para el apoyo de implementación MRV en varios países.

Material revisado por:   
Ana Mirian Villalobos, El Salvador, Ministry of Environment and Natural Resources  
Carole Andrianirina, Madagascar, National Coordination Bureau REDD+ (BNCCREDD)  
Jennifer Juliana Escamilla Valdez, El Salvador, Ministry of Environment and Natural Resources  
Phoebe Oduor, Kenya, Regional Centre For Mapping Of Resources For Development (RCMRD)  
Tatiana Nana, Cameroon, REDD+ Technical Secretariat

Atribución   
Olofsson, P. 2021. Analysis of sample data collected under simple random and systematic sampling. © World Bank. License: [Creative Commons Attribution license (CC BY 3.0 IGO)](http://creativecommons.org/licenses/by/3.0/igo/)

![](figures/wb_fcfc_gfoi.png)
