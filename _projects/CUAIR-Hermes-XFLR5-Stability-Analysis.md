---
layout: project
title: "Flight Cruise Analysis (CUAir)"
description: "XFLR5 Cruise Speed and Stability Margin Analysis"
technologies:
  - XFLR5
  - Vortex Lattice Method
  - Aerodynamic Stability Analysis
image: /assets/images/XFLR5-Cover.jpg
---

<br><br><br><br><br><br>

<details open>
<summary><strong>Overview</strong></summary>

<br>

This project involved aerodynamic stability and performance analysis of the Hermes aircraft's inverted V-tail configuration using XFLR5. The goal was to characterize cruise conditions and understand the tradeoffs between static margin, cruise speed, and lift-to-drag ratio, in order to inform CG placement and incidence angle decisions for the final airframe configuration.

Two key static margin targets were analyzed—22.5% and 32.5%—corresponding to different CG positions behind the wing leading edge. Fixed wing and tail incidence angles were used throughout (4.1° wing, 2° tail), with cruise speed solved for via Type 2 (fixed-lift) analysis.

</details>

---

<details open>
<summary><strong>XFLR5 Stability Setup</strong></summary>

<br>

The analysis used a Vortex Lattice Method (VLM) model of the full Hermes geometry, including the inverted V-tail surface. The workflow combined two analysis types:

<ul>
  <li><strong>Type 2 (fixed lift):</strong> With incidence angles fixed by manufacturing, this analysis sweeps over a range of conditions and solves for the cruise velocity required to generate the required lift at each point, producing a full performance curve.</li>
  <li><strong>Type 7 (stability analysis):</strong> Run on top of the Type 2 results to identify the single stable trim point along the generated curve — the operating condition where the aircraft is statically stable and trimmed simultaneously.</li>
</ul>

This two-step approach was necessary because the fixed incidence angles removed the freedom to tune trim independently, so the stable cruise point had to be found from within the Type 2 solution space.

Key aircraft parameters from XFLR5:

<table style="width:70%; border:1px solid #000; border-collapse:collapse; text-align:center;">
  <tr>
    <th>Parameter</th>
    <th>Value</th>
  </tr>
  <tr><td>Wing Span</td><td>2.520 m</td></tr>
  <tr><td>Wing Area</td><td>0.794 m²</td></tr>
  <tr><td>Plane Mass</td><td>15.855 kg</td></tr>
  <tr><td>Wing Loading</td><td>19.974 kg/m²</td></tr>
  <tr><td>Root Chord</td><td>0.382 m</td></tr>
  <tr><td>Aspect Ratio</td><td>8.00</td></tr>
</table>

</details>

---

<details open>
<summary><strong>SM = 22.5% Analysis</strong></summary>

<br>

<figure style="text-align:center;">
  <img src="{{ '/assets/images/XFLR5-Cover.jpg' | relative_url }}"
       alt="XFLR5 Performance with SM = 22.5%"
       style="width:100%; max-width:600px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    XFLR5 Performance with SM = 22.5
  </figcaption>
</figure>

With the CG positioned at x = 0.132 m behind the wing leading edge, XFLR5 predicted a static margin of 22.5%. The aircraft trimmed at the following cruise condition:

<table style="width:70%; border:1px solid #000; border-collapse:collapse; text-align:center;">
  <tr>
    <th>Parameter</th>
    <th>Value</th>
  </tr>
  <tr><td>Cruise Speed</td><td>20.4 m/s</td></tr>
  <tr><td>Angle of Attack (fuselage ref.)</td><td>2.5°</td></tr>
  <tr><td>Lift Coefficient (CL)</td><td>0.768</td></tr>
  <tr><td>CL/CD</td><td>~21</td></tr>
</table>

<br>

The XFLR5 output plots showed stable behavior: CL increasing linearly with alpha, a slightly negative Cm slope (confirming positive static margin), and a reasonable CL/CD near the operating point. The marked cruise point (red square) fell within the stable and efficient region of the polars.

<figure style="text-align:center;">
  <img src="{{ '/assets/images/XFLR5-SM22-Polars.png' | relative_url }}"
       alt="SM 22.5% Stability Polars"
       style="width:100%; max-width:700px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    XFLR5 stability polars for SM = 22.5% (Alpha, CL, Cm, CL/CD)
  </figcaption>
