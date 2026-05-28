---
layout: project
title: "Space Mission Design (MAE 5160)"
description: "Spacecraft C&DH, Power, and Ground Subsystem Design"
technologies:
  - Spacecraft Systems Architecture
  - C&DH Design
  - Power Subsystem Sizing
  - Trade Study Analysis
  - Risk Assessment
image: /assets/images/Charon-Cover.png
---

<br><br><br><br><br><br>

<details open>
<summary><strong>Overview</strong></summary>

<br>

Charon is a constellation of 24 laser-equipped spacecraft designed to detect, track, and ablate small space debris (1–10 cm) in low Earth orbit at 875 km altitude, reducing the debris population in the target band by approximately 50% over a 15-year operational lifespan. The mission was designed as part of a Preliminary Design Review (PDR) for MAE 5160: Spacecraft Technology and Systems Architecture at Cornell University.

My responsibility covered three subsystems: Command and Data Handling (C&DH), Power, and Ground. The work spanned requirements derivation, technology selection through weighted trade studies, component sizing, cost and mass estimation, risk assessment, and procurement planning. The remaining subsystems — ACS, Propulsion, TT&C, Payload, and Autonomy — were addressed by teammates.

</details>

---

<details open>
<summary><strong>Mission Timeline</strong></summary>

<br>

<div style="display:flex; flex-direction:column; gap:8px; max-width:800px; margin:auto 0 0.5rem 0;">
  <img src="{{ '/assets/images/Charon-Storyboard-A.png' | relative_url }}" alt="T+10min separation through T+60min Hohmann transfer" style="width:100%;">
  <img src="{{ '/assets/images/Charon-Storyboard-B.png' | relative_url }}" alt="T+75min solar array deployment through T+weeks calibration" style="width:100%;">
  <img src="{{ '/assets/images/Charon-Storyboard-C.png' | relative_url }}" alt="T+1-6mo debris tracking and laser initiation" style="width:100%;">
  <img src="{{ '/assets/images/Charon-Storyboard-D.png' | relative_url }}" alt="T+3-25yr full constellation through deorbit" style="width:100%;">
</div>
<p style="text-align:center; font-size:0.9em; color:#555; margin-top:0.4rem;">Mission storyboard panels: launch through end-of-life deorbit</p>

The mission was designed around the following operational sequence:

<table style="width:95%; border:1px solid #000; border-collapse:collapse; text-align:left;">
  <tr>
    <th style="padding:6px;">Mission Phase</th>
    <th style="padding:6px;">Event</th>
  </tr>
  <tr><td style="padding:6px;"><strong>T+10 min</strong></td><td style="padding:6px;">Separation from SpaceX Starship into ~250 km parking orbit. Initial ground contact.</td></tr>
  <tr><td style="padding:6px;"><strong>T+60 min</strong></td><td style="padding:6px;">Hohmann transfer to 875 km operational orbit. Coplanar launch required to minimize ΔV. [M1 met]</td></tr>
  <tr><td style="padding:6px;"><strong>T+75–100 min</strong></td><td style="padding:6px;">Solar array deployment, replenishing onboard battery stores.</td></tr>
  <tr><td style="padding:6px;"><strong>T+hours to days</strong></td><td style="padding:6px;">Attitude control checkout, initial ground station communication, subsystem health verification.</td></tr>
  <tr><td style="padding:6px;"><strong>T+weeks</strong></td><td style="padding:6px;">Sensor calibration, autonomous navigation validation, onboard ephemeris database check.</td></tr>
  <tr><td style="padding:6px;"><strong>T+1–3 months</strong></td><td style="padding:6px;">Debris tracking initiation; onboard catalog built from 1–10 cm detections. [M2 met]</td></tr>
  <tr><td style="padding:6px;"><strong>T+3–6 months</strong></td><td style="padding:6px;">Laser checkout and first ablation test engagements; measurable orbital decay confirmed. [P1 met]</td></tr>
  <tr><td style="padding:6px;"><strong>T+6–12 months</strong></td><td style="padding:6px;">Full operational capability; patrol-as-a-service begins across CHARON constellation. [F1 met]</td></tr>
  <tr><td style="padding:6px;"><strong>T+3–5 years</strong></td><td style="padding:6px;">24th satellite joins constellation; coordinated multi-satellite ablation fully operational. [FMS_1 met]</td></tr>
  <tr><td style="padding:6px;"><strong>T+15 years</strong></td><td style="padding:6px;">~2% of initial debris population eliminated per satellite across 15-year lifespan.</td></tr>
  <tr><td style="padding:6px;"><strong>T+15–25 years</strong></td><td style="padding:6px;">Controlled deorbit burn; atmospheric reentry and burnup. Compliant with 25-year post-mission deorbit standard. [PMS_2 met]</td></tr>
</table>

<br>

The Hohmann transfer time was calculated as T/2 = π × √(((r₁ + r₂)/2)³ / 398600) / 60 ≈ 50 min, confirming the T+60 min orbit insertion milestone.

</details>

---

<details>
<summary><strong>Requirements</strong></summary>

<br>

<h3>Mission Success Criteria</h3>

