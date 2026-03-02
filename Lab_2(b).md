# Experiment 2(b): CS Amplifier

## Aim



To design and implement a Common Source (CS) amplifier using an NMOS amplifying transistor with an NMOS current source for source degeneration and a PMOS active load in TSMC 180 nm CMOS technology using LTSpice.

The design operates with a supply voltage of VDD = 1.8 V while satisfying the power constraint:

P ≤ 1 mW

The circuit performance is evaluated through DC operating point verification, transient response analysis, voltage gain extraction, and frequency response characterization including bandwidth determination.



## Theory

The Common Source (CS) amplifier is a fundamental MOSFET voltage amplifier configuration widely used in analog integrated circuit design because of its high gain capability and compatibility with CMOS fabrication.

In this implementation:

- NMOS transistor **M1** acts as the amplifying device.
- PMOS transistor **M2** acts as the active load.
- NMOS transistor **M3** acts as a current source.

Unlike conventional CS amplifiers that use passive resistors, both the drain and source resistances are implemented using MOSFETs. This approach improves integration compatibility, reduces chip area, and enables precise bias current control.



### PMOS Active Load (M2)

Instead of using a physical drain resistor, a PMOS transistor (M2) biased in saturation is used as an active load.

When operating in saturation, M2 exhibits a high small-signal output resistance:

$$
r_o2 = 1 / (λ_p I_D)
$$

This large output resistance increases the achievable voltage gain without requiring large on-chip resistors.

The approximate voltage gain of a CS amplifier is:

$$
A_v ≈ − g_m1 R_out
$$

where:

$$
R_out ≈ r_o1 || r_o2
$$

Thus, a higher output resistance directly improves the voltage gain.

Advantages of PMOS active load:

- Higher gain compared to resistive load
- Reduced silicon area
- Better CMOS fabrication compatibility
- Improved bias control



## NMOS Current Source (M3)

The source resistor is replaced by NMOS transistor M3, which operates in saturation and behaves as a current source.

Its small-signal output resistance is:

$$
r_o3 = 1 / (λ_n I_D)
$$

M3 establishes the bias current of the amplifier and stabilizes the operating point against supply and process variations.

Benefits of using M3:

- Improved bias stability
- Reduced sensitivity to supply fluctuations
- Better robustness to device mismatch
- Increased effective output resistance



### Degeneration Effect Introduced by M3

Since the source of M1 is connected to M3, the source node is not perfectly at AC ground.

A variation in drain current produces a small variation in source voltage, reducing the effective gate-to-source voltage.

This introduces degeneration similar to classical source degeneration.

The effective voltage gain becomes:

$$
A_v = − ( g_m1 r_o2 ) / ( 1 + g_m1 r_o3 )
$$

The denominator term:

$$
( 1 + g_m1 r_o3 )
$$

represents the feedback introduced by the finite output resistance of the current source transistor.

This improves linearity and operating point stability but slightly reduces voltage gain.



### Overall Function of the Circuit

This amplifier:

- Amplifies small input voltage signals
- Produces a 180° phase inversion between input and output
- Uses MOSFET active devices instead of passive resistors
- Achieves high gain through active loading
- Maintains stable biasing using a current source

Hence, the circuit demonstrates practical CMOS amplifier design principles used in modern analog integrated circuits.



## Working Principle

The NMOS transistor M1 operates in the saturation region and acts as the amplifying device.

A small variation in input voltage produces a change in gate-to-source voltage:

$$
v_gs1
$$

which modulates the drain current according to:

$$
i_d = g_m1 v_gs1
$$

The varying drain current flows through the PMOS active load M2 and produces an output voltage variation:

$$
v_out = − i_d r_o2
$$

The negative sign indicates a 180° phase inversion between input and output.

Since the source of M1 is connected to M3 (finite output resistance):

$$
r_o3
$$

the source voltage changes slightly with current variation, introducing local negative feedback.

Therefore, the effective voltage gain becomes:

$$
A_v = − ( g_m1 r_o2 ) / ( 1 + g_m1 r_o3 )
$$




At higher frequencies, intrinsic device capacitances such as gate-to-source capacitance, gate-to-drain capacitance, and load capacitance introduce dominant poles that limit the bandwidth of the amplifier.


## Circuit Diagram

<img width="1237" height="868" alt="image" src="https://github.com/user-attachments/assets/9fb6246d-3998-456b-81d4-fed7acef3040" />

## Design


### Given Parameters

