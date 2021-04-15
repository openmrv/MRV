---
title: Stratified random sampling
summary: Sampling-based approaches in a remote sensing or geographical context are necessary because they allow us to estimate area bias, map accuracy and uncertainty. A sampling-based approach to estimation can be separated into three different components - sampling design, response design and analysis (Stehman & Czaplewski, 1998). The first component, sampling design, is illustrated in this tutorial for the case of stratified random sampling design. Other tutorials here on OpenMRV under process "Sampling design" explore other sampling design approaches (e.g. Simple random/systematic sampling design).
author: Pontus Olofsson
creation date: February, 2021
language: English
publisher and license: Copyright 2021, World Bank. This work is licensed under a Creative Commons Attribution 3.0 IGO

tags:
- OpenMRV

- QGIS
- GEE
- AREA2
- Sampling design
- Sample design
- Sample selection
- Sample
- Sampling frame
- Stratified
- Colombia

group:
- category: Stratified
  stage: Sampling
- category: Cluster
  stage: Sampling

---

# Stratified random sampling 

## 1 Background

A sampling-based approach to estimation can be separated into three different components: sampling design, response design and analysis (Stehman & Czaplewski, 1998). The first component, sampling design, is illustrated in this tutorial.  The sampling design defines the protocol for selecting the subset of units -- i.e. the sample -- from a larger population. In our case, the population is the equivalent of the study area, and characteristics of the study area, such as the area of a certain land cover, are estimated by analyzing the sample.  Sampling-based approaches in a remote sensing or geographical context are necessary because they allow us to estimate area bias, map accuracy and uncertainty. As explained in the GFOI Methods & Guidance Document, estimating areas of land cover and land cover change by simply counting pixels in maps will produce erroneous results because of classification errors (GFOI, 2016, p. 125):

> Methods that produce estimates of activity data as sums of areas of map units assigned to map classes are characterized as pixel counting and generally make no provision for accommodating the effects of map classification errors. Further, although confusion or error matrices and map accuracy indices can inform issues of systematic errors and precision, they do not directly produce the information necessary to construct confidence intervals. Therefore, pixel-counting methods provide no assurance that estimates are “neither over- nor under-estimates” or that “uncertainties are reduced as far as practicable”. The role of reference data, also characterized as accuracy assessment data, is to provide such assurance by adjusting for estimated systematic classification errors and estimating uncertainty, thereby providing the information necessary for construction of confidence intervals for compliance with IPCC good practice guidance.

When choosing a sampling design, we need to consider a few but important design criteria. Of primary importance is the adherence to probability sampling.  Probability sampling is defined in terms of inclusion probabilities, where an inclusion probability relates the likelihood of a given unit being included in the sample; the inclusion probability must be known for each unit selected in the sample and the inclusion probability must be greater than zero for all units in the study area (Stehman, 2009). Several probability sampling designs are applicable to accuracy and area estimation, with the most commonly used designs being simple random, stratified random, and systematic. Two-phase (also called double), two-stage and cluster sampling are applicable but more complicated. 

## 2 Learning Objectives
The objective of this tutorial is to provide the user an understanding of the various key decisions involved in designing a sampling-based effort to estimation. Of importance is an understanding of the relationship between the sample size and the allocation of sample units to strata, and critical estimation objectives such as target precision. Upon completion of the tutorial, the user should be able to choose a sample selection method -- systematic (SYS), simple random (SRS) or stratified random (STR) --, determine sample size, and allocate the sample to strata, based on estimation objectives.  For this specific tutorial, we will focus on Stratified random sampling design.
* Understand the various key decisions involved in designing a sampling-based effort to estimation
* Choose a sample selection method -- SYS, SRS or STR based on estimation objectives
* Determine sample size, and allocate the sample to strata, based on estimation objectives for the stratified random sampling design.

### 2.1 Pre-requisites
* Relevant terminology for sampling techniques can be found at the end of this document 
* Google Earth Engine (GEE) account. Please refer to process "Pre-processing" and tool "GEE" here on OpenMRV for more information about working in this environment.

## 3 Tutorial: Sampling design for estimation of area and map accuracy - Stratified random sampling

