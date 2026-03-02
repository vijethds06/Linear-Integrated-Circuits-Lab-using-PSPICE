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



### Conclusion of DC Analysis

The DC operating point confirms that:

- All three transistors (M1, M2, M3) operate in saturation.
- The desired bias current of approximately 200 µA is achieved.
- The output voltage is positioned near mid-supply, allowing reasonable signal swing.
- Power consumption remains well within the specified 1 mW limit.

Hence, the circuit is correctly biased and ready for small-signal amplification.


## Transient Analysis

<img width="1918" height="1078" alt="transient" src="https://github.com/user-attachments/assets/49ae3887-8c17-4d9f-8aa4-34b3c1a2751e" />

### Theoretical Gain Analysis

For a Common Source amplifier with a PMOS active load and a diode-connected NMOS transistor at the source, the voltage gain is given by:

$$
A_v = \frac{-g_{m1} r_{o2}}{1 + \frac{g_{m1}}{g_{m3}}}
$$



### Transconductance Calculation

The transconductance of M1 is:

$$
g_{m1} = \frac{2 I_D}{V_{OV}}
$$

Substituting:

$$
g_{m1} = \frac{2 \times 200 \times 10^{-6}}{0.25}
$$

$$
g_{m1} = 1.6 \times 10^{-3} \; S
$$

Since M3 carries the same drain current:

$$
g_{m3} = 1.6 \times 10^{-3} \; S
$$



### Output Resistance of PMOS (M2)

Assuming channel length modulation:

$$
r_{o2} = \frac{1}{\lambda I_D}
$$

Substituting:

$$
r_{o2} = \frac{1}{0.1 \times 200 \times 10^{-6}}
$$

$$
r_{o2} = 50 \; k\Omega
$$



### Theoretical Voltage Gain

Substituting values:

$$
A_v = \frac{1.6 \times 10^{-3} \times 50 \times 10^{3}}{1 + \frac{1.6 \times 10^{-3}}{1.6 \times 10^{-3}}}
$$

Since:

$$
\frac{g_{m1}}{g_{m3}} = 1
$$

The gain becomes:

$$
A_v = \frac{80}{2}
$$

$$
A_v = 40
$$



### Gain in dB

$$
A_v(dB) = 20 \log_{10}(40)
$$

$$
A_v(dB) = 32.04 \; dB
$$



### Simulated Gain (Transient Analysis)

From the transient waveform measurements:

### Input Peak-to-Peak Voltage

$$
V_{in(p-p)} = 1.2299V - 1.2190V
$$

$$
V_{in(p-p)} = 0.0199V
$$

### Output Peak-to-Peak Voltage

$$
V_{out(p-p)} = 1.3454V - 00.6576V
$$

$$
V_{out(p-p)} = 0.6879V
$$

---

### Simulated Voltage Gain

$$
A_v = \frac{V_{out(p-p)}}{V_{in(p-p)}}
$$

$$
A_v = \frac{0.6879}{0.0199}
$$

$$
A_v \approx 34.567
$$

---

### Simulated Gain in dB

$$
A_v(dB) = 20 \log_{10}(34.567)
$$

$$
A_v(dB) \approx 30.773 \; dB
$$



### Comparison

- **Theoretical Gain** ≈ 40 V/V (32.04 dB)  
- **Simulated Gain** ≈ 25.05 V/V (27.97 dB)

The reduction in simulated gain compared to theoretical gain is primarily due to:

- Finite output resistance of M1  
- Non-ideal behavior of the diode-connected transistor  
- Mobility degradation  
- Body effect  
- Parasitic capacitances included in the 180nm TSMC model  

Thus, the simulation results reasonably validate the theoretical estimation while accounting for practical second-order effects.


### Difference Between Theoretical and Practical Gain

The practical (simulated) voltage gain is lower than the theoretical gain due to non-ideal effects present in real MOSFET models. The theoretical analysis assumes ideal device behavior and simplified small-signal parameters, whereas simulation includes second-order effects.

Finite output resistance of the transistors reduces the effective output resistance at the drain node, thereby lowering the achievable gain. In addition, the diode-connected NMOS introduces stronger source degeneration in practice due to its non-ideal small-signal resistance.

Other factors such as channel length modulation, mobility degradation, body effect, and intrinsic parasitic capacitances further reduce the effective transconductance and output resistance compared to ideal assumptions.

Hence, the observed difference between theoretical and simulated gain is expected and confirms realistic device behavior in CMOS implementations.



##  AC Analysis

<img width="1918" height="1078" alt="ac" src="https://github.com/user-attachments/assets/1a9d1637-37af-4253-8c2f-0a096805d42f" />



The AC small-signal analysis of the Common Source (CS) amplifier with PMOS active load and diode-connected NMOS was carried out to evaluate the frequency response and bandwidth characteristics of the circuit.

From the Bode magnitude plot, the amplifier exhibits a **midband voltage gain of approximately 30.26 dB** (≈ 32.6 V/V), indicating strong small-signal amplification under proper saturation biasing conditions. The gain remains nearly constant across the low and mid-frequency regions, confirming stable biasing and correct amplifier operation.

The **−3 dB cutoff frequency occurs at approximately 49.2 MHz**, which defines the bandwidth of the amplifier. Up to this frequency, the amplifier maintains effective signal amplification with minimal attenuation.

Beyond the cutoff frequency, the gain decreases rapidly due to intrinsic MOSFET parasitic capacitances such as gate-to-drain ($C_{gd}$), gate-to-source ($C_{gs}$), and drain-to-bulk capacitances. These parasitic elements introduce dominant poles at the output node along with the load capacitance, thereby limiting the high-frequency response.

The phase response shows a phase shift approaching **−225° near the cutoff region**, which is consistent with the inverting behavior of a Common Source amplifier along with additional phase lag introduced by higher-order poles.

Overall, the AC analysis confirms that the amplifier achieves high midband gain with a bandwidth extending into the tens of megahertz range, demonstrating proper small-signal amplification performance suitable for low-power analog CMOS applications.

## Conclusion

The Common Source (CS) amplifier employing a PMOS active load and a diode-connected NMOS source device was successfully designed and implemented using TSMC 180 nm CMOS technology in LTSpice while satisfying the specified design constraints of **$V_{DD}=1.8,V$** and **power consumption $P \leq 1,mW$**.

The selected drain current of approximately **200 µA** ensured that the overall power dissipation remained within limits while providing sufficient transconductance for effective amplification. DC operating point analysis verified that all transistors operate in the saturation region, confirming proper biasing and stable small-signal operation.

Transient analysis demonstrated correct amplifier behavior, producing an amplified and inverted output waveform with minimal distortion around the bias point. The diode-connected NMOS provided self-biasing and improved operating point stability through source degeneration, enhancing linearity and robustness against device variations.

Theoretical and simulated gains show reasonable agreement, with minor deviations arising from practical second-order effects such as channel length modulation, body effect, mobility degradation, and intrinsic parasitic capacitances included in the device models.

AC small-signal analysis confirmed a **midband gain of approximately 30 dB** and a **−3 dB bandwidth near 49 MHz**, indicating a wide useful frequency range. The dominant pole observed at higher frequencies is primarily due to the combined effect of load capacitance and MOSFET parasitic capacitances at the output node.

Overall, the designed amplifier satisfies the required power constraint and demonstrates correct biasing, expected gain characteristics, stable frequency response, and reliable small-signal amplification performance suitable for low-power CMOS analog applications.





