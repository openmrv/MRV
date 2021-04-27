---
title: Collecte de données d'entraînement à l'aide de Google Earth Engine
summary: Ce tutoriel montre comment collecter des données d'entraînement  pour la classification de l'occupation du sol à l'aide de Google Earth Engine. Les utilisateurs doivent adapter les différentes composantes en fonction des objectifs de leur projet. Le processus est présenté ici pour les pays suivants - la Colombie, le Mozambique et le Cambodge, et pour une légende simple de quatre classes d'occupation du sol - forêt, eau, plantes herbacées et zones développées. Reportez-vous au processus "Pré-traitement" et à l'outil "GEE" ici sur OpenMRV pour plus d'informations et de ressources pour travailler dans cet environnement.
author: Karis Tenneson
creation date: décembre 2020
language: Français
publisher and license: Copyright 2021, Banque mondiale. Ce travail est sous licence Creative Commons Attribution 3.0 IGO

tags:
- OpenMRV
- Landsat
- Sentinel 2
- GEE
- Couverture nuageuse
- Capteurs optiques
- Haute résolution
- Télédétection
- Composite
- Mosaïque
- Cartographie de l'occupation  du sol
- Cartographie forestière
- Échantillon
- Plan d'échantillonnage
- Plan d'échantillonnage
- Sélection de l'échantillon
- Colombie
- Mozambique
- Cambodge

group:
- catégorie : Composite (Médiane)
  étape : Création du composite/Pré-traitement
- catégorie : Landsat
  étape : Entrées
- catégorie : Sentinel-2
  étape : Entrées
- catégorie : GEE
  étape : Collecte des données d'entraînement 
---

# Collecte de données d'entraînement  à l'aide de Google Earth Engine 

## 1 Contexte

Les données d'entraînement (apprentissage) sont essentielles à la classification supervisée des images. L'ensemble de données d'entraînement est un ensemble de données étiquetées qui est utilisé pour informer ou "former" un classificateur. Le classificateur formé peut ensuite être appliqué à de nouvelles données pour créer une classification. Par exemple, les données d'apprentissage sur l'occupation des sols contiendront des exemples de chaque classe dans la légende de l'étude. Sur la base de ces étiquettes, le classificateur peut prévoir la classe d'occupation de sol la plus probable pour chaque pixel d'une image. Il s'agit d'un exemple de classification catégorique et les étiquettes d'entraînement sont donc  de type catégoriques. En revanche, une variable continue (par exemple, le pourcentage de couverture forestière) peut être prédite à l'aide des étiquettes de variables continues.

Ce tutoriel montre comment collecter des données d'entrainement catégorielles pour la classification de l'occupation du sol à l'aide de Google Earth Engine (GEE). Les utilisateurs doivent ajuster les différentes composantes pour qu'elles correspondent aux objectifs de leur projet. Ici, le processus est démontré pour  la Colombie et pour une simple classification de quatre classes d'occupation des sols : Forêt (Forest), Eau (Water), Herbacé  (Herbaceous) et Développé (Developed).  


### 1.1 Google Earth Engine

Nous allons numériser les données d'entraînement dans Google Earth Engine. Reportez-vous au processus "Pré-traitement" et à l'outil "GEE" ici sur OpenMRV pour plus d'informations et de ressources pour travailler dans cet environnement.

## 2 Objectifs de la formation 

A la fin de cet exercice, vous serez en mesure de :

- Créer de nouvelles collections de caractéristiques dans GEE représentant les classes d'occupation du sol qui vous intéressent.
- Charger votre composite Landsat ou Sentinel pour l'utiliser comme image d'arrière-plan à utiliser comme référence.
- Collecter et exporter des données d'entraînement pour une classification catégorielle. 

### 2.1 Pré-requis 

* Google Earth Engine
  * Avoir un compte GEE.
* Concepts de télédétection
  * Compréhension de base sur les théories impliquées dans la classification des images.
  * Définition d'une légende thématique

