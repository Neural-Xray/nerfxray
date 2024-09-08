# Neural rendering enables dynamic tomography

## Motivation

X-ray computed tomography (CT) is an established method for 3d charazterization of objects with applications ranging from medical imaging to industrial component inspection.
While in this project we focus on materials engineering, the developed techniques can be used in many other domains. [1]

![Motivation](https://github.com/Neural-Xray/nerfxray/blob/main/assets/motivation.gif?raw=true)

### In-situ deformation experiments

Interrupted in-situ X-ray CT has become a prominent way to study material deformation.
For instance, the technique has been used to probe fracture behaviour of lattice materials (Shaikeea) or to reveal surprising new behaviours in homogeneous materials (Wang).
The principle of the method is to interrupt deformation sequence and obtain a _tomogram_ at quasi-static conditions.
The acquisition of a tomogram requires the collection of many (~3000) projections and subsequent tomographic reconstruction.
The exposure time in a lab-based X-ray CT system is on the order of 1 second, therefore tomogram acquisition takes about 1 hour.
The projection acquisition is repeated at every deformation step to obtain a complete 3d spatio-temporal dataset which can be used in downstream tasks such as constitutive modelling.

![CT acquisition](https://github.com/Neural-Xray/nerfxray/blob/main/assets/insitu.gif?raw=true)

### Objective

Due to the number of projections needed for conventional tomographic reconstruction, it has not been posible to obtain 3d reconstruction of _dynamic, high-speed_ deformations.
In this work we address this limitation.
We develop a framework based on neural rendering in which we combine high-fidelity CT obtained at the start and end of deformation with few (two) simultaneous projections are taken during deformation to obtain a full 3d spatio-temporal reconstruction.

## Approach

[video showing the pipeline]

## Simulation results

### Data efficiency of neural rendering

### Accurate estimation of deformation field

## Experimental results

### Localized deformation of Kelvin lattice

### Deformation of randomized lattice

## Limitations and broader impact

[show that the struts are being squished]

## References
[1] Brain CT animation adapted from Human Organ Atlas ([doi:10.15151/ESRF-DC-572252655](http://doi.org/10.15151/ESRF-DC-572252655), [https://human-organ-atlas.esrf.eu/datasets/572252538](https://human-organ-atlas.esrf.eu/datasets/572252538)) under CC-BY-4.0 license.