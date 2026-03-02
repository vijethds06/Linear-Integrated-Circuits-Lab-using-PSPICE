# Experiment 2(c): CS Amplifier

## Aim

To design and implement a **Common Source (CS) amplifier** using:

- An **NMOS transistor** as the amplifying device  
- A **PMOS transistor as the active load**  
- A **diode-connected NMOS transistor** for bias stabilization  

in **TSMC 180 nm CMOS technology** using LTSpice.

The design operates under the following constraints:

$$
V_{DD} = 1.8V
$$

$$
P \leq 1 \text{ mW}
$$

The objective further includes:

- Verification of the **DC operating point**
- Analysis of **transient response**
- Extraction of **voltage gain**
- Evaluation of **frequency response and bandwidth**

The circuit must ensure proper saturation operation of all transistors while maintaining low power consumption and stable small-signal amplification performance.

## Theory

The Common Source (CS) amplifier is one of the most fundamental single-stage MOSFET amplifier configurations widely used in analog integrated circuit design. In this configuration, the input signal is applied to the **gate**, the output is taken from the **drain**, and the **source** terminal serves as the common reference node.

The CS amplifier is known for providing:

- High voltage gain  
- 180° phase inversion between input and output  
- Good small-signal amplification capability  

In this experiment, the CS amplifier is implemented using:

- **NMOS transistor (M1)** as the amplifying device  
- **PMOS transistor (M2)** as the active load  
- **Diode-connected NMOS transistor (M3)** at the source  

This configuration replaces passive resistors with MOSFET-based elements, making the design fully compatible with CMOS fabrication technology.



### PMOS Active Load (M2)

Instead of using a physical drain resistor, a **PMOS transistor** is employed as an active load.

When operating in the saturation region, M2 provides a high small-signal output resistance:

$$
r_{o2} = \frac{1}{\lambda_p I_D}
$$

The approximate voltage gain of a Common Source amplifier is:

$$
A_v \approx -g_{m1} R_{out}
$$

where:

$$
R_{out} \approx r_{o1} \parallel r_{o2}
$$

Because the PMOS transistor provides a large output resistance compared to an integrated resistor, the achievable voltage gain increases without requiring large chip area or additional power consumption.

Advantages of using a PMOS active load:

- Higher gain compared to resistive load  
- Better integration compatibility  
- Reduced silicon area  
- Improved small-signal performance  



### Diode-Connected NMOS (M3)

In this topology, the source of the amplifying NMOS transistor (M1) is connected to a **diode-connected NMOS transistor (M3)**.

A diode-connected MOSFET has its **gate and drain shorted together**. This forces the device to operate in saturation (for proper biasing conditions).

The small-signal resistance of the diode-connected transistor is:

$$
r_{d3} = \frac{1}{g_{m3} + g_{ds3}}
$$

Since typically:

$$
g_{m3} \gg g_{ds3}
$$

the resistance can be approximated as:

$$
r_{d3} \approx \frac{1}{g_{m3}}
$$

This configuration provides:

- Self-biasing capability  
- Controlled source voltage  
- Improved operating point stability  
- Transistor-based current control  

However, it also introduces **source degeneration**, because the source node is no longer at AC ground.



### Source Degeneration Effect

Due to the finite small-signal resistance of M3, the effective voltage gain of the amplifier becomes:

$$
A_v = \frac{-g_{m1} (r_{o1} \parallel r_{o2})}{1 + g_{m1} r_{d3}}
$$

The denominator term:

$$
(1 + g_{m1} r_{d3})
$$

represents the degeneration introduced by the diode-connected transistor.

Effects of this degeneration:

- Improves bias stability  
- Enhances linearity  
- Reduces sensitivity to process variations  
- Stabilizes operating point  

However, the overall voltage gain is reduced compared to an ideal CS amplifier without degeneration.



### Overall Operation of the Circuit

The Common Source amplifier with PMOS active load and diode-connected NMOS:

- Amplifies small input voltage signals  
- Produces an inverted output signal (180° phase shift)  
- Operates with all transistors in saturation  
- Provides self-biasing through the diode-connected transistor  
- Achieves controlled gain with improved stability  

Compared to a simple CS amplifier:

- Gain is lower due to degeneration  
- Linearity and bias stability are improved  
- The design is more robust to device parameter variations  

This configuration is commonly used in analog integrated circuits where controlled gain, improved stability, and compact CMOS implementation are required.

## Working Principle



The NMOS transistor **M1** operates in the saturation region and functions as the primary amplifying device of the Common Source (CS) amplifier.

When a small AC signal is applied at the input, a variation occurs in the gate voltage, which directly changes the gate-to-source voltage of M1.

The small-signal drain current variation is given by:

$$
i_d = g_{m1} v_{gs1}
$$

where:

- $g_{m1}$ = transconductance of NMOS transistor M1  
- $v_{gs1}$ = small-signal gate-to-source voltage variation  

Thus, a small change in input voltage produces a proportional change in drain current.



### Output Voltage Formation (PMOS Active Load)

The varying drain current flows through the PMOS active load transistor **M2**, which is biased in saturation and provides a large small-signal output resistance.

The resulting output voltage variation at the drain node becomes:

$$
v_{out} = - i_d R_{out}
$$

where:

$$
R_{out} \approx r_{o1} \parallel r_{o2}
$$

Here:

- $r_{o1}$ = output resistance of NMOS transistor M1  
- $r_{o2}$ = output resistance of PMOS transistor M2  

The negative sign indicates a **180° phase inversion**, which is a characteristic feature of the Common Source amplifier.

An increase in input voltage increases the drain current, causing a larger voltage drop across the active load and reducing the output voltage.



### Role of the Diode-Connected NMOS (M3)

The source terminal of M1 is connected to a diode-connected NMOS transistor **M3**, whose gate and drain terminals are shorted together.

Because of this connection, M3 automatically operates in saturation and behaves as a nonlinear resistor that establishes the bias current of the amplifier.

The small-signal resistance offered by M3 is:

$$
r_{d3} = \frac{1}{g_{m3} + g_{ds3}}
$$

Since typically:

$$
g_{m3} \gg g_{ds3}
$$

the resistance may be approximated as:

$$
r_{d3} \approx \frac{1}{g_{m3}}
$$

This resistance appears at the source of M1 and prevents the source node from being an AC ground.



### Source Degeneration Effect

When the drain current of M1 increases, the voltage drop across M3 also increases.

As a result:

- Source voltage rises  
- Effective gate-to-source voltage decreases  

This introduces local negative feedback known as **source degeneration**.

The effective voltage gain becomes:

$$
A_v = \frac{-g_{m1}(r_{o1} \parallel r_{o2})}{1 + g_{m1} r_{d3}}
$$

The denominator term:

$$
(1 + g_{m1} r_{d3})
$$

represents the degeneration introduced by the diode-connected transistor.



### Effect on Amplifier Performance

The diode-connected NMOS provides several advantages:

- Self-adjusting bias current  
- Improved operating point stability  
- Reduced sensitivity to device parameter variations  
- Enhanced linearity of amplification  

However, the degeneration reduces the achievable voltage gain compared to an ideal CS amplifier with the source directly grounded.



### Overall Signal Operation

In summary:

- The input voltage controls the drain current through transconductance action of M1.  
- The PMOS transistor M2 converts this current variation into an output voltage through its large output resistance.  
- The diode-connected NMOS M3 stabilizes the operating point and introduces controlled degeneration at the source.  

Thus, the circuit achieves stable small-signal amplification with controlled gain, improved linearity, and reliable CMOS-compatible biasing suitable for low-power analog integrated circuit applications.


## Circuit Diagram

<img width="1202" height="929" alt="image" src="https://github.com/user-attachments/assets/ebb8d35d-5214-4a23-b9dd-29ac30ac2d14" />

## Design



### Given Parameters

- **Technology** : TSMC 180 nm CMOS  
- **Supply Voltage** :

