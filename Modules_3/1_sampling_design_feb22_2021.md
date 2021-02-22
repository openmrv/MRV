# Sampling design for estimation of area and map accuracy 

## 1. Background

A sampling-based approach to estimation can be separated into three different components: sampling design, response design and analysis (Stehman & Czaplewski, 1998)[^fn1]. The first component, sampling design, is illustrated in this tutorial.  The sampling design defines the protocol for selecting the subset of units -- i.e. the sample -- from a larger population. In our case, the population is the equivalent of the study area, and characteristics of the study area, such as the area of a certain land cover, are estimated by analyzing the sample.  Sampling-based approaches in a remote sensing or geographical context are necessary because they allow us to estimate area bias, map accuracy and uncertainty. As explained in the GFOI Methods & Guidance Document, estimating areas of land cover and land cover change by simply counting pixels in maps will produce erroneous results because of classification errors (GFOI, 2016, p. 125)[^fn2]:

> Methods that produce estimates of activity data as sums of areas of map units assigned to map classes are characterized as pixel counting and generally make no provision for accommodating the effects of map classification errors. Further, although confusion or error matrices and map accuracy indices can inform issues of systematic errors and precision, they do not directly produce the information necessary to construct confidence intervals. Therefore, pixel-counting methods provide no assurance that estimates are “neither over- nor under-estimates” or that “uncertainties are reduced as far as practicable”. The role of reference data, also characterized as accuracy assessment data, is to provide such assurance by adjusting for estimated systematic classification errors and estimating uncertainty, thereby providing the information necessary for construction of confidence intervals for compliance with IPCC good practice guidance.

When choosing a sampling design, we need to consider a few but important design criteria. Of primary importance is the adherence to probability sampling.  Probability sampling is defined in terms of inclusion probabilities, where an inclusion probability relates the likelihood of a given unit being included in the sample; the inclusion probability must be known for each unit selected in the sample and the inclusion probability must be greater than zero for all units in the study area (Stehman, 2009)[^fn3]. Several probability sampling designs are applicable to accuracy and area estimation, with the most commonly used designs being simple random, stratified random, and systematic. Two-phase (also called double), two-stage and cluster sampling are applicable but more complicated. 

## 2. How to choose a sampling design?
Choosing a sampling design often involves tradeoffs among different criteria and priorities.  The desire to  provide estimates for subregions or the need to meet precision targets will need to be balanced against desirable sampling design criteria such as the ease and practicality of implementation, cost effectiveness, the ease of accommodating changes in sample size.  Stehman (2009)[^fn3] provides a detailed review of sampling design options, objectives, and criteria, but the decision typically boils down to three key decisions: whether to use strata, whether to use clusters, and whether to implement a systematic or simple random selection protocol. 

### 2.1 Use strata?

