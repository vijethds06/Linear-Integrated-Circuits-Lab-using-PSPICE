# Experiment 2: CS Amplifier
---

## Aim

Implementation of a Common Source (CS) amplifier with NMOS source degeneration and PMOS active load using LTSpice.

### Design Specifications

- Supply Voltage: **VDD = 1.8 V**
- Power Constraint: **P ≤ 1 mW**

The design achieves proper biasing and amplification performance. The following analyses are performed:

- DC Operating Point Analysis
- Transient Response Analysis
- Voltage Gain Extraction
- Bandwidth Evaluation

## Theory

A Common Source (CS) amplifier is one of the most widely used MOSFET amplifier configurations for achieving high voltage gain. In this configuration, the input signal is applied to the gate terminal of the NMOS transistor, the output is taken from the drain terminal, and the source terminal serves as the common reference node.

In the proposed design, a PMOS transistor is used as an active load instead of a conventional drain resistor. Additionally, a source degeneration resistor is connected at the source terminal of the NMOS transistor to improve bias stability and linearity.

### PMOS Active Load



The PMOS transistor operates as an active load with its source connected to the supply voltage (VDD) and its gate biased using a constant DC voltage to maintain saturation operation.

Advantages of using a PMOS active load include:

- Higher output resistance
- Improved voltage gain
- Reduced silicon area in integrated circuit implementation

The large small-signal resistance offered by the PMOS device enhances the overall amplifier gain.



### Source Degeneration (Rs)

The source resistor introduces local negative feedback into the circuit.

Benefits include:

- Improved bias stability
- Reduced distortion
- Better linearity
- Reduced sensitivity to process variations

However, source degeneration reduces the effective transconductance of the NMOS transistor, thereby slightly reducing the voltage gain.



### Biasing and Operation

For proper amplification, both NMOS and PMOS transistors must operate in saturation.

NMOS saturation condition:

VDS ≥ VOV

where:

VOV = VGS − VTH

PMOS saturation condition:

VSD ≥ VOV

The DC bias point is selected such that the output voltage is approximately at mid-supply to allow maximum symmetrical signal swing.



### Voltage Gain

The approximate small-signal voltage gain is given by:


$$
A_v \approx \frac{-g_m r_o}{1 + g_m R_S}
$$


where:

- gm → NMOS transconductance
- ron → NMOS output resistance
- rop → PMOS output resistance
- Rs → Source degeneration resistor

The negative sign indicates a 180° phase inversion between input and output signals.



### Advantages

- High voltage gain due to active load
- Improved linearity from source degeneration
- Better DC bias stability
- Suitable for low-power CMOS analog integrated circuits

## Working Principle

The NMOS transistor (M1) functions as the primary amplifying device and is biased to operate in the saturation region. When a small AC signal is applied at the gate, it produces a variation in the gate-to-source voltage (VGS). This small change results in a proportional variation in the drain current given by:

$$
i_d = g_m v_{gs}
$$

where \( g_m \) is the transconductance of the NMOS transistor.

The varying drain current flows through the PMOS active load, which converts the current variation into a voltage variation at the output node. The small-signal output voltage can be expressed as:

$$
v_{out} = - i_d R_{out}
$$

The negative sign indicates a 180° phase shift between the input and output signals, which is characteristic of a Common Source amplifier.

The source resistor \( R_S \) introduces local negative feedback. When the drain current increases, the voltage across \( R_S \) also increases, raising the source potential. This reduces \( V_{GS} \), thereby limiting the increase in current and stabilizing the operating point.

Due to source degeneration, the effective voltage gain becomes:

$$
A_v \approx \frac{-g_m r_o}{1 + g_m R_S}
$$

Thus, the circuit provides voltage amplification with improved bias stability and linearity, at the cost of a slight reduction in gain.

## Ciruit Diagram

<img width="1051" height="865" alt="image" src="https://github.com/user-attachments/assets/777aad04-591c-454e-bd08-0f46665d6d9b" />

## Design




### Given Parameters

- Oxide thickness: \( t_{ox} = 4.1 \times 10^{-9} \, m \)
- Electron mobility: \( \mu_n = 273.809 \times 10^{-4} \, m^2/Vs \)
- Oxide permittivity:

