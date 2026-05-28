---
layout: project
title: "Wind Turbine Blade Design (MAE 4272)"
description: "Constrained Blade Optimization"
technologies:
  - MATLAB
  - Wind Tunnel
  - LabView
image: /assets/images/Turbine-Cover.png
---

<br><br><br><br><br><br><br><br>

<details open>
<summary><strong>Overview</strong></summary>

The project encompassed the design and experimental validation of wind turbine blades for MAE 4272.
</details>

<hr>

<details>
<summary><strong>Design Process</strong></summary>

Our group first determined the operating condition at which to simulate the blade geometry, including target windspeed,airfoil selection, chord distribution, and pitch schedule. The blades were designed for the expected value of the wind speed distribution of just under 5 m/s and validated against the highest anticipated wind speeds (Figure 1).

<figure style="text-align:center; margin: 2rem 0;">
  <img src="{{ '/assets/images/wind-distribution.png' | relative_url }}" 
       alt="Wind Speed Distribution"
       style="width:125%; max-width:600px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    Figure 1: Wind Speed Distribution
  </figcaption>
</figure>

The NACA 4412 airfoil was selected due to its favorable performance characteristics at an expected Reynolds Number of approximately 50000 (Figure 2). The target angle of attack at each blade section was chosen to maximize the lift-to-drag ratio (Cl/Cd), with local pitch adjusted accordingly. For geometric simplicity and manufacturability, the blade chord was linearly tapered along the span using a 1/3 tip to root ratio, informed by literature review of optimal values (Figure 3).

<figure style="text-align:center; margin: 2rem 0;">
  <img src="{{ '/assets/images/Blade-Design-Airfoil-Performances.png' | relative_url }}"
       alt="Blade Airfoil Performances"
       style="width:100%; max-width:600px; display:block; margin:0 auto;">

  <figcaption style="font-size:0.9em; color:#555; margin-top:0.75rem;">
    Figure 2: NACA 2412 (red), 4412 (brown), 6412 (blue) Performance Comparisons
  </figcaption>
</figure>


<figure style="text-align:center; margin: 2rem 0;">
  <img src="{{ '/assets/images/blade-cad.png' | relative_url }}" 
       alt="Blade CAD Geometry"
       style="width:125%; max-width:600px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    Figure 3: Blade CAD Geometry
  </figcaption>
</figure>

<figure style="text-align:center; margin: 2rem 0;">
  <img src="{{ '/assets/images/physical-blade.png' | relative_url }}" 
       alt="Physical Blade"
       style="width:125%; max-width:600px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    Figure 4: Physical Blade
  </figcaption>
</figure>

Prior to wind tunnel testing, blade performance was simulated using blade element momentum theory coupled with beam bending analysis.

 <h3><strong><br> Bending Stress Model</strong></h3> <br>


The normal force on each blade element is computed from the aerodynamic coefficients and local flow conditions:

$$
dF_N(r) = B \frac{1}{2}\rho U_{\text{rel}}(r)^2
\left[ C_L(r)\cos\phi(r) + C_D(r)\sin\phi(r) \right] c(r)\,dr
$$

where \(B\) is the number of blades, \(\rho\) is the air density, \(U_{\text{rel}}(r)\) is the relative velocity at radius \(r\), \(C_L(r)\) and \(C_D(r)\) are the lift and drag coefficients, \(\phi(r)\) is the flow angle, and \(c(r)\) is the local chord length.

The force acting on each discrete blade panel is approximated using the trapezoidal rule:

$$
F_{N,i} = \frac{1}{2}
\left( dF_{N,i} + dF_{N,i-1} \right)
\left( r_i - r_{i-1} \right)
$$

The bending moment at a given radial slice is obtained by summing the moments contributed by all outboard panels:

$$
M_N(r_{\text{slice}}) =
\sum_{i} F_{N,i} \left( r_i - r_{\text{slice}} \right)
$$

