# Neural rendering enables dynamic tomography

## Motivation

X-ray computed tomography (CT) is an established method for 3d characterization of objects with applications ranging from medical imaging to industrial component inspection.
While in this project we focus on materials engineering, the developed techniques can be used in many other domains.

![Motivation](https://github.com/Neural-Xray/nerfxray/blob/main/assets/motivation.gif?raw=true)
_Left: Detailed brain CT [1]. Middle: CT of a gear with a set screw. Right: Strain inside a lattice sample._

### In-situ deformation experiments

Interrupted in-situ X-ray CT has become a prominent way to study material deformation.
For instance, the technique has been used to probe fracture behaviour of lattice materials [2] or to reveal surprising new behaviours in homogeneous materials [3].
The principle of the method is to interrupt deformation sequence and obtain a _tomogram_ at quasi-static conditions.
The acquisition of a tomogram requires the collection of many (~3000) projections and subsequent tomographic reconstruction.
The exposure time in a lab-based X-ray CT system is on the order of 1 second, therefore tomogram acquisition takes about 1 hour.
The projection acquisition is repeated at every deformation step to obtain a complete 3d spatio-temporal dataset which can be used in downstream tasks such as constitutive modelling.

![CT acquisition](https://github.com/Neural-Xray/nerfxray/blob/main/assets/insitu.gif?raw=true)
_Typical X-ray CT workflow. First data (projections from many angles) are collected and then the 3d reconstruction is calculated._

### Objective

Due to the number of projections needed for conventional tomographic reconstruction, it has not been posible to obtain 3d reconstruction of _dynamic, high-speed_ deformations.
In this work we address this limitation.
We develop a framework based on neural rendering in which we combine high-fidelity CT obtained at the start and end of deformation with few (two) simultaneous projections are taken during deformation to obtain a full 3d spatio-temporal reconstruction.

## Approach

![Illustration of framework](https://github.com/Neural-Xray/nerfxray/blob/main/assets/framework.gif?raw=true)
_In the first step, the canonical volume is trained (<img src="assets/fire.svg" alt="fire" width="12"/>). In the second step, the canonical volume is frozen (<img src="assets/snowflake.svg" alt="snowflake" width="12"/>) and the deformation field is trained (<img src="assets/fire.svg" alt="fire" width="12"/>)._

## Simulation results

### Data efficiency of neural rendering

![Data efficiency of neural rendering](https://github.com/Neural-Xray/nerfxray/blob/main/assets/efficiency.gif?raw=true)

### Accurate estimation of deformation field

![Known deformation field](https://github.com/Neural-Xray/nerfxray/blob/main/assets/simulated.gif?raw=true)

## Experimental results

### Localized deformation of Kelvin lattice

![Localizing deformation in lattice](https://github.com/Neural-Xray/nerfxray/blob/main/assets/localized.gif?raw=true)

### Deformation of randomized lattice

![Randomized lattice](https://github.com/Neural-Xray/nerfxray/blob/main/assets/randomized.gif?raw=true)

## Limitations and broader impact

[show that the struts are being squished]

## References

[1] Brain CT animation adapted from Human Organ Atlas ([doi:10.15151/ESRF-DC-572252655](http://doi.org/10.15151/ESRF-DC-572252655), [https://human-organ-atlas.esrf.eu/datasets/572252538](https://human-organ-atlas.esrf.eu/datasets/572252538)) under CC-BY-4.0 license.

[2] Shaikeea, A.J.D., Cui, H., O’Masta, M. et al. The toughness of mechanical metamaterials. Nat. Mater. 21, 297–304 (2022). [doi.org/10.1038/s41563-021-01182-1](https://doi.org/10.1038/s41563-021-01182-1).

[3] Wang, Z., Das, S., Joshi, A. et al. 3D observations provide striking findings in rubber elasticity. PNAS, 121, 24 (2024). [doi.org/10.1073/pnas.2404205121](https://doi.org/10.1073/pnas.2404205121)
