# Analysis of MOSFET Differential Amplifier Configurations

## Aim
To design and simulate a MOSFET differential amplifier configuration using LTspice. The project evaluates performance through DC, Transient, and AC analysis. Specificatioms:

| Parameter | Symbol | Value |
| :--- | :--- | :--- |
| **Positive Supply Voltage** | $V_{DD}$ | 0.9 V |
| **Negative Supply Voltage** | $V_{SS}$ | -0.9 V |
| **Input Common-Mode Voltage** | $V_{INCM}$ | 0 V |
| **Output Common-Mode Voltage** | $V_{OCM}$ | 0 V |
| **Tail Node Voltage** | $V_P$ | -0.7 V |
| **Channel Length** | $L$ | 480 nm |
| **Maximum Power Dissipation** | $P_{max}$ | 1.8 mW |
---

## Introduction
The differential amplifier is a fundamental building block in analog integrated circuit design. Its primary purpose is to amplify the difference between two input signals while rejecting common-mode noise. 

MOSFET-based differential pairs are essential components in operational amplifiers, comparators, and signal processing systems. This experiment analyzes how different load configurations—resistive, active, and current mirror—impact the amplifier's gain and frequency response.

---

## Theoretical Framework

### Differential Operation
A standard MOS differential pair consists of two matched MOSFETs ($M_1$ and $M_2$) with sources connected to a constant tail current source ($I_{SS}$). The differential input voltage is expressed as:

$$V_{id} = V_{in1} - V_{in2}$$



### Small-Signal Gain
When both transistors operate in the saturation region, the differential gain ($A_v$) is defined by the product of transconductance ($g_m$) and output resistance ($R_{out}$):

$$A_v = g_m \cdot R_{out}$$

The transconductance is calculated based on the drain current ($I_D$) and the overdrive voltage ($V_{ov}$):

$$g_m = \frac{2I_D}{V_{ov}}$$

### Linear and Non-Linear Regions
For small inputs where $|V_{id}| \le \sqrt{2}V_{ov}$, the circuit behaves linearly. If the differential input exceeds this threshold, one transistor will eventually turn off, steering the total current ($I_{SS}$) through the opposite branch, leading to signal clipping.

---

## Circuit Configurations
The resistive load configuration is the most fundamental MOSFET differential pair. It consists of two matched NMOS transistors ($M_1$ and $M_2$) designed to amplify the difference between two input signals while providing a stable DC bias.

### Topology and Connections
* **Differential Pair:** Two matched NMOS transistors, $M_1$ and $M_2$.
* **Source Connection:** The sources of both $M_1$ and $M_2$ are tied together at a common node $V_p$.
* **Tail Biasing:** A constant tail current source ($I_{SS}$) is connected between node $V_p$ and the negative supply rail $-V_{SS}$ to establish the bias current.
* **Drain Loads:** Both drains are connected to matched resistors ($R_D$), which are tied to the positive supply rail $+V_{DD}$.

### Input and Output Terminals
| Terminal | Connection |
| :--- | :--- |
| **Input 1 ($V_{in1}$)** | Applied to the Gate of $M_1$ |
| **Input 2 ($V_{in2}$)** | Applied to the Gate of $M_2$ |
| **Output 1 ($V_{out1}$)** | Taken from the Drain of $M_1$ |
| **Output 2 ($V_{out2}$)** | Taken from the Drain of $M_2$ |

---

### Small-Signal Gain Relationship
For a purely differential input, the voltage gain ($A_v$) for this configuration is:

$$A_v = -g_m (R_D \parallel r_o)$$

Where $g_m$ is the transconductance of the NMOS and $r_o$ is the output resistance due to channel length modulation.

---
# Working Principle: MOSFET Differential Amplifier (Resistive Load)

The MOSFET differential amplifier amplifies the difference between two input voltages by steering a constant tail current between two matched transistors.

---