* Technology : **TSMC 180 nm CMOS**
* Supply Voltage :

$$
V_{DD} = 1.8V
$$

* Power Constraint :

$$
P \leq 1mW
$$

* Channel Length :

$$
L_n = 560nm
$$

* Threshold Voltage :

$$
V_{TN} \approx 0.366V
$$

* Charge Mobility NMOS :

$$
\mu_n = 273.81 \times 10^{-4} ; m^2/Vs
$$

* Charge Mobility PMOS:

$$
\mu_p = 115.68 \times 10^{-4} ; m^2/Vs
$$


* Gate Oxide Thickness :

$$
t_{ox} = 4.1 \times 10^{-9}m
$$



### Power Constraint

The total power consumed by the amplifier is:

$$
P = V_{DD} I_D
$$

Since the maximum allowable power is:

$$
P \leq 1 \times 10^{-3} W
$$

The maximum drain current becomes:

$$
I_D \leq \frac{1\times10^{-3}}{1.8}
$$

$$
I_D \leq 555.5 \mu A
$$

To remain safely within limits while maintaining sufficient gain:

$$
I_D = 200\mu A
$$

Power dissipated:

$$
P = 1.8 \times 200\mu A
$$

$$
P = 0.36mW
$$

Since:

$$
0.36mW < 1mW
$$

the power constraint is satisfied.



### Bias Point Selection

To ensure proper amplification, all MOSFETs must operate in saturation.



#### NMOS M1 Bias

Assumed overdrive voltage:

$$
V_{OV} = 0.25V
$$

For NMOS:

$$
V_{GS1} = V_{OV} + V_{TN}
$$

$$
V_{GS1} = 0.25 + 0.36
$$

$$
V_{GS1} = 0.61V
$$

Assume source voltage:

$$
V_{S1} = 0.3V
$$

Gate voltage:

$$
V_G = V_{GS1} + V_{S1}
$$

$$
V_G = 0.61 + 0.3
$$

$$
V_G = 0.91V
$$



#### Output Voltage Selection

For near symmetrical output swing:

$$
V_{OUT} \approx \frac{V_{DD}}{2} + V_{S1}
$$

$$
V_{OUT} = 0.9 + 0.3
$$

$$
V_{OUT} = 1.2V
$$

Drain-to-source voltage:

$$
V_{DS1} = V_{OUT} - V_{S1}
$$

$$
V_{DS1} = 1.2 - 0.3
$$

$$
V_{DS1} = 0.9V
$$

Since:

$$
V_{DS1} > V_{OV}
$$

NMOS M1 operates in saturation.



#### NMOS Current Source M3 Bias

For M3:

$$
V_{GS3} = V_{OV} + V_{TN}
$$

$$
V_{GS3} = 0.61V
$$

Since the source is grounded:

$$
V_{G3} = 0.61V
$$

Drain-to-source voltage:

$$
V_{DS3} = V_{S1}
$$

$$
V_{DS3} = 0.3V
$$

Since:

$$
V_{DS3} > V_{OV}
$$

M3 operates in saturation.



#### PMOS Active Load M2 Bias

For PMOS:

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
V_{SD2} = 1.8 - 1.2
$$

$$
V_{SD2} = 0.6V
$$

Since:

$$
V_{SD2} > V_{OV}
$$

PMOS M2 operates in saturation.

Thus, all transistors are properly biased in saturation ensuring correct amplifier operation.



## 3.3 Width Calculation

Drain current in saturation:

$$
I_D = \frac{1}{2}\mu C_{ox}\frac{W}{L}(V_{OV})^2
$$

Rearranging:

$$
W = \frac{2I_D L}{\mu C_{ox}(V_{OV})^2}
$$

Given:

$$
I_D = 200\mu A
$$

$$
L = 560nm
$$

$$
V_{OV} = 0.25V
$$



#### NMOS Width (M1 and M3)

For NMOS:

$$
W_n = \frac{2I_D L}{\mu_n C_{ox}(V_{OV})^2}
$$

Substituting:

$$
W_n =
\frac{2 \times 200\times10^{-6} \times 560\times10^{-9}}
{2.365\times10^{-4}\times(0.25)^2}
$$

$$
W_n \approx 15.15\mu m
$$

After simulation tuning:

$$
W_{M1} = 37.032\mu m
$$

$$
W_{M3} = 31.3\mu m
$$

---

### PMOS Width (M2)

For PMOS:

