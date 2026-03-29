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



# Circuit 2:-



# Circuit Configuration: Differential Amplifier with Active Load (Current Mirror)

The active load configuration is an advanced MOSFET differential amplifier where passive resistive loads are replaced by a **PMOS current mirror**. This design significantly increases output resistance and voltage gain while reducing chip area and improving power efficiency.

---

## 1. Topology and Circuit Architecture
The circuit is composed of three primary functional blocks: the input differential pair, the tail current source, and the active load current mirror.

<img width="1625" height="826" alt="image" src="https://github.com/user-attachments/assets/ea9f4bd3-646c-4a24-bad1-05ed3d290823" />



### A. Input Differential Pair (NMOS)
Consists of two matched NMOS transistors ($M_1, M_2$).
* **Function:** Converts the differential input voltage ($V_{id}$) into a current difference through current steering.
* **Connections:** * **Gates:** Connected to $V_{in1}$ and $V_{in2}$.
    * **Sources:** Coupled at the common tail node $V_p$.
    * **Drains:** Tied to the PMOS active loads ($M_4, M_5$).

### B. Tail Current Source
Implemented using an NMOS transistor ($M_3$).
* **Function:** Provides a constant quiescent current ($I_{SS}$), ensuring stable biasing and high Common-Mode Rejection (CMR).
* **Connections:** Drain to $V_p$, Source to $V_{SS}$, and Gate to a stable bias voltage $V_B$.

### C. Active Load (PMOS Current Mirror)
Consists of two matched PMOS transistors ($M_4, M_5$).
* **Diode-Connected PMOS ($M_4$):** The gate and drain are shorted to establish the reference current from the $M_1$ branch and set the $V_{SG}$ for the mirror.
* **Mirror PMOS ($M_5$):** Mirrors the current from $M_4$ into the $M_2$ branch. This configuration effectively converts the differential current into a high-swing output voltage.

---

## 2. Terminal Mapping

| Terminal | Connection | Function |
| :--- | :--- | :--- |
| **$V_{in1}$** | Gate of $M_1$ | Non-inverting input |
| **$V_{in2}$** | Gate of $M_2$ | Inverting input |
| **$V_{out1}$** | Drain of $M_1/M_4$ | Internal node voltage |
| **$V_{out2}$** | Drain of $M_2/M_5$ | High-gain output node |

---

## 3. Small-Signal Performance

### Voltage Gain ($A_v$)
Because the active load acts as a high-impedance current source rather than a simple resistor, the output resistance ($R_{out}$) is dramatically increased:
$$A_v = -g_m (r_{o,n} \parallel r_{o,p})$$

Where:
* **Transconductance:** $g_m = \frac{2I_D}{V_{ov}}$
* **Output Resistance:** $r_o = \frac{1}{\lambda I_D}$

### Comparison: Resistive vs. Active Load

| Feature | Resistive Load | Active Load |
| :--- | :--- | :--- |
| **Load Element** | Resistor $R_D$ | PMOS Current Mirror |
| **Output Resistance** | Moderate ($R_D \parallel r_o$) | Very High ($r_{o,n} \parallel r_{o,p}$) |
| **Voltage Gain** | Moderate | **High** 🚀 |
| **Silicon Area** | Large (Resistors are bulky) | Compact (Transistor-only) |
| **Efficiency** | Lower | Higher |

---

## 4. Design Insight
In a resistive load, increasing gain requires increasing $R_D$, which eventually limits the DC headroom and forces the transistors out of saturation. By using an **Active Load**, we achieve the equivalent of a massive resistance ($r_o$ is typically in the hundreds of $k\Omega$ to $M\Omega$ range) without the massive DC voltage drop, allowing for high gain even with low supply voltages like $0.9\text{V}$.

## 5. Summary Intuition
The functional flow of this architecture can be summarized as:

**$\text{Voltage Difference} \rightarrow \text{Current Steering} \rightarrow \text{Current Mirroring} \rightarrow \text{High-Gain Voltage Output}$**