$$
\varepsilon_{ox} = 4 \varepsilon_0 = 3.5416 \times 10^{-11} \, F/m
$$

- Threshold voltage:

$$
V_{TH} = 0.36 \, V
$$



### Power Constraint

The power dissipation must satisfy:

$$
P = V_{DD} \cdot I_D \leq 1 \, mW
$$

Given:

$$
V_{DD} = 1.8 \, V
$$

$$
1.8 \cdot I_D \leq 1 \times 10^{-3}
$$

$$
I_D \leq 555.5 \, \mu A
$$



### Assumed Overdrive Voltage

For proper amplifier operation, we assume:

$$
V_{OV} = 0.25 \, V
$$

Since

$$
V_{OV} = V_{GS} - V_{TH}
$$

Gate-to-source voltage becomes:

$$
V_{GS} = V_{OV} + V_{TH}
$$

$$
V_{GS} = 0.25 + 0.36
$$

$$
V_{GS} = 0.61 \, V
$$


### Biasing for Maximum Swing

To allow symmetrical output swing:

$$
V_{DS} = \frac{V_{DD}}{2}
$$

$$
V_{DS} = 0.9 \, V
$$



### Saturation Verification

For saturation:

$$
V_{DS} \geq V_{OV}
$$

Substituting:

$$
0.9 \geq 0.25
$$

Hence, the NMOS transistor operates in the saturation region.

### Gate Voltage

Applying KVL:

$$
V_G = V_{GS} + V_{RS}
$$

$$
V_G = 0.61 + 0.2
$$

$$
V_G = 0.81V
$$

##

### Source Degeneration Resistor

Assume source voltage drop:

$$
V_{RS} = 0.2V
$$

$$
V_{RS} = I_D R_S
$$

$$
0.2 = 200 \times 10^{-6} \times R_S
$$

$$
R_S = 1k\Omega
$$

##

### Output Bias Voltage

For near-symmetrical swing:

$$
V_{OUT} \approx \frac{V_{DD}}{2} + 0.2
$$


##


### PMOS Gate Bias Calculation

To ensure proper operation of the PMOS transistor in saturation, an overdrive voltage is selected as:

$$
V_{OVp} = 0.25 \, V
$$

The relationship between overdrive voltage and gate-to-source voltage is given by:

$$
V_{OVp} = V_{SG} - |V_{TP}|
$$

Given the PMOS threshold voltage:

$$
|V_{TP}| = 0.39 \, V
$$

Substituting,

$$
V_{SG} = V_{OVp} + |V_{TP}|
$$

$$
V_{SG} = 0.25 + 0.39
$$

$$
V_{SG} = 0.64 \, V
$$

For the PMOS device,

$$
V_{SG} = V_S - V_G
$$

Since the source terminal is connected to the supply voltage,

$$
V_S = V_{DD} = 1.8 \, V
$$

Therefore,

$$
V_G = V_S - V_{SG}
$$

$$
V_G = 1.8 - 0.64
$$

$$
V_G = 1.16 \, V
$$

Hence, the required PMOS gate bias voltage is:

$$
V_G = 1.16 \, V
$$

$$
V_{OUT} = \frac{1.8}{2} + 0.2
$$


$$
V_{OUT} = 1.1V
$$

### 3.3 Transistor Width Calculation

The drain current of a MOSFET operating in saturation is given by:

$$
I_D = \frac{1}{2} \mu_n C_{ox} \frac{W}{L} (V_{OV})^2
$$

Rearranging the expression to determine the required width:

$$
W = \frac{2 I_D L}{\mu_n C_{ox} (V_{OV})^2}
$$

The design target was:

$$
I_D = 200 \, \mu A
$$

---

### NMOS Width Design

Using the above equation and the chosen overdrive voltage, the initial calculated NMOS width was:

$$
W_n \approx 15.15 \, \mu m
$$

However, upon simulation, the obtained drain current was slightly lower than the expected 200 µA. This deviation occurs because practical MOSFET models in LTSpice include second-order effects such as channel length modulation, mobility degradation, and velocity saturation, which are not considered in the ideal square-law equation.

To compensate for these non-idealities and achieve the target drain current, the NMOS width was increased to:

$$
W_n = 56.159 \, \mu m
$$

After this adjustment, the simulated operating point matched the intended bias current.

---

### PMOS Width Design

