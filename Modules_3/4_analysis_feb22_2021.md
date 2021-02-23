# Analysis of sample data 

## 1. Background

In the previous tutorials, we designed and drew a sample from the country of Colombia, and we observed and recorded the reference land cover conditions at the locations of sample units. The collection of reference observations is referred to as the sample results or data, or the reference classification. In this tutorial we will apply various estimators to the sample data to estimate characteristics of the population we sampled -- i.e. characteristics of the country of Colombia such as the area of forest disturbance. An estimator is “The rule by which an estimate of some population characteristic [i.e. parameter] *μ* is calculated from the sample results” (Cochran, 1977, p. 11)[^fn1]. Note that that an estimator is not the same thing as an estimate – instead “An estimator is a function of the sample, while an estimate is the realized value of an estimator (that is, a number) that is obtained when a sample is actually taken” (Casella & Berger, 2002, p. 312)[^fn2]. An estimator has two important properties: variance and bias. The bias of an estimator *μ^* of a population parameter *μ* is the difference between *μ* and the expected value of *μ^* over all possible samples; that is, ![](https://latex.codecogs.com/gif.latex?\inline&space;\textup{Bias}(\hat{\mu})&space;=&space;\textup{E}(\hat{\mu})&space;-&space;\mu) (Casella & Berger, 2002, p. 330)[^fn2]. If  ![](https://latex.codecogs.com/gif.latex?\inline&space;\textup{Bias}(\hat{\mu})&space;=&space;\textup{E}(\hat{\mu})&space;-&space;\mu=0), then the estimator is said to be unbiased. Note that because an estimate is a number, it has no variance and no bias and therefore cannot be unbiased.

The other important property of an estimator is variance. The formal definition of the variance provides “a measure of the degree of spread of a distribution around its mean” (Casella & Berger, 2002, p. 59)[^fn2]. This definition is not very helpful in our context, instead, we are concerned with situations in which we have sampled a study area to estimate a certain population parameter (e.g. the area of forest or deforestation). For example, if we have a population of from which a sample of has been selected, the sample variance is *s^2^* and is easily calculated for common sampling designs. But the sample variance is less interesting compared to the variance of an estimator. For common designs, we can easily prove that the sample variance *s^2^*  is an unbiased estimator of the population variance *S^2^* (Cochran, 1977, p. 22, 26)[^fn1]. The variance of an estimator *u^*  is ![](https://latex.codecogs.com/gif.latex?\inline&space;\textup{V}(\hat{\mu})&space;=&space;S^2&space;\div&space;n) (assuming a small sample size, *n*, relative the populations size, *N*); the estimated variance of *u^* substitutes the sample variance *s^2^* for the population variance *S^2^* to create the variance estimator of  *u^*   as ![](https://latex.codecogs.com/gif.latex?\inline&space;\hat{V}(\hat{\mu})&space;=&space;s^2&space;\div&space;n) which is the variance estimator of primary interest to us as it allows us to quantify the uncertainty in things like the activity data or other parameters of interst.  

From here we can introduce two more important measures of spread: standard error and confidence interval. The standard error is the standard deviation (i.e. square root of the variance) of an estimator (Rice, 1995, p. 192)[^fn3] and hence has the same unit as the estimate. The standard deviation of an estimator is referred to as its standard error. Because the sample variance is an unbiased estimator of the population variance, we can estimate the standard error using the sample variance: ![](https://latex.codecogs.com/gif.latex?\inline&space;\textup{SE}(\hat{\mu})&space;=&space;\hat{V}(\hat{\mu})&space;\div&space;\sqrt{n}). Note that because a standard error is a standard deviation of an estimator, all standard errors are also standard deviations but not all standard deviations are standard errors. This sometimes causes confusion even though the definitions of standard error and standard deviation are consistent. Neither the variance nor the standard error is typically used to express the uncertainty in estimates, instead, a confidence interval is commonly used: "A 95% confidence interval for *μ* is a random interval that contains *μ* with probability .95; if we were to take many random samples [under the same sampling design] and form a confidence interval from each one, about 95% of these intervals would contain *μ*" (Rice, 1995, p. 217)[^fn3]. Confidence intervals are often in the form ![](https://latex.codecogs.com/gif.latex?\inline&space;\hat{\mu}&space;\pm&space;a\times\textup{SE}(\hat{\mu})) where *a* is a statistic related to the desired confidence level, referred to as z-score or standard score expressed as a percentage between 0 and 100%. For a certain confidence level *p* the area under the standard normal density function from *-z* to *+z* is *p* (Rice, 1995, p. 202)[^fn3]; for example, a confidence interval at the 95% confidence level  correspond to a z-score of 1.96 (often rounded to 2). A condition for using a z-score to compute a confidence interval is that the sampling distribution is approximately a normal distribution, which we can assume for large sample sizes. The confidence interval divided by the estimate is referred to as a margin of error (*MoE*) and is often expressed as a percentage.

The two properties, bias and variance, are important because we can ensure that the estimator we use is unbiased, and we can express the uncertainty in estimates. Neither is possible when using pixel-counting in maps or when sampling without adhering to probability sampling.  Another important aspect of an estimator is that it is a function of the sample, which means that the estimator has to correspond to the sampling design. For example, the sample mean is an unbiased estimator of the population mean for simple random sampling; for stratified random sampling, we need to use a stratified estimator which is expressed as the sum of the means of the simple random samples within strata weighted by stratum weights.

## 2. Analysis of sample results collected under SRS/SYS 
Sample results collected under simple random sampling are the most straightforward to analyze (the same estimators are used for both simple random and systematic sampling). Because no maps/stratifications are used and because the sample mean is unbiased estimator of the population mean, the analysis of SRS/SYS sample results can easily be completed in a spreadsheet.  Stratified random sampling was  illustrated in previous tutorials, and only dummy data are provided here to illustrate the construction of SRS/SYS estimators. Let's assume that the data in this spreadsheet are map and reference labels at locations selected under SRS: https://docs.google.com/spreadsheets/d/1pcK-rlhUo5lvmYqibT4zIv-bR5tF4Uu8DqPwIG8mJWQ/edit?usp=sharing The sample size is *n* = 100 and a label of 1 is forest disturbance, 2 is forest, and 3 is non-forest.         

Because the sample mean is unbiased estimator of the population mean the calculation of area proportions are straightforward; define *y_i* = 1 if forest disturbance was observed at sample location *i* and 0 otherwise; the are of forest disturbance is given by (Cochran, 1977, p. 22)[^fn1]:

![](https://latex.codecogs.com/svg.latex?\Large&space;\hat{y}=\frac{1}{n}\sum_{i=1}^{n}y_i)


In the spreadsheet, type into cell C1 "y_i" and in C2 "=if(B2=1,1,0)" and extend to cell C101. You should see:

| | A             | B            | C  |D     |E   
|-|:--------------|:-------------|:------|:-----|:---|
|1| Map           | Ref.         | y_i   |      |    |
|2| 2             |  2           | 0     |      |    |
|3| 2             |    2         | 0     |	    |    |
|4| 1             |    1         | 1     |      |    |
|5| 2             |    2         | 0     |      |    |

In cell D1, type *Area for. dist.*, and in D2 "=sum(B2:B101)/100" to construct a SRS estimator and apply it to the sample results. You should see:


| | A             | B            | C     |D        |E   
|-|:--------------|:-------------|:------|:--------|:---|
|1| Map           | Ref.    | y_i   | Area FD |    |
|2| 2             |  2           | 0     | 0.14    |    |
|3| 2             |    2         | 0     |	       |    |
|4| 1             |    1         | 1     |         |    |
|5| 2             |    2         | 0     |         |    |


Now lets calculate a margin of error of the area estimate. The SRS variance estimator is (Cochran, 1977, p. 26)[^fn1]

![](https://latex.codecogs.com/svg.latex?\Large&space;\hat{V}(\hat{y})=\frac{s^2}{n}&space;=&space;\frac{\sum&space;(y_i-\bar{y})^2}{n(n-1)})

To apply the variance estimator in the spreadsheet, type in cell D3 "Variance", and in cell D4  "=sum(ArrayFormula((C4:C103-D24)^2))/(100 * 99)" to apply the variance estimator; it should return 0.001414. Now type "Standard error" in D5, and in D6: "=sqrt(C4)"; type "95% CI" in D7 and in D8: "=1.96*D6". Finally type "Margin of error" in D9 and in D10 and "=D8/D2":

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

We have now estimated the area of forest disturbance using a sample of 100 units collected under SRS as 0.14 +- 0.074 corresponding to a margin of error of 53%. Note that the map information in column A was not used.  

Finally, lets calculate the accuracy of the map, starting with the overall accuracy: type "Overall acc." in cell E1, and in E2 "=COUNTIF(A2:A101,B2:B101)/100" -- this expression will count number of instances where the map and reference labels agree and divide by the sample size. The overall accuracy is the overall proportion of area correctly classified.

In cell F1 type "User's acc. FD" and in F2 "=countifs(A1:A101,"1",B1:B101,"1")/countif(A1:A101,1)"; the user’s accuracy of map class “is the conditional probability that an area classified as category i by the map is classified as category i by the reference data” (Stehman, 1997, p. 79):

Finally, in cell G1 type "Prod. acc. FD" and in G2 "=countifs(A1:A101,"1",B1:B101,"1")/countif(B1:B101,1)"; the producer’s accuracy of map class is “the conditional probability that an area classified as category j by the reference data is classified as category j by the map” (Stehman, 1997, p. 79).


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


## 3. Stratified estimation
When analyzing the SRS sample in the example above, no  map data were  used. While a simple random sampling facilitates the sample selection and analysis, we may produce a gain in precision in estimates if we  stratify the study area before drawing the sample. In particular, if the strata are defined to correspond to subpopulations that are homogenous, in that the population characteristics "vary little from unit to another, more precise estimates of any stratum mean can be obtained from a small sample in that stratum" (Cochran , 1977, p.89)[^fn1]. In the CODED tutorial, a map was produced that categorized the landscape into forest disturbance and stable forest and non-forest. If we are interested in an area estimate of the forest disturbance, using the map we produced -- provided it is accurate -- should allow us to produce a precise estimate from a relatively small sample in that stratum. 
 
When using a map to stratify the study region under stratified random sampling, it is common and convenient to present the sample results in an error matrix (also called confusion or contingency matrix). An error matrix is a cross-tabulation of the reference observations and map labels at sample locations. There are several ways to create an error matrix. For example, consider the following spreadsheet that was created in the sample selection tutorial; the map labels at sample units are in the map column, and let's assume that we have collected reference observations which are recorded in reference column: https://docs.google.com/spreadsheets/d/1-Z2LmLmwfxlVHwezO9N74P7GjfN_y0gjxUblKTfmCc8/edit?usp=sharing 

The codes are 
1: Stable forest
2: Stable non-forest
3: forest disturbance
4: Buffer into the forest around forest disturbance  

On rows 1 to 8 and columns E to K, create the following matrix:

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

First, add the strata weights from the sampling design tutorial (0.551, 0.407, 0.0137, 0.0287). In cell G4, we now want to calculate the number of units in the sample that we mapped as forest and also observed as forest in the reference data -- we do that with the following expression: "=countifs(B1:B536,"1",C1:C536,"1")". Redo the calculation for non-forest in cell H5 but change the "1" to "2"; and then again in cell I6 and J7. In cell H4, we want to calculate the number of sample units that were mapped as forest but observed as Non-forest in the reference data -- specify in cell H4 "=countifs(B1:B536,"1",C1:C536,"2")". Redo the  calculation for all the remaining cells by changing the code according to cell position; and sum the totals. This should give the following matrix:


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

A few interesting things to note here:  there are no reference observations of Buffer because we obviously  are not observing units as being "buffer". Of importance is that we now have estimated the number of errors in the map -- we have one error each of omitted forest disturbance in the forest and non-forest strata, and seven in the buffer stratum. We also have  two plus one errors of committed forest disturbance. 

Because we sampled Colombia under stratified random sampling, the mean is no longer an unbiased estimator of the population mean unless we need to account for the strata weights. It is therefore more helpful to express the error matrix as area proportions rather than sample counts. To do this, copy the error matrix to row 10 but leave the cells empty:

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

If we have done the calculations correctly, the row totals should equal the strata weights as these are the estimated area proportions of the strata. With the error matrix expressed in area proportions, we can easily apply a stratified estimator to estimate the area of each category (Cochran, 1977, Eq. 5.52)[^fn1] : 

![](https://latex.codecogs.com/gif.latex?\Large&space;\hat{\mu}_{j}=\hat{p}_{+j}&space;=&space;\sum_{h=1}^H&space;W_h&space;\frac{n_{hj}}{n_{h&plus;}})

In the error matrix of estimated area proportions, the stratified estimates equal the column totals. Hence, 

![](https://latex.codecogs.com/gif.latex?\Large&space;\hat{\mu}_{1}=0.578;\hat{\mu}_{2}=0.399;\hat{\mu}_{3}=0.231)

We now need to apply a stratified variance estimator to construct a 95% confidence interval around the estimates. The stratified variance estimator is (Cochran, 1977, Eq. 5.57)

![](https://latex.codecogs.com/gif.latex?\Large&space;\hat{V}(\hat{\mu}_{j})=\sum_{h=1}^H&space;W_h^2&space;\frac{\frac{n_{hj}}{n_{h+}}(1-\frac{n_{hj}}{n_{h+}})}{n_{h+}-1}=\sum_{h=1}^H&space;\frac{W_h\hat{p}_{hj}-\hat{p}_{hj}^2}{n_{h+}-1})

To apply the variance estimator to the sample results in error matrix, type in cell F17 "V(*μ*)" and in G17 "=($L12*G12-G12^2)/($K4-1) + ($L13*G13-G13^2)/($K5-1) + ($L14*G14-G14^2)/($K6-1) + ($L15*G15-G15^2)/($K7-1)" and expand to J18. 

Now type "SE(*μ*)" in cell F18 to calculate the standard error; in cell G18 type "=sqrt(G17)" and expand to J18. Then type "±95% CI" in cell F19 and in cell G19 type "=G18*1.96" and expand to J19. Finally, type "MoE [%]" in cell F20 and in cell G20 type "=G19/G16" and expand to I20, and convert to cells G to I in row 20  to percent. That should give following:


| | A   | B  | C |D |E      |F        |G         |H         |I          |J |K |L  |
|-|:----|:---|:--|:-|:------|:------|:----------|:----------|:----------|:-|:-|:--|
|16| 15 |  2 | 2 |  |      |Total   | 0.57811   |0.39922    |0.02307    |0 |1 |1  |
|17| 16 |  3 | 3 |  |      |V(μ)	|0.0000456	|0.0000403	|0.0000138	|0| |
|18| 17 |  1 | 2 |  |      |SE(μ)	|0.0067520	|0.0063466	|0.0037174	|0| | 
|19| 18 |  2 | 2 |  |      |±95% CI	|0.0132339	|0.0124393	|0.0072862	|0| |
|20| 19 |  4 | 1 |  |      |MoE [%]	|2.29%	    |3.12%	    |31.59%	    |0| |

That concludes the stratified estimation of area (these are the area proportion and need to be multiplied by the total area of Colombia to express the estimates in area units):

![](https://latex.codecogs.com/gif.latex?\Large&space;\hat{\mu}_{1}=0.578\pm0.0132)
![](https://latex.codecogs.com/gif.latex?\Large&space;\hat{\mu}_{2}=0.399\pm0.0124)
![](https://latex.codecogs.com/gif.latex?\Large&space;\hat{\mu}_{3}=0.231\pm0.0072)


Finally, lets calculate the accuracy of the map and map classes, starting with the user's accuracy. In cell F21 type "User's acc." and in G21 "=G12/K12"; H21 "=H13/K13"; I21 "=I14/K14". Repeat for the producer's accuracy on row 22 with cells G22 "=G12/G16"; H22 "=H13/H16"; I22 "=I14/I16". Add the overall accuracy on row 23 as "=sum(G12,H13,I14)". That should give the following:

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


## 4. Estimating the accuracy of a map different from the original stratification

When sample results have been collected using a stratification different than the map we want to use for accuracy assessment, we cannot apply the conventional stratified estimators illustrated above as these are biased when the rows of the population error matrix do not correspond to the strata used to select the sample. Instead, we need construct ratio estimators using indicator functions (Stehman, 2014)[^fn4]. For simplicity, let us collapse our sample results to two classes of reference observations:  *h* = 1 is forest disturbance and *h* = 2 is non-disturbance; and further, that we have constructed a new map disturbande non-disturbance. 

To esitmate the  overall accuracy of the new map using our existing sample results,  define the following variable 

![](https://latex.codecogs.com/gif.latex?y_u%5EO%20%3D%20%5Cbegin%7Bcases%7D%201%20%26%20%5Ctext%7Bif%20unit%20%5Ctextit%7Bu%7D%20is%20classified%20correctly%7D%5C%5C%200%20%26%20%5Ctext%7Bif%20unit%20%5Ctextit%7Bu%7D%20is%20classified%20incorrectly%7D%20%5Cend%7Bcases%7D)

The overall accuracy the population mean ![](https://latex.codecogs.com/gif.latex?%5Cinline%20%5Cdpi%7B100%7D%20%5Cbar%7BY%7D) based on a census of N pixels in the region; ![](https://latex.codecogs.com/gif.latex?%5Cinline%20%5Cdpi%7B100%7D%20%5Cbar%7BY%7D) is equivalent to the proportion of pixels correctly classified, i.e, the overall accuracy. An unbiased estimator of ![](https://latex.codecogs.com/gif.latex?%5Cinline%20%5Cdpi%7B100%7D%20%5Cbar%7BY%7D) is

![](https://latex.codecogs.com/gif.latex?%5Chat%7BO%7D%20%3D%20%5Chat%7B%5Cbar%7BY%7D%7D%20%3D%20%5Cfrac%7B%5Csum%20N_h%5E*%20%5Cbar%7By%7D_h%5EO%7D%7BN%7D%20%3D%20%5Cfrac%7BN_1%5E*%20%5Cbar%7By%7D_1%5EO%7D%7BN%7D%20&plus;%20%5Cfrac%7B%20N_2%5E*%20%5Cbar%7By%7D_2%5EO%7D%7BN%7D%20%3D%20%5Cfrac%7B1%7D%7BN%7D%20%28N_1%5E*%20%5Csum_%7Bu%20%5Cin%20h%3D1%7D%20%5Cfrac%7By_u%5EO%7D%7Bn_1%5E*%7D%20&plus;%20N_2%5E*%20%5Csum_%7Bu%20%5Cin%20h%3D2%7D%20%5Cfrac%7By_u%5EO%7D%7Bn_2%5E*%7D%29)

For the user’s accuracy of the new map,  define the following two variables

![](https://latex.codecogs.com/gif.latex?y_u%5EU%20%3D%20%5Cbegin%7Bcases%7D%201%20%26%20%5Ctext%7Bif%20unit%20%5Ctextit%7Bu%7D%20is%20classified%20correctly%20and%20map%20class%20forest%20dist.%7D%5C%5C%200%20%26%20%5Ctext%7Botherwise%3B%7D%20%5Cend%7Bcases%7D%20)

![](https://latex.codecogs.com/gif.latex?x_u%5EU%20%3D%20%5Cbegin%7Bcases%7D%201%20%26%20%5Ctext%7Bif%20unit%20%5Ctextit%7Bu%7D%20is%20map%20class%20forest%20dist.%7D%5C%5C%200%20%26%20%5Ctext%7Botherwise.%7D%20%5Cend%7Bcases%7D)


and for producer's accuracy:

![](https://latex.codecogs.com/gif.latex?y_u%5EP%20%3D%20%5Cbegin%7Bcases%7D%201%20%26%20%5Ctext%7Bif%20unit%20%24u%24%20is%20correctly%20classified%20and%20reference%20class%20forest%20dist.%7D%5C%5C%200%20%26%20%5Ctext%7Botherwise%3B%7D%20%5Cend%7Bcases%7D)

![](https://latex.codecogs.com/gif.latex?x_u%5EP%20%3D%20%5Cbegin%7Bcases%7D%201%20%26%20%5Ctext%7Bif%20unit%20%5Ctextit%7Bu%7D%20is%20reference%20class%20forest%20dist.%7D%5C%5C%200%20%26%20%5Ctext%7Botherwise.%7D%20%5Cend%7Bcases%7D)

We can now estimate user’s and producer's accuracy of the forest disturbance class using a ratio estimator with the stratum-specific means of *x* and *y*:

![](https://latex.codecogs.com/gif.latex?%5Chat%7BR%7D%20%3D%20%5Cfrac%7B%5Chat%7BY%7D%7D%7B%5Chat%7BX%7D%7D%20%3D%20%5Cfrac%7B%5Csum_%7Bh%3D1%7D%5EH%20N_h%5E*%20%5Cbar%7By%7D_h%7D%7B%5Csum_%7Bh%3D1%7D%5EH%20N_h%5E*%20%5Cbar%7Bx%7D_h%7D)

Note that ![](https://latex.codecogs.com/gif.latex?%5Cinline%20%5Cdpi%7B100%7D%20N_h%5E*) is the population size and ![](https://latex.codecogs.com/gif.latex?%5Cinline%20%5Cdpi%7B100%7D%20n_h%5E*) the sample size in the sample results, as opposed to the ![](https://latex.codecogs.com/gif.latex?%5Cinline%20%5Cdpi%7B100%7D%20N_h) population size and ![](https://latex.codecogs.com/gif.latex?%5Cinline%20%5Cdpi%7B100%7D%20n_h) sample size in the new map.  By counting the *x* and *y* in the new map, we calculate the sample counts to populate the following error matrix:

![](https://latex.codecogs.com/gif.latex?%5Cdpi%7B120%7D%20%5Cbegin%7Btabular%7D%7B%20l%20c%20c%20c%20c%7D%20Stratum%20%26%20%24%5Cbar%7By%7D_u%5EU%24%20%26%20%24%5Cbar%7Bx%7D_u%5EU%24%20%26%20%24%5Cbar%7By%7D_u%5EP%24%20%26%20%24%5Cbar%7Bx%7D_u%5EP%24%20%5C%5C%20%5Chline%201.%20Forest%20Dist.%20%26%20%24%5Cfrac%7B%5Csum%20y_u%5EU%7D%7Bn_1%5E*%7D%24%20%26%20%24%5Cfrac%7B%5Csum%20x_u%5EU%7D%7Bn_1%5E*%7D%24%20%26%20%24%5Cfrac%7B%5Csum%20y_u%5EP%7D%7Bn_1%5E*%7D%24%20%26%20%24%5Cfrac%7B%5Csum%20x_u%5EP%7D%7Bn_1%5E*%7D%24%5C%5C%202.%20Non-Dist.%20%26%20%24%5Cfrac%7B%5Csum%20y_u%5EU%7D%7Bn_2%5E*%7D%24%20%26%20%24%5Cfrac%7B%5Csum%20x_u%5EU%7D%7Bn_2%5E*%7D%24%20%26%20%24%5Cfrac%7B%5Csum%20y_u%5EP%7D%7Bn_2%5E*%7D%24%20%26%20%24%5Cfrac%7B%5Csum%20x_u%5EP%7D%7Bn_2%5E*%7D%24%20%5Cend%7Btabular%7D)


which allows to use easily construct the ratio estimator for estimation  of user's and producer's accuracy of the new forest disrurbance class (![](https://latex.codecogs.com/gif.latex?%5Cinline%20%5Cdpi%7B100%7D%20U_1) and ![](https://latex.codecogs.com/gif.latex?%5Cinline%20%5Cdpi%7B100%7D%20P_1)):

![](https://latex.codecogs.com/gif.latex?%5Cdpi%7B120%7D%20%5Chat%7BU%7D_1%20%3D%20%5Chat%7BR%7D%20%3D%20%5Cfrac%7B%5Cfrac%7BN_1%5E*%7D%7Bn_1%5E*%7D%20%5Csum_%7Bu%20%5Cin%20h%3D1%7D%20y_u%5EU%20&plus;%20%5Cfrac%7BN_2%5E*%7D%7Bn_2%5E*%7D%20%5Csum_%7Bu%20%5Cin%20h%3D2%7D%20y_u%5EU%7D%7B%5Cfrac%7BN_1%5E*%7D%7Bn_1%5E*%7D%20%5Csum_%7Bu%20%5Cin%20h%3D1%7D%20x_u%5EU%20&plus;%20%5Cfrac%7BN_2%5E*%7D%7Bn_2%5E*%7D%20%5Csum_%7Bu%20%5Cin%20h%3D2%7D%20x_u%5EU%7D)

![](https://latex.codecogs.com/gif.latex?%5Cdpi%7B120%7D%20%5Chat%7BP%7D_1%20%3D%20%5Chat%7BR%7D%20%3D%20%5Cfrac%7B%5Cfrac%7BN_1%5E*%7D%7Bn_1%5E*%7D%20%5Csum_%7Bu%20%5Cin%20h%3D1%7D%20y_u%5EP%20&plus;%20%5Cfrac%7BN_2%5E*%7D%7Bn_2%5E*%7D%20%5Csum_%7Bu%20%5Cin%20h%3D2%7D%20y_u%5EP%7D%7B%5Cfrac%7BN_1%5E*%7D%7Bn_1%5E*%7D%20%5Csum_%7Bu%20%5Cin%20h%3D1%7D%20x_u%5EP%20&plus;%20%5Cfrac%7BN_2%5E*%7D%7Bn_2%5E*%7D%20%5Csum_%7Bu%20%5Cin%20h%3D2%7D%20x_u%5EP%7D)

## 5. Post-stratification
As explained in the Sampling Design tutorial an important advantage of SRS/SYS is the ability to stratify the study area after sample results have been collected. Applying a stratification subsequent to sampling is referred to as post-stratification (PSTR), which is likely to increase the precision of estimates, and there are seldom reasons not to post-stratify provided that   maps exist over the study area. Another advantage is that the stratified estimator illustrated in Section 3, **Stratified Estimation** above, is directly applicable to the SRS or SYS sample data when crosstabulated with the labels of the poststratification in an error matrix (in this case, the stratified estimator is referred to as post-stratified estimator but the formula is exactly the same). Hence, to apply a PSTR estimator, just follow the steps  outlined in Section 3, **Stratified Estimation** above.

An important difference between STR and PSTR estimation is the formula for the variance estimator. According to Lohr (1999, Eq. 4.22)[^fn5] if *Wh* is known and “*nh* is reasonably large (≥30 or so)” – or “reasonably large, say > 20 in every stratum” (Cochran 1977, p. 134)[^fn1] – the variance estimator is

![](https://latex.codecogs.com/gif.latex?\Large&space;\hat{V}(\hat{\mu}_{PSTR})\approx\sum_{h=1}^H&space;W_h\frac{s_h^2}{n_{h}})

For proportions (Cochran, 1977, Eq. 3.5)[^fn1], the variance of stratum *h* can be expressed as

![](https://latex.codecogs.com/gif.latex?\Large&space;s_h^2=\frac{n_h}{n_{h}-1}p_h(1-p_h))

In a traditional error matrix, *p_h = n_hj ÷ n_h* where *n_hj* is the sample count of reference class *j* in
stratum *h*. Combining Lohr’s variance approximation and Cochran’s expression for stratum variance gives a poststratified variance estimator expressed using the elements of an error matrix:

![](https://latex.codecogs.com/gif.latex?%5Chat%7BV%7D%28%5Chat%7B%5Cmu%7D_%7BPSTR%7D%29%5Capprox%5Csum_%7Bh%3D1%7D%5EH%26space%3BW_h%5Cfrac%7Bs_h%5E2%7D%7Bn_%7Bh%7D%7D%3D%5Cfrac%7B1%7D%7Bn%7D%5Csum_%7Bh%3D1%7D%5EHW_h%5Cfrac%7Bn_h%7D%7Bn_h-1%7Dp_h%281-p_h%29%3D%5Cfrac%7B1%7D%7Bn%7D%5Csum_%7Bh%3D1%7D%5EHW_h%5Cfrac%7Bn_%7Bhj%7D%281-%5Cfrac%7Bn_%7Bhj%7D%7D%7Bn_{h+}%7D%29%7D%7Bn_{h+}-1%7D)

If you compare this to STR variance estimator Section 3, **Stratified Estimation** above, you will see that the PSTR variance estimator is very similar but not identical.  


## 6. Software to automate the analysis of sample results 

### 6.1 AREA2
The AREA2 application in Google Earth Engine has equations for all estimators described in this is tutorial. Note that in AREA2, the SRS estimator is referred to by its formal name, expansion estimator.  AREA2 is available here: https://code.earthengine.google.com/?accept_repo=projects/AREA2/public and more detailed documentation here: https://area2.readthedocs.io/

### 6.2 SEPAL
Stratified estimation estimation is automated in SEPAL; the documentation is available here: https://github.com/sig-gis/SEPAL-CEO  Scroll down to *Exercise 4.3: Area and uncertainty estimation* for a description of  stratified estimation. 

## License
This work is licensed under a [Creative Commons Attribution 3.0 IGO](https://creativecommons.org/licenses/by/3.0/igo/) 

Copyright 2020, World Bank. This work was developed by Pontus Olofsson under World Bank contract with GRH Consulting, LLC for the development of new -and collection of existing- Measurement, Reporting, and Verification related resources to support countries' MRV implementation. 

Attribution: Olofsson, P. (2021). *Open MRV: Analysis of sample data*. World Bank. License: Creative Commons Attribution license (CC BY 3.0 IGO)



## References
[^fn1]: Cochran, W. G. (1977). *Sampling Techniques*. New York, NY: Wiley

[^fn2]: Casella, G., & Berger, R. L. (2002). *Statistical Inference* (2nd ed.). Pacific Grove, CA: Duxbury Press

[^fn3]: Rice, J. A. (1995). *Mathematical Statistics and Data Analysis* (2nd ed.). Belmont, CA: Duxbury Press

[^fn4]: Stehman, S. V. (2014). Estimating area and map accuracy for stratified random sampling when the strata are different from the map classes. *International Journal of Remote Sensing*, 35(13), 4923-4939

[^fn5]: Lohr, S. L. (1999). *Sampling: Design and Analysis*. CRC Press




