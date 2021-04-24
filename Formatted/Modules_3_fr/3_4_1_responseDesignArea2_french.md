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

# Response design in AREA2 

## 1.Contexte

AREA2, abréviation de Area Estimation & Accuracy Assessment, est une application de Google Earth Engine qui fournit un support complet pour l'échantillonnage et l'estimation dans un cadre d'inférence basé sur la conception. Pour plus d'informations sur AREA2, veuillez consulter le site suivant https://area2.readthedocs.io/en/latest/.

Le plan de réponse définit la " réponse " des unités d'un échantillon. Dans le contexte de l'inférence basée sur le design dans un contexte géographique, " le design de réponse englobe toutes les étapes du protocole qui mènent à une décision concernant la concordance des classifications de référence et de la carte [et] la meilleure classification disponible des [conditions de surface du sol] pour chaque unité spatiale échantillonnée "  (Olofsson et al. 2014) [^fn1].  Les termes suivants sont importants :

**Données de référence**
Données caractérisant l'évaluation disponible la plus précise de la condition réelle à la localisation de l'échantillon (exemple : imagerie satellitaire à résolution fine).

**Observations de référence**
L'évaluation disponible la plus précise de l'état réel d'une unité de population.

**Classification de référence**
La classification de référence appliquée à la collection de toutes les unités d'échantillonnage.

**Plan de réponse**

Défini par (Stehman and Czaplewski, 1998)[^fn1]: “La référence ou classe réelle est obtenue pour chaque unité d'échantillonnage sur la base de l'interprétation de photographies aériennes ou de vidéographies, d'une observation au sol ou d'une combinaison de ces sources. Les méthodes utilisées pour déterminer cette référence de classification sont appelées "plan de réponse". Le plan d'intervention comprend les procédures de collecte des informations relatives à la détermination de la occupation du sol de référence, et les règles d'attribution d'une ou plusieurs [labels] de référence à chaque unité d'échantillonnage.” Connu sous le nom de “plan de mesure” par Särndal et al. (1992)[^fn2].

**Echantillon**

Un sous-ensemble de la population sélectionné parmi les unités de la population.

**Plan d'échantillonnage**

Synonyme de plan d'échantillonnage (Sampling Design), qui est le terme préféré dans la littérature de référence (Cochran, 1977[^fn3], Särndal et al., 1992[^fn2]). Le terme apparaît chez Rice (1995)[^fn4] ui utilise à la fois “sampling design, ***plan d'echantillonnage\***” et “sample design, ***plan d'echantillon\***”.

**Plan d'échantillonnage**

“Le concept de plan d'échantillonnage (sampling design ) est le protocole par lequel les unités de référence de l'échantillon sont sélectionnées” (Stehman and Czaplewski, 1998)[^fn1]. Le terme “Sampling design” est également utilisé par Cochran (1977)[^fn3] and Särndal et al. (1992)[^fn2] -- Le premier utilise également “sampling plan”.

**Sondage/Enquêtee**

Särndal et al. (1992)[^fn2] définissent une enquête comme une “investigation partielle d'une population finie”, et précisent que “les concepts d ‘enquête’ et ‘enquête par sondage’ sont utilisés pour désigner des enquêtes statistiques présentant les caractéristiques méthodologiques suivantes: [...] échantillonnage aléatoire [...] plan de mesure [et] estimation”. de facon plus precise une enquete par sondage ou un sondage est une enquête effectuee sur une partie de la population. Cette fraction de la population constitue l'échantillon et les méthodes qui permettent de construire cet echantillon s'appellent méthode d'échantillonnage.

**Plan de sondage**

Un “plan de sondage total” définit les procédures pour “obtenir la plus grande précision possible dans les estimations de l'enquête tout en trouvant un équilibre entre les erreurs d'échantillonnage et les erreurs non dues à l'échantillonnage [...] Le plan de sondage donne lieu à des opérations d'enquête” sélection de l'échantillon (Särndal et al., 1992)[^fn2]. Lohr (1999)[^fn5] décrit un plan de sondage total comme “Une philosophie de conception d'enquête visant à minimiser les erreurs de non-échantillonnage ainsi que les erreurs d'échantillonnage..” De plus, dans Lohr (1999) “plan d'enquête” est synonyme de plan d'échantillonnage.


