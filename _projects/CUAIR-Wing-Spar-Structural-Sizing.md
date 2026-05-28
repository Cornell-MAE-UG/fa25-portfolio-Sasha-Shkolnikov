---
layout: project
title: "Structural Wing-Spar Sizing (CUAir)"
description: "Wing-Spar Stress Analysis"
technologies:
  - ANSYS
  - Matlab
  - Solidworks CAD
image: /assets/images/Spar-Cover.png

---
<br><br><br><br><br><br><br>
<details open>
  <summary><strong>Overview</strong></summary>

  <br>

  The wing spars are the primary load-bearing structure of the airframe, transferring the lift produced by the wings to the rest of the aircraft. They experience substantial stresses and must be sized appropriately to optimize strength and weight. In the context of our student project team’s competition aircraft, careful spar selection is critical to meet performance requirements while minimizing weight for maximum efficiency and competitiveness.


</details>

---

<details>
  <summary><strong>Hand Calculations</strong></summary>

  <br>

  The load distribution was interpolated from a vortex-lattice-method derived lift distribution integrated over the wing span. The real airframe uses two spars in the midsection of the wing, and one in the outer section, however, due to unknown relative load distribution, the spars were modeled as a single inner cantilever beam connected to an outer beam. 

  <br>

<figure style="text-align:center; margin: 2rem 0;">
  <img src="{{ '/assets/images/Spar-Lift-Distribution.png' | relative_url }}"
       alt="Figure 1: Spar Lift Distribution"
       style="width:125%; max-width:600px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    Figure 1: Lift (Load) Distribution on Spar
  </figcaption>
</figure>

  <br>

  <figure style="text-align:center; margin: 2rem 0;">
  <img src="{{ '/assets/images/Spar-HandCalc-Setup.png' | relative_url }}"
       alt="Figure 2: Spar Set-up"
       style="width:125%; max-width:600px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    Figure 2: System Model for Hand Calculations 
  </figcaption>
</figure>

<br>

  Several spar cross-sectional geometries were analyzed, including an I-beam, Circle, and Square shape. A square spar was selected for the inner wing section because its higher bending moment of inertia results in lower stress, and it was significantly cheaper to procure than the lighter I-beam alternative. A circular cross section was used for the outer spar because the integrated loads are smaller and there is less internal volume available to accommodate a larger cross section.
<br>

<figure style="text-align:center; margin: 2rem 0;">
  <img src="{{ '/assets/images/Spar-Geometries.png' | relative_url }}"
       alt="Figure 3: Spar Geometries"
       style="width:125%; max-width:600px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    Figure 3: Candidate Spar Cross Sections 
  </figcaption>
</figure>

<h3>Mid-Wing Trade-Study</h3>

<table style="width:90%; border-collapse:collapse; text-align:center;">
  <tr>
    <th style="border:1px solid black;">Cross-Section</th>
    <th style="border:1px solid black;">Felt Stress</th>
    <th style="border:1px solid black;">Cost</th>
    <th style="border:1px solid black;">Weight</th>
  </tr>

  <tr>
    <td style="border:1px solid black;">I-beam</td>
    <td style="border:1px solid black; background-color:#ff6961;"><b>Prohibitive</b></td>
    <td style="border:1px solid black; background-color:#ff6961;"><b>Prohibitive</b></td>
    <td style="border:1px solid black; background-color:#c7f2c2;">Low</td>
  </tr>

  <tr>
    <td style="border:4px solid green;">Square</td>
    <td style="border:1px solid black; background-color:#ffe599;">Medium</td>
    <td style="border:1px solid black; background-color:#ffe599;">Medium</td>
    <td style="border:1px solid black; background-color:#ffb3b3;">High</td>
  </tr>

  <tr>
    <td style="border:1px solid black;">Circle</td>
    <td style="border:1px solid black; background-color:#ff6961;"><b>Prohibitive</b></td>
    <td style="border:1px solid black; background-color:#c7f2c2;">Low</td>
    <td style="border:1px solid black; background-color:#ffe599;">Medium</td>
  </tr>