# Working Principle: MOSFET Differential Amplifier with Active Load

The MOSFET differential amplifier with an active load operates by steering a constant tail current between two transistors based on the input voltage difference. A PMOS current mirror is utilized to convert this current difference into a high-gain voltage output.

---

## 1. Circuit Architecture
The circuit is composed of three primary sections:
* **Differential Pair ($M_1, M_2$):** Matched NMOS transistors that perform the input voltage-to-current conversion.
* **Tail Current Source ($M_3$):** Supplies a constant quiescent current $I_{SS}$.
* **Active Load ($M_4, M_5$):** A PMOS current mirror that replaces passive resistors to provide high output impedance.

### Fundamental Constraints
* **Current Sum:** $I_{D1} + I_{D2} = I_{SS}$ (The total current is fixed and redistributed).
* **Differential Input:** $V_{id} = V_{in1} - V_{in2}$ (Controls the current split between branches).

---

## 2. Operating Modes

### Common-Mode Operation (Balanced Condition)
When $V_{in1} = V_{in2}$:
* **Equal Biasing:** $V_{GS1} = V_{GS2}$, leading to an even current split: $I_{D1} = I_{D2} = \frac{I_{SS}}{2}$.
* **Mirror Action:** $M_4$ (diode-connected) sets the gate voltage for $M_5$, forcing $I_{D4} = I_{D5}$.
* **Differential Output:** Since the currents and transistor characteristics are matched, $V_{out1} = V_{out2}$, resulting in $V_{out,diff} = 0$.
* **Result:** High Common-Mode Rejection Ratio (CMRR).

### Differential Operation (Current Steering)
When $V_{in1} > V_{in2}$:
1. **Input Effect:** $V_{GS1}$ increases ($\uparrow$) and $V_{GS2}$ decreases ($\downarrow$).
2. **Steering:** $I_{D1}$ increases while $I_{D2}$ decreases to satisfy the $I_{SS}$ constant current constraint.
3. **Mirroring:** The PMOS load $M_5$ mirrors the increased current from $M_1$ ($I_{D5} = I_{D1}$).
4. **Net Output Current:** At the output node ($V_{out2}$), the net current is the difference between the mirrored current and the steered current:
   $$I_{out} = I_{D5} - I_{D2} = I_{D1} - I_{D2}$$

---

## 3. Current-to-Voltage Conversion
The output voltage is the product of the differential current and the output resistance:
$$V_{out} = I_{out} \cdot R_{out}$$
Where:
$$R_{out} = r_{o,n} \parallel r_{o,p}$$

**Design Insight:** Because $r_o$ (intrinsic transistor resistance) is significantly larger than a typical passive resistor $R_D$, even a minor current difference results in a massive voltage swing, leading to very high gain.

---

## 4. Small-Signal vs. Large-Signal Behavior

| Feature | Small-Signal ($|V_{id}| \le \sqrt{2}V_{ov}$) | Large-Signal ($|V_{id}| > \sqrt{2}V_{ov}$) |
| :--- | :--- | :--- |
| **Transistor State** | Both $M_1, M_2$ in Saturation | One transistor in Cutoff |
| **Current Change** | Linear/Smooth | Fully Steered ($I_D \approx I_{SS}$) |
| **Output Shape** | Proportional to Input | Saturated/Clipped |
| **Function** | Linear Amplifier | Switching Behavior |

---

## 5. Summary of Component Roles

| Component | Role |
| :--- | :--- |
| **$M_1, M_2$** | Convert input voltage difference into a current difference. |
| **$M_3$** | Provides constant bias current and improves CMRR. |
| **$M_4, M_5$** | Mirrors current and provides the high-impedance load required for gain. |

---

## 6. Technical Conclusion
The active load configuration is a powerful architecture because it:
1. **Eliminates bulky resistors:** Reduces silicon area.
2. **Maximizes Gain:** Leverages the high output resistance of MOSFETs in saturation.
3. **Enhances Efficiency:** Provides high voltage swing with minimal power consumption.