<table style="width:95%; border:1px solid #000; border-collapse:collapse; text-align:left;">
  <tr>
    <th style="padding:6px; width:80px;">Criteria</th>
    <th style="padding:6px;">Description</th>
    <th style="padding:6px; width:80px;">Priority</th>
  </tr>
  <tr><td style="padding:6px;">M1</td><td style="padding:6px;">Spacecraft can enter a stable orbit at an altitude known to be dense with debris</td><td style="padding:6px;">Minimal</td></tr>
  <tr><td style="padding:6px;">M2</td><td style="padding:6px;">Spacecraft can autonomously track/detect the constellation of small to mid-sized space debris</td><td style="padding:6px;">Minimal</td></tr>
  <tr><td style="padding:6px;">P1</td><td style="padding:6px;">Spacecraft can deorbit small to mid-sized space debris by using lasers to reduce the periapsis of debris orbits and record successfully deorbited debris</td><td style="padding:6px;">Partial</td></tr>
  <tr><td style="padding:6px;">P2</td><td style="padding:6px;">Able to deorbit itself after running out of power/propulsion</td><td style="padding:6px;">Partial</td></tr>
  <tr><td style="padding:6px;">F1</td><td style="padding:6px;">Dual-use for defense laser weapon testing</td><td style="padding:6px;">Full</td></tr>
  <tr><td style="padding:6px;">F2</td><td style="padding:6px;">Reduce the quantity of small to mid-sized space debris by 50% (250K) in the selected altitude band</td><td style="padding:6px;">Full</td></tr>
</table>

<br>

<h3>System Level Requirements</h3>

<table style="width:95%; border:1px solid #000; border-collapse:collapse; text-align:left;">
  <tr>
    <th style="padding:6px;">Requirement</th>
    <th style="padding:6px;">Justification</th>
  </tr>
  <tr><td style="padding:6px;">The spacecraft shall enter and maintain a circular orbit at 875 km altitude.</td><td style="padding:6px;">The densest band of space debris is located between 750 and 1000 km in altitude.</td></tr>
  <tr><td style="padding:6px;">The spacecraft shall be capable of autonomously maintaining current track, adjusting its attitude, and activating its laser payload to engage identified debris without requiring uplink commands from an AWS station.</td><td style="padding:6px;">Mission Success Criteria M2. Ground stations can provide targets for the spacecraft, however, the spacecraft should be able to identify and track them independently.</td></tr>
  <tr><td style="padding:6px;">The spacecraft shall interface with SpaceX Starship as the primary launch vehicle.</td><td style="padding:6px;">Starship can carry up to 250 tons and 9 m diameter payloads, and several satellites should be able to fit in every launch to operate at scale.</td></tr>
  <tr><td style="padding:6px;">The spacecraft shall be able to track and detect space debris ranging from 1 to 10 cm diameter from as far as 500 km away.</td><td style="padding:6px;">Ensures sufficient coverage both within and outside the densest band of space debris. Leads to 24 satellites required for coverage.</td></tr>
  <tr><td style="padding:6px;">The total mission budget shall be approximately $5 billion.</td><td style="padding:6px;">Each satellite's cost is estimated at $200 million.</td></tr>
  <tr><td style="padding:6px;">The spacecraft shall maintain a pointing knowledge and control accuracy sufficient to strike a 1 cm target at a range of 500 km.</td><td style="padding:6px;">So as to match the optical sensing capabilities.</td></tr>
  <tr><td style="padding:6px;">The spacecraft shall have a mission life of at least 15 years, and up to a maximum of 20 years before deorbiting.</td><td style="padding:6px;">The minimum value is typical for satellites. The maximum value comes from FCC regulations for LEO satellites to deorbit within 5 years of mission end.</td></tr>
  <tr><td style="padding:6px;">The spacecraft will be able to withstand the radiation dosage of its designed orbit for 15 years.</td><td style="padding:6px;">Extreme radiation associated with orbiting in Van Allen belts.</td></tr>
  <tr><td style="padding:6px;">The spacecraft shall be able to withstand the extreme temperature swings between illuminated and eclipse times.</td><td style="padding:6px;">There is an approximate 500°F (+250°F to −250°F) temperature difference while illuminated vs. in eclipse, affecting material expansion rates and internal temperatures.</td></tr>
  <tr><td style="padding:6px;">Overall satellite reliability shall be at least 75%.</td><td style="padding:6px;">For an adequate safety margin on Mission Criteria F2.</td></tr>
  <tr><td style="padding:6px;">The spacecraft shall have the power generation and storage infrastructure to change the track of space debris sufficiently for near-term deorbiting.</td><td style="padding:6px;">Mission Success Criteria P1, F1, F2.</td></tr>
</table>

<br>

<h3>C&DH, Power, Thermal, and Ground Subsystem Requirements</h3>