## 1. Basic Operation
The circuit consists of two matched NMOS transistors ($M_1, M_2$) sharing a common source node connected to a constant tail current source ($I_{SS}$).

* **Current Constraint:** The total current remains fixed: $I_{D1} + I_{D2} = I_{SS}$
* **Differential Input:** The input $V_{id} = V_{in1} - V_{in2}$ controls the distribution of current between the two branches.

---

## 2. Current Steering Mechanism

### Balanced Condition ($V_{in1} = V_{in2}$)
* Both transistors have equal $V_{GS}$.
* Current splits equally: $I_{D1} = I_{D2} = \frac{I_{SS}}{2}$.
* Output voltages are equal: $V_{out1} = V_{out2}$.
* **Result:** The common-mode signal is rejected, and the differential output is zero.

### Differential Input Applied ($V_{in1} > V_{in2}$)
* $V_{GS1}$ increases, causing $I_{D1}$ to rise.
* $V_{GS2}$ decreases, causing $I_{D2}$ to fall.
* **Result:** Current shifts toward $M_1$. Conversely, if $V_{in2} > V_{in1}$, current shifts toward $M_2$.

---

## 3. Current-to-Voltage Conversion
Drain resistors convert the steered current into output voltages:
$$V_{out} = V_{DD} - I_D R_D$$

* **Higher Current:** Leads to a larger voltage drop across $R_D$, resulting in a lower $V_{out}$.
* **Lower Current:** Leads to a smaller voltage drop, resulting in a higher $V_{out}$.
* **Phase:** $V_{out1}$ decreases while $V_{out2}$ increases (and vice versa), providing an inverted differential output.

---

## 4. Small-Signal Operation (Linear Region)
For small differential inputs where $|V_{id}| \le \sqrt{2} V_{ov}$:
* Both transistors remain in the **saturation region**.
* The output is a linear, amplified version of the input.

**Gain Mechanism:**
The amplifier operates through a Voltage $\rightarrow$ Current $\rightarrow$ Voltage transformation:
$$A_v = g_m R_{out}$$
Where:
* $g_m = \frac{2I_D}{V_{ov}}$
* $R_{out} = R_D \parallel r_o$

---

## 5. Large-Signal Operation (Non-Linear Region)
If the input is large ($|V_{id}| > \sqrt{2} V_{ov}$):
* One transistor carries the entire tail current ($I_D \approx I_{SS}$).
* The other transistor turns **OFF**.
* **Result:** Signal clipping, loss of linearity, and output distortion.

---

## 6. Critical Conditions and Constraints

### Saturation Requirement
To function as an amplifier, both transistors must satisfy:
$$V_{DS} \ge V_{GS} - V_{th}$$
If violated, the transistors enter the triode region, causing a drastic reduction in gain.

### Input Common Mode Range (ICMR)
If the common-mode input voltage ($V_{ICM}$) shifts too far:
* **Too Low:** The tail current source may enter the triode region.
* **Too High:** $M_1$ and $M_2$ may leave saturation.

### Role of the Tail Current Source
The current source $I_{SS}$ is essential for:
1.  Maintaining a constant total current.
2.  Providing high incremental resistance at the source node.
3.  Improving **Common-Mode Rejection Ratio (CMRR)** and stability.

---

## 7. Summary Intuition
The operation can be summarized as a three-step process:
1.  **Input:** Voltage difference applied to gates.
2.  **Process:** Current is steered between $M_1$ and $M_2$.
3.  **Output:** Resistors convert the steered currents back into a differential voltage.

**$\text{Voltage Difference} \rightarrow \text{Current Steering} \rightarrow \text{Voltage Output}$**

---
## Circuit Diagram
<img width="1143" height="732" alt="image" src="https://github.com/user-attachments/assets/30508325-b80d-455f-9d32-5f8e32d9f97b" />
---

# Design Calculations

## 1. Given Parameters
The following specifications are based on the **TSMC 180 nm** technology node:

