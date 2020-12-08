# 1.1 Image mosaic/composite creation for Landsat and Sentinel-2 in Google Earth Engine

## 1 Background

This tutorial will walk you through how to create a composite using Landsat and/or Sentinel-2 imagery on a national level in Google Earth Engine (GEE). Here, the process is demonstrated for the country of Colombia. The tutorial is accompanied by a GEE repository that contains three scripts, and a series of videos that walk you through some of the sections. The scripts enable you to create a composite that can be used in subsequent sections of this training. 

### 1.1 Pre-requisites for this module

* Basic to intermediate understanding of remote sensing concepts
  * You may refer to [NASA ARSET's Fundamentals of Remote Sensing](https://appliedsciences.nasa.gov/join-mission/training/english/fundamentals-remote-sensing) training. This includes basics of satellite remote sensing, including satellite orbits, types, resolutions, sensors, and processing levels. It is on demand and anyone can take it (available only in English)
* Google Earth Engine account 
  * Anyone can sign up for Google Earth Engine. GEE is free for non-commercial use. To sign up, please fill out [this form](https://earthengine.google.com/signup/). Once you have been accepted, you will receive an email with additional information
* Basic to intermediate programming knowledge
  * See useful tutorials and information on GEE JavaScript programming under Section 3 Google Earth Engine
* GEE works best with [Google Chrome browser](https://www.google.com/chrome/)

### 1.2 Repository

[This repository](https://code.earthengine.google.com/?accept_repo=users/openmrv/MRV) contains a subfolder called "Composite" with scripts that perform all the operations that you will learn in this tutorial. The main scripts are:

1. `Landsat_Sentinel2_Median` contains all the steps in the order you will go through (except for Section 4.2.6 Medoid composite) for creating median composites using Landsat and Sentinel-2 Collections.
2. `Landsat_Sentinel2_Median2` is an optimized version of the above script. It contains all user variables at the top and functions/code that do not need to be modified below.
3. `Landsat_Medoid` contains the compositing method using the Medoid instead of Median for the Landsat Collections.

Additionally, you will find two scripts that are a copy of the script 2. `Landsat_Sentinel2_Median2` but applied to two other countries: Mozambique and Cambodia. In the repository they are called `Mozambique` and `Cambodia`. These are explained in Section 6. Additional Examples.

Finally, the script called `Video` is the script generated from the recording of the videos. This script contain all the steps in this tutorial but with little to no written documentation.

It is encouraged that you follow the steps below by writing the scripts on your own to have a better learning experience, and only use the above scripts for consultation during the tutorial, or after the understanding of all the processes explained here.

### 1.3 Videos

The [Open MRV YouTube channel](https://www.youtube.com/channel/UCdPooUCxF3HRIWdEh4pwrqQ) contains videos that walk you through some sections of this and other modules. For this module, a video was created for each subsection of Section 4. Creating a composite. Please note that the script development in the videos might not be exactly the same as demonstrated in each step of the tutorial (i.e., order of code lines and variable names might differ, etc.), and that each video is built upon previous ones. In any case, the same outputs are produced. You can find in each section below a hyperlink to its corresponding video. It is recommended to go through each section before watching the videos.

## 2 Learning objectives

* Learn how to create an image mosaic/composite

* Become familiar with a variety of options that include: selecting dates, sensors, and mosaicking methods
* Learn how to export the mosaic/composite

## 3 Google Earth Engine

The appeal of using Google Earth Engine (GEE) is that GEE contains multi-petabytes of satellite imagery and geospatial datasets allowing users to compute massive-scale analysis in the cloud-based platform. GEE contains a JavaScript (used in this case) and a Python API, where users can upload their own datasets and use built-in functions  to accomplish a myriad of remote sensing and geospatial tasks at unprecedented speeds and scales. For more information about GEE please refer to [the main page about Google Earth Engine](https://earthengine.google.com/). There you can find useful tutorials and documentation. Some relevant links are highlighted below:

* [Datasets available](https://developers.google.com/earth-engine/datasets/) 
* [FAQs](https://earthengine.google.com/faq/)
* [Getting started with GEE](https://developers.google.com/earth-engine/guides/getstarted)
* [Introduction to the JavaScript API](https://developers.google.com/earth-engine/tutorials/tutorial_api_01)
* [Documentation](https://developers.google.com/earth-engine)
* [API reference](https://developers.google.com/earth-engine/apidocs)
* [Code Editor guide](https://developers.google.com/earth-engine/guides/playground)
* [Community tutorials](https://developers.google.com/earth-engine/tutorials)
* [Debugging Guide](https://developers.google.com/earth-engine/guides/debugging)
* [How to get help](https://developers.google.com/earth-engine/help)
* [Google Earth Outreach: Introduction to Google Earth Engine](https://www.google.com/earth/outreach/learn/introduction-to-google-earth-engine/)
* Google's [2019 Geo for Good Summit](https://sites.google.com/earthoutreach.org/geoforgood19/home) presentations:
  * [Earth Engine for non-coders](https://docs.google.com/presentation/d/10DTcBGPl0JeTEOJlSRNdj9dtGLwqq7HPLzegENygI-U/edit?usp=sharing)
  * [Coding in Earth Engine](https://docs.google.com/presentation/d/1KCOcW1PtFUzC4R2g3pbovtO19C4VPtjRXJxCwkG1b5Q/edit?usp=sharing)
  * [EE Datasets Tour and Data Upload](https://docs.google.com/presentation/d/1ODCtpBYLTNCFkFhTMBHmyVBU41XfYzv8WUN7c0dwizc/edit?usp=sharing)
  * [Earth Engine Big Data Structures](https://docs.google.com/presentation/d/1Ksax77YPEvmseush73-6GueGA765KHBNcxuJDE9154k/edit?usp=sharing)

![](figures/m1.1/GEEcodeEditor.png)



## 4 Creating a composite 

The general workflow of the process for this tutorial is demonstrated below: 

![](figures/m1.1/WB_graphs_v2-02-crop.png)



Now let's go through each of these steps. Open the Code Editor by typing [https://code.earthengine.google.com](https://code.earthengine.google.com) in your web browser. 

On the left side of the Code Editor is the **Docs** tab, which contains the complete JavaScript API documentation. The documentation can be searched and browsed from the Docs tab. All the GEE functions used in this tutorial can be found in the Docs tab.

Please note that in this specific tutorial, we are going to create a 2019 median composite for the country of Colombia for demonstration purposes. This tutorial does not guarantee that the methods shown will fit perfectly every user case (i.e., produce the best composite). One can, and should, test different time periods, study areas, and methods.

### 4.1 Area of Interest

> The following steps are demonstrated in the script `1_Landsat_Sentinel2_Median`.  
> [Video Instructions](https://youtu.be/KoEJW1i-v_w)

To start, we need to define our area of interest. We will use the [Large Scale International Boundary (2017) simplified dataset](https://developers.google.com/earth-engine/datasets/catalog/USDOS_LSIB_SIMPLE_2017) by the United States Department of State (USDOS) which contains polygons for all countries of the world. In GEE, this dataset is a `FeatureCollection`, i.e., a group of features. You can think of features as your vector data. You can find information about `FeatureCollection` [here](https://developers.google.com/earth-engine/guides/feature_collections).

Search "USDOS" in the *Search* box of the code editor and click on "LSIB 2017: Large Scale International Boundary Polygons, Simplified".

![](figures/m1.1/searchlisb.png)



A popup window will show the description, table schema (properties), and terms of use of this dataset.

![](figures/m1.1/lisbGEE.png)

Copy and past the code below to create a variable for this dataset.

```javascript
var lsib = ee.FeatureCollection("USDOS/LSIB_SIMPLE/2017");
```

> NOTE: Alternatively, **any** GEE dataset can be added to your script by clicking the *IMPORT* button next to the dataset. The imported dataset will show up at the top of the code editor under *Imports* as a variable with a default name `image` for images, `imageCollection` for Image Collections, `geometry` for geometries, `table` for Feature Collections, and so on. You can change this name by clicking over the default name (in this case `table`) and writing the new name.

Now, let's filter this `FeatureCollection` to grab only the polygon for Colombia. We will do this by using the `filterMetadata` function in GEE. One of the LSIB dataset's properties is called `country_na` and it represents the name of country (US-recognized) for each polygon. Therefore, we will filter our variable `lsib` by `country_na` that are equal to "Colombia". Copy and paste the code below to create a variable `country` for Colombia's boundaries.

```javascript
var country = lsib.filterMetadata('country_na','equals','Colombia');
```

To visualize this boundary, you can use the `Map.addLayer` function. But before, you should center the Map to this area of interest by using `Map.centerObject`. Copy and paste the code below to define the map center over Colombia and add the Colombia's polygon `country` to the map. Click *Run* to see the results. You will see that under the *Layers* panel you will have a layer named "Colombia".

```javascript
Map.centerObject(country,5);
Map.addLayer(country,{},'Colombia');
```

![](figures/m1.1/colombiaGEE2.png)

> NOTE: Adjust the zoom level to your preference by changing the number `5` to any number between 1 and 24. The higher the number, the more zoomed in the map. You can use the slider under the *Layers* panel on the map to change the opacity of the layer.
>
> NOTE 2: The `Map.addLayer` function can take 5 different arguments:
>
> * `eeObject`: The object to add to the map (in this case the variable `country`).
> * `visParams`: The visualization parameters. These are explained later on. In the example above we have left these empty `{}`.
> * `name`: The name of the layer (a string, in our case: `'Colombia'`).
> * `shown`: A flag indicating whether the layer should be on by default (This can be very helpful when testing different approaches and having various layers). This is a Boolean argument and it defaults to `True`.
> * `opacity`: The layer's opacity represented as a number between 0 and 1. Defaults to 1.



### 4.2 Landsat Collection

#### 4.2.1 Starting with Landsat 8

> [Video Instructions](https://youtu.be/J6o6NLqsobw)

We will start creating a composite from the Landsat 8 collection. First, let's define two time variables that we will call `startDate` and `endDate`. Here, we will create a composite for the year 2019, so use the code bock below to define the time variables. Date objects are by default in the `YYYY-MM-DD` format.

```javascript
var startDate = '2019-01-01';
var endDate = '2019-12-31';
```

Now, let's define our Landsat 8 collection variable. We will use the [USGS Landsat 8 Surface Reflectance Tier 1](https://developers.google.com/earth-engine/datasets/catalog/LANDSAT_LC08_C01_T1_SR) product in GEE. This dataset is the atmospherically corrected surface reflectance from the Landsat 8 OLI/TIRS sensors. These images contains 5 visible and near-infrared (VNIR) bands and 2 short-wave infrared (SWIR) bands processed to orthorectified surface reflectance, and two thermal infrared (TIR) bands processed to orthorectified brightness temperature.

```javascript
var l8 = ee.ImageCollection('LANDSAT/LC08/C01/T1_SR');
```

> NOTE: If you try to `print` this collection, an error message will be returned in the Console. This collection contains the entire Landsat 8 archive from 2013 to the present day for the entire globe. Any print collection query will abort after accumulating the metadata for over 5,000 elements.

Next, let's filter this collection to our area of interest (Colombia, `var country`) and time period (`startDate, endDate`). We will use the `filterBounds` and `filterDate` functions.

```javascript
var l8Filt = l8.filterBounds(country)
			   .filterDate(startDate,endDate);
```

Print `l8Filt` to see your filtered collection. Click *Run* after adding the line below. The *Console* will show that the collection has 956 images.

```javascript
print('L8 SR collection filtered',l8Filt);
```

![](figures/m1.1/printL8v4.png)

With your filtered collection, create a composite using a median reducer. We will use the `median()` function for `ee.ImageCollection` and the `clip()` function to clip the composite to the area of interest. 

The `median()` function for `ee.ImageCollection` is what is called in GEE a `ee.Reducer`, and we are using specifically the `ee.Reducer.median()` reducer. Reducers are the GEE way to aggregate data over time, space, bands, arrays, and other data structures. The figure below demonstrates an image collection being "reduced" to an individual image by a `ee.Reducer`:

![](figures/m1.1/Reduce_ImageCollection2.png)

In our case, we are taking the median over the time series (our collection).  The output is computed pixel-wise, such that each pixel in the output is composed of the median value of all the images in the collection at that location. Alternatively, you can test using mean `mean()`, min `min()`, etc, as reducers instead of median.

> For more information and examples about Reducers, and reducing an Image Collection specifically, please check these pages:
>
> * [Reducer Overview](https://developers.google.com/earth-engine/guides/reducers_intro)
> * [ImageCollection Reductions](https://developers.google.com/earth-engine/guides/reducers_image_collection)
> * [Reducing an ImageCollection](https://developers.google.com/earth-engine/guides/ic_reducing)
> * [Compositing, Masking, and Mosaicking](https://developers.google.com/earth-engine/tutorials/tutorial_api_05)

Copy and paste the code below and click *Run*. The output will be an `ee.Image`.

```javascript
var composite = l8Filt.median().clip(country);

Map.addLayer(composite,{bands:['B4','B3','B2'],min:300,max:3000},
             'L8 Composite 2019');

print('L8 composite 2019',composite);
```

> NOTE: There are a number of options available to adjust how images are displayed using the `Map.addLayer` function. These go in the `visParams` argument of the `Map.addLayer` function. The inputs that are most commonly used to modify display settings include the following:
>
> * Bands: allows the user to specify which bands to render as red, green, and blue. In the case above we are using Landsat 8's bands B4, B3, and B2 which correspond to red, green, and blue bands, respectively.
>* Min and max: sets the stretch range of the colors. The range is dependent on the data type. For example unsigned 16-bit imagery has a total range of 0 to 65,536. This option lets you set the display to a subset of that range. In this case, we set min as 300 and max as 3000 and these correspond to the surface reflectance values.
> * Palette: specifies the color palette used to display information. Not used in this case.
>
> You can test visualization parameters by clicking on gear icon ![](figures/m1.1/gear2.png) next to the layer "Composite 2019" and playing with the stretch options.
> 
> ![](figures/m1.1/visParams2.png)



![](figures/m1.1/l8cloudycomposite.png)

You should see a very cloudy image in the Map like the one above. Let's try adding a pre filter for clouds when filtering our collection. The Landsat collection comes with a property named `CLOUD_COVER`, and we can define a cloud cover percentage as a threshold to filter the scenes. We will use the `filterMetadata` function to filter images with cloud cover of less than 50%. Copy and paste the code below and click *Run*.

```javascript
var l8Filt2 = l8.filterBounds(country)
               .filterDate(startDate,endDate)
               .filterMetadata('CLOUD_COVER','less_than',50);

print('Landsat 8 SR collection filtered for clouds',l8Filt2);

var composite2 = l8Filt2.median().clip(country);

Map.addLayer(composite2,{bands:['B4','B3','B2'],min:300,max:3000},
             'L8 composite 2019 pre cloud filter');

print('L8 composite 2019 pre cloud filter',composite2);
```

You will see that this new composite looks slightly better than the previous one but still very cloudy. In the Console, also note that the new collection has 454 images compared to 956 in the previous not-cloud-filtered one.

![](figures/m1.1/l8cloudycompositev2.png)

Try adjusting the `CLOUD_COVER` threshold to different percentages and checking results. Example: with 20% set as the threshold, you can see that many parts of the country have image gaps. Additionally, some tiles, even with a cloud filter, still present large area cover of clouds.

![](figures/m1.1/l820cloudthreshold2.png)

This is due to persistent cloud cover in some regions of Colombia. We can apply a Cloud Mask to improve the results. The Landsat 8 collections contains a ["Quality Assessment (QA)" band](https://www.usgs.gov/core-science-systems/nli/landsat/landsat-collection-1-level-1-quality-assessment-band?qt-science_support_page_related_con=0#qt-science_support_page_related_con) called `pixel_qa` that provides useful information of certain conditions within the data, and allows users to apply per pixel filters. Each pixel in the QA band contains unsigned integers that represent bit-packed combinations of surface, atmospheric, and sensor conditions. Of particular interest here, are Bits 3 and 5 that represent cloud shadow, and cloud, respectively. 

We will create a `function` to apply a cloud mask to every image in the image collection by using the image collection function `map`. Copy and paste the code below and click *Run*.

```javascript
function maskL8srClouds(image) {
  // Bits 3 and 5 are cloud shadow and cloud, respectively.
  var cloudShadowBitMask = (1 << 3);
  var cloudsBitMask = (1 << 5);
  // Get the pixel QA band.
  var qa = image.select('pixel_qa');
  // Both flags should be set to zero, indicating clear conditions.
  var mask = qa.bitwiseAnd(cloudShadowBitMask).eq(0)
                .and(qa.bitwiseAnd(cloudsBitMask).eq(0));
  return image.updateMask(mask);
}

var l8FiltMasked = l8.filterBounds(country)
                .filterDate(startDate,endDate)
                .filterMetadata('CLOUD_COVER','less_than',50)
                .map(maskL8srClouds);

print('L8 SR collection filtered and masked', l8FiltMasked);

var l8compositeMasked = l8FiltMasked.median().clip(country);

print('L8 composite 2019 masked', l8compositeMasked);

Map.addLayer(l8compositeMasked,
             {bands:['B4','B3','B2'],min:0,max:2000},
             'L8 composite 2019 masked');
```

> NOTE: Because we are dealing with Bits, in the `maskL8srClouds(image)` function we utilized the left shit operator `<<` to shift the first operand the specified number of bits to the left, and the `bitwiseAnd` function to calculate the bitwise AND of the input values. For more details, check:
>
> * Bits: [Earth Observatory - Remote Sensing Pixels and Bits](https://earthobservatory.nasa.gov/features/RemoteSensing/remote_06.php), [NASA Earthdata - What is Remote Sensing?](https://earthdata.nasa.gov/learn/backgrounders/remote-sensing), [National University of Singapore - Digital Image](https://crisp.nus.edu.sg/~research/tutorial/image.htm)
> * [Left shift operator in JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Left_shift)
> * [GEE `bitwiseAnd` function](https://developers.google.com/earth-engine/apidocs/ee-image-bitwiseand)

![](figures/m1.1/l8masked2.png)

The resulting composite shows masked clouds and is a great improvement compared to previous composites. However, data gaps are still an issue due to cloud cover. If you do not specifically need an annual composite, you can create a two-year composite to try mitigating the missing data issue. We will try this next.

> NOTE: At this point, you probably have noticed that the layers are taking a while to load, i.e. the script is overall "slower". To avoid waiting too much to check results, and running into an `Earth Engine memory capacity exceeded` error, you can comment out some of the `print` and `Map.addLayer` statements, and/or unused variables by adding double forward slashes `//` at the beginning of the lines **or** by clicking on the desired line and pressing *Ctrl + /*. Use this strategy throughout the rest of this tutorial and only print and add layers to the map of desired composites, or to check intermediate errors if you run into one.
>
> Visual example of code snippet uncommented:
>
> ```javascript
> var composite = l8Filt.median().clip(country);
> 
> Map.addLayer(composite,{bands:['B4','B3','B2'],min:300,max:3000},'Composite 2019');
> 
> print('L8 composite 2019',composite);
> ```
>
> Visual example of code snippet commented:
>
> ```javascript
> // var composite = l8Filt.median().clip(country);
> 
> // Map.addLayer(composite,{bands:['B4','B3','B2'],min:300,max:3000},'Composite 2019');
> 
> // print('L8 composite 2019',composite);
> ```
>
> NOTE 2: You can also set the argument `shown` in the `Map.addLayer` functions to be `False` so the layers won't be on automatically when added to the Map.

#### 4.2.2 Adding one more year of data

> [Video Instructions](https://youtu.be/Q5cjLW_yf7k)

We will create a new variable `l8TwoYearComposite` which will be our Landsat 8 two-year composite. We will filter the Landsat 8 collection with a different start date this time (`2018-01-01`) to include images from both 2018 and 2019, apply the cloud mask function, then apply the median reducer to get the composite, and finally clip to the country of Colombia. Copy and past the code below and click *Run*:

```javascript
// Incorporating 2018 data
// Create a two-year composite by filtering Landsat 8 data in 2018 and 2019,
// applying the cloud mask, the median reducer, and clipping to country
var l8TwoYearComposite = l8.filterBounds(country)
                .filterDate('2018-01-01',endDate) // Note that we changed the start date
                .filterMetadata('CLOUD_COVER','less_than',60)
                .map(maskL8srClouds)
                .median()
                .clip(country);

Map.addLayer(l8TwoYearComposite,{bands:['B4','B3','B2'],min:0,max:2000},'Landsat 8 Two-Year composite');
```

![](figures/m1.1/twoYearComposite2.png)

The resultant image has substantially fewer gaps. Again, if the time period is not a constraint for the creation of your composite, you can incorporate more images from a third year, and so on.

Another option to improve data gaps is bringing in imagery from other sensors for the time period of interest. Luckily, the [Landsat collection spans different missions](https://www.usgs.gov/core-science-systems/nli/landsat/landsat-satellite-missions?qt-science_support_page_related_con=2#qt-science_support_page_related_con), which have continuously acquired uninterrupted data since 1972 at different acquisition dates. Next, we will try incorporating Landsat 7 images from 2019 to fill the gaps in the 2019 Landsat 8 composite, for demonstration.

#### 4.2.3 Adding the Landsat 7 Collection

> [Video Instructions](https://youtu.be/vu61q6vsno8)

Like Landsat 8, we will use the [USGS Landsat 7 Surface Reflectance Tier 1](https://developers.google.com/earth-engine/datasets/catalog/LANDSAT_LE07_C01_T1_SR) product in GEE. This dataset is the atmospherically corrected surface reflectance from the Landsat 7 ETM+ sensor. These images contain 4 visible and near-infrared (VNIR) bands and 2 short-wave infrared (SWIR) bands processed to orthorectified surface reflectance, and one thermal infrared (TIR) band processed to orthorectified brightness temperature. 

Let's first see how a Landsat 7 composite would look like for the sake of comprehensive understanding and completeness.

The next steps are very similar to the ones we did for Landsat 8. First, define your Landsat 7 collection variable.

```javascript
var l7 = ee.ImageCollection('LANDSAT/LE07/C01/T1_SR');
```

We will immediately apply a cloud mask to this collection since we saw that Colombia has consistent cloud cover. Let's define the cloud mask function for Landsat 7.

```javascript
function maskL7srClouds(image) {
  var qa = image.select('pixel_qa');
  // If the cloud bit (5) is set and the cloud confidence (7) is high
  // or the cloud shadow bit is set (3), then it's a bad pixel.
  var cloud = qa.bitwiseAnd(1 << 5)
                  .and(qa.bitwiseAnd(1 << 7))
                  .or(qa.bitwiseAnd(1 << 3));
  // Remove edge pixels that don't occur in all bands
  var maskL7 = image.mask().reduce(ee.Reducer.min());
  return image.updateMask(cloud.not()).updateMask(maskL7);
}
```

Let's filter the Landsat 7 collection with the same filters used for Landsat 8, apply the cloud mask, and create the Landsat 7 composite.

```javascript
var l7FiltMasked = l7.filterBounds(country)
                .filterDate(startDate,endDate)
                .filterMetadata('CLOUD_COVER','less_than',50)
                .map(maskL7srClouds);

print('L7 SR collection masked',l7FiltMasked);

var l7compositeMasked = l7FiltMasked.median().clip(country);

Map.addLayer(l7compositeMasked,{bands:['B3','B2','B1'],min:0,
                                max:2000},'L7 composite 2019 masked');
```

> NOTE: We used `bands:['B3','B2','B1']` this time because Landsat 7 has different band designations. The sensors aboard each of the Landsat satellites were designed to acquire data in different ranges of frequencies along the electromagnetic spectrum. Whereas for Landsat 8 the red, green, and blue bands are B4, B3, and B2, respectively, for Landsat 7, these same bands are B3, B2, and B1, respectively. For more information refer to [this page](https://www.usgs.gov/faqs/what-are-band-designations-landsat-satellites?qt-news_science_products=0#qt-news_science_products).

![](figures/m1.1/l7composite.png)

You should see an image with many gaps like the one above. The Landsat 7 was launched in 1999 but since 2003, the sensor has acquired and delivered data with data gaps caused by the Scan Line Corrector (SLC) failure. Without an operating SLC, the sensor’s line of sight traces a zig-zag pattern along the satellite ground track, and, as a result, the imaged area is duplicated. When the Level-1 data are processed, the duplicated areas are removed, leaving data gaps. For more information about Landsat 7 and SLC error, please refer to [this page](https://www.usgs.gov/core-science-systems/nli/landsat/landsat-7?qt-science_support_page_related_con=0#qt-science_support_page_related_con).

![](figures/m1.1/SLC.jpg)



However, even with the SLC error, we can still use the Landsat 7 data in our composite. Now, let's combine both Landsat 7 and 8 collections.

#### 4.2.4 Combining both sensors into one composite

> [Video Instructions](https://youtu.be/COobcYDThxo)

As mentioned previously, Landsat 7 and 8 have different band designations. Hence, let's start by creating a function to rename the bands from Landsat 7 to match Landsat 8's and map that function to our L7 collection. 

```javascript
// Since Landsat 7 and 8 have different band designations,
// let's create a function to rename L7 bands to match up L8.
function rename(image){
  return image.select(
    ['B1', 'B2', 'B3', 'B4', 'B5', 'B7'],
    ['B2', 'B3', 'B4', 'B5', 'B6', 'B7']);
}

// Apply the rename function
var l7FiltMaskedRenamed = l7FiltMasked.map(rename);

print('L7 SR collection renamed',l7FiltMaskedRenamed);
```

> NOTE: If you check the bands of the first images of both `l7FiltMasked` and `l7FiltMaskedRenamed` collections you will see that the band names got renamed, and not all bands got copied over (`sr_atmos_opacity`, `sr_cloud_qa`, `pixel_qa`,  `radsat_qa`, and `B6`). To copy these additional bands, simply add them to the rename function (for `B6` you will need to rename it so it does not have the same name as the new Band 5). The image below shows the bands of the first image of the Landsat 7 collection on the left, and the bands of the first image of the renamed Landsat 7 collection on the right.
>
> ![](figures/m1.1/rename2.png)

Now we merge both collections. We will use the `merge` function for `imageCollection`. Copy and paste the code below and click *Run*. You will see in the Console that now you have a collection with 999 images (563 from Landsat 8 and 436 from Landsat 7).

```javascript
// Merge Landsat collections
var l78 = l7FiltMaskedRenamed.merge(l8FiltMasked);
print('Merged collections',l78);
```

![](figures/m1.1/mergedCollection2.png)

Now, to create the composite, we do the same as before. Note that if you run the code below you will run into an error:

```javascript
// Create Landsat 7 and 8 image composite and add to Map
var l78composite = l78.median().clip(country); // can be changed to mean, min, etc
Map.addLayer(l78composite,{bands:['B4','B3','B2'],min:0,max:2000},
             'Landsat 7 and 8 composite');
```

![](figures/m1.1/tileError3.png)

This is because the Landsat 7 collection has 6 bands and the Landsat 8 has 12 bands. To be mosaicked and added to the map, they need to have the same number of bands. We will modify the code block that we are merging both collections to add a `select` function to the Landsat 8 collection. The `select` function will select specific bands from the images. We will select only the bands available in the Landsat 7 collection. Therefore, change the merging procedure to:

```javascript
// Merge Landsat collections
var l78 = l7FiltMaskedRenamed.merge(l8FiltMasked
          .select('B2','B3','B4','B5','B6','B7'));
print('Merged collections',l78);

// Create Landsat 7 and 8 image composite and add to Map
var l78composite = l78.median().clip(country); // can be changed to mean, min, etc
Map.addLayer(l78composite,{bands:['B4','B3','B2'],min:0,max:2000},
             'Landsat 7 and 8 2019 composite');
```

You should see an image composite that looks like this:

![](figures/m1.1/mergedComposite2.png)

Compared to the previous Landsat 8-only composite, you can see that some of the gaps have been filled. However, due to the general mosaicking/compositing nature, and Landsat 7's  SLC error, you can also see some artifacts in some regions. Example at centroid Latitude: 1.46, Longitude: -69.99. Landsat 8-only composite (left) and Landsat 7 and 8 composite (right) for 2019:

![](figures/m1.1/l8andMergedComparison.png)

#### 4.2.5 Trying to fill gaps with Focal Mean (or Median) functions

> [Video Instructions](https://youtu.be/hYtoWeVwoKs)

We can try filling gaps using a focal mean or focal median function to the images in the collection. These apply a morphological filter to each band of an image by inputting the pixels in a custom kernel and then applying a blend. For more information about GEE's focal functions check [this page](https://developers.google.com/earth-engine/guides/image_morph). On the same script, let's add the block of code below. First, we create a function to apply the `focal_mean` (or `focal_median`) function to each image in the Landsat 7 collection, then merge the collections as before, and create the composite. 

> NOTE: The `focal_mean` function contains 5 input arguments: `radius`, `kernelType`, `units`, `iterations`, and `kernel`. You can find information about each of them by searching focal mean in the *Docs* tab (and about any GEE function). For this example we defined a radius of 1.5, a square kernel type, pixel kernel, and 2 iterations. You can test with different variables. The larger these values the greater the blurring on the data.
>
> ![](figures/m1.1/focalMeanDocs.png)

```javascript
// Function to fill gaps from SLC error using focal mean 
function fillGap(image){
  return image.focal_mean(1.5, 'square', 'pixels', 2).blend(image);
}

// Apply fillGap function to Landsat 7 collection and merge with Landsat 8 collection
var l78Fill = l7FiltMaskedRenamed.map(fillGap).merge(l8FiltMasked
              .select('B2','B3','B4','B5','B6','B7'));

// Create commposite
var l78compositeFill = l78Fill.median().clip(country); // can be changed to mean, min, etc

Map.addLayer(l78compositeFill,{bands:['B4','B3','B2'],min:0,
                               max:2000},'Landsat 7 and 8 2019 composite focal fill');
```

You should see a composite like the one below. In this particular case, it might be worth not applying this method since it "created" new pixels that look like clouds and the previous method does a better job. However, for other regions, with less cloud cover, this additional step might be of use.

![](figures/m1.1/focalMean4.png)

#### 4.2.6 Medoid Composite

>  The following steps are demonstrated in the script `3_Landsat_Medoid`.
>
>  [Video Instructions](https://youtu.be/0cVKrY0IAYY)

A medoid is a representative object of a dataset whose average dissimilarity to all the objects in a cluster is minimal. The medoid approach in the remote sensing context was introduced by [Flood (2013)](https://www.mdpi.com/2072-4292/5/12/6481). For a given image pixel, the medoid is the value for a given band that is numerically closest to the median of all corresponding pixels among images considered (all images in the collection). We use the medoid approach to find the best available pixels for compositing, and as an alternative to median composites. The process requires little logic, is robust, and fast. You can think of the medoid as a multi-dimensional median. Please consult [Flood (2013)](https://www.mdpi.com/2072-4292/5/12/6481), and/or [Roberts et al. (2017)](https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=8004469) for a more in-depth explanation of the medoid approach.

We first calculate the difference between the median and the observation per image per band, then we get the medoid by selecting the image pixel with the smallest difference between the median and the observation per band. We will create a medoid composite for the Landsat merged collection of 2019 (`var l78`). Copy and paste the code below and check the results on the map.

```javascript
// Calculate median across images in collection per band
var l78median = l78.median(); // calculate the median of the annual image collection - returns a single 6 band image - the collection median per band
  
// Calculate the different between the median and the observation per image per band,
// then get the medoid by selecting the image pixel with the smallest difference 
// between median and observation per band.
var l78medoidComposite = l78.map(function(image) {
  var diff = ee.Image(image).subtract(l78median).pow(ee.Image.constant(2)); // get the difference between each image/band and the corresponding band median and take to power of 2 to make negatives positive and make greater differences weight more
  return diff.reduce('sum').addBands(image);  // per image in collection, sum the powered difference across the bands - set this as the first band add the SR bands to it - now a 7 band image collection
}).reduce(ee.Reducer.min(7)).select([1,2,3,4,5,6], ['B2','B3','B4','B5','B6','B7']) // find the powered difference that is the least - what image object is the closest to the median of the collection - and then subset the SR bands and name them - leave behind the powered difference band;
  .clip(country); 
  
Map.addLayer(l78medoidComposite,{bands:['B4','B3','B2'],min:0,max:2000},'L7&8 Medoid composite 2019');
```

![](figures/m1.1/LandsatMedoid2.png)



You should see an image like the one above. At first sight, you might think there is not much of a difference comparing with the median composite. However, the medoid composite can show significant improvements for certain pixels. See the example below for point (2.86, -74.73) where clouded areas in the median are better represented in the medoid composite.

![](figures/m1.1/MedoidComparison.png)

Now, let's create a 2019 median composite with the European Space Agency (ESA) Copernicus Sentinel-2 dataset. Sentinel-2 is a wide-swath, high-resolution, multi-spectral imaging mission supporting Copernicus Land Monitoring studies, including the monitoring of vegetation, soil and water cover, as well as observation of inland waterways and coastal areas. 

### 4.3 Sentinel-2 Collection

> The following steps are demonstrated in the script `1_Landsat_Sentinel2_Median`.
>
> [Video Instructions](https://youtu.be/13plGNvnmkI)

Let's start by defining our Sentinel-2 image collection variable. We will use the [Sentinel-2 MSI: MultiSpectral Instrument, Level-2A](https://developers.google.com/earth-engine/datasets/catalog/COPERNICUS_S2_SR) product in GEE from the European Space Agency, which is the Bottom-of-Atmosphere product (i.e. Surface Reflectance). 

```javascript
// We will use the Sentinel-2 Surface Reflection product.
// This dataset has already been atmospherically corrected
var s2 = ee.ImageCollection("COPERNICUS/S2_SR");
```

> NOTE: The Sentinel-2 L2 data in GEE are downloaded from ESA's [scihub](https://scihub.copernicus.eu/). They were computed by running [sen2cor](https://step.esa.int/main/third-party-plugins-2/sen2cor/). The assets contain 12 UINT16 spectral bands representing SR scaled by 10000 (unlike in L1 data, there is no B10). There are also several more L2-specific bands (see band list for details). See the [Sentinel-2 User Handbook](https://sentinel.esa.int/documents/247904/685211/Sentinel-2_User_Handbook) for details. In addition, three QA bands are present where one (QA60) is a bitmask band with cloud mask information. For more details, [see the full explanation of how cloud masks are computed.](https://sentinel.esa.int/web/sentinel/technical-guides/sentinel-2-msi/level-1c/cloud-masks)
>

We define a function to apply a cloud mask to Sentinel-2 images using the `QA60` band which contains information about cloud masks. Then, similarly to the Landsat collections, we will filter our Sentinel-2 collection by our defined parameters (`startDate`, `endDate`, `country`, etc). Copy and past the code below and click *Run*. 

```javascript
// Function to mask clouds S2
function maskS2srClouds(image) {
  var qa = image.select('QA60');

  // Bits 10 and 11 are clouds and cirrus, respectively.
  var cloudBitMask = 1 << 10;
  var cirrusBitMask = 1 << 11;

  // Both flags should be set to zero, indicating clear conditions.
  var mask = qa.bitwiseAnd(cloudBitMask).eq(0)
      .and(qa.bitwiseAnd(cirrusBitMask).eq(0));

  return image.updateMask(mask).divide(10000);
}

// Filter Sentinel-2 collection
var s2Filt = s2.filterBounds(country)
                .filterDate(startDate,endDate)
                .filterMetadata('CLOUDY_PIXEL_PERCENTAGE',
                                'less_than',50)
                .map(maskS2srClouds);

// print('Sentinel-2 Filtered collection',s2Filt);
```

> NOTE: For Sentinel-2 we use the property called `CLOUDY_PIXEL_PERCENTAGE` to filter cloudy scenes.
>
> NOTE 2: The `print` statement is commented out because if you try to print the collection it will return an error. Unlikely Landsat images which have a spatial resolution of 30 meters, Sentinel-2 images have a spatial resolution of 10 meters (for visible and NIR bands), the repeat cycle is shorter (12-day compared to 16-day of Landsat), and there is a difference in the swath width. These make the collection much larger, and, therefore, in this case, the filtered Sentinel-2 collection contains more than 5,000 elements, which is the limit to print in GEE.

Now, let's composite our 2019 collection and add to the map. 

```javascript
// Composite images
var s2composite = s2Filt.median().clip(country); // can be changed to mean, min, etc 

// Add composite to map
Map.addLayer(s2composite,{bands:['B4','B3','B2'],min:0.02,max:0.3,
                          gamma:1.5},'Sentinel-2 2019 composite');
```

![](figures/m1.1/s2composite2.png)

> Additional: You can try a different band combination to show the Sentinel-2 composite. Try the false color combination below using the SWIR 1, NIR, and Blue bands. This band combination is mostly used to monitor the health of crops because of how it uses short-wave and near-infrared. Both these bands are particularly good at highlighting dense vegetation which appears as dark green. [This page](https://gisgeography.com/sentinel-2-bands-combinations/) explains different Sentinel-2 band combinations.
>
> ```javascript
> // Test another band combination (SWIR 1, NIR, Blue)
> Map.addLayer(s2composite,{bands:['B11','B8','B2'],min:0,max:0.6},
>              'Sentinel-2 2019 composite SWIR/NIR/Blue');
> ```
>
> ![](figures/m1.1/s2compositeFalseColor2.png)

#### Warning: Surface Reflectance vs. Top-of-Atmosphere products

The European Space Agency did not produce Sentinel-2 Level-2 data (Bottom-of-Atmosphere reflectance; BOA) for all Level-1 assets (Top-of-Atmosphere radiance; TOA), and earlier Level-2 coverage is not global. You might not find these Surface Reflectance data for images before 2017. If you wish to work with images before 2017, please use the [Sentinel-2 MSI: MultiSpectral Instrument, Level-1C product](https://developers.google.com/earth-engine/datasets/catalog/COPERNICUS_S2) which corresponds to the Top-of-Atmosphere dataset. The GEE Asset ID for this collection is `"COPERNICUS/S2"`.

The Top-of-Atmosphere products have not been atmospherically corrected, therefore, a TOA composite will present differences compared to a BOA since it will represent influences from the atmosphere. An image of the 2019 median composite from Sentinel-2 L1 product is shown below together with the produced 2019 median composite from the L2 product for comparison.

![](figures/m1.1/TOA_BOAComparison3.png)

You can notice the blueish effect on the TOA composite. For more information about Sentinel-2 Processing Levels please check [this page](https://sentinel.esa.int/web/sentinel/user-guides/sentinel-2-msi/processing-levels) (and subpages [Level-0](https://sentinel.esa.int/web/sentinel/user-guides/sentinel-2-msi/processing-levels/level-0), [Level-1](https://sentinel.esa.int/web/sentinel/user-guides/sentinel-2-msi/processing-levels/level-1), and [Level-2](https://sentinel.esa.int/web/sentinel/user-guides/sentinel-2-msi/processing-levels/level-2)). Other resources about the differences between Radiance, Reflectance, and Top-of-Atmosphere are:

* Previously mentioned [NASA ARSET's Fundamentals of Remote Sensing](https://appliedsciences.nasa.gov/join-mission/training/english/fundamentals-remote-sensing) training (check for processing levels)
* [L3Harris Geospatial Solutions YouTube video](https://www.youtube.com/watch?v=sOk5fFPSDBA)
* [UN-SPIDER page](https://un-spider.org/node/10958)
* [USGS presentation](http://www.pancroma.com/downloads/General%20Landsat.pdf)
* Additional: [GEE Landsat algorithms](https://developers.google.com/earth-engine/guides/landsat) for different processing levels

## 5 Exporting your composite

Exporting data from the Code Editor is possible through the export functions, which include export options for images, tables, and videos. Export methods take several optional arguments so that you can control important characteristics of your output data, such as the resolution and region. You have three options to export an image: `Export.image.toDrive` to export to your Google Drive, `Export.image.toAsset` to export as a GEE Asset, and `Export.image.toCloudStorage` to export to your Google Cloud Storage. 

### 5.1 Export to your Google Drive

Add the statement below to the bottom of your script.  This will create a task in the *Task* tab that you can use to export your image  by clicking *Run*. The process is demonstrated for the combined Landsat median composite created. To export more composites, simply copy and paste the same code and change the name of the image composite for the additional Export functions.

```javascript
// To export to your Google Drive
Export.image.toDrive({
  image: l78composite,
  description: 'l78composite2019GDrive', // task name to be shown in the Tasks tab
  fileNamePrefix: 'l78composite', // filename to be saved in the Google Drive
  scale: 30, // the spatial resolution of the image
  region: country,
  maxPixels: 1e13
});
```

![](figures/m1.1/taskProcess.png)

> NOTE: In this example you have specified a few of the optional arguments recognized by `Export.image`. Though this function takes several optional parameters, it is valuable to familiarize yourself with these:
>
> * `maxPixels` - This restricts the numbers of pixels in the exported image. By default, this value is set to 10,000,000 pixels. You can set this argument to raise or lower the limit. “1e8” is 10 to the 8<sup>th</sup> power (10<sup>8</sup>).
> * `region` - By default, the viewport of the Code Editor is exported but you can also specify a geometry to change the export extent.
> * `scale` - The resolution in meters per pixel. The native resolution for Landsat data set is 30 meters.
> * `crs` - The coordinate reference system for the output image. This is specified using the EPSG code. You can look up the EPSG code for your desired spatial projections at http://spatialreference.org.
>
> NOTE 2: If you try to export an image that contains bands with different data types, you will see an error. All bands of a Sentinel-2 image are `unsigned int16`, therefore, you won't run into an error. However, for Landsat images, you will need to select specific bands by using the `select` function or cast bands to the same data type since data types vary for different bands (See below). We won't run into this problem since our Landsat combined composite only contains bands B2-7 that were selected previously, but for separate Landsat collections, you should apply the `select` function.
>
> ![](figures/m1.1/landsatDataType3.png)

Because we are exporting a composite for the entire country of Colombia, your export will take several minutes, perhaps hours. Once completed, you will notice that in the folder you specified, the composite you be broken down into separate GeoTiff files. E.g.:  l78composite2019-0000000000-0000000000.tif, l78composite2019-0000000000-000000xxxx.tif (with xxxx being different numbers), and so on.

> NOTE: to check the status of a task, hover the mouse over the export and click the ![](figures/m1.1/question2.png) icon. A window will appear showing the details:
>
> ![](figures/m1.1/taskDetails2.png)
>
> NOTE 2: For Sentinel-2, the pixel resolution is 10 meters and when exporting large images (like a composite for the entire country of Colombia) you might run into an export issue. If you ran into a size issue, increase the `scale`, or try to modify the `maxPixels`, or change the `region` to a smaller geometry. This is valid for all types of `Export` functions.

### 5.2 Export as an Asset

Similarly to the function above, copy and past the code below to export the image composite as a GEE Asset. The difference is `fileNamePrefix` becomes `assetId`. Change `YourPath` next to `assetId` to the actual path want the asset located.

```javascript
// To export as a GEE Asset
Export.image.toAsset({
  image: l78composite,
  description: 'l78composite2019Asset',
  assetId: 'YourPath/l78composite',
  scale: 30,
  region: country,
  maxPixels: 1e13
});
```

For information about managing your assets, please refer to [this page](https://developers.google.com/earth-engine/guides/asset_manager).

### 5.3 Export to a Google Cloud Storage bucket

If you use Google Cloud Storage, you can use the code block below. Change `YourBucket` to the actual bucket you want the image composite exported to.

```javascript
// To export to Google Cloud Storage
Export.image.toCloudStorage({
  image: l78composite,
  description: 'l78composite2019CloudStorage',
  fileNamePrefix: 'l78composite',
  bucket: 'YourBucket',
  scale: 30,
  region: country,
  maxPixels: 1e13
});
```

## 6 Additional Examples
In this tutorial, we have created and exported different composites for the country of Colombia. Now, you can test creating composites for the country of your choice. The scripts are designed in a way that all you need to do is change few lines of code. We will see examples for Mozambique and Cambodia. In all cases, the general process is the same as that demonstrated in Colombia. However, for other countries, some considerations might need to be taken into account when performing a land cover classification or detecting change in the landscape. Some considerations you will see in the following modules will be: 

* Accounting for Seasonality - Seasonal variability can present a challenge when performing land cover classification. In a dry season image over Mozambique, a deciduous forest could potentially be confused with herbaceous or non-forest land cover classes due to low vegetative greenness during a leaf-off period. Therefore, you might need to create separate composites for dry and wet seasons. You can achieve this by changing the `startDate` and `endDate` variables on the scripts.
* Accounting for Topography - Many of the remaining forests in Cambodia are located on hilly or mountainous terrain. Because topographic features cast a shadow, the reflectance of the landscape within the shadow can be lower than a similar non-shadowed landscape. Therefore, topography can also introduce a challenge to land cover classification or detecting change in the landscape.

### 6.1 Mozambique

In the scripts `1_Landsat_Sentinel2_Median` or `3_Landsat_Medoid`, simply change `'Colombia'` in line 15 (or in the appropriate line in case it's your own script) to `'Mozambique'  ` and click *Run*.

```javascript
var country = lsib.filterMetadata('country_na','equals','Mozambique');
```

In the script `2_Landsat_Sentinel2_Median2`, simply change `'Colombia'` in line 12 (or in the appropriate line in case it's your own script) to `'Mozambique'` and click *Run*. The script called `Mozambique` mentioned in Section 1.2. Repository is an exact copy of this script but with the change already made.

```javascript
var countryName = 'Mozambique';
```

Additionally, using the script `2_Landsat_Sentinel2_Median` or the script `Mozambique` as references, you can adjust any other user variable desired. E.g., zoom level, start and end dates, visualization parameters, and focal mean parameters. 

```javascript
/////////////////// User defined variables ////////////////////////////

// Country  Name
var countryName = 'Mozambique';

// Start and end date to filter collections
var startDate = '2019-01-01'; //YYY-MM-DD
var endDate = '2019-12-31'; // YYY-MM-DD

// Maximum cloud cover percentage
var cloudCoverPerc = 50;

// Map zoom level
var zoom = 5;

// Bands for visualization
var visParamL8 = {
  bands: ['B4','B3','B2'], // R, G, B
  min: 0, // minimum spectral value
  max: 2000 // maximum spectral value
  };

var visParamS2 = {
  bands: ['B11','B8','B2'], // SWIR 1, NIR, Blue
  min: 0, // minimum spectral value
  max: 0.6 // maximum spectral value, scaled
};

// Focal mean parameters
var radius = 1.5;
var kernelType = 'square';
var units = 'pixels';
var iterations = 2;
```

### 6.2 Cambodia

In the scripts `1_Landsat_Sentinel2_Median` or `3_Landsat_Medoid`, simply change `'Colombia'` in line 15 (or in the appropriate line in case it's your own script) to `'Cambodia'  ` and click *Run*.

```javascript
var country = lsib.filterMetadata('country_na','equals','Cambodia');
```

In the script `2_Landsat_Sentinel2_Median2`, simply change `'Colombia'` in line 12 (or in the appropriate line in case it's your own script) to `'Cambodia'` and click *Run*. The script called `Cambodia` mentioned in Section 1.2. Repository is an exact copy of this script but with the change already made.

```javascript
var countryName = 'Cambodia';
```

As mentioned above in the Mozambique example, you can adjust any other user variable desired. E.g., zoom level, start and end dates, visualization parameters, and focal mean parameters.

Congratulations, you have reached the end of this module. In the next modules, you will learn how to collect training data using QGIS and GEE.

## 7 FAQs

**Why are we using [LSIB Simplified](https://developers.google.com/earth-engine/datasets/catalog/USDOS_LSIB_SIMPLE_2017) and not [LSIB Detailed](https://developers.google.com/earth-engine/datasets/catalog/USDOS_LSIB_2017)?**

The more detailed a multi-polygon is, the more compute resources it needs. Because we are making computations on a national scale, we use the Simplified version to avoid runtime errors and/or delays. The usage of the Detailed version might cause an error known as `Earth Engine memory capacity exceeded` and/or cause the script to be overall slower.

**I typed 'colombia' to filter the LSIB dataset and it did not work. Why?**

The properties of a dataset are case-sensitive. The property `country_na` for the country of Colombia is a string that starts with a capital "C", therefore, you should filter the metadata by using `'Colombia'` and not `'colombia'`.

**Why use the Landsat Surface Reflectance Tier 1 product and not Tier 2?**

Tier 2 scenes adhere to the same radiometric standard as Tier 1 scenes, but do not meet the Tier 1 geometry specification due to less accurate orbital information (specific to older Landsat sensors), significant cloud cover, insufficient ground control, or other factors. You can find information about different Tiers [here](https://www.usgs.gov/media/videos/landsat-collections-what-are-tiers) and [here](https://www.usgs.gov/core-science-systems/nli/landsat/landsat-collection-1?qt-science_support_page_related_con=1#qt-science_support_page_related_con).

**Are there any issues in slow processing and visualization due to my computer processing capability and memory?**

No. Google Earth Engine is a cloud-based platform, therefore, all the processing is being done in Google's cloud, not in your local machine. All you need is an internet connection.

**I got a "Script Error" on the Console but I am not sure what it means or how it affects the script.**

Usually this "Script Error" will not affect your code. If the outputs are loaded correctly on the Console and the layers are added to the Map, you should not worry about this error. A real error that prevents the user to accomplish a result will show a message showing *what* the error is. For assistance debugging your code, please consult the [Debugging Guide](https://developers.google.com/earth-engine/guides/debugging) and the [How to get help](https://developers.google.com/earth-engine/help) weblinks available in Section 3. Google Earth Engine.



![](figures/m1.1/cc.png)  

This work is licensed under a [Creative Commons Attribution 3.0 IGO](https://creativecommons.org/licenses/by/3.0/igo/).

Copyright 2020, World Bank

This work was developed by Andrea Puzzi Nicolau under World Bank contract with GRH Consulting, LLC for the development of new- and collection of existing- Measurement, Reporting, and Verification related resources to support countries' MRV implementation.

Material reviewed by:   
Ana Mirian Villalobos, El Salvador, Ministry of Environment and Natural Resources  
Carole Andrianirina, Madagascar, National Coordination Bureau REDD+ (BNCCREDD)  
Foster Mensah, Ghana, Center for Remote Sensing and Geographic Information Services (CERGIS)  
Jennifer Juliana Escamilla Valdez, El Salvador, Ministry of Environment and Natural Resources 
Kenset Rosales, Guatemala, Ministry of Environment and Natural Resources  
Konan Yao Eric Landry, Côte d'Ivoire, REDD+ Permanent Executive Secretariat   
Paula Andrea Paz, Colombia, International Center for Tropical Agriculture (CIAT)  
Phoebe Oduor, Kenya, Regional Centre For Mapping Of Resources For Development (RCMRD) 
Raja Ram Aryal, Nepal, Forest Research and Training Centre  
Rajesh Bahadur Thapa, Nepal, International Centre for Integrated Mountain Development (ICIMOD)  
Sofia Garcia, Guatemala, Ministry of Environment and Natural Resources  
Tatiana Nana, Cameroon, REDD+ Technical Secretariat  

Attribution  
Nicolau, Andrea P. 2020. Image mosaic/composite creation for Landsat and Sentinel-2 in Google Earth Engine. © World Bank. License: [Creative Commons Attribution license (CC BY 3.0 IGO)](http://creativecommons.org/licenses/by/3.0/igo/)

![](figures/m1.1/wb.png)![](figures/m1.1/gfoi.png)