---
layout: project
title: "Aerodynamic Winglet Design"
description: "Winglet Design and Optimization"
technologies:
  - MATLAB
  - Vortex Lattice Method
  - ANSYS
  - SolidWorks CAD
  - 3D Printing
  - CNC Machining
image: /assets/images/Winglet-Cover.png
---



**Overview:**  This project encompassed the end-to-end design, optimization, manufacturing, and validation of aerodynamic winglets for a small unmanned aircraft. The winglets were designed to reduce induced drag, improve aircraft range, and serve as a structural integration point for avionics, while remaining lightweight and manufacturable. The work spanned aerodynamic theory, numerical optimization using a Vortex Lattice Method, CFD validation, CAD, prototyping, and qualification testing, culminating in a flight-ready system.

### Design Optimization Process

**Design Space:**  
A vertical raked winglet configuration was selected due to its structural simplicity, ease of manufacturing, and common use on RC and UAV platforms. The winglet airfoil was fixed to the wing's NACA 6412 to reduce design complexity and ensure predictable aerodynamic behavior. Design variables included the top and bottom winglet heights, and sweep angles, constrained by manufacturing limits and printer build volume.

<figure style="text-align:center;">
  <img src="{{ '/assets/images/Winglet-Optimization-Space.png' | relative_url }}"
       alt="Winglet Design Parameters"
       style="width:100%; max-width:600px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    Winglet Design Parameters
  </figcaption>
</figure>

<p>To quantify aerodynamic performance, the following range equation for battery-powered flight was used:</p>
<p style="text-align:center;">
R = E* &middot; η<sub>total</sub> &middot; (1/g) &middot; (L/D) &middot; (m<sub>battery</sub>/m)
</p>
Since only the % improvement in range was of interest, the range equation above was reduced to the following range score equation:
<p style="text-align:center; font-size:1.2em; line-height:1.5;">
Range Score = L / (D &middot; m)
</p>


**VLM Analysis**
For the initial optimization process, the Tornado Vortex Lattice Method solver was used, which is a MATLAB-based VLM tool similar to AVL, but allows direct modification of the source code. The solver was automated by removing interactive geometry prompts and enabling programmatic geometry generation, allowing constrained nonlinear optimization to be performed efficiently.

<figure style="text-align:center;">
  <img src="{{ '/assets/images/VLM-Sample-Graphic.png' | relative_url }}"
       alt="Winglet VLM Graphic"
       style="width:100%; max-width:600px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    Sample Winglet Geometry in Tornado VLM
  </figcaption>
</figure>

<figure style="text-align:center;">
  <img src="{{ '/assets/images/VLM-Sample-Results.png' | relative_url }}"
       alt="Winglet VLM Results"
       style="width:100%; max-width:600px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    Results for Sample Winglet Geometry in Tornado VLM
  </figcaption>
</figure>

Winglet mass was explicitly included in the optimization to prevent unrealistic aerodynamic gains. Winglet volume was computed analytically using fitted airfoil equations and triple integrals, with mass estimated based on material density and infill percentage. This enabled direct trade-offs between aerodynamic performance and weight penalty during optimization.

| Design Variable       | Value   |
|----------------------|---------|
| Top Height            | 0.11 m  |
| Top 1/4 Sweep Angle   | 1.03 rad|
| Bottom Height         | 0.10 m  |
| Bottom 1/4 Sweep Angle| 0.60 rad|

<br>

| Metric                     | Value   |
|-----------------------------|---------|
| Predicted Range Increase    | ≈ 20%   |
| Estimated Winglet Mass      | ≈ 300 g |

<br>

VLM Method Solvers like Tornado do not consider viscous drag, therefore the results were treated as qualitative, and the final range increase calculation was done using the higher fidelity ANSYS Fluent software. 


**ANSYS CFD Analysis:**
1. Simplified wing geometry created and exported as an IGES file.  
2. Imported into ANSYS and cleaned intersections using built-in tools, combining all surfaces into a single solid.  
3. Defined the computational enclosure: 5× chord in front, 10× chord behind, and 10× chord on the sides.  
4. Initialized Fluent solver with FMG grid.  
5. Applied local curvature and edge sizing for mesh refinement.  
6. Modeled 1° incidence angle by adjusting the relative airflow direction (+1° radial from standard unit circle).  

Winglet Performance Results:

| Configuration        | Lift \(L\) (N) | Drag \(D\) (N) | Mass (kg) | Range Score |
|----------------------|----------------|----------------|------------|-------------|
| Winglet-less         | 218.5          | 11.98          | 23.28      | 0.7835      |
| Winglet design       | 244.6          | 12.96          | 23.455     | 0.805       |

- Uses a better mass estimate for the winglet system based on prototype (including screws, washers, camera, crossfire): 0.175 kg.  
- Percent improvement in range score: **2.7%** at 25 m/s, 0° angle of attack, 1° incidence angle.  

A Note on Accuracy:
- The improvement is likely underestimated, as only the wing was modeled due to computational limits. While the wing accounts for most of the aircraft’s lift, it represents only a fraction of the total drag. As a result, the relative increase in lift is larger than the relative increase in drag, so the percent change in the full aircraft’s 𝐿/𝐷 and range would likely be higher.

 


**Manufacturing and Integration:**  
The winglet was split into a structural section and an aerodynamic section. The structural portion was printed in PLA and carried all fasteners and load paths, while the aerodynamic section was produced using lightweight foam or PLA Aero. The winglet was bolted into a reinforced outer wing rib and included integrated mounting for a camera and Crossfire antenna, with internal wiring routed through the winglet.

Multiple prototypes were fabricated to refine tolerances, insert placement, electronics integration, and structural robustness.

<figure style="text-align:center;">
  <img src="{{ '/assets/images/winglet-prototypes.png' | relative_url }}"
       alt="Winglet Prototypes"
       style="width:100%; max-width:600px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    Iterative winglet prototypes and material evaluations
  </figcaption>
</figure>

**Testing and Validation:**  
Final aerodynamic performance was validated using ANSYS Fluent. A simplified wing geometry was imported from SolidWorks, meshed with refinement near the winglet junction, and analyzed at a one-degree effective incidence angle. Compared to the baseline wing, the winglet-equipped configuration showed a measurable improvement in lift-to-drag ratio.

At cruise conditions, the CFD results indicated an approximately 2.7 percent increase in range score relative to the winglet-less configuration. This improvement is considered conservative due to omitted fuselage and tail effects.

<figure style="text-align:center;">
  <img src="{{ '/assets/images/winglet-cfd.png' | relative_url }}"
       alt="CFD Comparison"
       style="width:100%; max-width:600px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    CFD comparison between baseline wing and winglet-equipped configuration
  </figcaption>
</figure>

**Contributions:**  
I led the aerodynamic optimization effort, modified and automated the VLM solver in MATLAB, developed the CAD geometry, performed weight modeling, and supported CFD validation and physical prototyping. I also contributed to integration planning, manufacturing decisions, and qualification testing.
