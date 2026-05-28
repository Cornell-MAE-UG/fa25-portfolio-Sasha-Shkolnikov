---
layout: project
title: "Wind Turbine Blade Optimization (MAE 4021)"
description: "Constrained Blade Optimization"
technologies:
  - MATLAB
  - ANSYS
image: /assets/images/Blade-Optimization-Cover.png



---
<br>
<br>
<br>
<br>

<details open>
<summary><strong>Overview</strong></summary>

<br>

The goal of this senior design project is to accurately simulate a standard wind turbine blade in ANSYS,
comparing its performance to previous experimental data, as well as code based on blade element momentum
theory (BEM). The BEM code is then used to optimize the standard wind turbine blade and improve its
performance.


</details>

---

<details open>
<summary><strong>Standard Blade ANSYS Simulation</strong></summary>

<br>

A high-fidelity CFD simulation was conducted in ANSYS Fluent to establish a benchmark for the standard blade's performance.  The simulation utilized a rotating reference frame to account for the blade's rotation within a stationary domain. The flow was modeled using the SST k-omega turbulence model, which is well-suited for boundary layer flows and adverse pressure gradients typical of airfoils.
A rigorous mesh convergence study was performed to determine the blade performance. The mesh was successively refined until the calculated power output showed less than a 1% change, ensuring accuracy.

<br>

<figure style="text-align:center; margin-top: 2rem;">
  <img src="{{ '/assets/images/ANSYS-Refinement-Stats.png' | relative_url }}" 
       alt="Figure 2: Standard Blade Refinement"
       style="width:125%; max-width:600px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    Figure 1: Standard Blade Mesh Convergence Study
  </figcaption>
</figure>

<figure style="text-align:center; margin-top: 2rem;">
  <img src="{{ '/assets/images/ANSYS-Volume-Mesh.png' | relative_url }}" 
       alt="Figure 2: ANSYS Volume Mesh"
       style="width:125%; max-width:600px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    Figure 2: Volumetric Mesh used in ANSYS Simulation
  </figcaption>
</figure>


<figure style="text-align:center; margin-top: 2rem;">
  <img src="{{ '/assets/images/ANSYS-Blade.png' | relative_url }}" 
       alt="Figure 3: ANSYS Blade"
       style="width:125%; max-width:600px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    Figure 3: Pressure Distributions on Windward (left) and Leeward (right) Side of Blade
  </figcaption>
</figure>



</details>

---

<details open>
<summary><strong>Standard Blade BEM Code</strong></summary>

<br>

The Standard Blade was simulated in Matlab, using the BEM theory described in the "Wind Energy Explained" textbook.  The code used iterative solution of non-linear equations to determine the axial and tangential induction factors. The code incorporated key physical corrections, including the Prandtl tip loss factor to account for reduced lift at the blade tip and a correction for wake rotation. The code was driven by airfoil data as a function of angle of attack for the NACA 4412 airfoil.

<figure style="text-align:center; margin-top: 2rem;">
  <img src="{{ '/assets/images/Blade-Flowchart.png' | relative_url }}" 
       alt="Figure 4: Matlab Flowchart"
       style="width:125%; max-width:600px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    Figure 4: Flowchart of the Iterative BEM Algorithim
  </figcaption>
</figure>

<br>
<br>

The BEM code was validated against ANSYS and existing experimental data for the standard blade. The BEM model successfully captured the correct qualitative trends, and indicated optimal conditions at similar tip speed ratios to the ANSYS and experimental results. However,  the magnitude of the calculated power coefficient was higher than both the ANSYS and experimental values, a typical discrepancy due to the omission of hub drag and support losses in the BEM model.

<figure style="text-align:center; margin-top: 2rem;">
  <img src="{{ '/assets/images/Blade-Simulation-Comparison.png' | relative_url }}" 
       alt="Figure 5: Simulation Comparison"
       style="width:125%; max-width:600px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    Figure 5: Comparison of ANSYS and BEM Simulation to Experimental Results
  </figcaption>
</figure>


</details>

---

<details open>
<summary><strong>Optimized Blade BEM Code</strong></summary>

<br>

A similar BEM-driven code was then used to modify and optimize the geometry of the standard blade to achieve better performance. The goal was to maximize the power coefficient across a practical range of Tip-Speed Ratios (TSR). The ideal chord length and pitch (twist) angle distribution along the blade radius were calculated for each section using BEM thoery for a new, higher-performing airfoil (NACA 6412), selected for its superior lift-to-drag ratio at the operational Reynolds numbers (Figure 6). The optimized chord and pitch distributions were then linearized for simplicity.

<figure style="text-align:center; margin-top: 2rem;">
  <img src="{{ '/assets/images/Blade-Optimization-Airfoil-Selection.png' | relative_url }}" 
       alt="Figure 6: Airfoil Selection"
       style="width:125%; max-width:600px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    Figure 6: Optimized Blade Airfoil Selection
  </figcaption>
</figure>


<figure style="text-align:center; margin-top: 2rem;">
  <img src="{{ '/assets/images/Blade-Linearized.png' | relative_url }}" 
       alt="Figure 7: Blade Linearization"
       style="width:125%; max-width:600px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    Figure 7: Linearization of Ideal Blade Chord and Pitch Distribution
  </figcaption>
</figure>

Using the linearized optimal geometry, the blade was simulated in a range of TSRs, to identify a range where it might outperform the standard blade. BEM results predict that between a TSR of 5.5 and 6.5, the optimized blade generates up to 2% more power than the standard blade. Even marginal performance improvements, such as the 2% gain shown here, can compound over years of turbine operation to produce substantial increases in total energy generation. 

<figure style="text-align:center; margin-top: 2rem;">
  <img src="{{ '/assets/images/Blade-Optimization-Results.png' | relative_url }}" 
       alt="Figure 8: Blade Optimization Results"
       style="width:125%; max-width:600px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    Figure 8: Optimized Blade Performance Compared to Standard Blade
  </figcaption>
</figure>

Future works should aim to manufacture and physically test the designed blade in a range of TSR to validate the analytically predicted performance improvements.

</details>

---

<details>
<summary><strong>Contributions</strong></summary>

<br>

This was an individual senior design project. 
I am grateful for the guidance and support from my Primary Supervisor, Dr. Rebecca J. Barthelmie, as well as the ANSYS curriculum developed by Dr. Rajesh Bhaskaran.

</details>