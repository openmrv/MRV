# Sample selection 

## 1. Background

In the previous tutorial, we designed a sample by choosing a selection protocol and determining the sample size and allocation. In this tutorial we will physically draw from a study area the sample that we designed. Drawing a sample involve creating a *sampling frame* which is a list of population units that can be selected for inclusion in a sample. The population units in the list are referred to as sampling units. In other words, a frame is a device that provides observational access to the population by associating the population units with the sampling units (Särndal et al., 1992, p. 9)[^fn1]. In our case, the sampling frame is for example a list of all the pixels that make up the study area. We could, therefore, simply export a list of all map pixels with unique identifiers from which we randomly select *n* units. Under stratified random sampling, each pixel would in addition to the identifier also have a stratum code such that a random sample are selected from each stratum. Such an approach can easily become impractical as the number of population units tend to be large. Instead, sample selection is supported by various tools and software -- here, we illustrate how to draw a sample in QGIS, Google Earth Engine/AREA2, and a R script.   

## 2. Simple random and systematic sampling in QGIS
QGIS provides support for sampling populations defined by vector data. Hence, if you want to sample in strata that are defined by a raster, you will first need to vectorize the raster data. This is done Raster > Conversions > Polygonize (Raster to Vector). Vectorization for large rasters will take a long time and is not recommended; instead, use the alternatives below. For smaller study areas or for SYS and SRS designs, QGIS  works well -- let's go through the steps required to draw two samples under SRS and SYS from the country of Colombia.
#### 2.1 Simple random sampling
1. We first need a shapefile that outlines our study area. Download a shapefile of the Colombia border here: https://drive.google.com/file/d/1tXvczTra_5wrlXBhe00m_oKRpLK0GwwJ/view?usp=sharing
2. Display the file in QGIS: Layer > Add Layer > Add Vector Layer and select the colombiaborder.shp to draw shapefile on the canvas. 
3. Vector > Research Tools > Random Points Inside Polygons
4. Specify the Colombia border as input layer, Points count as sampling strategy and the total sample size under Point count; leave min. distance "Save to a file and click Run to draw the sample.

[image: SRS_QGIS.png]

#### Systematic sampling 
Drawing a sample under SYS in QGIS has the drawback that the population has to be rectangular which makes it harder to draw an exact number of units for a non-rectangular area. We can simply clip the sample units for the Colombia border but that will result in a smaller sample size  than specified. A workaround is to set a distance between based on the size of the study area. For example, if the study area is *x* km^2^, setting a the spacing between units to x/100  would result in a sample of 100 units   
1. After having added the shapefile in point 2.1.2 above, go to Vector > Reserach Tools > Regular Points
2. Select as input extent, the Colombia border shapefile
3. Specify a Point spacing or Point count -- if using the former, check the box "Use point spacing" 
4. Save to a file and click Run to draw the sample.

[image: SYS_QGIS.png]

## 3. Stratified random sampling in Google Earth Engine/AREA2
In the sampling design script we estimated a sample size required to reach a 25% margin of error of the forest disturbance area estimate, and we allocated the sample in strata for the purpose of area estimation. That gave use the following sample size:

| | A             | B            | C              |D              |E             |F         |
|-|:--------------|:-------------|:---------------|:--------------|:-------------|:---------|
|1| Stratum (*h*) | Forest (1)   | Non-Forest (2) |For. Dist. (3) |FD buf. (4)   |Total     |
|11| *nh* (final) |275      	|200	      |30	        |30              |535           |

