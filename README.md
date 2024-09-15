# Neural rendering enables dynamic tomography

## Motivation

X-ray computed tomography (X-CT) is an established method for 3d characterization of objects with applications ranging from medical imaging to industrial component inspection.
While in this project we focus on materials engineering, the developed techniques can be used in many other domains.

![Motivation](https://github.com/Neural-Xray/nerfxray/blob/main/assets/motivation.gif?raw=true)
_Left: Detailed brain X-CT [1]. Middle: X-CT of a gear with a set screw. Right: Strain inside a lattice sample._

### In-situ deformation experiments

Interrupted in-situ X-CT has been employed to study material response to deformation:
for instance it revealed new insights into fracture behaviour of lattice materials [2] or surprising new behaviours in rubber elasticity [3].
The principle of the method is to interrupt deformation sequence at several stages and obtain a _tomogram_ at quasi-static conditions.
The acquisition of a tomogram requires the collection of many (~3000) projections and subsequent tomographic reconstruction.
The exposure time in a lab-based X-CT system is on the order of 1 second, therefore tomogram acquisition takes about 1 hour (which has to be repeated at every deformation stage).

![CT acquisition](https://github.com/Neural-Xray/nerfxray/blob/main/assets/insitu.gif?raw=true)
_Typical X-ray CT workflow. First data (projections from many angles) are collected and then the 3d reconstruction is calculated._

## Objective and approach

Due to the number of projections needed for conventional tomographic reconstruction, it has not been posible to obtain 3d reconstruction of _dynamic, high-speed_ deformations.
In this work we address this limitation.
We develop a framework based on neural rendering in which we combine high-fidelity X-CT obtained at the start and end of deformation with few (two) simultaneous projections are taken during deformation to obtain a full 3d spatio-temporal reconstruction.

![Illustration of framework](https://github.com/Neural-Xray/nerfxray/blob/main/assets/framework.gif?raw=true)
Data that is collected consists of (i) full tomography at the before deformation (t=0), (ii) 2 projections per timestep during deformation (50 timesteps here), (iii) full tomography at the end (t=1). In the first step, the canonical volume is trained (<img src="assets/fire.svg" alt="fire" width="12"/>) using a combination of projection data and X-CT reconstructions. In the second step, the canonical volume is frozen (<img src="assets/snowflake.svg" alt="snowflake" width="12"/>) and the deformation field is trained (<img src="assets/fire.svg" alt="fire" width="12"/>) using all available data.

## Key results

### Data efficiency of neural rendering

Here we reconstruct the 3d object using only 16 simulated projections.
Cross-sectional slices at the highlighted plane are shown.
Traditional X-CT algorithm (SIRT) is compared to a Neural Radiance Field (NeRF) reconstruction.
It is demonstrated that the NeRF provides a more accurate reconstruction when the number of projections is low.

![Data efficiency of neural rendering](https://github.com/Neural-Xray/nerfxray/blob/main/assets/efficiency.gif?raw=true)

### Accurate estimation of deformation field

Testing the framework with simulated data enables us to compare the predicted deformation field with the known imposed field.
The reconstructed deformation field matches the imposed field not only at t=0 and t=1 (when many projections are available), but also at intermediate timesteps.

![Known deformation field](https://github.com/Neural-Xray/nerfxray/blob/main/assets/simulated.gif?raw=true)

### Localized deformation of Kelvin lattice

We now apply the framework to two real-world experiments.
The samples are 3d printed and compression experiments are captured.
Below is the neural reconstruction of a Kelvin lattice in which the deformation is localized to a plane of defects.
The comparison of reconstructed volumes (withheld X-CT vs NeRF) at an intermediate timestep t=0.6 showns an excellent match.

![Localizing deformation in lattice](https://github.com/Neural-Xray/nerfxray/blob/main/assets/localized.gif?raw=true)

### Deformation of randomized lattice

So far we only studied samples with well-defined periodic ordering.
Here we show that the framework is also applicable to more complex microstructures with the example of a randomized Kelvin lattice.
Below is the comparison of X-CT and NeRF reconstruction.
The lack of periodic ordering is visible in the detailed insets.
The surface deviations between the withehld X-CT and NeRF reconstruction at t=0.6 show an excellent match within 150 μm  (n.b. the resolution of the scans is 75 μm ).

![Randomized lattice](https://github.com/Neural-Xray/nerfxray/blob/main/assets/randomized.gif?raw=true)

## Limitations and broader impact

The two-component framework based on the canonical model and deformation field is limited to capturing topology-preserving deformations.
While this is sufficient for many applications, there are deformations which break topology such as fracture.
For such deformations a more expressive framework should be used.

The presented framework has the potential to achieve a paradigm shift in dynamic in-situ experiments visualized by X-ray.
Up until now, it was only possible to study materials in 3d under quasi-static conditions.
Using a framework such as the one we showcased here, it will be possible to develop experiments where high-speed dynamic behaviour of materials is studied in 3d for the first time.

## References

[1] Brain CT animation adapted from Human Organ Atlas ([doi:10.15151/ESRF-DC-572252655](http://doi.org/10.15151/ESRF-DC-572252655), [https://human-organ-atlas.esrf.eu/datasets/572252538](https://human-organ-atlas.esrf.eu/datasets/572252538)) under CC-BY-4.0 license.

[2] Shaikeea, A.J.D., Cui, H., O’Masta, M. et al. The toughness of mechanical metamaterials. Nat. Mater. 21, 297–304 (2022). [doi.org/10.1038/s41563-021-01182-1](https://doi.org/10.1038/s41563-021-01182-1).

[3] Wang, Z., Das, S., Joshi, A. et al. 3D observations provide striking findings in rubber elasticity. PNAS, 121, 24 (2024). [doi.org/10.1073/pnas.2404205121](https://doi.org/10.1073/pnas.2404205121)