Similarly, applying the saturation current equation for the PMOS device yielded an initial width of:

$$
W_p \approx 35.91 \, \mu m
$$

As observed with the NMOS device, simulation results indicated a slightly lower drain current than expected due to practical model effects.

To obtain the desired 200 µA operating current, the PMOS width was adjusted to:

$$
W_p = 82.1 \, \mu m
$$

Following this correction, the DC operating point aligned with the design specification.

## DC Analysis
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/ab527235-6586-4c58-9ce7-839579ed5b2e" />

 
### Interpretation

From the DC operating point analysis, the NMOS gate voltage is approximately **0.81 V** while the source voltage rises to about **0.199 V** due to the presence of the source degeneration resistor. This results in a gate-to-source voltage:

$$
V_{GS} = 0.81 - 0.199 \approx 0.611V
$$

Considering the threshold voltage of **0.36 V**, the overdrive voltage becomes:

$$
V_{OV} = V_{GS} - V_{TH} \approx 0.25V
$$

which closely matches the assumed design value. The drain current obtained from simulation is approximately **199 µA**, confirming that the circuit satisfies the intended bias current under the given power constraint. The output voltage settles near **1.108 V**, indicating that sufficient voltage headroom exists across the NMOS transistor to maintain operation in the saturation region.


The operating point results verify that both the NMOS amplifying transistor and the PMOS active load are correctly biased. The desired drain current is achieved while maintaining stable saturation operation and proper voltage swing at the output node. Hence, the circuit satisfies the required biasing conditions for reliable small-signal amplification under the specified supply voltage and power limitations.


## Transient Analysis

<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/e783ffb5-9221-4285-b136-a575523f66a5" />



The transient analysis confirms proper operation of the Common Source (CS) amplifier. The output waveform is clearly **amplified and phase inverted**, indicating a 180° phase shift between input and output, which is a characteristic feature of CS amplifiers.



### Input Signal Parameters

- Signal Type : Sine Wave  
- Frequency : **1 kHz**  
- Amplitude : **10 mV**  
- DC Offset : **0.81 V**



### Measured Peak-to-Peak Voltages

Input peak-to-peak voltage:

$$
V_{in(p-p)} = 0.8199V - 0.8V
$$

$$
V_{in(p-p)} = 0.01999V
$$

Output peak-to-peak voltage:

$$
V_{out(p-p)} = 1.344V - 0.82877V
$$

$$
V_{out(p-p)} = 0.51523V
$$



### Voltage Gain (Simulation)

Voltage gain is calculated as:

$$
A_v = \frac{V_{out(p-p)}}{V_{in(p-p)}}
$$

$$
A_v = \frac{0.51523}{19.99 \times 10^{-3}}
$$

$$
A_v = 25.77
$$

Gain expressed in decibels:

$$
A_v(dB) = 20 \log_{10}(25.77)
$$

$$
A_v(dB) = 28.22 dB
$$



## Theoretical Voltage Gain

Considering channel length modulation effects:

$$
\lambda = 0.1 \, V^{-1}
$$



### Transconductance

The small signal transconductance is given by:

$$
g_m = \frac{2I_D}{V_{OV}}
$$

$$
g_m = 1.6 \times 10^{-3} S
$$



### Output Resistance

The output resistance due to channel length modulation becomes:

$$
r_o = \frac{1}{\lambda I_D}
$$

$$
r_o = 50k\Omega
$$

Since both NMOS and PMOS contribute to output resistance:

$$
r_{out} = r_{o1} || r_{o2}
$$

$$
r_{out} = 25k\Omega
$$



### Voltage Gain with Source Degeneration

Including the effect of source degeneration resistance:

$$
A_v = \frac{g_m (r_{o1} || r_{o2})}{1 + g_m R_S}
$$

$$
A_v = 15.38
$$

Gain in decibels:

$$
A_v(dB) = 20 \log_{10}(15.38)
$$

$$
A_v(dB) = 23.739 dB
$$



### Observation

The simulated gain is lower than the theoretical value due to practical device behavior and model-dependent parameters such as effective channel length modulation and bias-dependent transconductance. However, both results confirm successful amplification with stable biasing and expected CS amplifier characteristics.



## AC Analysis

<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/947d6f0f-2bf0-4941-b66f-1660a41ab609" />


