---
title: Summary of My Bachelor's Thesis
date: 2024-02-26 21:42:00 +0100
tags: [summary, thesis]
math: true
---

Heating a pair of adjoining grapes in a microwave oven can ignite the point of contact. One can easily reproduce this event with equipment in daily life and the following video records what will be seen. 

{% include embed/youtube.html id='wA4uZGRENas' %}
(be cautious! You might burn your microwave oven if you experiment yourself) 

This physical phenomenon can be explained by a type of resonance occurring in optical cavities when they are irradiated by electromagnetic waves with appropriate wavelengths. In this case, the wavelength of the microwaves in the cavities, the grapes, is approximately equal to the diameter of the grapes. Hence a class of electromagnetic resonances depending on the size and shape of the cavities, known as Morphology-Dependent Resonances (MDRs), can occur in each grape and the ignition at the point of contact of the two grapes results from the redistribution of energies in the resonating electromagnetic waves, as suggested by Khattak, Bianucci, and Slepkov in [their paper](https://doi.org/10.1073/pnas.1818350116). Their conclusion is supported by simulations and experiments and it becomes a great advance in understanding this physical phenomenon theoretically as theories like the Mie scattering can be used to predict some MDRs (more specifically, MDRs in optical cavities with a spherical shape). 

To have a general theory for the electromagnetic hotspots at the point of contact of two adjoining cavities, two major questions need to be answered. 

1. At what condition, the MDRs will occur in an optical cavity? 
2. At what condition, there will be a hotspot at the point of contact if we bring two MDRs-holding cavities together? 

The answers to these two questions are given in my bachelor's thesis.

The first question has been more or less answered by many scientists already. Indeed, it is possible to calculate the electromagnetic fields inside and outside of an optical cavity by solving Maxwell's equation with appropriate boundary conditions at the surface of the optical cavity if one applies the technique of multipole expansion. That is, by expanding a general electromagnetic field as a series of eigenfunctions to the Laplace operator $$\nabla^2$$, the boundary conditions will then be transformed into relations among the coefficients in the expansions of electromagnetic fields around the surface of an optical cavity. If the optical cavity is spherical, then the technique of multipole expansion leads to the Mie scattering theory. Although MDRs in spherical optical cavities are predictable from the Mie scattering theory, the predictions of MDRs become extremely hard when the shapes of the optical cavities are slightly deformed as they consume many computational resources. To overcome this difficulty, I have devised a new approach that performs much faster than the multipole expansion approach. Drawing from the concept of standing waves, I have the inspiration that a resonance should occur if and only if the waves in the cavities are standing waves. That means the solution $$\psi$$ to the wave equation 
$$
\begin{equation}
  (\nabla^2+k^2)\psi=0
\end{equation}
$$
should be identically zero when evaluated at the surface of the optical cavity. Indeed, this new approach does give me the following data
![Desktop View](/assets/img/fig_in_bachelor's_thesis.png)
_FEM simulations (the heatmap) compared with the numerical solutions to my approach (resonances are predicted to occur at the white line). We have simulated the average energy density in optical cavities with spheroidal shapes of different sizes (x-axis) and different aspect ratios (y-axis)._
which is consistent with the Mie scattering theory in the case of spherical optical cavities as well as the simulation in the case of spheroidal optical cavities. Therefore, my answer to the first question deeply relates MDRs with standing waves. 

The answer to the second question in my thesis is partial as the problem in the case where the optical cavities have irregular shapes is not easy. In principle, the hotspots arising at the point of contact are due to the constructive interferences of the scattered electromagnetic fields around the point of contact. It is not easy to know the scattered electromagnetic fields in general. However, in the simple case, i.e. when the optical cavities are spherical, we can learn what causes the constructive interferences from the Mie scattering theory as MDRs in a spherical optical cavity are predicted by this theory. The conclusion is that it is the radial component (perpendicular to the tangent plane of the surface of an optical cavity) of the scattered electromagnetic field that can add constructively with another at the point of contact while the tangential component always cancels with another at the same spot. Hence, it is not always true that bringing a pair of MDRs-holding cavities together will cause a hotspot at the point of contact, and a hotspot can occur only when both cavities are in a mode of MDRs with the radial component of the scattered electromagnetic field maximized at the point of contact.  