**Intuition:** The circuit functions as a **$\text{Voltage} \rightarrow \text{Current} \rightarrow \text{Mirrored Current} \rightarrow \text{Large Voltage}$** converter.
# Design Calculations: Differential Amplifier with Active Load

## 1. Design Parameters and Process Constants
The following parameters are utilized for the TSMC 180nm process:

| Parameter | Symbol | Value |
| :--- | :--- | :--- |
| **Supply Voltage (Positive)** | $V_{DD}$ | 0.9 V |
| **Supply Voltage (Negative)** | $V_{SS}$ | -0.9 V |
| **Power Constraint** | $P$ | $\le 1.8\text{ mW}$ |
| **Channel Length** | $L$ | 480 nm |
| **Input/Output CM Voltage** | $V_{ICM} / V_{OCM}$ | 0 V |
| **Tail Node Voltage** | $V_p$ | -0.7 V |
| **Threshold Voltage (NMOS/PMOS)** | $V_{Tn} / V_{Tp}$ | $0.36\text{ V} / -0.36\text{ V}$ |
| **NMOS Process Parameter** | $\mu_n C_{ox}$ | 236.5 $\mu\text{A/V}^2$ |
| **PMOS Process Parameter** | $\mu_p C_{ox}$ | 118 $\mu\text{A/V}^2$ |

---

## 2. Power and Tail Current Allocation
The total power consumption is:
$$P = (V_{DD} - V_{SS}) \cdot I_{SS}$$
$$1.8 \cdot I_{SS} \le 1.8 \times 10^{-3} \implies I_{SS} \le 1\text{ mA}$$

**Design Choice:** $I_{SS} = 1\text{ mA}$ is selected to maximize transconductance.
For a balanced pair: $I_{D1} = I_{D2} = 0.5\text{ mA}$.

---

## 3. NMOS Differential Pair Sizing ($M_1, M_2$)
To maintain $V_p = -0.7\text{ V}$ with $V_{ICM} = 0\text{ V}$:
* **Gate-Source Voltage:** $V_{GS} = V_G - V_S = 0 - (-0.7) = 0.7\text{ V}$
* **Overdrive Voltage:** $V_{OV} = V_{GS} - V_{Tn} = 0.7 - 0.36 = 0.34\text{ V}$
* **Saturation Check:** $V_{DS} = V_D - V_S = 0 - (-0.7) = 0.7\text{ V}$. Since $0.7 > 0.34$, $M_1/M_2$ are in saturation.

**Width Calculation:**
$$W = \frac{2 I_D L}{\mu_n C_{ox} V_{OV}^2} = \frac{2 \cdot 0.5\text{mA} \cdot 480\text{nm}}{236.5\mu\text{A/V}^2 \cdot (0.34)^2} \approx 17.57\ \mu\text{m}$$
*Final tuned width (via simulation):* **$W_n \approx 28.5\ \mu\text{m}$**

---

## 4. PMOS Active Load Sizing ($M_4, M_5$)
The PMOS load must support $0.5\text{ mA}$ per branch with $V_{OCM} = 0\text{ V}$.
* **Source-Gate Voltage:** $V_{SG} = V_{DD} - V_{OCM} = 0.9 - 0 = 0.9\text{ V}$
* **Overdrive Voltage:** $V_{OVp} = V_{SG} - |V_{Tp}| = 0.9 - 0.36 = 0.54\text{ V}$

**Width Calculation:**
$$W = \frac{2 I_D L}{\mu_p C_{ox} V_{OVp}^2} = \frac{2 \cdot 0.5\text{mA} \cdot 480\text{nm}}{118\mu\text{A/V}^2 \cdot (0.54)^2} \approx 13.95\ \mu\text{m}$$
*Final tuned width:* **$W_p \approx 14\ \mu\text{m}$**

---

## 5. Tail Current Source Design ($M_3$)
To sink the full $I_{SS} = 1\text{ mA}$:
* **Gate Bias:** $V_B = -0.2\text{ V}$ (Source is at $V_{SS} = -0.9\text{ V}$)
* **$V_{GS3}$:** $-0.2 - (-0.9) = 0.7\text{ V}$
* **$V_{OV3}$:** $0.7 - 0.36 = 0.34\text{ V}$

