---
title: Simple random/systematic sampling
summary: Sampling-based approaches in a remote sensing or geographical context are necessary because they allow us to estimate area bias, map accuracy and uncertainty. A sampling-based approach to estimation can be separated into three different components - sampling design, response design and analysis (Stehman & Czaplewski, 1998). The first component, sampling design, is illustrated in this tutorial for the case of simple random/systematic sampling design. Other tutorials here on OpenMRV under process "Sampling design" explore other sampling design approaches (e.g. Stratified Random Sampling).
author: Pontus Olofsson
creation date: February, 2021
language: English
publisher and license: Copyright 2021, World Bank. This work is licensed under a Creative Commons Attribution 3.0 IGO

tags:
- OpenMRV
- Landsat
- Sentinel 2
- Sentinel 1
- GEE
- QGIS
- AREA2
- Cloud cover
- Optical sensors
- Remote sensing
- Composite
- Mosaic
- Time series
- Change detection
- Land cover mapping
- Forest mapping
- Deforestation mapping
- Degradation mapping
- Forest degradation mapping
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

# Simple random/systematic sampling

## 1 Contexte

Une approche d'estimation basée sur l'échantillonnage peut être séparée en trois volets différents : le plan d'échantillonnage, le plan de réponse et l'analyses (Stehman & Czaplewski, 1998)[^fn1]. La première composante, le plan d'échantillonnage, est illustrée dans ce tutoriel. Le plan d'échantillonnage définit le protocole de sélection du sous-ensemble d'unités - c'est-à-dire l'échantillon - dans une population plus large. Dans notre cas, la population est l'équivalent de la zone d'étude, et les caractéristiques de la zone d'étude, telles que la superficie d'une certaine couverture du sol, sont estimées en analysant l'échantillon. Les approches basées sur l'échantillonnage dans un contexte de télédétection sont nécessaires car elles nous permettent d'estimer le biais de zone, la précision des données et l'incertitude. Comme expliqué dans le document GFOI Methods & Guidance Document, 'estimation des zones d'occupation du sol et des changements d'occupation du sol en comptant simplement les pixels dans les cartes produira des résultats erronés en raison des erreurs de classification (GFOI, 2016, p. 125)[^fn2]:

> Les méthodes qui produisent des estimations de données d'activité sous la forme de sommes de superficies d'unités cartographiques assignées à des classes de cartes se caractérisent par un comptage de pixels et ne prévoient généralement pas de tenir compte des effets des erreurs de classification des cartes. De plus, bien que les matrices de confusion ou d'erreur et les indices de précision des cartes puissent renseigner sur les questions d'erreurs systématiques et de précision, elles ne produisent pas directement l'information nécessaire à la construction d'intervalles de confiance. Par conséquent, les méthodes de comptage de pixels ne fournissent aucune assurance que les estimations ne sont "ni surévaluées ni sous-évaluées" ou que "les incertitudes sont réduites autant que possible". Le rôle des données de référence, également caractérisées comme des données d'évaluation de la précision, est de fournir une telle assurance en ajustant les erreurs de classification systématiques estimées et en estimant l'incertitude, fournissant ainsi les informations nécessaires à la construction d'intervalles de confiance pour la conformité avec le guide des bonnes pratiques du GIEC.

Lors du choix d'un plan d'échantillonnage, nous devons tenir compte de quelques critères de conception, mais qui sont importants. Le respect de l'échantillonnage aléatoire est de première importance. L'échantillonnage aléatoire est défini en termes de probabilités d'inclusion, où une probabilité d'inclusion concerne la probabilité qu'une unité donnée soit incluse dans l'échantillon ; la probabilité d'inclusion doit être connue pour chaque unité sélectionnée dans l'échantillon et la probabilité d'inclusion doit être supérieure à zéro pour toutes les unités de la zone d'étude (Stehman, 2009)[^fn3]. Plusieurs plans d'échantillonnage aléatoire sont applicables à l'estimation de la précision et de la superficie, les plans les plus couramment utilisés étant le plan aléatoire simple, le plan aléatoire stratifié et le plan systématique. L'échantillonnage à deux phases (également appelé double), en deux étapes et en cluster (en grappe) est applicable mais plus complexe.