</table>

<br>

<h3>Outer-Wing Trade-Study</h3>

<table style="width:90%; border-collapse:collapse; text-align:center;">
  <tr>
    <th style="border:1px solid black;">Cross-Section</th>
    <th style="border:1px solid black;">Felt Stress</th>
    <th style="border:1px solid black;">Cost</th>
    <th style="border:1px solid black;">Weight</th>
  </tr>

  <tr>
    <td style="border:1px solid black;">I-beam</td>
    <td style="border:1px solid black; background-color:#c7f2c2;">Low</td>
    <td style="border:1px solid black; background-color:#ff6961;"><b>Prohibitive</b></td>
    <td style="border:1px solid black; background-color:#c7f2c2;">Low</td>
  </tr>

  <tr>
    <td style="border:1px solid black;">Square</td>
    <td style="border:1px solid black; background-color:#c7f2c2;">Low</td>
    <td style="border:1px solid black; background-color:#ffe599;">Medium</td>
    <td style="border:1px solid black; background-color:#ffb3b3;">High</td>
  </tr>

  <tr>
    <td style="border:4px solid green;">Circle</td>
    <td style="border:1px solid black; background-color:#c7f2c2;">Low</td>
    <td style="border:1px solid black; background-color:#c7f2c2;">Low</td>
    <td style="border:1px solid black; background-color:#ffe599;">Medium</td>
  </tr>
</table>

<br>
Detailed calculations for the chosen square-circular spar combination are shown below:
<br>

<figure style="text-align:center; margin: 2rem 0;">
  <img src="{{ '/assets/images/Spar-Stress-Graph.png' | relative_url }}"
       alt="Figure 4: Spar Stress Graph"
       style="width:125%; max-width:600px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    Figure 4: Stress Distribution along Spar System
  </figcaption>
</figure>

<figure style="text-align:center; margin: 2rem 0;">
  <img src="{{ '/assets/images/Spar-Deflection.png' | relative_url }}"
       alt="Figure 5: Spar Deflection Graph"
       style="width:125%; max-width:600px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    Figure 5: Spar Deflection
  </figcaption>
</figure>

<figure style="text-align:center; margin: 2rem 0;">
  <img src="{{ '/assets/images/Spar-Deflection-Scaled.png' | relative_url }}"
       alt="Figure 6: Spar Scale Deflection Graph"
       style="width:125%; max-width:600px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    Figure 6: Spar Deflection (scaled)
  </figcaption>
</figure>




</details>

---

<details>
  <summary><strong>Material Property Estimation</strong></summary>

  <br>

  The lower end yield strength (lower than flexural strength) for the composite beams was approximated as 500 MPa using known volume fractions of the fibers and Granta material software. This was validated in later physical testing of a weaker protruded CF tube, with a flexural strength of 538 MPa. The Young’s Moduli of 44.9 GPa and 50.4 GPa, used in predicting the deflection of the square and circular beam respectively, were experimentally determined by measuring the beam deflection due to a known load: 
  <br>

  <figure style="text-align:center; margin: 2rem 0;">
  <img src="{{ '/assets/images/Spar-Deflection-Formula.png' | relative_url }}"
       alt="Figure 7: Spar Deflection Formula"
       style="width:125%; max-width:600px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    Figure 7: Equation to Find Young's Modulus
  </figcaption>
</figure>


<figure style="text-align:center; margin: 2rem 0;">
  <img src="{{ '/assets/images/Spar-Modulus-Test.png' | relative_url }}"
       alt="Figure 8: Spar Modulus Test"
       style="width:125%; max-width:600px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    Figure 8: Set-up to Find Young's Modulus
  </figcaption>
</figure>


</details>

---