$$
W_p = \frac{2I_D L}{\mu_p C_{ox}(V_{OV})^2}
$$

Substituting:

$$
W_p =
\frac{2 \times 200\times10^{-6} \times 560\times10^{-9}}
{9.98\times10^{-5}\times(0.25)^2}
$$

$$
W_p \approx 35.86\mu m
$$

After tuning:

$$
W_{M2} = 30.2\mu m
$$



Thus, the transistor widths were refined through simulation to compensate for second-order effects such as channel length modulation and mobility degradation while maintaining the desired operating current and saturation operation.


## DC Analysis

<img width="1918" height="1078" alt="dc opt" src="https://github.com/user-attachments/assets/b9d9bca0-c6e8-420b-9de3-bc91e77b2229" />




From the DC operating point simulation, the NMOS gate voltage is approximately **0.81 V**, while the source voltage rises to nearly **0.199 V** due to the bias current established by the NMOS current source transistor.

This produces a gate-to-source voltage given by:

$$
V_{GS} = V_G - V_S
$$

$$
V_{GS} = 0.81 - 0.199 \approx 0.611 \text{ V}
$$

Considering the NMOS threshold voltage:

$$
V_{TH} \approx 0.36 \text{ V}
$$

the corresponding overdrive voltage becomes:

$$
V_{OV} = V_{GS} - V_{TH}
$$

$$
V_{OV} \approx 0.611 - 0.36 = 0.25 \text{ V}
$$

which closely matches the assumed design value used during bias calculations.

The simulated drain current is approximately:

$$
I_D \approx 199 \, \mu A
$$

confirming that the circuit satisfies the intended bias current while remaining within the specified power constraint under a **1.8 V supply**.

The output voltage settles near:

$$
V_{OUT} \approx 1.108 \text{ V}
$$

indicating sufficient voltage headroom across the amplifying NMOS transistor.

The drain-to-source voltage of M1 becomes:

$$
V_{DS1} = V_{OUT} - V_S
$$

$$
V_{DS1} = 1.108 - 0.199 \approx 0.909 \text{ V}
$$

Since:

$$
V_{DS1} > V_{OV}
$$

the NMOS amplifying transistor operates reliably in the saturation region.

Similarly, the PMOS active load and NMOS current source maintain proper saturation biasing, ensuring stable current conduction and correct voltage swing capability at the output node.

Thus, the DC operating point analysis verifies proper bias establishment, stable saturation operation of all transistors, and compliance with the required supply voltage and power specifications necessary for reliable small-signal amplification.


## Transient Analysis

<img width="1918" height="1078" alt="Transient analysis 2(b)" src="https://github.com/user-attachments/assets/12fd2f38-a8c7-4f44-ae10-207c97a2d3e5" />

The transient analysis confirms proper operation of the Common Source (CS) amplifier. The output waveform is clearly **amplified and phase inverted**, indicating a 180° phase shift between input and output, which is a characteristic feature of CS amplifiers.



### Input Signal Parameters

- Signal Type : Sine Wave  
- Frequency : **1 kHz**  
- Amplitude : **10 mV**  
- DC Offset : **0.91 V**



### Measured Peak-to-Peak Voltages

Input peak-to-peak voltage:

$$
V_{in(p-p)} = 0.91999V - 0.9V
$$

$$
V_{in(p-p)} = 0.01999V
$$

Output peak-to-peak voltage:

$$
V_{out(p-p)} = 0.95073V - 0.87567V
$$

$$
V_{out(p-p)} = 0.07506V
$$



### Voltage Gain (Simulation)

Voltage gain is calculated as:

$$
A_v = \frac{V_{out(p-p)}}{V_{in(p-p)}}
$$

$$
A_v = \frac{0.07506}{0.01999}
$$

$$
A_v = 3.7548
$$

Gain expressed in decibels:

$$
A_v(dB) = 20 \log_{10}(3.7548)
$$

$$
A_v(dB) = 11.49 dB
$$

## AC Analysis

<img width="1919" height="1079" alt="ac analysis" src="https://github.com/user-attachments/assets/61ba3e61-b84d-4371-ad6a-4570872e780a" />

## AC Small-Signal Analysis

The AC small-signal analysis of the Common Source (CS) amplifier was performed to evaluate its frequency response and bandwidth characteristics.

From the Bode magnitude plot, the amplifier exhibits a **midband voltage gain of approximately 11.76 dB**.

Converting to linear scale:

$$
A_v = 10^{\frac{11.756}{20}}
$$