To select this sample, lets use AREA2 to select a sample under stratified random sampling:
https://code.earthengine.google.com/?accept_repo=users%2Fopenmrv%2FMRV&scriptPath=projects%2FAREA2%2Fpublic%3A1.%20Sampling%20Design%2FStratified%20Random%20Sampling and specify the path to the CODED-based map of Colombia (https://code.earthengine.google.com/?asset=users/olofsson76/Open_MRV/Open_MRV_Col_strat_buffer) with a buffer under "Specify stratification/image to define study area"; use the other default arguments click "Load image" which will display the strata areas in the Console (NOTE: it will take a some time). Select Arbitrary sample size under "Determine sample size", and specify under "Allocate sample size to strata": 275, 200, 30, 30. Click "Create sample" -- note: only click once; it looks like GEE doesn't react but it's drawing the sample after you clicked. Clicking Add to map will display the sample units as red dots in the Map display. The final step is to export the sample: click the Tasks tab, and then Export sample in the Dialog – two entries named “sample_asset” and "sample_CSV" will appear in Tasks. These are identical but one is for exporting the sample as a CSV file, one to save as a GEE Asset file for use in Google Earth Engine. Click the Run button right next to the entries and save as GEE Asset and CSV (the latter should be saved to your Google Drive). Use the name “STR_sample_Col” for GEE Asset and the CSV file.  

[image: STR_AREA2.png]


## 3. Stratified random sampling in R

The World Bank as implemented the following scripts in R that allows a user to select a sample under STR using a stratification in raster format. The code comments are maninly in French but instructions for running the scipts are  provided below.  

The first script calculates the strata weights and is available for download here: https://drive.google.com/file/d/1b5kZD_Eb73MwKvWPpGIqokyJpQJZ0rZ1/view?usp=sharing
There are a few things that we need to specify before we can run the script. If you are running RStudio you will need install the following packages: rgdal, raster, and stringr.  Then after you have opended the script in RStudio you need to set the working directory. Below, the working directory is set to C:/Users/olofsson/Desktop/STR_example/ in a Windows operating system -- change this to the directory hosting your stratification. Note that you have to use a forward slash "/" even when specifying a Windows directory.
```R
###################DEFINIR DES ENTREES###############################################
#set working directory. Il faut definir ici le directoire. Il faut mettre / au lieu de \
wd <- "C:/Users/olofsson/Desktop/STR_example/"
setwd(wd)
```
Second, specify the name of the stratification in raster format, the spatial resolution  of the stratification, and the name of the output CSV file:

```R
# read a raster, GeoTiff or something. 
Raster <- raster('Col_strat_buffer_subset.tif')
 
##Resolution de la carte utilise
Res <- 30
 
##Fichier avec les superficies par estrate
Output <- "Col_Strat_buffer_subset_Wh.csv"
```
This will output the strata weights which we now can be used to design the sampling effort. (Note that there are many other ways to compute the areas of strata including  the "GDALINFO -hist" command.)

Now we can select the sample using the second script which is accessible from here: 
https://drive.google.com/file/d/1NbfEUBzwsAToxAkFFho2ltowb3Par8iE/view?usp=sharing

Again, there are few arguments in the code that we need to specify. First you have to create a CSV file with two columns, one column called "map_value" with the value of each stratum and another column called "final" with the number of sample size in each stratum. You must put the file in the work directory. Then on  
Line 12: set the working directory
Line 19: point to file containing the stratification 
Line 22: specify the resolution
Line 26: point to CSV file containing the sample size
Line 29: specify the name of the output CSV for use in Collect Earth
Line 35: specify the name of the output shapefile containing the sample

## License
This work is licensed under a [Creative Commons Attribution 3.0 IGO](https://creativecommons.org/licenses/by/3.0/igo/) 

Copyright 2020, World Bank. This work was developed by Pontus Olofsson under World Bank contract with GRH Consulting, LLC for the development of new -and collection of existing- Measurement, Reporting, and Verification related resources to support countries' MRV implementation. 

Attribution: Olofsson, P. (2021). *Open MRV: Sample Selection*. World Bank. License: Creative Commons Attribution license (CC BY 3.0 IGO)

## References
[^fn1]: Särndal, C. E., Svensson, B. H., & Wretman, J. H. (1992). *Model assisted survey sampling*. New York, NY: Springer

