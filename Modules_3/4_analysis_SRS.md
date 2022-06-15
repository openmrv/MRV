# Analysis of sample data  collected under simple random and systematic sampling

## 1. Background

After designing and drawing a sample from a study area (sampling design and selection), we need to observe and record the reference land cover conditions at the locations of sample units (response design). The collection of reference observations is referred to as the sample results or data, or the reference classification. In this tutorial we will apply various estimators to the sample data to estimate characteristics of the population we sampled -- i.e. characteristics of the study area such as the area of forest disturbance. An estimator is “The rule by which an estimate of some population characteristic [i.e. parameter] *μ* is calculated from the sample results” (Cochran, 1977, p. 11). Note that that an estimator is not the same thing as an estimate – instead “An estimator is a function of the sample, while an estimate is the realized value of an estimator (that is, a number) that is obtained when a sample is actually taken” (Casella & Berger, 2002, p. 312). An estimator has two important properties: variance and bias. The bias of an estimator *μ^* of a population parameter *μ* is the difference between *μ* and the expected value of *μ^* over all possible samples; that is, ![](https://latex.codecogs.com/gif.latex?\inline&space;\textup{Bias}(\hat{\mu})&space;=&space;\textup{E}(\hat{\mu})&space;-&space;\mu) (Casella & Berger, 2002, p. 330). If  ![](https://latex.codecogs.com/gif.latex?\inline&space;\textup{Bias}(\hat{\mu})&space;=&space;\textup{E}(\hat{\mu})&space;-&space;\mu=0), then the estimator is said to be unbiased. Note that because an estimate is a number, it has no variance and no bias and therefore cannot be unbiased.

The other important property of an estimator is variance. The formal definition of the variance provides “a measure of the degree of spread of a distribution around its mean” (Casella & Berger, 2002, p. 59). This definition is not very helpful in our context, instead, we are concerned with situations in which we have sampled a study area to estimate a certain population parameter (e.g. the area of forest or deforestation). For example, if we have a population of from which a sample of has been selected, the sample variance is *s^2^* and is easily calculated for common sampling designs. But the sample variance is less interesting compared to the variance of an estimator. For common designs, we can easily prove that the sample variance *s^2^*  is an unbiased estimator of the population variance *S^2^* (Cochran, 1977, p. 22, 26). The variance of an estimator *u^*  is ![](https://latex.codecogs.com/gif.latex?\inline&space;\textup{V}(\hat{\mu})&space;=&space;S^2&space;\div&space;n) (assuming a small sample size, *n*, relative the populations size, *N*); the estimated variance of *u^* substitutes the sample variance *s^2^* for the population variance *S^2^* to create the variance estimator of  *u^*   as ![](https://latex.codecogs.com/gif.latex?\inline&space;\hat{V}(\hat{\mu})&space;=&space;s^2&space;\div&space;n) which is the variance estimator of primary interest to us as it allows us to quantify the uncertainty in things like the activity data or other parameters of interst.  

From here we can introduce two more important measures of spread: standard error and confidence interval. The standard error is the standard deviation (i.e. square root of the variance) of an estimator (Rice, 1995, p. 192) and hence has the same unit as the estimate. The standard deviation of an estimator is referred to as its standard error. Because the sample variance is an unbiased estimator of the population variance, we can estimate the standard error using the sample variance: ![](https://latex.codecogs.com/gif.latex?\inline&space;\textup{SE}(\hat{\mu})&space;=&space;\hat{V}(\hat{\mu})&space;\div&space;\sqrt{n}). Note that because a standard error is a standard deviation of an estimator, all standard errors are also standard deviations but not all standard deviations are standard errors. This sometimes causes confusion even though the definitions of standard error and standard deviation are consistent. Neither the variance nor the standard error is typically used to express the uncertainty in estimates, instead, a confidence interval is commonly used: "A 95% confidence interval for *μ* is a random interval that contains *μ* with probability .95; if we were to take many random samples [under the same sampling design] and form a confidence interval from each one, about 95% of these intervals would contain *μ*" (Rice, 1995, p. 217). Confidence intervals are often in the form ![](https://latex.codecogs.com/gif.latex?\inline&space;\hat{\mu}&space;\pm&space;a\times\textup{SE}(\hat{\mu})) where *a* is a statistic related to the desired confidence level, referred to as z-score or standard score expressed as a percentage between 0 and 100%. For a certain confidence level *p* the area under the standard normal density function from *-z* to *+z* is *p* (Rice, 1995, p. 202); for example, a confidence interval at the 95% confidence level  correspond to a z-score of 1.96 (often rounded to 2). A condition for using a z-score to compute a confidence interval is that the sampling distribution is approximately a normal distribution, which we can assume for large sample sizes. The confidence interval divided by the estimate is referred to as a margin of error (*MoE*) and is often expressed as a percentage.

The two properties, bias and variance, are important because we can ensure that the estimator we use is unbiased, and we can express the uncertainty in estimates. Neither is possible when using pixel-counting in maps or when sampling without adhering to probability sampling.  Another important aspect of an estimator is that it is a function of the sample, which means that the estimator has to correspond to the sampling design. For example, the sample mean is an unbiased estimator of the population mean for simple random sampling; for stratified random sampling, we need to use a stratified estimator which is expressed as the sum of the means of the simple random samples within strata weighted by stratum weights.

## 2. Construction of SRS estimators 
Sample results collected under simple random sampling are the most straightforward to analyze (the same estimators are used for both simple random and systematic sampling). Because no maps/stratifications are used and because the sample mean is unbiased estimator of the population mean, the analysis of SRS/SYS sample results can easily be completed in a spreadsheet.  Stratified random sampling was  illustrated in previous tutorials, and only dummy data are provided here to illustrate the construction of SRS/SYS estimators. Let's assume that the data in this spreadsheet are map and reference labels at locations selected under SRS: https://docs.google.com/spreadsheets/d/1pcK-rlhUo5lvmYqibT4zIv-bR5tF4Uu8DqPwIG8mJWQ/edit?usp=sharing The sample size is *n* = 100 and a label of 1 is forest disturbance, 2 is forest, and 3 is non-forest.         

Because the sample mean is unbiased estimator of the population mean the calculation of area proportions are straightforward; define *y_i* = 1 if forest disturbance was observed at sample location *i* and 0 otherwise; the are of forest disturbance is given by (Cochran, 1977, p. 22):

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

To apply the variance estimator in the spreadsheet, type in cell D3 "Variance", and in cell D4  "=sum(ArrayFormula((C2:C101-D4)^2))/(100 * 99)" to apply the variance estimator; it should return 0.00122. Now type "Standard error" in D5, and in D6: "=sqrt(C4)"; type "95% CI" in D7 and in D8: "=1.96*D6". Finally type "Margin of error" in D9 and in D10 and "=D8/D2":

| | A             | B            | C     |D        |E   
|-|:--------------|:-------------|:------|:--------|:---|
|1| Map           | Ref.         | y_i   | Area FD |    |
|2| 2             |  2           | 0     | 0.14    |    |
|3| 2             |    2         | 0     |Variance	       |    |
|4| 1             |    1         | 1     |  0.00122        |    |
|5| 2             |    2         | 0     | Standard error  |    |
|6| 2             |    2         | 0     |  0.03493        |    |
|7| 2             |    2         | 0     | 95% CI          |    |
|8| 1             |    1         | 1     | 0.06846         |    |
|9| 2             |    1         | 1     | Margin of error |    |
|10| 2            |    2         | 0     | 48.9%           |    |

We have now estimated the area of forest disturbance using a sample of 100 units collected under SRS as 0.14 +- 0.068 corresponding to a margin of error of 48.9%. Note that the map information in column A was not used.  

Finally, lets calculate the accuracy of the map, starting with the overall accuracy: type "Overall acc." in cell E1, and in E2 "=COUNTIF(A2:A101,B2:B101)/100" -- this expression will count number of instances where the map and reference labels agree and divide by the sample size. The overall accuracy is the overall proportion of area correctly classified.

In cell F1 type "User's acc. FD" and in F2 "=countifs(A1:A101,"1",B1:B101,"1")/countif(A1:A101,1)"; the user’s accuracy of map class “is the conditional probability that an area classified as category i by the map is classified as category i by the reference data” (Stehman, 1997, p. 79):

Finally, in cell G1 type "Prod. acc. FD" and in G2 "=countifs(A1:A101,"1",B1:B101,"1")/countif(B1:B101,1)"; the producer’s accuracy of map class is “the conditional probability that an area classified as category j by the reference data is classified as category j by the map” (Stehman, 1997, p. 79).


| | A             | B            | C     |D        |E           |F             |G
|-|:--------------|:-------------|:------|:--------|:-----------|:-------------|:------------|
|1| Map           | Ref.         | y_i   | Area FD |Overall acc.|User's acc. FD|Prod. acc. FD|
|2| 2             |    2         | 0     | 0.14    | 0.65  |0.80|0.86|
|3| 2             |    2         | 0     |Variance         |    | |
|4| 1             |    1         | 1     |  0.00122        |    | |
|5| 2             |    2         | 0     | Standard error  |    | |
|6| 2             |    2         | 0     |  0.03493        |    | |
|7| 2             |    2         | 0     | 95% CI          |    | |
|8| 1             |    1         | 1     | 0.06846         |    | |
|9| 2             |    1         | 1     | Margin of error |    | |
|10| 2            |    2         | 0     | 48.9%           |    | |




## 3. Software to automate the analysis of sample results 

The AREA2 application in Google Earth Engine has equations for all estimators described in this is tutorial. Note that in AREA2, the SRS estimator is referred to by its formal name, expansion estimator.  AREA2 is available here: https://code.earthengine.google.com/?accept_repo=projects/AREA2/public and more detailed documentation here: https://area2.readthedocs.io/

## 4. FAQ

*Question: Are the estimators above the only option I have when working with sample results collected under SRS/SYS?*
Answer: No! You can stratify the study area after selection of the sample which will allow you to use a stratified estimator, which in this case is then referred to as a post-stratified estimator. You can also use a regression estimator which often works well when the map and reference observations are expressed as proportions.

*Question: Will SRS/SYS result in less precise estimates compared to stratified random sampling?*
Answer: It is hard to say that one sampling design and family of estimators are more or less precise in general, as the final precision will depend on several factors. To achieve the same precision as in stratified design, you would typically need a larger sample under SRS/SYS. This is especially true if the parameters of interest are small proportions of the study area.


## License
This work is licensed under a [Creative Commons Attribution 3.0 IGO](https://creativecommons.org/licenses/by/3.0/igo/) 

Copyright 2020, World Bank. This work was developed by Pontus Olofsson under World Bank contract with GRH Consulting, LLC for the development of new -and collection of existing- Measurement, Reporting, and Verification related resources to support countries' MRV implementation. 

License: Creative Commons Attribution license (CC BY 3.0 IGO)

Attribution: Olofsson, P. (2021). *Open MRV: Analysis of sample data under simple random and systematic sampling*. World Bank. 

Work reviewed by:
Ana Mirian Villalobos
Tatiana Nana
Carole Andrianirina
Jennifer Juliana Escamilla Valdez

## References


Casella, G., & Berger, R. L. (2002). *Statistical Inference* (2nd ed.). Pacific Grove, CA: Duxbury Press

Cochran, W. G. (1977). *Sampling Techniques*. New York, NY: Wiley


Lohr, S. L. (1999). *Sampling: Design and Analysis*. CRC Press


Rice, J. A. (1995). *Mathematical Statistics and Data Analysis* (2nd ed.). Belmont, CA: Duxbury Press

[^fn4]: Stehman, S. V. (2014). Estimating area and map accuracy for stratified random sampling when the strata are different from the map classes. *International Journal of Remote Sensing*, 35(13), 4923-4939