## 3 Tutoriel : Collecte de données d'entraînement dans GEE

### 3.1 Vue d'ensemble

Le processus de collecte des données d'entraînement dans GEE est détaillé dans les étapes ci-dessous. Le processus peut être généralement décrit en trois étapes principales :

1. Créer une nouvelle classe éléments  pour chaque occupation du sol afin de stocker les données d'entraînement.
2. Chargement d'une fond de carte 
3. Collecte des données d'entraînement en définissant manuellement les points d'entraînement. 
4. Exportation des données d'entraînement.

![diagramGEE](./figures/m1.2/m1.2.2/diagramGEE.JPG)

### 3.2 Création de nouvelles collections d'éléments

Les données d'entraînement peuvent être créées dans une multitude de plateformes.Dans ce tutoriel, vous créerez ces données en utilisant des collections de points avec des étiquettes d'occupation du sol uniques identifiées par un attribut "label". Par exemple, les forêts peuvent avoir un attribut "label" de 1, l'agriculture de 2, et ainsi de suite. Une méthode simple pour développer des données d'entraînement consiste à créer une collection d'éléments pour chaque occupation du sol en utilisant les données et l'imagerie disponibles dans Google Earth Engine. Ce tutoriel montre comment créer des données d'entraînement qui sont des géométries ponctuelles. Un processus similaire peut être utilisé avec des données de polygones. 

Pour commencer, ouvrez un navigateur web et naviguez jusqu'à [Google Earth Engine](https://code.earthengine.google.com/). 

Ensuite, vous devrez définir une nouvelle classe d'éléments pour chaque occupation du sol. 

1. Lorsque vous êtes dans le Earth Engine, naviguez vers les outils de dessin dans le coin supérieur gauche de la fenêtre de la carte. Cliquez sur l'icône pour ajouter des marqueurs de points. 

    ![AddMarker](./figures/m1.2/m1.2.2/AddMarker.jpg)

2. Cela ajoutera un nouveau panneau *Geometry Imports* dans votre fenêtre de carte, avec une étiquette pour les nouvelles propriétés. Vous pouvez maintenant dessiner dans la fenêtre de carte. Le nom par défaut de cette nouvelle couche est "geometry".

    ![GeometryImports](./figures/m1.2/m1.2.2/GeometryImports.JPG)

3. Maintenez votre curseur sur le nom "geometry" dans ce panneau jusqu'à ce qu'une icône d'engrenage apparaisse sur le côté droit de l'étiquette. Cliquez sur l'engrenage pour ouvrir le panneau afin de modifier la configuration de la couche.

    ![Settings](./figures/m1.2/m1.2.2/Settings.JPG)

4. Donnez ensuite à la couche un nom lié à l'occupation du sol qui vous intéresse, par exemple "forêt". 

    Pour ce tutoriel, nous vous recommandons d'utiliser cette clé de classification de la l'occupation du sol et les codes de classe numériques :

    - 1 Forest
    - 2 Water
    - 3 Herbaceous
    - 4 Developed 

5. Définissez ensuite le type (importation sous) sur FeatureCollection.
6. Ajoutez une propriété en cliquant sur la case *+ Property*. 
7. Donnez-lui une propriété "label" avec un identificateur entier unique. Dans ce cas, 1 représentera la forêt.
8. Enfin, changez la couleur si vous le souhaitez. Par exemple, vous pouvez choisir d'utiliser des marqueurs verts pour les étiquettes de forêt.
9. Cliquez sur *OK* pour enregistrer vos modifications.

    Votre panel devrait ressembler à ceci :

    ![GeomSettings](./figures/m1.2/m1.2.2/GeomSettings.jpg)

10. De retour à la fenêtre de la carte, passez votre souris sur les importations de la géomérie et cliquez sur l'option *+ new layer*.

    ![NewGeom](./figures/m1.2/m1.2.2/NewGeom.jpg)

11. Répétez les étapes 3 à 10 jusqu'à ce qu'une collection éléments soit établie pour chaque type de classe d'occupation des sols.

