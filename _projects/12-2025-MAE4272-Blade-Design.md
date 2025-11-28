---
layout: project
title: "12-2025 MAE 4272 Blade Design Project"
description: "Constrained Blade Optimization"
technologies:
  - MATLAB
  - Wind Tunnel
image: /assets/images/Wind-Turbine-Cover-Photo.jpeg

---



The MAE 4272 Blade Design Project encompassed designing wind turbine blades and testing their power output in a wind tunnel. 

Our group had to determine the operating condtion at which to optimize the blades for: airfoil, chord, and pitch. We designed for the expected value of the wind speed distribution, and validated against the highest expected wind speed (Figure 1). We chose the NACA 4412 as a high performing airfoil, and set the best Cl/Cd ratio as the target AoA that our pitch at each blade section would try to achieve. For geometry simplification, the chord was linearly tapered (Figure 2). Before testing in the real tunnel, our design's performance was simulated using basic blade element momentum and beam beanding theory. We also modeled the moment required by the torque break to ensure it would not fail under high loading (Figure 3).

<img src="{{ '/assets/images/wind-distribution.png' | relative_url }}" alt="Figure 1: Wind Distribution" style="width:60%; max-width:600px; display:block; margin:auto;">

<img src="{{ '/assets/images/blade-cad.png' | relative_url }}" alt="Figure 2: Blade CAD" style="width:60%; max-width:600px; display:block; margin:auto;">

<img src="{{ '/assets/images/blade-simulation.png' | relative_url }}" alt="Figure 3: Performance and Loading Modeling" style="width:60%; max-width:600px; display:block; margin:auto;">


We tested our blade at a variety of wind speed and rotation rate combinations, by varying the torque break's input voltage as well as the wind tunnel fan frequency, to generate several power curves for analysis. 


Testing summary: How the blades were tested and what data you analyzed

I contributed to the operating condition determination, worked extensively on the blade simulation and validation in Matlab, and helped operate the wind tunnel during the testing phase. 

Figures: Plots, CAD image, and photos 


This is how I solved the problem:

```python
    some code = 10;
    plot();
```

Aenean tincidunt aliquam arcu, in euismod dui dapibus eu. In placerat, mi et ultrices consequat, quam ligula cursus mauris, in semper neque nibh at est. Maecenas hendrerit dignissim porta. Phasellus nec fringilla dolor. Etiam efficitur nisi sit amet velit pharetra feugiat. Etiam ultrices turpis at leo semper, eleifend scelerisque neque malesuada. Aliquam molestie congue rhoncus. Donec blandit neque dolor, nec tristique mi pretium ac. Mauris tincidunt ullamcorper magna, nec pellentesque mi sagittis quis.