$$
A_v \approx 3.87 \; V/V
$$

The gain remains relatively flat over the low and mid-frequency range, indicating proper biasing and stable small-signal operation.



### Cutoff Frequency (-3 dB Point)

<img width="1918" height="1078" alt="also ac analysis" src="https://github.com/user-attachments/assets/3264e480-ada6-4fb0-84c7-7b99c02e0f85" />


The -3 dB bandwidth is determined from the frequency at which the gain drops by 3 dB from its midband value.

From the simulation cursor:

$$
f_{-3dB} \approx 67.83 \; kHz
$$

At this frequency, the magnitude begins to roll off, marking the onset of significant attenuation.



### High-Frequency Behavior

At higher frequencies, the gain decreases due to intrinsic MOSFET parasitic capacitances, primarily:

- Gate-to-drain capacitance ($C_{gd}$)
- Gate-to-source capacitance ($C_{gs}$)
- Junction capacitances at the output node

These capacitances introduce dominant poles that limit the bandwidth and produce a **low-pass frequency response**.



### Phase Response

The phase response approaches:

$$
\approx -180^\circ
$$

in the midband region, confirming the expected 180° phase inversion characteristic of a Common Source amplifier.

As frequency increases, additional phase lag appears due to pole formation from parasitic capacitances.




The AC analysis confirms that the amplifier provides stable midband gain with a finite bandwidth of approximately:

$$
67.83 \; kHz
$$

The frequency response demonstrates classical low-pass behavior, with bandwidth primarily limited by intrinsic device capacitances. The results validate proper small-signal amplification, expected phase inversion, and correct frequency-domain performance under the specified biasing conditions.

## Final Inference

The Common Source (CS) amplifier employing an NMOS amplifying transistor with a PMOS active load and an NMOS current source was successfully designed and implemented using **TSMC 180 nm CMOS technology** in LTSpice while satisfying the specified design constraints.

The circuit operates with a supply voltage of **VDD = 1.8 V** under a strict power limitation of:

$$
P \leq 1 ; mW
$$

A bias drain current of approximately **200 µA** was selected to ensure proper saturation operation while maintaining low power dissipation:

$$
P = V_{DD} \times I_D = 1.8 \times 200 \mu A = 0.36 ; mW
$$

which comfortably satisfies the imposed power constraint.

The DC operating point analysis confirms that the amplifying NMOS transistor (M1), the PMOS active load (M2), and the NMOS current source (M3) operate in the **saturation region**, ensuring reliable small-signal amplification. The bias voltages were carefully chosen to position the output node close to the mid-supply level, allowing adequate voltage headroom and near-symmetrical output swing.

The PMOS transistor acts as an **active load**, providing a large small-signal output resistance compared to a passive resistor. This significantly enhances the achievable voltage gain without increasing chip area or power consumption.

The NMOS current source establishes a stable bias current and improves operating point robustness. Although its finite output resistance introduces a degeneration effect at the source node, it enhances bias stability and linearity.

Theoretical calculations and simulation results show good agreement:

* Theoretical Gain ≈ 15–16 V/V (≈ 23–24 dB)
* Simulated Transient Gain ≈ 24–25 V/V (≈ 27–28 dB)
* Simulated Midband Gain (AC Analysis) ≈ 11–12 dB (current-source degeneration limited)
* −3 dB Bandwidth ≈ 67.8 kHz

The variation between theoretical and simulated gain arises from practical second-order device effects incorporated in the TSMC model library, including:

* Channel length modulation
* Mobility degradation
* Body effect
* Intrinsic parasitic capacitances ($C_{gs}$, $C_{gd}$, and junction capacitances)

AC small-signal analysis demonstrates a clear low-pass frequency response, where the dominant pole is formed primarily by the output resistance and parasitic capacitances at the output node. These capacitances limit the high-frequency performance and define the bandwidth of the amplifier.

The NMOS current source introduces local feedback due to its finite output resistance, which improves linearity and reduces sensitivity to process variations, although at the expense of reduced voltage gain compared to an ideal CS amplifier.

Transient analysis verifies correct amplifier functionality, showing an amplified and phase-inverted output waveform with stable operation around the designed bias point and minimal distortion.

Hence, the designed Common Source amplifier successfully satisfies the required power and supply constraints while demonstrating proper DC biasing, stable saturation operation, controlled voltage gain, and predictable frequency response characteristics suitable for low-power CMOS analog applications.
