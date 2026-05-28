---
layout: project
title: "Drivetrain Gear Generative Design(AM)"
description: "Topology-Optimized Gear via Fusion 360 and ANSYS"
technologies:
  - Fusion 360 Generative Design
  - ANSYS FEA
  - Additive Manufacturing
image: /assets/images/AM-Gear-Cover.png
---

<br><br><br><br><br><br>

<details open>
<summary><strong>Overview</strong></summary>

<br>

This project applied Fusion 360's generative design tools to produce topology-optimized gear geometries for additive manufacturing, then validated the selected design in ANSYS. The goal was to minimize mass while maintaining structural integrity under realistic gear loading, and to compare two candidate materials (Ti-6Al-4V and AlSi10Mg) across two manufacturing processes (Powder Bed Fusion and Directed Energy Deposition).

The result was a lattice-structured gear that reduced component mass by approximately 50% relative to the solid baseline, with the AlSi10Mg DED variant selected as the optimal design on the basis of mass efficiency and adequate safety factor.

</details>

---

<details open>
<summary><strong>Problem Definition</strong></summary>

<br>

The starting geometry was a standard spur gear. The generative design study was configured as follows:

<table style="width:80%; border:1px solid #000; border-collapse:collapse; text-align:left;">
  <tr><th style="padding:6px;">Parameter</th><th style="padding:6px;">Value</th></tr>
  <tr><td style="padding:6px;">Applied Load</td><td style="padding:6px;">1000 N, normal to the gear edge (single tooth)</td></tr>
  <tr><td style="padding:6px;">Constraint</td><td style="padding:6px;">Fixed on inner bore</td></tr>
  <tr><td style="padding:6px;">Preserved Geometry</td><td style="padding:6px;">Gear teeth and inner bore wall</td></tr>
  <tr><td style="padding:6px;">Symmetry</td><td style="padding:6px;">Per-tooth symmetry (loaded tooth rotates in operation)</td></tr>
  <tr><td style="padding:6px;">Materials</td><td style="padding:6px;">Ti-6Al-4V, AlSi10Mg</td></tr>
  <tr><td style="padding:6px;">Manufacturing Processes</td><td style="padding:6px;">Powder Bed Fusion (PBF), Directed Energy Deposition (DED)</td></tr>
</table>

<br>

<figure style="text-align:center;">
  <img src="{{ '/assets/images/AM-Gear-Setup.png' | relative_url }}"
       alt="Fusion 360 generative design setup showing preserved and obstacle geometry"
       style="width:100%; max-width:650px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    Fusion 360 generative design workspace — green regions are preserved geometry (teeth and bore wall); yellow is the obstacle region
  </figcaption>
</figure>

</details>

---

<details open>
<summary><strong>Generative Design Outcomes</strong></summary>

<br>

Four candidate designs were generated across two studies (Study 1 and Study 2), each producing two outcomes. All four designs produced organic lattice structures that efficiently channel load from the active tooth to the bore, while removing material from low-stress interior regions.

<figure style="text-align:center;">
  <img src="{{ '/assets/images/AM-Gear-Outcomes.png' | relative_url }}"
       alt="Four generative design outcomes shown in Fusion 360"
       style="width:100%; max-width:600px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    All four generative design outcomes — Study 1 and Study 2, Outcomes 1 and 2
  </figcaption>
</figure>

All four designs achieved safety factors greater than 3 under the applied torque load. AlSi10Mg designs saw higher stress concentrations near the inner bore and loaded tooth connections, while Ti-6Al-4V designs were significantly over-designed relative to the yield criterion.

</details>

---

<details open>
<summary><strong>Material Selection</strong></summary>

<br>

<table style="width:80%; border:1px solid #000; border-collapse:collapse; text-align:center;">
  <tr>
    <th style="padding:6px;">Metric</th>
    <th style="padding:6px;">Ti-6Al-4V (PBF / DED)</th>
    <th style="padding:6px;">AlSi10Mg (PBF / DED)</th>
  </tr>
  <tr><td style="padding:6px;">Mass (g)</td><td style="padding:6px;">149 / 147</td><td style="padding:6px;">89 / 84</td></tr>
  <tr><td style="padding:6px;">Max Stress (MPa)</td><td style="padding:6px;">70.7 / 71.5</td><td style="padding:6px;">70.8 / 78.0</td></tr>
  <tr><td style="padding:6px;">Safety Factor</td><td style="padding:6px;">12.5 / 12.3</td><td style="padding:6px;">3.39 / 3.08</td></tr>
</table>

<br>

AlSi10Mg achieves a comparable stress level at nearly 40% less mass. Although its safety factor is lower, it still comfortably exceeds the minimum requirement, making it the superior choice for mass-critical applications. The DED variant was selected for its slightly lower mass.

<figure style="text-align:center;">
  <img src="{{ '/assets/images/AM-Gear-Stress-Fusion.png' | relative_url }}"
       alt="Fusion 360 stress analysis across all four generative designs"
       style="width:100%; max-width:600px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    Fusion 360 von Mises stress distribution across all four candidate designs — stress concentrates near the bore and loaded tooth connections
  </figcaption>
</figure>

</details>

---

<details>
<summary><strong>ANSYS Validation</strong></summary>

<br>

The selected AlSi10Mg DED design was imported into ANSYS for an independent static structural analysis. ANSYS predicted a maximum von Mises stress of approximately 135 MPa — significantly higher than the 78 MPa from Fusion 360. The peak value is likely a stress singularity at a sharp geometric feature; however, a broader continuous region near the central hub also reaches elevated stress, confirming that the hub interface is the critical load path.

<figure style="text-align:center;">
  <img src="{{ '/assets/images/AM-Gear-ANSYS.png' | relative_url }}"
       alt="ANSYS von Mises stress analysis of selected AlSi10Mg DED gear"
       style="width:100%; max-width:700px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    ANSYS equivalent (von Mises) stress — max 135 MPa at hub; AlSi10Mg yield strength ≈ 270 MPa gives safety factor ≈ 2
  </figcaption>
</figure>

The discrepancy between Fusion and ANSYS results is expected given differences in mesh density, solver settings, and how each tool handles the inner bore constraint geometry.

</details>

---

<details>
<summary><strong>Mass Reduction Summary</strong></summary>

<br>

<table style="width:80%; border:1px solid #000; border-collapse:collapse; text-align:center;">
  <tr>
    <th style="padding:6px;">Material</th>
    <th style="padding:6px;">Baseline Mass (g)</th>
    <th style="padding:6px;">Optimized Mass — PBF / DED (g)</th>
    <th style="padding:6px;">Reduction</th>
  </tr>
  <tr><td style="padding:6px;">Ti-6Al-4V</td><td style="padding:6px;">287.5</td><td style="padding:6px;">149 / 147</td><td style="padding:6px;">~48%</td></tr>
  <tr><td style="padding:6px;">AlSi10Mg</td><td style="padding:6px;">173.3</td><td style="padding:6px;">89 / 84</td><td style="padding:6px;">~51%</td></tr>
</table>

<br>

Material choice drives the bulk of mass savings — AlSi10Mg's lower density eliminates roughly 50% of mass before any topology optimization is applied. The manufacturing process (PBF vs DED) has a secondary effect, contributing only a few grams of difference between variants.

</details>
