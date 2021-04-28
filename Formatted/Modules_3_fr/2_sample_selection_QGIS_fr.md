---
title: Procédure de sélection d'un échantillon à l'aide de QGIS
summary: Dans les méthodes de conception d'échantillonnage pour l'estimation de la superficie et de la précision des cartes, nous concevons un échantillon en choisissant un protocole de sélection et en déterminant la taille de l'échantillon et son allocation. Dans ce tutoriel, nous allons tirer physiquement d'une zone d'étude un échantillon qui a été conçu sur la base des tutoriels ici sur OpenMRV sous le processus " Plan d'échantillonnage ". Ici, nous illustrons comment procéder au prélèvement d'un échantillon dans QGIS.
author: Pontus Olofsson
creation date: Février, 2021
language: Français
publisher and license: Copyright 2021, Banque mondiale. Ce travail est autorisé sous une licence Creative Commons Attribution 3.0 IGO

tags:
- OpenMRV
- QGIS
- Plan d'échantillonnage
- Conception de l'échantillon
- Sélection de l'échantillon
- Échantillon
- Base d'échantillonnage
- Colombie

group:
- catégorie : Stratifié
  étape : Échantillonnage
- catégorie : Aléatoire simple
  étape : Échantillonnage
- catégorie : Cluster
  étape : Échantillonnage
- catégorie : Systématique
  étape : Échantillonnage

---

# Sélection d'un échantillon à l'aide de QGIS

## 1 Contexte

Dans le tutoriel précédent, nous avons conçu un échantillon en choisissant un protocole de sélection et en déterminant la taille de l'échantillon et la répartition. Dans ce tutoriel, nous allons physiquement prélever dans une zone d'étude l'échantillon que nous avons conçu. Le tirage d'un échantillon implique la création d'une *cadre d'échantillonnage* qui est une liste d'unités de population pouvant être sélectionnées pour être incluses dans un échantillon. Les unités de population de la liste sont appelées unités d'échantillonnage. En d'autres termes, une base de sondage est un dispositif qui permet d'observer la population en associant les unités de population aux unités d'échantillonnage (Särndal et al., 1992, p. 9). Dans notre cas, la base de sondage est par exemple une liste de tous les pixels qui composent la zone d'étude. Nous pourrions donc simplement exporter une liste de tous les pixels de la carte avec des identifiants uniques à partir desquels nous sélectionnons aléatoirement *n* unités. Dans les méthodes d'échantillonnage pour l'estimation de la superficie et de la précision des cartes, nous créons un échantillon en choisissant un protocole de sélection et en déterminant la taille de l'échantillon et l'allocation. Dans ce tutoriel, nous allons tirer matériellement d'une zone d'étude un échantillon qui a été conçu sur la base de tutoriels ici sur OpenMRV sous le processus " Plan d'échantillonnage ".

## 2 Objectifs d'apprentissage

À la fin du tutoriel, l'utilisateur devrait être en mesure d'échantillonner une zone d'étude arbitraire, soit par échantillonnage systématique (SYS), soit par échantillonnage aléatoire simple (SRS), en utilisant QGIS.

- Créer un échantillon dans QGIS sous SYS ou SRS

### 2.1 Prérequis 

-  Relevant terminology for sampling techniques can be found at the end of this document

## 3 Tutoriel: Création d'un échantillon à l'aide de QGIS

QGIS prend en charge l'échantillonnage de populations définies par des données vectorielles. Par conséquent, si vous voulez échantillonner dans des strates définies par un raster, vous devrez d'abord vectoriser les données raster. Ceci se fait par Raster > Conversions > Polygoniser (Raster vers Vecteur). La vectorisation pour les rasters de grande taille prend beaucoup de temps et n'est pas recommandée ; utilisez plutôt les alternatives ci-dessous. Pour les zones d'étude plus petites ou pour les plans SYS et SRS, QGIS fonctionne bien. Passons en revue les étapes nécessaires pour tirer deux échantillons sous SRS et SYS du pays de la Colombie.

