## 1.0 Background on change detection

The goal of image-based change detection is to identify and map when and where interesting changes happen on the Earth's surface.  The methods described in the following sections of this module (LandTrendr, CCDC, and CODED) all rely on a simple principle to do this:  Change on the surface is expected to cause a change in the spectral reflectance that is distinct enough that it can be captured by an algorithm. 

Implicit in the goal of change detection are several issues that users should consider as they embark on a change detection exercise.  

First, the definition of what makes a change "interesting" depends on the goal of a project.  For a project focused on detecting forest change and degradation, the interesting change on the surface is removal of or damage to trees.  Less interesting are things such as phenological change, vigor changes associated with year-to-year rainfall variation, or the conditions of the atmosphere above the forest.  

Second, the definitions of "when" and "where" a change is mapped depend on the sensor and algorithm configuration.  The temporal resolution to identify change using optical sensors is constrained by the sensor repeat cadence and cloud cover conditions near the surface.  Additionally, the depth of historical imagery imposes a limit on the first time that change can be tracked.  The "where" of change mapping depends on the spatial resolution of the sensor.  If the sensor spatial resolution is large relative to the footprint of the change process of interest, the actual area mapped as change may by a relatively poor rendering of the actual surface change. Consider mapping the building of a new road into a forest with the the 30 by 30m pixels common in Landsat imagery:  While the spectral properties of a road much narrower than 30m may still make it apparent that the pixel has changed, the area of that change cannot be resolved to units smaller than the size of the whole pixel.  

A basic understanding of the spectral underpinnings of change will aid users in interpreting how these factors are handled by the different change algorithms that follow. 

### 1.1  Change is movement in spectral space

The core concept of spectral-based change detection is that movement in spectral space corresponds to change in conditions on the ground.  As described in the landcover classification module earlier,   "spectral space" is the *n*-dimensional data space defined by the reflectance measured in different spectral bands.  Materials with different spectral signatures occupy different parts of this spectral space.  A change in location in this spectral space implies that the spectral signature has changed, and thus that the material itself (the conditions that define the spectral signature) has somehow changed.  

Thus, a pixel that begins in one portion of spectral space at time 1 and moves to a different part of spectral space at time 2 is implied to have changed surface condition.  If we simply compare the location in spectral space of a pixel at two different times, we can determine if change has occurred. 

![change_in_spectral_space](./figures/intro/change_in_spectral_space.png)

### 1.2 Uninteresting change causes movement in spectral space

Unfortunately, pixels can move their location in spectral space for reasons other than those of interest to the user.  For example, atmospheric conditions at the time of acquisition of imagery may cause the entire spectral space to shift. If the numeric position in the spectral space is used to define movement and thus change, then all of the pixels in the image will be considered change.  Unless we are interested in atmospheric effects, we hope to develop an algorithm that distinguishes this uninteresting change from actual change occurring on the ground. 



![atmospheric_effects](./figures/intro/atmospheric_effects.png)



Similarly, if vegetation has a phenological change in reflectance, a pixel will exhibit motion in spectral space.   Most pixels will also exhibit some motion in spectral space because of change in sun angle or illumination.  

### 1.3 Separating interesting and uninteresting change

The more we understand a pixel's motion in spectral space under "normal conditions", the better we can determine when something interesting happens.  The motion under normal conditions can be visualized as "random motion" in the spectral space.  When a pixel emerges from that region of normal motion into a different portion of spectral space, we have greater evidence that something interesting has happened to it. 

![random_vs_interesting_movement](./figures/intro/random_vs_interesting_movement.png)



The three algorithms described in subsequent sections all leverage this latter concept to recognize when an interesting change has occurred.  