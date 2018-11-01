---
title:  "Information theory in MEG: Physics Foundations for Source Space Encoding"
author:
date:   2018-10-16
---

Zachary Bednarke presented his work.

UW Neuroinformatics SIG 10/30/18

Zachary Bednarke
Information theory in MEG: Physics Foundations for Source Space Encoding

What is MEG?
- Non-invasive ST imaging of brain imaging (discretized mag field distribution, reconstruct underlying current)
- Pre-surgical mapping, epilepsy
- Neuromagnetic field=Post-synaptic potentials from neurons (primarily cortex), perpendicular to EEG
- Used for resting state studies, connectivity analysis, neurofeedback, infant studies
Getting MEG Ready for Traditional Neuro IT Goals
- Combining physics with info theory, establishing set of basis functions ideal for processing multichannel magnetic field data.
- Portable MEG: wearable source-space BCI, UW/Sandia Deep Brain Array
Roots of Zach’s Work
- Channel Capacity: specific ROI, max # of messages transmitted via sensor array?
- Optimal Encoding: Achieve same DOF as from PCA but w/physical interpretation of importance hierarchy→ get to principled approach to encoding brain function
Physics Foundations for Source Space Encoding
- B(mag field vector space), J (current VS) field microstates: info capacity of Shannon
- Lossless compression of magnetic field signal: Vector Spherical Harmonics basis in lieu of PCA
Vector Spherical Harmonics
- 3D vector of mag field coords fed into VSH fxns. Hierarchical in angular, radial complexity--lost if you decomposed w/fourier space.
- Lowest number of model parameters that explains data = low-variance estimators for J
- Transform to VSH space from sensor space is stable
- Natural basis of special functions for solutions to Maxwell equations
Total Information Extracted from MEG
- Minimize bit error in transmission of message (inverse problem)
- Calculate I(input, output) for multichannel MEG
- Measure noise covariance (Probability Density Fxn), calc confidence interval of delta x
- Divide input space volume by uncertainty volume = # mutually distinguishable messages
Proof of Lossless Compression w/ 70 DOF
Long term goals
- Estimate bandwidth of brain ROIs for SS BCI
- Sampling theory for VSH: Device design at Sandia (optimal placement)
- We may not need MRIs for babies (only get L of 4 or 5)


