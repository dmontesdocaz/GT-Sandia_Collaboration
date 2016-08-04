---
layout:     post
title:     Development of Model
date:       2016-07-19 12:00:00
author:     David Montes de Oca Zapiain
tags: 		
---
In a previous post the bounds for the effective property side of the model to be developed were clearly identified. 
In that post it was established that as long as every contrast ratio evaluated contained a microstructure of particles aligned with the stretching direction and another one with the particles normal to the stretching direction; all the other results from the different microstructures will be contained within these 2 microstructure’s results. 


The goal, as mentioned earlier, of this project is to establish a low-dimensional structure-property linkage that allows for the fast and accurate calculation of a property of interest. 


For this project the property of interest is the yield strength of this perfectly plastic 2-phase composite. 


The surrogate model to be developed is going to take as input the 2-pt statistics of the microstructure and the contrast ratio between the 2 phases and efficiently calculate the corresponding yield strength. 


The issue is that 2-pt statistics actually increases the dimensionality of the information analyzed. 
Thus for a linkage to be established in such a high-dimensional space will be certainly impossible. Consequently the first challenge to address is to reduce the dimensionality of the 2 point statistics information. 


In order to achieve that we are going to transform the information to a new set of orthogonal axis that order the information according to its variance. 

This transformation is called Principal Component analysis and allows to reduce the dimensionality of the information by providing us with the coordinates of each set of 2-point statistics in these new orthogonal set of axis. 

Consequently now it is needed a way to bound this input space, therefore we need to analyze what factors affect it the most. 

To analyze this we generate 37 different MS.
As mentioned earlier we have 4 different classes. 
In the class consisting of ellipses we modified their orientation but kept their aspect ratio somewhat constant. 
For the MS generated using PYMKS we consistently increased the grain size.
Finally for the circular precipitates we changed its location and increased the grain size a little bit.
The graph of the 37 different MS in PC space looks the following:

![PCA plot of initial 37 MS]({{ site.url }}/GT-Sandia_Collaboration/img/post_img/img8.jpg)


From the PCA plot it can be seen that the SPPARKS MS are quite consistent and do not show much variance among themselves. 

On the other hand we see that the PYMKS generated MS have a clear distinct path in PC space, we also see that the circular precipitates are close together but then somehow space out. 


This led us to imply that the biggest effect in PC space for the 2-pt statistics are the size of the grains. 
Thus if we want to capture the extreme cases of this space we need to include the biggest precipitates possible, that keep the volume fraction constant at .5.


In order to demonstrate this last claim we generated a new MS with big elliptical grains and recalculated the PCA, the results are the following:


![PCA plot of 38 MS]({{ site.url }}/GT-Sandia_Collaboration/img/post_img/img9.jpg)


It can be clearly seen from the plot that adding this new MS with the big elliptical precipitates added this new point in PCA space farther away from the others.

Consequently besides changing the orientation and distribution of the precipitates we also need to change the size of the precipitates.