<table style="width:95%; border:1px solid #000; border-collapse:collapse; text-align:left;">
  <tr>
    <th style="padding:6px; width:80px;">ID</th>
    <th style="padding:6px;">Requirement</th>
  </tr>
  <tr><td style="padding:6px;">CDH-1</td><td style="padding:6px;">The spacecraft shall implement a MIL-STD-1553B dual-redundant data bus operating at 1 Mb/s for primary command and data handling functions</td></tr>
  <tr><td style="padding:6px;">CDH-2</td><td style="padding:6px;">The C&DH bus shall not exceed 40% loading at initial design and shall not exceed 60% loading at fielding</td></tr>
  <tr><td style="padding:6px;">CDH-3</td><td style="padding:6px;">The flight computer shall exhibit no unrecoverable soft errors within the 15-year mission lifetime</td></tr>
  <tr><td style="padding:6px;">CDH-4</td><td style="padding:6px;">The spacecraft shall provide a minimum of 20 Gb of onboard bulk data storage</td></tr>
  <tr><td style="padding:6px;">CDH-5</td><td style="padding:6px;">The spacecraft shall implement a separate high-rate payload data bus operating at a minimum of 9 Mb/s</td></tr>
  <tr><td style="padding:6px;">CDH-6</td><td style="padding:6px;">All C&DH components shall tolerate a minimum total ionising dose of 5 krad (COTS) or 300 krad (radiation-hardened) as appropriate to the selected component grade</td></tr>
  <tr><td style="padding:6px;">CDH-7</td><td style="padding:6px;">The flight computer shall incorporate RAM and EEPROM, and the spacecraft shall provide a separate Solid State Recorder for bulk payload data storage</td></tr>
  <tr><td style="padding:6px;">PWR-1</td><td style="padding:6px;">The power subsystem shall provide a minimum peak power of 30 kW during laser operation, a minimum dormant power of 7.5 kW during laser-off periods, and a minimum average power of 10 kW based on a 10% laser duty cycle</td></tr>
  <tr><td style="padding:6px;">PWR-2</td><td style="padding:6px;">The power subsystem shall store a minimum of 61.45 MJ (17.1 kWh) of energy to sustain operations through eclipse and peak demand periods</td></tr>
  <tr><td style="padding:6px;">PWR-3</td><td style="padding:6px;">The power subsystem's batteries shall be charged to full capacity (61.45 MJ) to provide initial power to the spacecraft before the solar array is deployed, with enough margin to demonstrate ablation should the solar array fail to deploy</td></tr>
  <tr><td style="padding:6px;">THM-1</td><td style="padding:6px;">The thermal subsystem shall be able to dissipate 21.1 kW of heat corresponding to the simultaneous use of the laser and all powered components</td></tr>
  <tr><td style="padding:6px;">GND-1</td><td style="padding:6px;">The ground segment shall utilise a minimum of four AWS Ground Station as a Service contacts at Stockholm, Bahrain, Cape Town, and Alaska to provide near-worldwide coverage</td></tr>
  <tr><td style="padding:6px;">GND-2</td><td style="padding:6px;">The ground segment shall support a downlink data dump rate of 150 Mb/s</td></tr>
  <tr><td style="padding:6px;">GND-3</td><td style="padding:6px;">The ground segment shall implement encrypted communications with frequency hopping for all mission-sensitive data transfers</td></tr>
  <tr><td style="padding:6px;">GND-4</td><td style="padding:6px;">The spacecraft shall provide inter-satellite relay capability to support distributed mission operations</td></tr>
  <tr><td style="padding:6px;">GND-5</td><td style="padding:6px;">The ground segment shall use AWS EC2 compute 61 Gb of telemetry per orbit</td></tr>
  <tr><td style="padding:6px;">GND-6</td><td style="padding:6px;">The ground segment shall store 4.7 Pb of data in AWS S3 per satellite over its lifetime, of which the prior month's data (25.8 Tb) must be instantly retrievable</td></tr>
</table>

</details>

---

<details open>
<summary><strong>C&DH Subsystem</strong></summary>

<br>

The C&DH subsystem manages all onboard command routing, data handling, storage, and fault protection over the 15-year mission lifetime in an 875 km LEO radiation environment.

<figure style="text-align:center;">
  <img src="{{ '/assets/images/Charon-CDANDH-Architecture.png' | relative_url }}"
       alt="C&DH Architecture Diagram"
       style="width:100%; max-width:650px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    C&DH architecture: MIL-STD-1553B dual-redundant bus connecting flight computer, EDAC, SSR, and subsystem terminals
  </figcaption>
</figure>

<h3>Main Data Bus</h3>

The main bus implements a MIL-STD-1553B dual-redundant architecture at 1 Mb/s, with bus loading constrained to 40% at initial design and 60% at fielding. An integrated vs. distributed topology trade was performed:

<ul>
  <li><strong>Integrated (SMAD 16-8):</strong> Deterministic transmission via a centralized bus controller; MIL-STD-1553B was originally designed for this use. Constrains flexibility as all subsystems must conform to a shared standard.</li>
  <li><strong>Distributed (SMAD 16-9):</strong> Multiple CPUs can perform the same task, providing redundancy. Non-deterministic, but acceptable given 1553B's command/response scheduling.</li>
</ul>

A distributed architecture was selected to meet the 0.93 reliability requirement through improved redundancy, despite increased testing complexity.

<h3>Payload Data Bus</h3>

A separate high-rate payload bus operating at a minimum of 9 Mb/s is required. Since MIL-STD-1553B's physical layer is limited to 1 Mbps, an FPGA-based IP core solution — specifically the DDC SSRT-Core (BU-69210) — was selected to support higher data rates while retaining 1553B protocol heritage.

<h3>Flight Computer</h3>

<figure style="text-align:center;">
  <img src="{{ '/assets/images/Charon-RHPPC-SBC.png' | relative_url }}"
       alt="Honeywell RHPPC Single Board Computer"
       style="width:100%; max-width:550px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    Honeywell RHPPC Single Board Computer — selected baseline flight computer
  </figcaption>
</figure>

The Honeywell RHPPC Single Board Computer was selected as the baseline flight computer. Key properties:
<ul>
  <li>Rated to ≥100 krad TID — meets the 300 krad radiation-hardened requirement with 1.6 mm aluminium shielding (vs. 0.6 mm baseline, a negligible design change)</li>
  <li>Native MIL-STD-1553B interface</li>
  <li>Unrecoverable SER of 4.8 × 10⁻⁵ per SBC per day; mean time to unrecoverable error ≈ 57 years — well in excess of the 15-year mission lifetime</li>
</ul>

<h3>Data Storage and EDAC</h3>

The 3D Plus 3DSS64G08US2818 RTIMS Flash (64 Gb) satisfies both the mass storage and EDAC requirements as a single integrated module. Operating in Reed Solomon + Hamming protection mode, it provides 32 Gb of EDAC-protected usable storage per module. Approximately 7 modules are needed to meet the 200 Gb requirement. A 3 mm aluminium spot shield reduces the radiation environment to ~48 krad, within the device's rated 50 krad TID tolerance. Estimated unit cost: ~$15,000–$45,000 per module.

<h3>C&DH Sizing Summary</h3>