Dans ce tutoriel, vous apprendrez à déterminer les conditions de référence en examinant un ensemble de données de référence aux emplacements des unités d'un ensemble de données d'échantillon à l'aide d'AREA2. Cet ensemble de données échantillons comprendra quatre strates : forêt, non-forêt, perturbation forestière et une zone tampon autour de la perturbation forestière. L'objectif est d'estimer la superficie de la perturbation forestière ; par conséquent, vous apprendrez à collecter des observations de référence sur la forêt, la zone non forestière et la perturbation forestière. Vous pouvez également utiliser d'autres outils pour accomplir cette tâche. Vous pouvez trouver d'autres tutoriels ici sur OpenMRV sous " Collecte de données d'échantillonnage " et les outils " CE ", et " CEO ".


## 2 Learning Objectives

Upon completion of the tutorial, the user should be able to display a set of reference data at locations of sample units designed and drawn from a study area. The user should be able to determine reference conditions at the land surface by examining time series of Landsat data in combination with high resolution data in Google Earth. 

* Display a set of reference data at locations of sample units in GEE
* Determine reference conditions at the land surface by examining time series of Landsat data in combination with high resolution data in GEE

### 2.1 Pre-requisites
* A general understanding of image interpretation. Image interpretation is the process of looking at moderate, high, or very high spatial resolution imagery (from satellites or aerial photography) and labeling the objects of interest in your sample locations. Photo interpretation is the core skill needed to effectively determine reference conditions at the land surface.


## 3 Tutorial: Response design in Area2

### 3.1 Préparer les données de référence
 La première étape consiste à extraire les séries temporelles des données Landsat aux localisations de l'échantillon. Pour ce faire, nous utilisons le script Save Feature Timeseries : https://code.earthengine.google.com/21658946c5c1456003aedcdd2eb303ce Ce script n'a pas d'interface graphique mais tout ce que nous avons à faire est de pointer le script vers l'actif GEE contenant l'échantillon. En haut du script, ajoutez simplement la ligne suivante en spécifiant l'emplacement de l'échantillon sélectionné à l'étape précédente :
 ```javascript
 var sample = ee.FeatureCollection('users/olofsson76/Open_MRV/STR_sample_Col')
 ```
 Changez également les dates de 'début' et de 'fin' dans le script en fonction de votre période d'étude. Cliquez sur Exécuter dans Tâches et enregistrez le résultat sous forme de ressource GEE en le nommant "[filename]_TS".


### 3.2 Examiner les données de référence sur les sites d'échantillonnage

Le collecteur de référence se trouve ici: https://code.earthengine.google.com/05e5344851a67c0332134e30a2940249
Une fois chargé, spécifiez un chemin pour sauvegarder votre travail sous "Inputs and Outputs" et par "Link to FC", spécifiez l'emplacement de l'actif contenant l'échantillon après avoir été traité en utilisant le script Save Feature Timeseries comme décrit ci-dessus. Cochez "Load chart data from feature collection" et cliquez sur "Load". Cela devrait afficher la taille de l'échantillon -- dans mon cas, j'utilise l'échantillon de 535 unités que nous avons conçu dans le tutoriel sur le plan d'échantillonnage.

Pour commencer, sous "Interprétation de l'échantillon", spécifiez "1" et appuyez sur la touche Entrée -- cela affichera les données de référence pour la première unité de l'échantillon. Les graphiques de séries temporelles situés au centre de l'interface sont importants : les séries temporelles sont affichées pour les bandes rouge, NIR et SWIR1 de Landsat, et pour les transformations de Tasseled Cap (Kauth-Thomas) : luminosité, verdure et humidité. Les six premiers graphiques montrent les données des séries temporelles pour la période d'étude spécifiée dans le script Save Features Timeseries ci-dessus ; vous pouvez zoomer sur un certain intervalle de temps et les graphiques peuvent être affichés dans une fenêtre séparée en cliquant sur la flèche à côté de chaque graphique. Les six derniers graphiques sont des graphiques de séries chronologiques annuelles cumulées, de sorte que les données de chaque année sont tracées "au-dessus" les unes des autres.   

