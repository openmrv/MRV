---
title: Sample selection using AREA2
summary: In sampling design methods for estimation of area and map accuracy, we design a sample by choosing a selection protocol and determining the sample size and allocation. In this tutorial we will physically draw from a study area a sample that was designed based on tutorials here on OpenMRV under process "Sampling design". Here, we illustrate how to draw a sample in AREA2. For more information about AREA2 please refer to https://area2.readthedocs.io/en/latest/
author: Pontus Olofsson
creation date: February, 2021
language: English
publisher and license: Copyright 2021, World Bank. This work is licensed under a Creative Commons Attribution 3.0 IGO

tags:
- OpenMRV
- Landsat
- Sentinel 2
- GEE
- AREA2
- Cloud cover
- Optical sensors
- Remote sensing
- Composite
- Mosaic
- Time series
- Sampling design
- Sample design
- Sample selection
- Sample
- Sampling frame
- Stratified
- Simple Random
- Systematic
- Response design
- Survey
- Survey design
- Accuracy
- Accuracy assessment
- Area Estimation
- Reference data
- Reference classification
- Reference observations
- Colombia

group:
- category: Stratified
  stage: Sampling
- category: Simple Random
  stage: Sampling
- category: Cluster
  stage: Sampling
- category: Systematic
  stage: Sampling
- category: Stratified
  stage: Area Estimation/Accuracy assessment
- category: Expansion
  stage: Area Estimation/Accuracy assessment
- category: Model-assisted
  stage: Area Estimation/Accuracy assessment
- category: Ratio
  stage: Area Estimation/Accuracy assessment
---

# Sample selection using AREA2

## 1 Contexte

Dans le tutoriel précédent, nous avons conçu un échantillon en choisissant un protocole de sélection et en déterminant la taille de l'échantillon et la répartition. Dans ce tutoriel, nous allons physiquement prélever dans une zone d'étude l'échantillon que nous avons conçu. Le tirage d'un échantillon implique la création d'une *cadre d'échantillonnage* qui est une liste d'unités de population pouvant être sélectionnées pour être incluses dans un échantillon. Les unités de population de la liste sont appelées unités d'échantillonnage. En d'autres termes, une base de sondage est un dispositif qui permet d'observer la population en associant les unités de population aux unités d'échantillonnage (Särndal et al., 1992, p. 9)[^fn1]. Dans notre cas, la base de sondage est par exemple une liste de tous les pixels qui composent la zone d'étude. Nous pourrions donc simplement exporter une liste de tous les pixels de la carte avec des identifiants uniques à partir desquels nous sélectionnons aléatoirement *n* unités. Dans le cadre d'un échantillonnage aléatoire stratifié, chaque pixel aurait, en plus de l'identifiant, un code de strate de sorte qu'un échantillon aléatoire soit sélectionné dans chaque strate. Une telle approche peut facilement devenir impraticable car le nombre d'unités de population tend à être important. Au lieu de cela, la sélection d'échantillons est prise en charge par divers outils et logiciels ; ici, nous illustrons comment dessiner un échantillon dans QGIS, Google Earth Engine/AREA2, et un script R.

## 2 Objectifs d'apprentissage

- Upon completion of the tutorial, the user should be able to sample an arbitrary study area under stratified random sampling (STR) using AREA2.
  - Draw a sample in GEE/AREA2 under STR

### 2.1 Prérequis pour ce module

- Relevant terminology for sampling techniques can be found at the end of this document

## 3 Tutorial: Sample selection using AREA2

### 3.1 Echantillonnage aléatoire stratifié dans Google Earth Engine/AREA2

Dans le script du plan d'échantillonnage, nous avons estimé la taille de l'échantillon nécessaire pour atteindre une marge d'erreur de 25% de l'estimation de la zone de perturbation de la forêt, et nous avons réparti l'échantillon en strates aux fins de l'estimation de la zone. Cela a donné la taille d'échantillon suivante :

|      | A             | B         | C             | D              | E           | F     |
| ---- | ------------- | --------- | ------------- | -------------- | ----------- | ----- |
| 1    | Stratum (*h*) | Forêt (1) | Non-Forêt (2) | For. Dist. (3) | FD buf. (4) | Total |
| 11   | *nh* (final)  | 275       | 200           | 30             | 30          | 535   |

