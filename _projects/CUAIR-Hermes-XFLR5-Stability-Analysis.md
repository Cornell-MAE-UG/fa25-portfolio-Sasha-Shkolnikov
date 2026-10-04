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
<summary><strong>Fuselage Modeling via ANSYS-Derived Drag</strong></summary>

<br>

XFLR5's VLM solver can't take in or mesh complex fuselage CAD, it really only handles lifting surfaces like the wing and tail. So instead of approximating the fuselage as some crude lifting body, I treated it as a non-lifting drag object defined by a Cd and reference area, pulling that Cd from a CFD study I had already run on the actual fuselage in ANSYS Fluent.

That study resolved the wake behind the fuselage in some detail, velocity recombining at 0.05, 0.2, and 0.35 m aft of the body, the low-pressure separation region, and the vorticity spinning off around it. That's what informed how I sized the body-of-influence refinement region, about 1.5 body-lengths downstream and 0.5 upstream, before pulling a Cd out of it.

<figure style="text-align:center;">
  <img src="{{ '/assets/images/ANSYS-Fuselage-Wake-Vectors.png' | relative_url }}"
       alt="ANSYS velocity vector field showing fuselage wake"
       style="width:100%; max-width:700px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    Velocity vector field around the fuselage, the extended low-velocity wake shows why the BOI needed to reach at least ~1.5 body-lengths downstream and ~0.5 upstream to fully capture it
  </figcaption>
</figure>

To make sure the Cd wasn't just an artifact of one meshing choice, I ran a sensitivity check across a few combinations of surface and volume sizing, curvature resolution, boundary layers, and BOI radius:

<table style="width:95%; border:1px solid #000; border-collapse:collapse; text-align:center;">
  <tr>
    <th style="border:1px solid #000; padding:4px;">Min. Surface</th>
    <th style="border:1px solid #000; padding:4px;">Min. Volume</th>
    <th style="border:1px solid #000; padding:4px;">Curvature</th>
    <th style="border:1px solid #000; padding:4px;">Boundary Layers</th>
    <th style="border:1px solid #000; padding:4px;">Body of Influence</th>
    <th style="border:1px solid #000; padding:4px;">Cd</th>
  </tr>
  <tr>
    <td style="border:1px solid #000; padding:4px;">0.000576</td>
    <td style="border:1px solid #000; padding:4px;">0.000576</td>
    <td style="border:1px solid #000; padding:4px;">5</td>
    <td style="border:1px solid #000; padding:4px;">10</td>
    <td style="border:1px solid #000; padding:4px;">0.01</td>
    <td style="border:1px solid #000; padding:4px;">0.247</td>
  </tr>
  <tr>
    <td style="border:1px solid #000; padding:4px;">0.001</td>
    <td style="border:1px solid #000; padding:4px;">0.001</td>
    <td style="border:1px solid #000; padding:4px;">2</td>
    <td style="border:1px solid #000; padding:4px;">10</td>
    <td style="border:1px solid #000; padding:4px;">0.02</td>
    <td style="border:1px solid #000; padding:4px;">0.257</td>
  </tr>
  <tr>
    <td style="border:1px solid #000; padding:4px;">0.008</td>
    <td style="border:1px solid #000; padding:4px;">0.008</td>
    <td style="border:1px solid #000; padding:4px;">0</td>
    <td style="border:1px solid #000; padding:4px;">10</td>
    <td style="border:1px solid #000; padding:4px;">0.02</td>
    <td style="border:1px solid #000; padding:4px;">0.266</td>
  </tr>
  <tr>
    <td style="border:1px solid #000; padding:4px;">0.001</td>
    <td style="border:1px solid #000; padding:4px;">0.001</td>
    <td style="border:1px solid #000; padding:4px;">5</td>
    <td style="border:1px solid #000; padding:4px;">15</td>
    <td style="border:1px solid #000; padding:4px;">0.02</td>
    <td style="border:1px solid #000; padding:4px;">0.263</td>
  </tr>
  <tr>
    <td style="border:1px solid #000; padding:4px;">0.001</td>
    <td style="border:1px solid #000; padding:4px;">0.001</td>
    <td style="border:1px solid #000; padding:4px;">5</td>
    <td style="border:1px solid #000; padding:4px;">20</td>
    <td style="border:1px solid #000; padding:4px;">0.02</td>
    <td style="border:1px solid #000; padding:4px;">0.259</td>
  </tr>
</table>

<br>

Cd averaged 0.258 across the five runs, with a spread of about ±0.011. Worth noting this isn't a real grid convergence study, since most runs changed several meshing parameters at once instead of refining one variable at a time, so that ±0.011 is really just scatter across different reasonable meshing choices, not a formal bound. The one case where I did isolate a single variable, boundary layers at 15 versus 20 with everything else held fixed, still shifted Cd by 0.004, so the result was close to settled but probably hadn't fully converged. Given time constraints, I treated 0.258 ± 0.011 as a reasonable working estimate rather than something rigorous.

That Cd, combined with the fuselage's frontal area, got entered directly into XFLR5's fuselage drag object. This gave the stability model a drag contribution grounded in actual resolved CFD physics instead of a crude VLM approximation of the fuselage, while still keeping the fuselage non-lifting and out of the VLM mesh, which is consistent with how XFLR5 is meant to be used.

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
