---
title: Collecte des données d'apprentissage
summary: Ce tutoriel montre comment collecter des données d'apprentissage catégorielles pour la classification de l'occupation du sol en utilisant QGIS ou Google Earth Engine. Les utilisateurs doivent adapter les différentes composantes en fonction des objectifs de leur projet. Le processus est présenté ici pour les pays suivants - Colombie, Mozambique et Cambodge, ainsi que pour une légende simple de quatre classes d'occupation du sol - forêt, eau, plantes herbacées et zones développées.
author:
- Eric Bullock
- Karis Tenneson
creation date: décembre 2020
language: Français
publisher and license: Copyright 2020, Banque mondiale. Ce travail est sous licence Creative Commons Attribution 3.0 IGO

tags:
- OpenMRV
- Landsat
- Sentinel 2
- Planet Labs
- MODIS
- QGIS
- GEE
- Couverture nuageuse
- Capteurs optiques
- Haute résolution
- Télédétection
- Composite
- Mosaïque
- Cartographie de l'occupation  du sol
- Cartographie forestière
- Echantillon
- Plan d'échantillonnage
- Plan d'échantillonnage
- Sélection de l'échantillon
- Colombie
- Mozambique
- Cambodge

group:
- catégorie : Composite (Médiane)
  étape : Création du composite/pré-traitement 
- catégorie : Landsat
  étape : Entrées
- catégorie : Sentinel-2 Sentinel-2
  étape : Entrées
- catégorie : MODIS MODIS
  étape : Entrées
- catégorie : QGIS QGIS
  étape : Collecte de données d'entraînement
- catégorie : GEE
  étape : Collecte des données d'entraînement
---

## 1  Contexte

Les données d'entraînement sont essentielles à la classification supervisée des images. L'ensemble de données d'entraînement est un ensemble de données labellisées qui est utilisé pour informer ou "entraîner" un classificateur. Le classificateur formé peut ensuite être appliqué à de nouvelles données pour créer une classification. Par exemple, les données d'entraînement d'occupation du sol contiendront des exemples de chaque classe dans la légende de l'étude, et sur la base de ces labels, le classificateur peut être utilisé pour prédire la classe d'occupation du sol la plus probable pour chaque pixel d'une image. Il s'agit d'un exemple de classification catégorielle et les labels d'entraînement sont donc catégoriels. En revanche, une variable continue (par exemple, le pourcentage de couverture des arbres) peut être prédite en utilisant des données d'entraînement continues.

Ce tutoriel montre comment collecter des données d'entraînement catégorielles pour la classification de l'occupation du sol en utilisant QGIS ou Google Earth Engine. Les utilisateurs doivent choisir l'option qui leur est la plus familière (QGIS ou Google Earth Engine) et ajuster les différents composants en fonction des objectifs de leurs projets. Le processus est présenté ici pour les pays suivants : Colombie, Mozambique et Cambodge, ainsi que pour une légende simple de quatre classes d'occupation du sol : Forêt, Eau, Herbacée, et Développé.1.2 Tutorials

- Pour la collecte de données d'entraînement à l'aide de **QGIS**, veuillez vous référer à [1.2.1 Lien ](https://github.com/openmrv/MRV/blob/main/Formatted/Modules_1/Training_Data_QGIS_m1.2.1.md)
- FPour la collecte de données d'entraînement à l'aide **Google Earth Engine**, veuillez vous référer à [1.2.2 Lien ](https://github.com/openmrv/MRV/blob/main/Formatted/Modules_1/Training_Data_GEE_m.1.2.2.md)

------

[![img](https://github.com/openmrv/MRV/raw/main/Formatted/Modules_1/figures/m1.1/cc.png)](https://github.com/openmrv/MRV/blob/main/Formatted/Modules_1/figures/m1.1/cc.png)

Cette œuvre est soumise à une licence  [Creative Commons Attribution 3.0 IGO](https://creativecommons.org/licenses/by/3.0/igo/).

Copyright 2020, Banque mondiale

Ce travail a été réalisé par Eric Bullock et Karis Tenneson dans le cadre d'un contrat de la Banque mondiale avec GRH Consulting, LLC pour le développement de nouvelles ressources - et la collecte de ressources existantes - liées à la mesure, au rapportage et à la vérification pour soutenir la mise en œuvre du MRV dans les pays.

Attribution
Bullock, E., Tenneson, K. 2020. Création de mosaïque/composite d'images pour Landsat et Sentinel-2 dans Google Earth Engine. Banque mondiale. Licence: [Creative Commons Attribution license (CC BY 3.0 IGO)](http://creativecommons.org/licenses/by/3.0/igo/)
