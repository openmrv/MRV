# Plan d'échantillonnage pour l'estimation de la superficie et la précision des carte

## 1. Contexte

Une approche d'estimation basée sur l'échantillonnage peut être séparée en trois volets différents : le plan d'échantillonnage, le plan de réponse et l'analyses (Stehman & Czaplewski, 1998)[^fn1]. La première composante, le plan d'échantillonnage, est illustrée dans ce tutoriel.  Le plan d'échantillonnage définit le protocole de sélection du sous-ensemble d'unités - c'est-à-dire l'échantillon - dans une population plus large. Dans notre cas, la population est l'équivalent de la zone d'étude, et les caractéristiques de la zone d'étude, telles que la superficie d'une certaine couverture du sol, sont estimées en analysant l'échantillon.  Les approches basées sur l'échantillonnage dans un contexte de télédétection sont nécessaires car elles nous permettent d'estimer le biais de zone, la précision des données et l'incertitude. Comme expliqué dans le document GFOI Methods & Guidance Document, 'estimation des zones d'occupation du sol et des changements d'occupation du sol en comptant simplement les pixels dans les cartes produira des résultats erronés en raison des erreurs de classification (GFOI, 2016, p. 125)[^fn2]:

> Les méthodes qui produisent des estimations de données d'activité sous la forme de sommes de superficies d'unités cartographiques assignées à des classes de cartes se caractérisent par un comptage de pixels et ne prévoient généralement pas de tenir compte des effets des erreurs de classification des cartes. De plus, bien que les matrices de confusion ou d'erreur et les indices de précision des cartes puissent renseigner sur les questions d'erreurs systématiques et de précision, elles ne produisent pas directement l'information nécessaire à la construction d'intervalles de confiance. Par conséquent, les méthodes de comptage de pixels ne fournissent aucune assurance que les estimations ne sont "ni surévaluées ni sous-évaluées" ou que "les incertitudes sont réduites autant que possible". Le rôle des données de référence, également caractérisées comme des données d'évaluation de la précision, est de fournir une telle assurance en ajustant les erreurs de classification systématiques estimées et en estimant l'incertitude, fournissant ainsi les informations nécessaires à la construction d'intervalles de confiance pour la conformité avec le guide des bonnes pratiques du GIEC.

Lors du choix d'un plan d'échantillonnage, nous devons tenir compte de quelques critères de conception, mais qui sont importants. Le respect de l'échantillonnage aléatoire est de première importance.  L'échantillonnage aléatoire est défini en termes de probabilités d'inclusion, où une probabilité d'inclusion concerne la probabilité qu'une unité donnée soit incluse dans l'échantillon ; la probabilité d'inclusion doit être connue pour chaque unité sélectionnée dans l'échantillon et la probabilité d'inclusion doit être supérieure à zéro pour toutes les unités de la zone d'étude (Stehman, 2009)[^fn3]. Plusieurs plans d'échantillonnage aléatoire sont applicables à l'estimation de la précision et de la superficie, les plans les plus couramment utilisés étant le plan aléatoire simple, le plan aléatoire stratifié et le plan systématique. L'échantillonnage à deux phases (également appelé double), en deux étapes et en cluster (en grappe) est applicable mais plus complexe.

## 2 Objectifs d'apprentissage

L'objectif de ce tutoriel est de fournir à l'utilisateur une compréhension des diverses décisions clés impliquées dans la conception d'un effort d'estimation basé sur l'échantillonnage. Il est important de comprendre la relation entre la taille de l'échantillon et l'allocation des unités d'échantillonnage aux strates, ainsi que les objectifs primordiaux de l'estimation tels que la précision cible. À la fin du tutoriel, l'utilisateur devrait être en mesure de choisir une méthode de sélection d'échantillon -- SYS, SRS ou STR --, de déterminer la taille de l'échantillon et d'allouer l'échantillon aux strates, en fonction des objectifs liés à l'estimation.

- Comprendre les différentes décisions clés impliquées dans la conception d'un effort d'estimation basé sur l'échantillonnage
- Choisir une méthode de sélection d'échantillon -- SYS, SRS ou STR en fonction des objectifs d'estimation.
- Déterminer la taille de l'échantillon et l'allouer à des strates, en fonction des objectifs d'estimation.

### 2.1 Prérequis pour ce module

- Révision de la terminologie pertinente pour les techniques d'échantillonnage dans le tutoriel 3.1 Terminologie
- Il est fortement conseillé de comprendre les tutoriels précédents des modules 1 et 2.

## 2. Comment choisir un plan d'échantillonnage?

Le choix d'un plan d'échantillonnage nécessite souvent des compromis entre différents critères et priorités.  Le désir de fournir des estimations pour des sous-régions ou la nécessité d'atteindre des objectifs de précision devront être mis en balance avec des critères souhaitables du plan d'échantillonnage tels que la facilité et la praticabilité de la mise en œuvre, la rentabilité, la facilité d'adaptation aux changements de la taille de l'échantillon.  Stehman (2009)[^fn3] fournit un examen détaillé des options, des objectifs et des critères du plan d'échantillonnage, mais la décision se résume généralement à trois décisions clés : l'utilisation de strates, l'utilisation de clusters (ou par grappe)et la mise en œuvre d'un protocole de sélection aléatoire systématique ou simple. 

### 2.1 Echatillonnnage Stratifié?