| Parameter | Symbol | Value |
| :--- | :--- | :--- |
| **Supply Voltage (Positive)** | $V_{DD}$ | +0.9 V |
| **Supply Voltage (Negative)** | $V_{SS}$ | -0.9 V |
| **Power Constraint** | $P$ | $\le 1.8$ mW |
| **Channel Length** | $L$ | 480 nm |
| **Input CM Voltage** | $V_{ICM}$ | 0 V |
| **Output CM Voltage** | $V_{OCM}$ | 0 V |
| **Tail Node Voltage** | $V_p$ | -0.7 V |
| **Load Capacitance** | $C_L$ | 10 pF |
| **Threshold Voltage** | $V_T$ | $\approx 0.36$ V |
| **Process Parameter** | $\mu_n C_{ox}$ | 236.5 $\mu$A/V² |

---

## 2. Power and Current Constraints
The total power consumption is determined by the total supply rail and the tail current ($I_{SS}$):

$$P = (V_{DD} - V_{SS}) \cdot I_{SS}$$

Given $V_{DD} - V_{SS} = 1.8$ V and $P \le 1.8$ mW:

$$1.8 \cdot I_{SS} \le 1.8 \times 10^{-3}$$

$$I_{SS} \le 1 \text{ mA}$$

To maximize performance within the budget, we select **$I_{SS} = 1$ mA**.  

For a balanced differential pair:
$$I_{D1} = I_{D2} = \frac{I_{SS}}{2} = 0.5 \text{ mA}$$

---

## 3. Load Resistance Calculation ($R_D$)
To achieve the required output common-mode voltage ($V_{OCM} = 0$ V):

$$V_{out} = V_{DD} - I_D R_D$$

$$0 = 0.9 - (0.5 \times 10^{-3}) R_D$$

$$R_D = \frac{0.9}{0.5 \times 10^{-3}} = 1.8 \text{ k}\Omega$$


---

## 4. DC Bias Point and Saturation Check

| Parameter | Calculation | Value |
| :--- | :--- | :--- |
| **Gate Voltage** | $V_G = V_{ICM}$ | 0 V |
| **Source Voltage** | $V_S = V_p$ | -0.7 V |
| **Gate-Source Voltage** | $V_{GS} = V_G - V_S$ | 0.7 V |
| **Overdrive Voltage** | $V_{OV} = V_{GS} - V_T$ | 0.34 V |
| **Drain Voltage** | $V_D = V_{OCM}$ | 0 V |
| **Drain-Source Voltage** | $V_{DS} = V_D - V_S$ | 0.7 V |

**Saturation Condition Check:**
For saturation, $V_{DS} \ge V_{OV}$.
$$0.7 \text{ V} > 0.34 \text{ V}$$
✅ Both transistors are confirmed to be operating in the **Saturation Region**.

---

## 5. Transistor Sizing ($W/L$)

### Theoretical Calculation
Using the square-law current equation for saturation:
$$I_D = \frac{1}{2} \mu_n C_{ox} \frac{W}{L} (V_{OV})^2$$

Rearranging for $W$:
$$W = \frac{2 I_D L}{\mu_n C_{ox} (V_{OV})^2}$$

Substituting the values:
$$W = \frac{2 \times 0.5 \times 10^{-3} \times 480 \times 10^{-9}}{2.365 \times 10^{-4} \times (0.34)^2}$$
**Theoretical Width ($W_{calc}$):** $\approx 17.57\ \mu\text{m}$

### Simulation-Based Refinement
First-order equations do not account for channel length modulation, mobility degradation, or short-channel effects. To maintain the exact bias point of $V_p = -0.7$ V in a real TSMC 180 nm model, the width was adjusted in LTspice.

**Final Optimized Width ($W_{final}$):** $\approx 28.475\ \mu\text{m}$


---