<table style="width:70%; border:1px solid #000; border-collapse:collapse; text-align:center;">
  <tr>
    <th>Parameter</th>
    <th>Value</th>
    <th>Source</th>
  </tr>
  <tr><td>Volume</td><td>~7,500 cm³</td><td>SMAD Table 11-29</td></tr>
  <tr><td>Mass</td><td>~5.5 kg</td><td>SMAD Table 11-29</td></tr>
  <tr><td>Power (used)</td><td>~15.5 W</td><td>SMAD Table 11-29 / RHPPC: 11 W</td></tr>
  <tr><td>Total Cost</td><td>~$4.4M</td><td>Data bus $200k + Flight computer $4M + Storage $200k</td></tr>
</table>

</details>

---

<details>
<summary><strong>Power Subsystem</strong></summary>

<br>

The power subsystem must satisfy three simultaneous requirements: 30 kW peak during laser operation, 7.5 kW dormant during laser-off periods, and 10 kW average based on a 10% laser duty cycle. Energy storage of 61.45 MJ (17.1 kWh) is required to sustain operations through eclipse and peak demand.

<figure style="text-align:center;">
  <img src="{{ '/assets/images/Charon-HESS-Architecture.png' | relative_url }}"
       alt="HESS Architecture Diagram"
       style="width:100%; max-width:650px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    Hybrid Energy Storage System (HESS) architecture — power management controller mediates battery and supercapacitor bank
  </figcaption>
</figure>

<h3>Solar Array</h3>

Solar cell degradation of 1%/year means the array retains 0.99¹⁵ = 86% of its beginning-of-life output by end of mission. To guarantee the required 10 kW average at end of life, the array must generate 11.4 kW at beginning of life.

Using a 32% triple-junction cell efficiency and the standard sizing relation:

<p style="text-align:center;">
  A<sub>panels</sub> = 1.22 × P<sub>req,0</sub> ÷ (P<sub>density</sub> × η<sub>cells</sub> × f<sub>eclipse</sub>) ≈ <strong>45 m²</strong>
</p>

The array is shielded with 0.5 mm solar cell cover glass (SCHOTT/Qioptiq), adding 56.25 kg at a glass density of 2.5 g/cm³. Deployment uses a Solar Array Drive Assembly (SADA) analogous to the Psyche mission ROSA system; the array folds to ~60% of deployed area at launch (6.5 m × 4.1 m stowed), deploying in approximately 8 minutes post orbit insertion.

<figure style="text-align:center;">
  <img src="{{ '/assets/images/Charon-Release-Mechanisms.png' | relative_url }}"
       alt="Dual Redundant Release Mechanisms"
       style="width:100%; max-width:650px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    Two candidate dual-redundant solar array release mechanisms: shared shaft (left) vs. independent shafts (right)
  </figcaption>
</figure>

<figure style="text-align:center;">
  <img src="{{ '/assets/images/Charon-Thermal-Dissipators.png' | relative_url }}"
       alt="Thermal Dissipators Concept"
       style="width:100%; max-width:650px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    Thermal dissipator concept for managing heat rejected from the solar array panels
  </figcaption>
</figure>

<table style="width:70%; border:1px solid #000; border-collapse:collapse; text-align:center;">
  <tr><th>Parameter</th><th>Value</th></tr>
  <tr><td>Array Area</td><td>45 m² deployed / ~1.33 m² stowed</td></tr>
  <tr><td>Array Mass (with shielding)</td><td>113 kg (57 kg panels + 56 kg cover glass)</td></tr>
  <tr><td>Power Output (BOL)</td><td>11,400 W</td></tr>
  <tr><td>Total Cost</td><td>~$15.9M ($9.1M panels + $6.8M cover glass)</td></tr>
</table>

<h3>Hybrid Energy Storage System (HESS)</h3>

A Hybrid Energy Storage System architecture was selected, consistent with NASA JPL's Energy Storage Technologies for Future Planetary Science Missions recommendation to combine primary batteries with ultracapacitors to address the distinct nominal and peak power profiles.

<ul>
  <li><strong>Nominal power — Li-CFx primary batteries:</strong> 350–400 Wh/kg specific energy. At this specific energy, the 17.1 kWh storage requirement corresponds to ~45.6 kg of battery cells. Cost: ~$2.58M.</li>
  <li><strong>Peak power — Ultracapacitors:</strong> Specific power exceeding 1 kW/kg; 30 kW peak demand requires ~30 kg. At 5 Wh/kg specific energy, this 30 kg bank provides 150 Wh — sufficient for 900 pulses at 600 J per pulse, with recharge from the battery bank between sequences. Cost: ~$1,500.</li>
</ul>

A custom power management controller mediates switching between the battery and capacitor bank based on instantaneous demand and the timing of upcoming laser engagements.

<table style="width:70%; border:none; text-align:center; margin: 1rem auto;">
  <tr>
    <td style="padding:10px;">
      <img src="{{ '/assets/images/Charon-LiCFx-Battery.png' | relative_url }}"
           alt="Li-CFx Battery Cells"
           style="width:100%; max-width:220px; display:block; margin:auto;">
      <div style="font-size:0.85em; color:#555; margin-top:4px;">Li-CFx primary battery cells (EaglePicher)</div>
    </td>
    <td style="padding:10px;">
      <img src="{{ '/assets/images/Charon-Supercapacitor.png' | relative_url }}"
           alt="Supercapacitor"
           style="width:100%; max-width:220px; display:block; margin:auto;">
      <div style="font-size:0.85em; color:#555; margin-top:4px;">Space-qualified supercapacitor (Kyocera AVX)</div>
    </td>
  </tr>
</table>

