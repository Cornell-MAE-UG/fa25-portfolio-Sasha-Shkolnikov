---
layout: project
title: "Aerodynamic Winglets"
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

<!-- Table 1: Winglet Design Variables -->
<table style="width:50%; border: 1px solid #000; border-collapse: collapse; text-align:center;">
  <tr>
    <th style="border: 1px solid #000; padding: 8px;">Design Variable</th>
    <th style="border: 1px solid #000; padding: 8px;">Value</th>
  </tr>
  <tr>
    <td style="border: 1px solid #000; padding: 8px;">Top Height</td>
    <td style="border: 1px solid #000; padding: 8px;">0.11 m</td>
  </tr>
  <tr>
    <td style="border: 1px solid #000; padding: 8px;">Top 1/4 Sweep Angle</td>
    <td style="border: 1px solid #000; padding: 8px;">1.03 rad</td>
  </tr>
  <tr>
    <td style="border: 1px solid #000; padding: 8px;">Bottom Height</td>
    <td style="border: 1px solid #000; padding: 8px;">0.10 m</td>
  </tr>
  <tr>
    <td style="border: 1px solid #000; padding: 8px;">Bottom 1/4 Sweep Angle</td>
    <td style="border: 1px solid #000; padding: 8px;">0.60 rad</td>
  </tr>
</table>

<br>

<!-- Table 2: Performance Metrics -->
<table style="width:50%; border: 1px solid #000; border-collapse: collapse; text-align:center;">
  <tr>
    <th style="border: 1px solid #000; padding: 8px;">Metric</th>
    <th style="border: 1px solid #000; padding: 8px;">Value</th>
  </tr>
  <tr>
    <td style="border: 1px solid #000; padding: 8px;">Predicted Range Increase</td>
    <td style="border: 1px solid #000; padding: 8px;">≈ 20%</td>
  </tr>
  <tr>
    <td style="border: 1px solid #000; padding: 8px;">Estimated Winglet Mass</td>
    <td style="border: 1px solid #000; padding: 8px;">≈ 300 g</td>
  </tr>
</table>

<br>

VLM Method Solvers like Tornado do not consider viscous drag, therefore the results were treated as qualitative, and the final range increase calculation was done using the higher fidelity ANSYS Fluent software. 


**Refined Analysis using ANSYS CFD:**
1. Simplified wing geometry 
2. Defined the computational enclosure: 5× chord in front, 10× chord behind, and 10× chord on the sides.  
3. Initialized Fluent solver with FMG grid.  
4. Applied local curvature and edge sizing for mesh refinement.  
5. Modeled 1° incidence angle by adjusting the relative airflow direction
6. Used a better mass estimate for the winglet system based on prototype (including screws, washers, camera, crossfire): 0.175 kg.  



<table style="width:80%; border: 1px solid #000; border-collapse: collapse; text-align:center; margin-bottom: 16px;">
  <tr>
    <th style="border: 1px solid #000; padding: 8px;">Configuration</th>
    <th style="border: 1px solid #000; padding: 8px;">Lift (L) [N]</th>
    <th style="border: 1px solid #000; padding: 8px;">Drag (D) [N]</th>
    <th style="border: 1px solid #000; padding: 8px;">Mass [kg]</th>
    <th style="border: 1px solid #000; padding: 8px;">Range Score</th>
  </tr>
  <tr>
    <td style="border: 1px solid #000; padding: 8px;">Winglet-less</td>
    <td style="border: 1px solid #000; padding: 8px;">218.5</td>
    <td style="border: 1px solid #000; padding: 8px;">11.98</td>
    <td style="border: 1px solid #000; padding: 8px;">23.28</td>
    <td style="border: 1px solid #000; padding: 8px;">0.7835</td>
  </tr>
  <tr>
    <td style="border: 1px solid #000; padding: 8px;">Winglet design</td>
    <td style="border: 1px solid #000; padding: 8px;">244.6</td>
    <td style="border: 1px solid #000; padding: 8px;">12.96</td>
    <td style="border: 1px solid #000; padding: 8px;">23.455</td>
    <td style="border: 1px solid #000; padding: 8px;">0.805</td>
  </tr>
</table>

<p>Percent improvement in range score: <strong>2.7%</strong>
<br>
 (at 25 m/s, 0° angle of attack, 1° incidence angle)</p>


Accuracy Note:
The improvement is likely underestimated, as only the wing was modeled due to computational limits. While the wing accounts for most of the aircraft’s lift, it represents only a fraction of the total drag. As a result, the relative increase in lift is larger than the relative increase in drag, so the percent change in the full aircraft’s 𝐿/𝐷 and range would likely be higher.

 


**Manufacturing and Integration:**  

Multiple prototypes were fabricated to refine tolerances and explore material options.

<figure style="text-align:center;">
  <img src="{{ '/assets/images/Winglet-Prototype-3D-Printed.png' | relative_url }}"
       alt="Winglet Prototype 1"
       style="width:100%; max-width:600px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    Fully 3D Printed Prototype
  </figcaption>
</figure>

<figure style="text-align:center;">
  <img src="{{ '/assets/images/Winglet-Prototype-Foam.png' | relative_url }}"
       alt="Winglet Prototype 2"
       style="width:100%; max-width:600px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    Foam Section of Hybrid 3D Printed/Foam Prototype
  </figcaption>
</figure>


The final winglet design was split into a structural section and an aerodynamic section. The structural portion was printed in PLA and carried all fasteners and load paths, while the aerodynamic section was produced using lightweight foam or PLA Aero. The winglet was bolted into a reinforced outer wing rib and included integrated mounting for a camera and Crossfire antenna, with internal wiring routed through the winglet.



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
