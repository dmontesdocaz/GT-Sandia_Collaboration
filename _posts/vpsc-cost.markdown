---
layout:     	post
title:      	A study of VPSC computational cost
date:       	2015-09-14 12:00
author:     	Yang Wu, Marat I. Latypov
tags:         	
---


# Introduction

In this study we tracked the computational cost of VPSC simulations for a simple example of  a single-phase fcc polycrystalline specimen under uniaxial tensile test. We simulated the final texture under three different hardening laws and four different interaction models. The main purpose of this study was to compare the computational time between different schemes in VPSC7 and also to have a general idea of the computational cost of VPSC7.

# Constant simulation settings

To focus on the effect of the interaction scheme on the computational cost of VPSC simulations, most of the other simulation settings were kept constant. Some of their effects on the CPU time required for simulations will be considered in the next studies.

## Boundary conditions

The specimen was under uniaxial tension along $$x_{3}$$ up to $$\epsilon_{33}$$ = 100%. A Boundary Condition file was called by the main program. 
``  50   3   0.02    298.         nsteps  ictrl  eqincr  temp
* boundary conditions
    -0.5     0.0      0.0        |    vel.grad
    0.0     -0.5     0.0                   |
    0.0      0.0      1.0                  | ``
In this first set of simulations, we used the  settings from the examples of VPSC7 software. We kept the number of incremental deformation steps as 50 and the magnitude of increment imposed to achieve the final deformation as 0.02. In the next report, we will study the impact on the computational time by these parameters.

## Initial texture

