## Experiment 1: CS Amplifier

A MOSFET (Metal–Oxide–Semiconductor Field Effect Transistor) is a semiconductor device widely used for switching and amplification applications. It is a voltage-controlled device, where the voltage applied at the gate terminal controls the current flowing between the drain and source terminals. MOSFETs offer advantages such as high input impedance, low power consumption, and fast switching speed, making them suitable for analog as well as digital electronic circuits.

A MOSFET amplifier is an electronic circuit that uses a MOSFET (Metal Oxide Semiconductor Field Effect Transistor) to increase the amplitude of an input signal. Since a MOSFET is a voltage controlled device, a small change in gate voltage controls a larger drain current, which produces an amplified output signal. MOSFET amplifiers are widely used in analog circuits due to their high input impedance, low power consumption, good thermal stability, and suitability for integrated circuit design.

MOSFET amplifiers are mainly classified into three types based on the terminal that is common to both input and output:

1.Common Source (CS) Amplifier

2.Common Drain (CD) Amplifier or Source Follower

3.Common Gate (CG) Amplifier

The Common Source amplifier is the most widely used configuration because it provides high voltage gain. In this configuration, the source terminal is connected to ground and acts as the common reference for both input and output. The input signal is applied at the gate terminal, while the output is taken from the drain through a load resistor connected to the supply voltage VDD. When the input voltage increases, the drain current increases, causing a larger voltage drop across the drain resistor. As a result, the output voltage decreases, producing a 180 degree phase shift between input and output.

The CS amplifier is usually biased such that VDS is approximately equal to VDD/2 to set a proper Q-point in the saturation region. This allows maximum undistorted signal swing and linear amplification. It offers high voltage gain and moderate input impedance but has relatively higher output impedance. Due to its amplification capability, the CS amplifier is commonly used in audio amplifiers, sensor signal conditioning circuits, and analog communication systems. 

The below is the general representation of a CS Amplifier.

<img width="159" height="166" alt="image" src="https://github.com/user-attachments/assets/da39b9c0-bd89-4f62-935c-42300d622bc7" />

The circuit consists of an NMOS (N-channel MOSFET) in which the gate terminal is connected to the input voltage Vin. For the channel to form and allow current conduction, the applied input voltage must be greater than the threshold voltage of the MOSFET. A DC power supply is connected at the drain terminal to provide the required operating power, while the source terminal is connected to ground.

The drain current flows from the supply through the drain towards the source. In this circuit, the applied input is a voltage signal, and the objective is to obtain an amplified output voltage. Since a MOSFET is a voltage controlled current device, the primary output parameter is the drain current. To convert this current into a voltage, a resistor is connected at the drain terminal. According to Ohm’s law, V = I × R, the voltage developed across this resistor becomes the output voltage.

From the output characteristics, it can be observed that the amplifier operates in the saturation region of the MOSFET, which is suitable for proper amplification.

<img width="391" height="317" alt="image" src="https://github.com/user-attachments/assets/2fd32ad4-13c1-4dcb-8062-622cce7e38a3" />

A Q-point (quiescent point) is established in a MOSFET to ensure that it operates in its optimal region for proper amplification. It provides a stable DC operating condition, minimizes distortion, and allows the amplifier to achieve the desired gain. Setting an appropriate Q-point also enables the maximum possible signal swing without clipping or driving the device into non-linear regions.

The input DC voltage can also be established at the gate terminal using the voltage divider biasing method, which helps in setting a stable operating point for the MOSFET. Capacitors act as an AC short circuit and a DC open circuit, meaning they allow AC signals to pass while blocking DC components. However, the impedance of the capacitor varies with frequency and plays an important role in determining the frequency response of the system.

<img width="664" height="340" alt="image" src="https://github.com/user-attachments/assets/ed03eca5-da0b-47d5-9d29-f3cb79d08e73" />

The following represents the Voltage Transfer Characteristic (VDS vs VGS) of a MOSFET.

<img width="560" height="420" alt="image" src="https://github.com/user-attachments/assets/8437a192-3429-4bb5-92a8-25c7432e46b1" />


When VGS is less than the threshold voltage VTH, the MOSFET remains in the cut-off region and no drain current flows, resulting in VDS being approximately equal to VDD. When VGS exceeds VTH, the MOSFET turns ON. If VDS is greater than or equal to the overdrive voltage VOV, the device operates in the saturation region, which is required for amplification. However, if VDS becomes less than VOV, the MOSFET enters the triode region.

The saturation region is preferred for amplifier operation because the characteristics become nearly linear in this region. When an input signal is applied around this operating point, the amplifier provides higher and more linear gain. Therefore, this almost linear portion of the curve is important while selecting the Q-point.