### 3.3 Charger des fons de carte 
Les données de référence sont essentielles pour la collecte des données d'entraînement, et pour la plupart des objectifs, il suffit d'utiliser des images à haute résolution. Deux facteurs critiques dans la sélection des données de référence sont :

- Les classes cibles peuvent être distinguées grâce à une interprétation visible.
- Le temps de l'imagerie de référence chevauche les données d'entrée utilisées pour la classification.

Il existe une carte de base de l'imagerie de référence à haute résolution disponible directement dans GEE. L'inconvénient est qu'il s'agit d'une mosaïque d'images haute résolution, sans information disponible sur la date d'acquisition.

Pour compléter les informations disponibles dans ces mosaïques d'images haute résolution, il est suggéré de charger également la mosaïque d'images que vous utiliserez pour effectuer la classification supervisée. Les tutoriels sous le nom de "Pré-traitement" et l'outil "GEE" ici sur OpenMRV montrent comment créer une image composite/mosaïque. Vous pouvez ensuite basculer entre l'imagerie haute résolution disponible et le composite d'imagerie pour la date d'intérêt afin de vous assurer qu'aucun changement d'occupation du sol ne s'est produit entre les dates des deux acquisitions d'images. 

N'oubliez pas que vous voulez que les données de référence correspondent à la période et à l'étendue géographique de votre région d'étude. Ici, le processus est démontré pour la Colombie et pour l'année 2019. 

