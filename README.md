# S‑Parameters — Mismatched Load


---



## 1. Introduction

S‑parameters (scattering parameters) are a way to describe the behaviour of linear RF and microwave networks in terms of incident and reflected travelling waves at ports. They are especially convenient at high frequencies where measuring voltages and currents directly is difficult. When a load is not equal to the system reference impedance (typically 50 Ω), the load is *mismatched* and reflections occur. This README focuses on how mismatched loads affect S‑parameter values and common derived metrics (return loss, VSWR), with practical examples.



<img width="590" height="297" alt="image" src="https://github.com/user-attachments/assets/002e98d7-377a-4a55-9495-62f4a5fc1c1c" />

## 2. Overview

* S‑parameters relate incident waves `a` and reflected waves `b` at each port of a network via the S‑matrix:
  $$\mathbf{b} = \mathbf{S},\mathbf{a}$$
* For a 1‑port network (or measuring port of a 2‑port with the other port terminated), the key parameter is `S11` — the input reflection coefficient seen looking into the port, normalized to the reference impedance (Z_0).
* A perfectly matched load (Z_L = Z_0) produces no reflection: ((ZL - Z0)/(ZL + Z0)), (S_{11} = 0) (or ((or 
−
∞
−∞ dB return) dB return loss). A mismatched load yields ((ZL - Z0)/(ZL + Z0)) and non‑zero S11 (expressible as magnitude and phase).

## 3. Key equations and definitions

### Waves and S‑matrix (two‑port form)

Let `a_i` and `b_i` be the normalized incident and reflected waves at port `i`. For an N‑port network:

$$ b_i = \sum_{j=1}^N S_{ij} a_j $$

In vector form: (\mathbf{b} = \mathbf{S},\mathbf{a}).

### Reflection coefficient (load)

For a load (Z_L) connected to characteristic impedance (Z_0):

$$ \Gamma_L = \frac{Z_L - Z_0}{Z_L + Z_0} $$

If you measure `S11` of a simple one‑port that is just the loaded termination (no other network), then:

$$ S_{11} = \Gamma_L. $$

(If there is additional network between the port and the load, `S11` includes those network effects and is not simply (\Gamma_L).)

### Return loss (RL) and VSWR

* Return loss in dB:

$$ RL = -20\log_{10} |\Gamma| $$

* Voltage Standing Wave Ratio (VSWR):

$$ \text{VSWR} = \frac{1 + |\Gamma|}{1 - |\Gamma|} $$

### Converting between S and Z (for a 2‑port, port‑wise)

Given Z‑parameters referenced to (Z_0) (the general formulas are available in microwave texts). For a single port normalized to (Z_0), the relation between the port impedance (Z_{in}) and (\Gamma) is:

$$ \Gamma = \frac{Z_{in} - Z_0}{Z_{in} + Z_0} $$

### Incident/reflected wave normalization (practical note)

The normalized wave definitions used by network analyzers commonly are:

$$ a = \frac{V + Z_0 I}{2\sqrt{Z_0}} \quad\text{and}\quad b = \frac{V - Z_0 I}{2\sqrt{Z_0}} $$

(These give convenience when forming power-calibrated measurements.)



## 4. Applications

* **Antenna engineering** — ensuring antenna feed matches transmission line impedance to minimize reflected power and maximize radiated power.
* **RF/microwave components** — filters, amplifiers, and mixers must be specified with S‑parameters to guarantee behaviour when connected to other 50 Ω systems.

* <img width="1024" height="1024" alt="image" src="https://github.com/user-attachments/assets/10434e5a-2a3b-4409-872d-360668b88245" />

* **Network analyzer measurements** — S‑parameters are the native language of vector network analyzers (VNAs); mismatched loads require correction or calibration (SOLT, TRL) for accurate de‑embedded S‑parameters.
* **Power delivery & protection** — reflections can increase stress on amplifiers and cause instability; designs include matching networks and isolators to protect equipment.

## 5. Simple analogy
<img width="1024" height="1024" alt="image" src="https://github.com/user-attachments/assets/d5187e2b-7fc7-40dc-8693-c255ccddcf7f" />


Think of the transmission line as a water pipe and the load as a valve at the end. If the valve (load) has the same opening as the pipe (matched), water flows smoothly with no backflow. If the valve is too closed or too wide (mismatched), water sloshes back toward the source — that backflow is like the reflected wave measured by S11.

## 6. Conclusions

* S‑parameters give a compact, measurable description of RF networks using travelling waves.
* A mismatched load causes a nonzero reflection coefficient (\Gamma), which directly appears as non‑zero `S11` for a one‑port termination.
* Use return loss and VSWR to quantify mismatch severity; smaller (|\Gamma|) means better match.
* In practice, VNAs + proper calibration are used to measure S‑parameters and de‑embed the DUT from fixture effects.

## 7. References

**Books (classic textbooks)**

* D. M. Pozar, *Microwave Engineering*, 4th ed., Wiley. (chapters on S‑parameters, network analysis and matching networks)
* R. E. Collin, *Foundations for Microwave Engineering*, 2nd ed., Wiley.
* David K. Cheng, *Field and Wave Electromagnetics* (for basics on waves and impedances).

**Web sources & application notes (good starting points)**

* Keysight (Agilent) application notes on S‑parameters and network analyzer basics (search "Keysight S-parameters application note").
* Rohde & Schwarz application notes on return loss, VSWR, and VNA calibration (search "R&S S-parameter basics").
* National Instruments / NI tutorials on VNAs and scattering parameters.

---