Our texture was represented by a set of 5000 equal-weight random orientations, which were generated in Matlab by using [MTEX toolbox](http://mtex-toolbox.github.io/). 

## Convergence settings

Default settings given in the VPSC manual (examples) were accepted:
``*PRECISION SETTINGS FOR CONVERGENCE PROCEDURES (default values)
0.001 0.001 0.001 0.001    errs,errd,errm,errso
100 100 25     itmax:   max # of iter, external, internal and SO loops
0  2  10  2    irsvar & jrsini,jrsfin,jrstep (dummy if irsvar=0)
1              ibcinv (0: don't use <Bc>**-1, 1: use <Bc>**-1 in SC eq)``
As can be seen, 0.001 is used for the relative tolerances allowed in the convergence procedures. And the maximum number of iterations are set as follow: 
**ITMAXEXT :**  is the maximum number of iterations allowed in the convergence procedure of the loop over grain stress states.
**ITMAXINT :**  is the maximum number of iterations allowed in the convergence procedure of the loop over the overall modulus.
**ITMAXSO :**  is the maximum number of iterations associated with the *Second Order* loop.

# Variable simulation settings

In the current set of simulations, two simulation settings were variable: the hardening behavior of the material and the VPSC interaction scheme.

## Hardening behavior 

Three cases of hardening were studied (see Figure below):

- **h0 :** Perfectly plastic material: 
the most simple case, where there is no hardening (blue curve).
- **h1 :** Linear hardening:
the limit case of Voce hardening law corresponding to $$\tau_{1}^{s}=0 (red curve)$$
- **h2 :** Non-linear hardening:
high hardening rate observed at the onset of plasticity, and its decrease towards a constant hardening rate at large strains (black curve).

![enter image description here](https://lh3.googleusercontent.com/-YCOHGzVJlJs/VfVh7hWMuwI/AAAAAAAAAgE/YKe_6QSsIxk/s0/hardening.png "hardening.png")

The hardening parameters for these three cases are found in the figure above and  were fed to **FILECRYS** file as tau0x, tau1x, thet0, thet1:
``*Constitutive law
   0      Voce=0, MTS=1
   1      iratesens (0:rate insensitive, 1:rate sensitive)
   50     grsze --> grain size only matters if HPfactor is non-zero
 {110}<111> SLIP -------------------------------------------
 20                               nrsx
 1.0   0.0   0.2   0.2   0.        tau0x,tau1x,thet0,thet1, hpfac
 1.0    1.0                          hlatex(1,im),im=1,nmodes``
 This is an **h1** hardening case example. 
 
## Interaction schemes

There are 6 different interaction models provided by VPSC7 software. 
``*MODELING CONDITIONS FOR THE RUN
0              interaction (0:FC,1:affine,2:secant,3:neff=10,4:tangent,5:SO)``

**FC ** is the Taylor model, **affine**,**secant**,**neff=10**,**tangent** and **SO** are different self-consistent models.

Four cases were studied:

- **FC **
- **affine**: $$M_{ijkl}^{(r),aff}=n\gamma_{0}\sum_{s}\frac{m_{ij}^{s}m_{kl}^{s}}{\tau_{0}^s}(\frac{m_{pq}^s\sigma_{pq}^{(r)}}{\tau_{0}^{s}})^{n-1}$$
- **secant**: $$M_{ijkl}^{(r),sec}=\gamma_{0}\sum_{s}\frac{m_{ij}^{s}m_{kl}^{s}}{\tau_{0}^s}(\frac{m_{pq}^s\sigma_{pq}^{(r)}}{\tau_{0}^{s}})^{n-1}$$
- **tangent** 

These simulations were run on a personal laptop. Here is the CPU and RAM information:
Item |Description 
 ---|---
**CPU**| Intel(R) Core(TM) i7-4700MQ CPU @ 2.40 GHz 2.40 GHz
**RAM**|8.00 GB (7.72 GB Available)

# Results

The results of running the described set of simulations are given in the table below

Texture | hardening | Interaction | Stress-Strain Curve| Pole Figure|Computational time
---|---|---|---|---|---
5000 | h0 | FC |![1](https://lh3.googleusercontent.com/-OAcNiU13CkA/VfWComWjU-I/AAAAAAAAAgg/itZADvKM5QE/s0/1.png "1.png")|![1](https://lh3.googleusercontent.com/sslN37HA7i247npuasrGh_c9LtzTjWzAdOIT8K8N3lE=s0 "1.png")|2.12"
5000 | h0 | affine | ![2](https://lh3.googleusercontent.com/-DkFw4K18niI/VfWCxaan-FI/AAAAAAAAAgs/66hqu6qpy6o/s0/2.png "2.png")|![2](https://lh3.googleusercontent.com/Wd7z9hHULinrCBsVEonPdRANJ3nFXzqFRLRuy8FICHg=s0 "2.png")|10.46"
5000 | h0 | secant | ![3](https://lh3.googleusercontent.com/-JKC-QoVJV94/VfWC3hAe71I/AAAAAAAAAg4/YklDsEFlGE4/s0/3.png "3.png")|![3](https://lh3.googleusercontent.com/Ipk1AtXmX3x9APk7nu3XJgIvURfw1wg8tr2t_x0V8Ao=s0 "3.png")|4.42"
5000 | h0 | tangent | ![4](https://lh3.googleusercontent.com/9NORv9uslUFoQDCp_Sez7avDR2YjCsx3jdVWh2930QE=s0 "4.png")|![4](https://lh3.googleusercontent.com/HWfPw1UDpmisZ74kxBqMAz9cKihoSUgwgFOrVRE_qJ0=s0 "4.png")|7.11"
5000 | h1 | FC | ![5](https://lh3.googleusercontent.com/dUPWarXVMDPkMhRpjUhy4P4po09HA9bzoQF7eXmuoso=s0 "5.png")|![5](https://lh3.googleusercontent.com/xdvmLFkaabl85RIAls4Kbhb_E-8aO329fxEDZtJEmL4=s0 "5.png")|2.18"
5000 | h1 | affine | ![6](https://lh3.googleusercontent.com/7wCzgt7DhhVScakaOWYGHvx3Ez8PAkXxnVH8mR5jym0=s0 "6.png")|![6](https://lh3.googleusercontent.com/r_wNlNgfnbBiFaBR5CI6oT87gr81F-CFj53I11jzSFQ=s0 "6.png")|10.24"
5000 | h1 | secant | ![7](https://lh3.googleusercontent.com/ZMXAmX_DfDYTjaceckIR43Xf5SddfP9L52zzD8TLzuM=s0 "7.png")|![7](https://lh3.googleusercontent.com/O3aYYM-wxjWh1weKnIfOgjEL0mIGbH_KLdogeqZ0YuM=s0 "7.png")|4.40"
5000 | h1 | tangent | ![8](https://lh3.googleusercontent.com/YW_3nNEZv5qMuI7HALSVZdQxk53IP7TIEXXqQTo1NM4=s0 "8.png")|![8](https://lh3.googleusercontent.com/v74kX8_AzcvTOWta7owdtyWSRyVUyKRCEbxf7eMe_Zw=s0 "8.png")|7.13"
5000 | h2 | FC | ![9](https://lh3.googleusercontent.com/yBcE-YClrqWVdf7Alo-58QbrUbPCs2qF2o963gSt5rA=s0 "9.png")|![9](https://lh3.googleusercontent.com/4UhC8VsuSkZmKte2nqePj2ACW4Dk_e4Oby-gTCZ7HM4=s0 "9.png")|2.62"
5000 | h2 | affine | ![10](https://lh3.googleusercontent.com/MZ8ViNk5US66hD7V2p_5SnBnKhJs0-W5riu5cNdPP0w=s0 "10.png")|![10](https://lh3.googleusercontent.com/wiW1Mub4hMdJFtMLqQyL2k10qiw3F6f88dk1wRYNlhk=s0 "10.png")|10.52"
5000 | h2 | secant | ![11](https://lh3.googleusercontent.com/34pD1L_55eN322VJg1_8UpLgbfaUwy9GgIaqiFHmomc=s0 "11.png")|![11](https://lh3.googleusercontent.com/w9jBfryqJQ-2axxAlCQ5M78_Yb42drDtY_DhqpaJmPc=s0 "11.png")|6.24"
5000 | h2 | tangent | ![12](https://lh3.googleusercontent.com/ys7JANpyttcGPxX7b6wVEnQv1TbnYVeunt4Xg8Zor-E=s0 "12.png")|![12](https://lh3.googleusercontent.com/x2UZsqqijzKQAAfI0DAZnYG0dhXaSN4Iv24l2ldvtLQ=s0 "12.png")|10.21"

# Conclusions

From this first set of simulations with a simple example, we can see that the interaction model significantly affects the computational time of VPSC. If we set Taylor model computational time as a reference, Affine SC model spends five times more time than FC, Secant model spends twice time more and Tangent model spends four times more. 
From perfectly plastic to non-linear hardening material, for FC Taylor interaction model, the computational time increases from 2.12" to 2.62"; but for affine Self-Consistent interaction model, the computational time drops from 10.46" to 10.24", then increases to 10.52". Therefore, we can conclude that, for this simple uniaxial test, the hardening law barely affects the computational time.
Next, we will study the impact of other simulation settings such as equivalent strain increment, etc. Also, other Boundary Conditions will be tested.

# Appendix: Scripting

In the parametric studies as the one discussed above, handling files and running the simulations manually can be tedious and time consuming. To automate the process, a Python script was prepared, which also calculates the CPU time spent for each simulation. 

The workflow with the script was the following
a number of `vpsc.in` files were prepared with desired various simulation settings and stored in a folder.
the script  copied the vpsc.in files one by one into the working folder and submitted a VPSC simulation with each of input files.
the script calculated the CPU time required for each simulation and wrote the result into an output file (`cpuStats.out`)
the script additionally copied output texture and stress--strain files so that the results can be also checked for each simulation run.

The source code of the python script is given below. The 

{% highlight python %}

import os
import shutil
import subprocess
import timeit

# specify VPSC working folder containing vpsc7.exe
workDir = 'C:\\Users\\UserName\\Documents\\vpsc-cost'

# specify folder containing input files
inpDir = workDir + '\\in'


# define file names
dstInpFile = workDir + '\\vpsc7.in'
exeFile = workDir + '\\vpsc7.exe'
outTexFile = workDir + '\\TEX_PH1.OUT'
outStrFile = workDir + '\\STR_STR.OUT'

# create output file name for CPU time 
cpuStatFileName = workDir + '\\cpuStats.out'
cpuStatFile = open(cpuStatFileName,'w')

# start loop over all input files existing in inpDir 
for root, dirs, filenames in os.walk(inpDir):
    for f in filenames:
        inpFile = os.path.join(root, f)
                
        # copy input file from in folder to the working folder with vpsc.exe
        shutil.copyfile(inpFile,dstInpFile)
        
        # count execution time and run vpsc simulation
        startTime = timeit.default_timer()
        subprocess.call([exeFile])
        cpuTime = timeit.default_timer() - startTime
        
        # write cpu time to a file
        cpuStatFile.write(f)
        cpuStatFile.write(' - ')
        cpuStatFile.write(str(cpuTime))
        cpuStatFile.write('\n')
        
        # copy OUT files
        dstTexFile = workDir + '\\out-tex\\' + f + '-tex.out'
        dstStrFile = workDir + '\\out-str\\' + f + '-str.out'
        
        shutil.copyfile(outTexFile,dstTexFile)
        shutil.copyfile(outStrFile,dstStrFile)

# close the output file
cpuStatFile.close() 

{% endhighlight %}