### 3.1 How to choose a sampling design?
Choosing a sampling design often involves tradeoffs among different criteria and priorities.  The desire to  provide estimates for subregions or the need to meet precision targets will need to be balanced against desirable sampling design criteria such as the ease and practicality of implementation, cost effectiveness, the ease of accommodating changes in sample size.  Stehman (2009) provides a detailed review of sampling design options, objectives, and criteria, but the decision typically boils down to three key decisions: whether to use strata, whether to use clusters, and whether to implement a systematic or simple random selection protocol. 

#### 3.1.1 Use strata?

Strata are “subpopulations that are non-overlapping, and together comprise the whole population” (Cochran, 1977, p. 89). Stratifying the study area prior to the sample selection can ensure that estimates of accuracy and area are obtained for certain subregions in the study area, and it results in higher precision of estimates. Accordingly, there are several good reasons for using strata. Even with simple random sampling, the use of strata after selecting the sample is a good idea (see Section 3.2.1 Post stratification below). Stratified sampling provides an  obvious advantage  if we are interested in a very small proportion of the study area, as is often the case in tropical MRVs. For example, the area of forest loss, even in countries with rampant deforestation, is often a very small proportion of the country, especially over short time intervals. The use of a map of forest loss (and other categories) to stratify the study area in such situations allows for targeted sampling in areas of particular interest. Not stratifying in such situations will require a very large sample size. 

#### 3.1.2 Use simple random or systematic selection?
Systematic selection involves  selecting a starting point at random with equal probability and then sampling with a fixed distance between sample locations. In short, simple random selection is preferable if collecting reference observations in satellite data whereas systematic selection is preferable if visiting sample locations in situ (Olofsson et al. 2014). The rationale for this recommendation is that systematically selected units are easier to locate in the field while random selection is easier to augment. Note that the same estimators are used with both simple random or systematic selection. 

#### 3.1.3 Use cluster?
A cluster is a sampling unit that consists of one or more of the basic assessment units specified by the response design. For example, a cluster could be a 3 × 3 block of 9 pixels or a 1 km × 1 km cluster containing 100 1 ha assessment units. In cluster sampling, a sample of clusters is selected and the spatial units within each cluster are therefore selected as a group rather than selected as individual entities. Two-stage sampling is a form of cluster sampling where large primary sampling units are (PSUs) are selected at the first stage;  smaller secondary sampling units (SSUs) are selected within each PSU in the second stage.  Such designs have the benefit of requiring reference data (i.e. the data used for collecting reference observations) only over PSUs instead of the entire study area which is the case with the aforementioned designs. However, unless the cost savings are considerable, cluster-based designs are not recommended as the correlation between SSUs  often reduces precision relative to a simple random sample of equal size, and because they are complicated designs that are difficult to augment with sample results that are difficult to analyze. 

### 3.2 Stratified random sampling
The motivation to use STR arises when we are trying to estimate something that is a small proportion of the population, and under SRS/SYS, a very large sample size is required. In such situations, stratified random sampling (STR) is recommended. STR is simply when “simple random sampling is taken in each stratum” (Cochran 1977, p. 89). Accordingly, we split the population into strata and select a sample in each strata under SRS (or SYS). STR adds another level of complexity and requires us to determine how to allocate the sample unit to strata in addition to determining the total sample size. For more information about SRS/SYS, please consult here on OpenMRV the tutorials under process "Sampling design".

#### 3.2.1 Sample size
Just as with SRS/SYS, we need to specify a precision objective and calculate using the STR variance estimator the total sample size (*n*) required to meet the target precision. Solving the STR variance estimator gives (Olofsson et al., 2014, Eq. 13. modified from Cochran, 1977, Eq 5.25)

