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

<details open>
<summary><strong>Overview</strong></summary>

<br>

This project encompassed the end-to-end design, optimization, manufacturing, and validation of aerodynamic winglets for a small unmanned aircraft. The winglets were designed to reduce induced drag associated with pressure differences on the top and bottom surfaces of the wing. They serve to improve aircraft range, and as a structural integration point for avionics, while remaining lightweight and manufacturable.

The work spanned aerodynamic theory, numerical optimization using a Vortex Lattice Method, CFD validation, CAD, prototyping, and qualification testing, culminating in a flight-ready system.

</details>

---

<details open>
<summary><strong>VLM Analysis and Optimization</strong></summary>

<br>

A vertical raked winglet configuration was selected due to its structural simplicity, ease of manufacturing, and common use on RC and UAV platforms. The winglet airfoil was fixed to the wing's NACA 6412 to reduce design complexity and ensure predictable aerodynamic behavior. Design variables included the top and bottom winglet heights, and sweep angles, constrained by manufacturing limits and printer build volume.

<figure style="text-align:center;">
  <img src="{{ '/assets/images/Winglet-Optimization-Space.png' | relative_url }}"
       alt="Winglet Design Parameters"
       style="width:100%; max-width:600px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    Winglet Design Parameters
  </figcaption>
</figure>

<p>To quantify aerodynamic performance, the  range equation for battery-powered flight was simplified into a range score:</p>

<p style="text-align:center;">
  R = E · η<sub>total</sub> · (1/g) · (L/D) · (m<sub>battery</sub>/m)
</p>

<p style="text-align:center; font-size:1.2em; line-height:1.5;">
  Range Score = L / (D · m)
</p>


<br>

For the initial optimization process, the Tornado Vortex Lattice Method solver was used. Tornado is a MATLAB-based VLM tool similar to AVL, but allows direct modification of the source code. The solver was automated by removing interactive geometry prompts and enabling programmatic geometry generation, allowing constrained nonlinear optimization to be performed efficiently.

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

Winglet mass was explicitly included in the optimization. Winglet volume was computed analytically using fitted airfoil equations and triple integrals, with mass estimated based on material density and infill percentage.

<table style="width:50%; border:1px solid #000; border-collapse:collapse; text-align:center;">
  <tr>
    <th>Design Variable</th>
    <th>Value</th>
  </tr>
  <tr><td>Top Height</td><td>0.11 m</td></tr>
  <tr><td>Top 1/4 Sweep Angle</td><td>1.03 rad</td></tr>
  <tr><td>Bottom Height</td><td>0.10 m</td></tr>
  <tr><td>Bottom 1/4 Sweep Angle</td><td>0.60 rad</td></tr>
</table>

<br>

<table style="width:50%; border:1px solid #000; border-collapse:collapse; text-align:center;">
  <tr>
    <th>Metric</th>
    <th>Value</th>
  </tr>
  <tr><td>Predicted Range Increase</td><td>≈ 20%</td></tr>
  <tr><td>Estimated Winglet Mass</td><td>≈ 300 g</td></tr>
</table>

<br>

VLM solvers do not consider viscous drag; therefore results were treated qualitatively and refined using ANSYS Fluent.

</details>

---

<details open>
<summary><strong>Refined Analysis using ANSYS CFD</strong></summary>

<br>

1. Simplified wing geometry  <br>
2. Computational enclosure: 5× chord upstream, 10× downstream and laterally  <br>
3. FMG grid initialization  <br>
4. Local curvature and edge mesh refinement  <br>
5. 1° incidence via freestream direction  <br>
6. Updated system mass from prototype: 0.175 kg

<hr>

<p style="text-align:center; font-weight:600; margin: 1rem 0;">
  ANSYS Results
</p>

<table style="width:80%; border:1px solid #000; border-collapse:collapse; text-align:center; margin: 0 auto;">
  <tr>
    <th>Configuration</th>
    <th>Lift (N)</th>
    <th>Drag (N)</th>
    <th>Mass (kg)</th>
    <th>Range Score</th>
  </tr>
  <tr>
    <td>Winglet-less</td>
    <td>218.5</td>
    <td>11.98</td>
    <td>23.28</td>
    <td>0.7835</td>
  </tr>
  <tr>
    <td>Winglet design</td>
    <td>244.6</td>
    <td>12.96</td>
    <td>23.455</td>
    <td>0.805</td>
  </tr>
</table>

<p style="text-align:center; font-size:0.9em; color:#555; margin-top:0.5rem;">
  <strong>Percent improvement in range/range score: 2.7%</strong>
</p>

<hr>


<figure style="text-align:center;">
  <img src="{{ '/assets/images/Winglet-ANSYS.png' | relative_url }}"
       alt="Winglet ANSYS Visual"
       style="width:100%; max-width:600px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    ANSYS visualization showing wingtips disturbing vortices
  </figcaption>
</figure>

</details>


---

<details>
<summary><strong>Manufacturing and Integration</strong></summary>

<br>

Multiple prototypes were fabricated to refine tolerances and explore material options:
<br>