The AC small signal analysis of the Common Source (CS) amplifier was performed to evaluate frequency response and bandwidth performance.

From the Bode magnitude plot, the amplifier exhibits a **midband voltage gain of approximately 28.41 dB** (≈ 26.3 V/V) at low and mid frequencies. The gain remains nearly constant over a wide frequency range, indicating proper biasing and stable small-signal operation.

At higher frequencies, the gain gradually decreases due to **parasitic capacitances of the MOSFETs**, such as gate-drain and gate-source capacitances, which introduce dominant poles in the circuit.

The amplifier shows a clear **low-pass frequency response**, where the midband gain is maintained until the cutoff region, beyond which attenuation increases rapidly.

The phase response also confirms the expected behavior of a Common Source amplifier, approaching a phase inversion close to 180° in the midband region.

Overall, the AC analysis verifies successful amplification with good midband gain and finite bandwidth limited primarily by intrinsic device capacitances.

<img width="1885" height="1025" alt="image" src="https://github.com/user-attachments/assets/0da11b76-9c50-4e9c-92a9-f84ccefe4752" />

## -3 dB Cutoff Frequency (Bandwidth)

From the AC analysis, the midband gain of the amplifier is approximately 28 dB.  
The −3 dB point occurs when the gain drops by 3 dB from its midband value.

Midband Gain ≈ 28.4 dB  
−3 dB Gain Level ≈ 25.4 dB  

From the Bode plot, this occurs at:

f_H ≈ 37.66 MHz

This frequency represents the **upper cutoff frequency** of the amplifier.

Beyond this point, the gain starts decreasing rapidly due to internal MOSFET parasitic capacitances (Cgs, Cgd) which introduce dominant poles in the circuit.

Hence, the bandwidth of the amplifier is approximately:

Bandwidth ≈ 37.66 MHz

This confirms that the circuit behaves as a low-pass amplifier with a finite high-frequency limit determined by device parasitics.


## Inference

The Common Source (CS) amplifier employing a PMOS active load and source degeneration was successfully designed and implemented using TSMC 180 nm CMOS technology in LTSpice while satisfying the specified design constraints:

- Supply Voltage : VDD = 1.8 V  
- Power Consumption : P ≤ 1 mW  
- Load Capacitance : CL = 10 pF  

A drain current of approximately 200 µA was selected to ensure reliable biasing while maintaining the total power dissipation within limits:

P = VDD × ID ≈ 1.8 × 200 µA = 0.36 mW

which comfortably satisfies the power constraint.

The DC operating point confirms that both NMOS and PMOS transistors operate in the saturation region, ensuring proper small-signal amplification. The bias voltages were chosen such that the output node is positioned close to mid-supply, enabling a near-symmetrical output voltage swing and minimizing signal distortion.

The PMOS transistor functions as an active load, providing a large effective output resistance compared to a passive resistor, thereby improving voltage gain without increasing power consumption.

Theoretical and simulated results show reasonable agreement:

- Theoretical Gain ≈ 15.38 V/V (23.74 dB)  
- Simulated Transient Gain ≈ 24.53 V/V (27.79 dB)  
- Simulated Midband Gain (AC Analysis) ≈ 27–28 dB  
- −3 dB Bandwidth ≈ 37–40 MHz  
- Unity Gain Frequency ≈ 1.5 GHz  

The deviation between theoretical and simulated gain arises due to practical second-order effects included in the TSMC device models such as:

- Channel Length Modulation
- Mobility degradation
- Body effect
- Parasitic capacitances (Cgs, Cgd, Cdb)

AC analysis indicates that the load capacitance (CL) together with the output resistance forms the dominant pole at the output node, which limits the high-frequency response and defines the amplifier bandwidth.

The inclusion of source degeneration introduces local negative feedback. This improves bias stability, enhances linearity, and reduces sensitivity to process variations. However, it also reduces the achievable voltage gain compared to an ideal CS amplifier without degeneration.

Transient analysis confirms proper amplifier operation, showing an amplified and inverted output waveform with minimal distortion around the bias point.

Hence, the designed Common Source amplifier successfully meets the required power constraint and demonstrates correct DC biasing, stable operation in saturation, expected voltage gain characteristics, and appropriate frequency response behavior suitable for low-power analog applications.