### 3.1 Échantillonnage aléatoire simple

1. Nous avons d'abord besoin d'un fichier de format vectoriel délimite notre zone d'étude. Téléchargez un shapefile de la zone de délimitation de la Colombie ici : https://drive.google.com/file/d/1tXvczTra_5wrlXBhe00m_oKRpLK0GwwJ/view?usp=sharing
2. Affichez le fichier dans QGIS : Calque > Ajouter un couche > Ajouter une couche vectorielle et sélectionnez le fichier de forme colombiaborder.shp pour le dessiner sur le canevas.
3. Vectoriel > Outils de recherche > Points aléatoires à l'intérieur des polygones
4. Spécifiez la limite de la Colombie comme couche d'entrée, le nombre de points comme stratégie d'échantillonnage et la taille totale de l'échantillon sous Nombre de points ; laissez la distance minimale " Enregistrer dans un fichier et cliquez sur Exécuter pour obtenir l'échantillon.

![](./figures/SRS_QGIS.PNG)

### 3.2 Échantillonnage systématique

Le tracé d'un échantillon sous SYS dans QGIS présente l'inconvénient que la population doit être rectangulaire, ce qui rend plus difficile le tracé d'un nombre exact d'unités pour une zone non rectangulaire. Nous pouvons simplement découper les unités d'échantillonnage pour la frontière de la Colombie, mais cela donnera une taille d'échantillon plus petite que celle spécifiée. Une solution consiste à définir une distance entre les unités en fonction de la taille de la zone d'étude. Par exemple, si la zone d'étude est de *x* km^2^, en fixant l'espacement entre les unités à x/100, on obtient un échantillon de 100 unités.

1. Après avoir ajouté le fichier de données vectoriel dans la section 3.1 étapes 1 et 2 ci-dessus, allez dans **Vector** > **Reserach Tools** > **Regular Points**.
2. Sélectionnez comme zone d'entrée, le shapefile de la Colombie
3. Spécifiez l'espacement des points ou le nombre de points -- si vous utilisez le premier, cochez la case "Utiliser l'espacement des points".
4. Enregistrez dans un fichier et cliquez sur Exécuter pour dessiner l'échantillon.

![](figures/SYS_QGIS.PNG)

## 4 Foire aux questions

**Dois-je utiliser QGIS pour creer un échantillon ?**

Non, pas du tout ! Ceci n'est qu'un exemple et il existe de nombreuses autres façons d'échantillonner une zone d'étude. Les applications courantes comprennent AREA2, R, ENVI et ArcGIS. Ici, sur OpenMRV, sous le processus " Plan d'échantillonnage " et les outils " AREA2 " et " GEE ", vous pouvez apprendre comment sélectionner un échantillon en utilisant AREA2.

**Dois-je sélectionner des pixels ? Et si je veux sélectionner des segments ou des blocs de pixels?**

L'unité spatiale de l'échantillon ne doit pas nécessairement être un pixel, mais doit être de taille égale pour satisfaire aux critères de l'échantillonnage probabiliste. Les pixels sont utilisés comme unités dans ce tutoriel pour des raisons de simplicité. Pour une discussion approfondie des unités spatiales, voir Stehman et Wickham (2011).

## 5 Terminologie relative aux techniques d'échantillonnage

Une liste de termes relatifs aux techniques d'échantillonnage et d'inférence est fournie dans la documentation d'AREA2 : https://area2.readthedocs.io/en/latest/definitions.html Vous trouverez ci-dessous quelques termes supplémentaires qui ne figurent pas dans la documentation d'AREA2.

### 5.1 Plan de réponse