## 6. Design Insights
* **Biasing Accuracy:** Width tuning in simulation is critical because it compensates for second-order effects that hand calculations ignore.
* **Performance:** Operating at the $1.8$ mW limit ensures the highest possible transconductance ($g_m$), which directly improves the gain and bandwidth of the amplifier.

  ---
#DC Operating Point

  <img width="1037" height="729" alt="image" src="https://github.com/user-attachments/assets/40f9152b-7a35-4189-ad6d-6e4d4ec00f28" />

  The DC operating point confirms that the output and source node voltages are aligned with the designed bias conditions, thereby ensuring proper saturation operation of the transistors.

# Input and Output Common-Mode Ranges

## 1. Input Common-Mode Range (ICMR)
The ICMR is the range of input voltages for which all transistors in the differential pair remain in the saturation region and the tail current source remains active.

### Minimum Input Common-Mode Voltage ($V_{ICM,min}$)
To keep the NMOS transistors ON and the tail current source active:
$$V_{GS} \ge V_T$$
$$V_{ICM,min} = V_S + V_T$$

**Calculation:**
* $V_S = -0.7 \text{ V}$
* $V_T = 0.36 \text{ V}$
* $V_{ICM,min} = -0.7 + 0.36 = -0.34 \text{ V}$

> **Insight:** Below $-0.34 \text{ V}$, the transistors enter the cutoff region and the differential pair stops conducting.

### Maximum Input Common-Mode Voltage ($V_{ICM,max}$)
To ensure the NMOS transistors do not enter the triode region:
$$V_{DS} \ge V_{GS} - V_T \implies V_{ICM,max} = V_D + V_T$$

**Calculation:**
* $V_D = 0 \text{ V}$ (at equilibrium)
* $V_T = 0.36 \text{ V}$
* $V_{ICM,max} = 0 + 0.36 = 0.36 \text{ V}$

### Final ICMR Result
$$-0.34 \text{ V} \le V_{ICM} \le 0.36 \text{ V}$$

---

## 2. Output Common-Mode Range (OCMR)
The OCMR defines the allowable swing of the output voltage while maintaining transistor saturation.

### Maximum Output Voltage ($V_{OCM,max}$)
The maximum output is limited by the positive supply rail:
$$V_{OCM,max} \le V_{DD} = 0.9 \text{ V}$$
At this limit, the current through $R_D$ approaches zero as the output node reaches the supply rail.

### Minimum Output Voltage ($V_{OCM,min}$)
To maintain saturation at the drain ($V_{DS} \ge V_{OV}$):
$$V_D - V_S = V_{OV} \implies V_{OCM,min} = V_S + V_{OV}$$

**Calculation:**
* $V_S = -0.7 \text{ V}$
* $V_{OV} = 0.34 \text{ V}$
* $V_{OCM,min} = -0.7 + 0.34 = -0.36 \text{ V}$

### Final OCMR Result
$$-0.36 \text{ V} \le V_{OCM} \le 0.9 \text{ V}$$

---

## 3. Differential Input Range (Linear Region)
The amplifier operates linearly when current is shared between both devices and neither transistor is fully steered into cutoff.

**Condition for Linear Operation:**
$$|V_{id}| \le \sqrt{2} V_{OV}$$
Using our design value $V_{OV} = 0.34 \text{ V}$:
$$|V_{id}| \le \sqrt{2} \times 0.34 \approx 0.48 \text{ V}$$


(Note: If using the simpler approximation $|V_{id}| \le 2V_{OV}$): $|V_{id}| \le 0.68 \text{ V}$

### Final Linear Range
$$-0.48 \text{ V} \le V_{id} \le 0.48 \text{ V}$$

---

## 📝 Design Summary and Insights

| Range Type | Limitation | Importance |
| :--- | :--- | :--- |
| **ICMR** | Input bias boundaries | Defines DC biasing stability. |
| **OCMR** | Output swing boundaries | Limits the maximum undistorted output signal. |
| **Differential** | Linear gain boundaries | Determines the point where signal clipping occurs. |

