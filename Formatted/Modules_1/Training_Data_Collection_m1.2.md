---
title: Training Data Collection
summary: This tutorial will demonstrate how to collect categorical training data for land cover classification using QGIS or Google Earth Engine. Users should adjust the various components to match their project objectives. Here, the process is demonstrated for the countries of Colombia, Mozambique, and Cambodia, and for a simple legend of four land cover classes - Forest, Water, Herbaceous, and Developed.
author:
- Eric Bullock
- Karis Tenneson
creation date: December, 2020
language: English
publisher and license: Copyright 2021, World Bank. This work is licensed under a Creative Commons Attribution 3.0 IGO

tags:
- OpenMRV
- Landsat
- Sentinel 2
- Planet Labs
- MODIS
- QGIS
- GEE
- Cloud cover
- Optical sensors
- High resolution
- Remote sensing
- Composite
- Mosaic
- Land cover mapping
- Forest mapping
- Sample
- Sample design
- Sampling design
- Sample selection
- Colombia
- Mozambique
- Cambodia

group:
- category: Composite (Median)
  stage: Composite creation/Pre-process
- category: Landsat
  stage: Inputs
- category: Sentinel-2
  stage: Inputs
- category: MODIS
  stage: Inputs
- category: QGIS
  stage: Training data collection
- category: GEE
  stage: Training data collection
---

# Training Data Collection

## 1 Background

Training data is instrumental to supervised image classification. The training dataset is a labeled set of data that is used to inform or "train" a classifier. The trained classifier can then be applied to new data to create a classification. For example, land cover training data will contain examples of each class in the study's legend, and based on these labels the classifier can be used to predict the most likely land cover class for each pixel in an image. This is an example of a categorical classification and the training labels are therefore categorical. By contrast, a continuous variable (e.g. percent tree cover) can be predicted using continuous training labels.

This tutorial will demonstrate how to collect categorical training data for land cover classification using QGIS or Google Earth Engine. Users should choose the option that they are more familiar with (QGIS or Google Earth Engine), and should adjust the various components to match their project objectives. Here, the process is demonstrated for the countries of Colombia, Mozambique, and Cambodia, and for a simple legend of four land cover classes: Forest, Water, Herbaceous, and Developed.  

### 1.1 Tutorials

* For training data collection using **QGIS** please refer to process "Training Data Collection" and tool "QGIS" here on OpenMRV
* For training data collection using **Google Earth Engine**, please refer to process "Training Data Collection" and tool "GEE" here on OpenMRV

-----

![](figures/m1.1/cc.png)  

This work is licensed under a [Creative Commons Attribution 3.0 IGO](https://creativecommons.org/licenses/by/3.0/igo/).

Copyright 2021, World Bank

This work was developed by Eric Bullock and Karis Tenneson under World Bank contract with GRH Consulting, LLC for the development of new- and collection of existing- Measurement, Reporting, and Verification related resources to support countries' MRV implementation.

Attribution  
Bullock, E., Tenneson, K. 2021. Training Data Collection. © World Bank. License: [Creative Commons Attribution license (CC BY 3.0 IGO)](http://creativecommons.org/licenses/by/3.0/igo/)

![](figures/m1.1/wb_fcfc_gfoi.png)