<details>
  <summary><strong>ANSYS Calculations</strong></summary>

  <br>

  As a first-approach analysis, the square inner spar and circular outer spar were modeled using shell elements with large-deflection effects enabled, applying material properties representative of intermediate carbon-fiber behavior. The combined spar system was fixed at the inner root and the two spars were constrained to each other with a fully fixed (“welded”) interface, representing a simplified load transfer between sections. The model predicts a maximum deflection of approximately 8 cm, which is acceptable for the intended application. Peak stresses reached 370 MPa, a value that lies on the conservative lower end of the estimated carbon-fiber strength range (500 MPa–1 GPa). However, these stresses are likely overestimated due to localized concentrations at the spar interface and the simplified boundary conditions. With the inclusion of rib support, an aft spar, and a more representative load transfer model between the two spars, the stress distribution is expected to become more realistic and fall within acceptable limits.
  <br>

  <figure style="text-align:center; margin: 2rem 0;">
  <img src="{{ '/assets/images/Spar-ANSYS-1.png' | relative_url }}"
       alt="Figure 9: Spar ANSYS 1"
       style="width:125%; max-width:600px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    Figure 9: ANSYS Approach 1
  </figcaption>
</figure>

  
  <figure style="text-align:center; margin: 2rem 0;">
  <img src="{{ '/assets/images/Spar-ANSYS-1.2.png' | relative_url }}"
       alt="Figure 10: Spar ANSYS 1.2"
       style="width:125%; max-width:600px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    Figure 10: Results of ANSYS Approach 1
  </figcaption>
</figure>

<br>

A colleague working on the larger wing system, and who had greater familiarity with ANSYS at the time, performed a more refined analysis of the spars. By including the components involved in the spar-to-spar load transfer, as well as modeling the lift as a surface pressure on a structural wing skin, a better estimate of the maximum stress of around 300 MPa was found, with the same 8cm max deflection. This agreement in deflection supports the conclusion that the global stiffness response, and therefore the overall load path and bending behavior, was captured accurately in the initial analysis, despite limitations in local stress accuracy at the spar interface. The analysis also showed that, aside from the localized stress concentration near the spar interface, the cantilever beam model used in the hand calculations was overly conservative. A safety factor of approximately 1.7 is acceptable given the conservative nature of the model and the expectation that the number of loading cycles will remain below levels at which fatigue becomes a concern.


<figure style="text-align:center; margin: 2rem 0;">
  <img src="{{ '/assets/images/Spar-ANSYS-2.1.png' | relative_url }}"
       alt="Figure 11: Spar ANSYS 2.1"
       style="width:125%; max-width:600px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    Figure 11: ANSYS Approach 2
  </figcaption>
</figure>



<figure style="text-align:center; margin: 2rem 0;">
  <img src="{{ '/assets/images/Spar-ANSYS-2.2.png' | relative_url }}"
       alt="Figure 12: Spar ANSYS 2.2"
       style="width:125%; max-width:600px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    Figure 12: Results of ANSYS Approach 2
  </figcaption>
</figure>


</details>

---

<details>
  <summary><strong>Wing Loading Testing</strong></summary>

  <br>

  Because there were many uncertainties and simplifications involved in the above hand calculations and simulation, the integration and testing subteam fabricated a wing-loading test rig to physically test the airframe’s response to loading. At this point, the aircraft weight was higher than the figure used in initial calculations (45 lbf --> 55 lbf), so the tested g-load was modified to preserve the same overall force values (3.75g's --> 3g's). The spar system successfully passed wing-loading, though a small indentation was observed due to bearing stress where the spar contacted an adjacent component. This led to the addition of a fillet on that component to reduce local contact stresses and improve load transfer. Although the wing-loading platform did not measure internal stresses, subsequent tests on a modified airframe—with the outer wing also constructed from structural carbon fiber—showed deflections of around 11 cm, roughly matching both the hand calculations and the ANSYS predictions.

  <br>

  <figure style="text-align:center; margin: 2rem 0;">
  <img src="{{ '/assets/images/Spar-WLTR.png' | relative_url }}"
       alt="Figure 12: Spar WLTR"
       style="width:125%; max-width:600px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    Figure 13: Wing Loading Testing
  </figcaption>
</figure>
</details>

**Contributions:** 
I performed the hand calculations, spar selection, a coarse ANSYS model, CAD, and installed the spars onto the airframe.
