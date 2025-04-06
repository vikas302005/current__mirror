# current__mirror
analysis of current mirror circuit

The current mirror circuit is a fundamental building block in IC design, ensuring that multiple transistors receive a stable and consistent biasing current. In an ideal world, each transistor would be biased using a dedicated current source to guarantee stability, but that's not practical in most cases. Instead, engineers rely on the current mirror approach, where the design cleverly replicates a reference current across multiple transistors. By carefully adjusting the width-to-length ((W/L)) ratio of each transistor, we can control the amount of drain current ((I_D)) flowing through each device, ensuring proper operation and balance within the circuit.


![image](https://github.com/user-attachments/assets/ca40d6df-6b58-435e-80b6-36934f011361)



1. **Starting Out:**  
   You have a circuit running at 1.8 V and using 1 mW of power. That means the total current flowing through the circuit is about 0.555 mA.

2. **Splitting the Current:**  
   If the current is split equally between two branches (using a 1:1 width-to-length ratio), each branch gets roughly 0.2777 mA. In another case, if the ratio is 1:2, the transistor you're focusing on only gets about one-third of the total current.

3. **Setting Up the Amplifier:**  
   To make sure the NMOS transistor can work as an amplifier with a gain (amplification factor) of at least 10, you need to look at how its key characteristics combine. In this circuit, the gain is determined by the transconductance (gm) and the effective output resistance (Rout) seen by the transistor. The combined output resistance from both the NMOS and PMOS parts comes out to be around 1.33 kΩ, thanks to the effect of channel length modulation.

4. **Calculating the Overdrive Voltage:**  
   The transistor’s performance depends on its overdrive voltage (V_OV), which is tied to its transconductance through the relationship gm = 2I_D/V_OV. With our numbers, solving for V_OV gives you roughly 0.0737 V.

5. **Getting the Right Bias Voltage:**  
   Finally, to really turn on the transistor as needed, you add its overdrive voltage to its threshold voltage (approximately 0.496 V). This sums up to about 0.569 V for the gate-source voltage (V_GS). This is the voltage you need to provide to the NMOS to have it work as a proper amplifier.

In simple words, to get your NMOS transistor amplifying correctly, you should drive its input with roughly **0.569 V**. 


Circuit Diagram:

![image](https://github.com/user-attachments/assets/93940c3c-f954-47c0-9fa9-b0aeb932dec3)

For the P-channel MOSFETs, M1, M2: - W = 10 µm, L = 180 nm

For the N-channel MOSFETs, M3: - W = 31.23 µm, L = 180 nm

i. Using L = 180 nm

1.DC Analysis

![image](https://github.com/user-attachments/assets/aab8cc83-4ca9-474c-a6d8-ef516916e69e)

The simulation results look really promising—they line up almost perfectly with our calculations. The currents running through our NMOS (M3) and PMOS transistors (M1, M2) are nearly the same, which means our circuit is meeting the power criteria, a crucial aspect of chip design.
For example, when we compute the power using
 P = I_{total} \times V_{DD} = 0.55401mA* 1.8V= 0.9972mW 
we see that it's right on target with our budget.
The next step is to check how the circuit performs in a dynamic scenario. We do this by running a transient analysis to ensure the voltage gain meets our requirements. To make this happen, we set up the input voltage (V_{in}) as a sinusoidal signal with a DC offset of 0.569 V. This way, we can confirm the circuit behaves as intended under real operating conditions.

Transient Analysis

![image](https://github.com/user-attachments/assets/726e0b24-b411-423e-99bc-963efcbed647)

https://github.com/tanmay665K/LIC-Lab/blob/main/Expt_6/media/image6.png

https://github.com/tanmay665K/LIC-Lab/blob/main/Expt_6/media/image7.png

For a 10 mV input pulse, the output peaks at 1.2381 V. When we compare the swing—from a baseline of 0.96 V up to 1.2381 V—we get a difference of about 0.2781 V. Dividing this output swing by the 10 mV input gives us a voltage gain of approximately:

A_V = {0.96 - 1.2381}/{0.01} =27.81V/V (or about 28.884 dB)

This clearly exceeds our design requirement of a gain greater than or equal to 10 V/V.

AC Analysis

https://github.com/tanmay665K/LIC-Lab/blob/main/Expt_6/media/image8.png

Finally, we move on to AC analysis, where we can calculate the 3 dB bandwidth and verify our calculated dB gain.

From here, we can see our 3 dB BW = 629.997 MHz – 0 = 629.997 MHz

The midband gain we are obtaining from our frequency response, i.e., 29.298 dB is also similar to the value we calculated, 28.884 dB.

Circuit 2: Ratio of 1:2 using L = 180 nm

![image](https://github.com/user-attachments/assets/0c7d332e-c2f4-4291-bfd6-2afe5bbe6d29)

DC Analysis –

![image](https://github.com/user-attachments/assets/5545150a-a237-4028-b7be-8049788a4c72)

Transient Analysis –

![image](https://github.com/user-attachments/assets/92be9108-71e1-4f3f-81fb-9e1fe2772b53)

Gain (V/V) = (1.26006-0.96)/ (-10 mV) = 30.006 V/V = 29.544 dB for an input voltage of 10 mV peak voltage, frequency of 1 kHz, sine wave. Let us perform the frequency response to verify this.

AC Analysis –

https://github.com/tanmay665K/LIC-Lab/raw/main/Expt_6/media/image12.png

Our simulation shows that our midband gain is around 29.325 dB, which is almost identical to our design target of 29.544 dB. In practical terms, this means we’re achieving a voltage gain of roughly 29.25 V/V—a drop in performance that's very minimal compared to our expected 30.006 V/V.

![image](https://github.com/user-attachments/assets/048d8828-677a-4d8c-ae8b-b67dbd69d5b9)

For the NMOS transistor (M3), we set the width at 65.19 µm and the channel length at 500 nm. Meanwhile, each PMOS transistor (M1 and M2) is sized with a width of 10 µm and a channel length of 500 nm.

DC Analysis:

![image](https://github.com/user-attachments/assets/397bf934-9169-4744-9d00-bf743bea1d98)

Transient Analysis:

![image](https://github.com/user-attachments/assets/c81553e8-bd4b-4a0e-b645-96e0a661aeed)

AC Analysis –

![image](https://github.com/user-attachments/assets/3ae4da87-c652-4cb1-b6a0-5c764c8fa1e6)

Our simulation shows that our design is performing impressively—a gain of about 37.87 dB with a 3 dB bandwidth of around 122.33 MHz. This tells us that the amplifier not only boosts the signal significantly but also handles a wide range of frequencies effectively.
Moving on to Circuit 2, where we're aiming for a 1:2 ratio while keeping the channel length at 500 nm, here’s how the transistors are sized:
- The NMOS device (M3) is set to a width of 85.243 µm with a 500 nm channel length.
- For the PMOS transistors, M1 has a width of 10 µm and M2 is sized at 20 µm, both with a channel length of 500 nm.

DC Analysis –

![image](https://github.com/user-attachments/assets/24a95ba5-10ab-4cb6-9bcc-a458edf8e9ad)

Transient Analysis –

![image](https://github.com/user-attachments/assets/980f94c4-b5b9-42cf-aaa6-18220a10cb9f)

AC Analysis –

![image](https://github.com/user-attachments/assets/0395c2fc-2398-4b1b-9b95-aa5e383c6a7e)

result and inference:

We experimented with current mirror circuits, tweaking channel lengths and the aspect ratios (W/L ratios) of the transistors to see how they perform. One clear takeaway is the classic trade-off between gain and bandwidth:
- Gain vs. Bandwidth:
When we use the 180 nm technology, the gain sits around 29 dB with a super high bandwidth of over 600 MHz. But if we switch to a 1 μm design, the gain jumps to somewhere between 35 and 39 dB, while the bandwidth drops to under 100 MHz. It’s like having two extremes: one design gives you speed, and the other gives you a boost in strength.
- Effects of Channel Length:
As we increase the channel length (from 180 nm to 500 nm to 1 μm), three things happen:- Gain increases: Longer channels reduce the channel length modulation (a kind of performance loss), which means the circuit can produce a higher gain.
- Bandwidth decreases: Longer channels also bring extra parasitic capacitances, which slow the circuit down.
- Bigger transistors: To keep the current steady with longer channels, we found that you need to use wider transistors—for example, the NMOS width had to go from about 31 µm to roughly 121 µm.

- W/L Ratio Impact:
We also compared two configurations—a 1:1 ratio versus a 1:2 ratio. Across the board, the 1:2 ratio method delivered better gain:- At 180 nm, the gain improved just a little (from about 29.298 dB to 29.325 dB).
- For 500 nm, there was a slight bump (from 37.87 dB to 38.015 dB).
- And at 1 μm, the difference was quite noticeable (from 35.481 dB to 38.693 dB).


In plain language, what all this means is that by choosing the right channel length and W/L ratio, you can tailor your current mirror circuit to meet your specific needs. However, keep in mind that increasing gain often comes with a payoff: a reduction in bandwidth and sometimes a larger chip area due to larger transistor sizes.