Défini par (Stehman and Czaplewski, 1998): “La référence ou classe réelle est obtenue pour chaque unité d'échantillonnage sur la base de l'interprétation de photographies aériennes ou de vidéographies, d'une observation au sol ou d'une combinaison de ces sources. Les méthodes utilisées pour déterminer cette référence de classification sont appelées "plan de réponse". Le plan d'intervention comprend les procédures de collecte des informations relatives à la détermination de la occupation du sol de référence, et les règles d'attribution d'une ou plusieurs [labels] de référence à chaque unité d'échantillonnage.” Connu sous le nom de “plan de mesure” par Särndal et al. (1992).

### 5.2 Echantillon

Un sous-ensemble de la population sélectionné parmi les unités de la population.

### 5.3 Plan d'échantillonnage

Synonyme de plan d'échantillonnage (Sampling Design), qui est le terme préféré dans la littérature de référence (Cochran, 1977, Särndal et al., 1992). Le terme apparaît chez Rice (1995) ui utilise à la fois “sampling design, ***plan d'echantillonnage\***” et “sample design, ***plan d'echantillon\***”.

### 5.4 Plan d'échantillonnage

“Le concept de plan d'échantillonnage (sampling design ) est le protocole par lequel les unités de référence de l'échantillon sont sélectionnées” (Stehman and Czaplewski, 1998). Le terme “Sampling design” est également utilisé par Cochran (1977) and Särndal et al. (1992) -- Le premier utilise également “sampling plan”.

### 5.5 Sondage/Enquêtee

Särndal et al. (1992) définissent une enquête comme une “investigation partielle d'une population finie”, et précisent que “les concepts d ‘enquête’ et ‘enquête par sondage’ sont utilisés pour désigner des enquêtes statistiques présentant les caractéristiques méthodologiques suivantes: [...] échantillonnage aléatoire [...] plan de mesure [et] estimation”. de facon plus precise une enquete par sondage ou un sondage est une enquête effectuee sur une partie de la population. Cette fraction de la population constitue l'échantillon et les méthodes qui permettent de construire cet echantillon s'appellent méthode d'échantillonnage.

### 5.6 Plan d'enquête

UN “plan de sondage total” définit les procédures pour “obtenir la plus grande précision possible dans les estimations de l'enquête tout en trouvant un équilibre entre les erreurs d'échantillonnage et les erreurs non dues à l'échantillonnage [...] Le plan de sondage donne lieu à des opérations d'enquête” sélection de l'échantillon (Särndal et al., 1992). Lohr (1999) décrit un plan de sondage total comme “Une philosophie de conception d'enquête visant à minimiser les erreurs de non-échantillonnage ainsi que les erreurs d'échantillonnage..” De plus, dans Lohr (1999) “plan d'enquête” est synonyme de plan d'échantillonnage.

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

Copyright 2021, Banque Mondiale. 

Ce travail a été développé par Pontus Olofsson dans le cadre d'un contrat de la Banque mondiale avec GRH Consulting, LLC pour le développement de nouvelles ressources - et la collecte de ressources existantes - liées à la mesure, la communication et la vérification pour soutenir la mise en œuvre du MRV dans les pays.

Matériel révisé par :   
Ana Mirian Villalobos, El Salvador, Ministry of Environment and Natural Resources  
Carole Andrianirina, Madagascar, National Coordination Bureau REDD+ (BNCCREDD)  
Foster Mensah, Ghana, Center for Remote Sensing and Geographic Information Services (CERGIS)  
Jennifer Juliana Escamilla Valdez, El Salvador, Ministry of Environment and Natural Resources   
Phoebe Oduor, Kenya, Regional Centre For Mapping Of Resources For Development (RCMRD)  
Rajesh Bahadur Thapa, Nepal, International Centre for Integrated Mountain Development (ICIMOD)  
Tatiana Nana, Cameroon, REDD+ Technical Secretariat

Attribution   
Olofsson, P. 2021. Sample selection using QGIS. © World Bank. License: [Creative Commons Attribution license (CC BY 3.0 IGO)](http://creativecommons.org/licenses/by/3.0/igo/)

![](./figures/wb_fcfc_gfoi.png)
