---
title: Échantillonnage aléatoire stratifié
summary: Dans le contexte de la télédétection ou de la géographie, les approches basées sur l'échantillonnage sont nécessaires car elles nous permettent d'estimer le biais de la zone, la précision de la carte et l'incertitude. Une approche d'estimation basée sur l'échantillonnage peut être séparée en trois composantes différentes - le plan d'échantillonnage, le plan de réponse et l'analyse (Stehman & Czaplewski, 1998). La première composante, le plan d'échantillonnage, est illustrée dans ce tutoriel pour le cas du plan d'échantillonnage aléatoire stratifié. D'autres tutoriels ici sur OpenMRV sous le processus "Plan d'échantillonnage" explorent d'autres approches de plan d'échantillonnage (par exemple le plan d'échantillonnage aléatoire simple/systématique).
author: Pontus Olofsson
creation date: Février, 2021
language: Françai
publisher and license: Copyright 2021, Banque mondiale. Ce travail est sous licence Creative Commons Attribution 3.0 IGO

tags:
- OpenMRV
- QGIS
- GEE
- Plan d'échantillonnage
- Conception de l'échantillon
- Sélection de l'échantillon
- Échantillon
- Cadre d'échantillonnage
- Stratifié
- Colombie

group:
- catégorie : Stratifié
  étape : Echantillonnage
- catégorie : Cluster
  étape : Echantillonnage
- catégorie : Stratifié
  étape : Calcul de la superficie
- catégorie : Expansion
  étape : Calcul de la superficie
- catégorie : Modèle assisté
  étape : Calcul de la superficie
- catégorie : Ratio
  étape : Calcul de la superficie
---

# Échantillonnage aléatoire stratifié

## 1 Contexte

Une approche d'estimation basée sur l'échantillonnage peut être séparée en trois volets différents : le plan d'échantillonnage, le plan de réponse et l'analyses (Stehman & Czaplewski, 1998). La première composante, le plan d'échantillonnage, est illustrée dans ce tutoriel. Le plan d'échantillonnage définit le protocole de sélection du sous-ensemble d'unités - c'est-à-dire l'échantillon - dans une population plus large. Dans notre cas, la population est l'équivalent de la zone d'étude, et les caractéristiques de la zone d'étude, telles que la superficie d'une certaine couverture du sol, sont estimées en analysant l'échantillon. Les approches basées sur l'échantillonnage dans un contexte de télédétection sont nécessaires car elles nous permettent d'estimer le biais de zone, la précision des données et l'incertitude. Comme expliqué dans le document GFOI Methods & Guidance Document, 'estimation des zones d'occupation du sol et des changements d'occupation du sol en comptant simplement les pixels dans les cartes produira des résultats erronés en raison des erreurs de classification (GFOI, 2016, p. 125):

> Les méthodes qui produisent des estimations de données d'activité sous la forme de sommes de superficies d'unités cartographiques assignées à des classes de cartes se caractérisent par un comptage de pixels et ne prévoient généralement pas de tenir compte des effets des erreurs de classification des cartes. De plus, bien que les matrices de confusion ou d'erreur et les indices de précision des cartes puissent renseigner sur les questions d'erreurs systématiques et de précision, elles ne produisent pas directement l'information nécessaire à la construction d'intervalles de confiance. Par conséquent, les méthodes de comptage de pixels ne fournissent aucune assurance que les estimations ne sont "ni surévaluées ni sous-évaluées" ou que "les incertitudes sont réduites autant que possible". Le rôle des données de référence, également caractérisées comme des données d'évaluation de la précision, est de fournir une telle assurance en ajustant les erreurs de classification systématiques estimées et en estimant l'incertitude, fournissant ainsi les informations nécessaires à la construction d'intervalles de confiance pour la conformité avec le guide des bonnes pratiques du GIEC.

Lors du choix d'un plan d'échantillonnage, nous devons tenir compte de quelques critères de conception, mais qui sont importants. Le respect de l'échantillonnage aléatoire est de première importance. L'échantillonnage aléatoire est défini en termes de probabilités d'inclusion, où une probabilité d'inclusion concerne la probabilité qu'une unité donnée soit incluse dans l'échantillon ; la probabilité d'inclusion doit être connue pour chaque unité sélectionnée dans l'échantillon et la probabilité d'inclusion doit être supérieure à zéro pour toutes les unités de la zone d'étude (Stehman, 2009). Plusieurs plans d'échantillonnage aléatoire sont applicables à l'estimation de la précision et de la superficie, les plans les plus couramment utilisés étant le plan aléatoire simple, le plan aléatoire stratifié et le plan systématique. L'échantillonnage à deux phases (également appelé double), en deux étapes et en cluster (en grappe) est applicable mais plus complexe.

## 2 Objectifs d'apprentissage

Pour ce tutoriel spécifique, nous nous focaliserons sur le plan d'échantillonnage aléatoire stratifié.L'objectif de ce tutoriel est de fournir à l'utilisateur une compréhension des diverses décisions clés impliquées dans la conception d'un effort d'estimation basé sur l'échantillonnage. Il est important de comprendre la relation entre la taille de l'échantillon et l'allocation des unités d'échantillonnage aux strates, ainsi que les objectifs primordiaux de l'estimation tels que la précision cible. À la fin du tutoriel, l'utilisateur devrait être en mesure de choisir une méthode de sélection d'échantillon -- SYS, SRS ou STR --, Déterminer la taille de l'échantillon et l'allouer aux strates, en fonction des objectifs d'estimation pour le plan d'échantillonnage aléatoire stratifié

- Comprendre les différentes décisions clés impliquées dans la conception d'un effort d'estimation basé sur l'échantillonnage
- Choisir une méthode de sélection d'échantillon -- SYS, SRS ou STR en fonction des objectifs d'estimation.
- Déterminer la taille de l'échantillon et l'allouer à des strates, en fonction des objectifs d'estimation.

### 2.1 Pré-requis

- Révision de la terminologie pertinente pour les techniques d'échantillonnage dans le tutoriel 3.1 Terminologie
- Il est fortement conseillé d'avoir Compte Google Earth Engine (GEE). Veuillez vous référer au processus "Pré-traitement" et à l'outil "GEE" ici sur OpenMRV pour plus d'informations sur le travail dans cet environnement.

## 3 Tutoriel : Plan d'échantillonnage pour l'estimation de la superficie et de la précision  - Échantillonnage aléatoire stratifié

### 3.1 Comment choisir un plan d'échantillonnage?

Le choix d'un plan d'échantillonnage nécessite souvent des compromis entre différents critères et priorités. Le désir de fournir des estimations pour des sous-régions ou la nécessité d'atteindre des objectifs de précision devront être mis en balance avec des critères souhaitables du plan d'échantillonnage tels que la facilité et la praticabilité de la mise en œuvre, la rentabilité, la facilité d'adaptation aux changements de la taille de l'échantillon. Stehman (2009) fournit un examen détaillé des options, des objectifs et des critères du plan d'échantillonnage, mais la décision se résume généralement à trois décisions clés : l'utilisation de strates, l'utilisation de clusters (ou par grappe)et la mise en œuvre d'un protocole de sélection aléatoire systématique ou simple.

#### 3.1.1 Echatillonnnage Stratifié?

Les strates sont “des sous-populations qui ne se chevauchent pas et qui, ensemble, constituent la population entière” (Cochran, 1977, p. 89). La stratification de la zone d'étude avant la sélection de l'échantillon peut garantir que les estimations de la précision et de la superficie sont obtenues pour certaines sous-régions de la zone d'étude, et il en résulte une plus grande précision des estimations. Par conséquent, il existe plusieurs bonnes raisons d'utiliser des strates. Même avec un échantillonnage aléatoire simple, l'utilisation de strates après la sélection de l'échantillon est une bonne idée. L'échantillonnage stratifié présente un avantage évident si nous nous intéressons à une très petite proportion de la zone d'étude, comme c'est souvent le cas dans les MRV tropicaux. Par exemple, la zone de perte de forêt, même dans les pays où la déforestation est rampante, est souvent une très petite proportion du pays, surtout sur de courts intervalles de temps. L'utilisation d'une carte des pertes de forêts (et d'autres catégories) pour stratifier la zone d'étude dans de telles situations permet un échantillonnage ciblé dans des zones d'intérêt particulier. Ne pas effectuer de stratification dans de telles situations exigera une très grande taille d'échantillon.