## 2 Objectifs d'apprentissage

L'objectif de ce tutoriel est de fournir à l'utilisateur une compréhension des diverses décisions clés impliquées dans la conception d'un effort d'estimation basé sur l'échantillonnage. Il est important de comprendre la relation entre la taille de l'échantillon et l'allocation des unités d'échantillonnage aux strates, ainsi que les objectifs primordiaux de l'estimation tels que la précision cible. À la fin du tutoriel, l'utilisateur devrait être en mesure de choisir une méthode de sélection d'échantillon -- SYS, SRS ou STR --, de déterminer la taille de l'échantillon et d'allouer l'échantillon aux strates, en fonction des objectifs liés à l'estimation.

- Comprendre les différentes décisions clés impliquées dans la conception d'un effort d'estimation basé sur l'échantillonnage
- Choisir une méthode de sélection d'échantillon -- SYS, SRS ou STR en fonction des objectifs d'estimation.
- Déterminer la taille de l'échantillon et l'allouer à des strates, en fonction des objectifs d'estimation.

### 2.1 Prérequis pour ce module

- Révision de la terminologie pertinente pour les techniques d'échantillonnage dans le tutoriel 3.1 Terminologie
- Il est fortement conseillé de comprendre les tutoriels précédents des modules 1 et 2.

## 3 Tutorial: Sampling design for estimation of area and map accuracy - Simple random/systematic sampling

### 3.1 Comment choisir un plan d'échantillonnage?

Le choix d'un plan d'échantillonnage nécessite souvent des compromis entre différents critères et priorités. Le désir de fournir des estimations pour des sous-régions ou la nécessité d'atteindre des objectifs de précision devront être mis en balance avec des critères souhaitables du plan d'échantillonnage tels que la facilité et la praticabilité de la mise en œuvre, la rentabilité, la facilité d'adaptation aux changements de la taille de l'échantillon. Stehman (2009)[^fn3] fournit un examen détaillé des options, des objectifs et des critères du plan d'échantillonnage, mais la décision se résume généralement à trois décisions clés : l'utilisation de strates, l'utilisation de clusters (ou par grappe)et la mise en œuvre d'un protocole de sélection aléatoire systématique ou simple.

#### 3.1.1 Echatillonnnage Stratifié?