$$
V_{DD} = 1.8V
$$

- **Power Constraint** :

$$
P \leq 1mW
$$

- **Channel Length** :

$$
L_n = 560nm
$$

- **Threshold Voltage** :

$$
V_{TN} \approx 0.366V
$$

- **Electron Mobility** :

$$
\mu_n = 273.81 \times 10^{-4} \; m^2/Vs
$$

- **Load Capacitance** :

$$
C_L = 10pF
$$

- **Gate Oxide Thickness** :

$$
t_{ox} = 4.1 \times 10^{-9} m
$$



### Power Constraint

The total power consumed by the circuit is:

$$
P = V_{DD} I_D
$$

Since:

$$
P \leq 1 \times 10^{-3} W
$$

Maximum allowable drain current becomes:

$$
I_D \leq \frac{1 \times 10^{-3}}{1.8}
$$

$$
I_D \leq 555.5 \mu A
$$

To remain safely within limits while maintaining reasonable gain:

$$
I_D = 200 \mu A
$$

Power dissipated:

$$
P = 1.8 \times 200 \mu A
$$

$$
P = 0.36 mW
$$

Since:

$$
0.36mW < 1mW
$$

the power constraint is satisfied.



## 3.2 Bias Point Selection

Assumed overdrive voltage:

$$
V_{OV} = 0.25V
$$

---

### NMOS M1 Bias

For M1:

$$
V_{GS1} = V_{OV} + V_{TN}
$$

$$
V_{GS1} = 0.25 + 0.366
$$

$$
V_{GS1} = 0.61V
$$

Since M3 is diode-connected:

$$
V_{S1} = V_{GS3}
$$

$$
V_{S1} = 0.61V
$$

Therefore, input gate voltage becomes:

$$
V_{IN} = V_{GS1} + V_{S1}
$$

$$
V_{IN} = 0.61 + 0.61
$$

$$
V_{IN} = 1.22V
$$



### Output Voltage Selection

For near-symmetrical output swing in this configuration:

$$
V_{OUT} = \frac{V_{DD}}{2} + V_{DS3}
$$

$$
V_{OUT} = 0.9 + 0.61
$$

$$
V_{OUT} = 1.51V
$$

Drain-to-source voltage of M1:

$$
V_{DS1} = V_{OUT} - V_{S1}
$$

$$
V_{DS1} = 1.51 - 0.61
$$

$$
V_{DS1} = 0.90V
$$

Since:

$$
V_{DS1} > V_{OV}
$$

M1 operates in saturation.

---

### NMOS M3 (Diode-Connected) Bias

For M3:

$$
V_{GS3} = V_{OV} + V_{TN}
$$

$$
V_{GS3} = 0.61V
$$

Since M3 is diode-connected:

$$
V_{DS3} = V_{GS3}
$$

$$
V_{DS3} = 0.61V
$$

Since:

$$
V_{DS3} > V_{OV}
$$

M3 operates in saturation.



### PMOS M2 Bias

For PMOS M2:

$$
V_{SG2} = V_{OV} + |V_{TP}|
$$

$$
V_{SG2} = 0.25 + 0.39
$$

$$
V_{SG2} = 0.64V
$$

Drain-to-source voltage:

$$
V_{SD2} = V_{DD} - V_{OUT}
$$

$$
V_{SD2} = 1.8 - 1.51
$$

$$
V_{SD2} = 0.29V
$$

Since:

$$
V_{SD2} > V_{OV}
$$

M2 operates in saturation.

Thus, all three transistors operate in saturation ensuring proper amplifier operation.



### Width Calculation

The drain current in saturation is given by:

$$
I_D = \frac{1}{2} \mu C_{ox} \frac{W}{L} (V_{OV})^2
$$

Rearranging:

$$
W = \frac{2 I_D L}{\mu C_{ox} (V_{OV})^2}
$$

Given:

$$
I_D = 200 \mu A
$$

$$
L = 560nm
$$

$$
V_{OV} = 0.25V
$$



### NMOS M1 Width