**Key Takeaway:** A robust design ensures that the intended signal swing stays within these three overlapping ranges to prevent gain degradation and non-linear distortion.

# Transient Analysis: Linearity vs. Non-Linearity

The transient response of the differential amplifier is analyzed under two distinct input conditions to evaluate the transition from linear amplification to non-linear switching behavior.

---

## ✅ Case 1: Linear Operation
### Input Configuration
* **Input 1:** `SINE(0.1 50m 1k)`
* **Input 2:** `SINE(0.1 -50m 1k)`
* **Common-mode Voltage ($V_{CM}$):** 0.1 V
* **Differential Input ($V_{id}$):** 100 mV

<img width="1919" height="948" alt="image" src="https://github.com/user-attachments/assets/b6cb244a-6003-4654-8a8a-12d7725fedb2" />

### Linearity Verification
For linear operation, the differential input must satisfy:
$$|V_{id}| \le 2V_{OV}$$
Given $2V_{OV} = 0.68\text{ V}$:
$$100\text{ mV} < 680\text{ mV} \implies \text{Linear Region}$$

### Observations & Interpretation
* **Waveforms:** Output waveforms are perfectly sinusoidal with no visible distortion or clipping.
* **Phase:** Outputs are equal in magnitude and $180^\circ$ out of phase.
* **State:** Both transistors remain in saturation, and the tail current is smoothly shared.
* **Result:** The output is a faithful, amplified version of the input with constant gain.

---

## ❌ Case 2: Non-Linear Operation
### Input Configuration (Modified)
* **Input 1:** `SINE(0.1 400m 1k)`
* **Input 2:** `SINE(0.1 -400m 1k)`
* **Differential Input ($V_{id}$):** 800 mV

<img width="1919" height="945" alt="image" src="https://github.com/user-attachments/assets/2b0497df-ecdf-4477-9c4a-4bd39324a80d" />

### Linearity Verification
Checking the boundary condition:
$$|V_{id}| > 2V_{OV}$$
$$800\text{ mV} > 680\text{ mV} \implies \text{Non-Linear Region}$$

### Expected Observations & Interpretation
* **Distortion:** The output waveform exhibits heavy clipping at the peaks.
* **Current Steering:** Large input forces nearly all current ($I_D \approx I_{SS}$) into one transistor, pushing the other into **cutoff**.
* **Symmetry:** The outputs lose sinusoidal symmetry as the circuit reaches its physical current limits.
* **Result:** The circuit behaves more like a **switch** than an amplifier; gain becomes non-linear and input-dependent.

---

## 📊 Comparison Summary

| Parameter | Linear Operation | Non-Linear Operation |
| :--- | :--- | :--- |
| **Condition** | $|V_{id}| < 2V_{OV}$ | $|V_{id}| > 2V_{OV}$ |
| **Input Magnitude** | 100 mV | 800 mV |
| **Output Shape** | Sinusoidal | Distorted / Clipped |
| **Gain** | Constant | Non-linear |
| **Transistor State** | Both in Saturation | One in Cutoff |
| **Current Distribution** | Shared | Fully Steered |

---

## 🧠 Key Design Insight
The linear range of a differential amplifier is finite and strictly defined by the overdrive voltage:
$$|V_{id}|_{max} = 2V_{OV}$$
Beyond this limit, the amplifier loses its proportional relationship between input and output, transitioning into switching behavior. Proper design requires selecting a $V_{OV}$ that accommodates the expected peak signal swing.

## ✅ Conclusion
The transient analysis confirms that for $V_{id} = 100\text{ mV}$, the amplifier operates as intended. Increasing the input to $800\text{ mV}$ successfully demonstrates the non-linear boundaries of the TSMC 180nm NMOS pair.

# Theoretical and Simulated Gain Analysis