Les strates sont “des sous-populations qui ne se chevauchent pas et qui, ensemble, constituent la population entière” (Cochran, 1977, p. 89)[^fn4]. La stratification de la zone d'étude avant la sélection de l'échantillon peut garantir que les estimations de la précision et de la superficie sont obtenues pour certaines sous-régions de la zone d'étude, et il en résulte une plus grande précision des estimations. Par conséquent, il existe plusieurs bonnes raisons d'utiliser des strates. Même avec un échantillonnage aléatoire simple, l'utilisation de strates après la sélection de l'échantillon est une [bonne idée](###markdown-header-3.1-Post-stratification). L'échantillonnage stratifié présente un avantage évident si nous nous intéressons à une très petite proportion de la zone d'étude, comme c'est souvent le cas dans les MRV tropicaux. Par exemple, la zone de perte de forêt, même dans les pays où la déforestation est rampante, est souvent une très petite proportion du pays, surtout sur de courts intervalles de temps. L'utilisation d'une carte des pertes de forêts (et d'autres catégories) pour stratifier la zone d'étude dans de telles situations permet un échantillonnage ciblé dans des zones d'intérêt particulier. Ne pas effectuer de stratification dans de telles situations exigera une très grande taille d'échantillon.    

### 2.2 Utilisation d'une sélection aléatoire simple ou systématique?
La sélection systématique consiste à choisir un point de départ au hasard avec une probabilité égale, puis à échantillonner avec une distance fixe entre les emplacements d'échantillonnage. En bref, la sélection aléatoire simple est préférable si l'on recueille des observations de référence dans les données satellitaires alors que la sélection systématique est préférable si l'on visite les sites d'échantillonnage in situ (Olofsson et al. 2014)[^fn5]. Cette recommandation se justifie par le fait que les unités sélectionnées systématiquement sont plus faciles à localiser sur le terrain tandis que la sélection aléatoire est plus facile à faire augmenter. Notez que les mêmes estimateurs sont utilisés avec la sélection aléatoire simple ou systématique.

### 2.3 Echatillonnnage  par grappes?
Une grappe est une unité d'échantillonnage qui consiste en une ou plusieurs unités d'évaluation de base spécifiées par le plan d'échantillonnage. Par exemple, une grappe peut être un bloc 3 × 3 de 9 pixels ou une grappe de 1 km × 1 km contenant 100 unités d'évaluation de 1 ha. Dans l'échantillonnage en grappes, un échantillon de grappes est sélectionné et les unités spatiales de chaque grappe sont donc sélectionnées en tant que groupe plutôt qu'en tant qu'entités individuelles. L'échantillonnage en deux étapes est une forme d'échantillonnage en grappes où de grandes unités primaires d'échantillonnage (UPE) sont sélectionnées à la première étape ; de plus petites unités secondaires d'échantillonnage (USE) sont sélectionnées dans chaque UPE à la deuxième étape.  Ces plans ont l'avantage de ne nécessiter des données de référence (c'est-à-dire les données utilisées pour collecter les observations de référence) que sur les PSU au lieu de la zone d'étude entière comme c'est le cas avec les plans susmentionnés. Cependant, à moins que les économies ne soient considérables, les plans en grappes ne sont pas recommandés car la corrélation entre les UPE réduit souvent la précision par rapport à un simple échantillon aléatoire de taille égale, et parce qu'il s'agit de plans compliqués qu'il est difficile d'enrichir de résultats d'échantillons difficiles à analyser. 


## 3. Échantillonnage aléatoire simple/systématique
Si les unités (par exemple, les pixels) d'une population/zone d'étude sont numérotées de 1 to *N*, 'échantillonnage aléatoire simple (EAS) est “une méthode permettant de sélectionner *n* unités parmi les *N* de telle sorte que chacune des   [ensembles de *n* unités spécifiées] ait une probabilité égale d'être tirée” (Cochran 1977, p. 18)[^fn4]. Dans un contexte de la teledetection, nous sommes souvent intéressés par l'estimation d'une proportion de la population/zone d'étude, telle que la proportion de surface d'une certaine occupation du sol ou d'un changement d'occupation du sol, à partir des données de l'échantillon. En utilisant les notions de Cochran, les unités d'une population sont  ![](https://latex.codecogs.com/gif.latex?\inline&space;y_1&space;\ldots&space;y_N) à partir desquelles un échantillon   ![](https://latex.codecogs.com/gif.latex?\inline&space;y_1&space;\ldots&space;y_n) est sélectionné sous SRS ; on consigne  ![](https://latex.codecogs.com/gif.latex?\inline&space;y_i=1) si la couverture végétale d'intérêt est observée à l'unité  *i* et ![](https://latex.codecogs.com/gif.latex?\inline&space;y_i=0) sinon. Un avantage du SRS est que la moyenne des observations est un estimateur sans biais de la proportion de population (*p*) d'intérêt (Cochran, 1977, Eq 3.3)[^fn4]:

![](https://latex.codecogs.com/svg.latex?\Large&space;\bar{y}=\frac{1}{n}\sum_{i=1}^{n}y_i=\hat{p})

et la variance de la proportion estimée *p^* est facilement estimée comme étant (Cochran, 1977, Eq 3.11)[^fn4]

![](https://latex.codecogs.com/svg.latex?\Large&space;\hat{V}(\hat{p})=\frac{\hat{p}(1-\hat{p})}{n-1})

Ces estimateurs sont également applicables à des données d'échantillon recueillies dans le cadre d'un échantillonnage systématique simple (SYS). L'analyse simple des données d'échantillon collectées sous SRS/SYS, et la possibilité d'augmenter facilement la taille de l'échantillon (surtout sous SRS), rendent ces plans intéressants.

### 3.1 Post stratification 
Un autre avantage important du SRS/SYS est la possibilité de stratifier la zone d'étude après la collecte des résultats de l'échantillonnage - l'application d'une stratification après l'échantillonnage est appelée post-stratification (PSTR). L'application d'une stratification postérieure à l'échantillonnage est appelée post-stratification (PSTR). La PSTR est susceptible d'augmenter la précision des estimations, et il y a rarement des raisons de ne pas post-stratifier en utilisant des cartes. 

### 3.2 Taille de l'échantillon
La détermination de la taille de l'échantillon indépendamment du plan consiste à calculer le nombre d'unités dans un échantillon nécessaire pour atteindre une certaine précision cible d'une estimation d'un paramètre de population d'intérêt. Le calcul est basé sur la résolution de l'estimateur de variance correspondant au plan pour *n*. Si la variance de l'estimateur de variance ci-dessus est la variance souhaitée d'une estimation, la résolution pour *n* donne (Cochran, 1977, Eq. 4.2)[^fn4] 

![](https://latex.codecogs.com/svg.latex?\Large&space;n=\frac{\hat{p}(1-\hat{p})}{\hat{V}(\hat{p})})

où *p^* st une estimation de la proportion d'unités de la classe d'intérêt dans la zone d'étude. Par exemple, supposons que nous voulons estimer la précision globale (comme dans  Olofsson et al., 2014, p. 53)[^fn5]avec une marge d'erreur de 5 %. Nous définirions alors *p* comme la précision globale de la carte. Nous ne connaissons évidemment pas la précision globale de la carte à ce stade, de sorte qu'une appréciation objective est nécessaire. Si nous supposons une précision globale de 80 %, une marge d'erreur de 5 % (*MoE*) se traduirait par une variance de (le z-score de 1,96 au niveau de confiance de 95 % est arrondi à 2).



![](https://latex.codecogs.com/svg.latex?\Large&space;MoE=\frac{2\sqrt{\hat{V}}(\hat{p})}{\hat{p}}\Leftrightarrow\hat{V}(\hat{p})=(\frac{MoE\times&space;\hat{p}}{2})^2=(\frac{0.05\times0.8}{2})^2=0.0004)

ce qui donne une taille d'échantillon égale à

![](https://latex.codecogs.com/svg.latex?\Large&space;n=\frac{\hat{p}(1-\hat{p})}{\hat{V}(\hat{p})}=\frac{0.8(1-0.8)}{0.0004}=400)

Bien que l'estimation de la précision globale ait été illustrée dans  Olofsson et al. (2014)[^fn5], spécifier une marge d'erreur de la précision globale de la carte n'est pas intuitif et constitue rarement un objectif d'estimation. Un exemple plus réaliste serait l'estimation de la zone de déforestation ou de dégradation des forêts avec une certaine précision. Dans le tutoriel CODED, une carte de la déforestation, de la dégradation forestière, de la forêt et de la non-forêt a été créée pour la Colombie ; pour des raisons de simplicité, nous regroupons la déforestation et la dégradation de forêt en une seule classe de perturbation de forêt, qui a été cartographiée comme représentant 1,4% du pays de 2010 à 2020. Remarque : pour l'estimation des données d'activité dans le cadre de REDD+ (et d'autres initiatives), il est recommandé d'estimer la déforestation et la dégradation séparément - et donc d'utiliser une strate de déforestation et une strate de dégradation - plutôt que de combiner les deux classes en une seule classe de perturbation forestière. Ici, nous utilisons une classe de perturbation combinée pour faciliter l'illustration du flux de travail et des calculs.  Supposons que nous voulions estimer la zone de perturbation forestière (encore une fois, déforestation et dégradation combinées) avec une marge d'erreur de 25 %. Notez que 25% est utilisé ici simplement pour illustrer le flux de travail -- l'erreur cible dépendra des circonstances de l'étude. Premièrement, une marge d'erreur de 25% équivaut à une variance de  



![](https://latex.codecogs.com/svg.latex?\Large&space;\hat{V}(\hat{p})=(\frac{MoE\times&space;\hat{p}}{2})^2=(\frac{0,25\times0,014}{2})^2=0,000003)

ce qui donne une taille d'échantillon de

![](https://latex.codecogs.com/svg.latex?\Large&space;n=\frac{\hat{p}(1-\hat{p})}{\hat{V}(p)}=\frac{0.014(1-0.014)}{0.000003}=4,600)

La collecte d'observations sur près de cinq mille sites d'échantillonnage est rarement réalisable pour une étude spécifique. Cet exemple illustre l'un des inconvénients du SRS/SYS : comme nous n'utilisons aucune information sur la localisation de la déforestation, une très grande taille d'échantillon est nécessaire pour obtenir une grande précision. Une autre façon, plus rapide, d'estimer l'échantillon dans ce cas est de supposer que nous avons besoin d'au moins 30 unités dans les zones de déforestation, ce qui nécessiterait une taille d'échantillon de 30/0,014 = 2 142 unités, ce qui est plus acceptable mais toujours important, et nous n'échantillonnons pas pour atteindre un objectif de précision. (Faites défiler vers le bas à  **4.3 Allocation** pour une explication de la raison pour laquelle 30 est le "chiffre magique".)

## 4. Échantillonnage aléatoire stratifié
L'exemple ci-dessus illustre l'inconvénient du SRS/SYS : lorsque nous essayons d'estimer quelque chose qui représente une petite proportion de la population, une très grande taille d'échantillon est nécessaire dans le cadre du SRS/SYS. Dans de telles situations, l'échantillonnage aléatoire stratifié (EAS) est recommandé. On parle de EAS lorsque  “l'échantillonnage aléatoire simple est effectué dans chaque strate” (Cochran 1977, p. 89)[^fn4]. Par conséquent, nous divisons la population en strates et sélectionnons un échantillon dans chaque strate sous SRS (ou SYS). Le EAS ajoute un autre niveau de complexité et nous oblige à déterminer comment répartir l'unité d'échantillonnage entre les strates en plus de déterminer la taille totale de l'échantillon. 

### 4.1 Taille de l'échantillon
Comme pour le SRS/SYS, nous devons spécifier un objectif de précision et calculer à l'aide de l'estimateur de variance EAS la taille totale de l'échantillon (*n*) nécessaire pour atteindre la précision cible. En résolvant l'estimateur de variance EAS, on obtient  (Olofsson et al., 2014, Eq. 13. modifié à partir de Cochran, 1977, Eq 5.25)[^fn4]

![](https://latex.codecogs.com/svg.latex?\Large&space;n=\left&space;[\frac{\sum_{h}W_h\textup{SD}_h}{\text{SE}(p)}\right&space;]^2)

*Wh* est le poids de la strate *h*, qui est simplement la superficie de la strate exprimée en proportion de la zone d'étude totale ; SD*h* est l'écart-type de la strate *h*, qui est expliqué ci-dessous. L'erreur standard cible est SE(*p*). Revenons maintenant à l'exemple de la perturbation de forêt en Colombie mais utilisons maintenant la carte que nous avons générée dans le tutoriel CODED de la perturbation, de la forêt stable et de la non-forêt stable. Le calcul de la taille de l'échantillon sous EAS est un peu plus compliqué, nous utiliserons donc une feuille de calcul de Google Sheets (ou Microsoft Excel si vous préférez). La feuille de calcul utilisée dans ce tutoriel est accessible ici : https://docs.google.com/spreadsheets/d/1lmPt35SvR3X7txpn0cwd-xkgwC_4nRPL520OZZcRKX0/edit?usp=sharing  

#### Étape 1 
Tout d'abord, nous devons calculer le nombre de pixels de chaque strate ; ceci peut être fait en utilisant GDAL, QGIS, Google Earth Engine, etc. ; dans le tutoriel CODED, ces zones sont affichées dans la *Console* de Google Earth Engine. Si ce n'est pas le cas, ou si vous avez un actif GEE existant, chargez l'actif en utilisant le script AREA2 Stratified Random Sampling  (https://code.earthengine.google.com/6a0f89221d40ee039362974d303ff5aa) pour calculer les poids des strates. Ajoutez ces chiffres sur la première ligne "Area [px]". Dans la deuxième ligne, exprimez ces surfaces sous forme de proportion  (dans la cellule  B3 tapez "=B2/sum($B2:$D2") et prolongez jusqu'à  E2). Ces proportions sont appelées poids des strates (*Wh*). 


| | A             | B            | C              |D              |E             |
|-|:--------------|:-------------|:---------------|:--------------|:-------------|
|1| Stratum (*h*) | Forêt (1) | Non-Forêt (2) |For. Dist. (3) |Total     |
|2| Superficie [m2] |658 196  561  513| 462 219 395  097 |15 594 353 281| 1 136 010 309 891 |
|3| *Wh*          |0,579       |0,407         |0,0137	         |1         |

#### Étape 2
Après avoir calculé *Wh*, nous devons calculer les deux variables restantes de l'équation : l'écart-type de la strate *h* (SD*h*) et l'erreur-type cible (SE(*p*)). L'écart type de la strate *h* est un peu difficile à comprendre et nécessite une estimation de la proportion de la strate *h* qui est la classe cible (*qh*). 

![](https://latex.codecogs.com/svg.latex?\Large&space;\textup{SD}_h=\sqrt{q_h(1-q_h)})

Dans notre exemple, la proportion de perturbations dans la zone d'étude est la cible, ce qui signifie que *qh* est la proportion de la strate *h* qui est une perturbation - si la carte était parfaite (ce qui n'est pas le cas !) alors *q1* (forêt) = *q2* (non-forêt) = 0 ; *q3* (perturbation) = 1 mais nous ne pouvons pas supposer que c'est le cas. Aucune carte n'est parfaite et une hypothèse plus réaliste est que, disons, 80% des perturbations dans la zone d'étude sont capturées par la classe de carte des perturbations, et que de petites fractions des strates de forêt et de non-forêt sont des perturbations en raison d'une erreur de classification. Si *q1* = 0,001, alors nous supposons que 0,001 × 658 196 561 513/30^2^ = 0,7 M pixels de perturbation dans la strate forêt. La strate non forêt étant légèrement plus petite, si nous pensons qu'une quantité similaire de perturbations est également présente dans la strate non forêt, nous devrions supposer *q2* = 0,002. Par conséquent, ajoutons ces chiffres (0,001, 0,002 et 0,8) à la ligne 4 et calculons SD*h* à la ligne 5, cellule B5 comme "=sqrt(B4*(1-B4))" et étendons à la cellule D5. Pour simplifier, calculez le produit de SD*h et de *Wh* à la ligne 6 de telle sorte que la cellule B6 = B3*B5 et étendez-le à D5 :

| | A             | B            | C              |D              |E             |
|-|:--------------|:-------------|:---------------|:--------------|:-------------|
|1| Stratum (*h*) | Forêt (1) | Non-Forêt(2) |For. Dist. (3) |Total         |
|2| Superficie  [m2] |658 196 561 513| 462 219 395 097 |15 594 353 281| 1 136 010 309 891 |
|3| *Wh*          |0,579          |0,407          |0,0137	         |1         |
|4|*qh*           |	0,001        |	0,002	     |	0,8             | 		    |
|5|SD*h*          |	0,0316       |	0,0447	     |0,4	             |          |
|6|SD*h* x *Wh*   |	0,0183       |	0,01818      |	0,005491        |	        |

#### Étape 3
Fixons maintenant l'objectif de l'échantillonnage : la marge d'erreur souhaitée de la zone de perturbation. Dans la formule d'estimation de la taille de l'échantillon, l'objectif est exprimé sous la forme d'une erreur standard. Si nous visons à nouveau une marge d'erreur de 25%, alors

![](https://latex.codecogs.com/svg.latex?\Large&space;MdE=\frac{1,96\times\textup{SE}(\hat{p})}{\hat{p}}\Leftrightarrow\textup{SE}(\hat{p})=\frac{MdE\times&space;\hat{p}}{1,96}=\frac{0,1\times0,01}{1,96}=0,0005)

Nous utilisons ici un z-score de 1,96 qui correspond à un niveau de confiance de 95%. Si nous spécifions le MdE dans la cellule D7, nous pouvons alors calculer l'erreur standard cible dans la cellule D8 :"=(D7/100)*D3/2":



| | A             | B            | C              |D              |E             |
|-|:--------------|:-------------|:---------------|:--------------|:-------------|
|1| Stratum (*h*) | Forêt (1) | Non-Forêt (2) |For. Dist. (3) |Total     |
|2| Superficie  [m2] |658 196 561 513| 462 219 395 097 |15 594 353 281| 1 136 010 309 891 |
|3| *Wh*          |0,579       |0,407         |0,0137	         |1         |
|4|*qh*           |	0,001        |	0,002	     |	0,8             | 		    |
|5|SD*h*          |	0,0316       |	0,0447	     |0,4	             |          |
|6|SD*h* x *Wh*   |	0,0183     |	0,01818  |	0,005491 |	|
|7| MoE [%]       |   || 25        |            |
|8| SE(*p^*)      |   || 0,0017  |            |

#### Étape 4
Enfin, nous pouvons maintenant calculer facilement la taille de l'échantillon à la ligne 8, cellule E9 comme suit :"=(sum(B6:D6)/B7)^2"

| | A             | B            | C              |D              |E             |
|-|:--------------|:-------------|:---------------|:--------------|:-------------|
|1| Stratum (*h*) | Forêt (1) | Non-Forêt(2) |For. Dist. (3) |Total     |
|2| Superficie  [m2] |658 196 561 513| 462 219 395 097 |15 594 353 281| 1 136 010 309 891 |
|3| *Wh*          |0,579       |0,407         |0,0137	         |1         |
|4|*qh*           |	0,001        |	0,002	     |	0,8             | 		    |
|5|SD*h*          |	0,0316       |	0,0447	     |0,4	             |          |
|6|SD*h* x *Wh*   |	0,0183     |	0,01818  |	0,005491 |	|
|7| MdE [%]      |   || 25        |            |
|8| SE(*p^*)      |   || 0,00172  |            |
|9| *n*           |              |            |               | 599    |

ce qui donne une taille d'échantillon de 599 -- c'est-à-dire environ 1/8 de la taille d'échantillon de 4 600 requise par le SRS pour atteindre la même précision. Pour modifier la précision cible, il nous suffit maintenant d'ajuster notre précision cible dans la cellule D7.

### 4.2 Strates tampons
Un problème potentiel dans la situation ci-dessus est que les omissions de perturbations présentes dans la strate de forêt auront un impact important sur la précision des estimations.  Ces erreurs d'omission sont des unités d'échantillon dans la strate forêt qui ont été observées dans les données de référence comme étant des perturbations. La question est expliquée en détail dans  Olofsson et al. (2020)[^fn6]  aet ici nous reconnaissons simplement que la "contribution à l'incertitude" des erreurs d'omission dépend dans une large mesure de la taille de la strate dans laquelle elles se produisent. Nous souhaitons donc diminuer la taille de la strate forêt qui représente actuellement 83% de la zone d'étude. En particulier, nous voulons créer de petites substrats où les omissions de perturbations sont susceptibles de se produire. Une approche explorée dans la littérature est la création de strates tampons autour des strates de changement -- le raisonnement est que les erreurs sont susceptibles de se produire près des changements correctement cartographiés. Dans notre cas, une telle strate tampon pourrait être définie comme les pixels de la strate forêt adjacente à la perturbation. 

La création d'un tampon n'est pas illustrée dans les tutoriels précédents, alors faisons-le maintenant. Cliquez sur ce lien : Un script pour créer un tampon dans la sortie CODED est disponible dans AREA2 : 
https://code.earthengine.google.com/861290ef20f0d76e7639d430471c7eae 

Vous pouvez également utiliser cette carte existante de la Colombie basée sur le CODED avec un tampon :

https://code.earthengine.google.com/?asset=users/olofsson76/Open_MRV/Open_MRV_Col_strat_buffer
Pour obtenir les poids des strates, ouvrez le script dans AREA2 pour sélectionner un échantillon sous échantillonnage aléatoire stratifié :
https://code.earthengine.google.com/?accept_repo=users%2Fopenmrv%2FMRV&scriptPath=projects%2FAREA2%2Fpublic%3A1.%20Sampling%20Design%2FStratified%20Random%20Sampling et spécifier le chemin d'accès à la carte de la Colombie basée sur la CODED avec un tampon sous "Specify stratification/image to define study area" ; utiliser les autres arguments par défaut, cliquer sur "Load image" qui affichera les zones de strates dans la console (NOTE : cela prendra un certain temps). J'obtiens les zones suivantes : Forêt (0), Non-forêt (1), Perturbation de la forêt (2) et une zone tampon-2 pixels (3). [m^2^]:

0: 625 597 113 080
1: 462 219 395 097
2: 15 594 353 281
3: 32 599 448 433

Ajoutons ces chiffres dans un deuxième onglet de la feuille de calcul et calculons les poids des strates :

| | A             | B            | C              |D              |E             |F         |
|-|:--------------|:-------------|:---------------|:--------------|:-------------|:---------|
|1| Stratum (*h*) | Forêt (1) | Non-Forêt (2) |For. Dist. (3) |FD buf. (4)   |Total     |
|2| Superficie [m2] |625 597 113 080|462 219 395 097|15 594 353 281 |32 599 448 433|1 136 010 309 891|
|3| *Wh*          |0,551       |0,407         |0,0137	      |0,0287	         |1         |

Si nous pensons que la strate tampon est efficace pour capturer les erreurs d'omission, nous pouvons diminuer *qh* pour la strate forêt -- si nous supposons que la moitié des pixels de perturbation dans la strate forêt seront "capturés" par la strate tampon, alors *q1* = 0,0005 et *q4* = 0,0075. Avec une marge d'erreur cible de 25%, la taille de l'échantillon tombe à 502.
	
| | A             | B            | C              |D              |E             |F         |
|-|:--------------|:-------------|:---------------|:--------------|:-------------|:---------|
|1| Stratum (*h*) | Forêt (1) | Non-Forêt (2) |For. Dist. (3) |FD buf. (4)   |Total     |
|2| Superficie  [m2] |625 597 113 080|462 219 395 097|15 594 353 281 |32 599 448 433|1 136 010 309 891|
|3| *Wh*          |0,551       |0,407         |0,0137	      |0,0287	         |1         |
|4|*qh*           |	0,0005    |	0,002    |	0,8        |	0,0075	|  |
|5|SD*h*          |	0,0223     |	0,04468  |	0,4        |	0,086277 |	|
|6|SD*h* x *Wh*   |	0,0123     |	0,01818  |	0,005491	|	0,002475 |	|
|7|*MdE* [%]      |		       	|	          |	25		    |	         |	|
|8|SE(*p^*)	      |		        |	          |0,001716	    |	         |	|
|9|*n*		      |			    |	          |             |	         |502|

Un tampon de trois pixels a été utilisé ici à titre d'exemple. Pour plus d'informations sur la manière de déterminer la taille des strates de la mémoire tampon, voir  Olofsson et al. (2020)[^fn6]. 

### 4.3 Allocation
Supposons que nous ayons choisi une marge d'erreur de 15% avec une strate tampon et une taille d'échantillon de 958.  Nous devons maintenant décider comment allouer l'échantillon aux strates. En bref, une allocation proportionnelle aux poids des strates est efficace pour estimer les paramètres qui incluent des calculs entre strates -- ces paramètres sont notamment la surface, la précision globale et la précision du producteur. L'estimation de la précision de l'utilisateur est basée sur des calculs au sein des strates qui bénéficient d'une allocation égale. L'obtention d'une précision élevée de la précision de l'utilisateur est rarement un objectif d'estimation, ce qui suggère qu'une allocation proportionnelle est préférable. Revenons à la feuille de calcul, calculons sur la ligne 10 la taille de l'échantillon dans chaque strate suivant une allocation proportionnelle : dans la cellule B10 : "=B3*$F$9" et prolongez jusqu'à E10.

| | A             | B            | C              |D              |E             |F         |
|-|:--------------|:-------------|:---------------|:--------------|:-------------|:---------|
|1| Stratum (*h*) | Forêt (1) | Non-Forêt (2) |For. Dist. (3) |FD buf. (4)   |Total     |
|2| Superficie [m2] |625 597 113 080|462 219 395 097|15 594 353 281 |32 599 448 433|1 136 010 309 891|
|3| *Wh*          |0,551       |0,407         |0,0137	    |0,0287	         |1             |
|4|*qh*           |	0,0005    |	0,002    |	0,8        |	0,0075	   |              |
|5|SD*h*          |	0,0223     |	0,04468  |	0,4        |	0,086277    |              |
|6|SD*h* x *Wh*   |	0,0123     |	0,01818  |	0,005491	|	0,002475    |              |
|7|*MdE* [%]      |		       	|	          |	25		    |	             |              |
|8|SE(*p^*)	      |		        |	          |0.001716	    |	             |              |
|9|*n*		      |			    |	          |             |	             |502           |
|10| *nh* (prop.) |277	|204	|7	|14|	502


Cela semble raisonnable mais nous avons besoin d'au moins 30 unités par strate, donc à la ligne 11, augmentons la taille de l'échantillon dans la strate de perturbation à 30 et arrondissons les tailles d'échantillon dans la strate forêt à 275 et la strate non-forêt à 200. Cela donne l'allocation finale. 

| | A             | B            | C              |D              |E             |F         |
|-|:--------------|:-------------|:---------------|:--------------|:-------------|:---------|
|1| Stratum (*h*) | Forêt (1) | Non-Forêt(2) |For. Dist. (3) |FD buf. (4)   |Total     |
|2| Superficie [m2] |625 597 113 080|462 219 395 097|15 594 353 281 |32 599 448 433|1 136 010 309 891|
|3| *Wh*          |0,551       |0,407         |0,0137	    |0,0287	         |1             |
|4|*qh*           |	0,0005    |	0,002    |	0,8        |	0,0075	    |              |
|5|SD*h*          |	0,0223     |	0,04468  |	0,4        |	0,086277    |              |
|6|SD*h* x *Wh*   |	0,0123     |	0,01818  |	0,005491	|	0,002475    |              |
|7|*MoE* [%]      |		       	|	          |	25		    |	             |              |
|8|SE(*p^*)	      |		        |	          |0,001716	    |	             |              |
|9|*n*		      |			    |	          |             |	             |502           |
|10| *nh* (prop.) |277      	|204	      |7	        |14              |502           |
|11| *nh* (final) |275      	|200	      |30	        |30              |535           |

La raison pour laquelle 30 est considéré comme la taille minimale de l'échantillon est mieux décrite par Lohr  (1999)![^fn8]: 

> Le terme imprécis "suffisamment grand" apparaît dans le théorème central limite parce que l'adéquation de l'approximation normale dépend de n et du degré de ressemblance de la population {yi, i = 1, ... , N} ressemble à une population générée à partir de la distribution normale. Le "nombre magique" de n = 30 [est] souvent cité dans les ouvrages d'introduction aux statistiques comme une taille d'échantillon "suffisamment grande" pour que le théorème central limite s'applique

Le théorème de la limite centrale est important car il stipule que la somme de variables aléatoires indépendantes est normalement distribuée même si les variables elles-mêmes ne le sont pas. Par exemple, le théorème nous permet de construire des intervalles de confiance en utilisant des z-scores  communs et une erreur standard.

## 5. Échantillonnage en deux étapes/cluster ou par grappes
En raison de la complexité associée à l'échantillonnage à deux phases, il y a beaucoup moins d'exemples de ce type de plans dans la littérature que de plans STR et SRS/SYS. De plus, il n'existe pas de règles fixes pour guider la taille de l'échantillon et des unités primaires d'échantillonnage (UPE), si ce n'est de trouver un compromis entre le nombre global d'observations et un niveau raisonnable d'incertitude pour les estimations au sein des UPE  (Sannier et al., 2013)[^fn9]. IAu lieu de créer des exemples, nous allons parcourir deux exemples dans la littérature. 

Le premier exemple est celui de  Potapov et al. (2014)[^fn7] qui ont estimé la superficie de la perte de forêt 2000-2011 à travers l'Amazonie péruvienne à l'appui de REDD+.  La principale source de données de référence était l'imagerie commerciale haute résolution ; une conception en deux étapes a été choisie à des fins d'économie, car le budget ne permettait d'acheter que 30 jeux de données haute résolution. Dans une conception en deux étapes, les données de référence ne sont nécessaires que pour les UPE et non pour l'ensemble de la zone d'étude.   Par conséquent, la taille de l'échantillon des 30 UPE a été déterminée sur la base de raisons budgétaires et non en spécifiant une précision cible comme dans les exemples ci-dessus. La taille des PSUs de 12 × 12 km a été choisie pour s'aligner sur les images à haute résolution. Les 5 532 blocs, chacun de 12 × 12 km, couvrant la zone d'étude ont été séparés en une strate de changement forestier élevé (337 blocs) et faible (5 195 blocs), à partir desquels 21 et 9 UPE ont été sélectionnées dans le cadre de la STR. (Cette sélection a été guidée par les règles d'allocation optimale de l'échantillon de Cochran (1977)[^fn4].) Dans chacune des 30 UPE, 100 unités d'échantillonnage secondaires (UES) ont été sélectionnées dans le cadre du SRS lors de la deuxième étape de l'échantillonnage. 

Un deuxième exemple est fourni par  Sannier et al. (2013)[^fn9] qui ont estimé la proportion de la couverture de la forêt et la déforestation nette au Gabon en utilisant un échantillonnage à deux étapes. L'échantillonnage à deux étapes a été choisi car il représentait un compromis entre la facilité de collecte des données et la distribution géographique. La zone d'étude a été divisée en 251 blocs de 20 × 20 km, chacun d'entre eux étant à son tour divisé en 100 blocs de 2 × 2 km. Lors de la première étape, une UPE de 2 × 2 km a été sélectionnée dans chacun des 251 blocs de 20 × 20 km sous SRS. Dans la deuxième étape, 50 SSU correspondant à un pixel Landsat ont été sélectionnées dans le cadre du SRS.   

## 6. Logiciel permettant d'estimer la taille de l'échantillon
SEPAL/CEO a un support intégré pour l'estimation de la taille de l'échantillon comme expliqué dans cette publication (défilement vers le bas jusqu'à la section 14). 

Similaire à SEPAL est cette feuille de calcul développée par la Banque Mondiale qui calcule également la taille de l'échantillon nécessaire pour atteindre une précision de l'exactitude globale https://onedrive.live.com/view.aspx?resid=9815683804F2F2C7!37340&ithint=file%2cxlsx&authkey=!ANcP-Xna7Knk_EE



## 7. Sélection de l'échantillon
La dernière étape du plan d'échantillonnage consiste à tirer physiquement l'échantillon de la zone d'étude, ce qui est abordé dans le prochain tutoriel.



## 4 Foire aux questions (FAQs)

**Je ne comprends pas la variable qh qui est utilisée pour calculer la taille de l'échantillon sous STR - qu'est-ce qu'elle signifie ?**

La variable *qh* est nécessaire pour calculer l'écart-type de la strate *h* et représente la proportion de la strate *h* qui est la classe cible. Dans l'exemple ci-dessus, nous avons trois strates (avant la création de la strate tampon), *h* = 1 est forestière, *h* = 2 est non forestière, et *h* = 3 est une perturbation de type forêt, cette dernière étant la classe cible. Dans ce cas, *qh* est la proportion de perturbations de forêt dans chaque strate. Si la carte était parfaite, alors toutes les perturbations forestières de la zone d'étude seraient présentes dans la strate des perturbations forestières et donc *q3* = 1, tandis que *q1* et *q2* seraient égaux à zéro. Aucune carte n'est parfaite et nous devrons supposer un certain niveau d'erreur de classification. Notez que cette information est inconnue au stade de la conception et qu'il est nécessaire de faire des suppositions. Par exemple, si *q3* = 0,8, nous supposons que 80 % des perturbations forestières de l'étude sont présentes dans la strate des perturbations forestières. Si *q1* = 0,001, nous supposons que 0,1 % de la strate forestière est une perturbation de forêt.

**Je n'ai aucune idée de la façon dont on détermine les valeurs de qh - que dois-je faire ?**

La variable *qh* est essentiellement une indication de la façon dont la stratification capture la classe d'intérêt. Étant donné que des cartes sont généralement utilisées pour stratifier la zone d'étude, je vous conseille de vérifier l'exactitude des cartes précédentes de la même zone. Notez que *qh* pour *h* = la classe d'intérêt, est la précision anticipée de l'utilisateur de la classe d'intérêt.

**Comment déterminer une erreur standard souhaitée?**

Certains programmes spécifient une précision souhaitée ou requise ; le Forest Carbon Partnership Facility  (FCPF), par exemple, stipule une marge d'erreur de 30% au niveau de confiance de 95% pour les estimations de surface des données d'activité. La marge d'erreur est égale à 1,96 fois l'erreur standard divisée par l'estimation de la superficie. Lorsque de telles exigences de précision ne sont pas spécifiées, une erreur standard cible doit être déterminée sur la base d'autres critères. Il est à noter que plus la proportion de surface de la classe recherchée est faible, plus l'échantillon doit être important pour atteindre une faible marge d'erreur. Par conséquent, pour les petites proportions de surface, la précision ciblée devra être allégée pour éviter d'avoir à sélectionner un très grand échantillon.

**Si j'utilise une strate tampon, combien de pixels doit-elle avoir**

Il est difficile de fournir des recommandations car la taille du tampon dépendra des situations. Un tampon plus grand "capturera" probablement plus d'erreurs d'omission mais aura un poids de strate plus grand. Un tampon plus grand est recommandé dans les situations d'une petite classe d'intérêt en présence d'une grande strate stable (comme une forêt stable). Les exemples dans la littérature vont de 1 à 3 pixels. Une exploration plus détaillée de l'impact de la taille du tampon est présentée dans Olofsson et al. (2020).



## License

Cette œuvre est soumise à une licence [Creative Commons Attribution 3.0 IGO](https://creativecommons.org/licenses/by/3.0/igo/) 

Copyright 2020, Banque Mondiale. Ce travail a été développé par Pontus Olofsson dans le cadre d'un contrat de la Banque mondiale avec GRH Consulting, LLC pour le développement de nouvelles ressources - et la collecte de ressources existantes - liées à la mesure, la communication et la vérification pour soutenir la mise en œuvre du MRV dans les pays. 

Matériel révisé par :
Ana Mirian Villalobos, El Salvador, Ministry of Environment and Natural Resources
Carole Andrianirina, Madagascar, National Coordination Bureau REDD+ (BNCCREDD)
Foster Mensah, Ghana, Center for Remote Sensing and Geographic Information Services (CERGIS)
Jennifer Juliana Escamilla Valdez, El Salvador, Ministry of Environment and Natural Resources
Paula Andrea Paz, Colombia, International Center for Tropical Agriculture (CIAT)
Phoebe Oduor, Kenya, Regional Centre For Mapping Of Resources For Development (RCMRD)
Rajesh Bahadur Thapa, Nepal, International Centre for Integrated Mountain Development (ICIMOD)
Tatiana Nana, Cameroon, REDD+ Technical Secretariat

Attribution: Olofsson, P. (2021). *Open MRV: Sampling Design*. World Bank. License: Creative Commons Attribution license (CC BY 3.0 IGO)

## References
[^fn1]: Stehman, S. V., & Czaplewski, R. L. (1998). Design and analysis for thematic map accuracy assessment: fundamental principles. *Remote Sensing of Environment*, 64(3), 331-344.
[^fn2]: GFOI (2016). *Integration of remote-sensing and ground-based observations for estimation of emissions and removals of greenhouse gases in forests: Methods and guidance from the Global Forest Observations Initiative* (2nd ed.), Rome: UN Food and Agriculture Organization
[^fn3]: Stehman, S. V. (2009). Sampling designs for accuracy assessment of land cover. *International Journal of Remote Sensing*, 30, 5243-5272.
[^fn4]: Cochran, W. G. (1977). Sampling techniques (3rd ed.), New York: Wiley
[^fn5]: Olofsson, P., Foody, G. M., Herold, M., Stehman, S. V., Woodcock, C. E., & Wulder, M. A. (2014). Good practices for estimating area and assessing accuracy of land change. *Remote Sensing of Environment*, 148, 42-57.
[^fn6]: Olofsson, P., Arévalo, P., Espejo, A. B., Green, C., Lindquist, E., McRoberts, R. E., & Sanz, M. J. (2020). Mitigating the effects of omission errors on area and area change estimates. *Remote Sensing of Environment*, 236, 111492.   
[^fn7]: Potapov, P. V., Dempewolf, J., Talero, Y., Hansen, M. C., Stehman, S. V., Vargas, C., ... & Giudice, R. (2014). National satellite-based humid tropical forest change assessment in Peru in support of REDD+ implementation. *Environmental Research Letters*, 9, 124012.
[^fn8]: Lohr, S. L. (1999). *Sampling: Design and Analysis: Design And Analysis*. CRC Press.
[^fn9]: Sannier, C., McRoberts, R. E., Fichet, L. V., & Makaga, E. M. K. (2014). Using the regression estimator with Landsat data to estimate proportion forest cover and net proportion deforestation in Gabon. *Remote Sensing of Environment*, 151, 138-148.