**Width Calculation:**
$$W_3 = \frac{2 I_{SS} L}{\mu_n C_{ox} V_{OV3}^2} \approx 35.14\ \mu\text{m}$$
*Final tuned width:* **$W_3 \approx 35\ \mu\text{m}$**

---

## 📊 Final Design Summary

| Transistor | Function | Width ($W$) |
| :--- | :--- | :--- |
| **$M_1, M_2$** | Input Differential Pair | $28.5\ \mu\text{m}$ |
| **$M_3$** | Tail Current Source | $35.0\ \mu\text{m}$ |
| **$M_4, M_5$** | PMOS Active Load | $14.0\ \mu\text{m}$ |

## ✅ Conclusion
The active load differential amplifier was successfully designed within the $1.8\text{ mW}$ power constraint. By replacing resistors with a PMOS current mirror, the design achieves high output impedance and increased gain while maintaining stable saturation across all branches.

# DC Analysis: Active Load Differential Amplifier

## 1. Objective
To verify the DC operating point of the MOSFET differential amplifier with an active load. This analysis ensures that all transistors operate in the saturation region while satisfying the specified power and voltage constraints.

---

## 2. Simulation Setup
The DC operating point was extracted using the LTspice directive `.op` with the following parameters:

| Parameter | Symbol | Value |
| :--- | :--- | :--- |
| **Positive Supply** | $V_{DD}$ | +0.9 V |
| **Negative Supply** | $V_{SS}$ | -0.9 V |
| **Input Voltages** | $V_{in1}, V_{in2}$ | 0 V |
| **Bias Voltage** | $V_B$ | -0.2 V |

### Transistor Dimensions (Final Optimized)
| Transistor | Type | Width ($W$) | Length ($L$) |
| :--- | :--- | :--- | :--- |
| **$M_1, M_2$** | NMOS (Pair) | $48.45\ \mu\text{m}$ | $0.48\ \mu\text{m}$ |
| **$M_3, M_4$** | PMOS (Load) | $50.00\ \mu\text{m}$ | $0.48\ \mu\text{m}$ |
| **$M_5$** | NMOS (Tail) | $90.00\ \mu\text{m}$ | $0.48\ \mu\text{m}$ |

---

## 3. Simulation Results (Operating Point)
<img width="674" height="621" alt="image" src="https://github.com/user-attachments/assets/e7171ad2-f3e1-4242-89c5-29e1e60ec722" />

### Node Voltages
* **$V_{DD}$ / $V_{SS}$:** $0.9\text{ V}$ / $-0.9\text{ V}$
* **Tail Node ($V_p$):** $-0.785\text{ V}$
* **Output Nodes ($V_{out1}, V_{out2}$):** $0.074\text{ V}$

### Quiescent Currents
* **Tail Current ($I_{SS}$):** $0.955\text{ mA}$
* **Branch Currents ($I_{D1}, I_{D2}$):** $0.478\text{ mA}$

---

## 4. Verification of Design Conditions

### A. Current Splitting
$$I_{D1} \approx I_{D2} \approx \frac{I_{SS}}{2}$$
$$0.478\text{ mA} \approx \frac{0.955\text{ mA}}{2} = 0.4775\text{ mA} \quad \text{(Verified } \checkmark\text{)}$$
This confirms proper differential symmetry and balanced operation.

### B. Output Symmetry
$V_{out1} = V_{out2} = 0.074\text{ V}$. The matching of these voltages confirms the effectiveness of the PMOS current mirror and the absence of a DC differential offset.

### C. Saturation Region Check
* **NMOS Pair ($M_1, M_2$):**
  $V_{DS} = V_D - V_S = 0.074 - (-0.785) = 0.859\text{ V}$
  Since $V_{DS} (0.859\text{ V}) > V_{OV} (0.34\text{ V})$, the NMOS transistors are in **Saturation**.