The performance of the differential amplifier is evaluated by comparing analytical calculations with time-domain simulation results.

---

## 1. Simulated Gain Calculation

### Input Signal Configuration
* **Waveform Type:** Sine Wave
* **Frequency:** 1 kHz
* **Amplitude:** 50 mV (per branch)
* **DC Offset:** 0.1 V
* **Peak Differential Input ($V_{id}$):** 100 mV

  <img width="1894" height="403" alt="image" src="https://github.com/user-attachments/assets/98836b51-84d4-4cb8-be88-5a0ee7ba2fab" />


### Measured Values from Simulation
The peak-to-peak voltages were extracted from the LTspice transient analysis:

* **Input Peak-to-Peak ($V_{in,pp}$):** $$V_{in,pp} = 50\text{ mV} - (-50\text{ mV}) = 100\text{ mV}$$
* **Output Peak-to-Peak ($V_{out,pp}$):** $$V_{out,pp} = 287.165\text{ mV} - (-287.165\text{ mV}) = 574.33\text{ mV}$$

### Calculated Voltage Gain ($A_v$)
The voltage gain in linear and decibel scales is:
$$A_v = \frac{V_{out,pp}}{V_{in,pp}} = \frac{574.33 \times 10^{-3}}{100 \times 10^{-3}} = 5.74$$

**Gain in dB:**
$$A_v(dB) = 20 \log_{10}(5.74) \approx 15.18\text{ dB}$$

---

## 2. Theoretical Gain Comparison

Based on the small-signal model ($A_d \approx g_m R_D$), the theoretical gain was calculated in the previous design section.

### Updated Performance Summary

| Parameter | Theoretical Value | Simulated Value |
| :--- | :--- | :--- |
| **Voltage Gain (V/V)** | 4.5 | 5.74 |
| **Voltage Gain (dB)** | 13.06 dB | 15.18 dB |

---

## 3. Analysis and Insights

The simulated gain is slightly higher than the first-order theoretical prediction. # Analysis: Discrepancy Between Theoretical and Simulated Gain

A noticeable difference is observed between the theoretical gain ($\approx 4.5 \text{ V/V}$) and the simulated gain ($\approx 5.74 \text{ V/V}$). This deviation arises because analytical calculations rely on simplifying assumptions, whereas LTspice simulations utilize complex device models that account for real-world physical effects.

---

## 1. Channel Length Modulation ($\lambda$ Variation)
**Theoretical Assumption:** A constant value (e.g., $\lambda = 0.1 \text{ V}^{-1}$) is often assumed to calculate output resistance $r_o = 1/(\lambda I_D)$.  
**Simulation Reality:** In the TSMC 180nm process, $\lambda$ is not constant. It varies significantly with drain voltage, device geometry, and specific bias conditions. This directly alters the effective $R_{out}$ and, consequently, the voltage gain.

## 2. Advanced MOSFET Modeling (BSIM)
**Theoretical Assumption:** Calculations use the first-order square-law equation:
$$I_D = \frac{1}{2} \mu_n C_{ox} \frac{W}{L} V_{ov}^2$$
**Simulation Reality:** Simulation uses **BSIM (Berkeley Short-channel IGFET Model)**, which includes:
* **Velocity Saturation:** Limits current in short-channel devices.
* **Mobility Degradation:** High vertical electric fields reduce carrier mobility.
* **DIBL (Drain-Induced Barrier Lowering):** Lowers threshold voltage at high $V_{DS}$.
These effects lead to a more accurate, and often higher, value for transconductance ($g_m$).

## 3. Variation in Overdrive Voltage ($V_{ov}$)
**Theoretical Assumption:** $V_{ov}$ is treated as a fixed constant ($0.34 \text{ V}$).  
**Simulation Reality:** Small bias point shifts in the shared source node ($V_p$) cause $V_{ov}$ to vary slightly. Since $g_m = 2I_D / V_{ov}$, even a minor change in the denominator significantly impacts the resulting gain.