<table style="width:70%; border:1px solid #000; border-collapse:collapse; text-align:center;">
  <tr><th>Component</th><th>Mass</th><th>Cost</th></tr>
  <tr><td>Solar array (panels + cover glass)</td><td>113 kg</td><td>~$15.9M</td></tr>
  <tr><td>Li-CFx battery</td><td>45.6 kg</td><td>~$2.58M</td></tr>
  <tr><td>Supercapacitor bank</td><td>30 kg</td><td>~$1,500</td></tr>
  <tr><td>HESS controller</td><td>TBD</td><td>TBD</td></tr>
  <tr><td><strong>Power Subtotal</strong></td><td><strong>~188.6 kg</strong></td><td><strong>~$18.5M</strong></td></tr>
</table>

<br>

A thermal management system for the capacitor discharge circuit is flagged as an open item prior to CDR.

</details>

---

<details>
<summary><strong>Ground Segment</strong></summary>

<br>

The ground segment uses AWS Ground Station as a Service (GSaaS) with four contacts at Stockholm, Bahrain, Cape Town, and Alaska for near-worldwide coverage.

<figure style="text-align:center;">
  <a href="https://drive.google.com/file/d/16IrJrj5i7copBM55YgDFnToM-ES2vgM3/view?usp=sharing" target="_blank">
    <img src="{{ '/assets/images/Charon-Ground-Coverage.png' | relative_url }}"
         alt="Satellite Ground Coverage Tracks"
         style="width:100%; max-width:700px; display:block; margin:auto;">
  </a>
  <figcaption style="font-size:0.9em; color:#555;">
    Satellite ground tracks over the four AWS Ground Station locations — click to open interactive simulation
  </figcaption>
</figure>

<h3>Station Selection</h3>

<figure style="text-align:center;">
  <img src="{{ '/assets/images/Charon-Ground-Stations.png' | relative_url }}"
       alt="Ground Station Characteristics"
       style="width:100%; max-width:750px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    AWS Ground Station capabilities by location — frequency ranges, bandwidth, and polarisation
  </figcaption>
</figure>

Three stations (Stockholm, Bahrain, Cape Town) support X-band wideband downlink across 7,750–8,500 MHz with 50–400 MHz bandwidth in RHCP. Alaska does not support X-band wideband and instead provides X-band demodulated/decoded downlink across the same frequency range with up to 500 MHz bandwidth in RHCP. RHCP was selected as the standard polarisation across all four stations as the more widely used convention.

<h3>Downlink Data Rate</h3>

The 150 Mb/s downlink requirement is satisfied via the Shannon-Hartley relation:

<p style="text-align:center;">
  Data Rate = Bandwidth × log₂(1 + S/N)
</p>

With available bandwidths of 50–400 MHz at wideband stations and up to 500 MHz at Alaska, the requirement is satisfiable at appropriate signal-to-noise ratios.

<h3>Encryption and Security</h3>

AWS Ground Station provides AWS-owned encryption keys as a baseline for non-sensitive operations. For sensitive operations including ephemerides and mission-critical data, customer-managed keys are implemented through AWS Key Management Service (KMS). Frequency hopping is not provided by AWS infrastructure and will be sourced from Space Force or equivalent client communications infrastructure.

<h3>Contact Windows</h3>

<figure style="text-align:center;">
  <img src="{{ '/assets/images/Charon-Scheduling-Windows.png' | relative_url }}"
       alt="Sample Scheduling Windows"
       style="width:100%; max-width:550px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    Sample AWS Ground Station scheduling windows showing contact opportunities across stations
  </figcaption>
</figure>

<figure style="text-align:center;">
  <img src="{{ '/assets/images/Charon-Downlink-Times.png' | relative_url }}"
       alt="Downlink Times"
       style="width:100%; max-width:500px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    Downlink window durations per orbit pass
  </figcaption>
</figure>

<h3>Ground Segment Cost</h3>

Using AWS reserved contact pricing of $10/min for wideband contacts and a 407-second dump window per 6,145-second orbit: cost per orbit ≈ $68. Over 15 years at ~76,995 orbits, ground segment cost ≈ <strong>$5.2M per satellite</strong> over mission lifetime.

</details>

---

<details>
<summary><strong>Trade Studies</strong></summary>

<br>

<h3>Power Source Trade Study</h3>

The trade was narrowed to solar photovoltaic vs. solar thermal dynamic — the only practical candidates for Earth-orbiting spacecraft at constellation scale per SMAD. Three weighted criteria were evaluated:

<table style="width:95%; border:1px solid #000; border-collapse:collapse; text-align:center;">
  <tr>
    <th>Criterion</th>
    <th>Weighting</th>
    <th>Solar Photovoltaic</th>
    <th>Solar Thermal Dynamic</th>
  </tr>
  <tr>
    <td>1/Size (1/m²)</td><td>0.25</td>
    <td>1/45</td><td>1/27</td>
  </tr>
  <tr>
    <td>Specific Power (W/kg)</td><td>0.50</td>
    <td>200 (SMAD 11-33)</td><td>15 (SMAD 11-33)</td>
  </tr>
  <tr>
    <td>1/Specific Cost (W/$)</td><td>0.25</td>
    <td>1/800–1/3000 (SMAD 11-33)</td><td>1/1000–1/2000 (SMAD 11-33)</td>
  </tr>
  <tr>
    <td><strong>Result (optimal bound)</strong></td><td>—</td>
    <td style="background-color:#c7f2c2;"><strong>1.00</strong></td><td>0.83</td>
  </tr>
  <tr>
    <td><strong>Result (lower bound)</strong></td><td>—</td>
    <td style="background-color:#c7f2c2;"><strong>1.00</strong></td><td>0.65</td>
  </tr>
</table>

<br>

Solar photovoltaic won decisively across both cost bounds, primarily due to its 13× advantage in specific power (200 vs. 15 W/kg). Although it requires larger collection area (45 vs. 27 m²), foldable deployment technology resolves this at launch. It also carries significantly less system complexity and established flight heritage.

