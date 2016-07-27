---
layout:     post
title:     Classes for Calibration Set
date:       2016-07-27 11:56:00
author:     David Montes de Oca Zapiain
tags: 		
---

The first step in every data driven model consists in clearly determining the state space from which the calibration set, used to obtain the PCA weights, is going to be obtained.  

Also the microstructure function, which is going to help us identify the different states present in the Microstructure, needs to be defined.


This microstructure function discretizes the microstructure into a uniform grid of spatial cell, voxels, then it allows us to identify the amount of one local state space inside those previously defined voxels. 


Since we are dealing with a 2-phase composite the amount of local states present are only two. It was also decided to use a specific type of microstructure gridding denominated Eulerian or binary. This type gridding only allows for only one local state to occupy a voxel, thus the values of our specified Microstructure function take a value of 0 or 1 depending on what local state occupies that voxel. 
For more information about the microstructure function and how it is defined please refer to this ([paper][paper]).

Now that the Microstructure function has been defined for our project we need to define the sample space from which the calibration set will be obtained. 
Thankfully for us the bounds for effective properties for 2-phase composites are clearly defined. 
These bounds are commonly known as Voigt and Reuss Bounds or iso-strain and iso-stress models, the following image illustrates these specific models.


![Bounds for Effective Properties for 2 Phase Composites]({{ site.url }}/GT-Sandia_Collaboration/img/post_img/img6.JPG)


This is extremely helpful for us since these models state that the results of any other simulation, varying the morphology and orientation of the precipitates in the matrix and as long as the volume fraction is kept constant, are going to be between the results of these 2 models. 

Thus by including the results of these two models for every different contrast ratio analyzed we will have successfully accounted for the extreme cases and therefore bounded the sample space. 

Consequently for us now the next step is to define the different classes of Microstructure morphology that will be analyzed in this project. 


Taking the effective composite theory into account 4 different classes are going to be evaluated for this project. It is extremely important to mention that the surrogate model that is going to be established for this project is extremely modular and allows for the inclusion of more classes and for the expansion of the calibration set in an extremely easy fashion, thus is a very scalable framework. 


The following image shows the 4 different classes to be analyzed in this project:


![Classes for Project]({{ site.url }}/GT-Sandia_Collaboration/img/post_img/img7.JPG)

The 4 class analyzed consist of:


•	Grain resembling microstructures, the size of the grains will be varied in this class.


•	Spherical Inclusions randomly inserted in the matrix.


•	2-phase Microstructures resulting from a grain growth simulation.


•	Elliptical inclusions inserted in the matrix. For this class the aspect ratio and orientation of the inclusions will be varied.

The different classes analyzed will be generated different tools:

•	The first class in the image will be generated using PYMKS 2-phase Microstructure Generator. 
For more information please visit this ([link][link]): 

•	The second and fourth class of the image will be generated using a computationally efficient Microstructure Generator, for more information about it please visit the following ([website] [website]):

•	Finally the last class will be generated using SPPARKS grain growth software.  


[paper]: https://eds.a.ebscohost.com/eds/pdfviewer/pdfviewer?sid=8c2d8243-59c3-48a8-bd67-67e2cd3c2f83%40sessionmgr4008&vid=0&hid=4208
[link]: http://materialsinnovation.github.io/pymks/datageneration.html
 [website]: http://dx.doi.org/10.1088/0965-0393/16/6/065009
 
