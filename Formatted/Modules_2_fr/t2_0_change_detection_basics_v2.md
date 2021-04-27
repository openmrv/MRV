---
title: Notions de base sur les méthodes de détection des changements
summary: Ce tutoriel donne un aperçu des bases des méthodes de détection des changements et présente trois algorithmes différents (LandTrendr, CCDC et CODED) pour le suivi des changements du paysage. Il y a des tutoriels approfondis ici sur OpenMRV sous le processus "Détection de changement" pour ces trois algorithmes si vous voulez en savoir plus ou si vous voulez,vous-même, essayer la détection de changement de l'occupation du sol.

author:
- Robert E Kennedy
- Eric Bullock
creation date: Janvier 2021
language: Français
publisher and license: Copyright 2021, Banque mondiale. Ce travail est sous licence Creative Commons Attribution 3.0 IGO

tags:
- OpenMRV
- Télédétection
- Détection des changements


group:
- catégorie : Composite ( Médoïde) et
  étape : Création composite/Pré-traitement
- catégorie : Composite (Médian)
  stade : Création composite/Pré-traitement
- catégorie : Landsat
  étape : Entrées
- catégorie : Sentinel-2 
  étape : Entrées
- catégorie : CCDC
  étape : Détection des changements
- catégorie : CODED
  étape : Détection des changements
- catégorie : LandTrendr
  étape : Détection des changements
---

# Basics of Change Detection methods

## 1 Contexte

L'objectif de la détection des changements par l'image est d'identifier et de cartographier quand et où des changements importants se produisent à la surface de la Terre.  Les méthodes décrites ici sur OpenMRV sous le processus "Détection des changements" et les outils "GEE", "LandTrendr", "CCDC" et "CODED"  reposent toutes sur un principe simple pour ce faire :  On s'attend à ce que les changements à la surface provoquent une modification de la réflectance spectrale suffisamment distincte pour pouvoir être saisie par un algorithme.  

L'objectif de la détection des changements sous-entend plusieurs questions que les utilisateurs doivent prendre en compte lorsqu'ils se lancent dans un exercice de détection des changements.  

Premièrement, la définition de ce qui rend un changement "intéressant" dépend de l'objectif d'un projet.  Pour un projet axé sur la détection du changement et de la dégradation des forêts, le changement intéressant en surface est la destruction ou la détérioration des arbres.  Les changements phénologiques, les changements de robustesse associés à la variation des précipitations d'une année sur l'autre ou les conditions de l'atmosphère au-dessus de la forêt sont moins intéressants.

Deuxièmement, les définitions de "quand" et "où" un changement est cartographié dépendent de la configuration du capteur et de l'algorithme.  La résolution temporelle pour identifier un changement à l'aide de capteurs optiques est limitée par la vitesse de balayage du capteur et les conditions de couverture nuageuse près de la surface.  De plus, la portée de l'imagerie historique impose une limite à la première fois où un changement peut être suivi.  Le "lieu" de la cartographie des changements dépend de la résolution spatiale du capteur. Si la résolution spatiale du capteur est élevée par rapport à l'empreinte du processus de changement qui nous intéresse, la zone réelle cartographiée comme changement peut par un rendu relativement peu satisfaisant du changement réel de la surface. Imaginez de cartographier la construction d'une nouvelle route dans une forêt avec le satellite Landsat de resolution spatiale 30 par 30 m :  Si les propriétés spatiales d'une route beaucoup plus étroite que 30 m peuvent encore faire apparaître que le pixel a changé, la zone de ce changement ne peut pas être résolue en unités plus petites que la taille du pixel entier.  

Une compréhension de base des fondements spectraux du changement aidera les utilisateurs à interpréter la façon dont ces facteurs sont traités par différents algorithmes de changement qui peuvent être trouvés ici sur OpenMRV sous le processus "Détection des changements" et les outils "GEE", "LandTrendr", "CCDC" et "CODED".