<h3>Radiation Protection Trade Study</h3>

At 875 km LEO over 15 years, the baseline TID was derived from Kuntepce et al. (2023) at 434 krad(Si) (800 km reference), then scaled by ×1.25 for the deeper inner Van Allen belt penetration at 875 km, yielding 543 krad(Si) at 0.5 mm aluminium shielding. Both COTS (~5–25 krad tolerance) and radiation-hardened components (~300 krad tolerance) require additional shielding. The dose-depth relationship was characterized by the empirical fit:

<p style="text-align:center;">
  Dose = 189,548 × t<sup>−1.38</sup> (t in mm Al)
</p>

<figure style="text-align:center;">
  <img src="{{ '/assets/images/Charon-Radiation-Dose-Depth.png' | relative_url }}"
       alt="Radiation Dosage vs Shielding Thickness"
       style="width:100%; max-width:600px; display:block; margin:auto;">
  <figcaption style="font-size:0.9em; color:#555;">
    Radiation dosage vs. aluminium shielding thickness — empirical fit: Dose = 189,548 × t<sup>−1.38</sup>
  </figcaption>
</figure>

The trade study evaluated COTS with heavy aluminium shielding vs. radiation-hardened components across two weighted criteria:

<table style="width:95%; border:1px solid #000; border-collapse:collapse; text-align:center;">
  <tr>
    <th>Criterion</th>
    <th>Weighting</th>
    <th>COTS + 12 mm Al</th>
    <th>Radiation Hardened + 0.61 mm Al</th>
  </tr>
  <tr>
    <td>Specific Cost (1/$M)</td><td>0.40</td>
    <td>1/1.55</td><td>1/2.05</td>
  </tr>
  <tr>
    <td>Specific Mass (1/kg)</td><td>0.60</td>
    <td>1/100</td><td>1/35</td>
  </tr>
  <tr>
    <td><strong>Result</strong></td><td>—</td>
    <td>1.00</td>
    <td style="background-color:#c7f2c2;"><strong>2.02</strong></td>
  </tr>
</table>

<br>

Radiation-hardened components won by a factor of 2, primarily due to their dramatically lower shielding mass (2.6 kg vs. ~52 kg total), saving ~65 kg — a direct launch cost reduction. Although rad-hard parts carry a higher unit cost ($0.5M–$3M vs. $1k–$50k), the mass savings and lower qualification risk justify the selection.

</details>

---

<details>
<summary><strong>Risk Assessment</strong></summary>

<br>

<p style="font-size:0.9em; color:#555; margin-bottom:4px;">Consequence (↑) vs. Likelihood (→) — green: low · yellow: medium · orange: high · red: critical</p>

<table style="border-collapse:collapse; text-align:center; max-width:560px; margin:0 auto 1.5rem auto;">
  <tr>
    <td style="border:none; padding:4px 8px 4px 0; font-size:0.85em; text-align:right; vertical-align:middle; writing-mode:vertical-lr; transform:rotate(180deg); height:180px;">Consequence</td>
    <td style="border:none; padding:0;">
      <table style="border-collapse:collapse; text-align:center;">
        <tr>
          <td style="border:none; padding:2px 6px; font-size:0.8em; font-weight:bold;">5</td>
          <td style="border:1px solid #888; padding:14px 10px; background:#c7f2c2; min-width:70px;"></td>
          <td style="border:1px solid #888; padding:14px 10px; background:#FFE599; min-width:70px; font-size:0.82em;"><strong>RSK-03</strong></td>
          <td style="border:1px solid #888; padding:14px 10px; background:#F4B942; min-width:70px;"></td>
          <td style="border:1px solid #888; padding:14px 10px; background:#E8756A; min-width:70px;"></td>
          <td style="border:1px solid #888; padding:14px 10px; background:#E8756A; min-width:70px;"></td>
        </tr>
        <tr>
          <td style="border:none; padding:2px 6px; font-size:0.8em; font-weight:bold;">4</td>
          <td style="border:1px solid #888; padding:14px 10px; background:#c7f2c2;"></td>
          <td style="border:1px solid #888; padding:14px 10px; background:#FFE599; font-size:0.82em;"><strong>RSK-06</strong></td>
          <td style="border:1px solid #888; padding:14px 10px; background:#F4B942; font-size:0.82em;"><strong>RSK-02</strong><br><em>(2+ stations)</em></td>
          <td style="border:1px solid #888; padding:14px 10px; background:#F4B942;"></td>
          <td style="border:1px solid #888; padding:14px 10px; background:#E8756A;"></td>
        </tr>
        <tr>
          <td style="border:none; padding:2px 6px; font-size:0.8em; font-weight:bold;">3</td>
          <td style="border:1px solid #888; padding:14px 10px; background:#c7f2c2;"></td>
          <td style="border:1px solid #888; padding:14px 10px; background:#c7f2c2;"></td>
          <td style="border:1px solid #888; padding:14px 10px; background:#FFE599; font-size:0.82em;"><strong>RSK-02<br>RSK-05</strong></td>
          <td style="border:1px solid #888; padding:14px 10px; background:#F4B942; font-size:0.82em;"><strong>RSK-04</strong></td>
          <td style="border:1px solid #888; padding:14px 10px; background:#F4B942;"></td>
        </tr>
        <tr>
          <td style="border:none; padding:2px 6px; font-size:0.8em; font-weight:bold;">2</td>
          <td style="border:1px solid #888; padding:14px 10px; background:#c7f2c2;"></td>
          <td style="border:1px solid #888; padding:14px 10px; background:#c7f2c2;"></td>
          <td style="border:1px solid #888; padding:14px 10px; background:#c7f2c2;"></td>
          <td style="border:1px solid #888; padding:14px 10px; background:#FFE599; font-size:0.82em;"><strong>RSK-01</strong></td>
          <td style="border:1px solid #888; padding:14px 10px; background:#FFE599;"></td>
        </tr>
        <tr>
          <td style="border:none; padding:2px 6px; font-size:0.8em; font-weight:bold;">1</td>
          <td style="border:1px solid #888; padding:14px 10px; background:#c7f2c2;"></td>
          <td style="border:1px solid #888; padding:14px 10px; background:#c7f2c2;"></td>
          <td style="border:1px solid #888; padding:14px 10px; background:#c7f2c2;"></td>
          <td style="border:1px solid #888; padding:14px 10px; background:#c7f2c2;"></td>
          <td style="border:1px solid #888; padding:14px 10px; background:#c7f2c2;"></td>
        </tr>
        <tr>
          <td style="border:none;"></td>
          <td style="border:1px solid #888; padding:4px; font-size:0.8em; font-weight:bold;">1</td>
          <td style="border:1px solid #888; padding:4px; font-size:0.8em; font-weight:bold;">2</td>
          <td style="border:1px solid #888; padding:4px; font-size:0.8em; font-weight:bold;">3</td>
          <td style="border:1px solid #888; padding:4px; font-size:0.8em; font-weight:bold;">4</td>
          <td style="border:1px solid #888; padding:4px; font-size:0.8em; font-weight:bold;">5</td>
        </tr>
        <tr>
          <td style="border:none;"></td>
          <td colspan="5" style="border:none; padding:4px; font-size:0.85em; font-weight:bold;">Likelihood</td>
        </tr>
      </table>
    </td>
  </tr>