The resulting bending stress at the outer fiber of the blade cross-section is then computed as:

$$
\sigma = \frac{M y}{I}
$$

where \(M\) is the bending moment at the section, \(y\) is the distance from the neutral axis to the outer fiber, and \(I\) is the bending moment of inertia about the bending moment axis.

The cross-section used for neutral axis and bending moment of inertia calculations was approximated as a rectangle with the same chord and inertia as the true airfoil (Figure 5).<br>


<figure style="text-align:center; margin: 2rem 0;">
  <img src="{{ '/assets/images/Blade-Geometry-Simplification.png' | relative_url }}" 
       alt="Airfoil Geometry Simplification"
       style="width:125%; max-width:600px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    Figure 5: Airfoil Geometry Simplification
  </figcaption>
</figure> 
<br>


The torque brake loading was also modeled to verify that it would not fail under high-load conditions.



<h3><strong><br> Torque Brake Loading Model</strong></h3> <br>


The tangential force on each blade element is calculated from the aerodynamic coefficients and local flow conditions:

$$
dF_T(r) = B \frac{1}{2}\rho U_{\text{rel}}(r)^2
\left[ C_L(r)\sin\phi(r) - C_D(r)\cos\phi(r) \right] c(r)\,dr
$$

where \(B\) is the number of blades, \(\rho\) is the air density, \(U_{\text{rel}}(r)\) is the relative velocity at radius \(r\), \(C_L(r)\) and \(C_D(r)\) are the lift and drag coefficients, \(\phi(r)\) is the flow angle, and \(c(r)\) is the local chord length.

The tangential force on each discrete blade panel is approximated using the trapezoidal rule:

$$
F_{T,i} = \frac{1}{2}
\left( dF_{T,i} + dF_{T,i-1} \right)
\left( r_i - r_{i-1} \right)
$$

The total torque applied to the torque brake is obtained by summing the moments from all blade panels:

$$
M_T = \sum_i F_{T,i}\, r_i
$$

where \(r_i\) is the radial position of each blade panel.

<h3><strong><br> Theoretial Results</strong></h3> <br>

The resulting blade performance (Power and Power Coefficient), blade loading (Max Bending Stress), and torque loading (Total Torque) predictions are captured in Figure 6. <br>

<figure style="text-align:center; margin: 2rem 0;">
  <img src="{{ '/assets/images/blade-simulation.png' | relative_url }}" 
       alt="Blade Performance Simulation"
       style="width:125%; max-width:600px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    Figure 6: Theoretical Power and Loading Predictions
  </figcaption>
</figure>

</details>

<hr>

<details>
<summary><strong>Testing Process</strong></summary>

The blades were tested across a range of wind speeds and rotational rates by varying both the wind tunnel fan frequency and the input voltage to the torque brake. This approach generated multiple power curves for analysis (Figure 7).

Each torque brake voltage corresponded to a distinct equilibrium rotational speed, while each fan frequency established a different freestream velocity. While the theoretical predictions correctly captured the expected cubic dependence of power on wind speed, they overestimated the measured power output by approximately a factor of three and significantly underestimated the free-spin rotational rate.

The discrepancies are attributed in part to the exclusion of frictional losses in the model and more generally to the assumption of a single, constant linear induction factor.

<figure style="text-align:center; margin: 2rem 0;">
  <img src="{{ '/assets/images/ExperimentalVSTheoretical.png' | relative_url }}"
       alt="Theoretical vs Experimental Power Curves"
       style="width:125%; max-width:600px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    Figure 7: Theoretical vs Experimental Power Curves
  </figcaption>
</figure>

</details>

<hr>

<details>
<summary><strong>Contributions</strong></summary>

I helped determine the blade operating conditions, wrote the code to estimate the blade performance and stress analysis simulations in MATLAB, and assisted with wind tunnel operation and data collection during experimental testing.

</details>