#### 3.1.2 Utilisation d'une sélection aléatoire simple ou systématique?

La sélection systématique consiste à choisir un point de départ au hasard avec une probabilité égale, puis à échantillonner avec une distance fixe entre les emplacements d'échantillonnage. En bref, la sélection aléatoire simple est préférable si l'on recueille des observations de référence dans les données satellitaires alors que la sélection systématique est préférable si l'on visite les sites d'échantillonnage in situ (Olofsson et al. 2014). Cette recommandation se justifie par le fait que les unités sélectionnées systématiquement sont plus faciles à localiser sur le terrain tandis que la sélection aléatoire est plus facile à faire augmenter. Notez que les mêmes estimateurs sont utilisés avec la sélection aléatoire simple ou systématique.

#### 3.1.3 Echatillonnnage par grappes?

Une grappe est une unité d'échantillonnage qui consiste en une ou plusieurs unités d'évaluation de base spécifiées par le plan d'échantillonnage. Par exemple, une grappe peut être un bloc 3 × 3 de 9 pixels ou une grappe de 1 km × 1 km contenant 100 unités d'évaluation de 1 ha. Dans l'échantillonnage en grappes, un échantillon de grappes est sélectionné et les unités spatiales de chaque grappe sont donc sélectionnées en tant que groupe plutôt qu'en tant qu'entités individuelles. L'échantillonnage en deux étapes est une forme d'échantillonnage en grappes où de grandes unités primaires d'échantillonnage (UPE) sont sélectionnées à la première étape ; de plus petites unités secondaires d'échantillonnage (USE) sont sélectionnées dans chaque UPE à la deuxième étape. Ces plans ont l'avantage de ne nécessiter des données de référence (c'est-à-dire les données utilisées pour collecter les observations de référence) que sur les PSU au lieu de la zone d'étude entière comme c'est le cas avec les plans susmentionnés. Cependant, à moins que les économies ne soient considérables, les plans en grappes ne sont pas recommandés car la corrélation entre les UPE réduit souvent la précision par rapport à un simple échantillon aléatoire de taille égale, et parce qu'il s'agit de plans compliqués qu'il est difficile d'enrichir de résultats d'échantillons difficiles à analyser.

L'exemple ci-dessus illustre l'inconvénient du SRS/SYS : lorsque nous essayons d'estimer quelque chose qui représente une petite proportion de la population, une très grande taille d'échantillon est nécessaire dans le cadre du SRS/SYS. Dans de telles situations, l'échantillonnage aléatoire stratifié (EAS) est recommandé. On parle de EAS lorsque “l'échantillonnage aléatoire simple est effectué dans chaque strate” (Cochran 1977, p. 89). Par conséquent, nous divisons la population en strates et sélectionnons un échantillon dans chaque strate sous SRS (ou SYS). Le EAS ajoute un autre niveau de complexité et nous oblige à déterminer comment répartir l'unité d'échantillonnage entre les strates en plus de déterminer la taille totale de l'échantillon.

### 3.2 Échantillonnage aléatoire stratifié

La motivation pour utiliser le STR apparaît lorsque nous essayons d'estimer quelque chose qui représente une petite proportion de la population, et que dans le cadre du SRS/SYS, une très grande taille d'échantillon est nécessaire. Dans de telles situations, l'échantillonnage aléatoire stratifié (STR) est recommandé. On parle de STR lorsque " l'échantillonnage aléatoire simple est effectué dans chaque strate " (Cochran 1977, p. 89). En conséquence, nous divisons la population en strates et sélectionnons un échantillon dans chaque strate sous SRS (ou SYS). La STR ajoute un autre niveau de complexité et nous oblige à déterminer comment allouer l'unité d'échantillonnage aux strates en plus de déterminer la taille totale de l'échantillon. Pour plus d'informations sur SRS/SYS, veuillez consulter ici sur OpenMRV les tutoriels sous le processus " Plan d'échantillonnage ".
Pour plus d'informations sur le SRS/SYS, veuillez consulter ici sur OpenMRV les tutoriels sous le processus " Plan d'échantillonnage ".

#### 3.2.1 Taille de l'échantillon

Comme pour le SRS/SYS, nous devons spécifier un objectif de précision et calculer à l'aide de l'estimateur de variance STR la taille totale de l'échantillon (*n*) nécessaire pour atteindre la précision cible. En résolvant l'estimateur de variance STR, on obtient (Olofsson et al., 2014, Eq. 13. modifié à partir de Cochran, 1977, Eq 5.25)

[![img](https://camo.githubusercontent.com/2ceb9061ac9e8f8c8224ba8a4375927c1025357f1b34e260ca08185a446b1633/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f2535434c617267652673706163653b6e3d2535436c6566742673706163653b2535422535436672616325374225354373756d5f25374268253744575f6825354374657874757025374253442537445f6825374425374225354374657874253742534525374428702925374425354372696768742673706163653b25354425354532)](https://camo.githubusercontent.com/2ceb9061ac9e8f8c8224ba8a4375927c1025357f1b34e260ca08185a446b1633/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f2535434c617267652673706163653b6e3d2535436c6566742673706163653b2535422535436672616325374225354373756d5f25374268253744575f6825354374657874757025374253442537445f6825374425374225354374657874253742534525374428702925374425354372696768742673706163653b25354425354532)

*Wh* est le poids de la strate *h*, qui est simplement la superficie de la strate exprimée en proportion de la zone d'étude totale ; SD*h* est l'écart-type de la strate *h*, qui est expliqué ci-dessous. L'erreur standard cible est SE(*p*). Nous allons démontrer le calcul en utilisant une carte provenant d'un autre tutoriel ici sur OpenMRV qui peut être trouvé sous le processus "Détection de changement" et l'outil "CODED". Cette carte est une carte de perturbation, de forêt stable et de non-forêt stable et peut être trouvée en tant que ressource GEE [ici](https://code.earthengine.google.com/?asset=users/openmrv/MRV/CODED_Colombia_Stratification_No_Buffer). Le calcul de la taille de l'échantillon sous STR  peut etre compliqué, nous utiliserons donc une feuille de calcul de Google Sheets (ou Microsoft Excel si vous préférez). La feuille de calcul utilisée dans ce tutoriel est accessible ici : https://drive.google.com/file/d/1R4uMOKMmr3nXumDAFh9InQBV0m_BZ0_y/view?usp=sharing

##### Étape 1

Tout d'abord, nous devons calculer le nombre de pixels de chaque strate ; ceci peut être fait en utilisant GDAL, QGIS, Google Earth Engine, etc. ; Si vous avez utilisé l'outil "CODED" ici sur OpenMRV, ces zones sont affichées dans la *Console* de Google Earth Engine.Si ce n'est pas le cas, ou si vous avez un actif GEE existant, chargez l'actif en utilisant le script AREA2 Stratified Random Sampling (https://code.earthengine.google.com/a0164c748c4772055214d96e57f43c39) pour calculer les poids des strates. Ajoutez ces chiffres sur la première ligne "Area [px]". Dans la deuxième ligne, exprimez ces surfaces sous forme de proportion (dans la cellule B3 tapez "=B2/sum($B2:$D2") et prolongez jusqu'à E2). Ces proportions sont appelées poids des strates (*Wh*).

|      | A               | B               | C               | D              | E                 |
| ---- | --------------- | --------------- | --------------- | -------------- | ----------------- |
| 1    | Stratum (*h*)   | Forêt (1)       | Non-Forêt (2)   | For. Dist. (3) | Total             |
| 2    | Superficie [m2] | 658 196 561 513 | 462 219 395 097 | 15 594 353 281 | 1 136 010 309 891 |
| 3    | *Wh*            | 0,579           | 0,407           | 0,0137         | 1                 |

##### Étape 2

Après avoir calculé *Wh*, nous devons calculer les deux variables restantes de l'équation : l'écart-type de la strate *h* (SD*h*) et l'erreur-type cible (SE(*p*)). L'écart type de la strate *h* est un peu difficile à comprendre et nécessite une estimation de la proportion de la strate *h* qui est la classe cible (*qh*).

[![img](https://camo.githubusercontent.com/374b6595c00ff76aa1a45e320f1a76d5b307df2c27d6d6a01badd28fd1334999/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f2535434c617267652673706163653b25354374657874757025374253442537445f683d25354373717274253742715f6828312d715f6829253744)](https://camo.githubusercontent.com/374b6595c00ff76aa1a45e320f1a76d5b307df2c27d6d6a01badd28fd1334999/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f2535434c617267652673706163653b25354374657874757025374253442537445f683d25354373717274253742715f6828312d715f6829253744)

Dans notre exemple, la proportion de perturbations dans la zone d'étude est la cible, ce qui signifie que *qh* est la proportion de la strate *h* qui est une perturbation - si la carte était parfaite (ce qui n'est pas le cas !) alors *q1* (forêt) = *q2* (non-forêt) = 0 ; *q3* (perturbation) = 1 mais nous ne pouvons pas supposer que c'est le cas. Aucune carte n'est parfaite et une hypothèse plus réaliste est que, disons, 80% des perturbations dans la zone d'étude sont capturées par la classe de carte des perturbations, et que de petites fractions des strates de forêt et de non-forêt sont des perturbations en raison d'une erreur de classification. Si *q1* = 0,001, alors nous supposons que 0,001 × 658 196 561 513/30^2^ = 0,7 M pixels de perturbation dans la strate forêt. La strate non forêt étant légèrement plus petite, si nous pensons qu'une quantité similaire de perturbations est également présente dans la strate non forêt, nous devrions supposer *q2* = 0,002. Par conséquent, ajoutons ces chiffres (0,001, 0,002 et 0,8) à la ligne 4 et calculons SD*h* à la ligne 5, cellule B5 comme "=sqrt(B4*(1-B4))" et étendons à la cellule D5. Pour simplifier, calculez le produit de SD*h et de \*Wh\* à la ligne 6 de telle sorte que la cellule B6 = B3*B5 et étendez-le à D5 :

|      | A               | B               | C               | D              | E                 |
| ---- | --------------- | --------------- | --------------- | -------------- | ----------------- |
| 1    | Stratum (*h*)   | Forêt (1)       | Non-Forêt(2)    | For. Dist. (3) | Total             |
| 2    | Superficie [m2] | 658 196 561 513 | 462 219 395 097 | 15 594 353 281 | 1 136 010 309 891 |
| 3    | *Wh*            | 0,579           | 0,407           | 0,0137         | 1                 |
| 4    | *qh*            | 0,001           | 0,002           | 0,8            |                   |
| 5    | SD*h*           | 0,0316          | 0,0447          | 0,4            |                   |
| 6    | SD*h* x *Wh*    | 0,0183          | 0,01818         | 0,005491       |                   |

##### Étape 3

Fixons maintenant l'objectif de l'échantillonnage : la marge d'erreur souhaitée de la zone de perturbation. Dans la formule d'estimation de la taille de l'échantillon, l'objectif est exprimé sous la forme d'une erreur standard. Si nous visons à nouveau une marge d'erreur de 25%, alors

[![img](https://camo.githubusercontent.com/e0b8240d9bcb6bb4ba8fb111fd35fbaf6005890c54144f49afabc806eb63ab0e/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f2535434c617267652673706163653b4d64453d25354366726163253742312c393625354374696d65732535437465787475702537425345253744282535436861742537427025374429253744253742253543686174253742702537442537442535434c65667472696768746172726f7725354374657874757025374253452537442825354368617425374270253744293d253543667261632537424d644525354374696d65732673706163653b25354368617425374270253744253744253742312c39362537443d25354366726163253742302c3125354374696d6573302c3031253744253742312c39362537443d302c30303035)](https://camo.githubusercontent.com/e0b8240d9bcb6bb4ba8fb111fd35fbaf6005890c54144f49afabc806eb63ab0e/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f2535434c617267652673706163653b4d64453d25354366726163253742312c393625354374696d65732535437465787475702537425345253744282535436861742537427025374429253744253742253543686174253742702537442537442535434c65667472696768746172726f7725354374657874757025374253452537442825354368617425374270253744293d253543667261632537424d644525354374696d65732673706163653b25354368617425374270253744253744253742312c39362537443d25354366726163253742302c3125354374696d6573302c3031253744253742312c39362537443d302c30303035)

Nous utilisons ici un z-score de 1,96 qui correspond à un niveau de confiance de 95%. Si nous spécifions le MdE dans la cellule D7, nous pouvons alors calculer l'erreur standard cible dans la cellule D8 :"=(D7/100)*D3/2":

|      | A               | B               | C               | D              | E                 |
| ---- | --------------- | --------------- | --------------- | -------------- | ----------------- |
| 1    | Stratum (*h*)   | Forêt (1)       | Non-Forêt (2)   | For. Dist. (3) | Total             |
| 2    | Superficie [m2] | 658 196 561 513 | 462 219 395 097 | 15 594 353 281 | 1 136 010 309 891 |
| 3    | *Wh*            | 0,579           | 0,407           | 0,0137         | 1                 |
| 4    | *qh*            | 0,001           | 0,002           | 0,8            |                   |
| 5    | SD*h*           | 0,0316          | 0,0447          | 0,4            |                   |
| 6    | SD*h* x *Wh*    | 0,0183          | 0,01818         | 0,005491       |                   |
| 7    | MoE [%]         |                 |                 | 25             |                   |
| 8    | SE(*p^*)        |                 |                 | 0,0017         |                   |

##### Étape 4

Enfin, nous pouvons maintenant calculer facilement la taille de l'échantillon à la ligne 8, cellule E9 comme suit :"=(sum(B6:D6)/B7)^2"

|      | A               | B               | C               | D              | E                 |
| ---- | --------------- | --------------- | --------------- | -------------- | ----------------- |
| 1    | Stratum (*h*)   | Forêt (1)       | Non-Forêt(2)    | For. Dist. (3) | Total             |
| 2    | Superficie [m2] | 658 196 561 513 | 462 219 395 097 | 15 594 353 281 | 1 136 010 309 891 |
| 3    | *Wh*            | 0,579           | 0,407           | 0,0137         | 1                 |
| 4    | *qh*            | 0,001           | 0,002           | 0,8            |                   |
| 5    | SD*h*           | 0,0316          | 0,0447          | 0,4            |                   |
| 6    | SD*h* x *Wh*    | 0,0183          | 0,01818         | 0,005491       |                   |
| 7    | MdE [%]         |                 |                 | 25             |                   |
| 8    | SE(*p^*)        |                 |                 | 0,00172        |                   |
| 9    | *n*             |                 |                 |                | 599               |

ce qui donne une taille d'échantillon de 599 -- c'est-à-dire environ 1/8 de la taille d'échantillon de 4 600 requise par le SRS pour atteindre la même précision. Pour modifier la précision cible, il nous suffit maintenant d'ajuster notre précision cible dans la cellule D7.

#### 3.2.2 Strates tampons

Un problème potentiel dans la situation ci-dessus est que les omissions de perturbations présentes dans la strate de forêt auront un impact important sur la précision des estimations. Ces erreurs d'omission sont des unités d'échantillon dans la strate forêt qui ont été observées dans les données de référence comme étant des perturbations. La question est expliquée en détail dans Olofsson et al. (2020) aet ici nous reconnaissons simplement que la "contribution à l'incertitude" des erreurs d'omission dépend dans une large mesure de la taille de la strate dans laquelle elles se produisent. Nous souhaitons donc diminuer la taille de la strate forêt qui représente actuellement 83% de la zone d'étude. En particulier, nous voulons créer de petites substrats où les omissions de perturbations sont susceptibles de se produire. Une approche explorée dans la littérature est la création de strates tampons autour des strates de changement -- le raisonnement est que les erreurs sont susceptibles de se produire près des changements correctement cartographiés. Dans notre cas, une telle strate tampon pourrait être définie comme les pixels de la strate forêt adjacente à la perturbation.

Illustrons la création d'un tampon. Cliquez sur ce lien : Un script pour créer un tampon dans la sortie de l'outil "CODED" ici sur OpenMRV est disponible dans AREA2: https://code.earthengine.google.com/23d803fa4162f691ae456d07ff634299.
Vous pouvez également utiliser cette carte existante de la Colombie basée sur le CODED avec un tampon :
https://code.earthengine.google.com/?asset=users/olofsson76/Open_MRV/Open_MRV_Col_strat_buffer Pour obtenir les poids des strates, ouvrez le script dans AREA2 pour sélectionner un échantillon sous échantillonnage aléatoire stratifié : [https://code.earthengine.google.com/a0164c748c4772055214d96e57f43c39](https://code.earthengine.google.com/?accept_repo=users%2Fopenmrv%2FMRV&scriptPath=projects%2FAREA2%2Fpublic%3A1. Sampling Design%2FStratified Random Sampling) et spécifier le chemin d'accès à la carte de la Colombie basée sur la CODED avec un tampon sous "Specify stratification/image to define study area" ; utiliser les autres arguments par défaut, cliquer sur "Load image" qui affichera les zones de strates dans la console (NOTE : cela prendra un certain temps). J'obtiens les zones suivantes : Forêt (0), Non-forêt (1), Perturbation de la forêt (2) et une zone tampon-2 pixels (3). [m^2^]:

0: 625 597 113 080 1: 462 219 395 097 2: 15 594 353 281 3: 32 599 448 433

Ajoutons ces chiffres dans un deuxième onglet de la feuille de calcul et calculons les poids des strates :

|      | A               | B               | C               | D              | E              | F                 |
| ---- | --------------- | --------------- | --------------- | -------------- | -------------- | ----------------- |
| 1    | Stratum (*h*)   | Forêt (1)       | Non-Forêt (2)   | For. Dist. (3) | FD buf. (4)    | Total             |
| 2    | Superficie [m2] | 625 597 113 080 | 462 219 395 097 | 15 594 353 281 | 32 599 448 433 | 1 136 010 309 891 |
| 3    | *Wh*            | 0,551           | 0,407           | 0,0137         | 0,0287         | 1                 |

Si nous pensons que la strate tampon est efficace pour capturer les erreurs d'omission, nous pouvons diminuer *qh* pour la strate forêt -- si nous supposons que la moitié des pixels de perturbation dans la strate forêt seront "capturés" par la strate tampon, alors *q1* = 0,0005 et *q4* = 0,0075. Avec une marge d'erreur cible de 25%, la taille de l'échantillon tombe à 502.

|      | A               | B               | C               | D              | E              | F                 |
| ---- | --------------- | --------------- | --------------- | -------------- | -------------- | ----------------- |
| 1    | Stratum (*h*)   | Forêt (1)       | Non-Forêt (2)   | For. Dist. (3) | FD buf. (4)    | Total             |
| 2    | Superficie [m2] | 625 597 113 080 | 462 219 395 097 | 15 594 353 281 | 32 599 448 433 | 1 136 010 309 891 |
| 3    | *Wh*            | 0,551           | 0,407           | 0,0137         | 0,0287         | 1                 |
| 4    | *qh*            | 0,0005          | 0,002           | 0,8            | 0,0075         |                   |
| 5    | SD*h*           | 0,0223          | 0,04468         | 0,4            | 0,086277       |                   |
| 6    | SD*h* x *Wh*    | 0,0123          | 0,01818         | 0,005491       | 0,002475       |                   |
| 7    | *MdE* [%]       |                 |                 | 25             |                |                   |
| 8    | SE(*p^*)        |                 |                 | 0,001716       |                |                   |
| 9    | *n*             |                 |                 |                |                | 502               |

Un tampon de trois pixels a été utilisé ici à titre d'exemple. Pour plus d'informations sur la manière de déterminer la taille des strates de la mémoire tampon, voir Olofsson et al. (2020).

#### 3.2.3 Allocation

Supposons que nous ayons choisi une marge d'erreur de 15% avec une strate tampon et une taille d'échantillon de 958. Nous devons maintenant décider comment allouer l'échantillon aux strates. En bref, une allocation proportionnelle aux poids des strates est efficace pour estimer les paramètres qui incluent des calculs entre strates -- ces paramètres sont notamment la surface, la précision globale et la précision du producteur. L'estimation de la précision de l'utilisateur est basée sur des calculs au sein des strates qui bénéficient d'une allocation égale. L'obtention d'une précision élevée de la précision de l'utilisateur est rarement un objectif d'estimation, ce qui suggère qu'une allocation proportionnelle est préférable. Revenons à la feuille de calcul, calculons sur la ligne 10 la taille de l'échantillon dans chaque strate suivant une allocation proportionnelle : dans la cellule B10 : "=B3*$F$9" et prolongez jusqu'à E10.

|      | A               | B               | C               | D              | E              | F                 |
| ---- | --------------- | --------------- | --------------- | -------------- | -------------- | ----------------- |
| 1    | Stratum (*h*)   | Forêt (1)       | Non-Forêt (2)   | For. Dist. (3) | FD buf. (4)    | Total             |
| 2    | Superficie [m2] | 625 597 113 080 | 462 219 395 097 | 15 594 353 281 | 32 599 448 433 | 1 136 010 309 891 |
| 3    | *Wh*            | 0,551           | 0,407           | 0,0137         | 0,0287         | 1                 |
| 4    | *qh*            | 0,0005          | 0,002           | 0,8            | 0,0075         |                   |
| 5    | SD*h*           | 0,0223          | 0,04468         | 0,4            | 0,086277       |                   |
| 6    | SD*h* x *Wh*    | 0,0123          | 0,01818         | 0,005491       | 0,002475       |                   |
| 7    | *MdE* [%]       |                 |                 | 25             |                |                   |
| 8    | SE(*p^*)        |                 |                 | 0.001716       |                |                   |
| 9    | *n*             |                 |                 |                |                | 502               |
| 10   | *nh* (prop.)    | 277             | 204             | 7              | 14             | 502               |

Cela semble raisonnable mais nous avons besoin d'au moins 30 unités par strate, donc à la ligne 11, augmentons la taille de l'échantillon dans la strate de perturbation à 30 et arrondissons les tailles d'échantillon dans la strate forêt à 275 et la strate non-forêt à 200. Cela donne l'allocation finale.

|      | A               | B               | C               | D              | E              | F                 |
| ---- | --------------- | --------------- | --------------- | -------------- | -------------- | ----------------- |
| 1    | Stratum (*h*)   | Forêt (1)       | Non-Forêt(2)    | For. Dist. (3) | FD buf. (4)    | Total             |
| 2    | Superficie [m2] | 625 597 113 080 | 462 219 395 097 | 15 594 353 281 | 32 599 448 433 | 1 136 010 309 891 |
| 3    | *Wh*            | 0,551           | 0,407           | 0,0137         | 0,0287         | 1                 |
| 4    | *qh*            | 0,0005          | 0,002           | 0,8            | 0,0075         |                   |
| 5    | SD*h*           | 0,0223          | 0,04468         | 0,4            | 0,086277       |                   |
| 6    | SD*h* x *Wh*    | 0,0123          | 0,01818         | 0,005491       | 0,002475       |                   |
| 7    | *MoE* [%]       |                 |                 | 25             |                |                   |
| 8    | SE(*p^*)        |                 |                 | 0,001716       |                |                   |
| 9    | *n*             |                 |                 |                |                | 502               |
| 10   | *nh* (prop.)    | 277             | 204             | 7              | 14             | 502               |
| 11   | *nh* (final)    | 275             | 200             | 30             | 30             | 535               |

La raison pour laquelle 30 est considéré comme la taille minimale de l'échantillon est mieux décrite par Lohr (1999)!:

> Le terme imprécis "suffisamment grand" apparaît dans le théorème central limite parce que l'adéquation de l'approximation normale dépend de n et du degré de ressemblance de la population {yi, i = 1, ... , N} ressemble à une population générée à partir de la distribution normale. Le "nombre magique" de n = 30 [est] souvent cité dans les ouvrages d'introduction aux statistiques comme une taille d'échantillon "suffisamment grande" pour que le théorème central limite s'applique

Le théorème de la limite centrale est important car il stipule que la somme de variables aléatoires indépendantes est normalement distribuée même si les variables elles-mêmes ne le sont pas. Par exemple, le théorème nous permet de construire des intervalles de confiance en utilisant des z-scores communs et une erreur standard.

### 3.3 Échantillonnage en deux étapes/cluster ou par grappes

En raison de la complexité associée à l'échantillonnage à deux phases, il y a beaucoup moins d'exemples de ce type de plans dans la littérature que de plans STR et SRS/SYS. De plus, il n'existe pas de règles fixes pour guider la taille de l'échantillon et des unités primaires d'échantillonnage (UPE), si ce n'est de trouver un compromis entre le nombre global d'observations et un niveau raisonnable d'incertitude pour les estimations au sein des UPE (Sannier et al., 2013). IAu lieu de créer des exemples, nous allons parcourir deux exemples dans la littérature.

Le premier exemple est celui de Potapov et al. (2014) qui ont estimé la superficie de la perte de forêt 2000-2011 à travers l'Amazonie péruvienne à l'appui de REDD+. La principale source de données de référence était l'imagerie commerciale haute résolution ; une conception en deux étapes a été choisie à des fins d'économie, car le budget ne permettait d'acheter que 30 jeux de données haute résolution. Dans une conception en deux étapes, les données de référence ne sont nécessaires que pour les UPE et non pour l'ensemble de la zone d'étude. Par conséquent, la taille de l'échantillon des 30 UPE a été déterminée sur la base de raisons budgétaires et non en spécifiant une précision cible comme dans les exemples ci-dessus. La taille des PSUs de 12 × 12 km a été choisie pour s'aligner sur les images à haute résolution. Les 5 532 blocs, chacun de 12 × 12 km, couvrant la zone d'étude ont été séparés en une strate de changement forestier élevé (337 blocs) et faible (5 195 blocs), à partir desquels 21 et 9 UPE ont été sélectionnées dans le cadre de la STR. (Cette sélection a été guidée par les règles d'allocation optimale de l'échantillon de Cochran (1977).) Dans chacune des 30 UPE, 100 unités d'échantillonnage secondaires (UES) ont été sélectionnées dans le cadre du SRS lors de la deuxième étape de l'échantillonnage.

Un deuxième exemple est fourni par Sannier et al. (2013) qui ont estimé la proportion de la couverture de la forêt et la déforestation nette au Gabon en utilisant un échantillonnage à deux étapes. L'échantillonnage à deux étapes a été choisi car il représentait un compromis entre la facilité de collecte des données et la distribution géographique. La zone d'étude a été divisée en 251 blocs de 20 × 20 km, chacun d'entre eux étant à son tour divisé en 100 blocs de 2 × 2 km. Lors de la première étape, une UPE de 2 × 2 km a été sélectionnée dans chacun des 251 blocs de 20 × 20 km sous SRS. Dans la deuxième étape, 50 SSU correspondant à un pixel Landsat ont été sélectionnées dans le cadre du SRS.

### 3.4 Logiciel permettant d'estimer la taille de l'échantillon

SEPAL/CEO a un support intégré pour estimer la taille de l'échantillon comme expliqué dans [cette documentation](https://sepal-ceo.readthedocs.io/en/latest/).

Similaire à SEPAL est cette feuille de calcul développée par la Banque Mondiale qui calcule également la taille de l'échantillon nécessaire pour atteindre une précision de l'exactitude globale https://onedrive.live.com/view.aspx?resid=9815683804F2F2C7!37340&ithint=file%2cxlsx&authkey=!ANcP-Xna7Knk_EE

### 3.5 Sélection de l'échantillon

La dernière étape du plan d'échantillonnage consiste à tirer physiquement l'échantillon de la zone d'étude, qui est abordé ici sur OpenMRV sous le processus "Plan d'échantillonnage" et les outils "QGIS", "GEE", "AREA2".

## 4 Foire aux questions

**Je ne comprends pas la variable qh qui est utilisée pour calculer la taille de l'échantillon sous STR - qu'est-ce qu'elle signifie ?**

La variable *qh* est nécessaire pour calculer l'écart-type de la strate *h* et représente la proportion de la strate *h* qui est la classe cible. Dans l'exemple ci-dessus, nous avons trois strates (avant la création de la strate tampon), *h* = 1 est forestière, *h* = 2 est non forestière, et *h* = 3 est une perturbation de type forêt, cette dernière étant la classe cible. Dans ce cas, *qh* est la proportion de perturbations de forêt dans chaque strate. Si la carte était parfaite, alors toutes les perturbations forestières de la zone d'étude seraient présentes dans la strate des perturbations forestières et donc *q3* = 1, tandis que *q1* et *q2* seraient égaux à zéro. Aucune carte n'est parfaite et nous devrons supposer un certain niveau d'erreur de classification. Notez que cette information est inconnue au stade de la conception et qu'il est nécessaire de faire des suppositions. Par exemple, si *q3* = 0,8, nous supposons que 80 % des perturbations forestières de l'étude sont présentes dans la strate des perturbations forestières. Si *q1* = 0,001, nous supposons que 0,1 % de la strate forestière est une perturbation de forêt.

**Je n'ai aucune idée de la façon dont on détermine les valeurs de qh - que dois-je faire ?**

La variable *qh* est essentiellement une indication de la façon dont la stratification capture la classe d'intérêt. Étant donné que des cartes sont généralement utilisées pour stratifier la zone d'étude, je vous conseille de vérifier l'exactitude des cartes précédentes de la même zone. Notez que *qh* pour *h* = la classe d'intérêt, est la précision anticipée de l'utilisateur de la classe d'intérêt.

**Comment déterminer une erreur standard souhaitée?**

Certains programmes spécifient une précision souhaitée ou requise ; le Forest Carbon Partnership Facility (FCPF), par exemple, stipule une marge d'erreur de 30% au niveau de confiance de 95% pour les estimations de surface des données d'activité. La marge d'erreur est égale à 1,96 fois l'erreur standard divisée par l'estimation de la superficie. Lorsque de telles exigences de précision ne sont pas spécifiées, une erreur standard cible doit être déterminée sur la base d'autres critères. Il est à noter que plus la proportion de surface de la classe recherchée est faible, plus l'échantillon doit être important pour atteindre une faible marge d'erreur. Par conséquent, pour les petites proportions de surface, la précision ciblée devra être allégée pour éviter d'avoir à sélectionner un très grand échantillon.

**Si j'utilise une strate tampon, combien de pixels doit-elle avoir**

Il est difficile de fournir des recommandations car la taille du tampon dépendra des situations. Un tampon plus grand "capturera" probablement plus d'erreurs d'omission mais aura un poids de strate plus grand. Un tampon plus grand est recommandé dans les situations d'une petite classe d'intérêt en présence d'une grande strate stable (comme une forêt stable). Les exemples dans la littérature vont de 1 à 3 pixels. Une exploration plus détaillée de l'impact de la taille du tampon est présentée dans Olofsson et al. (2020).

## 5 Terminologie relative aux techniques d'échantillonnage

Une liste de termes relatifs aux techniques d'échantillonnage et d'inférence est fournie dans la documentation d'AREA2 : https://area2.readthedocs.io/en/latest/definitions.html Vous trouverez ci-dessous quelques termes supplémentaires qui ne figurent pas dans la documentation d'AREA2.

### 5.1 Plan de réponse

Défini par (Stehman and Czaplewski, 1998): “La référence ou classe réelle est obtenue pour chaque unité d'échantillonnage sur la base de l'interprétation de photographies aériennes ou de vidéographies, d'une observation au sol ou d'une combinaison de ces sources. Les méthodes utilisées pour déterminer cette référence de classification sont appelées "plan de réponse". Le plan d'intervention comprend les procédures de collecte des informations relatives à la détermination de la occupation du sol de référence, et les règles d'attribution d'une ou plusieurs [labels] de référence à chaque unité d'échantillonnage.” Connu sous le nom de “plan de mesure” par Särndal et al. (1992).

### 5.2 Echantillon

Un sous-ensemble de la population sélectionné parmi les unités de la population.

### 5.3 Plan d'échantillonnage

Synonyme de plan d'échantillonnage (Sampling Design), qui est le terme préféré dans la littérature de référence (Cochran, 1977, Särndal et al., 1992). Le terme apparaît chez Rice (1995) ui utilise à la fois “plan d'echantillonnage” et “plan d'echantillon”.

### 5.4 Plan d'échantillonnage

“Le concept de plan d'échantillonnage (sampling design ) est le protocole par lequel les unités de référence de l'échantillon sont sélectionnées” (Stehman and Czaplewski, 1998). Le terme “Sampling design” est également utilisé par Cochran (1977) and Särndal et al. (1992) -- Le premier utilise également “sampling plan”.

### 5.5 Sondage/Enquêtee

Särndal et al. (1992) définissent une enquête comme une “investigation partielle d'une population finie”, et précisent que “les concepts d ‘enquête’ et ‘enquête par sondage’ sont utilisés pour désigner des enquêtes statistiques présentant les caractéristiques méthodologiques suivantes: [...] échantillonnage aléatoire [...] plan de mesure [et] estimation”. de facon plus precise une enquete par sondage ou un sondage est une enquête effectuee sur une partie de la population. Cette fraction de la population constitue l'échantillon et les méthodes qui permettent de construire cet echantillon s'appellent méthode d'échantillonnage.

### 5.6 Plan d'enquête

UN “plan de sondage total” définit les procédures pour “obtenir la plus grande précision possible dans les estimations de l'enquête tout en trouvant un équilibre entre les erreurs d'échantillonnage et les erreurs non dues à l'échantillonnage [...] Le plan de sondage donne lieu à des opérations d'enquête” sélection de l'échantillon (Särndal et al., 1992). Lohr (1999) décrit un plan de sondage total comme “Une philosophie de conception d'enquête visant à minimiser les erreurs de non-échantillonnage ainsi que les erreurs d'échantillonnage..” De plus, dans Lohr (1999) “plan d'enquête” est synonyme de plan d'échantillonnage.

## 6 References

Cochran, W.G., 1977. *Sampling Techniques*, John Wiley & Sons, New York, NY.

GFOI. 2016. *Integration of remote-sensing and ground-based observations for estimation of emissions and removals of greenhouse gases in forests: Methods and guidance from the Global Forest Observations Initiative* (2nd ed.), UN Food and Agriculture Organization, Rome.

Lohr, S.L., 1999. *Sampling: Design And Analysis,* CRC Press.

Olofsson, P., Arévalo, P., Espejo, A.B., Green, C., Lindquist, E., McRoberts, R.E. and Sanz, M.J., 2020. Mitigating the effects of omission errors on area and area change estimates. Remote Sensing of Environment, 236, p.111492. https://doi.org/10.1016/j.rse.2019.111492

Olofsson, P., Foody, G.M., Herold, M., Stehman, S.V., Woodcock, C.E. and Wulder, M.A., 2014. Good practices for estimating area and assessing accuracy of land change. Remote Sensing of Environment, 148, pp.42-57. https://doi.org/10.1016/j.rse.2014.02.015

Potapov, P.V., Dempewolf, J., Talero, Y., Hansen, M.C., Stehman, S.V., Vargas, C., Rojas, E.J., Castillo, D., Mendoza, E., Calderón, A. and Giudice, R., 2014. National satellite-based humid tropical forest change assessment in Peru in support of REDD+ implementation. Environmental Research Letters, 9(12), p.124012. https://doi.org/10.1088/1748-9326/9/12/124012

Rice, J.A., 1995. Mathematical Statistics and Data Analysis (2nd ed.), Duxbury Press, Belmont, CA.

Sannier, C., McRoberts, R.E., Fichet, L.V. and Makaga, E.M.K., 2014. Using the regression estimator with Landsat data to estimate proportion forest cover and net proportion deforestation in Gabon. Remote Sensing of Environment, 151, pp.138-148. https://doi.org/10.1016/j.rse.2013.09.015

Särndal, C.E., Svensson, B.H., & Wretman, J.H., 1992. Model assisted survey sampling, Springer Science & Business Media, New York, NY.

Stehman, S.V., 2009. Sampling designs for accuracy assessment of land cover. International Journal of Remote Sensing, 30(20), pp.5243-5272. https://doi.org/10.1080/01431160903131000

Stehman, S.V., & Czaplewski, R.L., 1998. Design and analysis for thematic map accuracy assessment: fundamental principles. *Remote Sensing of Environment*, 64(3), 331-344. https://doi.org/10.1016/S0034-4257(98)00010-8

-----

![](./figures/cc.png)  

Cette œuvre est soumise à une licence [Creative Commons Attribution 3.0 IGO](https://creativecommons.org/licenses/by/3.0/igo/)

Copyright 2021, Banque Mondiale. 

Ce travail a été développé par Pontus Olofsson dans le cadre d'un contrat de la Banque mondiale avec GRH Consulting, LLC pour le développement de nouvelles ressources - et la collecte de ressources existantes - liées à la mesure, la communication et la vérification pour soutenir la mise en œuvre du MRV dans les pays.

Matériel révisé par :   
Ana Mirian Villalobos, El Salvador, Ministry of Environment and Natural Resources  
Carole Andrianirina, Madagascar, National Coordination Bureau REDD+ (BNCCREDD)  
Foster Mensah, Ghana, Center for Remote Sensing and Geographic Information Services (CERGIS)    
Jennifer Juliana Escamilla Valdez, El Salvador, Ministry of Environment and Natural Resources   
Paula Andrea Paz, Colombia, International Center for Tropical Agriculture (CIAT)    
Phoebe Oduor, Kenya, Regional Centre For Mapping Of Resources For Development (RCMRD)   
Rajesh Bahadur Thapa, Nepal, International Centre for Integrated Mountain Development (ICIMOD)    
Tatiana Nana, Cameroon, REDD+ Technical Secretariat 

Attribution  
Olofsson, P. 2021. Stratified random sampling. © World Bank. License: [Creative Commons Attribution license (CC BY 3.0 IGO)](http://creativecommons.org/licenses/by/3.0/igo/)

![](figures/wb_fcfc_gfoi.png)

