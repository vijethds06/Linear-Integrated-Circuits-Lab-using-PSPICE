## Experiment 1 CS Amplifier

A MOSFET (Metal–Oxide–Semiconductor Field Effect Transistor) is a semiconductor device widely used for switching and amplification applications. It is a voltage-controlled device, where the voltage applied at the gate terminal controls the current flowing between the drain and source terminals. MOSFETs offer advantages such as high input impedance, low power consumption, and fast switching speed, making them suitable for analog as well as digital electronic circuits.

An amplifier is an electronic circuit used to increase the amplitude of a signal without significantly altering its original shape. It takes a small input signal and produces a larger output signal using power from a DC supply. Amplifiers are commonly used in audio systems, communication circuits, sensors, and signal processing applications. In MOSFET amplifiers, the device operates mainly in the saturation region to achieve linear and efficient amplification.



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
     Take Id= 200uA, this also satisfies the Id<=555.5uA.
     Applying Kvl at the output side: Vout= Vdd- IdRd
                                     0.9= 1.8 - Rd(200E-6)
                                     Rd = 4.5K ohm


     At saturation we know the current Id formula: Id= (un x wx Eox x Vov^2)/2x tox x l
     We get w= 3.248E-6 m
     But at this width, we get Id= 146uA which is not equal to the set current values.
     By trial and error method we got that at w= 4.518E-6 m we get Id= 200uA
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




                                                 
                                                  
  
  