Pour sélectionner cet échantillon, utilisons AREA2 pour sélectionner un échantillon sous échantillonnage aléatoire stratifié : [https://code.earthengine.google.com/?accept_repo=users%2Fopenmrv%2FMRV&scriptPath=projects%2FAREA2%2Fpublic%3A1.%20Sampling%20Design%2FStratified%20Random%20Sampling](https://code.earthengine.google.com/?accept_repo=users%2Fopenmrv%2FMRV&scriptPath=projects%2FAREA2%2Fpublic%3A1. Sampling Design%2FStratified Random Sampling) et spécifions le chemin d'accès à la carte de la Colombie basée sur le CODED (https://code.earthengine.google.com/?asset=users/olofsson76/Open_MRV/Open_MRV_Col_strat_buffer) avec un tampon sous "Spécifier la stratification/l'image pour définir la zone d'étude" ; utilisez les autres arguments par défaut ; cliquez sur "Charger l'image", ce qui affichera les zones de strates dans la Console (NOTE : cela prendra un certain temps). Sélectionnez une taille d'échantillon arbitraire sous "Determine sample size", et spécifiez sous "Allocate sample size to strata" : 275, 200, 30, 30. Cliquez sur "Create sample" -- note : ne cliquez qu'une seule fois ; il semble que GEE ne réagisse pas mais il dessine l'échantillon après que vous ayez cliqué. En cliquant sur "Add to map", les unités de l'échantillon s'afficheront sous forme de points rouges dans l'affichage de la carte. La dernière étape consiste à exporter l'échantillon : cliquez sur l'onglet Tâches, puis sur Exporter l'échantillon dans la boîte de dialogue - deux entrées nommées "sample_asset" et "sample_CSV" apparaîtront dans Tâches. Elles sont identiques, mais l'une sert à exporter l'échantillon sous forme de fichier CSV, l'autre à l'enregistrer sous forme de fichier GEE Asset à utiliser dans Google Earth Engine. Cliquez sur le bouton Exécuter juste à côté des entrées et enregistrez en tant que GEE Asset et CSV (ce dernier devrait être enregistré dans votre Google Drive). Utilisez le nom "STR_sample_Col" pour GEE Asset et le fichier CSV.

![](figures/STR_AREA2.png)

## 4 Foire aux questions (FAQs)

**Dois-je utiliser les applications mentionnées dans ce tutoriel pour sélectionner un échantillon?**

Non, pas du tout ! Ce ne sont que quelques exemples et il existe de nombreuses autres façons d'échantillonner une zone d'étude. Les applications courantes comprennent R, ENVI et ArcGIS.

**Dois-je sélectionner des pixels ? Et si je veux sélectionner des segments ou des blocs de pixels?**

L'unité spatiale de l'échantillon ne doit pas nécessairement être un pixel, mais doit être de taille égale pour satisfaire aux critères de l'échantillonnage probabiliste. Les pixels sont utilisés comme unités dans ces tutoriels pour des raisons de simplicité. Pour une discussion approfondie des unités spatiales, voir Stehman et Wickham (2011).

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

## References

Cochran, W.G., 1977. Sampling Techniques, John Wiley & Sons, New York, NY.

Lohr, S.L., 1999. Sampling: Design And Analysis, CRC Press.

Rice, J.A., 1995. Mathematical Statistics and Data Analysis (2nd ed.), Duxbury Press, Belmont, CA.

Särndal, C.E., Svensson, B.H., & Wretman, J.H., 1992. Model assisted survey sampling, Springer Science & Business Media, New York, NY.

Stehman, S.V., & Czaplewski, R.L., 1998. Design and analysis for thematic map accuracy assessment: fundamental principles. Remote Sensing of Environment, 64(3), 331-344. https://doi.org/10.1016/S0034-4257(98)00010-8

Stehman, S.V. and Wickham, J.D., 2011. Pixels, blocks of pixels, and polygons: Choosing a spatial unit for thematic accuracy assessment. Remote Sensing of Environment, 115(12), pp.3044-3055. https://doi.org/10.1016/j.rse.2011.06.007



-----

![](./figures/cc.png)  

Ce travail est autorisé sous une licence [Creative Commons Attribution 3.0 IGO](https://creativecommons.org/licenses/by/3.0/igo/)

Copyright 2020, Banque Mondiale. Ce travail a été développé par Pontus Olofsson dans le cadre d'un contrat de la Banque mondiale avec GRH Consulting, LLC pour le développement de nouvelles ressources - et la collecte de ressources existantes - liées à la mesure, la communication et la vérification pour soutenir la mise en œuvre du MRV dans les pays.

Matériel révisé par : Ana Mirian Villalobos, El Salvador, Ministry of Environment and Natural Resources Carole Andrianirina, Madagascar, National Coordination Bureau REDD+ (BNCCREDD) Foster Mensah, Ghana, Center for Remote Sensing and Geographic Information Services (CERGIS) Jennifer Juliana Escamilla Valdez, El Salvador, Ministry of Environment and Natural Resources Phoebe Oduor, Kenya, Regional Centre For Mapping Of Resources For Development (RCMRD) Rajesh Bahadur Thapa, Nepal, International Centre for Integrated Mountain Development (ICIMOD) Tatiana Nana, Cameroon, REDD+ Technical Secretariat

Attribution: Olofsson, P. (2021). *Open MRV: Sample Selection*. World Bank. License: Creative Commons Attribution license (CC BY 3.0 IGO)

![](./figures/wb_fcfc_gfoi.png)