A 180 degree phase shift is observed between the input and output signals. When the input voltage increases, the drain current ID also increases. This increases the voltage drop across the drain resistor (ID × RD), causing VDS to decrease as VGS increases. Hence, the output is inverted with respect to the input.

It is also important that the applied AC input signal satisfies VGS << 2VOV for proper amplifier operation. If the positive peak of the signal becomes too large, the negative portion may push the MOSFET into the triode region, causing distortion. Similarly, if the negative peak increases excessively, the device may enter the cut-off region, leading to signal clipping.

Although careful parameter selection can result in very high gain, extremely high gain is often undesirable due to instability and distortion. To reduce and stabilize the gain, a source resistor is introduced, which provides source degeneration and improves linearity and stability. Additionally, a bypass capacitor can be connected across the source resistor to increase AC gain by allowing AC signals to bypass the source resistance while maintaining DC bias stability.

Frequency response of CS amplifier:

<img width="418" height="231" alt="image" src="https://github.com/user-attachments/assets/68300b90-2780-410c-b662-5309369da0ec" />

The figure shows the frequency response of an amplifier, which describes how the gain changes with frequency. At low frequencies, the gain is small because the coupling and bypass capacitors offer high reactance (impedance) at low frequencies. This restricts the flow of AC signals and reduces signal transfer, causing attenuation. Hence, the amplifier behaves like a high-pass filter in this region. As frequency increases, the capacitor reactance decreases, allowing more signal to pass and the gain rises until it reaches the midband region.

In the midband region, the capacitors behave almost like short circuits for AC signals and parasitic effects are minimal. Therefore, the amplifier provides maximum and nearly constant gain, resulting in proper linear amplification.

At high frequencies, the gain again decreases due to the presence of parasitic capacitances within the MOSFET (gate-to-source and gate-to-drain capacitances), wiring capacitances, and load capacitances. These introduce additional poles and reduce signal amplification by shunting high-frequency signals to ground. Thus, the amplifier behaves like a low-pass filter at high frequencies.

The frequencies fL (lower cutoff frequency) and fH (upper cutoff frequency) are the points where the gain falls by 3 dB from the midband gain, and the frequency range between them defines the bandwidth of the amplifier.








Q) Design a CS amplifier circuit using nMOS in TSMC 180nm tech.lib in LTSPICE. Use Vdd= 1.8V, P<=1mW , Cl= 10pF, Ln= 560nm.
Circuit: <img width="1001" height="842" alt="image" src="https://github.com/user-attachments/assets/0519ecfd-08c9-4ee3-8a79-3b62a239b841" />
Calculation: 
Given:- tox= 4.1E-9
        un= 273.809E-4
        Eox= E x Eo= 4 x Eo= 3.5416E-11
        Vth= 0.36V


  We know that Power = Voltage x Current
  P= V x I <= 1E-3 W
  P= 1.8 x Id <= 1E-3
  Id<=555.5uA


  Since it is an amplifier we need to bias thisin the saturation region.
  We take Vds= 50% of Vdd = 0.9V
  
  
  Here we observe Vgs= 0.9, Vth= 0.36V, therefore Vov= Vgs - Vth= 0.9-0.36= 0.34V

  By concept, at saturation, Vds>=Vov: 0.9>=0.34, therefore the condition is satisfied and it is in saturation. 

  1. DC operating point:
     
     Take Id = 200 µA, which also satisfies the condition Id ≤ 555.5 µA.

Applying KVL at the output side:

Vout = Vdd − IdRd

0.9 = 1.8 − Rd(200 × 10⁻⁶)

Rd = 4.5 kΩ


For saturation region operation, the drain current equation is:

Id = (µn × W × εox × Vov²) / (2 × tox × L)

From this relation, the calculated width obtained is:

W = 3.248 × 10⁻⁶ m

However, at this width the obtained drain current is:

Id = 146 µA

which is not equal to the desired current value.

Therefore, using the trial and error method, it was observed that:

W = 4.518 × 10⁻⁶ m

gives

Id = 200 µA.

 <img width="855" height="417" alt="Screenshot 2026-02-22 230852" src="https://github.com/user-attachments/assets/fae6a91b-aff2-4e82-8e40-c7d4a446755e" />

The difference between the calculated and obtained width for 200 µA occurs because the theoretical calculation assumes ideal MOSFET behavior, while the practical or simulated device includes non-ideal effects such as channel length modulation, mobility degradation, threshold voltage variations, and parasitic parameters. These factors change the actual drain current, resulting in a different required width.

