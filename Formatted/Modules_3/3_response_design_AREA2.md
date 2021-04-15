---
title: Response design in AREA2
summary: This tutorial will go through how to use AREA2 for response design and collection of reference observations. AREA2, short for Area Estimation & Accuracy Assessment, is a Google Earth Engine application that provides comprehensive support for sampling and estimation in a design-based inference framework. For more information about AREA2 please refer to https://area2.readthedocs.io/en/latest/
author: Pontus Olofsson
creation date: February, 2021
language: English
publisher and license: Copyright 2021, World Bank. This work is licensed under a Creative Commons Attribution 3.0 IGO

tags:
- OpenMRV
- Remote sensing
- GEE
- AREA2
- Time series
- Response design
- Survey
- Survey design
- Reference data
- Reference classification
- Reference observations
- Colombia

group:
- category: GEE
  stage: Reference data collection
---

# Response design in AREA2 

## 1 Background

AREA2, short for Area Estimation & Accuracy Assessment, is a Google Earth Engine application that provides comprehensive support for sampling and estimation in a design-based inference framework. For more information about AREA2 please refer to https://area2.readthedocs.io/en/latest/.

The response design defines the "response" of the units in a sample. In the context of design-based inference in a geographical context, "the response design encompasses all steps of the protocol that lead to a decision regarding agreement of the reference and map classifications and the best available classification of land surface conditions for each spatial unit sampled" (Olofsson et al. 2014). Of importance the following terms:

**Reference data**

Data characterizing the most accurate available assessment of the true condition at the sample location (example: fine-resolution satellite imagery).

**Reference observations**

The most accurate available assessment of the true condition of a population unit.

**Reference classification**

The reference classification applied to the collection of all sample units.

Additional terminology regarding sampling and inference techniques can be found in the AREA2 documentation: https://area2.readthedocs.io/en/latest/definitions.html. Below are a few terms not included in the AREA2 documentation:

**Response design** (similar definitions)

Defined by (Stehman and Czaplewski, 1998):  “The reference or ‘true’ classification is obtained for each sampling unit based on interpreting aerial photography or videography, a ground visit, or a combination of these sources. The methods used to determine this reference classification are called the ‘response design.’ The response design includes procedures to collect information pertaining to the reference land-cover determination, and rules for assigning one or more reference labels to each sampling unit.” Referred to as “measurement plan” by Särndal et al. (1992).

**Sample**

A subset of population units selected from the population.

**Sample design**

Synonymous with sampling design, which is the preferred term in the seminal literature (Cochran, 1977, Särndal et al., 1992). The term occurs in Rice (1995) who uses both “sampling design” and “sample design”. 

**Sampling design**

“The sampling design is the protocol by which the reference sample units are selected.” (Stehman and Czaplewski, 1998). “Sampling design” is also used by Cochran (1977) and Särndal et al. (1992) - the former also uses “sampling plan”. Tutorials addressing sampling design can be found here on OpenMRV under process "Sampling design".

**Survey**

Särndal et al. (1992) defines a survey as a “partial investigation of a finite population”, and further that “that the terms ‘survey’ and ‘sample survey’ are used to denote statistical investigations with the following methodological features: [...] probability sampling [...] measurement plan [and] estimation”

**Survey design**

A “total survey design” defines the procedures for “obtaining the possible precision in the survey estimates while striking a balance between sampling and non-sampling errors [...] The survey design gives rise to survey operations” such as sample selection (Särndal et al., 1992). Lohr (1999) describes a total survey design as “A philosophy of survey design for minimizing nonsampling as well as sampling errors.” Also, in Lohr (1999) “survey design” is synonymous with sampling design. 

In this tutorial you will learn how to determine reference conditions by examining a set of reference data at locations of the units of a sample dataset using AREA2. This sample dataset will have four strata: forest, non-forest, forest disturbance and a buffer around the forest disturbance. The objective is to estimate the area of forest disturbance; accordingly, you will learn how to collect reference observations of *forest, non-forest*, and *forest disturbance*. 

You can also use other tools to accomplish this. You can find more tutorials here on OpenMRV under "Sample data collection" and tools "CE", and "CEO".

## 2 Learning Objectives

Upon completion of the tutorial, the user should be able to display a set of reference data at locations of sample units designed and drawn from a study area. The user should be able to determine reference conditions at the land surface by examining time series of Landsat data in combination with high resolution data in Google Earth. 

* Display a set of reference data at locations of sample units in GEE
* Determine reference conditions at the land surface by examining time series of Landsat data in combination with high resolution data in GEE

### 2.1 Pre-requisites
* A general understanding of image interpretation. Image interpretation is the process of looking at moderate, high, or very high spatial resolution imagery (from satellites or aerial photography) and labeling the objects of interest in your sample locations. Photo interpretation is the core skill needed to effectively determine reference conditions at the land surface.

## 3 Tutorial: Response design in AREA2

### 3.1 Prepare reference data

The first step is to extract time series of Landsat data at sample locations. We do this using the script Save Feature Timeseries: https://code.earthengine.google.com/?scriptPath=projects%2FGLANCE%3Aglance%2Fsubmit%2FprepareTS%2FextractTS_getRegion. This script does not have a GUI but all we need to do is point the script to the GEE asset containing the sample. At the top of the script, simply add the following line specifying the location of the sample (here we are demonstrating the exercise using a sample dataset generated in another tutorial here on OpenMRV under process "Sample selection" and tools "AREA2" and "QGIS"):

