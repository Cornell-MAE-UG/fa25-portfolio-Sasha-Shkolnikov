---
layout: project
title: "Wind Turbine Blade Design Project"
description: "Constrained Blade Optimization"
technologies:
  - MATLAB
  - Wind Tunnel
  - LabView
image: /assets/images/Wind-Turbine-Cover-Photo.jpeg

---



**Overview:** The MAE 4272 Blade Design Project encompassed designing wind turbine blades and testing their power output in a wind tunnel. 

**Design Process:** Our group had to determine the operating condition at which to optimize the blades for: airfoil, chord, and pitch. We designed for the expected value of the wind speed distribution, and validated against the highest expected wind speed (Figure 1). We chose the NACA 4412 as a high performing airfoil, and set the best Cl/Cd ratio as the target AoA that our pitch at each blade section would try to achieve. For geometry simplification, the chord was linearly tapered (Figure 2). Before testing in the real tunnel, our design's performance was simulated using basic blade element momentum and beam beanding theory. We also modeled the moment required by the torque break to ensure it would not fail under high loading (Figure 4).

<figure style="text-align:center;">
  <img src="{{ '/assets/images/wind-distribution.png' | relative_url }}" 
       alt="Figure 1: Wind Distribution"
       style="width:125%; max-width:600px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    Figure 1: Wind Speed Distribution
  </figcaption>
</figure>


<figure style="text-align:center;">
  <img src="{{ '/assets/images/blade-cad.png' | relative_url }}" 
       alt="Figure 2: Blade CAD Model"
       style="width:125%; max-width:600px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    Figure 2: Blade CAD Geometry
  </figcaption>
</figure>

<figure style="text-align:center;">
  <img src="{{ '/assets/images/physical-blade.png' | relative_url }}" 
       alt="Figure 3: Physical Blade"
       style="width:125%; max-width:600px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    Figure 3: Physical Blade
  </figcaption>
</figure>



<figure style="text-align:center;">
  <img src="{{ '/assets/images/blade-simulation.png' | relative_url }}" 
       alt="Figure 3: Blade Performance Simulation"
       style="width:125%; max-width:600px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    Figure 4: Theoretical Power and Loading Predictions
  </figcaption>
</figure>

**Testing Process:** We tested our blade at a variety of wind speed and rotation rate combinations, by varying the torque break's input voltage as well as the wind tunnel fan frequency, to generate several power curves for analysis (Figure 4). Each voltage corresponded to a different equilibrium rotation rate, and each fan frequency corresponded to a different air-speed. Our theoretical predictions had the same general velocity-cubed dependence, but overestimated the power produced by approximately three-fold. It also significantly underestimated the free-spin rate. We attribute the power overestimation partially to the lack of friction in our model, and the discrepency more generally to setting a single value for the linear induction factor.

<figure style="text-align:center;">
  <img src="{{ '/assets/images/ExperimentalVSTheoretical.png' | relative_url }}"
       alt="Figure 4: Theoretical vs Experimental Power Curves"
       style="width:125%; max-width:600px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    Figure 4: Theoretical vs Experimental Power Curves
  </figcaption>
</figure>

**Contributions:** I contributed to the operating condition determination, worked extensively on the blade simulation and validation in Matlab, and helped operate the wind tunnel during the testing phase. 


