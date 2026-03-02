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