2. DC sweep:
    
    <img width="1919" height="1079" alt="Screenshot 2026-02-22 231707" src="https://github.com/user-attachments/assets/74bcd83a-4d47-4373-a0e4-94ca4964b254" />

     The given graph represents the DC transfer characteristics of a Common Source NMOS amplifier, obtained by sweeping the input voltage from 0 V to 1.8 V and observing the output voltage at the drain. For low input voltages below the threshold voltage, the MOSFET remains in the cut-off region, resulting in negligible drain current and an output voltage close to ​Vdd (1.8 V). As the input voltage increases beyond the threshold, the MOSFET enters the saturation region, where the drain current increases rapidly and the output voltage decreases sharply, providing amplification. At higher input voltages, the MOSFET operates in the triode region, causing the output voltage to drop close to ground. This behavior demonstrates the inverting nature and amplification operation of the common source amplifier.


3. Transient Analysis:
        <img width="1919" height="1079" alt="Screenshot 2026-02-22 231928" src="https://github.com/user-attachments/assets/fe9fb7f3-43b5-4618-addc-2c15681f428a" />

    
     The given waveform shows the transient response of a Common Source NMOS amplifier, where the input signal (blue) is a small sinusoidal voltage applied at the gate and the output signal (green) is taken from the drain. It can be observed that the output waveform is amplified and 180° phase shifted (inverted) with respect to the input signal, which is the characteristic behavior of a common source amplifier. The larger amplitude of the output compared to the input indicates voltage amplification, while the sinusoidal shape without distortion confirms that the MOSFET is properly biased and operating in the saturation region around the Q-point.

     The Q-point (Quiescent Point) is the DC operating condition of a MOSFET when no input signal is applied, defined by the values of VDS and drain current ID. It is chosen such that the MOSFET operates in the saturation region for proper and linear amplification. Typically, the Q-point is set by selecting VDS ≈ VDD/2, which places the operating point at the center of the load line. This allows the output voltage to swing equally in both directions, ensuring maximum undistorted signal amplification and preventing the device from entering cut-off or triode regions.

4. AC analysis:
    
    <img width="1919" height="1079" alt="Screenshot 2026-02-23 005657" src="https://github.com/user-attachments/assets/9fd8b9bb-cf33-4996-9454-4975593174ad" />

    The given graph represents the frequency response (AC analysis) of a Common Source NMOS amplifier, showing the variation of voltage gain with frequency. At low and mid frequencies, the amplifier provides a nearly constant gain of about 10.4 dB, indicating stable amplification in the midband region. As the frequency increases, the gain gradually decreases due to the effect of parasitic capacitances and the load capacitor (C1), which introduce poles in the circuit. The −3 dB point, observed around 3.63 MHz, represents the upper cutoff frequency, where the gain reduces to approximately 7.46 dB, defining the bandwidth limit of the amplifier. Beyond this frequency, the gain drops rapidly, showing reduced amplification at higher frequencies.

   Theoretical Gain:

   Gain (Av) = gm x Rd= (2 x Id x Rd)/Vov
                  = (2 x 200E-6 x 4.5E3)/(0.9-0.36)
                  = 3.33

   Av dB = 20log(Gain)
              = 20log(3.33) = 10.45 dB

   Practical Gain is observed to be 10.4 dB.

   The theoretical and practical values of gain are observed to be nearly matching, which indicates proper design and accurate biasing of the MOSFET amplifier. The theoretical gain is calculated using ideal device equations by neglecting parasitic effects, whereas the practical or simulated gain includes second-order effects such as channel length modulation, parasitic capacitances, and device model parameters. The close agreement between both values confirms that the amplifier operates correctly in the saturation region and validates the design assumptions and calculations.

# Result
 The MOSFET Common Source amplifier was successfully designed and analyzed using DC operating point, DC sweep, transient, and AC analyses. The DC operating point analysis confirmed that the MOSFET is properly biased in the saturation region with an appropriate Q-point, ensuring stable operation and maximum undistorted signal swing. The DC sweep analysis verified the voltage transfer characteristics, demonstrating the transition between cut-off, saturation, and triode regions and confirming the inverting behavior of the amplifier. The transient analysis showed that the output signal is amplified and exhibits a 180 degree phase shift with respect to the input, validating proper amplification around the chosen operating point. The AC analysis provided the frequency response of the amplifier, identifying the midband gain, cutoff frequencies, and bandwidth, while highlighting the effects of capacitors and parasitic elements at low and high frequencies. Overall, the theoretical calculations and simulation results were found to be in close agreement, confirming the correct design and performance of the Common Source MOSFET amplifier.





                                                 
                                                  
  
  
