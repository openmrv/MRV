# Analyse des données de l'échantillon

## 1. Contexte

Dans les tutoriels précédents, nous avons conçu et réalisé un échantillon pour la Colombie, et nous avons observé et documenté les données de référence de l'occupation du sol à chaque unité d'échantillonnage. La collection d'observations de référence est appelée les résultats ou les données de l'échantillon, ou encore la classification de référence. Dans ce tutoriel, nous appliquerons divers estimateurs aux données de l'échantillon pour estimer les caractéristiques de la population que nous avons échantillonnée, à savoir les caractéristiques telles que la zone de perturbation des forêts. Un estimateur est  “ la règle par laquelle une estimation d'une caractéristique de la population [c'est-à-dire un paramètre] *μ* est calculée à partir des résultats de l'échantillon”  (Cochran, 1977, p. 11)[^fn1]. Notez qu'un estimateur n'est pas la même chose qu'une estimation - au contraire, “un estimateur est une fonction de l'échantillon, tandis qu'une estimation est la valeur réalisée d'un estimateur (c'est-à-dire un nombre) qui est obtenue lorsqu'un échantillon est effectivement prélevé ” (Casella & Berger, 2002, p. 312)[^fn2]. Un estimateur possède deux propriétés importantes : la variance et le biais. Le biais d'un estimateur *μ^* d'un paramètre de population *μ* est la différence entre *μ* et la valeur attendue de *μ^* sur tous les échantillons possibles ; soit , ![](https://latex.codecogs.com/gif.latex?\inline&space;\textup{Bias}(\hat{\mu})&space;=&space;\textup{E}(\hat{\mu})&space;-&space;\mu) (Casella & Berger, 2002, p. 330)[^fn2]. Si  ![](https://latex.codecogs.com/gif.latex?\inline&space;\textup{Bias}(\hat{\mu})&space;=&space;\textup{E}(\hat{\mu})&space;-&space;\mu=0), alors l'estimateur est dit sans biais. Notez que parce qu'une estimation est un nombre, elle n'a pas de variance ni de biais et ne peut donc pas être sans biais.

L'autre propriété importante d'un estimateur est la variance. La définition formelle de la variance indique “une mesure du degré de dispersion d'une distribution autour de sa moyenne” (Casella & Berger, 2002, p. 59)[^fn2]. Cette définition n'est pas très utile dans notre contexte, nous nous intéressons plutôt aux situations dans lesquelles nous avons échantillonné une zone d'étude pour estimer un certain paramètre de population (par exemple, la superficie de la forêt ou la déforestation). Par exemple, si nous avons une population de dans laquelle un échantillon de a été sélectionné, la variance de l'échantillon est *s^2^* et est facilement calculée pour les plans d'échantillonnage courants. Mais la variance de l'échantillon est moins intéressante que la variance d'un estimateur. Pour les plans d'échantillonnage courants, nous pouvons facilement prouver que la variance de l'échantillon *s^2^* est un estimateur sans biais de la variance de la population *S^2^* (Cochran, 1977, p. 22, 26)[^fn1]. La variance d'un estimateur *u^*  ![](https://latex.codecogs.com/gif.latex?\inline&space;\textup{V}(\hat{\mu})&space;=&space;S^2&space;\div&space;n) (en supposant une petite taille d'échantillon, *n*, par rapport à la taille de la population, *N*)); la variance estimée de *u^* substitue la variance de l'échantillon *s^2^* à la variance de la population *S^2^* pour créer l'estimateur de variance de *u^* comme ![](https://latex.codecogs.com/gif.latex?\inline&space;\hat{V}(\hat{\mu})&space;=&space;s^2&space;\div&space;n) qui est l'estimateur de variance qui nous intéresse le plus car il nous permet de quantifier l'incertitude dans des choses comme les données d'activité ou d'autres paramètres importants.  

A partir de là, nous pouvons introduire deux mesures plus importantes de la dispersion : l'erreur standard et l'intervalle de confiance. L'erreur standard est l'écart type (c'est-à-dire la racine carrée de la variance) d'un estimateur (Rice, 1995, p. 192)[^fn3] et a donc la même unité que l'estimation. L'écart-type d'un estimateur est appelé son erreur-type. Comme la variance de l'échantillon est un estimateur sans biais de la variance de la population, nous pouvons estimer l'erreur standard à l'aide de la variance de l'échantillon : ![](https://latex.codecogs.com/gif.latex?\inline&space;\textup{SE}(\hat{\mu})&space;=&space;\hat{V}(\hat{\mu})&space;\div&space;\sqrt{n}). Notez que, comme une erreur standard est un écart type d'un estimateur, toutes les erreurs standard sont également des écarts types, mais tous les écarts types ne sont pas des erreurs standard. Cela prête parfois à confusion, même si les définitions de l'erreur standard et de l'écart standard sont cohérentes. Ni la variance ni l'erreur standard ne sont généralement utilisées pour exprimer l'incertitude des estimations, à la place, un intervalle de confiance est couramment utilisé  : " Un intervalle de confiance de 95 % pour *μ* est un intervalle aléatoire qui contient *μ* avec une probabilité de 0,95 ; si nous devions prendre de nombreux échantillons aléatoires [selon le même plan d'échantillonnage] et former un intervalle de confiance à partir de chacun d'eux, environ 95 % de ces intervalles contiendraient *μ*." (Rice, 1995, p. 217)[^fn3]. Les intervalles de confiance sont souvent de la forme  ![](https://latex.codecogs.com/gif.latex?\inline&space;\hat{\mu}&space;\pm&space;a\times\textup{SE}(\hat{\mu})) où *a* est une statistique liée au niveau de confiance souhaité, appelée score z ou score standard, exprimée en pourcentage entre 0 et 100 %. Pour un certain niveau de confiance *p*, l'aire sous la fonction de densité normale standard de  *-z*  à  *+z* est *p* (Rice, 1995, p. 202)[^fn3]; par exemple, un intervalle de confiance au niveau de confiance de 95% correspond à un z-score de 1,96 (souvent arrondi à 2). Une condition pour utiliser un z-score pour calculer un intervalle de confiance est que la distribution de l'échantillonnage soit approximativement une distribution normale, ce que l'on peut supposer pour des échantillons de grande taille. L'intervalle de confiance divisé par l'estimation est appelé marge d'erreur (*MdE*) et est souvent exprimé en pourcentage.



Les deux propriétés, biais et variance, sont importantes car nous pouvons nous assurer que l'estimateur que nous utilisons est sans biais et nous pouvons exprimer l'incertitude des estimations. Ni l'un ni l'autre n'est possible lorsqu'on utilise le comptage de pixels dans les cartes ou lorsqu'on procède à un échantillonnage sans appliquer le principe de l'échantillonnage probabiliste.  Un autre aspect important d'un estimateur est qu'il est une fonction de l'échantillon, ce qui signifie que l'estimateur doit correspondre au plan d'échantillonnage. Par exemple, la moyenne de l'échantillon est un estimateur sans biais de la moyenne de la population pour un échantillonnage aléatoire simple ; pour un échantillonnage aléatoire stratifié, nous devons utiliser un estimateur stratifié qui est exprimé comme la somme des moyennes des échantillons aléatoires simples dans les strates pondérées par les poids des strates.



## 2. Analysis of sample results collected under SRS/SYS 
Les résultats des échantillons collectés par échantillonnage aléatoire simple sont les plus simples à analyser (les mêmes estimateurs sont utilisés pour l'échantillonnage aléatoire simple et systématique). Étant donné qu'aucune carte/stratification n'est utilisée et que la moyenne de l'échantillon est un estimateur non biaisé de la moyenne de la population, l'analyse des résultats des échantillons SRS/SYS peut facilement être réalisée dans une feuille de calcul.  L'échantillonnage aléatoire stratifié a été illustré dans les tutoriels précédents, et seules des données fictives sont fournies ici pour illustrer la construction des estimateurs SRS/SYS. Supposons que les données de cette feuille de calcul soient des cartes et des labels de référence à des emplacements sélectionnés dans le cadre du SRS :[Lien]( https://docs.google.com/spreadsheets/d/1pcK-rlhUo5lvmYqibT4zIv-bR5tF4Uu8DqPwIG8mJWQ/edit?usp=sharing) .La taille de l'échantillon est *n* = 100 et la classe 1 correspond à une perturbation de la forêt, 2 à une forêt et 3 à une zone non forestière.

Comme la moyenne de l'échantillon est un estimateur sans biais de la moyenne de la population, le calcul des proportions de surface est simple ; on définit   *y_i* = 1 si une perturbation de forêt a été observée à l'emplacement de l'échantillon *i* et 0 sinon ; la valeur de la perturbation de forêt est donnée par (Cochran, 1977, p. 22)[^fn1]:

![](https://latex.codecogs.com/svg.latex?\Large&space;\hat{y}=\frac{1}{n}\sum_{i=1}^{n}y_i)


Dans le tableur, tapez dans la cellule C1 "y_i" et dans C2 "=if(B2=1,1,0)" et étendez à la cellule C101. Vous devriez voir :

| | A             | B            | C  |D     |E   
|-|:--------------|:-------------|:------|:-----|:---|
|1| Map           | Ref.         | y_i   |      |    |
|2| 2             |  2           | 0     |      |    |
|3| 2             |    2         | 0     |	    |    |
|4| 1             |    1         | 1     |      |    |
|5| 2             |    2         | 0     |      |    |

Dans la cellule D1, tapez *Area for. dist.*, et dans D2 "=sum(B2:B101)/100" pour construire un estimateur SRS et l'appliquer aux résultats de l'échantillon. Vous devriez voir :

| | A             | B            | C     |D        |E   
|-|:--------------|:-------------|:------|:--------|:---|
|1| Map           | Ref.    | y_i   | Area FD |    |
|2| 2             |  2           | 0     | 0.14    |    |
|3| 2             |    2         | 0     |	       |    |
|4| 1             |    1         | 1     |         |    |
|5| 2             |    2         | 0     |         |    |


Calculons maintenant la marge d'erreur de l'estimation de la surface. L'estimateur de variance SRS est (Cochran, 1977, p. 26)[^fn1]

![](https://latex.codecogs.com/svg.latex?\Large&space;\hat{V}(\hat{y})=\frac{s^2}{n}&space;=&space;\frac{\sum&space;(y_i-\bar{y})^2}{n(n-1)})

Pour appliquer l'estimateur de variance dans le tableur, tapez dans la cellule  D3 "Variance", et dans la cellule  D4  "=sum(ArrayFormula((C4:C103-D24)^2))/(100 * 99)" pour appliquer l'estimateur de variance ; il devrait donner   0.001414. Tapez maintenant "Standard error" en D5, et en  D6: "=sqrt(C4)"; typez  "95% CI" en D7 et en  D8: "=1.96*D6". Enfin tapez   "Margin of error" en D9 et en D10 et "=D8/D2":

| | A             | B            | C     |D        |E   
|-|:--------------|:-------------|:------|:--------|:---|
|1| Map           | Ref.         | y_i   | Area FD |    |
|2| 2             |  2           | 0     | 0.14    |    |
|3| 2             |    2         | 0     |Variance	       |    |
|4| 1             |    1         | 1     |  0.001414       |    |
|5| 2             |    2         | 0     | Standard error  |    |
|6| 2             |    2         | 0     |  0.0376         |    |
|7| 2             |    2         | 0     | 95% CI          |    |
|8| 1             |    1         | 1     | 0.0737          |    |
|9| 2             |    1         | 1     | Margin of error |    |
|10| 2             |    2         | 0    | 53%             |    |

Nous avons maintenant estimé la zone de perturbation forestière à l'aide d'un échantillon de 100 unités collectées dans le cadre du SRS à 0,14 +- 0,074, ce qui correspond à une marge d'erreur de 53 %. Notez que les informations cartographiques de la colonne A n'ont pas été utilisées.  

Enfin, calculons la précision de la carte, en commençant par la précision globale : tapez "Overall acc." dans la cellule E1, et dans E2 "=COUNTIF(A2:A101,B2:B101)/100" -- cette expression comptera le nombre de cas où la carte et les étiquettes de référence concordent et divisera par la taille de l'échantillon. La précision globale est la proportion globale de la zone correctement classée.

Dans la cellule F1, tapez "User's acc. FD" et dans F2 "=countifs(A1:A101, "1",B1:B101, "1")/countif(A1:A101,1)" ; la précision de l'utilisateur de la classe de la carte  “est la probabilité conditionnelle qu'une zone classée comme catégorie i par la carte soit classée comme catégorie i par les données de référence” (Stehman, 1997, p. 79):

Enfin, dans la cellule G1, tapez "Prod. acc. FD" et dans G2 "=countifs(A1:A101, "1",B1:B101, "1")/countif(B1:B101,1)" ; la précision de la classe de la carte est “tla probabilité conditionnelle qu'une zone classée comme catégorie j par les données de référence soit classée comme catégorie j par la carte ” (Stehman, 1997, p. 79).

| | A             | B            | C     |D        |E           |F             |G
|-|:--------------|:-------------|:------|:--------|:-----------|:-------------|:------------|
|1| Map           | Ref.         | y_i   | Area FD |Overall acc.|User's acc. FD|Prod. acc. FD|
|2| 2             |    2         | 0     | 0.14    | 0.65  |0.80|0.86|
|3| 2             |    2         | 0     |Variance         |    | |
|4| 1             |    1         | 1     |  0.001414       |    | |
|5| 2             |    2         | 0     | Standard error  |    | |
|6| 2             |    2         | 0     |  0.0376         |    | |
|7| 2             |    2         | 0     | 95% CI          |    | |
|8| 1             |    1         | 1     | 0.0737          |    | |
|9| 2             |    1         | 1     | Margin of error |    | |
|10| 2             |    2         | 0     | 53%            |    | |


## 3. L'estimation stratifiée
Lors de l'analyse de l'échantillon SRS dans l'exemple ci-dessus, aucune donnée cartographique n'a été utilisée. Bien qu'un échantillonnage aléatoire simple facilite la sélection et l'analyse de l'échantillon, nous pouvons obtenir un gain de précision dans les estimations si nous stratifions la zone d'étude avant de tirer l'échantillon. En particulier, si les strates sont définies pour correspondre à des sous-populations homogènes, c'est-à-dire que les caractéristiques de la population "varient peu d'une unité à l'autre, des estimations plus précises de la moyenne d'une strate peuvent être obtenues à partir d'un petit échantillon dans cette strate" (Cochran , 1977, p.89)[^fn1]. Dans le tutoriel CODED, une carte a été produite qui classait le paysage en forêt perturbée, forêt stable et non-forêt. Si nous sommes intéressés par une estimation de la superficie de la perturbation de la forêt, en utilisant la carte que nous avons produite - à condition qu'elle soit précise - nous devrions pouvoir produire une estimation précise à partir d'un échantillon relativement petit dans cette strate. 

Lorsqu'on utilise une carte pour stratifier la région étudiée dans le cadre d'un échantillonnage aléatoire stratifié, il est courant et pratique de présenter les résultats de l'échantillon dans une matrice d'erreurs (également appelée matrice de confusion ou de contingence). Une matrice d'erreurs est un tableau croisé des observations de référence et des étiquettes de la carte aux emplacements de l'échantillon. Il existe plusieurs façons de créer une matrice d'erreurs. Par exemple, considérez la feuille de calcul suivante, créée dans le cadre du tutoriel sur la sélection d'échantillons ; les labels cartographiques des unités d'échantillonnage figurent dans la colonne des cartes, et supposons que nous ayons collecté des observations de référence, enregistrées dans la colonne des références: [Lien Feuille de Calcul](https://docs.google.com/spreadsheets/d/1-Z2LmLmwfxlVHwezO9N74P7GjfN_y0gjxUblKTfmCc8/edit?usp=sharing) 

Les codes sont les suivants 
1 : Forêt stable
2 : Non-forêt stable
3 : perturbation de forêt
4 : Tampon dans la forêt autour de la perturbation de forêt  

Sur les lignes 1 à 8 et les colonnes E à K, créez la matrice suivante :

| | A    | B   | C    |D |E      |F        |G         |H         |I        |J            |K     |L       |
|-|:-----|:----|:-----|:-|:------|:--------|:---------|:---------|:--------|:------------|:-----|:------|
|1| ID  | Map  | Ref. |  |*Sample*|*count* |*error*   |*matrix*  |         |             |       |      |
|2| 1    |  1  | 1    |  |      |          | R        |E         |F.       |             |       |      |
|3| 2    |  1  | 1    |  |      |          | Forest   |Non-forest|For. Dis.| Buffer      |Total  |*Wh*  |
|4| 3    |  4  | 1    |  |  M   |Forest    |          |          |         |             |       |      |
|5| 4    |  3  | 3    |  |  A   |Non-forest|          |          |         |             |       |      |
|6| 5    |  1  | 1    |  | P    |For. Dis. |          |          |         |             |       |      |
|7| 6    |  2  | 2    |  |      |Buffer    |          |          |         |             |       |      |
|8| 7    |  1  | 1    |  |      |Total     |          |          |         |             |       |      |

Premièrement, ajoutez les poids des strates du tutoriel sur le plan d'échantillonnage (0,551, 0,407, 0,0137, 0,0287). Dans la cellule G4, nous voulons maintenant calculer le nombre d'unités de l'échantillon que nous avons cartographiées comme forêt et également observées comme forêt dans les données de référence -- nous le faisons avec l'expression suivante : "=countifs(B1:B536,"1",C1:C536,"1")". Refaites le calcul pour les non-forêts dans la cellule H5, mais changez le "1" en "2" ; puis à nouveau dans les cellules I6 et J7. Dans la cellule H4, nous voulons calculer le nombre d'unités d'échantillonnage qui ont été cartographiées comme étant de la forêt mais observées comme étant non forestières dans les données de référence -- spécifiez dans la cellule H4 "=countifs(B1:B536, "1",C1:C536, "2")". Refaites le calcul pour toutes les cellules restantes en modifiant le code en fonction de la position de la cellule ; et additionnez les totaux. Cela devrait donner la matrice suivante :


| | A    | B   | C    |D |E      |F        |G         |H         |I        |J       |K        |L      |
|-|:-----|:----|:-----|:-|:------|:--------|:---------|:---------|:--------|:-------|:--------|:------|
|1| ID  | Map  | Ref. |  |*Error*|*matrix* |          |          |         |        |         |       |
|2| 1    |  1  | 1    |  |*sample*| *counts*| R       |E         |F.       |        |         |       |
|3| 2    |  1  | 1    |  |      |          | Forest   |Non-forest|For. Dis.| Buffer |Total    |*Wh*   |
|4| 3    |  4  | 1    |  |  M   |Forest    |271       | 3        | 1       |0       |275      |0.551  |
|5| 4    |  3  | 3    |  |  A   |Non-forest| 6        |193       | 1       |0       |200      |0.407  |
|6| 5    |  1  | 1    |  | P    |For. Dis. | 2        |1         | 27      |0       |30       |0.0137 |
|7| 6    |  2  | 2    |  |      |Buffer    | 23       |0         | 7       |0       |30       |0.0287 |
|8| 7    |  1  | 1    |  |      |Total     | 302      |197       | 36      |0       |535      | 1     |

Quelques éléments intéressants à noter ici : il n'y a pas d'observations de référence pour la zone tampon car nous n'observons évidemment pas les unités comme étant "tampon". Il est important de noter que nous avons maintenant estimé le nombre d'erreurs dans la carte : nous avons une erreur pour chaque perturbation forestière omise dans les strates forestières et non forestières, et sept dans la strate tampon. Nous avons également deux erreurs plus une de perturbation de forêt engagée. 

Parce que nous avons échantillonné la Colombie selon un échantillonnage aléatoire stratifié, la moyenne n'est plus un estimateur sans biais de la moyenne de la population, sauf si nous devons tenir compte des poids des strates. Il est donc plus utile d'exprimer la matrice d'erreurs sous forme de proportions de zones plutôt que de nombres d'échantillons. Pour ce faire, copiez la matrice d'erreurs sur la ligne 10 mais laissez les cellules vides :     

| | A   | B  | C |D |E      |F        |G         |H         |I        |J       |K        |L      |
|-|:----|:---|:--|:-|:------|:--------|:---------|:---------|:--------|:-------|:--------|:------|
| 9|  8 |  2 | 2 |  |       |         |          |          |         |       |         |       |
|10|  9 |  2 | 2 |  |*Error*|*matrix* |          |          |         |       |         |       |
|11| 10 |  2 | 2 |  |*area*|*proportions*| R     |E         |F.       |       |         |       |
|12| 11 |  3 | 3 |  |      |          | Forest   |Non-forest|For. Dis.| Buffer|Total    |*Wh*   |
|13| 12 |  1 | 1 |  |  M   |Forest    |          |          |         |       |         |0.551  |
|14| 13 |  1 | 1 |  |  A   |Non-forest|          |          |         |       |         |0.407  |
|15| 14 |  1 | 1 |  | P    |For. Dis. |          |          |         |       |         |0.0137 |
|16| 15 |  2 | 2 |  |      |Buffer    |          |          |         |       |         |0.0287 |
|17| 16 |  3 | 3 |  |      |Total     |          |          |         |       |         | 1     |

The estimated area proportions of a cell belonging to stratum *h* and observed in the reference data as *j* is (*h+* denotes a sum across columns; hence, *n<sub>h+</sub>* means the sample size allocated to stratum *h*)

Les proportions de surface estimées d'une cellule appartenant à la strate *h* et observées dans les données de référence en tant que *j* sont (*h+* désigne une somme entre les colonnes ; par conséquent, *n<sub>h+</sub>* signifie la taille de l'échantillon alloué à la strate *h*)

![](https://latex.codecogs.com/gif.latex?\Large&space;\hat{p}_{hj}&space;=&space;W_h&space;\frac{n_{hj}}{n_{h&plus;}})

To estimate the area proportions, type in G13: "=$L12*G4/$K4" and expand to J13. Redo the calculation for the rows, which should give the following matrix:

| | A   | B  | C |D |E      |F        |G         |H         |I        |J       |K        |L      |
|-|:----|:---|:--|:-|:------|:--------|:---------|:---------|:--------|:-------|:--------|:------|
| 9|  8 |  2 | 2 |  |       |         |          |          |         |       |         |       |
|10|  9 |  2 | 2 |  |*Error*|*matrix* |          |          |         |       |         |       |
|11| 10 |  2 | 2 |  |*area*|*proportions*| R     |E         |F.       |       |         |       |
|12| 11 |  3 | 3 |  |      |          | Forest   |Non-forest|For. Dis.| Buffer|Total    |*Wh*   |
|13| 12 |  1 | 1 |  |  M   |Forest    |0.54299|0.00601|0.00200|0|0.55100|0.551  |
|14| 13 |  1 | 1 |  |  A   |Non-forest| 0.01221|0.39276|0.00204|0|0.40700 |0.407  |
|15| 14 |  1 | 1 |  | P    |For. Dis. | 0.00091|0.00046|0.01233|0|0.01370 |0.0137  |
|16| 15 |  2 | 2 |  |      |Buffer    |0.02200|0      |0.00670|0|0.02870 |0.0287  |
|17| 16 |  3 | 3 |  |      |Total     | 0.57811|0.39922|0.02307|0|1 |1  |

Si nous avons effectué les calculs correctement, les totaux des lignes doivent être égaux aux poids des strates, car il s'agit des proportions de surface estimées des strates. Avec la matrice d'erreur exprimée en proportions de surface, nous pouvons facilement appliquer un estimateur stratifié pour estimer la surface de chaque catégorie. (Cochran, 1977, Eq. 5.52)[^fn1] : 

![](https://latex.codecogs.com/gif.latex?\Large&space;\hat{\mu}_{j}=\hat{p}_{+j}&space;=&space;\sum_{h=1}^H&space;W_h&space;\frac{n_{hj}}{n_{h&plus;}})

Dans la matrice d'erreur des proportions estimées de la zone, les estimations stratifiées sont égales aux totaux des colonnes. Par conséquent,

![](https://latex.codecogs.com/gif.latex?\Large&space;\hat{\mu}_{1}=0.578;\hat{\mu}_{2}=0.399;\hat{\mu}_{3}=0.231)

Nous devons maintenant appliquer un estimateur de variance stratifié pour construire un intervalle de confiance à 95% autour des estimations. L'estimateur de la variance stratifiée est(Cochran, 1977, Eq. 5.57)

![](https://latex.codecogs.com/gif.latex?\Large&space;\hat{V}(\hat{\mu}_{j})=\sum_{h=1}^H&space;W_h^2&space;\frac{\frac{n_{hj}}{n_{h+}}(1-\frac{n_{hj}}{n_{h+}})}{n_{h+}-1}=\sum_{h=1}^H&space;\frac{W_h\hat{p}_{hj}-\hat{p}_{hj}^2}{n_{h+}-1})

Pour appliquer l'estimateur de variance aux résultats de l'échantillon dans la matrice d'erreurs, tapez dans la cellule  F17 "V(*μ*)" et en G17 "=($L12*G12-G12^2)/($K4-1) + ($L13*G13-G13^2)/($K5-1) + ($L14*G14-G14^2)/($K6-1) + ($L15*G15-G15^2)/($K7-1)" et étendre à  J18. 

Tapez maintenant  "SE(*μ*)" idans la cellule F18 pour calculer l'erreur standard ; dans la cellule G18, tapez "=sqrt(G17)"  et élargissez à J18. Tapez ensuite  "±95% CI" dans la cellule F19 et dans la cellule G19 tapez "=G18*1.96" et étendez à J19. Enfin, tapez  "MoE [%]" dans la cellule F20 et dans la cellule G20 tapez  "=G19/G16" aet développez jusqu'à I20, et convertissez les cellules G à I de la ligne 20 en pourcentage. Cela devrait donner le résultat suivant :


| | A   | B  | C |D |E      |F        |G         |H         |I          |J |K |L  |
|-|:----|:---|:--|:-|:------|:------|:----------|:----------|:----------|:-|:-|:--|
|16| 15 |  2 | 2 |  |      |Total   | 0.57811   |0.39922    |0.02307    |0 |1 |1  |
|17| 16 |  3 | 3 |  |      |V(μ)	|0.0000456	|0.0000403	|0.0000138	|0| |
|18| 17 |  1 | 2 |  |      |SE(μ)	|0.0067520	|0.0063466	|0.0037174	|0| |
|19| 18 |  2 | 2 |  |      |±95% CI	|0.0132339	|0.0124393	|0.0072862	|0| |
|20| 19 |  4 | 1 |  |      |MoE [%]	|2.29%	    |3.12%	    |31.59%	    |0| |

Ceci conclut l'estimation stratifiée de la superficie (il s'agit de la proportion de la superficie et elle doit être multipliée par la superficie totale de la Colombie pour exprimer les estimations en unités de superficie) :

![](https://latex.codecogs.com/gif.latex?\Large&space;\hat{\mu}_{1}=0.578\pm0.0132)
![](https://latex.codecogs.com/gif.latex?\Large&space;\hat{\mu}_{2}=0.399\pm0.0124)
![](https://latex.codecogs.com/gif.latex?\Large&space;\hat{\mu}_{3}=0.231\pm0.0072)


Enfin, calculons la précision de la carte et des classes de cartes, en commençant par la précision de l'utilisateur. Dans la cellule   F21 Dans la cellule   "User's acc." et en  G21 "=G12/K12"; H21 "=H13/K13"; I21 "=I14/K14". Répétez  à la ligne 22 avec les cellules G22 "=G12/G16"; H22 "=H13/H16"; I22 "=I14/I16". Ajoutez la précision globale à la ligne 23 comme   "=sum(G12,H13,I14)". Cela devrait donner ce qui suit :

| | A   | B  | C |D |E      |F        |G         |H         |I          |J |K |L  |
|-|:----|:---|:--|:-|:------|:------|:----------|:----------|:----------|:-|:-|:--|
|16| 15 |  2 | 2 |  |      |Total   | 0.57811   |0.39922    |0.02307    |0 |1 |1  |
|17| 16 |  3 | 3 |  |      |V(μ)	|0.0000456	|0.0000403	|0.0000138	|0| |
|18| 17 |  1 | 2 |  |      |SE(μ)	|0.0067520	|0.0063466	|0.0037174	|0| |
|19| 18 |  2 | 2 |  |      |±95% CI	|0.0132339	|0.0124393	|0.0072862	|0| |
|20| 19 |  4 | 1 |  |      |MoE [%]	|2.29%	    |3.12%	    |31.59%	    |0| |
|21| 20 |  3 | 3 |  |      |User's acc.	|0.985	    |0.965	    |0.900	    |0| |
|22| 21 |  3 | 3 |  |      |Prod. acc.	|0.939	    |0.984	    |0.535	    |0| |
|23| 22 |  2 | 2 |  |      |Over. acc.	|0.948	    |    |	    || |


## 4. Estimation de la précision d'une carte différente de la stratification initiale

Lorsque les résultats de l'échantillon ont été collectés à l'aide d'une stratification différente de la carte que nous voulons utiliser pour l'évaluation de la précision, nous ne pouvons pas appliquer les estimateurs stratifiés classiques illustrés ci-dessus, car ils sont biaisés lorsque les lignes de la matrice d'erreur de la population ne correspondent pas aux strates utilisées pour sélectionner l'échantillon. Au lieu de cela, nous devons construire des estimateurs de ratio en utilisant des fonctions indicatrices (Stehman, 2014)[^fn4]. Pour simplifier, réduisons les résultats de notre échantillon à deux classes d'observations de référence :  *h* = 1 est la perturbation de la forêt et *h* = 2 est la non perturbation ; et en outre, que nous avons construit une nouvelle carte de perturbation et de non perturbation. 

Pour estimer la précision globale de la nouvelle carte en utilisant les résultats de notre échantillon existant, définissez les variables suivantes

![](https://latex.codecogs.com/gif.latex?y_u%5EO%20%3D%20%5Cbegin%7Bcases%7D%201%20%26%20%5Ctext%7Bif%20unit%20%5Ctextit%7Bu%7D%20is%20classified%20correctly%7D%5C%5C%200%20%26%20%5Ctext%7Bif%20unit%20%5Ctextit%7Bu%7D%20is%20classified%20incorrectly%7D%20%5Cend%7Bcases%7D)

La précision globale la moyenne de population  ![](https://latex.codecogs.com/gif.latex?%5Cinline%20%5Cdpi%7B100%7D%20%5Cbar%7BY%7D) basée sur un recensement de N pixels dans la région ; ![](https://latex.codecogs.com/gif.latex?%5Cinline%20%5Cdpi%7B100%7D%20%5Cbar%7BY%7D) iest équivalent à la proportion de pixels correctement classés, c'est-à-dire la précision globale. Un estimateur sans biais de   ![](https://latex.codecogs.com/gif.latex?%5Cinline%20%5Cdpi%7B100%7D%20%5Cbar%7BY%7D) est le suivant

![](https://latex.codecogs.com/gif.latex?%5Chat%7BO%7D%20%3D%20%5Chat%7B%5Cbar%7BY%7D%7D%20%3D%20%5Cfrac%7B%5Csum%20N_h%5E*%20%5Cbar%7By%7D_h%5EO%7D%7BN%7D%20%3D%20%5Cfrac%7BN_1%5E*%20%5Cbar%7By%7D_1%5EO%7D%7BN%7D%20&plus;%20%5Cfrac%7B%20N_2%5E*%20%5Cbar%7By%7D_2%5EO%7D%7BN%7D%20%3D%20%5Cfrac%7B1%7D%7BN%7D%20%28N_1%5E*%20%5Csum_%7Bu%20%5Cin%20h%3D1%7D%20%5Cfrac%7By_u%5EO%7D%7Bn_1%5E*%7D%20&plus;%20N_2%5E*%20%5Csum_%7Bu%20%5Cin%20h%3D2%7D%20%5Cfrac%7By_u%5EO%7D%7Bn_2%5E*%7D%29)

Pour la précision de l'utilisateur de la nouvelle carte, définissez les deux variables suivantes

![](https://latex.codecogs.com/gif.latex?y_u%5EU%20%3D%20%5Cbegin%7Bcases%7D%201%20%26%20%5Ctext%7Bif%20unit%20%5Ctextit%7Bu%7D%20is%20classified%20correctly%20and%20map%20class%20forest%20dist.%7D%5C%5C%200%20%26%20%5Ctext%7Botherwise%3B%7D%20%5Cend%7Bcases%7D%20)

![](https://latex.codecogs.com/gif.latex?x_u%5EU%20%3D%20%5Cbegin%7Bcases%7D%201%20%26%20%5Ctext%7Bif%20unit%20%5Ctextit%7Bu%7D%20is%20map%20class%20forest%20dist.%7D%5C%5C%200%20%26%20%5Ctext%7Botherwise.%7D%20%5Cend%7Bcases%7D)


and for producer's accuracy:

![](https://latex.codecogs.com/gif.latex?y_u%5EP%20%3D%20%5Cbegin%7Bcases%7D%201%20%26%20%5Ctext%7Bif%20unit%20%24u%24%20is%20correctly%20classified%20and%20reference%20class%20forest%20dist.%7D%5C%5C%200%20%26%20%5Ctext%7Botherwise%3B%7D%20%5Cend%7Bcases%7D)

![](https://latex.codecogs.com/gif.latex?x_u%5EP%20%3D%20%5Cbegin%7Bcases%7D%201%20%26%20%5Ctext%7Bif%20unit%20%5Ctextit%7Bu%7D%20is%20reference%20class%20forest%20dist.%7D%5C%5C%200%20%26%20%5Ctext%7Botherwise.%7D%20%5Cend%7Bcases%7D)

Nous pouvons maintenant estimer la précision de l'utilisateur et du producteur de la classe de perturbation de forêt en utilisant un estimateur de ratio avec les moyennes de *x* et *y* spécifiques à la strate :

![](https://latex.codecogs.com/gif.latex?%5Chat%7BR%7D%20%3D%20%5Cfrac%7B%5Chat%7BY%7D%7D%7B%5Chat%7BX%7D%7D%20%3D%20%5Cfrac%7B%5Csum_%7Bh%3D1%7D%5EH%20N_h%5E*%20%5Cbar%7By%7D_h%7D%7B%5Csum_%7Bh%3D1%7D%5EH%20N_h%5E*%20%5Cbar%7Bx%7D_h%7D)

Notez que  ![](https://latex.codecogs.com/gif.latex?%5Cinline%20%5Cdpi%7B100%7D%20N_h%5E*) est la taille de la population et   ![](https://latex.codecogs.com/gif.latex?%5Cinline%20%5Cdpi%7B100%7D%20n_h%5E*) celle de l'échantillon dans les résultats de l'échantillon, par opposition à la   ![](https://latex.codecogs.com/gif.latex?%5Cinline%20%5Cdpi%7B100%7D%20N_h)  taille de la population et   ![](https://latex.codecogs.com/gif.latex?%5Cinline%20%5Cdpi%7B100%7D%20n_h) staille de l'échantillon dans la nouvelle carte.  En comptant les *x* et *y* dans la nouvelle carte, nous calculons le nombre d'échantillons pour remplir la matrice d'erreurs suivante :

![](https://latex.codecogs.com/gif.latex?%5Cdpi%7B120%7D%20%5Cbegin%7Btabular%7D%7B%20l%20c%20c%20c%20c%7D%20Stratum%20%26%20%24%5Cbar%7By%7D_u%5EU%24%20%26%20%24%5Cbar%7Bx%7D_u%5EU%24%20%26%20%24%5Cbar%7By%7D_u%5EP%24%20%26%20%24%5Cbar%7Bx%7D_u%5EP%24%20%5C%5C%20%5Chline%201.%20Forest%20Dist.%20%26%20%24%5Cfrac%7B%5Csum%20y_u%5EU%7D%7Bn_1%5E*%7D%24%20%26%20%24%5Cfrac%7B%5Csum%20x_u%5EU%7D%7Bn_1%5E*%7D%24%20%26%20%24%5Cfrac%7B%5Csum%20y_u%5EP%7D%7Bn_1%5E*%7D%24%20%26%20%24%5Cfrac%7B%5Csum%20x_u%5EP%7D%7Bn_1%5E*%7D%24%5C%5C%202.%20Non-Dist.%20%26%20%24%5Cfrac%7B%5Csum%20y_u%5EU%7D%7Bn_2%5E*%7D%24%20%26%20%24%5Cfrac%7B%5Csum%20x_u%5EU%7D%7Bn_2%5E*%7D%24%20%26%20%24%5Cfrac%7B%5Csum%20y_u%5EP%7D%7Bn_2%5E*%7D%24%20%26%20%24%5Cfrac%7B%5Csum%20x_u%5EP%7D%7Bn_2%5E*%7D%24%20%5Cend%7Btabular%7D)


qui permet d'utiliser facilement l'estimateur de ratio pour l'estimation de la précision de l'utilisateur et du producteur de la nouvelle classe de perturbation de la forêt (![](https://latex.codecogs.com/gif.latex?%5Cinline%20%5Cdpi%7B100%7D%20U_1) and ![](https://latex.codecogs.com/gif.latex?%5Cinline%20%5Cdpi%7B100%7D%20P_1)):

![](https://latex.codecogs.com/gif.latex?%5Cdpi%7B120%7D%20%5Chat%7BU%7D_1%20%3D%20%5Chat%7BR%7D%20%3D%20%5Cfrac%7B%5Cfrac%7BN_1%5E*%7D%7Bn_1%5E*%7D%20%5Csum_%7Bu%20%5Cin%20h%3D1%7D%20y_u%5EU%20&plus;%20%5Cfrac%7BN_2%5E*%7D%7Bn_2%5E*%7D%20%5Csum_%7Bu%20%5Cin%20h%3D2%7D%20y_u%5EU%7D%7B%5Cfrac%7BN_1%5E*%7D%7Bn_1%5E*%7D%20%5Csum_%7Bu%20%5Cin%20h%3D1%7D%20x_u%5EU%20&plus;%20%5Cfrac%7BN_2%5E*%7D%7Bn_2%5E*%7D%20%5Csum_%7Bu%20%5Cin%20h%3D2%7D%20x_u%5EU%7D)

![](https://latex.codecogs.com/gif.latex?%5Cdpi%7B120%7D%20%5Chat%7BP%7D_1%20%3D%20%5Chat%7BR%7D%20%3D%20%5Cfrac%7B%5Cfrac%7BN_1%5E*%7D%7Bn_1%5E*%7D%20%5Csum_%7Bu%20%5Cin%20h%3D1%7D%20y_u%5EP%20&plus;%20%5Cfrac%7BN_2%5E*%7D%7Bn_2%5E*%7D%20%5Csum_%7Bu%20%5Cin%20h%3D2%7D%20y_u%5EP%7D%7B%5Cfrac%7BN_1%5E*%7D%7Bn_1%5E*%7D%20%5Csum_%7Bu%20%5Cin%20h%3D1%7D%20x_u%5EP%20&plus;%20%5Cfrac%7BN_2%5E*%7D%7Bn_2%5E*%7D%20%5Csum_%7Bu%20%5Cin%20h%3D2%7D%20x_u%5EP%7D)

## 5. Post-stratification
Comme expliqué dans le tutoriel sur le plan d'échantillonnage, un avantage important du SRS/SYS est la possibilité de stratifier la zone d'étude après la collecte des résultats de l'échantillonnage. L'application d'une stratification après l'échantillonnage est appelée post-stratification (PSTR), ce qui est susceptible d'augmenter la précision des estimations, et il y a rarement des raisons de ne pas post-stratifier, à condition que des cartes existent sur la zone d'étude. Un autre avantage est que l'estimateur stratifié illustré à la section 3, **Estimation stratifiée** ci-dessus, est directement applicable aux données de l'échantillon SRS ou SYS lorsqu'il est croisé avec les étiquettes de la post-stratification dans une matrice d'erreurs (dans ce cas, l'estimateur stratifié est appelé estimateur post-stratifié mais la formule est exactement la même). Par conséquent, pour appliquer un estimateur PSTR, il suffit de suivre les étapes décrites dans la section 3, **Estimation stratifiée** ci-dessus.

Une différence importante entre l'estimation STR et PSTR est la formule de l'estimateur de la variance. Selon   Lohr (1999, Eq. 4.22)[^fn5] si *Wh* est connu et que “*nh* est raisonnablement grand (≥30 environ)” - ou “raisonnablement grand, disons > 20 dans chaque strate” (Cochran 1977, p. 134)[^fn1] – l'estimateur de variance est

![](https://latex.codecogs.com/gif.latex?\Large&space;\hat{V}(\hat{\mu}_{PSTR})\approx\sum_{h=1}^H&space;W_h\frac{s_h^2}{n_{h}})

Pour les proportions (Cochran, 1977, Eq. 3.5)[^fn1], la variance de la strate *h* peut être exprimée comme suit

![](https://latex.codecogs.com/gif.latex?\Large&space;s_h^2=\frac{n_h}{n_{h}-1}p_h(1-p_h))

Dans une matrice d'erreur traditionnelle, *p_h = n_hj ÷ n_h* where *n_hj* iest le nombre d'échantillons de la classe de référence *j* dans la strate *h*. En combinant l'approximation de la variance de Lohr et l'expression de Cochran pour la variance de strate, on obtient un estimateur de variance post-stratifié exprimé à l'aide des éléments d'une matrice d'erreurs :

![](https://latex.codecogs.com/gif.latex?%5Chat%7BV%7D%28%5Chat%7B%5Cmu%7D_%7BPSTR%7D%29%5Capprox%5Csum_%7Bh%3D1%7D%5EH%26space%3BW_h%5Cfrac%7Bs_h%5E2%7D%7Bn_%7Bh%7D%7D%3D%5Cfrac%7B1%7D%7Bn%7D%5Csum_%7Bh%3D1%7D%5EHW_h%5Cfrac%7Bn_h%7D%7Bn_h-1%7Dp_h%281-p_h%29%3D%5Cfrac%7B1%7D%7Bn%7D%5Csum_%7Bh%3D1%7D%5EHW_h%5Cfrac%7Bn_%7Bhj%7D%281-%5Cfrac%7Bn_%7Bhj%7D%7D%7Bn_{h+}%7D%29%7D%7Bn_{h+}-1%7D)

Si vous comparez cela à l'estimateur de variance STR Section 3, **Estimation stratifiée** ci-dessus, vous verrez que l'estimateur de variance PSTR est très similaire mais pas identique.  


## 6. Logiciel pour automatiser l'analyse des résultats des échantillons  

### 6.1 AREA2
L'application AREA2 de Google Earth Engine contient les équations de tous les estimateurs décrits dans ce tutoriel. Notez que dans AREA2, l'estimateur SRS est désigné par son nom officiel, l'estimateur d'expansion.  AREA2 est disponible ici : [Lien application AREA2](https://code.earthengine.google.com/?accept_repo=projects/AREA2/public) et une documentation plus détaillée ici :[Lien documentation plus approfondie ]( https://area2.readthedocs.io/)

### 6.2 SEPAL
L'estimation stratifiée est automatisée dans SEPAL ; la documentation est disponible ici: https://github.com/sig-gis/SEPAL-CEO  Faites défiler la page jusqu'à *Exercice 4.3 : Estimation de la surface et de l'incertitude* pour une description de l'estimation stratifiée.  

## Licence
Cet ouvrage est soumis à une licence  [Creative Commons Attribution 3.0 IGO](https://creativecommons.org/licenses/by/3.0/igo/) 

Copyright 2020, Banque mondiale. Ce travail a été développé par Pontus Olofsson dans le cadre d'un contrat de la Banque mondiale avec GRH Consulting, LLC pour le développement de nouvelles ressources - et la collecte de ressources existantes - liées à la mesure, la notification et la vérification pour soutenir la mise en œuvre du MRV par les pays. 

Attribution : Olofsson, P. (2021). *MRV ouvert : Analyse d'un échantillon de données*. Banque mondiale. Licence : Licence Creative Commons Attribution (CC BY 3.0 IGO)



## References
[^fn1]: Cochran, W. G. (1977). *Sampling Techniques*. New York, NY: Wiley

[^fn2]: Casella, G., & Berger, R. L. (2002). *Statistical Inference* (2nd ed.). Pacific Grove, CA: Duxbury Press

[^fn3]: Rice, J. A. (1995). *Mathematical Statistics and Data Analysis* (2nd ed.). Belmont, CA: Duxbury Press

[^fn4]: Stehman, S. V. (2014). Estimating area and map accuracy for stratified random sampling when the strata are different from the map classes. *International Journal of Remote Sensing*, 35(13), 4923-4939

[^fn5]: Lohr, S. L. (1999). *Sampling: Design and Analysis*. CRC Press