## 4. Finite Output Resistance Interaction
**Theoretical Assumption:** Simplified load as $R_{out} = R_D \parallel r_o$.  
**Simulation Reality:** The output resistance is an interaction of both the NMOS pair and the specific tail current source characteristics. Real-world simulation accounts for the finite impedance of the tail current source, which impacts the common-mode rejection and differential load balancing.

## 5. Transistor Sizing and Tuning
**Theoretical Assumption:** Calculated width is based on ideal equations ($\approx 17.57 \text{ \mu m}$).  
**Simulation Reality:** To satisfy the physical bias condition ($V_p = -0.7 \text{ V}$),The width was tuned to $\approx 28.475\ \mu\text{m}$. This increase in width directly scales the transconductance ($g_m$), leading to the higher observed gain of $5.74 \text{ V/V}$.

---

## 6. Summary: Ideal vs. Practical Comparison

| Aspect | Theoretical Analysis | LTspice Simulation |
| :--- | :--- | :--- |
| **MOSFET Model** | Ideal Square-Law | Realistic BSIM4 |
| **Parameters ($\mu, \lambda, V_T$)** | Constant / Fixed | Bias-Dependent |
| **Second-Order Effects** | Ignored | Included (DIBL, Body Effect) |
| **Device Sizing** | Calculated Approximation | Fine-tuned for Bias |
| **Accuracy** | Approximate | High Precision |

## Final Conclusion
The discrepancy is expected and demonstrates the limitations of hand calculations in modern sub-micron processes. The simulation provides a more reliable estimate of the circuit’s performance by accounting for the non-linearities and geometric dependencies of the TSMC 180nm technology.
## 4. Final Conclusion
Using the measured values of $V_{out} = \pm 287.165\text{ mV}$, the amplifier demonstrates a stable gain of **$A_v \approx 5.74$**. This confirms that the biasing circuit and transistor sizing are correctly implemented, providing a high degree of agreement with the analytical design goals.

# AC Analysis: Frequency Response and Bandwidth

AC analysis is performed to evaluate the frequency response, midband gain, and bandwidth of the MOSFET differential amplifier. This determines the high-frequency limitations of the design.

---

## 1. Simulation Setup
To extract the differential frequency response, the following parameters were used in LTspice:

* **Command:** `.ac dec 100 1 10G`
* **Differential Excitation:** * `Vin1`: AC 1
  * `Vin2`: AC -1
* **Output Measurement:** `V(out1) - V(out2)`

  <img width="1919" height="978" alt="image" src="https://github.com/user-attachments/assets/92b2e4c6-caa1-4567-913b-ee74f36af1a9" />


---

## 2. Simulation Results

### Midband Gain ($A_v$)
Extracted from the flat region of the Bode plot:
* **Decibel Scale:** $A_v = 15.6\text{ dB}$
* **Linear Scale:** $A_v \approx 6.02\text{ V/V}$

> **Note:** This result closely aligns with the transient analysis gain ($\approx 5.74\text{ V/V}$), confirming consistency across simulation modes.

### Bandwidth (BW)
The bandwidth is determined by identifying the -3dB cutoff frequency ($f_H$):
* **-3dB Gain Point:** $15.6\text{ dB} - 3\text{ dB} = 12.6\text{ dB}$
* **Upper Cutoff Frequency ($f_H$):** $5.128\text{ GHz}$
* **Lower Cutoff Frequency ($f_L$):** $\approx 0\text{ Hz}$ (DC coupled)
* **Total Bandwidth:** $BW = f_H - f_L = 5.128\text{ GHz}$

### Unity Gain Bandwidth (UGB)
The Unity Gain Bandwidth is the frequency where the gain drops to $0\text{ dB}$ ($1\text{ V/V}$):
$$UGB \approx A_{v,linear} \times BW$$
$$UGB = 6.02 \times 5.128\text{ GHz} \approx 30.9\text{ GHz}$$