For NMOS:

$$
W_{M1} =
\frac{2 \times 200 \times 10^{-6} \times 560 \times 10^{-9}}
{2.365 \times 10^{-4} \times (0.25)^2}
$$

$$
W_{M1} \approx 15.15 \mu m
$$

After tuning in simulation to obtain exact:

$$
I_D = 200 \mu A
$$

Final width:

$$
W_{M1} = 75.75 \mu m
$$



### NMOS M3 Width

Since M3 also carries the same current:

$$
W_{M3} \approx 15.15 \mu m
$$

After tuning:

$$
W_{M3} = 75.75 \mu m
$$



### PMOS M2 Width

For PMOS:

$$
W_{M2} =
\frac{2 \times 200 \times 10^{-6} \times 560 \times 10^{-9}}
{9.98 \times 10^{-5} \times (0.25)^2}
$$

$$
W_{M2} \approx 35.86 \mu m
$$

After tuning:

$$
W_{M2} = 57.25 \mu m
$$



Thus, transistor widths were refined through simulation to compensate for non-ideal second-order effects while maintaining the desired drain current and proper saturation conditions.


## DC Analysis

<img width="1918" height="1078" alt="dc" src="https://github.com/user-attachments/assets/be182e8d-0612-4e24-add7-d7da8a604db4" />

## DC Operating Point Analysis (Lab 2c)

From the DC operating point results, the supply voltage is:

$$
V_{DD} = 1.8V
$$

The input bias voltage is:

$$
V_{IN} = 1.22V
$$

The output node settles at:

$$
V_{OUT} \approx 0.903V
$$

---

### NMOS M1 Analysis

The source voltage of M1 is approximately:

$$
V_{S1} \approx 0.5419V
$$

Thus, the gate-to-source voltage becomes:

$$
V_{GS1} = V_{IN} - V_{S1}
$$

$$
V_{GS1} = 1.22 - 0.5419
$$

$$
V_{GS1} \approx 0.678V
$$

Given:

$$
V_{TN} \approx 0.366V
$$

The overdrive voltage is:

$$
V_{OV1} = V_{GS1} - V_{TN}
$$

$$
V_{OV1} \approx 0.678 - 0.366
$$

$$
V_{OV1} \approx 0.312V
$$

Drain-to-source voltage:

$$
V_{DS1} = V_{OUT} - V_{S1}
$$

$$
V_{DS1} = 0.903 - 0.5419
$$

$$
V_{DS1} \approx 0.361V
$$

Since:

$$
V_{DS1} > V_{OV1}
$$

M1 operates in the saturation region.

---

### Diode-Connected NMOS M3

Because M3 is diode-connected:

$$
V_{DS3} = V_{GS3}
$$

From simulation:

$$
V_{GS3} \approx 0.5419V
$$

Since:

$$
V_{DS3} > V_{OV}
$$

M3 also operates in saturation and properly establishes the bias current.

---

### PMOS Active Load M2

The PMOS gate voltage is:

$$
V_G = 1.16V
$$

Source is at:

$$
V_S = 1.8V
$$

Thus:

$$
V_{SG2} = 1.8 - 1.16
$$

$$
V_{SG2} = 0.64V
$$

This satisfies the overdrive requirement for PMOS operation in saturation.

---

### Drain Current Verification

The simulated drain current is approximately:

$$
I_D \approx 199 \mu A
$$

Power consumption:

$$
P = V_{DD} \times I_D
$$

$$
P = 1.8 \times 199\mu A
$$

$$
P \approx 0.358mW
$$

Since:

$$
0.358mW < 1mW
$$

the power constraint is satisfied.

---

## Conclusion of DC Analysis

The DC operating point confirms that:

- All three transistors (M1, M2, M3) operate in saturation.
- The desired bias current of approximately 200 µA is achieved.
- The output voltage is positioned near mid-supply, allowing reasonable signal swing.
- Power consumption remains well within the specified 1 mW limit.

Hence, the circuit is correctly biased and ready for small-signal amplification.