* **PMOS Load ($M_3, M_4$):**
  $V_{SD} = V_S - V_D = 0.9 - 0.074 = 0.826\text{ V}$
  Since $V_{SD} (0.826\text{ V}) > V_{OVp} (0.54\text{ V})$, the PMOS transistors are in **Saturation**.

---

## 5. Comparison: Ideal vs. Simulated Values

| Parameter | Ideal Design | Simulated Result | Deviation |
| :--- | :--- | :--- | :--- |
| **Tail Current ($I_{SS}$)** | $1.0\text{ mA}$ | $0.955\text{ mA}$ | $-4.5\%$ |
| **Tail Voltage ($V_p$ )** | $-0.7\text{ V}$ | $-0.785\text{ V}$ | $-12\%$ |
| **Output Voltage ($V_{out}$)**| $0\text{ V}$ | $0.074\text{ V}$ | $+74\text{ mV}$ |

### Reasons for Deviation
1. **Channel Length Modulation:** Theoretical formulas assume infinite $r_o$; simulation accounts for finite $r_o$ which pulls the DC nodes slightly.
2. **Body Effect & DIBL:** The 180nm model includes Drain-Induced Barrier Lowering, which shifts the threshold voltage based on the $V_{DS}$ of the tail transistor.
3. **Mobility Degradation:** High vertical electric fields in the channel reduce carrier mobility, slightly lowering the expected current.
4. **Sub-threshold Conduction:** BSIM models account for current flow even near $V_T$, affecting the precise $V_{GS}$ required for a given $I_D$.

---

## 6. Final Conclusion
The DC analysis validates that the active load differential amplifier is correctly biased. Despite minor physical deviations, all transistors remain firmly in the saturation region, satisfying the necessary conditions for high-gain linear amplification.



# Transient Analysis: Time-Domain Response

## 1. Objective
To analyze the time-domain response of the MOSFET differential amplifier with an active load and verify its performance in both the linear (small-signal) and non-linear (large-signal) operating regions.

---

## 2. Simulation Setup
The transient analysis was performed using the following LTspice directive:
* **Directive:** `.tran 5m`
* **Input Frequency:** $1\text{ kHz}$ (allows for multiple cycles of observation)

---

## 3. Case 1: Linear Region Analysis (Small-Signal)

### Input Configuration
* **$V_{in1}$ / $V_{in2}$:** $50\text{ mV}$ / $-50\text{ mV}$ (Symmetric Sine)
* **Differential Input ($V_{id}$):** $100\text{ mV}$

### Linearity Verification

<img width="1919" height="900" alt="image" src="https://github.com/user-attachments/assets/ac34964f-02ae-4afd-b2a1-47ba274df782" />

Condition for linear operation: $|V_{id}| < 2V_{OV}$
$$2V_{OV} = 2 \times 0.34 = 0.68\text{ V}$$
$$100\text{ mV} < 680\text{ mV} \quad \checkmark \text{ (Linear Region Verified)}$$

### Measured Results & Gain
| Parameter | Value |
| :--- | :--- |
| **Input Peak-to-Peak ($V_{in,pp}$)** | $100\text{ mV}$ |
| **Output Peak-to-Peak ($V_{out,pp}$)** | $366\text{ mV}$ |
| **Voltage Gain ($A_v$)** | $3.66$ |
| **Gain in dB** | $\approx 11.27\text{ dB}$ |

**Inference:** In this mode, the circuit operates as a high-fidelity linear amplifier. Both NMOS transistors remain in saturation, and the tail current is smoothly distributed between the two branches.

---

## 4. Case 2: Non-Linear Region Analysis (Large-Signal)

### Input Configuration
* **$V_{in1}$ / $V_{in2}$:** $400\text{ mV}$ / $-400\text{ mV}$
* **Differential Input ($V_{id}$):** $800\text{ mV}$

### Linearity Verification
$$800\text{ mV} > 680\text{ mV} \quad \times \text{ (Non-Linear Region)}$$

### Observed Behavior