<figure style="text-align: center; margin: 2rem 0;">
  <img src="{{ '/assets/images/Winglet-Prototype-3D-Printed.png' | relative_url }}"
       alt="PLA Prototype"
       style="width:100%; max-width:600px; display:block; margin: 0 auto;">
  <figcaption style="margin-top: 0.5rem;">
    Fully 3D Printed PLA Prototype
  </figcaption>
</figure>


This prototype was very sturdy, however it was too heavy to be integrated into the aircraft, which was already nearing the 55lbf FAA limit.
<br>

<figure style="text-align: center; margin: 2rem 0;">
  <img src="{{ '/assets/images/Winglet-Prototype-PLAAero.png' | relative_url }}"
       alt="PLA Aero Prototype"
       style="width:100%; max-width:600px; display:block; margin:auto;">
  <figcaption>3D Printed PLA Aero Aerodynamic Section</figcaption>
</figure>

This prototype was much lighter, but the PLA Aero proved to be very brittle, and when attempting to sand it down to reduce the roughness, the layer lines would simply seperate.
<br>

<figure style="text-align: center; margin: 2rem 0;">
  <img src="{{ '/assets/images/Winglet-Hybrid-Prototype.png' | relative_url }}"
       alt="Hybrid Prototype"
       style="width:100%; max-width:600px; display:block; margin:auto;">
  <figcaption>Hybrid 3D Printed / Foam Prototype</figcaption>
</figure>

After flattening the bottom airfoil of the winglet to eliminate the negative geometry required by the 3-axis CNC machine, this configuration proved to be the ideal solution. The bottom airfoil was then refined with light sanding, which was significantly easier in foam than in PLA. The 3D-printed section added minimal weight while serving an important structural role, supporting both the antenna receivers and the live-feed camera, as well as tolerating the stress of scrweing the winglets into the wing.

</details>

---

<details>
<summary><strong>Stress Calculations and Testing</strong></summary>

<br>

<table style="width:95%; border:1px solid #000; border-collapse:collapse; text-align:center;">
  <tr>
    <th>Failure Mode / Location</th>
    <th>Calculation</th>
    <th>Stress (MPa)</th>
    <th>Allowable Strength</th>
    <th>Margin</th>
  </tr>

  <tr>
    <td>Screw Shear (2× M4, minor diameter)</td>
    <td>P / 2A</td>
    <td>0.36 MPa</td>
    <td>414 MPa (steel, shear)</td>
    <td>✓✓✓</td>
  </tr>

  <tr>
    <td>Bearing Stress on 3D Print</td>
    <td>P / (D·t)</td>
    <td>0.50</td>
    <td>~50 MPa (PLA, compressive)</td>
    <td>✓✓</td>
  </tr>

  <tr>
    <td>Shear Tear-Out in 3D Print</td>
    <td>F / (2·e·t)</td>
    <td>0.69</td>
    <td>~22 MPa (PLA, shear)</td>
    <td>✓✓</td>
  </tr>

  <tr>
    <td>Bearing Stress on Winglet Connector</td>
    <td>P / (D·t)</td>
    <td>1.10</td>
    <td>50–100 MPa (Nylon CF)</td>
    <td>✓✓</td>
  </tr>

  <tr>
    <td>Rib / Skin Interface Shear</td>
    <td>P / (C·t)</td>
    <td>0.054</td>
    <td>≥7 MPa (Epoxy)</td>
    <td>✓✓✓</td>
  </tr>

  <tr>
    <td>Rib / Winglet Connector Interface Shear</td>
    <td>P / A</td>
    <td>0.245</td>
    <td>≥7 MPa (Epoxy)</td>
    <td>✓✓✓</td>
  </tr>
</table>

<p style="font-size:0.9em; color:#555;">
A conservative 10 lbf applied load, well above expected aerodynamic drag, shows all failure modes operating at stresses at least an order of magnitude below material limits.
</p>

<figure style="text-align:center;">
  <img src="{{ '/assets/images/Winglet-Shear-Test.png' | relative_url }}"
       alt="Winglet Shear Test"
       style="width:100%; max-width:600px; display:block; margin:auto;">
  <figcaption>Applied shear load during qualification testing</figcaption>
</figure>

During test flights, it was observed that the winglet connectors would occasionally shear off the wing, particularly in cold weather when the epoxy became brittle. To address this issue, the screws were lengthened and extended into the wing rib, further constraining the sliding motion that could otherwise lead to shear failure.


</details>


---

<details>
<summary><strong>Finished Product</strong></summary>

<br>

<figure style="text-align:center;">
  <img src="{{ '/assets/images/Winglets-Final-Photo.png' | relative_url }}"
       alt="Winglets Installed"
       style="width:100%; max-width:600px; display:block; margin:auto;">
  <figcaption>Winglets installed on aircraft during competition</figcaption>
</figure>

</details>

---

<details>
<summary><strong>Contributions</strong></summary>

<br>

I led the project through the full design cycle from ideation through integration. I am grateful for guidance from Dr. Rajesh Bhaskaran on ANSYS simulation procedures and for manufacturing support from Vincent Chicone, who CNC-machined the foam winglet sections.

</details>
