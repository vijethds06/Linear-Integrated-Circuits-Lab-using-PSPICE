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
##
<img width="1143" height="732" alt="image" src="https://github.com/user-attachments/assets/30508325-b80d-455f-9d32-5f8e32d9f97b" />
---
# Design Calculations

## 1. Given Parameters
The following specifications are used for the TSMC 180 nm process node:

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
| **Process Parameter** | $\mu_n C_{ox}$ | 236.5 µA/V² |

---

## 2. Power and Current Constraints
The total power consumption is determined by the total supply rail and the tail current ($I_{SS}$):

$$P = (V_{DD} - V_{SS}) \cdot I_{SS}$$

Given $V_{DD} - V_{SS} = 1.8$ V and $P \le 1.8$ mW:
$$1.8 \cdot I_{SS} \le 1.8 \times 10^{-3}$$
$$I_{SS} \le 1 \text{ mA}$$

**Design Choice:** We choose $I_{SS} = 1$ mA to maximize transconductance ($g_m$).
For a balanced differential pair, the quiescent drain current for each transistor is:
$$I_{D1} = I_{D2} = \frac{I_{SS}}{2} = 0.5 \text{ mA}$$

---

## 3. Load Resistance Calculation ($R_D$)
To maintain the required output common-mode voltage ($V_{OCM} = 0$ V):

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
The transistors are confirmed to be operating in the **Saturation Region**.

---

## 5. Transistor Sizing ($W/L$)

### Theoretical Calculation
Using the square-law current equation for saturation:
$$I_D = \frac{1}{2} \mu_n C_{ox} \frac{W}{L} (V_{OV})^2$$

Rearranging for $W$:
$$W = \frac{2 I_D L}{\mu_n C_{ox} (V_{OV})^2}$$

Substituting the values:
* $I_D = 0.5$ mA
* $L = 480$ nm
* $\mu_n C_{ox} = 236.5$ µA/V²
* $V_{OV} = 0.34$ V

**Theoretical Width ($W_{calc}$):** $\approx 17.57$ µm



### Simulation-Based Refinement
The theoretical width serves as a first-order approximation. Real-world device physics (Channel Length Modulation, Mobility Degradation, and Short-Channel Effects) require fine-tuning to maintain the exact bias point ($V_p = -0.7$ V).

**Final Fine-Tuned Width ($W_{final}$):** $\approx 28.475$ µm

---

## 6. Design Insights
* **Width Tuning:** Increasing $W$ increases drain current for a fixed $V_{GS}$. Tuning $W$ in LTspice ensures the specific $V_p$ node voltage is achieved despite second-order effects.
* **Power Efficiency:** The design operates exactly at the $1.8$ mW limit to provide the highest possible gain-bandwidth product within the given constraints.
