# Description

This program walk-through documents the orbital maintenance strategy for a spacecraft in a highly elliptical polar orbit around Saturn. The objective was to counteract periapsis precession caused by the planet's oblateness ($J_2$ effect) to ensure a fixed orbital geometry for scientific observation. I chose this problem to explore the complexities of station keeping in non-Earth environments. Saturn's significantly larger $J_2$ term ($0.01629$) provides a rigorous test for orbital perturbation theories, requiring precise maneuver planning to maintain a fixed periapsis.
<br />

**The Mission:** Maintain a fixed periapsis for a spacecraft in a polar orbit with a 22.5-day period and a 1,500 km periapsis altitude.
<br />

**The Challenge:** Saturn’s gravitational irregularities cause a perigee precession ($\Delta\omega$) of approximately $-1.090^{\circ}$ per orbit. Without intervention, the location of the closest approach would drift, compromising the mission's science requirements.

## 2. Orbital Geometry and Perturbation Analysis

The spacecraft follows a highly eccentric elliptical path. I derived the following orbital parameters through MATLAB simulation to define the system:
<br />

* **Periapsis Radius ($r_p$):** $61,830\text{ km}$
* **Apoapsis Radius ($r_a$):** $3,012,188\text{ km}$
* **Eccentricity ($e$):** $0.959773$

<p align="center">
  <img src="https://i.imgur.com/uqvyahq.png" height="80%" width="80%" alt="Saturn Orbital Eccentricity"/>
  <br />
  <i>Figure 1: Visual demonstration of the extreme eccentricity of the orbit</i>
</p>

## 3. Optimization Strategy: Brute Force vs. fmincon

I implemented two distinct numerical methods to find the minimum fuel consumption ($\Delta V$) required to negate this precession.
<br />

* **Method 1: Brute-Force Sweep (Inspection):** I performed a high-density sweep of 20,000 true anomaly ($\theta$) values to calculate the $\Delta V$ required at every possible point in the orbit.
* **Method 2: Optimal Control Theory (fmincon):** I utilized MATLAB’s `fmincon` to solve a constrained optimization problem, minimizing the objective function:

$$J = \sqrt{\Delta v_r^2 + \Delta v_\theta^2}$$

<p align="center">
  <img src="https://i.imgur.com/LzC0Yr4.png" height="80%" width="80%" alt="Delta V Sensitivity Plot"/>
  <br />
  <i>Figure 2: Variation of Delta V required across the orbit, pinpointing the optimal burn location</i>
</p>

## 4. Final Station-Keeping Requirements

The analysis concluded that the $J_2$ effect can be effectively managed with high-precision maneuvers scheduled at the specific true anomaly identified by the optimizer.
<br />

* **Optimal Burn Location:** The maneuver should be applied at a true anomaly of $-162.446^{\circ}$.
* **$\Delta V$ per Orbit:** $81.409\text{ m/s}$.
* **Total $\Delta V$ (2-Year/730-day Mission):** $2,641.284\text{ m/s}$.
* **Burn Components:** The maneuver requires a combination of $19.55\text{ m/s}$ radial and $-79.03\text{ m/s}$ tangential velocity changes.