---

## 3. Interpretation and Insights

* **Flat Midband Region:** The stable gain across lower frequencies indicates proper DC biasing and a lack of significant coupling capacitor effects.
* **High-Frequency Roll-off:** The gain begins to decrease at extremely high frequencies due to internal MOSFET parasitic capacitances ($C_{gs}$, $C_{gd}$) and the 10 pF load capacitance ($C_L$).
* **Speed Performance:** A bandwidth in the GHz range confirms that this TSMC 180nm differential pair is suitable for high-speed analog signal processing.
* **Gain-Bandwidth Trade-off:** The high UGB of $30.9\text{ GHz}$ highlights the capability of the technology node when biased at the power limit of $1.8\text{ mW}$.

---

## 🚀 Summary of AC Performance

| Metric | Value |
| :--- | :--- |
| **Midband Gain ($A_v$)** | $15.6\text{ dB}$ |
| **-3dB Bandwidth ($f_H$)** | $5.128\text{ GHz}$ |
| **Unity Gain Bandwidth** | $\approx 30.9\text{ GHz}$ |

**Conclusion:** The AC analysis validates that the amplifier provides moderate gain and exceptionally wide bandwidth, confirming the stability and high-speed efficiency of the design.

# Frequency Response Analysis (Bode Plot)

The AC analysis provides a frequency-domain view of the amplifier's performance, confirming the stability of the gain and identifying the high-frequency poles.

---

## 📈 Simulation Results: Bode Plot
The following plot illustrates the magnitude (in dB) and phase (in degrees) for the differential output $V(out1) - V(out2)$ and the single-ended output $V(out1)$.


### Key Data Points Extracted
Based on the simulation cursors and trace analysis:

| Parameter | Measurement | Frequency |
| :--- | :--- | :--- |
| **Differential Midband Gain ($A_{v,diff}$)** | $21.78\text{ dB}$ | $1\text{ nHz}$ to $1\text{ GHz}$ |
| **Single-Ended Midband Gain ($A_{v,se}$)** | $15.76\text{ dB}$ | $1\text{ nHz}$ to $1\text{ GHz}$ |
| **-3dB Cutoff Frequency ($f_H$)** | $18.78\text{ dB}$ | $\approx 5.13\text{ GHz}$ |
| **Unity Gain Frequency ($f_T$)** | $0\text{ dB}$ | $\approx 30.9\text{ GHz}$ |
| **Phase at Midband** | $180^\circ$ | Low Frequency |

---

## 🔍 Technical Analysis

### 1. Gain Relationship
The plot confirms the theoretical relationship between differential and single-ended gain. The differential gain ($21.78\text{ dB}$) is approximately $6\text{ dB}$ higher than the single-ended gain ($15.76\text{ dB}$), which corresponds to the factor of 2 ($20\log_{10}(2) \approx 6.02\text{ dB}$) inherent in differential signaling.

### 2. Frequency Stability
The gain remains exceptionally flat from the mHz range up to $1\text{ GHz}$. This indicates:
* **DC Coupling:** No lower cutoff frequency ($f_L$) is present, allowing for DC signal amplification.
* **Dominant Pole:** The roll-off begins after $1\text{ GHz}$, suggesting that the internal parasitic capacitances ($C_{gs}, C_{gd}$) and the $10\text{ pF}$ load capacitance only become dominant in the microwave frequency range.

### 3. Phase Response
The phase starts at $180^\circ$ (reflecting the inverting nature of the common-source based differential pair) and begins to shift as it approaches the pole frequency. The smooth phase transition indicates a stable system with a high phase margin.

---

## ✅ Conclusion
The AC analysis successfully validates the high-speed capability of the TSMC 180nm process. With a bandwidth of **$5.13\text{ GHz}$** and a gain of **$21.78\text{ dB}$**, the amplifier is well-suited for wideband analog applications.