Above the time series data is the outline of the sample unit draped on top of the default GEE satellite imagery -- click "KML" to display high resolution data in Google Earth at sample locations.

 ![](./figures/AREA2_ref_collector.png)

Pour l'instant, nous recommandons à l'utilisateur de noter les étiquettes de référence dans une feuille de calcul séparée, car la mise en œuvre de la sauvegarde des étiquettes de référence dans une collection unique de caractéristiques est en cours. Des vidéos illustrant la manière d'observer les conditions de référence en examinant les données de référence sont fournies ici (les vidéos font partie du projet NASA MEaSUREs GLanCE à l'Université de Boston http://sites.bu.edu/measures/):  
* https://drive.google.com/file/d/1Y_D49kE_oiXxGEJEcPGT8FavrzdMj2qh/view?usp=sharing
* https://drive.google.com/file/d/1Md5NajZAngJsVWWiTCbgSdLiEyw7u6BE/view?usp=sharing

## 4 Frequently Asked Questions (FAQs)

**If I can't determine the reference conditions at the location of a sample unit, can I discard that unit from the sample?**

It is imperative that the reference observations represent reference conditions; therefore, it is better to discard a sample unit than guessing. At the same time, removing units because the provision of reference labels is impossible violates the rules of probability sampling. For these reasons, it is difficult to provide guidelines for how many sample units can be discarded. (A renowned colleague of mine once told me that it is acceptable to remove discard up to 15% of the units in sample but he didn't want to be quoted, and I have not found any support for this figure in the literature.)



## References
Cochran, W.G., 1977. *Sampling Techniques*, John Wiley & Sons, New York, NY.

Lohr, S.L., 1999. *Sampling: Design And Analysis,* CRC Press.

Olofsson, P., Foody, G.M., Herold, M., Stehman, S.V., Woodcock, C.E. and Wulder, M.A., 2014. Good practices for estimating area and assessing accuracy of land change. Remote Sensing of Environment, 148, pp.42-57. https://doi.org/10.1016/j.rse.2014.02.015

Rice, J.A., 1995. *Mathematical Statistics and Data Analysis* (2nd ed.), Duxbury Press, Belmont, CA.

Särndal, C.E., Svensson, B.H., & Wretman, J.H., 1992. *Model assisted survey sampling*, Springer Science & Business Media, New York, NY.

Stehman, S.V., & Czaplewski, R.L., 1998. Design and analysis for thematic map accuracy assessment: fundamental principles. *Remote Sensing of Environment*, 64(3), 331-344. https://doi.org/10.1016/S0034-4257(98)00010-8

-----

![](figures/cc.png)  

Cette œuvre est soumise à une licence  [Creative Commons Attribution 3.0 IGO](https://creativecommons.org/licenses/by/3.0/igo/) 

Copyright 2021, Banque Mondiale. 

Ce travail a été développé par Pontus Olofsson dans le cadre d'un contrat de la Banque mondiale avec GRH Consulting, LLC pour le développement de nouvelles ressources - et la collecte de ressources existantes - liées à la mesure, la notification et la vérification pour soutenir la mise en œuvre du MRV par les pays. 

Material reviewed by:   
Ana Mirian Villalobos, El Salvador, Ministry of Environment and Natural Resources  
Carole Andrianirina, Madagascar, National Coordination Bureau REDD+ (BNCCREDD)  
Jennifer Juliana Escamilla Valdez, El Salvador, Ministry of Environment and Natural Resources   
Phoebe Oduor, Kenya, Regional Centre For Mapping Of Resources For Development (RCMRD)   
Tatiana Nana, Cameroon, REDD+ Technical Secretariat

Attribution: 
Olofsson, P. 2021. Sample selection using QGIS. © World Bank. License:  [Creative Commons Attribution license (CC BY 3.0 IGO)](http://creativecommons.org/licenses/by/3.0/igo/) 

![](figures/wb_fcfc_gfoi.png)