Strata are “subpopulations that are non-overlapping, and together comprise the whole population” (Cochran, 1977, p. 89)[^fn4]. Stratifying the study area prior to the sample selection can ensure that estimates of accuracy and area are obtained for certain subregions in the study area, and it results in higher precision of estimates. Accordingly, there are several good reasons for using strata. Even with simple random sampling, the use of strata after selecting the sample is a [good idea](###markdown-header-3.1-Post-stratification). Stratified sampling provides an  obvious advantage  if we are interested in a very small proportion of the study area, as is often the case in tropical MRVs. For example, the area of forest loss, even in countries with rampant deforestation, is often a very small proportion of the country, especially over short time intervals. The use of a map of forest loss (and other categories) to stratify the study area in such situations allows for targeted sampling in areas of particular interest. Not stratifying in such situations will require a very large sample size.       

### 2.2 Use simple random or systematic selection?
Systematic selection involves  selecting a starting point at random with equal probability and then sampling with a fixed distance between sample locations. In short, simple random selection is preferable if collecting reference observations in satellite data whereas systematic selection is preferable if visiting sample locations in situ (Olofsson et al. 2014)[^fn5]. The rationale for this recommendation is that systematically selected units are easier to locate in the field while random selection is easier to augment. Note that the same estimators are used with both simple random or systematic selection. 

### 2.3 Use cluster?
A cluster is a sampling unit that consists of one or more of the basic assessment units specified by the response design. For example, a cluster could be a 3 × 3 block of 9 pixels or a 1 km × 1 km cluster containing 100 1 ha assessment units. In cluster sampling, a sample of clusters is selected and the spatial units within each cluster are therefore selected as a group rather than selected as individual entities. Two-stage sampling is a form of cluster sampling where large primary sampling units are (PSUs) are selected at the first stage;  smaller secondary sampling units (SSUs) are selected within each PSU in the second stage.  Such designs have the benefit of requiring reference data (i.e. the data used for collecting reference observations) only over PSUs instead of the entire study area which is the case with the aforementioned designs. However, unless the cost savings are considerable, cluster-based designs are not recommended as the correlation between SSUs  often reduces precision relative to a simple random sample of equal size, and because they are complicated designs that are difficult to augment with sample results that are difficult to analyze.   


## 3. Simple random/systematic sampling
If the units (e.g. pixels) of a population/study area are numbered from 1 to *N*, simple random sampling (SRS) is “A method for selecting *n* units out of the *N* such that every one of [the sets of *n* specified units] has an equal chance of being drawn” (Cochran 1977, p. 18)[^fn4]. In a geography context, we are often interested in estimating a proportion of the population/study area, such as the area proportion of a certain land cover or change in land cover, from the sample data. Using Cochran's notions, the units of a population are ![](https://latex.codecogs.com/gif.latex?\inline&space;y_1&space;\ldots&space;y_N) from which a sample  ![](https://latex.codecogs.com/gif.latex?\inline&space;y_1&space;\ldots&space;y_n) is selected under SRS; we record ![](https://latex.codecogs.com/gif.latex?\inline&space;y_i=1) if the land cover of interest is observed at unit *i* and ![](https://latex.codecogs.com/gif.latex?\inline&space;y_i=0) otherwise. An advantage of SRS is that the mean of the observations is an unbiased estimator of the population proportion (*p*) of interest (Cochran, 1977, Eq 3.3)[^fn4]:

![](https://latex.codecogs.com/svg.latex?\Large&space;\bar{y}=\frac{1}{n}\sum_{i=1}^{n}y_i=\hat{p})

and the variance of the estimated proportion *p^* is  easily estimated as (Cochran, 1977, Eq 3.11)[^fn4]

![](https://latex.codecogs.com/svg.latex?\Large&space;\hat{V}(\hat{p})=\frac{\hat{p}(1-\hat{p})}{n-1})

These estimators are applicable also to sample data collected under simple systematic sampling (SYS). The straightforward analysis of sample data collected under SRS/SYS, and the ability to augment the sample size with ease (especially under SRS), make these designs attractive.  
 
### 3.1 Post stratification 
Another important advantage of SRS/SYS is the ability to stratify the study area after sample results have been collected -- applying a stratification subsequent to sampling is referred to as post-stratification (PSTR). PSTR is likely to increase the precision of estimates, and there are seldom reasons not to post-stratify using maps. 

### 3.2 Sample size
Determining the sample size regardless of design involves calculating the number of units in a sample required to meet a certain target precision of an estimate of a population parameter of interest. The calculation is based on solving the variance estimator corresponding to the design for *n*. If the variance in variance estimator above is the desired variance of an estimate, solving for *n* gives  (Cochran, 1977, Eq. 4.2)[^fn4] 

![](https://latex.codecogs.com/svg.latex?\Large&space;n=\frac{\hat{p}(1-\hat{p})}{\hat{V}(\hat{p})})

where *p^* is an estimate of the proportion of units in the class of interest in the study area. For example, let's assume we want to  estimate the overall accuracy (as in Olofsson et al., 2014, p. 53)[^fn5] with a 5% margin of error. We would then define *p* as overall map accuracy. We obviously don't know the overall accuracy of the map at this stage so an educated guess is required. If we assume 80% overall accuracy, a 5% margin of error (*MoE*) would translate into a variance of (the z-score of 1.96 at the 95% confidence level is rounded to 2)

![](https://latex.codecogs.com/svg.latex?\Large&space;MoE=\frac{2\sqrt{\hat{V}}(\hat{p})}{\hat{p}}\Leftrightarrow\hat{V}(\hat{p})=(\frac{MoE\times&space;\hat{p}}{2})^2=(\frac{0.05\times0.8}{2})^2=0.0004)

which gives a sample size of

![](https://latex.codecogs.com/svg.latex?\Large&space;n=\frac{\hat{p}(1-\hat{p})}{\hat{V}(\hat{p})}=\frac{0.8(1-0.8)}{0.0004}=400)

Even though estimation of overall accuracy was illustrated in Olofsson et al. (2014)[^fn5], specifying a margin of error of the overall map accuracy is not intuitive and rarely an estimation objective. A more realistic example would be the  estimation of the area of deforestation or forest degradation with a certain precision. In the CODED tutorial, a map of  deforestation, forest degradation, forest and non-forest was created for Colombia; for the sake of simplicity, let's lump the deforestation and forest degradation into a single forest disturbance class, which was mapped as 1.4% of the country from 2010 to 2020. Note, for estimation of activity data within REDD+ (and other initiatives), it is recommended to estimate deforestation and degradation separately -- and hence use a deforestation stratum and a degradation stratum -- rather than combining the two classes into a single forest disturbance class. Here, we are using a combined disturbance class to faciliate the illustration of the workflow and calculations.  Let's assume we want to estimate the area of forest disturbance (again, combined deforestation and degradation) with a 25% margin of error. Note that 25% is used here simply to illustrate the workflow -- the target error will depend on the circumstances of the study. First, a 25% margin of error is equivalent to a variance of  

![](https://latex.codecogs.com/svg.latex?\Large&space;\hat{V}(\hat{p})=(\frac{MoE\times&space;\hat{p}}{2})^2=(\frac{0.25\times0.014}{2})^2=0.000003)

which gives a sample size of

![](https://latex.codecogs.com/svg.latex?\Large&space;n=\frac{\hat{p}(1-\hat{p})}{\hat{V}(p)}=\frac{0.014(1-0.014)}{0.000003}=4,600)

Collecting observations at almost five thousand sample locations is rarely attainable for an individual study. The example illustrates one of the drawbacks with SRS/SYS -- because we are not using any information on the location of deforestation, a very large sample size is required to achieve high precision. Another, quicker, way to estimate the sample in this case is to assume that we need at least 30 units in areas of deforestation which would require a sample size of 30/0.014 = 2,142 units which is more manageable but still large, and we are not sampling to meet a precision target. (Scroll down to **4.3 Allocation** for an explanation of why 30 is the "magic number".)

## 4. Stratified random sampling
The example above illustrates the drawback of SRS/SYS -- when we are trying to estimate something that is a small proportion of the population, a very large sample size is required under SRS/SYS. In such situations, stratified random sampling (STR) is recommended. STR is simply when “simple random sampling is taken in each stratum” (Cochran 1977, p. 89)[^fn4]. Accordingly, we split the population into strata and select a sample in each strata under SRS (or SYS). STR adds another level of complexity and requires us to determine how to allocate the sample unit to strata in addition to determining the total sample size. 

### 4.1 Sample size
Just as with SRS/SYS, we need to specify a precision objective and calculate using the STR variance estimator the total sample size (*n*) required to meet the target precision. Solving the STR variance estimator gives (Olofsson et al., 2014, Eq. 13. modified from Cochran, 1977, Eq 5.25)[^fn4]

![](https://latex.codecogs.com/svg.latex?\Large&space;n=\left&space;[\frac{\sum_{h}W_h\textup{SD}_h}{\text{SE}(p)}\right&space;]^2)

*Wh* is the weight of stratum *h*, which is simply the area of the stratum expressed as a proportion of the total study area; SD*h* is the standard deviation of stratum *h*, which is explained below. The target standard error is SE(*p*). Now, let's go back to the forest disturbance example from Colombia but now let's use the map that we generated in the CODED tutorial of disturbance, stable forest and stable non-forest. The sample size calculation under STR is a bit more complicated so we'll use a spreadsheet from Google Sheets (or Microsoft Excel if you prefer). The spreadsheet used in this tutorial can be accessed here: https://docs.google.com/spreadsheets/d/1lmPt35SvR3X7txpn0cwd-xkgwC_4nRPL520OZZcRKX0/edit?usp=sharing  

#### Step 1 
First we need to compute the  number of pixels of each stratum; this can be done using GDAL, QGIS, Google Earth Engine, etc.; in the CODED tutorial, these areas are printed in the *Console* in Google Earth Engine. If not, or if you have an existing GEE asset, load the asset using the AREA2 Stratified Random Sampling script  (https://code.earthengine.google.com/6a0f89221d40ee039362974d303ff5aa) to compute the strata weights. Add these numbers on the first row "Area [px]". On the second row, express these areas as a proportion (in cell B3 type "=B2/sum($B2:$D2") and extend to E2). These proportions are referred to as the strata weights (*Wh*) 


| | A             | B            | C              |D              |E             |
|-|:--------------|:-------------|:---------------|:--------------|:-------------|
|1| Stratum (*h*) | Forest (1)   | Non-Forest (2) |For. Dist. (3) |Total     |
|2| Area [m2]     |658,196,561,513|	462,219,395,097|15,594,353,281|	1,136,010,309,891|
|3| *Wh*          |0.579       |0.407         |0.0137	         |1         |

#### Step 2
Note that we  have calculated *Wh*, we need to calculate the remaining two variables in the equation: the standard deviation of stratum *h* (SD*h*) and the target standard error (SE(*p*)). SD*h* is somewhat tricky to understand and requires a best guess of the proportion of stratum *h* that is the target class (*qh*). 

![](https://latex.codecogs.com/svg.latex?\Large&space;\textup{SD}_h=\sqrt{q_h(1-q_h)})

In our example, the proportion of disturbance in the study area is the target, which means that *qh* is the proportion of stratum *h* that is disturbance -- if the map were perfect (which it isn't!) then *q1* (forest) = *q2* (non-forest) = 0; *q3* (disturbance) = 1 but we cannot assume that that is the case. No map is perfect and a more realistic assumption is that, let's say, 80% of the disturbance in the study area is captured by the disturbance map class, and that small fractions of the  forest and non-forest strata are disturbance because of classification error. If *q1* = 0.001, then we assume that 0.001 × 658,196,561,513/30^2^ = 0.7M pixels of disturbance in the forest stratum. Because the non-forest stratum is slightly smaller, if we believe a similar amount of disturbance is present also in the non-forest stratum, we should assume *q2* = 0.002. Accordingly, let's add these numbers (0.001, 	0.002   and	0.8	 ) on row 4 and calculate SD*h* on row 5, cell  B5 as "=sqrt(B4*(1-B4))" and extend to cell D5. For simplicity calculate the product of SD*h* and *Wh* on row 6 such that cell B6 = B3*B5 and extend to D5:

| | A             | B            | C              |D              |E             |
|-|:--------------|:-------------|:---------------|:--------------|:-------------|
|1| Stratum (*h*) | Forest (1)   | Non-Forest (2) |For. Dist. (3) |Total         |
|2| Area [m2]     |658,196,561,513|	462,219,395,097|15,594,353,281|	1,136,010,309,891|
|3| *Wh*          |0.579          |0.407          |0.0137	         |1         |
|4|*qh*           |	0.001         |	0.002	      |	0.8              | 		    |
|5|SD*h*          |	0.0316        |	0.0447	      |0.4	             |          |
|6|SD*h* x *Wh*   |	0.0183        |	0.01818       |	0.005491         |	        |	

#### Step 3
Now, let's set the target of the sampling: the desired margin of error of the area of disturbance. In the formula for estimating the sample size, the target is expressed as a standard error. If again targeting a 25% margin of error, then

![](https://latex.codecogs.com/svg.latex?\Large&space;MoE=\frac{1.96\times\textup{SE}(\hat{p})}{\hat{p}}\Leftrightarrow\textup{SE}(\hat{p})=\frac{MoE\times&space;\hat{p}}{1.96}=\frac{0.1\times0.01}{1.96}=0.0005)

We are here using a z-score of 1.96 which corresponds to the 95% confidence level. If we specify the MoE in cell D7, then we can calculate the target standard error in cell D8: "=(D7/100)*D3/2":

| | A             | B            | C              |D              |E             |
|-|:--------------|:-------------|:---------------|:--------------|:-------------|
|1| Stratum (*h*) | Forest (1)   | Non-Forest (2) |For. Dist. (3) |Total     |
|2| Area [m2]     |658,196,561,513|	462,219,395,097|15,594,353,281|	1,136,010,309,891|
|3| *Wh*          |0.579       |0.407         |0.0137	         |1         |
|4|*qh*           |	0.001         |	0.002	      |	0.8              | 		    |
|5|SD*h*          |	0.0316        |	0.0447	      |0.4	             |          |
|6|SD*h* x *Wh*   |	0.0183      |	0.01818   |	0.005491 |	|	
|7| MoE [%]       |   || 25        |            |  
|8| SE(*p^*)      |   || 0.0017   |            |  
 
#### Step 4
Finally, we can now easily calculate the sample size on row 8, cell E9 as: "=(sum(B6:D6)/B7)^2"

| | A             | B            | C              |D              |E             |
|-|:--------------|:-------------|:---------------|:--------------|:-------------|
|1| Stratum (*h*) | Forest (1)   | Non-Forest (2) |For. Dist. (3) |Total     |
|2| Area [m2]     |658,196,561,513|	462,219,395,097|15,594,353,281|	1,136,010,309,891|
|3| *Wh*          |0.579       |0.407         |0.0137	         |1         |
|4|*qh*           |	0.001         |	0.002	      |	0.8              | 		    |
|5|SD*h*          |	0.0316        |	0.0447	      |0.4	             |          |
|6|SD*h* x *Wh*   |	0.0183      |	0.01818   |	0.005491 |	|	
|7| MoE [%]       |   || 25        |            |  
|8| SE(*p^*)      |   || 0.00172   |            |  
|9| *n*           |              |            |               | 599    |

which gives a sample size of 599 -- i.e. about 1/8 of the sample size of 4,600 required under SRS to reach the same precision. To change the target precision, we now simply need  to either adjust our target precision in cell D7.

### 4.2 Buffer strata
A potential issue in the situation above is that the omissions of disturbance present in the forest stratum will have a big impact on the precision of estimates.  Such omission errors are sample units in the forest stratum that were observed in the reference data as being disturbance. The issue is explained in detail in Olofsson et al. (2020)[^fn6]  and here we just recognize that the "uncertainty contribution" of omission errors to a large extent depends on the size of the stratum in which they occur. We would therefore like to decrease the size of the forest stratum which is currently 83% of the study area. In particular, we want to create small substrata where disturbance omissions are likely to occur. One approach explored in the literature is the creation of buffer strata around change strata -- the rationale is that errors are likely to occur close to correctly mapped change. In our case, such a buffer stratum might be defined as the pixels in the forest stratum adjacent to the disturbance. 

The creation of a buffer is not illustrated in the previous tutorials so let's do that now. Click this link: A script to create a buffer in the CODED output is available in AREA2: 
https://code.earthengine.google.com/861290ef20f0d76e7639d430471c7eae 
Alternatively,  you can use this existing CODED-based map of Colombia with a buffer:
https://code.earthengine.google.com/?asset=users/olofsson76/Open_MRV/Open_MRV_Col_strat_buffer
To get the strata weights, open the script in AREA2 to select a sample under stratified random sampling:
https://code.earthengine.google.com/?accept_repo=users%2Fopenmrv%2FMRV&scriptPath=projects%2FAREA2%2Fpublic%3A1.%20Sampling%20Design%2FStratified%20Random%20Sampling and specify the path to the CODED-based map of Colombia with a buffer under "Specify stratification/image to define study area"; use the other default arguments click "Load image" which will display the strata areas in the Console (NOTE: it will take a some time). I get the following areas of Forest (0), Non-forest (1), Forest disturbance (2) and a 2-pixel buffer (3) [m^2^]:

0: 625,597,113,080
1: 462,219,395,097
2: 15,594,353,281
3: 32,599,448,433

Lets add these numbers in a second tab in to the spreadsheet and calculate the strata weights:

| | A             | B            | C              |D              |E             |F         |
|-|:--------------|:-------------|:---------------|:--------------|:-------------|:---------|
|1| Stratum (*h*) | Forest (1)   | Non-Forest (2) |For. Dist. (3) |FD buf. (4)   |Total     |
|2| Area [m2]     |625,597,113,080|462,219,395,097|15,594,353,281 |32,599,448,433|1,136,010,309,891|
|3| *Wh*          |0.551       |0.407         |0.0137	      |0.0287	         |1         |



If we believe that the buffer stratum is efficient in capturing omission errors, we can decrease *qh* for the forest stratum -- if we assume that half of the pixels of disturbance in the forest stratum will be "captured"  by the buffer stratum, then *q1* = 0.0005 and *q4* = 0.0075. With a target margin of error 25%, the sample size drops to 502.
	
| | A             | B            | C              |D              |E             |F         |
|-|:--------------|:-------------|:---------------|:--------------|:-------------|:---------|
|1| Stratum (*h*) | Forest (1)   | Non-Forest (2) |For. Dist. (3) |FD buf. (4)   |Total     |
|2| Area [m2]     |625,597,113,080|462,219,395,097|15,594,353,281 |32,599,448,433|1,136,010,309,891|
|3| *Wh*          |0.551       |0.407         |0.0137	      |0.0287	         |1         |
|4|*qh*           |	0.0005    	|	0.002     |	0.8         |	0.0075	 |  |		
|5|SD*h*          |	0.0223      |	0.04468   |	0.4         |	0.086277 |	|		
|6|SD*h* x *Wh*   |	0.0123      |	0.01818   |	0.005491	|	0.002475 |	|	
|7|*MoE* [%]      |		       	|	          |	25		    |	         |	|
|8|SE(*p^*)	      |		        |	          |0.001716	    |	         |	|		
|9|*n*		      |			    |	          |             |	         |502|		

A buffer of three pixels were used here just as an example. For more information about how to determine the size of buffer strata, please see Olofsson et al. (2020)[^fn6]. 

### 4.3 Allocation
Lets assume that we settled for the margin of error of 15% with a buffer stratum and a sample size of 958.  We now need to decide how to allocate the sample to strata. In short, an allocation proportional to the strata weights are efficient for estimating parameters that include across-strata calculations -- such parameters include area, overall and producer's accuracy. Estimation of user's accuracy is based on within-strata calculations that benefit from an equal allocation. Achieving a high precision of the user's accuracy is rarely an estimation objective which suggests that a proportional allocation is preferable. Going back to the spreadsheet, lets calculate on row 10 the sample size in each stratum following a proportional allocation: in cell B10:  "=B3*$F$9" and extend to E10.

| | A             | B            | C              |D              |E             |F         |
|-|:--------------|:-------------|:---------------|:--------------|:-------------|:---------|
|1| Stratum (*h*) | Forest (1)   | Non-Forest (2) |For. Dist. (3) |FD buf. (4)   |Total     |
|2| Area [m2]     |625,597,113,080|462,219,395,097|15,594,353,281 |32,599,448,433|1,136,010,309,891|
|3| *Wh*          |0.551       |0.407         |0.0137	    |0.0287	         |1             |
|4|*qh*           |	0.0005    	|	0.002     |	0.8         |	0.0075	     |              |		
|5|SD*h*          |	0.0223      |	0.04468   |	0.4         |	0.086277     |              |		
|6|SD*h* x *Wh*   |	0.0123      |	0.01818   |	0.005491	|	0.002475     |              |	
|7|*MoE* [%]      |		       	|	          |	25		    |	             |              |
|8|SE(*p^*)	      |		        |	          |0.001716	    |	             |              |		
|9|*n*		      |			    |	          |             |	             |502           |
|10| *nh* (prop.) |277	|204	|7	|14|	502


This seems reasonable but we need at least 30 units per stratum, therefore on row 11 lets bump up the sample size in the disturbance stratum to 30 and round the sample sizes in forest stratum to 275 and non-forest stratum to 200. That gives the final allocation. 

| | A             | B            | C              |D              |E             |F         |
|-|:--------------|:-------------|:---------------|:--------------|:-------------|:---------|
|1| Stratum (*h*) | Forest (1)   | Non-Forest (2) |For. Dist. (3) |FD buf. (4)   |Total     |
|2| Area [m2]     |625,597,113,080|462,219,395,097|15,594,353,281 |32,599,448,433|1,136,010,309,891|
|3| *Wh*          |0.551       |0.407         |0.0137	    |0.0287	         |1             |
|4|*qh*           |	0.0005    	|	0.002     |	0.8         |	0.0075	     |              |		
|5|SD*h*          |	0.0223      |	0.04468   |	0.4         |	0.086277     |              |		
|6|SD*h* x *Wh*   |	0.0123      |	0.01818   |	0.005491	|	0.002475     |              |	
|7|*MoE* [%]      |		       	|	          |	25		    |	             |              |
|8|SE(*p^*)	      |		        |	          |0.001716	    |	             |              |		
|9|*n*		      |			    |	          |             |	             |502           |
|10| *nh* (prop.) |277      	|204	      |7	        |14              |502           |
|11| *nh* (final) |275      	|200	      |30	        |30              |535           |

The reason for why 30 is regarded is the minimum sample size is best described by Lohr (1999)![^fn8]: 

> The imprecise term “sufficiently large” occurs in the central limit theorem because the adequacy of the normal approximation depends on n and on how closely the population {yi, i = 1, ... , N} resembles a population generated from the normal distribution. The “magic number” of n = 30 [is] often cited in introductory statistics books as a sample size that is “sufficiently large” for the central limit theorem to apply

The central limit theorem is important because it states that the sum of independent random variables are normally distributed  even if the variables themselves are not. For example, the theorem allows us to construct confidence intervals by using common z-scores and a standard error.

## 5. Two-stage/cluster sampling
Because of the complexity associated with two-stage sampling, there are far fewer examples of these types of designs in the literature compared to STR and SRS/SYS. Further, there are no fixed rules to guide the size of the sample and the primary sampling units (PSUs) other than to find a compromise between the overall number of observations and a reasonable level of uncertainty for within-PSU estimates (Sannier et al., 2013)[^fn9]. Instead of creating examples, we will review two examples in literature. 

The first example is Potapov et al. (2014)[^fn7] who estimated the area of forest loss 2000-2011 across the Peruvian Amazon in support of REDD+.  The main source of reference data was commercial high resolution imagery; a two-stage design was chosen for cost-saving purposes as the budget allowed for purchasing only 30 high resolution datasets. In a two-stage design, reference data are only needed for the PSUs and not for the entire study area.   Accordingly, the sample size of the 30 PSUs was determined based on budgetary reasons and not specifying a target precision as in the examples above. The size of the PSUs of 12 × 12 km was chosen to align with the high resolution images. The 5,532 blocks, each 12 × 12 km,  covering the study area were seperated into a high (337 blocks) and low (5,195 blocks) forest-change stratum, from which 21 and 9 PSUs were selected under STR. (This selection was guided by the rules of optimal sample allocation in Cochran (1977)[^fn4].) Within each of the 30 PSUs, 100 secondary sampling units (SSUs) were selected under SRS in the second stage of the sampling. 

A second example is provided in Sannier et al. (2013)[^fn9] who estimated the proportion of forest cover and net  deforestation in Gabon using two-stage sampling. Two-stage sampling was chosen because it represented a compromise between the ease of data collection and geographic distribution. The study area was partitioned into 251 blocks of 20 × 20 km, each of which were further partitioned into 100 2 × 2 km blocks. In the first stage, one 2 × 2 km PSU was selected in each of the 251 20 x 20 km blocks under SRS. In the second stage, 50 SSUs corresponding to a Landsat pixel were selected under SRS.   

## 6. Software that allows for sample size estimation
SEPAL/CEO has built-in support for estimating sample size as explained in this documentation (scroll down to section 14). 

Similar to SEPAL is this spreadsheet developed by the World Bank which also calculates the sample size required to meet a precision of overall accuracy: https://onedrive.live.com/view.aspx?resid=9815683804F2F2C7!37340&ithint=file%2cxlsx&authkey=!ANcP-Xna7Knk_EE
 


## 7. Selecting the sample
The final step of the sampling design is to physically draw the sample from the study area, which is covered in the next tutorial.

## License
This work is licensed under a [Creative Commons Attribution 3.0 IGO](https://creativecommons.org/licenses/by/3.0/igo/) 

Copyright 2020, World Bank. This work was developed by Pontus Olofsson under World Bank contract with GRH Consulting, LLC for the development of new -and collection of existing- Measurement, Reporting, and Verification related resources to support countries' MRV implementation. 

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
