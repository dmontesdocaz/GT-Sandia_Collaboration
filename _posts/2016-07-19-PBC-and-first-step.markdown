---
layout:     post
title:     PBC and First Steps
date:       2016-07-19 12:00:00
author:     David Montes de Oca Zapiain
tags: 		
---
The objective of this project is to establish a process structure linkage between a 2 phase composite and a property associated with damage. 

The first step in every data-driven model consists in generating a calibration set on which the sample space is thoroughly sampled for it to be able to establish a robust linkage.


Sandia National lab has kindly provided with various simulations obtained from SPPARKS. These simulations model the grain growth of a 2D 1000x1000 pixel microstructure, this results in a polycrystal. 

Thus the first task addressed is to be able to obtain a 2 phase composite from the data-sets received from Sandia. This task was accomplished by randomly mapping the grain ids associated with the polycrystal to just 2 different ones. 

The results look the following:

![Polycrystal to 2-phase Composite]({{ site.url }}/GT-Sandia_Collaboration/img/post_img/img1.jpg)

Now that a protocol has been established that allows us to systematically obtain 2 phase composites from the data-sets provide to us, it is necessary to determine the parameters of the Finite Element simulations on which the linkage is going to be calibrated on. 


It was decided to model the plastic deformation of a perfectly plastic high modulus material. The reason to select a high modulus is to ensure that the effects of the elastic strains are negligible, since their magnitude compared to the total strain will be infinitesimal. 


Since it is desired to use the established linkage for a wide variety of microstructures is necessary to invoke the concept of Representative Volume Elements. The main idea of this concepts consist of using a statistical representation of a large volume via a smaller statistically equivalent one.


In order for this assumption to be used the establishment of Periodic Boundary Conditions is imperative. With the implementation of this boundary conditions it can be successfully simulated with a small volume the effects of a boundary condition in an infinite medium. 


Consequently the first step that needs to be taken is to ensure that Periodic Boundary Conditions are set up correctly for the perfectly plastic simulations we intend to perform. These boundary conditions are implemented using the following equation:


![PBC equation]({{ site.url }}/GT-Sandia_Collaboration/img/post_img/img2.jpg)

It is important to mention that this equation is for the specific case where the microstructure is being pulled in the sample “X” direction. Nevertheless its concept can be expanded to any of the orthogonal directions in which the simulation is pulled. 

Applying these constraints to our input files allowed us to correctly implement the Periodic Boundary Conditions, this can be verified by applying a macroscopic strain to a homogenous microstructure and the resulting strain field must be homogenous as well, without not hot-spots.

From the following picture it can be observed that since these hotspots do not appear these Boundary Conditions were successfully applied.


![Homogenous PBC ]({{ site.url }}/GT-Sandia_Collaboration/img/post_img/img3.jpg)