<img width="1919" height="908" alt="image" src="https://github.com/user-attachments/assets/ae7c6496-d8a3-4524-921e-32d650328b4c" />

* **Waveform Distortion:** The output is heavily distorted and clipped at the peaks.
* **Current Steering:** One transistor carries the full tail current ($I_D \approx I_{SS}$) while the other enters the **cutoff region**.
* **Inference:** The circuit transitions from an amplifier to a **switching device**. Gain becomes non-linear and highly dependent on the input magnitude.

---

## 5. Comparison: Linear vs. Non-Linear Operation

| Parameter | Linear Region | Non-Linear Region |
| :--- | :--- | :--- |
| **Input Magnitude ($V_{id}$)** | $100\text{ mV}$ | $800\text{ mV}$ |
| **Output Waveform** | Pure Sinusoidal | Distorted / Clipped |
| **Gain** | Constant | Variable / Compressed |
| **Transistor State** | Both Saturation | One Cutoff |
| **Current Distribution** | Shared/Balanced | Fully Steered |

---

## 6. Analysis of Deviations
Even in the linear region, slight deviations from ideal behavior occur due to:
1. **Finite Output Resistance:** $R_{out} = r_{o,n} \parallel r_{o,p}$. Finite $r_o$ values in the TSMC 180nm process reduce the achievable gain.
2. **Channel Length Modulation:** Causes variations in drain current as $V_{DS}$ swings.
3. **Mobility Degradation:** High vertical electric fields reduce carrier mobility and transconductance ($g_m$).
4. **Current Mirror Mismatch:** Minor variations in the PMOS mirror load lead to small DC offsets and gain reduction.

---

## 7. Conclusion
The transient response validates the design of the active load differential amplifier. The results confirm that the circuit provides stable, undistorted amplification for signals within the $680\text{ mV}$ limit and correctly exhibits current-steering saturation beyond that threshold.

# AC Analysis: Frequency Response (Active Load)

## 1. Objective
To determine the small-signal voltage gain, bandwidth, and Gain-Bandwidth Product (GBW) of the MOSFET differential amplifier with an active load using frequency-domain simulation.

---

## 2. Simulation Setup
The AC analysis was performed using the following LTspice configuration:

* **Directive:** `.ac dec 10 0.1n 1000G`
* **Input Configuration (Differential):**
  * `Vin1`: DC 0, AC 1
  * `Vin2`: DC 0, AC -1
* **Output Measurement:** The differential output $V(out1) - V(out2)$ is plotted in dB using the expression:
  $$20 \log_{10}(V(out1) - V(out2))$$

---

## 3. Simulation Results

### Midband Gain ($A_v$)
Extracted from the flat region of the Bode plot:
* **Decibel Scale:** $A_v \approx 12\text{ dB}$
* **Linear Scale:** $A_v = 10^{\frac{12}{20}} \approx 3.98 \approx 4\text{ V/V}$

### Bandwidth (BW)
The bandwidth is determined at the $-3\text{ dB}$ point from the midband gain:
* **-3 dB Point:** $12\text{ dB} - 3\text{ dB} = 9\text{ dB}$
* **Cutoff Frequency ($f_H$):** $\approx 1\text{ GHz}$
* **Resulting Bandwidth:** $BW \approx 1\text{ GHz}$

### Gain-Bandwidth Product (GBW)
$$GBW = A_v \times BW$$
$$GBW = 4 \times 1\text{ GHz} = 4\text{ GHz}$$

---

## 4. Observations and Analysis

<img width="1919" height="876" alt="image" src="https://github.com/user-attachments/assets/0cf37c4c-b9f9-40c2-b780-9e30dc3eae37" />


* **Flat Midband:** The gain remains constant across a wide frequency range, indicating stable biasing.
* **Roll-off Behavior:** The response exhibits a single-pole roll-off starting at $1\text{ GHz}$ with a slope of $-20\text{ dB/decade}$.
* **High-Frequency Limits:** The gain decreases at high frequencies due to parasitic effects and internal MOSFET capacitances ($C_{gs}, C_{gd}$).