Les strates sont “des sous-populations qui ne se chevauchent pas et qui, ensemble, constituent la population entière” (Cochran, 1977, p. 89)[^fn4]. La stratification de la zone d'étude avant la sélection de l'échantillon peut garantir que les estimations de la précision et de la superficie sont obtenues pour certaines sous-régions de la zone d'étude, et il en résulte une plus grande précision des estimations. Par conséquent, il existe plusieurs bonnes raisons d'utiliser des strates. Même avec un échantillonnage aléatoire simple, l'utilisation de strates après la sélection de l'échantillon est une [bonne idée](https://github.com/openmrv/MRV/blob/main/Formatted/Modules_3_fr/3_1_sampling_design_french.md###markdown-header-3.1-Post-stratification). L'échantillonnage stratifié présente un avantage évident si nous nous intéressons à une très petite proportion de la zone d'étude, comme c'est souvent le cas dans les MRV tropicaux. Par exemple, la zone de perte de forêt, même dans les pays où la déforestation est rampante, est souvent une très petite proportion du pays, surtout sur de courts intervalles de temps. L'utilisation d'une carte des pertes de forêts (et d'autres catégories) pour stratifier la zone d'étude dans de telles situations permet un échantillonnage ciblé dans des zones d'intérêt particulier. Ne pas effectuer de stratification dans de telles situations exigera une très grande taille d'échantillon.

#### 3.1.2 Utilisation d'une sélection aléatoire simple ou systématique?

La sélection systématique consiste à choisir un point de départ au hasard avec une probabilité égale, puis à échantillonner avec une distance fixe entre les emplacements d'échantillonnage. En bref, la sélection aléatoire simple est préférable si l'on recueille des observations de référence dans les données satellitaires alors que la sélection systématique est préférable si l'on visite les sites d'échantillonnage in situ (Olofsson et al. 2014)[^fn5]. Cette recommandation se justifie par le fait que les unités sélectionnées systématiquement sont plus faciles à localiser sur le terrain tandis que la sélection aléatoire est plus facile à faire augmenter. Notez que les mêmes estimateurs sont utilisés avec la sélection aléatoire simple ou systématique.

#### 3.1.3 Echatillonnnage par grappes?

Une grappe est une unité d'échantillonnage qui consiste en une ou plusieurs unités d'évaluation de base spécifiées par le plan d'échantillonnage. Par exemple, une grappe peut être un bloc 3 × 3 de 9 pixels ou une grappe de 1 km × 1 km contenant 100 unités d'évaluation de 1 ha. Dans l'échantillonnage en grappes, un échantillon de grappes est sélectionné et les unités spatiales de chaque grappe sont donc sélectionnées en tant que groupe plutôt qu'en tant qu'entités individuelles. L'échantillonnage en deux étapes est une forme d'échantillonnage en grappes où de grandes unités primaires d'échantillonnage (UPE) sont sélectionnées à la première étape ; de plus petites unités secondaires d'échantillonnage (USE) sont sélectionnées dans chaque UPE à la deuxième étape. Ces plans ont l'avantage de ne nécessiter des données de référence (c'est-à-dire les données utilisées pour collecter les observations de référence) que sur les PSU au lieu de la zone d'étude entière comme c'est le cas avec les plans susmentionnés. Cependant, à moins que les économies ne soient considérables, les plans en grappes ne sont pas recommandés car la corrélation entre les UPE réduit souvent la précision par rapport à un simple échantillon aléatoire de taille égale, et parce qu'il s'agit de plans compliqués qu'il est difficile d'enrichir de résultats d'échantillons difficiles à analyser.

### 3.2 Échantillonnage aléatoire simple/systématique

Si les unités (par exemple, les pixels) d'une population/zone d'étude sont numérotées de 1 to *N*, 'échantillonnage aléatoire simple (EAS) est “une méthode permettant de sélectionner *n* unités parmi les *N* de telle sorte que chacune des [ensembles de *n* unités spécifiées] ait une probabilité égale d'être tirée” (Cochran 1977, p. 18)[^fn4]. Dans un contexte de la teledetection, nous sommes souvent intéressés par l'estimation d'une proportion de la population/zone d'étude, telle que la proportion de surface d'une certaine occupation du sol ou d'un changement d'occupation du sol, à partir des données de l'échantillon. En utilisant les notions de Cochran, les unités d'une population sont [![img](https://camo.githubusercontent.com/24075d79a1be7cdb61571f6a8ceb68d58a6c3c1399369df900c56d923f9316e1/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f6769662e6c617465783f253543696e6c696e652673706163653b795f312673706163653b2535436c646f74732673706163653b795f4e)](https://camo.githubusercontent.com/24075d79a1be7cdb61571f6a8ceb68d58a6c3c1399369df900c56d923f9316e1/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f6769662e6c617465783f253543696e6c696e652673706163653b795f312673706163653b2535436c646f74732673706163653b795f4e) à partir desquelles un échantillon [![img](https://camo.githubusercontent.com/6e5cd92f578094ee5fda46b4e476e5661801cf207fe1ef9b903ed86f9a8457fa/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f6769662e6c617465783f253543696e6c696e652673706163653b795f312673706163653b2535436c646f74732673706163653b795f6e)](https://camo.githubusercontent.com/6e5cd92f578094ee5fda46b4e476e5661801cf207fe1ef9b903ed86f9a8457fa/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f6769662e6c617465783f253543696e6c696e652673706163653b795f312673706163653b2535436c646f74732673706163653b795f6e) est sélectionné sous SRS ; on consigne [![img](https://camo.githubusercontent.com/52cdecab550e057a3a14457e68aa90be99952930db7abe33da4b146e45764dd2/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f6769662e6c617465783f253543696e6c696e652673706163653b795f693d31)](https://camo.githubusercontent.com/52cdecab550e057a3a14457e68aa90be99952930db7abe33da4b146e45764dd2/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f6769662e6c617465783f253543696e6c696e652673706163653b795f693d31) si la couverture végétale d'intérêt est observée à l'unité *i* et [![img](https://camo.githubusercontent.com/bc6a9d36a69d8f67c256bb69384819538068971cc76bd8baefadec4e6b660d63/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f6769662e6c617465783f253543696e6c696e652673706163653b795f693d30)](https://camo.githubusercontent.com/bc6a9d36a69d8f67c256bb69384819538068971cc76bd8baefadec4e6b660d63/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f6769662e6c617465783f253543696e6c696e652673706163653b795f693d30) sinon. Un avantage du SRS est que la moyenne des observations est un estimateur sans biais de la proportion de population (*p*) d'intérêt (Cochran, 1977, Eq 3.3)[^fn4]:

[![img](https://camo.githubusercontent.com/d0263fe4179fb434408059650a1044b68ed963d42042ed3798e19e482cd67abf/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f2535434c617267652673706163653b253543626172253742792537443d25354366726163253742312537442537426e25374425354373756d5f253742693d312537442535452537426e253744795f693d25354368617425374270253744)](https://camo.githubusercontent.com/d0263fe4179fb434408059650a1044b68ed963d42042ed3798e19e482cd67abf/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f2535434c617267652673706163653b253543626172253742792537443d25354366726163253742312537442537426e25374425354373756d5f253742693d312537442535452537426e253744795f693d25354368617425374270253744)

et la variance de la proportion estimée *p^* est facilement estimée comme étant (Cochran, 1977, Eq 3.11)[^fn4]

[![img](https://camo.githubusercontent.com/cbdc4c514304e3b0831a7282c5215208c0140f4212ac71575cc25e59420b497b/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f2535434c617267652673706163653b253543686174253742562537442825354368617425374270253744293d253543667261632537422535436861742537427025374428312d25354368617425374270253744292537442537426e2d31253744)](https://camo.githubusercontent.com/cbdc4c514304e3b0831a7282c5215208c0140f4212ac71575cc25e59420b497b/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f2535434c617267652673706163653b253543686174253742562537442825354368617425374270253744293d253543667261632537422535436861742537427025374428312d25354368617425374270253744292537442537426e2d31253744)

Ces estimateurs sont également applicables à des données d'échantillon recueillies dans le cadre d'un échantillonnage systématique simple (SYS). L'analyse simple des données d'échantillon collectées sous SRS/SYS, et la possibilité d'augmenter facilement la taille de l'échantillon (surtout sous SRS), rendent ces plans intéressants.

#### 3.2.1 Post stratification

Un autre avantage important du SRS/SYS est la possibilité de stratifier la zone d'étude après la collecte des résultats de l'échantillonnage - l'application d'une stratification après l'échantillonnage est appelée post-stratification (PSTR). L'application d'une stratification postérieure à l'échantillonnage est appelée post-stratification (PSTR). La PSTR est susceptible d'augmenter la précision des estimations, et il y a rarement des raisons de ne pas post-stratifier en utilisant des cartes.

#### 3.2.2 Taille de l'échantillon

La détermination de la taille de l'échantillon indépendamment du plan consiste à calculer le nombre d'unités dans un échantillon nécessaire pour atteindre une certaine précision cible d'une estimation d'un paramètre de population d'intérêt. Le calcul est basé sur la résolution de l'estimateur de variance correspondant au plan pour *n*. Si la variance de l'estimateur de variance ci-dessus est la variance souhaitée d'une estimation, la résolution pour *n* donne (Cochran, 1977, Eq. 4.2)[^fn4]

[![img](https://camo.githubusercontent.com/fa88088c6a263ed7966ab90b95c8bfa702a0793df088e02f709989e3e096fb39/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f2535434c617267652673706163653b6e3d253543667261632537422535436861742537427025374428312d253543686174253742702537442925374425374225354368617425374256253744282535436861742537427025374429253744)](https://camo.githubusercontent.com/fa88088c6a263ed7966ab90b95c8bfa702a0793df088e02f709989e3e096fb39/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f2535434c617267652673706163653b6e3d253543667261632537422535436861742537427025374428312d253543686174253742702537442925374425374225354368617425374256253744282535436861742537427025374429253744)

où *p^* st une estimation de la proportion d'unités de la classe d'intérêt dans la zone d'étude. Par exemple, supposons que nous voulons estimer la précision globale (comme dans Olofsson et al., 2014, p. 53)[^fn5]avec une marge d'erreur de 5 %. Nous définirions alors *p* comme la précision globale de la carte. Nous ne connaissons évidemment pas la précision globale de la carte à ce stade, de sorte qu'une appréciation objective est nécessaire. Si nous supposons une précision globale de 80 %, une marge d'erreur de 5 % (*MoE*) se traduirait par une variance de (le z-score de 1,96 au niveau de confiance de 95 % est arrondi à 2).

[![img](https://camo.githubusercontent.com/811c93d26457b9e49663479d0985118d502336c1979d048117088530dd7ce7d4/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f2535434c617267652673706163653b4d6f453d25354366726163253742322535437371727425374225354368617425374256253744253744282535436861742537427025374429253744253742253543686174253742702537442537442535434c65667472696768746172726f77253543686174253742562537442825354368617425374270253744293d28253543667261632537424d6f4525354374696d65732673706163653b253543686174253742702537442537442537423225374429253545323d2825354366726163253742302e303525354374696d6573302e382537442537423225374429253545323d302e30303034)](https://camo.githubusercontent.com/811c93d26457b9e49663479d0985118d502336c1979d048117088530dd7ce7d4/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f2535434c617267652673706163653b4d6f453d25354366726163253742322535437371727425374225354368617425374256253744253744282535436861742537427025374429253744253742253543686174253742702537442537442535434c65667472696768746172726f77253543686174253742562537442825354368617425374270253744293d28253543667261632537424d6f4525354374696d65732673706163653b253543686174253742702537442537442537423225374429253545323d2825354366726163253742302e303525354374696d6573302e382537442537423225374429253545323d302e30303034)

ce qui donne une taille d'échantillon égale à

[![img](https://camo.githubusercontent.com/0d228a3402fa0aa5b648553e40ddb50ade37829d771c90cd127f8adae4d5094b/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f2535434c617267652673706163653b6e3d253543667261632537422535436861742537427025374428312d2535436861742537427025374429253744253742253543686174253742562537442825354368617425374270253744292537443d25354366726163253742302e3828312d302e3829253744253742302e303030342537443d343030)](https://camo.githubusercontent.com/0d228a3402fa0aa5b648553e40ddb50ade37829d771c90cd127f8adae4d5094b/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f2535434c617267652673706163653b6e3d253543667261632537422535436861742537427025374428312d2535436861742537427025374429253744253742253543686174253742562537442825354368617425374270253744292537443d25354366726163253742302e3828312d302e3829253744253742302e303030342537443d343030)

Bien que l'estimation de la précision globale ait été illustrée dans Olofsson et al. (2014)[^fn5], spécifier une marge d'erreur de la précision globale de la carte n'est pas intuitif et constitue rarement un objectif d'estimation. Un exemple plus réaliste serait l'estimation de la zone de déforestation ou de dégradation des forêts avec une certaine précision. Dans le tutoriel CODED, une carte de la déforestation, de la dégradation forestière, de la forêt et de la non-forêt a été créée pour la Colombie ; pour des raisons de simplicité, nous regroupons la déforestation et la dégradation de forêt en une seule classe de perturbation de forêt, qui a été cartographiée comme représentant 1,4% du pays de 2010 à 2020. Remarque : pour l'estimation des données d'activité dans le cadre de REDD+ (et d'autres initiatives), il est recommandé d'estimer la déforestation et la dégradation séparément - et donc d'utiliser une strate de déforestation et une strate de dégradation - plutôt que de combiner les deux classes en une seule classe de perturbation forestière. Ici, nous utilisons une classe de perturbation combinée pour faciliter l'illustration du flux de travail et des calculs. Supposons que nous voulions estimer la zone de perturbation forestière (encore une fois, déforestation et dégradation combinées) avec une marge d'erreur de 25 %. Notez que 25% est utilisé ici simplement pour illustrer le flux de travail -- l'erreur cible dépendra des circonstances de l'étude. Premièrement, une marge d'erreur de 25% équivaut à une variance de

[![img](https://camo.githubusercontent.com/878db9bbc34df76fd57a2535b9aa88d16dd0ea024275ca53eda70eb81514ad95/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f2535434c617267652673706163653b253543686174253742562537442825354368617425374270253744293d28253543667261632537424d6f4525354374696d65732673706163653b253543686174253742702537442537442537423225374429253545323d2825354366726163253742302c323525354374696d6573302c3031342537442537423225374429253545323d302c303030303033)](https://camo.githubusercontent.com/878db9bbc34df76fd57a2535b9aa88d16dd0ea024275ca53eda70eb81514ad95/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f2535434c617267652673706163653b253543686174253742562537442825354368617425374270253744293d28253543667261632537424d6f4525354374696d65732673706163653b253543686174253742702537442537442537423225374429253545323d2825354366726163253742302c323525354374696d6573302c3031342537442537423225374429253545323d302c303030303033)

ce qui donne une taille d'échantillon de

[![img](https://camo.githubusercontent.com/dfce4941c2735664ba896945af7acca926fdf8bbd7781e284a6498244ee5e28d/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f2535434c617267652673706163653b6e3d253543667261632537422535436861742537427025374428312d2535436861742537427025374429253744253742253543686174253742562537442870292537443d25354366726163253742302e30313428312d302e30313429253744253742302e3030303030332537443d342c363030)](https://camo.githubusercontent.com/dfce4941c2735664ba896945af7acca926fdf8bbd7781e284a6498244ee5e28d/68747470733a2f2f6c617465782e636f6465636f67732e636f6d2f7376672e6c617465783f2535434c617267652673706163653b6e3d253543667261632537422535436861742537427025374428312d2535436861742537427025374429253744253742253543686174253742562537442870292537443d25354366726163253742302e30313428312d302e30313429253744253742302e3030303030332537443d342c363030)

La collecte d'observations sur près de cinq mille sites d'échantillonnage est rarement réalisable pour une étude spécifique. Cet exemple illustre l'un des inconvénients du SRS/SYS : comme nous n'utilisons aucune information sur la localisation de la déforestation, une très grande taille d'échantillon est nécessaire pour obtenir une grande précision. Une autre façon, plus rapide, d'estimer l'échantillon dans ce cas est de supposer que nous avons besoin d'au moins 30 unités dans les zones de déforestation, ce qui nécessiterait une taille d'échantillon de 30/0,014 = 2 142 unités, ce qui est plus acceptable mais toujours important, et nous n'échantillonnons pas pour atteindre un objectif de précision. (Faites défiler vers le bas à **4.3 Allocation** pour une explication de la raison pour laquelle 30 est le "chiffre magique".)

### 3.3 Échantillonnage en deux étapes/cluster ou par grappes

En raison de la complexité associée à l'échantillonnage à deux phases, il y a beaucoup moins d'exemples de ce type de plans dans la littérature que de plans STR et SRS/SYS. De plus, il n'existe pas de règles fixes pour guider la taille de l'échantillon et des unités primaires d'échantillonnage (UPE), si ce n'est de trouver un compromis entre le nombre global d'observations et un niveau raisonnable d'incertitude pour les estimations au sein des UPE (Sannier et al., 2013)[^fn9]. IAu lieu de créer des exemples, nous allons parcourir deux exemples dans la littérature.

Le premier exemple est celui de Potapov et al. (2014)[^fn7] qui ont estimé la superficie de la perte de forêt 2000-2011 à travers l'Amazonie péruvienne à l'appui de REDD+. La principale source de données de référence était l'imagerie commerciale haute résolution ; une conception en deux étapes a été choisie à des fins d'économie, car le budget ne permettait d'acheter que 30 jeux de données haute résolution. Dans une conception en deux étapes, les données de référence ne sont nécessaires que pour les UPE et non pour l'ensemble de la zone d'étude. Par conséquent, la taille de l'échantillon des 30 UPE a été déterminée sur la base de raisons budgétaires et non en spécifiant une précision cible comme dans les exemples ci-dessus. La taille des PSUs de 12 × 12 km a été choisie pour s'aligner sur les images à haute résolution. Les 5 532 blocs, chacun de 12 × 12 km, couvrant la zone d'étude ont été séparés en une strate de changement forestier élevé (337 blocs) et faible (5 195 blocs), à partir desquels 21 et 9 UPE ont été sélectionnées dans le cadre de la STR. (Cette sélection a été guidée par les règles d'allocation optimale de l'échantillon de Cochran (1977)[^fn4].) Dans chacune des 30 UPE, 100 unités d'échantillonnage secondaires (UES) ont été sélectionnées dans le cadre du SRS lors de la deuxième étape de l'échantillonnage.

Un deuxième exemple est fourni par Sannier et al. (2013)[^fn9] qui ont estimé la proportion de la couverture de la forêt et la déforestation nette au Gabon en utilisant un échantillonnage à deux étapes. L'échantillonnage à deux étapes a été choisi car il représentait un compromis entre la facilité de collecte des données et la distribution géographique. La zone d'étude a été divisée en 251 blocs de 20 × 20 km, chacun d'entre eux étant à son tour divisé en 100 blocs de 2 × 2 km. Lors de la première étape, une UPE de 2 × 2 km a été sélectionnée dans chacun des 251 blocs de 20 × 20 km sous SRS. Dans la deuxième étape, 50 SSU correspondant à un pixel Landsat ont été sélectionnées dans le cadre du SRS.

### 3.4 Logiciel permettant d'estimer la taille de l'échantillon

SEPAL/CEO a un support intégré pour l'estimation de la taille de l'échantillon comme expliqué dans cette publication (défilement vers le bas jusqu'à la section 14).

Similaire à SEPAL est cette feuille de calcul développée par la Banque Mondiale qui calcule également la taille de l'échantillon nécessaire pour atteindre une précision de l'exactitude globale https://onedrive.live.com/view.aspx?resid=9815683804F2F2C7!37340&ithint=file%2cxlsx&authkey=!ANcP-Xna7Knk_EE

### 3.5 Sélection de l'échantillon

La dernière étape du plan d'échantillonnage consiste à tirer physiquement l'échantillon de la zone d'étude, ce qui est abordé dans le prochain tutoriel.

## 4 Foire aux questions (FAQs)

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

Copyright 2020, Banque Mondiale. Ce travail a été développé par Pontus Olofsson dans le cadre d'un contrat de la Banque mondiale avec GRH Consulting, LLC pour le développement de nouvelles ressources - et la collecte de ressources existantes - liées à la mesure, la communication et la vérification pour soutenir la mise en œuvre du MRV dans les pays.

Matériel révisé par : Ana Mirian Villalobos, El Salvador, Ministry of Environment and Natural Resources Carole Andrianirina, Madagascar, National Coordination Bureau REDD+ (BNCCREDD) Foster Mensah, Ghana, Center for Remote Sensing and Geographic Information Services (CERGIS) Jennifer Juliana Escamilla Valdez, El Salvador, Ministry of Environment and Natural Resources Paula Andrea Paz, Colombia, International Center for Tropical Agriculture (CIAT) Phoebe Oduor, Kenya, Regional Centre For Mapping Of Resources For Development (RCMRD) Rajesh Bahadur Thapa, Nepal, International Centre for Integrated Mountain Development (ICIMOD) Tatiana Nana, Cameroon, REDD+ Technical Secretariat

Attribution: Olofsson, P. 2021. Simple random/systematic sampling. © World Bank. License: [Creative Commons Attribution license (CC BY 3.0 IGO)](http://creativecommons.org/licenses/by/3.0/igo/)