```javascript
var sample = ee.FeatureCollection('users/olofsson76/Open_MRV/STR_sample_Col')
```

Also change the dates at 'start' and 'end' in the script according to you study period. Click Run in Tasks and save the output as a GEE asset and name it "[filename]_TS".

### 3.2 Examine reference data at sample locations

The reference collector is located here: https://code.earthengine.google.com/09964c3fbb9a7d9f8530ee687be8bb90
Once loaded, specify a path to save your work under "Inputs and Outputs" and by "Link to FC", specify the location of the asset containing the sample after being processed using the Save Feature Timeseries script as described above. Check "Load chart data from feature collection" and click "Load". This should display the sample size -- in my case, I am using the sample of 535 units that we designed in the sampling design tutorial. 

To get started, under  "Sample interpretation" specify "1" and hit enter -- this will display reference data for the first unit in the sample. Of importance are the time series plots in the center of the interface -- time series are displayed for Landsat bands Red, NIR and SWIR1, and for the Tasseled Cap (Kauth-Thomas) transformations Brightness, Greenness and Wetness. The first six plots show time series data for the study period specified in the Save Features Timeseries script above; you can zoom into a certain time interval and the plots can be popped to a seperate window by clicking the arrow next the each plot. The latter six plots are accumulated annual time series plots such that data for each year are plotted "on top" of each other.  

Above the time series data is the outline of the sample unit draped on top of the default GEE satellite imagery -- click "KML" to display high resolution data in Google Earth at sample locations.

![](figures/AREA2_ref_collector.png)

For now, we recommend the user to write down the reference labels in a separate spreadsheet as the the implementation of the saving the reference labels in a single feature collection is ongoing. Videos illustrating how to observe reference conditions by examining the reference data are provided here (the videos are part of the NASA MEaSUREs GLanCE project at Boston University http://sites.bu.edu/measures/):  
https://drive.google.com/file/d/1Y_D49kE_oiXxGEJEcPGT8FavrzdMj2qh/view?usp=sharing
https://drive.google.com/file/d/1Md5NajZAngJsVWWiTCbgSdLiEyw7u6BE/view?usp=sharing

## 4 Frequently Asked Questions (FAQs)

**If I can't determine the reference conditions at the location of a sample unit, can I discard that unit from the sample?**

It is imperative that the reference observations represent reference conditions; therefore, it is better to discard a sample unit than guessing. At the same time, removing units because the provision of reference labels is impossible violates the rules of probability sampling. For these reasons, it is difficult to provide guidelines for how many sample units can be discarded. (A renowned colleague of mine once told me that it is acceptable to remove discard up to 15% of the units in sample but he didn't want to be quoted, and I have not found any support for this figure in the literature.)

## 5 References

Cochran, W.G., 1977. *Sampling Techniques*, John Wiley & Sons, New York, NY.

Lohr, S.L., 1999. *Sampling: Design And Analysis,* CRC Press.

Olofsson, P., Foody, G.M., Herold, M., Stehman, S.V., Woodcock, C.E. and Wulder, M.A., 2014. Good practices for estimating area and assessing accuracy of land change. Remote Sensing of Environment, 148, pp.42-57. https://doi.org/10.1016/j.rse.2014.02.015

Rice, J.A., 1995. *Mathematical Statistics and Data Analysis* (2nd ed.), Duxbury Press, Belmont, CA.

Särndal, C.E., Svensson, B.H., & Wretman, J.H., 1992. *Model assisted survey sampling*, Springer Science & Business Media, New York, NY.

Stehman, S.V., & Czaplewski, R.L., 1998. Design and analysis for thematic map accuracy assessment: fundamental principles. *Remote Sensing of Environment*, 64(3), 331-344. https://doi.org/10.1016/S0034-4257(98)00010-8

-----

![](figures/cc.png)  

This work is licensed under a [Creative Commons Attribution 3.0 IGO](https://creativecommons.org/licenses/by/3.0/igo/).

Copyright 2021, World Bank

This work was developed by Pontus Olofsson under World Bank contract with GRH Consulting, LLC for the development of new- and collection of existing- Measurement, Reporting, and Verification related resources to support countries' MRV implementation.

Material reviewed by:   
Ana Mirian Villalobos, El Salvador, Ministry of Environment and Natural Resources  
Carole Andrianirina, Madagascar, National Coordination Bureau REDD+ (BNCCREDD)  
Jennifer Juliana Escamilla Valdez, El Salvador, Ministry of Environment and Natural Resources   
Phoebe Oduor, Kenya, Regional Centre For Mapping Of Resources For Development (RCMRD)   
Tatiana Nana, Cameroon, REDD+ Technical Secretariat  

Attribution  
Olofsson, P. 2021. Response Design in AREA2. © World Bank. License: [Creative Commons Attribution license (CC BY 3.0 IGO)](http://creativecommons.org/licenses/by/3.0/igo/)

![](figures/wb_fcfc_gfoi.png)