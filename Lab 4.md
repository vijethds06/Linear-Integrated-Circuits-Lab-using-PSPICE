# Circuit 1: Differential Amplifier with Resistive Load (Full Analysis)

---

## 1. Circuit Diagram

![Circuit Diagram](https://github.com/user-attachments/assets/30508325-b80d-455f-9d32-5f8e32d9f97b)

---

## 2. DC Analysis (Operating Point Verification)

![DC Operating Point](https://github.com/user-attachments/assets/40f9152b-7a35-4189-ad6d-6e4d4ec00f28)

---

### Observations

* Tail node voltage ≈ -0.7 V
* Output nodes centered around 0 V
* Drain currents are equally distributed
* $I_{D1} \approx I_{D2} \approx 0.5$ mA

---

### Interpretation

* Equal current distribution confirms **perfect symmetry**

* NMOS transistors satisfy:
  $$
  V_{DS} > V_{OV}
  $$
  → ensuring **saturation region operation**

* Tail current source is functioning correctly and maintaining constant current

---

### Inference

* The amplifier is **properly biased**
* It is operating in the **active (linear amplification) region**
* Ready for small-signal amplification

---

### Design Insight

* Proper DC biasing is **critical** because:

  * It determines gain
  * It ensures linear operation
  * It avoids distortion

* Any mismatch here would:

  * Break symmetry
  * Reduce CMRR
  * Introduce offset

---

### Practical Insight

* DC stability ensures:

  * Reliable operation in ICs
  * Temperature tolerance
  * Process variation robustness

---

## 3. Transient Analysis (Time-Domain Behavior)

---

### Case 1: Linear Operation

![Linear Response](https://github.com/user-attachments/assets/b6cb244a-6003-4654-8a8a-12d7725fedb2)

#### Observations

* Output signals are sinusoidal
* Outputs are 180° out of phase
* No clipping observed

---

#### Interpretation

* Both transistors remain in **saturation region**
* Current is smoothly shared between branches
* Linear relationship between input and output exists

---

#### Inference

$$
|V_{id}| < 2V_{OV}
$$

* Circuit operates as a **linear amplifier**
* Gain remains constant

---

#### Design Insight

* Linear region depends strictly on **overdrive voltage**
* Smaller $V_{OV}$ → more sensitive amplifier
* Larger $V_{OV}$ → larger linear range

---

#### Practical Insight

* Used in:

  * Audio amplifiers
  * Sensor interfaces
  * Analog front-ends

---

### Case 2: Non-Linear Operation

![Non Linear Response](https://github.com/user-attachments/assets/2b0497df-ecdf-4477-9c4a-4bd39324a80d)

#### Observations

* Output waveform is clipped
* Peaks are flattened
* Signal distortion is visible

---

#### Interpretation

* One transistor carries full current
* Other transistor enters **cutoff region**
* Current steering becomes extreme

---

#### Inference

$$
|V_{id}| > 2V_{OV}
$$

* Circuit leaves linear region
* Acts like a **switching device**

---

#### Design Insight

* This defines **maximum input signal limit**
* Critical for:

  * Signal integrity
  * Distortion control

---

#### Practical Insight

* This behavior is used in:

  * Comparators
  * Digital switching circuits

---

## 4. Gain Analysis

---

### Observations

* Input peak-to-peak: 100 mV
* Output peak-to-peak: 574.33 mV

---

### Calculation

$$
A_v = \frac{V_{out}}{V_{in}} = 5.74
$$

$$
A_v(dB) = 15.18 dB
$$

---

### Interpretation

* Gain achieved through:

  * Transconductance ($g_m$)
  * Load resistance ($R_D$)

---

### Inference

* Amplifier provides **moderate gain**
* Suitable for general analog amplification

---

### Design Insight

Why simulated gain > theoretical?

* Channel length modulation increases $r_o$
* Width tuning increases $g_m$
* Real models (BSIM) are more accurate

---

### Practical Insight

* Gain is sufficient for:

  * Pre-amplification stages
  * Signal conditioning

---

## 5. AC Analysis (Frequency Domain)

![AC Response](https://github.com/user-attachments/assets/92b2e4c6-caa1-4567-913b-ee74f36af1a9)

---

### Observations

* Flat midband gain
* High-frequency roll-off
* No low-frequency cutoff

---

### Interpretation

* Flat region → stable operation
* Roll-off due to:

  * $C_{gs}$
  * $C_{gd}$
  * Load capacitance

---

### Inference

* Wideband amplifier behavior
* High-speed performance confirmed

---

### Design Insight

* Bandwidth limited by:
  $$
  f_H = \frac{1}{2\pi R_{out} C_L}
  $$

* Trade-off:

  * Higher gain → lower bandwidth

---

### Practical Insight

* Suitable for:

  * RF circuits
  * High-speed analog systems

---

## 6. Final Conclusion (Circuit 1)

* Moderate gain (~15 dB)
* Extremely high bandwidth (~GHz)
* Excellent linear behavior (within limits)

### Final Inference

This circuit provides a **strong foundation** for:

* Analog IC design
* Differential signaling
* High-speed amplification

---

# Circuit 2: Differential Amplifier with Active Load (Current Mirror) — Full Analysis

---

## 1. Circuit Diagram

![Active Load Circuit](https://github.com/user-attachments/assets/ea9f4bd3-646c-4a24-bad1-05ed3d290823)

---

## 2. DC Analysis (Operating Point Verification)

![DC Active Load](https://github.com/user-attachments/assets/e7171ad2-f3e1-4242-89c5-29e1e60ec722)

---

### Observations

* Tail current ≈ 0.955 mA
* Branch currents:
  $$
  I_{D1} \approx I_{D2} \approx 0.478 \text{ mA}
  $$
* Output voltages:
  $$
  V_{out1} = V_{out2} \approx 0.074 \text{ V}
  $$
* Tail node voltage slightly shifted from ideal

---

### Interpretation

* Equal current splitting confirms **proper differential operation**

* PMOS current mirror accurately replicates current

* All transistors satisfy:
  $$
  V_{DS} > V_{OV}
  $$
  → ensuring **saturation region**

* Slight voltage deviation due to:

  * Channel length modulation
  * Finite output resistance

---

### Inference

* Circuit is **correctly biased**
* Active load is functioning effectively
* Suitable for high-gain amplification

---

### Design Insight

* Unlike resistive load:

  * Output resistance is:
    $$
    R_{out} = r_{o,n} \parallel r_{o,p}
    $$

* Since $r_o$ is very large:
  → Gain increases significantly

* Small mismatches in mirror:
  → Can introduce offset

---

### Practical Insight

* This topology is widely used in:

  * Operational amplifiers
  * Analog ICs
  * Differential input stages

---

## 3. Transient Analysis (Time-Domain Behavior)

---

### Case 1: Linear Region

![Linear Active](https://github.com/user-attachments/assets/ac34964f-02ae-4afd-b2a1-47ba274df782)

---

#### Observations

* Output waveform is sinusoidal
* Slight reduction in amplitude compared to Circuit 1
* Symmetry maintained

---

#### Interpretation

* Both NMOS transistors remain in saturation
* Current mirror correctly mirrors current
* Differential output is preserved

---

#### Inference

$$
|V_{id}| < 2V_{OV}
$$

* Circuit behaves as a **linear amplifier**
* Gain is stable but lower than expected

---

#### Design Insight

* Gain reduction due to:

  * Finite $r_o$
  * Current mirror non-idealities
  * Voltage headroom limitations

---

#### Practical Insight

* Still suitable for:

  * Analog signal amplification
  * IC front-end stages

---

### Case 2: Non-Linear Region

![Nonlinear Active](https://github.com/user-attachments/assets/ae7c6496-d8a3-4524-921e-32d650328b4c)

---

#### Observations

* Output waveform is heavily distorted
* Clipping occurs
* Asymmetry appears

---

#### Interpretation

* One transistor carries almost entire current
* Other transistor goes into cutoff
* Current mirror amplifies imbalance

---

#### Inference

$$
|V_{id}| > 2V_{OV}
$$

* Circuit exits linear region
* Behaves like a **current steering switch**

---

#### Design Insight

* Mirror amplifies imbalance → distortion more pronounced
* Large signals reduce linearity drastically

---

#### Practical Insight

* Used in:

  * Comparators
  * Switching circuits

---

## 4. Gain Analysis

---

### Observations

* Input: 100 mV
* Output: 366 mV

---

### Calculation

$$
A_v = 3.66
$$

$$
A_v(dB) \approx 11.27 dB
$$

---

### Interpretation

* Gain depends on:

  * $g_m$ (input pair)
  * $r_o$ (active load)

---

### Inference

* Gain is **moderate**, not maximum theoretical
* Limited by real-world non-idealities

---

### Design Insight

Why gain is not very high (despite theory)?

* Finite output resistance
* Current mirror mismatch
* Voltage headroom constraints

---

### Practical Insight

* Real circuits always show:

  * Lower gain than theory
  * More stable operation

---

## 5. AC Analysis (Frequency Response)

![AC Active Load](https://github.com/user-attachments/assets/0cf37c4c-b9f9-40c2-b780-9e30dc3eae37)

---

### Observations

* Midband gain ≈ 12 dB
* Bandwidth ≈ 1 GHz
* Single-pole roll-off observed

---

### Interpretation

* Dominant pole formed due to:

  * Output resistance
  * Parasitic capacitances

* Gain-bandwidth trade-off evident

---

### Inference

* Circuit provides:

  * Moderate gain
  * High bandwidth

---

### Design Insight

* Increasing gain:
  → increases $R_{out}$
  → reduces bandwidth

* Classic trade-off:
  $$
  Gain \times Bandwidth = Constant
  $$

---

### Practical Insight

* Suitable for:

  * Integrated amplifiers
  * Moderate-speed analog circuits

---

## 6. Final Conclusion (Circuit 2)

* Higher output resistance than Circuit 1
* More compact and efficient design
* Gain limited by practical effects

---

### Final Inference

This circuit demonstrates the **power of active loads** in analog design:

* Replaces bulky resistors
* Increases gain potential
* Improves integration capability

---

### Key Takeaway

The active load differential amplifier is a **core building block of modern analog ICs**, balancing:

* Gain
* Area
* Power efficiency

---
# Circuit 3: Differential Amplifier with PMOS Current Source Load — Full Analysis

---

## 1. Circuit Diagram

![Current Source Load Circuit](https://github.com/user-attachments/assets/f5c6dc77-4463-4040-b333-9b3161931ecd)

---

## 2. DC Analysis (Operating Point Verification)

---

### Observations

* Tail current approximately constant (~1 mA)
* Current splits equally:
  $$
  I_{D1} \approx I_{D2}
  $$
* Output nodes show symmetric voltages
* No noticeable DC offset

---

### Interpretation

* Independent PMOS current sources maintain **constant load current**

* Balanced bias ensures:

  * Symmetrical operation
  * Equal voltage swing

* All transistors satisfy:
  $$
  V_{DS} > V_{OV}
  $$
  → ensuring **saturation region operation**

---

### Inference

* Circuit is **perfectly balanced and stable**
* Fully differential operation achieved
* No bias mismatch present

---

### Design Insight

* Unlike current mirror:

  * No dependency between branches
  * Each side controlled independently

* This improves:

  * Matching accuracy
  * Stability
  * Output symmetry

---

### Practical Insight

* Used in:

  * Precision analog circuits
  * Fully differential amplifiers
  * Instrumentation amplifiers

---

## 3. Transient Analysis (Time-Domain Behavior)

---

### Case 1: Linear Region

#### Observations

* Output waveforms are sinusoidal
* Perfect symmetry between outputs
* No visible distortion

---

#### Interpretation

* Both NMOS devices operate in saturation
* PMOS loads maintain constant current
* Current steering occurs smoothly

---

#### Inference

$$
|V_{id}| < 2V_{OV}
$$

* Circuit operates as a **highly linear amplifier**

---

#### Design Insight

* Independent current sources:
  → Reduce distortion
  → Improve linearity

* No mirror-induced mismatch

---

#### Practical Insight

* Ideal for:

  * High-precision amplification
  * Low-distortion applications

---

### Case 2: Non-Linear Region

#### Observations

* Output waveform shows clipping
* Still maintains symmetry
* Less distortion asymmetry compared to Circuit 2

---

#### Interpretation

* One transistor dominates current
* Other approaches cutoff
* PMOS loads maintain bias stability

---

#### Inference

* Circuit enters **non-linear region**
* However, maintains better symmetry than other circuits

---

#### Design Insight

* Even in non-linear region:
  → Better signal integrity than current mirror

---

#### Practical Insight

* Suitable where:

  * Large signals exist
  * But symmetry is critical

---

## 4. Gain Analysis

---

### Observations

* Gain slightly lower than Circuit 2
* Stable output amplitude

---

### Interpretation

* Gain determined by:
  $$
  A_v = g_m (r_{o,n} \parallel r_{o,p})
  $$

* No mirror amplification factor

---

### Inference

* Gain is **moderate but stable**
* Less sensitive to mismatch

---

### Design Insight

* Trade-off:

  * Lose gain
  * Gain stability and symmetry

---

### Practical Insight

* Preferred in:

  * Precision analog systems
  * Balanced signal processing

---

## 5. AC Analysis (Frequency Response)

---

### Observations

* Flat gain region
* Smooth roll-off
* Stable response

---

### Interpretation

* Dominant pole due to:

  * Output resistance
  * Load capacitance

---

### Inference

* Circuit offers:

  * Stable bandwidth
  * Predictable behavior

---

### Design Insight

* Slightly lower gain → slightly higher bandwidth
* Better stability than Circuit 2

---

### Practical Insight

* Suitable for:

  * High-speed precision circuits

---

## 6. Final Conclusion (Circuit 3)

* Best symmetry among all designs
* Most stable and predictable
* Slightly lower gain but superior linearity

---

### Final Inference

This circuit is ideal when:

* Precision is more important than gain
* Fully differential outputs are required

---

# FINAL COMPARISON OF ALL CIRCUITS

---

## Performance Comparison Table

| Parameter         | Resistive Load    | Active Load (Mirror) | Current Source Load |
| ----------------- | ----------------- | -------------------- | ------------------- |
| Gain              | Moderate (~15 dB) | Moderate (~12 dB)    | Moderate            |
| Bandwidth         | Very High (GHz)   | High                 | High                |
| Output Type       | Differential      | Single-ended         | Fully Differential  |
| Output Resistance | Low               | Very High            | High                |
| Linearity         | Good              | Moderate             | Best                |
| Symmetry          | Moderate          | Moderate             | Excellent           |
| Area              | Large             | Compact              | Compact             |
| Complexity        | Low               | High                 | Medium              |
| Stability         | High              | Moderate             | Very High           |

---

## Deep Comparative Insights

---

### 1. Gain Perspective

* Active Load → Highest theoretical gain
* Resistive Load → Stable gain
* Current Source → Moderate but consistent

---

### 2. Linearity Perspective

* Best → Current Source Load
* Worst → Active Load (due to mirror mismatch)

---

### 3. Bandwidth Perspective

* Best → Resistive Load
* Limited → Active Load

---

### 4. Practical IC Design Perspective

* Most used → Active Load
* Most precise → Current Source
* Most basic → Resistive Load

---

# OVERALL CONCLUSION

---

## Key Engineering Insights

### 1. Trade-Offs Define Design

Every configuration demonstrates a trade-off between:

* Gain
* Bandwidth
* Linearity
* Complexity

---

### 2. No “Best” Circuit

* **Resistive Load:** Best for simplicity and bandwidth
* **Active Load:** Best for integration and gain
* **Current Source Load:** Best for precision and symmetry

---

### 3. Real-World Understanding

* Theoretical models ≠ Practical results
* Non-idealities significantly impact performance

---

## Final Statement

This project successfully demonstrates how **load configuration directly influences amplifier performance**, making it one of the most critical design decisions in analog electronics.

---

## Viva-Ready One-Line Answer

"A differential amplifier’s performance is primarily determined by its load configuration, which governs gain, bandwidth, linearity, and overall efficiency."

---