</table>

<table style="width:95%; border:1px solid #000; border-collapse:collapse; text-align:center;">
  <tr>
    <th>Risk</th>
    <th>Likelihood</th>
    <th>Consequence</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>RSK-01</td><td>4</td><td>2</td>
    <td style="text-align:left; padding:6px;">Solar arrays degrade faster than expected (1%/year). If unchecked, laser firing frequency or overall spacecraft function may be jeopardized. Mitigation: FASTRAD simulation; array resized with additional cover glass if needed.</td>
  </tr>
  <tr>
    <td>RSK-02</td><td>3</td><td>3 / 4</td>
    <td style="text-align:left; padding:6px;">AWS ground station outage. Satellites store up to 3 orbits of data for short outages; relay via inter-satellite links if one station fails. Multi-station outage (2+) escalates to consequence 4 and risks data loss. Mitigation: constellation relay simulation and on-orbit testing.</td>
  </tr>
  <tr>
    <td>RSK-03</td><td>2</td><td>5</td>
    <td style="text-align:left; padding:6px;">Solar array fails to deploy. Catastrophic power loss disables all systems including laser payload. Three mitigation strategies identified: pre-charged battery reserve, cable-free conducting hinges, and dual-redundant release mechanisms.</td>
  </tr>
  <tr>
    <td>RSK-04</td><td>4</td><td>3</td>
    <td style="text-align:left; padding:6px;">Power generation/storage TRL lower than anticipated (especially Li-CFx and supercapacitors), affecting size, mass, and cost. Mitigation: TRL 6 by PDR, TRL 9 by CDR; formal RFQ from EaglePicher/Saft before PDR.</td>
  </tr>
  <tr>
    <td>RSK-05</td><td>3</td><td>3</td>
    <td style="text-align:left; padding:6px;">Launch vehicle single-point dependency (TRL 7). Starship is the sole qualifying vehicle based on fairing diameter; continued schedule delays may necessitate redesigning the solar array deployment from a single-fold to a multi-fold configuration, increasing hinge count, mass, cost, and deployment failure points.</td>
  </tr>
  <tr>
    <td>RSK-06</td><td>2</td><td>4</td>
    <td style="text-align:left; padding:6px;">Thermal radiator design and orientation (TRL 7+). The radiator assembly — while using individually flight-proven coating and panel technologies — has not been validated in the specific combination and orientation proposed for this mission. If inter-segment radiation interference is not adequately characterised, the spacecraft may be unable to reject the full 21.1 kW thermal load, requiring a reduction in laser duty cycle.</td>
  </tr>
</table>

</details>

---

<details>
<summary><strong>Subsystem Summary</strong></summary>

<br>

<table style="width:95%; border:1px solid #000; border-collapse:collapse; text-align:center;">
  <tr>
    <th style="padding:6px;">Subsystem</th>
    <th style="padding:6px;">Mass (kg)</th>
    <th style="padding:6px;">Size (m³)</th>
    <th style="padding:6px;">Power (kW)*</th>
    <th style="padding:6px;">Cost ($M)</th>
  </tr>
  <tr><td style="padding:6px;">Propulsion</td><td>120</td><td>0.60</td><td>−1.0</td><td>11.0</td></tr>
  <tr><td style="padding:6px;">Autonomy</td><td>—</td><td>—</td><td>—</td><td>—</td></tr>
  <tr><td style="padding:6px;">ACS</td><td>60</td><td>0.30</td><td>−0.08</td><td>8.5</td></tr>
  <tr><td style="padding:6px;">Payload</td><td>107</td><td>6.00</td><td>−2.0</td><td>75.0</td></tr>
  <tr><td style="padding:6px;">TT&C</td><td>8</td><td>0.121</td><td>−0.04</td><td>10.0</td></tr>
  <tr><td style="padding:6px;">C&DH</td><td>5.5</td><td>0.0075</td><td>−0.0155</td><td>4.4</td></tr>
  <tr><td style="padding:6px;">Power</td><td>188.6</td><td>1.33</td><td>+11.4</td><td>18.5</td></tr>
  <tr><td style="padding:6px;">Ground</td><td>—</td><td>—</td><td>—</td><td>5.5</td></tr>
  <tr><td style="padding:6px;">Thermal</td><td>140</td><td>56.0</td><td>—</td><td>0.94</td></tr>
  <tr><td style="padding:6px;">Structures**</td><td>250</td><td>—</td><td>—</td><td>30.7</td></tr>
  <tr style="font-weight:bold; background:#f5f5f5;"><td style="padding:6px;">Totals</td><td>879</td><td>64</td><td>+3.1***</td><td>165</td></tr>
  <tr style="font-weight:bold;"><td style="padding:6px;">Constraint</td><td>1,000</td><td>1,100†</td><td>0</td><td>200</td></tr>
  <tr style="font-weight:bold; background:#c7f2c2;"><td style="padding:6px;">Margin</td><td>121</td><td>1,036</td><td>8.3††</td><td>35</td></tr>
  <tr><td style="padding:6px; font-style:italic;">Contingency</td><td>50</td><td>—</td><td>—</td><td>5.19</td></tr>