### Theoretical Comparison
The theoretical gain for an active load is $A_v = g_m (r_{o,n} \parallel r_{o,p})$.

| Parameter | Theoretical | Simulated |
| :--- | :--- | :--- |
| **Gain (V/V)** | $\approx 4\text{--}6$ | $\approx 4$ |
| **Bandwidth** | High | $1\text{ GHz}$ |
| **GBW** | High | $4\text{ GHz}$ |

---

## 5. Reasons for Deviation from Ideal Values
The slight reduction in simulated gain compared to the maximum theoretical potential is due to:
1. **Finite Output Resistance ($r_o$):** Real MOSFETs in the 180nm node have lower $r_o$ than ideal models, which shunts the output.
2. **Channel Length Modulation:** $\lambda$ effects reduce the effective impedance of the PMOS current mirror.
3. **Parasitic Capacitances:** Internal junction and gate capacitances introduce poles that limit the high-frequency reach.
4. **Mobility Degradation:** High vertical electric fields in the channel reduce $g_m$ and consequently lower the midband gain.

---

## 6. Conclusion
The AC analysis confirms that the active load differential amplifier provides a stable midband gain of **$12\text{ dB}$** and a high bandwidth of **$1\text{ GHz}$**. The wide Gain-Bandwidth Product of **$4\text{ GHz}$** validates the efficiency of the active load configuration in providing high-speed performance with minimal silicon area.


# Conclusion: MOSFET Differential Amplifier Analysis (Resistive Load)

The MOSFET differential amplifier with resistive load was successfully designed, simulated, and analyzed under the specified TSMC 180nm constraints. The project demonstrates a robust correlation between theoretical analog design and practical circuit simulation.

---

## 🔑 Key Achievement Summary

### 1. DC Biasing and Power Efficiency
The biasing conditions were verified through DC analysis, ensuring both NMOS transistors operate firmly in the **saturation region**. 
* The selected tail current ($I_{SS} = 1\text{ mA}$) successfully maximized transconductance ($g_m$) while remaining strictly within the **$1.8\text{ mW}$ power constraint**.
* The alignment between calculated and simulated bias points confirms the accuracy of the initial design parameters.

### 2. Transient Performance and Linearity
Transient analysis validated the amplifier’s integrity in the time domain:
* **Linear Region:** For a differential input of $V_{id} = 100\text{mV}$, the circuit produced a sinusoidal, undistorted output with a measured gain of **$A_v \approx 5.74\text{ V/V}$**.
* **Non-Linear Transition:** Simulations confirmed that for larger signals ($|V_{id}| > 2V_{ov}$), the amplifier transitions into non-linear behavior, exhibiting signal clipping and current steering saturation.

### 3. AC Response and High-Frequency Capability
The frequency response analysis highlights the suitability of this design for high-speed applications:
* **Midband Gain:** $15.6\text{ dB}$ ($\approx 6.02\text{ V/V}$)
* **-3dB Bandwidth:** $5.128\text{ GHz}$
* **Gain-Bandwidth Product (GBP):** $\approx 30.87\text{ GHz}$

---

## 🔬 Analysis of Deviations
While the simulation results show high agreement with theoretical models, a small deviation in gain was noted ($4.5\text{ V/V}$ theoretical vs $5.74\text{ V/V}$ simulated). This is attributed to realistic non-ideal effects present in the BSIM simulation models, including:
* **Channel Length Modulation ($\lambda$):** Affecting the final output resistance ($r_o$).
* **Mobility Degradation:** Influencing the effective transconductance at high electric fields.
* **Internal Parasitics:** Intrinsic MOSFET capacitances that influence the high-frequency roll-off.

---

## 🏁 Final Statement
The resistive load differential amplifier serves as a stable, high-bandwidth foundation for analog signal processing. The design provides **moderate gain**, **exceptional bandwidth**, and **predictable linearity**, making it a reliable building block for more complex integrated systems like operational amplifiers and comparators.



# Circuit 3 :-