![](https://latex.codecogs.com/svg.latex?\Large&space;n=\left&space;[\frac{\sum_{h}W_h\textup{SD}_h}{\text{SE}(p)}\right&space;]^2)

*Wh* is the weight of stratum *h*, which is simply the area of the stratum expressed as a proportion of the total study area; SD*h* is the standard deviation of stratum *h*, which is explained below. The target standard error is SE(*p*). We will demonstrate the calculation using a map from another tutorial here on OpenMRV that can be found under process "Change detection" and tool "CODED". This map is a map of disturbance, stable forest and stable non-forest and can be found as a GEE asset [here](https://code.earthengine.google.com/?asset=users/openmrv/MRV/CODED_Colombia_Stratification_No_Buffer). The sample size calculation under STR can be complicated so we'll use a spreadsheet from Google Sheets (or Microsoft Excel if you prefer). The spreadsheet used in this tutorial can be accessed here: https://docs.google.com/spreadsheets/d/1lmPt35SvR3X7txpn0cwd-xkgwC_4nRPL520OZZcRKX0/edit?usp=sharing  

##### Step 1 
First we need to compute the  number of pixels of each stratum; this can be done using GDAL, QGIS, Google Earth Engine, etc.; if you went through the tool "CODED" here on OpenMRV, these areas are printed in the *Console* in Google Earth Engine. If not, or if you have an existing GEE asset, load the asset using the AREA2 Stratified Random Sampling script  (https://code.earthengine.google.com/6a0f89221d40ee039362974d303ff5aa) to compute the strata weights. Add these numbers on the first row "Area [px]". On the second row, express these areas as a proportion (in cell B3 type "=B2/sum($B2:$D2") and extend to E2). These proportions are referred to as the strata weights (*Wh*) 


| | A             | B            | C              |D              |E             |
|-|:--------------|:-------------|:---------------|:--------------|:-------------|
|1| Stratum (*h*) | Forest (1)   | Non-Forest (2) |For. Dist. (3) |Total     |
|2| Area [m2]     |658,196,561,513|	462,219,395,097|15,594,353,281|	1,136,010,309,891|
|3| *Wh*          |0.579       |0.407         |0.0137	         |1         |

##### Step 2
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

##### Step 3
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

##### Step 4
Finally, we can now easily calculate the sample size on row 8, cell E9 as: "=(sum(B6:D6)/B7)^2"

| | A             | B            | C              |D              |E             |
|-|:--------------|:-------------|:---------------|:--------------|:-------------|
|1| Stratum (*h*) | Forest (1)   | Non-Forest (2) |For. Dist. (3) |Total             |
|2| Area [m2]     |658,196,561,513|	462,219,395,097|15,594,353,281|	1,136,010,309,891|
|3| *Wh*          |0.579          |0.407           |0.0137	      |1                 |
|4|*qh*           |	0.001         |	0.002	       |0.8           | 		         |
|5|SD*h*          |	0.0316        |	0.0447	       |0.4	          |                  |
|6|SD*h* x *Wh*   |	0.0183        |	0.01818        |0.005491      |	                 |
|7| MoE [%]       |               |                |25            |                  |
|8| SE(*p^*)      |               |                |0.00172       |                  |
|9| *n*           |               |                |              | 599              |

which gives a sample size of 599 -- i.e. about 1/8 of the sample size of 4,600 required under SRS to reach the same precision. To change the target precision, we now simply need to either adjust our target precision in cell D7.

#### 3.2.2 Buffer strata
A potential issue in the situation above is that the omissions of disturbance present in the forest stratum will have a big impact on the precision of estimates.  Such omission errors are sample units in the forest stratum that were observed in the reference data as being disturbance. The issue is explained in detail in Olofsson et al. (2020) and here we just recognize that the "uncertainty contribution" of omission errors to a large extent depends on the size of the stratum in which they occur. We would therefore like to decrease the size of the forest stratum which is currently 83% of the study area. In particular, we want to create small substrata where disturbance omissions are likely to occur. One approach explored in the literature is the creation of buffer strata around change strata -- the rationale is that errors are likely to occur close to correctly mapped change. In our case, such a buffer stratum might be defined as the pixels in the forest stratum adjacent to the disturbance. 

Let's illustrate the creation of a buffer. Click this link: A script to create a buffer in the output from the tool "CODED" here on OpenMRV is available in AREA2: 
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

A buffer of three pixels were used here just as an example. For more information about how to determine the size of buffer strata, please see Olofsson et al. (2020). 

#### 3.2.3 Allocation
Let's assume that we settled for the margin of error of 15% with a buffer stratum and a sample size of 958.  We now need to decide how to allocate the sample to strata. In short, an allocation proportional to the strata weights are efficient for estimating parameters that include across-strata calculations -- such parameters include area, overall and producer's accuracy. Estimation of user's accuracy is based on within-strata calculations that benefit from an equal allocation. Achieving a high precision of the user's accuracy is rarely an estimation objective which suggests that a proportional allocation is preferable. Going back to the spreadsheet, lets calculate on row 10 the sample size in each stratum following a proportional allocation: in cell B10:  "=B3*$F$9" and extend to E10.

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

The reason for why 30 is regarded is the minimum sample size is best described by Lohr (1999): 

> The imprecise term “sufficiently large” occurs in the central limit theorem because the adequacy of the normal approximation depends on n and on how closely the population {yi, i = 1, ... , N} resembles a population generated from the normal distribution. The “magic number” of n = 30 [is] often cited in introductory statistics books as a sample size that is “sufficiently large” for the central limit theorem to apply

The central limit theorem is important because it states that the sum of independent random variables are normally distributed  even if the variables themselves are not. For example, the theorem allows us to construct confidence intervals by using common z-scores and a standard error.

### 3.3 Two-stage/cluster sampling
Because of the complexity associated with two-stage sampling, there are far fewer examples of these types of designs in the literature compared to STR and SRS/SYS. Further, there are no fixed rules to guide the size of the sample and the primary sampling units (PSUs) other than to find a compromise between the overall number of observations and a reasonable level of uncertainty for within-PSU estimates (Sannier et al., 2013). Instead of creating examples, we will review two examples in literature. 

The first example is Potapov et al. (2014) who estimated the area of forest loss 2000-2011 across the Peruvian Amazon in support of REDD+. The main source of reference data was commercial high resolution imagery; a two-stage design was chosen for cost-saving purposes as the budget allowed for purchasing only 30 high resolution datasets. In a two-stage design, reference data are only needed for the PSUs and not for the entire study area.   Accordingly, the sample size of the 30 PSUs was determined based on budgetary reasons and not specifying a target precision as in the examples above. The size of the PSUs of 12 × 12 km was chosen to align with the high resolution images. The 5,532 blocks, each 12 × 12 km,  covering the study area were seperated into a high (337 blocks) and low (5,195 blocks) forest-change stratum, from which 21 and 9 PSUs were selected under STR. (This selection was guided by the rules of optimal sample allocation in Cochran (1977).) Within each of the 30 PSUs, 100 secondary sampling units (SSUs) were selected under SRS in the second stage of the sampling. 

A second example is provided in Sannier et al. (2013) who estimated the proportion of forest cover and net  deforestation in Gabon using two-stage sampling. Two-stage sampling was chosen because it represented a compromise between the ease of data collection and geographic distribution. The study area was partitioned into 251 blocks of 20 × 20 km, each of which were further partitioned into 100 2 × 2 km blocks. In the first stage, one 2 × 2 km PSU was selected in each of the 251 20 x 20 km blocks under SRS. In the second stage, 50 SSUs corresponding to a Landsat pixel were selected under SRS.   

### 3.4 Software that allows for sample size estimation
SEPAL/CEO has built-in support for estimating sample size as explained in [this documentation](https://sepal-ceo.readthedocs.io/en/latest/).

Similar to SEPAL is this spreadsheet developed by the World Bank which also calculates the sample size required to meet a precision of overall accuracy: https://onedrive.live.com/view.aspx?resid=9815683804F2F2C7!37340&ithint=file%2cxlsx&authkey=!ANcP-Xna7Knk_EE

### 3.5 Selecting the sample
The final step of the sampling design is to physically draw the sample from the study area, which is covered here on OpenMRV under process "Sampling design" and tools "QGIS", "GEE", "AREA2".

## 4 Frequently Asked Questions (FAQs)
**I don't understand the qh variable that is used to calculate the sample size under STR -- what does it mean?**

The variable *qh* is needed to calculate the standard deviation of stratum *h* and is he proportion of stratum *h* that is the target class. In the example above we have three strata (before creating the buffer stratum), *h* = 1 is forest, *h* = 2 is non-forest, and *h* = 3 is forest disturbance, with the latter being the target class. In this case, *qh* is the proportion of forest disturbance in each strata. If the map was perfect, then all the forest disturbance in the study area would be present in the forest disturbance stratum and hence *q3* = 1, while *q1* and *q2* would be zero. No map is perfect and we will need to assume some level of classification error. Note that this information is unknown at the design stage and an educated guess is necessery. For example, if  *q3* = 0.8, then we are assuming that 80% of the forest disturbance in the study is present in the forest disturbance stratum. If *q1* = 0.001, then we assume that 0.1% of the forest stratum is forest disturbance. 

**I have no idea how to determine values of qh -- what do I do?**

The variable *qh* is in essence an indication of how well the stratification captures the class of interest. Because maps are typically used to stratify the study area, I would recommend reviewing the accuracy of previous maps of the same area. Note that *qh* for *h* = the class of interest, is the anticipated user's accuracy of the class of interest.

**How do I determine a target standard error?**

Certain programs specify a desired or required precision; the Forest Carbon Partnership Facility (FCPF) for example stipulate a margin of error of 30% at the 95% confidence level for area estimates of activity data. The margin of error is 1.96 times the standard error divided by the area estimate. When no such precision requirements are specified, a target standard error needs to be determined based on other critera. Note that the smaller the area proportion of the target class, the larger the sample is needed to reach a small margin of error. Accordingly, for small area proportions, the target precision will need to be relaxed to avoid having to select a very large sample. 

**If I use a buffer stratum, how many pixels should it be?**

It is hard to provide recommendations as the size of the buffer will depend on the situations. A larger buffer will probably "capture" more omission errors but will have a larger stratum weights. A larger buffer is recommended in situations of a small class of interest in the presence of a large stable stratum (such as stable forest). Examples in the literature range from 1 to 3 pixels. A more detailed exploration of the impact of buffer size is presented in Olofsson et al. (2020). 

## 5 Terminology

A list of terms relevant to the sampling and inference techniques are provided in the AREA2 documentation: https://area2.readthedocs.io/en/latest/definitions.html  Below are a few additional terms not included in the AREA2 documentation.  

### 5.1 Response design

Defined by (Stehman and Czaplewski, 1998):  “The reference or ‘true’ classification is obtained for each sampling unit based on interpreting aerial photography or videography, a ground visit, or a combination of these sources. The methods used to determine this reference classification are called the ‘response design.’ The response design includes procedures to collect information pertaining to the reference land-cover determination, and rules for assigning one or more reference [labels] to each sampling unit.” Referred to as “measurement plan” by Särndal et al. (1992).

### 5.2 Sample

A subset of population units selected from the population.

### 5.3 Sample design

Synonymous with sampling design, which is the preferred term in the seminal literature (Cochran, 1977, Särndal et al., 1992). The term occurs in Rice (1995) who uses both “sampling design” and “sample design”. 

### 5.4 Sampling design

“The sampling design is the protocol by which the reference sample units are selected.” (Stehman and Czaplewski, 1998). “Sampling design” is also used by Cochran (1977) and Särndal et al. (1992) - the former also uses “sampling plan”. 

### 5.5 Survey

Särndal et al. (1992) defines a survey as a “partial investigation of a finite population”, and further that “that the terms ‘survey’ and ‘sample survey’ are used to denote statistical investigations with the following methodological features: [...] probability sampling [...] measurement plan [and] estimation”

### 5.6 Survey design

A “total survey design” defines the procedures for “obtaining the possible precision in the survey estimates while striking a balance between sampling and non-sampling errors [...] The survey design gives rise to survey operations” such as sample selection (Särndal et al., 1992). Lohr (1999) describes a total survey design as “A philosophy of survey design for minimizing nonsampling as well as sampling errors.” Also, in Lohr (1999) “survey design” is synonymous with sampling design. 

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

![](figures/cc.png)  

This work is licensed under a [Creative Commons Attribution 3.0 IGO](https://creativecommons.org/licenses/by/3.0/igo/)

Copyright 2021, World Bank 

This work was developed by Pontus Olofsson under World Bank contract with GRH Consulting, LLC for the development of new -and collection of existing- Measurement, Reporting, and Verification related resources to support countries’ MRV implementation. 

Material reviewed by:   
Ana Mirian Villalobos, El Salvador, Ministry of Environment and Natural Resources  
Carole Andrianirina, Madagascar, National Coordination Bureau REDD+ (BNCCREDD)  
Foster Mensah, Ghana, Center for Remote Sensing and Geographic Information Services (CERGIS)    
Jennifer Juliana Escamilla Valdez, El Salvador, Ministry of Environment and Natural Resources   
Paula Andrea Paz, Colombia, International Center for Tropical Agriculture (CIAT)    
Phoebe Oduor, Kenya, Regional Centre For Mapping Of Resources For Development (RCMRD)   
Rajesh Bahadur Thapa, Nepal, International Centre for Integrated Mountain Development (ICIMOD)    
Tatiana Nana, Cameroon, REDD+ Technical Secretariat  

Attribution  
Olofsson, P. 2021. Stratified random sampling. © World Bank. License:  [Creative Commons Attribution license (CC BY 3.0 IGO)](http://creativecommons.org/licenses/by/3.0/igo/)  
![](figures/wb_fcfc_gfoi.png)