</table>

<br>

<p style="font-size:0.88em; color:#444; line-height:1.6;">
  * Power figures include duty cycle averaging across the laser operational profile. Negative values indicate draw; positive indicates generation.<br>
  ** Significant uncertainties remain in the structures subsystem and are to be resolved prior to CDR.<br>
  *** Net power balance at 10% laser duty cycle. Peak draw during laser firing is 30 kW; solar array generates 11.4 kW BOL.<br>
  † In practice the volume constraint scales to 1,100/n m³ for n satellites per Starship flight. In two dimensions, the 9 m fairing diameter is the operative sizing driver, applicable primarily to the power subsystem and potentially thermal.<br>
  †† The majority of the power margin reflects conservative overestimates of non-payload subsystem draws. Further modelling prior to CDR may reduce this margin as subsystem power characterisation improves.<br>
  Estimates for subsystems not covered in this paper (ACS, Propulsion, Payload, TT&C, Structures) are provided by project co-authors Zubin Bhaumik and Julius Goldberg.
</p>

</details>

---

<details>
<summary><strong>Procurement and Long Lead Items</strong></summary>

<br>

<ul>
  <li><strong>Li-CFx batteries (18–36 months, sole-source risk):</strong> Only EaglePicher and Saft are credible space-qualified suppliers. Custom 17.1 kWh / 45.6 kg pack requires a new qualification programme with 15-year shelf life verification.</li>
  <li><strong>RHPPC Single Board Computer (12–24 months):</strong> Heritage Honeywell radiation-hardened flight computer with limited ongoing production and a constrained supply chain at ≥100 krad tolerance.</li>
  <li><strong>Solar cell cover glass, 500 µm, 45 m² (12–24 months):</strong> Non-standard thickness — SCHOTT 0787 standard only reaches 150 µm. Qioptiq/Pilkington CMX/CMG extends to 500 µm but requires custom cutting, space screening, and ECSS qualification.</li>
  <li><strong>Photovoltaic panels, 45 m² (18–36 months):</strong> Custom array requiring NRE, radiation qualification at 875 km, and cover glass CIC integration. Spectrolab, AZUR SPACE, and SolAero all have long backlogs.</li>
  <li><strong>Space-qualified supercapacitors, 30 kg bank (12–24 months):</strong> Non-standard at this scale. Most heritage devices are CubeSat-scale; custom assembly and qualification required.</li>
  <li><strong>3D Plus RTIMS Flash SSR (12–18 months):</strong> Space-grade (-IS) screening plus custom 3 mm aluminium spot shielding fabrication required.</li>
</ul>

<table style="width:90%; border:none; text-align:center; margin: 1rem auto;">
  <tr>
    <td style="padding:10px; vertical-align:top;">
      <img src="{{ '/assets/images/Charon-Solar-Glass.png' | relative_url }}"
           alt="Solar Cell Cover Glass"
           style="width:100%; max-width:180px; display:block; margin:auto;">
      <div style="font-size:0.85em; color:#555; margin-top:4px;">Solar cell cover glass (500 µm, SCHOTT/Qioptiq)</div>
    </td>
    <td style="padding:10px; vertical-align:top;">
      <img src="{{ '/assets/images/Charon-Solar-Panel.png' | relative_url }}"
           alt="Photovoltaic Panel"
           style="width:100%; max-width:280px; display:block; margin:auto;">
      <div style="font-size:0.85em; color:#555; margin-top:4px;">Triple-junction photovoltaic panel (NRL concept)</div>
    </td>
  </tr>
</table>

<br>

Three Make/Buy decisions were identified for PDR:
<ol>
  <li><strong>Custom HESS switching controller</strong> — no off-the-shelf space-qualified product exists for this semi-active topology with laser-engagement-aware precharging logic.</li>
  <li><strong>Li-CFx vs. Li-ion battery chemistry</strong> — Li-CFx offers best specific energy but sole-source risk; Li-ion has established flight heritage and broader supply chain. Final selection pending RFQ responses.</li>
  <li><strong>Custom vs. heritage solar array deployment system</strong> — buying and scaling the Psyche mission ROSA heritage system reduces cost and schedule risk; key question is whether scaling to 45 m² triggers full requalification.</li>
</ol>

</details>

---

<details>
<summary><strong>Contributions</strong></summary>

<br>

I was the primary author of the C&DH, Power, and Ground subsystem sections of the SDR. This included requirements derivation, technology selection through weighted trade studies, component sizing, cost and mass estimation, risk assessment, and long lead item / make-buy analysis. The Radiation Protection trade study shielding calculations were developed using data from Kuntepce et al. (2023) as the TID baseline.

The ACS, Propulsion, TT&C, Payload, and Autonomy subsystems were addressed by teammates Zubin Bhaumik and Julius Goldberg. The course was taught by Professor Gregory Falco.

</details>