</figure>

</details>

---

<details>
<summary><strong>SM = 32.5% Analysis</strong></summary>

<br>

<figure style="text-align:center;">
  <img src="{{ '/assets/images/XFLR5-SM325.png' | relative_url }}"
       alt="XFLR5 Performance with SM = 32.5%"
       style="width:100%; max-width:600px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    XFLR5 Performance with SM = 32.5
  </figcaption>
</figure>

Moving the CG forward to x = 0.1 m behind the wing leading edge increased the static margin to 32.5%, requiring a higher cruise speed to generate the same lift:

<table style="width:70%; border:1px solid #000; border-collapse:collapse; text-align:center;">
  <tr>
    <th>Parameter</th>
    <th>Value</th>
  </tr>
  <tr><td>Cruise Speed</td><td>24.8 m/s</td></tr>
  <tr><td>Angle of Attack (fuselage ref.)</td><td>−0.167°</td></tr>
  <tr><td>Lift Coefficient (CL)</td><td>0.521</td></tr>
  <tr><td>CL/CD</td><td>~21</td></tr>
</table>

<br>

The higher static margin results in a more stable aircraft, but forces cruise at a higher speed and lower CL, with reduced proximity to the optimal lift-to-drag point. Additionally, more forward CG placement can reduce elevator authority.

<figure style="text-align:center;">
  <img src="{{ '/assets/images/XFLR5-SM32-Polars.png' | relative_url }}"
       alt="SM 32.5% Stability Polars"
       style="width:100%; max-width:700px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    XFLR5 stability polars for SM = 32.5% (Alpha, CL, Cm)
  </figcaption>
</figure>

</details>

---

<details>
<summary><strong>Minimum Speed Estimation</strong></summary>

<br>

For stall speed, the lowest converged XFLR5 solution was used as a conservative minimum: <strong>18 m/s</strong>. At this condition, the local Cl distribution showed root airfoils approaching stall behavior, with the Cl polar beginning to plateau. This represents the practical lower bound for controlled flight with the fixed incidence configuration.

<figure style="text-align:center;">
  <img src="{{ '/assets/images/XFLR5-Stall-Visualization.png' | relative_url }}"
       alt="Stall Visualization at 18 m/s"
       style="width:100%; max-width:600px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    Local Cl distribution at 18 m/s — root airfoils approaching stall
  </figcaption>
</figure>

<figure style="text-align:center;">
  <img src="{{ '/assets/images/XFLR5-Cl-Polar.png' | relative_url }}"
       alt="Local Cl Polar at Stall Speed"
       style="width:100%; max-width:500px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    Local Cl polar showing stall onset at 18 m/s
  </figcaption>
</figure>

</details>

---

<details>
<summary><strong>Design Tradeoffs</strong></summary>

<br>

Given the fixed incidence angles, three paths forward were evaluated:

<table style="width:95%; border:1px solid #000; border-collapse:collapse; text-align:center;">
  <tr>
    <th>Option</th>
    <th>Tradeoffs</th>
  </tr>
  <tr>
    <td>Don't reduce cruise speed (SM = 32.5%)</td>
    <td>Decent CL/CD, but chance of poor elevator authority. Cruise speed is higher than desired.</td>
  </tr>
  <tr>
    <td>Reduce static margin (move CG back, SM = 22.5%)</td>
    <td>Slightly less statically stable, which may improve elevator authority. Allows slower cruise at better CL/CD.</td>
  </tr>
  <tr>
    <td>Fly trimmed with upward elevator deflection</td>
    <td>Enables slower cruise, but at worse CL/CD due to drag and increased alpha. Also reduces pitch-up maneuvering envelope.</td>
  </tr>
</table>

<br>

The reduced static margin approach (SM = 22.5%, CG at x = 0.132 m) was identified as the most favorable balance: slower cruise speed, better aerodynamic efficiency, and maintained trim authority without relying on sustained elevator deflection.

</details>

---

<details>
<summary><strong>Contributions</strong></summary>

<br>

I performed the XFLR5 stability analyses across both CG configurations, set up the VLM geometry and analysis types, interpreted the trim polars, and synthesized the design tradeoff comparison.

</details>
