# Response design in AREA2 

## 1. Background
The response design defines the "response" of the units in a sample. In the contex of design-based inference in a geographical context, "the response design encompasses all steps of the protocol that lead to a decision regarding agreement of the reference and map classifications [and] the best available classification of [land surface conditions] for each spatial unit sampled" (Olofsson et al. 2014) [^fn1].  Of imporance the following terms:

**Reference data**
Data characterizing the most accurate available assessment of the true condition at the sample location (example: fine-resolution satellite imagery).

**Reference observations**
The most accurate available assessment of the true condition of a population unit.

**Reference classification**
The reference classification applied to the collection of all sample units.

In this tutorial, we will determine reference conditions by examining a set of reference data at locations of the units of the sample that we drew from Colombia in the previous tutorial. We defined four strata: forest, non-forest, forest disturbance and a buffer around the forest disturbance. The objective is to estimate the area of forest disturbance; accordingly, we will collect reference observations of *forest, non-forest*, and *forest disturbance*.

## 2. Prepare reference data
 The first step is to extract time series of Landsat data at sample locations. We do this using the script Save Feature Timeseries: https://code.earthengine.google.com/?scriptPath=projects%2FGLANCE%3Aglance%2Fsubmit%2FprepareTS%2FextractTS_getRegion This script does not have a GUI but all we need to do is point the script to the GEE asset containing the sample. At the top of the script, simply add the following line specifying the location of the sample selected in the previous step:
 ```
 var sample = ee.FeatureCollection('users/olofsson76/Open_MRV/STR_sample_Col')
 ```
 Also change the dates at 'start' and 'end' in the script according to you study period. Click Run in Tasks and save the output as a GEE asset and name it "[filename]_TS".
 
 
## 3. Examine reference data at sample locations

The reference collector is located here: https://code.earthengine.google.com/09964c3fbb9a7d9f8530ee687be8bb90
Once loaded, specify a path to save your work under "Inputs and Outputs" and by "Link to FC", specify the location of the asset containing the sample after being processed using the Save Feature Timeseries script as described above. Check "Load chart data from feature collection" and click "Load". This should display the sample size -- in my case, I am using the sample of 535 units that we designed in the sampling design tutorial. 

To get started, under  "Sample interpretation" specify "1" and hit enter -- this will display reference data for the first unit in the sample. Of importance are the time series plots in the center of the interface -- time series are displayed for Landsat bands Red, NIR and SWIR1, and for the Tasseled Cap (Kauth-Thomas) transformations Brightness, Greenness and Wetness. The first six plots show time series data for the study period specified in the Save Features Timeseries script above; you can zoom into a certain time interval and the plots can be popped to a seperate window by clicking the arrow next the each plot. The latter six plots are accumulated annual time series plots such that data for each year are plotted "on top" of each other.  

Above the time series data is the outline of the sample unit draped on top of the default GEE satellite imagery -- click "KML" to display high resolution data in Google Earth at sample locations.

 [image: AREA2_ref_collector.png]
 
For now, we recommend the user to write down the reference labels in a seperate spreadsheet as the the implementation of the saving the reference labels in a single feature collection is ongoing. Videos illustrating how to observe reference conditions by examining the reference data are provided here (the videos are part of the NASA MEaSUREs GLanCE project at Boston University http://sites.bu.edu/measures/):  
https://drive.google.com/file/d/1Y_D49kE_oiXxGEJEcPGT8FavrzdMj2qh/view?usp=sharing
https://drive.google.com/file/d/1Md5NajZAngJsVWWiTCbgSdLiEyw7u6BE/view?usp=sharing

## License
This work is licensed under a [Creative Commons Attribution 3.0 IGO](https://creativecommons.org/licenses/by/3.0/igo/) 

Copyright 2020, World Bank. This work was developed by Pontus Olofsson under World Bank contract with GRH Consulting, LLC for the development of new -and collection of existing- Measurement, Reporting, and Verification related resources to support countries' MRV implementation. 

Attribution: Olofsson, P. (2021). *Open MRV: Response Design*. World Bank. License: Creative Commons Attribution license (CC BY 3.0 IGO)

## References
[^fn1]: Olofsson, P., Foody, G. M., Herold, M., Stehman, S. V., Woodcock, C. E., & Wulder, M. A. (2014). Good practices for estimating area and assessing accuracy of land change. *Remote Sensing of Environment*, 148, 42-57.
