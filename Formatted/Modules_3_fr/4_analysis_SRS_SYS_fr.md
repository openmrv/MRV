---
title: Analysis of sample data collected under SRS/SYS
summary: In this tutorial we will apply various estimators to a sample dataset to estimate characteristics of the population sampled -- i.e. characteristics of the study area such as the area of forest disturbance. This tutorial focus on sample data collected under SRS/SYS.
author: Pontus Olofsson
creation date: February, 2021
language: English
publisher and license: Copyright 2021, World Bank. This work is licensed under a Creative Commons Attribution 3.0 IGO

tags:
- OpenMRV
- AREA2
- GEE
- Accuracy
- Accuracy assessment
- Area Estimation
- Colombia

group:
- category: Stratified
  stage: Area Estimation/Accuracy assessment
---



# Analysis of sample data collected under SRS/SYS

## 1 Contexte

Dans les tutoriels précédents, nous avons conçu et réalisé un échantillon pour la Colombie, et nous avons observé et documenté les données de référence de l'occupation du sol à chaque unité d'échantillonnage. La collection d'observations de référence est appelée les résultats ou les données de l'échantillon, ou encore la classification de référence. Dans ce tutoriel, nous appliquerons divers estimateurs aux données de l'échantillon pour estimer les caractéristiques de la population que nous avons échantillonnée, à savoir les caractéristiques telles que la zone de perturbation des forêts. Un estimateur est “ la règle par laquelle une estimation d'une caractéristique de la population [c'est-à-dire un paramètre] *μ* est calculée à partir des résultats de l'échantillon” (Cochran, 1977, p. 11)[^fn1]. Notez qu'un estimateur n'est pas la même chose qu'une estimation - au contraire, “un estimateur est une fonction de l'échantillon, tandis qu'une estimation est la valeur réalisée d'un estimateur (c'est-à-dire un nombre) qui est obtenue lorsqu'un échantillon est effectivement prélevé ” (Casella & Berger, 2002, p. 312)[^fn2]. Un estimateur possède deux propriétés importantes : la variance et le biais. Le biais d'un estimateur *μ^* d'un paramètre de population *μ* est la différence entre *μ* et la valeur attendue de *μ^* sur tous les échantillons possibles ; soit , [![img](https://camo.githubusercontent.com/0a124237fea316e5d657b6f75cfa463307793bdf49738b559fbb5426df5f67a9/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f6769662e6c617465783f253543696e6c696e652673706163653b25354374657874757025374242696173253744282535436861742537422535436d75253744292673706163653b3d2673706163653b25354374657874757025374245253744282535436861742537422535436d75253744292673706163653b2d2673706163653b2535436d75)](https://camo.githubusercontent.com/0a124237fea316e5d657b6f75cfa463307793bdf49738b559fbb5426df5f67a9/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f6769662e6c617465783f253543696e6c696e652673706163653b25354374657874757025374242696173253744282535436861742537422535436d75253744292673706163653b3d2673706163653b25354374657874757025374245253744282535436861742537422535436d75253744292673706163653b2d2673706163653b2535436d75) (Casella & Berger, 2002, p. 330)[^fn2]. Si [![img](https://camo.githubusercontent.com/e5e04116142d61c833f0e7b6448aaf64d482b730db11cb20b4661a866906ec93/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f6769662e6c617465783f253543696e6c696e652673706163653b25354374657874757025374242696173253744282535436861742537422535436d75253744292673706163653b3d2673706163653b25354374657874757025374245253744282535436861742537422535436d75253744292673706163653b2d2673706163653b2535436d753d30)](https://camo.githubusercontent.com/e5e04116142d61c833f0e7b6448aaf64d482b730db11cb20b4661a866906ec93/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f6769662e6c617465783f253543696e6c696e652673706163653b25354374657874757025374242696173253744282535436861742537422535436d75253744292673706163653b3d2673706163653b25354374657874757025374245253744282535436861742537422535436d75253744292673706163653b2d2673706163653b2535436d753d30), alors l'estimateur est dit sans biais. Notez que parce qu'une estimation est un nombre, elle n'a pas de variance ni de biais et ne peut donc pas être sans biais.

L'autre propriété importante d'un estimateur est la variance. La définition formelle de la variance indique “une mesure du degré de dispersion d'une distribution autour de sa moyenne” (Casella & Berger, 2002, p. 59)[^fn2]. Cette définition n'est pas très utile dans notre contexte, nous nous intéressons plutôt aux situations dans lesquelles nous avons échantillonné une zone d'étude pour estimer un certain paramètre de population (par exemple, la superficie de la forêt ou la déforestation). Par exemple, si nous avons une population de dans laquelle un échantillon de a été sélectionné, la variance de l'échantillon est *s^2^* et est facilement calculée pour les plans d'échantillonnage courants. Mais la variance de l'échantillon est moins intéressante que la variance d'un estimateur. Pour les plans d'échantillonnage courants, nous pouvons facilement prouver que la variance de l'échantillon *s^2^* est un estimateur sans biais de la variance de la population *S^2^* (Cochran, 1977, p. 22, 26)[^fn1]. La variance d'un estimateur *u^* [![img](https://camo.githubusercontent.com/06f72d13b4ac52188eccb8cdf11aff5dd0eb293b7f548eb136c12607cb5e4fc5/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f6769662e6c617465783f253543696e6c696e652673706163653b25354374657874757025374256253744282535436861742537422535436d75253744292673706163653b3d2673706163653b53253545322673706163653b2535436469762673706163653b6e)](https://camo.githubusercontent.com/06f72d13b4ac52188eccb8cdf11aff5dd0eb293b7f548eb136c12607cb5e4fc5/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f6769662e6c617465783f253543696e6c696e652673706163653b25354374657874757025374256253744282535436861742537422535436d75253744292673706163653b3d2673706163653b53253545322673706163653b2535436469762673706163653b6e) (en supposant une petite taille d'échantillon, *n*, par rapport à la taille de la population, *N*)); la variance estimée de *u^* substitue la variance de l'échantillon *s^2^* à la variance de la population *S^2^* pour créer l'estimateur de variance de *u^* comme [![img](https://camo.githubusercontent.com/70b5db5d67b6dc02868c46296e02cceea82eb2b361cb9f8c9e791d301a786b5b/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f6769662e6c617465783f253543696e6c696e652673706163653b25354368617425374256253744282535436861742537422535436d75253744292673706163653b3d2673706163653b73253545322673706163653b2535436469762673706163653b6e)](https://camo.githubusercontent.com/70b5db5d67b6dc02868c46296e02cceea82eb2b361cb9f8c9e791d301a786b5b/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f6769662e6c617465783f253543696e6c696e652673706163653b25354368617425374256253744282535436861742537422535436d75253744292673706163653b3d2673706163653b73253545322673706163653b2535436469762673706163653b6e) qui est l'estimateur de variance qui nous intéresse le plus car il nous permet de quantifier l'incertitude dans des choses comme les données d'activité ou d'autres paramètres importants.

A partir de là, nous pouvons introduire deux mesures plus importantes de la dispersion : l'erreur standard et l'intervalle de confiance. L'erreur standard est l'écart type (c'est-à-dire la racine carrée de la variance) d'un estimateur (Rice, 1995, p. 192)[^fn3] et a donc la même unité que l'estimation. L'écart-type d'un estimateur est appelé son erreur-type. Comme la variance de l'échantillon est un estimateur sans biais de la variance de la population, nous pouvons estimer l'erreur standard à l'aide de la variance de l'échantillon : [![img](https://camo.githubusercontent.com/0427c01f6a33aeee4b7a31db2a96dba1c23729b4939ed280ad82842e59e6bdfd/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f6769662e6c617465783f253543696e6c696e652673706163653b2535437465787475702537425345253744282535436861742537422535436d75253744292673706163653b3d2673706163653b25354368617425374256253744282535436861742537422535436d75253744292673706163653b2535436469762673706163653b253543737172742537426e253744)](https://camo.githubusercontent.com/0427c01f6a33aeee4b7a31db2a96dba1c23729b4939ed280ad82842e59e6bdfd/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f6769662e6c617465783f253543696e6c696e652673706163653b2535437465787475702537425345253744282535436861742537422535436d75253744292673706163653b3d2673706163653b25354368617425374256253744282535436861742537422535436d75253744292673706163653b2535436469762673706163653b253543737172742537426e253744). Notez que, comme une erreur standard est un écart type d'un estimateur, toutes les erreurs standard sont également des écarts types, mais tous les écarts types ne sont pas des erreurs standard. Cela prête parfois à confusion, même si les définitions de l'erreur standard et de l'écart standard sont cohérentes. Ni la variance ni l'erreur standard ne sont généralement utilisées pour exprimer l'incertitude des estimations, à la place, un intervalle de confiance est couramment utilisé : " Un intervalle de confiance de 95 % pour *μ* est un intervalle aléatoire qui contient *μ* avec une probabilité de 0,95 ; si nous devions prendre de nombreux échantillons aléatoires [selon le même plan d'échantillonnage] et former un intervalle de confiance à partir de chacun d'eux, environ 95 % de ces intervalles contiendraient *μ*." (Rice, 1995, p. 217)[^fn3]. Les intervalles de confiance sont souvent de la forme [![img](https://camo.githubusercontent.com/4524fcedf9dec9bd0a4882b9f787f1cd11ad363239b7a5b8a41e95135a65f3cf/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f6769662e6c617465783f253543696e6c696e652673706163653b2535436861742537422535436d752537442673706163653b253543706d2673706163653b6125354374696d65732535437465787475702537425345253744282535436861742537422535436d7525374429)](https://camo.githubusercontent.com/4524fcedf9dec9bd0a4882b9f787f1cd11ad363239b7a5b8a41e95135a65f3cf/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f6769662e6c617465783f253543696e6c696e652673706163653b2535436861742537422535436d752537442673706163653b253543706d2673706163653b6125354374696d65732535437465787475702537425345253744282535436861742537422535436d7525374429) où *a* est une statistique liée au niveau de confiance souhaité, appelée score z ou score standard, exprimée en pourcentage entre 0 et 100 %. Pour un certain niveau de confiance *p*, l'aire sous la fonction de densité normale standard de *-z* à *+z* est *p* (Rice, 1995, p. 202)[^fn3]; par exemple, un intervalle de confiance au niveau de confiance de 95% correspond à un z-score de 1,96 (souvent arrondi à 2). Une condition pour utiliser un z-score pour calculer un intervalle de confiance est que la distribution de l'échantillonnage soit approximativement une distribution normale, ce que l'on peut supposer pour des échantillons de grande taille. L'intervalle de confiance divisé par l'estimation est appelé marge d'erreur (*MdE*) et est souvent exprimé en pourcentage.

Les deux propriétés, biais et variance, sont importantes car nous pouvons nous assurer que l'estimateur que nous utilisons est sans biais et nous pouvons exprimer l'incertitude des estimations. Ni l'un ni l'autre n'est possible lorsqu'on utilise le comptage de pixels dans les cartes ou lorsqu'on procède à un échantillonnage sans appliquer le principe de l'échantillonnage probabiliste. Un autre aspect important d'un estimateur est qu'il est une fonction de l'échantillon, ce qui signifie que l'estimateur doit correspondre au plan d'échantillonnage. Par exemple, la moyenne de l'échantillon est un estimateur sans biais de la moyenne de la population pour un échantillonnage aléatoire simple ; pour un échantillonnage aléatoire stratifié, nous devons utiliser un estimateur stratifié qui est exprimé comme la somme des moyennes des échantillons aléatoires simples dans les strates pondérées par les poids des strates.

## 2 Learning Objectives

- Construct SRS/SYS estimator and SRS/SYS variance estimator
- Estimate overall user’s producer’s accuracy of a map using reference observations
- Estimate map accuracy and area estimation

### 2.1 Pre-requisites for this module

- Relevant terminology is found at the end of this document
- More information about sampling design, and response design can be found here on OpenMRV under processes "Sampling design", and "Sample data collection".



## 3 Tutorial: Analysis of sample data collected under SRS/SYS

### 3.1 Construction of SRS estimators

Les résultats des échantillons collectés par échantillonnage aléatoire simple sont les plus simples à analyser (les mêmes estimateurs sont utilisés pour l'échantillonnage aléatoire simple et systématique). Étant donné qu'aucune carte/stratification n'est utilisée et que la moyenne de l'échantillon est un estimateur non biaisé de la moyenne de la population, l'analyse des résultats des échantillons SRS/SYS peut facilement être réalisée dans une feuille de calcul. L'échantillonnage aléatoire stratifié a été illustré dans les tutoriels précédents, et seules des données fictives sont fournies ici pour illustrer la construction des estimateurs SRS/SYS. Supposons que les données de cette feuille de calcul soient des cartes et des labels de référence à des emplacements sélectionnés dans le cadre du SRS :[Lien](https://docs.google.com/spreadsheets/d/1pcK-rlhUo5lvmYqibT4zIv-bR5tF4Uu8DqPwIG8mJWQ/edit?usp=sharing) .La taille de l'échantillon est *n* = 100 et la classe 1 correspond à une perturbation de la forêt, 2 à une forêt et 3 à une zone non forestière.

Comme la moyenne de l'échantillon est un estimateur sans biais de la moyenne de la population, le calcul des proportions de surface est simple ; on définit *y_i* = 1 si une perturbation de forêt a été observée à l'emplacement de l'échantillon *i* et 0 sinon ; la valeur de la perturbation de forêt est donnée par (Cochran, 1977, p. 22)[^fn1]:

[![img](https://camo.githubusercontent.com/9526e607fa79beca79b6ebbbe348e578036eeddf4a888c049b87b895c7140593/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f2535434c617267652673706163653b253543686174253742792537443d25354366726163253742312537442537426e25374425354373756d5f253742693d312537442535452537426e253744795f69)](https://camo.githubusercontent.com/9526e607fa79beca79b6ebbbe348e578036eeddf4a888c049b87b895c7140593/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f2535434c617267652673706163653b253543686174253742792537443d25354366726163253742312537442537426e25374425354373756d5f253742693d312537442535452537426e253744795f69)

Dans le tableur, tapez dans la cellule C1 "y_i" et dans C2 "=if(B2=1,1,0)" et étendez à la cellule C101. Vous devriez voir :

|      | A    | B    | C    | D    | E    |
| ---- | ---- | ---- | ---- | ---- | ---- |
| 1    | Map  | Ref. | y_i  |      |      |
| 2    | 2    | 2    | 0    |      |      |
| 3    | 2    | 2    | 0    |      |      |
| 4    | 1    | 1    | 1    |      |      |
| 5    | 2    | 2    | 0    |      |      |

Dans la cellule D1, tapez *Area for. dist.*, et dans D2 "=sum(B2:B101)/100" pour construire un estimateur SRS et l'appliquer aux résultats de l'échantillon. Vous devriez voir :

|      | A    | B    | C    | D       | E    |
| ---- | ---- | ---- | ---- | ------- | ---- |
| 1    | Map  | Ref. | y_i  | Area FD |      |
| 2    | 2    | 2    | 0    | 0.14    |      |
| 3    | 2    | 2    | 0    |         |      |
| 4    | 1    | 1    | 1    |         |      |
| 5    | 2    | 2    | 0    |         |      |

Calculons maintenant la marge d'erreur de l'estimation de la surface. L'estimateur de variance SRS est (Cochran, 1977, p. 26)[^fn1]

[![img](https://camo.githubusercontent.com/c148de221fa80e31980ec517a407742cfff0cfbe41df7820357cbe822f64f340/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f2535434c617267652673706163653b253543686174253742562537442825354368617425374279253744293d2535436672616325374273253545322537442537426e2537442673706163653b3d2673706163653b2535436672616325374225354373756d2673706163653b28795f692d2535436261722537427925374429253545322537442537426e286e2d3129253744)](https://camo.githubusercontent.com/c148de221fa80e31980ec517a407742cfff0cfbe41df7820357cbe822f64f340/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f2535434c617267652673706163653b253543686174253742562537442825354368617425374279253744293d2535436672616325374273253545322537442537426e2537442673706163653b3d2673706163653b2535436672616325374225354373756d2673706163653b28795f692d2535436261722537427925374429253545322537442537426e286e2d3129253744)

Pour appliquer l'estimateur de variance dans le tableur, tapez dans la cellule D3 "Variance", et dans la cellule D4 "=sum(ArrayFormula((C4:C103-D24)^2))/(100 * 99)" pour appliquer l'estimateur de variance ; il devrait donner 0.001414. Tapez maintenant "Standard error" en D5, et en D6: "=sqrt(C4)"; typez "95% CI" en D7 et en D8: "=1.96*D6". Enfin tapez "Margin of error" en D9 et en D10 et "=D8/D2":

|      | A    | B    | C    | D               | E    |
| ---- | ---- | ---- | ---- | --------------- | ---- |
| 1    | Map  | Ref. | y_i  | Area FD         |      |
| 2    | 2    | 2    | 0    | 0.14            |      |
| 3    | 2    | 2    | 0    | Variance        |      |
| 4    | 1    | 1    | 1    | 0.001414        |      |
| 5    | 2    | 2    | 0    | Standard error  |      |
| 6    | 2    | 2    | 0    | 0.0376          |      |
| 7    | 2    | 2    | 0    | 95% CI          |      |
| 8    | 1    | 1    | 1    | 0.0737          |      |
| 9    | 2    | 1    | 1    | Margin of error |      |
| 10   | 2    | 2    | 0    | 53%             |      |

Nous avons maintenant estimé la zone de perturbation forestière à l'aide d'un échantillon de 100 unités collectées dans le cadre du SRS à 0,14 +- 0,074, ce qui correspond à une marge d'erreur de 53 %. Notez que les informations cartographiques de la colonne A n'ont pas été utilisées.

Enfin, calculons la précision de la carte, en commençant par la précision globale : tapez "Overall acc." dans la cellule E1, et dans E2 "=COUNTIF(A2:A101,B2:B101)/100" -- cette expression comptera le nombre de cas où la carte et les étiquettes de référence concordent et divisera par la taille de l'échantillon. La précision globale est la proportion globale de la zone correctement classée.

Dans la cellule F1, tapez "User's acc. FD" et dans F2 "=countifs(A1:A101, "1",B1:B101, "1")/countif(A1:A101,1)" ; la précision de l'utilisateur de la classe de la carte “est la probabilité conditionnelle qu'une zone classée comme catégorie i par la carte soit classée comme catégorie i par les données de référence” (Stehman, 1997, p. 79):

Enfin, dans la cellule G1, tapez "Prod. acc. FD" et dans G2 "=countifs(A1:A101, "1",B1:B101, "1")/countif(B1:B101,1)" ; la précision de la classe de la carte est “tla probabilité conditionnelle qu'une zone classée comme catégorie j par les données de référence soit classée comme catégorie j par la carte ” (Stehman, 1997, p. 79).

|      | A    | B    | C    | D               | E            | F              | G             |
| ---- | ---- | ---- | ---- | --------------- | ------------ | -------------- | ------------- |
| 1    | Map  | Ref. | y_i  | Area FD         | Overall acc. | User's acc. FD | Prod. acc. FD |
| 2    | 2    | 2    | 0    | 0.14            | 0.65         | 0.80           | 0.86          |
| 3    | 2    | 2    | 0    | Variance        |              |                |               |
| 4    | 1    | 1    | 1    | 0.001414        |              |                |               |
| 5    | 2    | 2    | 0    | Standard error  |              |                |               |
| 6    | 2    | 2    | 0    | 0.0376          |              |                |               |
| 7    | 2    | 2    | 0    | 95% CI          |              |                |               |
| 8    | 1    | 1    | 1    | 0.0737          |              |                |               |
| 9    | 2    | 1    | 1    | Margin of error |              |                |               |
| 10   | 2    | 2    | 0    | 53%             |              |                |               |



### 3.2  Logiciel pour automatiser l'analyse des résultats des échantillons

#### AREA2

L'application AREA2 de Google Earth Engine contient les équations de tous les estimateurs décrits dans ce tutoriel. Notez que dans AREA2, l'estimateur SRS est désigné par son nom officiel, l'estimateur d'expansion. AREA2 est disponible ici : [Lien application AREA2](https://code.earthengine.google.com/?accept_repo=projects/AREA2/public) et une documentation plus détaillée ici :[Lien documentation plus approfondie](https://area2.readthedocs.io/)

## 4 Frequently Asked Questions (FAQs)

**Are the estimators above the only option I have when working with sample results collected under SRS/SYS?**

No! You can stratify the study area after selection of the sample which will allow you to use a stratified estimator, which in this case is then referred to as a post-stratified estimator. You can also use a regression estimator which often works well when the map and reference observations are expressed as proportions.

**Will SRS/SYS result in less precise estimates compared to stratified random sampling?**

It is hard to say that one sampling design and family of estimators are more or less precise in general, as the final precision will depend on several factors. To achieve the same precision as in stratified design, you would typically need a larger sample under SRS/SYS. This is especially true if the parameters of interest are small proportions of the study area.

## 5 Terminologie relative aux techniques d'échantillonnage

Une liste de termes relatifs aux techniques d'échantillonnage et d'inférence est fournie dans la documentation d'AREA2 : https://area2.readthedocs.io/en/latest/definitions.html Vous trouverez ci-dessous quelques termes supplémentaires qui ne figurent pas dans la documentation d'AREA2.

### 5.1 Plan de réponse

Défini par (Stehman and Czaplewski, 1998)[^fn1]: “La référence ou classe réelle est obtenue pour chaque unité d'échantillonnage sur la base de l'interprétation de photographies aériennes ou de vidéographies, d'une observation au sol ou d'une combinaison de ces sources. Les méthodes utilisées pour déterminer cette référence de classification sont appelées "plan de réponse". Le plan d'intervention comprend les procédures de collecte des informations relatives à la détermination de la occupation du sol de référence, et les règles d'attribution d'une ou plusieurs [labels] de référence à chaque unité d'échantillonnage.” Connu sous le nom de “plan de mesure” par Särndal et al. (1992)[^fn2].

### 5.2 Echantillon

Un sous-ensemble de la population sélectionné parmi les unités de la population.

### 5.3 Plan d'échantillonnage

Synonyme de plan d'échantillonnage (Sampling Design), qui est le terme préféré dans la littérature de référence (Cochran, 1977[^fn3], Särndal et al., 1992[^fn2]). Le terme apparaît chez Rice (1995)[^fn4] ui utilise à la fois “sampling design, ***plan d'echantillonnage\***” et “sample design, ***plan d'echantillon\***”.

### 5.4 Plan d'échantillonnage

“Le concept de plan d'échantillonnage (sampling design ) est le protocole par lequel les unités de référence de l'échantillon sont sélectionnées” (Stehman and Czaplewski, 1998)[^fn1]. Le terme “Sampling design” est également utilisé par Cochran (1977)[^fn3] and Särndal et al. (1992)[^fn2] -- Le premier utilise également “sampling plan”.

### 5.5 Sondage/Enquêtee

Särndal et al. (1992)[^fn2] définissent une enquête comme une “investigation partielle d'une population finie”, et précisent que “les concepts d ‘enquête’ et ‘enquête par sondage’ sont utilisés pour désigner des enquêtes statistiques présentant les caractéristiques méthodologiques suivantes: [...] échantillonnage aléatoire [...] plan de mesure [et] estimation”. de facon plus precise une enquete par sondage ou un sondage est une enquête effectuee sur une partie de la population. Cette fraction de la population constitue l'échantillon et les méthodes qui permettent de construire cet echantillon s'appellent méthode d'échantillonnage.

### 5.6 Plan d'enquête

UN “plan de sondage total” définit les procédures pour “obtenir la plus grande précision possible dans les estimations de l'enquête tout en trouvant un équilibre entre les erreurs d'échantillonnage et les erreurs non dues à l'échantillonnage [...] Le plan de sondage donne lieu à des opérations d'enquête” sélection de l'échantillon (Särndal et al., 1992)[^fn2]. Lohr (1999)[^fn5] décrit un plan de sondage total comme “Une philosophie de conception d'enquête visant à minimiser les erreurs de non-échantillonnage ainsi que les erreurs d'échantillonnage..” De plus, dans Lohr (1999) “plan d'enquête” est synonyme de plan d'échantillonnage.

### 5.7 Données de référence

Données caractérisant l'évaluation la plus précise possible de la condition réelle à l'emplacement de l'échantillon (exemple : imagerie satellite à haute résolution).

### 5.8 Les observations de référence 

L'évaluation la plus exacte possible de l'état réel d'une unité de population.

### 5.9 Reference classification 

La classification de référence appliquée à la collection de toutes les unités d'échantillonnage.

## 6 References

Cochran, W.G., 1977. *Sampling Techniques*, John Wiley & Sons, New York, NY.

Casella, G., & Berger, R. L., 2002. *Statistical Inference* (2nd ed.), Duxbury Press, Pacific Grove, CA.

Lohr, S.L., 1999. *Sampling: Design And Analysis,* CRC Press.

Rice, J.A., 1995. *Mathematical Statistics and Data Analysis* (2nd ed.), Duxbury Press, Belmont, CA.

Stehman, S.V., 2014. Estimating area and map accuracy for stratified random sampling when the strata are different from the map classes. *International Journal of Remote Sensing*, 35(13), 4923-4939.

-----

![](./figures/cc.png)

Cet ouvrage est soumis à une licence [Creative Commons Attribution 3.0 IGO](https://creativecommons.org/licenses/by/3.0/igo/)

Copyright 2020, Banque mondiale. Ce travail a été développé par Pontus Olofsson dans le cadre d'un contrat de la Banque mondiale avec GRH Consulting, LLC pour le développement de nouvelles ressources - et la collecte de ressources existantes - liées à la mesure, la notification et la vérification pour soutenir la mise en œuvre du MRV par les pays.



Matériel révisé par : 

Ana Mirian Villalobos, El Salvador, Ministry of Environment and Natural Resources
Carole Andrianirina, Madagascar, National Coordination Bureau REDD+ (BNCCREDD)
Jennifer Juliana Escamilla Valdez, El Salvador, Ministry of Environment and Natural Resources
Phoebe Oduor, Kenya, Regional Centre For Mapping Of Resources For Development (RCMRD)
Tatiana Nana, Cameroon, REDD+ Technical Secretariat

Attribution : Olofsson, P. (2021). *MRV ouvert : Analyse d'un échantillon de données*. Banque mondiale. Licence :  [Creative Commons Attribution license (CC BY 3.0 IGO)](http://creativecommons.org/licenses/by/3.0/igo/)

![](./figures/wb_fcfc_gfoi.png)