1. Vous pouvez créer un composite Sentinel-2 pour 2019 à la volée et l'ajouter à la carte. Collez le code suivant dans la fenêtre de l'éditeur de code et cliquez sur *Run* pour charger le composite dans la fenêtre de la carte.

    ```javascript
    var countries = ee.FeatureCollection("USDOS/LSIB_SIMPLE/2017");
    var colombia = countries.filter(ee.Filter.eq('country_na','Colombia'));
    Map.centerObject(colombia, 8);

    function maskS2clouds(image){
        return image.updateMask(image.select('QA60').eq(0))}

    var s1_collection = ee.ImageCollection("COPERNICUS/S2_SR");

    var s1_composite_masked = s1_collection.filterBounds(colombia) 
        .filterDate('2019-01-01','2019-12-31') 
        .map(maskS2clouds) 
        .median();

    var vis = {'bands': ['B4', 'B3', 'B2'], 'min': 0, 'max': 1250};
    Map.addLayer(s1_composite_masked, vis, 'Sentinel 2 2019 Masked');
    ````

    ![gee](./figures/m1.2/m1.2.2/gee.JPG)

2. Il existe également une autre façon de charger des images dans GEE, cette deuxième option consiste à charger une image à partir de l'onglet Actifs. Si vous avez exporté une image composite dans votre dossier GEE Asset, vous pouvez l'importer en naviguant dans le dossier Assets. Ensuite, passez votre souris sur le nom de l'image composite et sélectionnez la flèche à importer dans l'éditeur de code. Assurez-vous que l'image que vous chargez à partir de votre dossier Asset est définie comme "image" afin que le code GEE fonctionne. 

    ![import](./figures/m1.2/m1.2.2/import.jpg)

3. Copiez ensuite le texte suivant dans l'éditeur de code pour le charger dans la fenêtre de la carte et cliquez sur *Run*.

    ```javascript
    Map.centerObject(image, 8);
    
    var vis = {'bands': ['B4', 'B3', 'B2'], 'min': 0, 'max': 1250};
    Map.addLayer(image, vis, 'image');
    ```

    Vous pouvez également consulter le site officiel [Earth Engine resources](https://developers.google.com/earth-engine/tutorials/tutorial_api_04) pour obtenir des informations sur la recherche et l'affichage des collections d'images.

### 3.4 Collecter des données d' entraînement

Une fois que vous avez décidé de l'imagerie de référence, il est temps de commencer à collecter des données sur la formation. En allant classe par classe, naviguez dans votre région d'étude en recueillant des données ponctuelles. Voici quelques considérations :

- Les données d'entraînement doivent être représentatives de l'ensemble de votre région d'étude. Cela signifie qu'il est préférable de collecter davantage de données dans toute la région d'étude que dans quelques grandes zones de formation.
- Veillez à inclure des exemples à la limite des classes, car ces zones seront plus difficiles à distinguer lors de la phase de classification. 
- Il n'existe pas de chiffre magique pour un nombre adéquat de points d'entraînement. Préparez-vous à ce que ce soit un processus interactif au cours duquel vous recueillez des données de formation, effectuez votre analyse, puis collectez d'autres données de formation pour corriger les erreurs de classification. 
- Prenez votre temps - cet ensemble de données sera inestimable pour votre recherche et peut l'être aussi pour d'autres. 

1. Sélectionnez la couche d'occupation de sol dans le panneau *Importations géométriques* de la fenêtre de la carte.
2. Sélectionnez le marqueur de points et cliquez dans la carte pour ajouter des points de cette occupation du sol (voici une brève [vidéo](https://youtu.be/tJx7plJLqW4) pour illustrer la manière de procéder). Vous pouvez activer et désactiver l'image composite dans le panneau des couches. Vous pouvez également basculer entre la carte et le composite satellite dans le coin supérieur droit de la fenêtre de la carte.

    ![ToggleImage](./figures/m1.2/m1.2.2/ToggleImage.jpg)

3. Si vous laissez tomber un point par accident, vous pouvez le déplacer ou le supprimer en utilisant la main panoramique, sélectionner le point et le modifier en le faisant glisser pour le déplacer ou le supprimer (voici une brève [vidéo](https://youtu.be/Q6QElHXYOT0) pour illustrer la manière de procéder). Cliquez sur *Exit* pour quitter les points d'édition.

4. Répétez le processus jusqu'à ce que vous ayez de nombreux échantillons de chacune des quatre classes d'occupation des sols dans votre région d'étude. Il est conseillé d'enregistrer le script pendant le processus en sélectionnant le bouton *Save* en haut de la fenêtre de l'éditeur de code. 

### 3.5 Visualisation des données d'entraînement

Une fois que vous avez recueilli les données d'entrainement pour chaque classe, il est utile de les styliser pour voir la répartition dans la zone d'étude. Idéalement, vous voulez avoir des points d'entraînement qui sont représentatifs de la variabilité des classes. Ici, cela signifie que nous voulons avoir suffisamment de points de forêt, d'eau, d'herbacées et de points développés pour nous assurer qu'ils représentent bien ces classes dans toute la Colombie. 

1. Zoom arrière sur l'étendue de la zone d'étude, en l'occurrence la Colombie.
2. Prenez le temps d'examiner votre échantillon et assurez-vous qu'il n'y a pas de "lacunes" majeures dans les données d'entraînement. 

### 3.6 Fusionner et exporter des données
L'étape finale consiste à fusionner chaque élément de l'occupation des sols en une classe finale d'éléments avec toutes les classes d'occupation des sols regroupées. Ensuite, il faut exporter les données. Voici une brève [vidéo](https://youtu.be/r8UBDKztBpY) pour illustrer la manière de procéder.

1. Les éléments de formation peuvent être combinés avec la méthode de "fusion". Par exemple, pour "Forest", "Water", "Herbaceous" et "Developed", qui représentent tous des collections d'éléments, vous pouvez entrer le code suivant N'oubliez pas que JavaScript est sensible à la casse, alors vérifiez la capitalisation entre vos déclarations de fusion et vos noms de géométrie.

    ```javascript
    var training = Forest.merge(Water)
                         .merge(Herbaceous)
                         .merge(Developed);
    ```

2. Les résultats doivent ensuite être enregistrés sous forme de Earth Engine asset pour la classification dans GEE, ou exportés vers votre Google Drive pour la classification à l'aide d'un SIG de bureau. 

    2a. Vous pouvez exporter vers Asset avec le code suivant.
    
    ```javascript
    Export.table.toAsset({
      collection: training,
      description: 'LCsample2019',
      assetId: 'LCsample2019'
    });
    ```

   2b. Vous pouvez exporter vers Google Drive avec le code suivant.

    ```javascript
    Export.table.toDrive({
      collection: training,
      description: 'LCsample2019',
      fileFormat: 'SHP'
    });
    ```

3. Cliquez ensuite sur Run pour exécuter. Cela vous permettra d'aller dans l'onglet Tasks et d'exécuter l'exportation. Des informations supplémentaires sur la façon d'exporter des données dans GEE sont disponibles [ici](https://developers.google.com/earth-engine/guides/exporting).

## 4 Autres exemples : Mozambique et Cambodge 
Essayons maintenant de reproduire le même processus que ci-dessus dans de nouvelles régions d'étude : le Mozambique et le Cambodge. Cette section est facultative et vous permettra de vous entraîner à collecter des données dans différentes régions d'étude. Le processus général est le même que celui qui a été démontré en Colombie. 
Ces exemples montreront comment collecter des données de formation d'une manière qui soit robuste aux différents types de forêts et à la topographie. L'objectif est d'améliorer la robustesse des données d'entraînement, ce qui peut en fin de compte améliorer la qualité de votre classification de l'occupation du sol. Les utilisateurs doivent tenir compte des conditions climatiques et topographiques de leur région d'étude pour déterminer si ces étapes supplémentaires sont nécessaires. 

Effacez votre code précédent en allant sur le bouton *Reset* à côté du bouton *Run*, en cliquant sur la flèche vers le bas, et en cliquant sur *Clear Script*. 

### 4.1 Mozambique

Le Mozambique est un pays écologiquement diversifié qui se compose d'un mélange de zones climatiques tropicales et tempérées. De ce fait, il existe de grandes étendues d'écosystèmes forestiers à feuilles persistantes et à feuilles caduques. En Colombie, nous n'avons pas directement pris en compte les effets saisonniers des forêts, car celles-ci couvrent une proportion relativement faible du pays. La superficie des forêts de feuillus est beaucoup plus importante au Mozambique, ce qui peut présenter un défi pour la classification de l'occupation des sols en raison de la variabilité intra-annuelle de la réflectance entre les stades phénologiques. 

Pour illustrer ce point, observez la variabilité temporelle de l'indice de végétation par différence normalisée (NDVI) au cours d'une année pour un pixel Landsat de 30 mètres dans une forêt saisonnière au Mozambique. Le NDVI est une transformation spectrale qui est couramment utilisée pour analyser la végétation photosynthétiquement active. La saison des pluies au Mozambique s'étend de novembre à mai environ.

La variabilité des saisons peut présenter un défi lors de la classification de l'occupation du sol. Par exemple, si nous devions classifier une image de la saison sèche au Mozambique, une forêt de feuillus pourrait potentiellement être confondue avec des classes d' occupation  herbacée ou non forestière en raison de la faible intensité de la couleur verte de la végétation pendant une période de feuillaison. Pour éviter toute confusion dans le processus de classification, il est essentiel que les données d'entrainement soient représentatives de la variabilité au sein de la classe (c'est-à-dire la variabilité saisonnière des forêts ou d'autres classes végétatives). En d'autres termes, s'il existe des zones importantes de forêts à feuilles caduques et à feuilles persistantes, les données de formation pour une classe "Forêt" plus large doivent contenir des exemples des deux. 

Notre objectif est de faire en sorte que notre classe "Forêt" contienne des exemples de différents types de forêts, comme l'indiquent leurs trajectoires saisonnières. Il existe de nombreuses façons de le faire, et nous allons ici utiliser Google Earth Engine pour examiner la variabilité intra-annuelle de l'NDVI. 

1. Tout d'abord, faisons du Mozambique notre nouvelle région d'étude pour l'année 2019. Pour vous installer, collez le code suivant dans la fenêtre de l'éditeur de code et cliquez sur *Run* pour charger le composite dans la fenêtre de la carte. Cela inclut la fonction de masquage des nuages introduite dans la section 3.3 de ce matériel de formation.

    ```javascript
    var countries = ee.FeatureCollection("USDOS/LSIB_SIMPLE/2017");
    var mozambique = countries.filter(ee.Filter.eq('country_na', 'Mozambique'));
    Map.centerObject(mozambique, 8);
    ```
    
    Poursuivez maintenant la formation à partir d'ici, en commençant par la section 3.4, afin de recueillir de nouvelles données d'entraînement pour le Mozambique.

2. Calculer l' NDVI en utilisant les bandes Rouge (B4) et NIR (B8) de l'imagerie Sentinel-2. Nous aurons également besoin de la fonction de masquage des nuages présentée dans la section 3.3. 

    ```javascript
    function doNDVI(image){
      return image.normalizedDifference(['B4','B8']).rename('NDVI')
    }

    function maskS2clouds(image){
        return image.updateMask(image.select('QA60').eq(0))}
    ```

3. Maintenant, nous pouvons filtrer la collection Sentinel-2 en deux groupes : les images pendant le pic de la saison sèche et les images pendant le pic de la saison des pluies. Nous pouvons ensuite cartographier les collections pour appliquer les masques de nuages et calculer le NDVI. 

    ```javascript
    var s1_collection = ee.ImageCollection("COPERNICUS/S2_SR").map(maskS2clouds);

    var dry_season = s1_collection.filterBounds(mozambique).filterDate('2019-09-01','2019-11-01').map(doNDVI);

    var rainy_season = s1_collection.filterBounds(mozambique).filterDate('2019-01-01','2019-04-01').map(doNDVI);
    ```

4. Pour calculer la variabilité saisonnière, nous pouvons alors combiner ces deux collections et calculer la variance NDVI par pixel en utilisant un [reducer](https:/developers.google.com/earth-engine/guides/reducers_intro). 

    ```javascript
    var combined = rainy_season.merge(dry_season);
    var variance = combined.reduce(ee.Reducer.variance()); 

    var viz = {'min': 0, 'max': 0.1, 'palette': ['red','yellow','green']};
    Map.addLayer(variance, viz);
    ```

    ![MozambiqueNDVI](./figures/m1.2/m1.2.2/MozambiqueNDVI.JPG)

    La carte qui est chargée est la variance saisonnière de NDVI, dans laquelle le rouge indique une variabilité moindre et le vert une variabilité plus importante. 

5. Une étape supplémentaire que nous pouvons faire pour aider à l'identification des forêts est d'utiliser un ensemble de données sur le couvert forestier pour masquer les pixels non forestiers. L'ensemble de données mondiales UMD-Hansen sur la couverture forestière, la perte et le gain est parfait à cet effet. Bien qu'il ne soit pas recommandé d'utiliser cet ensemble de données directement comme données d'entraînement, il s'agit d'un bon outil pour identifier les éventuels lieux de changement des forêts. Ici, nous utiliserons la couche "Tree Cover 2000" pour masquer notre couche de variance NDVI en pixels qui étaient inférieurs à 30% de couverture de la canopée des arbres en 2000. 

    ```javascript
    var umd_hansen = ee.Image("UMD/hansen/global_forest_change_2019_v1_7").select('treecover2000');
    var mask = umd_hansen.gt(30);
    var variance_masked = variance.updateMask(mask);
    Map.addLayer(variance_masked, viz);
    ```

    ![MozambiqueNDVImasked](./figures/m1.2/m1.2.2/MozambiqueNDVImasked.JPG)

6. Maintenant que nous collectons des données d'entraînement pour la classe "Forêt", il est important de référencer cette couche pour s'assurer que les données d'entraînement tiennent compte des différences de variabilité spectrale saisonnière dans les forêts. Tout d'abord, voyons pourquoi il pourrait être avantageux d'effectuer les étapes énumérées ci-dessus : 
    - Certaines forêts ont des modèles saisonniers de productivité. 
    - Nous voulons nous assurer que nos données d'entrainement "Forêt" incluent des exemples de tous les types de forêts dans un domaine d'étude. 
    - Une façon simple et préliminaire de tenir compte de la saisonnalité dans une classification consiste à fournir des données de formation représentatives.
    - GEE nous permet d'identifier facilement les forêts saisonnières en fonction de la variance des valeurs NDVI sur une année.
    - L'ensemble de données UMD-Hansen aide à former la collecte de données en masquant les pixels non forestiers.

7. En suivant les instructions décrites ci-dessus, allez classe par classe pour collecter des points d'entraînement. Pour la classe Forêt, superposez occasionnellement les points d'entraînement sur la carte de variance de la NDVI. Il n'est pas nécessaire de faire une évaluation détaillée, mais il vaut la peine de s'assurer visuellement que les échantillons d'entraînement représentent les forêts saisonnières et non saisonnières. Pour ce faire, il suffit d'alterner les zones rouges, vertes et jaunes sur la couche de variabilité de la NDVI, et de basculer entre cette couche et l'image de référence pour s'assurer que les endroits sont bien des forêts. 

8. N'oubliez pas de sauvegarder fréquemment. 

### 4.2 Cambodge

Le dernier exemple de collecte de données sur la formation en matière de GEE est celui du Cambodge. Le Cambodge a un climat de mousson tropicale avec une saison des pluies allant de mai à octobre environ. Ces dernières années, le Cambodge a connu un taux relativement élevé de changement d'utilisation des terres, souvent sous la forme de déforestation. 

La plupart des forêts restantes au Cambodge sont situées sur des terrains vallonnés ou montagneux. La topographie, cependant, peut introduire un défi à la classification de l'occupation des sols. Comme les caractéristiques topographiques projettent une ombre, la réflectance du paysage dans l'ombre peut être inférieure à celle d'un paysage similaire non ombragé. Pour réduire cet effet, il est important de collecter des données d'entraînement qui soient représentatives des différentes conditions topographiques d'une région d'étude. Cet exemple montrera comment procéder. 

1. Si vous souhaitez plutôt vous entraîner à collecter des données d'entraînement au Cambodge, collez le code suivant dans l'éditeur de code et passez ensuite à la section 3.4 pour continuer. 

    ```javascript
    var countries = ee.FeatureCollection("USDOS/LSIB_SIMPLE/2017");
    var cambodia = countries.filter(ee.Filter.eq('country_na', 'Cambodia'));
    Map.centerObject(cambodia, 8);

    function maskS2clouds(image){
        return image.updateMask(image.select('QA60').eq(0))}

    var s1_collection = ee.ImageCollection("COPERNICUS/S2_SR");

    var s1_composite_masked = s1_collection.filterBounds(cambodia) 
        .filterDate('2019-01-01','2019-12-31') 
        .map(maskS2clouds) 
        .median();

    var vis = {'bands': ['B4', 'B3', 'B2'], 'min': 0, 'max': 1250};
    Map.addLayer(s1_composite_masked, vis, 'Sentinel 2 2019 Masked');
    ```

2. Naviguez jusqu'au bouton 'Map / Satellite' situé sur le côté droit de l'écran et cliquez sur "Satellite". Cela vous permettra de voir la carte de terrain qui facilitera la visualisation des caractéristiques topographiques dans l'imagerie de référence, afin qu'elle puisse être utilisée comme information supplémentaire lors de la collecte des données de référence. Veillez à collecter des échantillons d'entraînement pour les forêts qui varient en fonction de leur disposition topographique. Par exemple, les échantillons doivent être collectés sur un terrain qui diffère par sa pente et son aspect. Il n'est pas nécessaire d'être précis, et cela peut être fait de manière optionnelle pour n'importe quelle occupation du sol. 

    ![MapSatellite](./figures/m1.2/m1.2.2/MapSatellite.JPG)

3. Vous pouvez également modifier la transparence des couches que vous créez en cliquant sur "Layers" sur le côté droit de l'écran et en ajustant la couche, comme le montre l'image ci-dessous. 

    ![LayerTransparency](./figures/m1.2/m1.2.2/LayerTransparency.JPG)

4. N'oubliez pas de sauvegarder fréquemment.


## 5 Foire aux questions

**Pourquoi utilisons-nous des géométries de points plutôt que des polygones?**

Des polygones peuvent également être utilisées comme données d'entraînement, mais gardez à l'esprit que l'autocorrélation spatiale entraînera des informations redondantes dérivées de chaque polygone. Nous recommandons donc de collecter des échantillons ponctuels représentatifs de l'ensemble des données plutôt que de quelques polygones.  


**Comment choisir les données à utiliser comme référence?**

Les données de référence doivent recouvrir dans le temps et dans l'espace les données utilisées dans votre analyse. S'il existe plusieurs sources de données répondant à ce critère, l'utilisateur doit choisir les données qu'il trouve les plus faciles à interpréter en se basant sur la légende de sa classification. 


**Les données relatives à la formation doivent-elles être dérivées selon un plan d'échantillonnage probabiliste?**

Non, il n'est pas nécessaire d'obtenir des données d'entraînement en utilisant un plan d'échantillonnage basé sur les probabilités. Cependant, si les données de formation ont été créées de cette manière (par exemple un échantillon aléatoire simple interprété), il n'y a aucune raison pour qu'elles ne puissent pas être utilisées pour la classification. 


**Combien de points dois-je obtenir pour chaque classe?**

Il n'y a pas de nombre magique pour le nombre de points de formation pour chaque classe. Il est généralement recommandé d'utiliser un processus itératif, dans lequel des données d'entraînement supplémentaires sont ajoutées après avoir effectué une classification, puis la classification est créée à nouveau ; le processus se répète jusqu'à ce que les résultats soient jugés adéquats. 

**Peut-on diviser les données d'entraînement pour en utiliser une partie pour la validation?**

Si les données d'entraînement ont été collectées de manière opportuniste, ou en d'autres termes *non* en utilisant un échantillon probabiliste, alors il n'est généralement pas recommandé de les utiliser pour la validation car cela introduirait un biais. 

-----

![](./figures/m1.1/cc.png)

Ce travail est sous licence [Creative Commons Attribution 3.0 IGO](https://creativecommons.org/licenses/by/3.0/igo/) 

Copyright 2021, Banque mondiale 

Ce travail a été développé par Karis Tenneson dans le cadre d'un contrat de la Banque mondiale avec GRH Consulting, LLC pour le développement de nouvelles ressources - et la collecte des ressources existantes - liées à la mesure, la notification et la vérification afin de soutenir la mise en œuvre du MRV par les pays. 

Matériel examiné par :   
Carole Andrianirina, Madagascar, National Coordination Bureau REDD+ (BNCCREDD)  
Foster Mensah, Ghana, Center for Remote Sensing and Geographic Information Services (CERGIS)  
Jennifer Juliana Escamilla Valdez, El Salvador, Ministry of Environment and Natural Resources   
Kenset Rosales, Guatemala, Ministry of Environment and Natural Resources  
Konan Yao Eric Landry, Côte d'Ivoire, REDD+ Permanent Executive Secretariat     
Paula Andrea Paz, Colombia, International Center for Tropical Agriculture (CIAT)  
Phoebe Oduor, Kenya, Regional Centre For Mapping Of Resources For Development (RCMRD)   
Raja Ram Aryal, Nepal, Forest Research and Training Centre 

Attribution   
Tenneson, K. 2021. Formation à la collecte de données à l'aide de Google Earth Engine.  Banque mondiale. License:  [Creative Commons Attribution license (CC BY 3.0 IGO)](http://creativecommons.org/licenses/by/3.0/igo/

![](./figures/m1.1/wb_fcfc_gfoi.png)