### 1.1 **Le changement est un mouvement dans le domaine spectral**

Le concept de base de la détection des changements basée sur le spectre est que le changement dans l'espace spectral correspond au changement des conditions au sol.  Comme décrit précédemment dans le module de classification de la d'occupation de sol, l'"espace spectral" est l'espace de données  à *n*-dimensionnel défini par la réflectance mesurée dans différentes bandes spectrales.  Des objets ayant des signatures spectrales différentes occupent différentes parties de cet espace spectral.  Un changement d'emplacement dans cet espace spectral implique que la signature spectrale a changé, et donc que l’object lui-même (les conditions qui définissent la signature spectrale) a changé d'une manière ou d'une autre.  

Ainsi, un pixel qui est dans une partie de l'espace spectral au temps t1 et qui se déplace vers une autre partie de l'espace spectral au temps t2 est supposé avoir changé d'état de surface.  Si nous comparons simplement l'emplacement d'un pixel dans l'espace spectral à deux dates différentes, nous pouvons déterminer si un changement s'est produit. 

![change_in_spectral_space](./figures/intro/change_in_spectral_space.png)



### 1.2 **Un changement inintéressant provoque un mouvement dans l'espace spectral**

Hélas, les pixels peuvent déplacer leur emplacement dans l'espace spectral pour des raisons autres que celles qui intéressent l'utilisateur.  Par exemple, les conditions météorologiques au moment de l'acquisition de l'image peuvent entraîner un déplacement de l'ensemble de l'espace spectral. Si la position numérique dans l'espace spectral est utilisée pour définir le mouvement et donc le changement, alors tous les pixels de l'image seront considérés comme ayant changé.  À moins que nous ne nous intéressions aux effets  (météorologiques) atmosphériques, nous espérons développer un algorithme qui distingue ce changement sans intérêt  du changement effectif se produisant au sol.



![atmospheric_effects](./figures/intro/atmospheric_effects.png)



De même, si la végétation présente un changement phénologique de la réflectance, un pixel présentera un déplacement dans l'espace spectral.   La plupart des pixels présentent également un certain mouvement dans l'espace spectral en raison d'un décalage de l'angle du soleil ou de l'éclairage.

### 1.3 **Distinction entre les transformations intéressantes et les transformations sans intérêt**

Plus nous comprenons le mécanisme de déplacement d'un pixel dans l'espace spectral sous des " conditions normales ", mieux nous pouvons déterminer quand quelque chose d'intéressant se produit.  Le mouvement dans les conditions normales peut être visualisé comme un " déplacement aléatoire " dans l'espace spectral.  Lorsqu'un pixel émerge de cette région de mouvement normal dans une autre partie de l'espace spectral, nous avons davantage de preuves que quelque chose d'intéressant est survenu.

![random_vs_interesting_movement](./figures/intro/random_vs_interesting_movement.png)



Les algorithmes décrits ici sur OpenMRV sous le processus "Détection des changements" et les outils "GEE", "LandTrendr", "CCDC" et "CODED" s'appuient tous sur ce dernier concept pour reconnaître quand un changement intéressant s'est produit.

-----

![](figures/cc.png)  

This work is licensed under a [Creative Commons Attribution 3.0 IGO](https://creativecommons.org/licenses/by/3.0/igo/).

Copyright 2021, World Bank

Ce travail a été développé par Robert E Kennedy, Eric Bullock dans le cadre d'un contrat de la Banque mondiale avec GRH Consulting, LLC pour le développement de nouvelles ressources - et la collecte des ressources existantes - liées à la mesure, la notification et la vérification afin de soutenir la mise en œuvre du MRV par les pays. 

Attribution  
Kennedy, R. E., Bullock, E. 2021. Basics of Change Detection methods. © World Bank. License: [Creative Commons Attribution license (CC BY 3.0 IGO)](http://creativecommons.org/licenses/by/3.0/igo/)

![](figures/wb_fcfc_gfoi.png)
