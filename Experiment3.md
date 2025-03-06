# Experminet 3:- MOS Differential Amplifier 
## AIM:Design and analyse the MOS differential amplifier circuit for the given specification.
- VDD=3.2V
- P<=2.8mW
- Vicm=1.6V
- Vocm=1.7V
- Vp= 0.6V
### *Perform DC analysis, transient analysis and frequency response and extract the required paramenters.* 

## Overview:


A MOS Differential Amplifier is a key circuit in analog electronics, used for signal amplification, common-mode rejection, and noise suppression. It consists of two matched MOSFETs, a current source, and load resistors.

**Circuit Diagram:**
![MOS differential amplifier](https://github.com/shivaanii33/LIC-Lab/blob/52110e1853d4575edfdec76bafaeec429ba6d917/images/Screenshot%202025-03-03%20225209.png)

**Working Principle**
- Differential Input: The circuit amplifies the difference between the two input voltages (V_IN1 - V_IN2).
- Current Source Biasing: The total bias current (I_BIAS) is constant, ensuring stable operation.
- Output Voltages: The amplified signals appear at V_OUT1 and V_OUT2.
![key components](https://github.com/shivaanii33/LIC-Lab/blob/966b6e7a2e0489e3310ef2e9bbb45008c497c658/images/Screenshot%202025-03-03%20232202.png)

The sum of the two drain currents ID1 and ID2 must equal IBIAS. We also know that the two drain currents are equal because, in this idealized analysis, both halves of the circuit are identical. Thus,

![currents](https://github.com/shivaanii33/LIC-Lab/blob/ec7d886a29f5b565224f69184f1f69cdd5f25a10/images/Screenshot%202025-03-03%20230122.png)

Let’s assume for the moment that the transistors are in saturation. The equation for saturation-mode drain current is the following:

![currents](https://github.com/shivaanii33/LIC-Lab/blob/9b9095811bc1715f898f1aa399f29d3c25861cdb/images/Screenshot%202025-03-03%20230129.png)

 The drain current is already established (by the current source) and the gates are tied to the ground node; this means that the source voltage will settle on whatever value creates a gate-to-source voltage (VGS) corresponding to a drain current of IBIAS/2.


 ## Design:
  Given p=2.8mW

  since p=VddxIss;

  - **Iss** = p/Vdd = 2.8m/3.2 = **0.875mA**
  
 -  **I1=I2=Iss/2 =  0.4375mA**
  
  *Applying KVL along the loop*
  
  Vdd-I1Rd-Vocm1=0

  Rd=(Vdd-Vocm)/I1

  Rd=(3.2-1.7)/0.4375x10^-3

  - **Rd=3428ohm**

  Rss=Vp/Iss = 0.6/0.875m

  - **Rss=685.7ohm**

  ![circuit diagram](https://github.com/shivaanii33/LIC-Lab/blob/52110e1853d4575edfdec76bafaeec429ba6d917/images/Screenshot%202025-03-03%20225209.png)
  adddd newww oneeee

### 1) DC Analysis:
The DC Analysis of a MOS Differential Amplifier determines the operating point (biasing conditions) of the transistors by sweeping the input voltages and analyzing the DC output voltages and currents.


*Considering the half circuit*

 ![half circuit](https://github.com/shivaanii33/LIC-Lab/blob/211867682ab9b21d088fab71e7edcfb8c6c8f53a/images/Screenshot%202025-03-03%20234100.png)
> Here 
- **VG = 1.6V**, Now VGS = VG-VS 
VS=I1(2Rss) = 0.437m(2x685.7)

- **VS= 0.56v**

Therefore **VGS1= VGS2 = VG-VS = 1.6-0.59 = 1.01V**

---
*On applying KVL to the half circuit:*

- **VDS=VDD-IdRd-VS**
VDS = 3.2-(0.4375m)(3.428K)-0.56

- **VDS=1.14V**

Hence the required Qpoint for both the transistors are (*since both half of circuits are mirror's of each other*)

- **M1 Q-Point(VDS1,Id1) -> (1.14V,0.4375mA)**
- **M2 Q-Point(VDS2,Id2) -> (1.14V,0.4375mA)**

---
### Procedure for the simulation in ltspice

- Create a new Experiment Workspace
- Enter a spice directive by clicking on .t option on the ribbon  .lib tsmc018.lib  This specifies the BSIM3 Model of the MOSFET, if you stored this file in some other location specify that in the command
- Add the transistor NMOS4 and Change the name of the transistor to CMOSN
- Assign the specified values for the voltages and the resistors
- Now we can start finding appropriate Aspect Ratio for our MOSFET, we will take a range and combination of values for W (width) and L (length) of the MOSFET
- After getting a suitable value we will perform Transient and AC Analysis

**Effect of L (Channel length)**

For this analysis we will keep Rd=3.428Kohm and Rss=685.7ohm and perform a Linear parameter sweep for W and List paramter sweep for L, with the help of the commands

.step param W 30n  250n 1n

Keep L = 180nm , then you will get a curve for ID vs W for L = 180 nm\

![idvsw](https://github.com/shivaanii33/LIC-Lab/blob/cd5eea4a11ad5b6a6028ef5c6d2d9c624667b448/images/Screenshot%202025-03-04%20003531.png)

![idvsw](https://github.com/shivaanii33/LIC-Lab/blob/99e486abeae8c2dd28387f122e5778e25f058ded/images/Screenshot%202025-03-04%20003616.png)

from this we'll get to know the range of w for which the required amount of current can be obtained 
 
 > for around **w=2.4858537µm, l=180nm** the value of the required parameters will be almost equal.

 ---


For the **DC Operating Point:**

- Go to Simuate -> Configure Analysis -> DC operating point
- Add the .op text on the experiment workspace
- Click on the Play button to turn on the simulation, this will generate a text file with all the voltages and currents for more info go to View -> SPICE Output Log

![DC operating](https://github.com/shivaanii33/LIC-Lab/blob/83c926784733f49900df362a2f24909725d5c9a9/images/Screenshot%202025-03-04%20010201.png)

- SPICE Netlist

![DC operating](https://github.com/shivaanii33/LIC-Lab/blob/b9f937da41d45a25a75f579fd065d40de742de77/images/Screenshot%202025-03-04%20010311.png)

**The valvue of Gm is 1.12e-03**

**The value of Vt=0.489V**

---

*Also we have to verify that the transistor is working in saturation region, this can be done by checking that whether VGD is greater than or lesser that Vt*

For VGD=VG-VD=1.6-1.70

VGD = -0.10 , but Vt=0.489V

Hence **VGD<Vt**; therefore mosfets are in saturation region.

## Transient Analysis
Transient analysis helps in understanding the time-domain behavior of the circuit when subjected to a varying input signal. 
> The simulation set up for the transient analysis is as mentioned below.

![transient simusetup](https://github.com/shivaanii33/LIC-Lab/blob/4a3c6d34d5899d7874191c48ed9733999e267e99/images/Screenshot%202025-03-04%20230524.png)

> If both inputs of a differential amplifier are equal during transient analysis, the output should ideally be zero, since the amplifier amplifies the difference between the inputs:

![bothinputeq](https://github.com/shivaanii33/LIC-Lab/blob/9255734fc6091b827c3a64f71fb507ca22069b85/images/Screenshot%202025-03-04%20224130.png)

The amplifier is designed to amplify differences, not identical signals.
When inputs are equal, the circuit operates in common mode, which should be rejected.
Vout= Ad(V1-V2); if V1=V2 then **Vout=0**

*Hence both the inputs should be different. so we can give 180deg phase shift for one of the input.*

![phase](https://github.com/shivaanii33/LIC-Lab/blob/2d70b2dee767bc5525c781d5b68e6b671f7ee8ad/images/Screenshot%202025-03-04%20230542.png)

>> The obtained results are as shown 

![trans1](https://github.com/shivaanii33/LIC-Lab/blob/df8715fb5224298f2871283c07307975d00b8792/images/Screenshot%202025-03-04%20223603.png)

![trans2](https://github.com/shivaanii33/LIC-Lab/blob/82f173d033cb3c467a008738c541435f709c13c8/images/Screenshot%202025-03-04%20223955.png)

differential gain = Voutdiff/Vindiff

- **Av*diff* =  324.65441mV/99.470253mV = 3.217V/V**
- **The valvue of Gm is 1.12e-03**
- **Overall gain Av= gm*rd= 3.53V/V**

This transient analysis shows the response of a differential amplifier. The green waveform represents the differential input signal (V1-V2) , while the blue waveform represents the differential output (Vocm1-Vocm2). The amplifier effectively amplifies the input signal while rejecting common-mode noise. 

## Frequency Response 

![freq](https://github.com/shivaanii33/LIC-Lab/blob/0d1af10cb6a7796874d6dfd88dac80ccc97f58ab/images/Screenshot%202025-03-05%20000357.png)


> From the graph the gain in db scale is **11.187db-3db= 8.187db**

# Circuit 2 
![circuit2](https://github.com/shivaanii33/LIC-Lab/blob/4e772f37a3f15a1cfb1dc6549e6d79ed4383b471/Screenshot%202025-03-06%20231213.png)

Replacing \( R3 \) with a current source \( Iss \) transforms the circuit into a fully differential pair with an active current source. This modification eliminates source degeneration, increasing the **gain** and improving **common-mode rejection (CMRR)**. The current source ensures a stable **bias current**, making the circuit less sensitive to variations in component values. Without \( R3 \), the **transconductance \( g_m \) is higher**, resulting in a larger differential gain given by \(**Ad=gm*rd**). 

---
## DC Analysis 

*The procedure is same as the above mentioned for the previous circuit*

![dc2](https://github.com/shivaanii33/LIC-Lab/blob/8ceacf6fcaf63dc9b2647701f234fe66a4c21351/images/Screenshot%202025-03-06%20231829.png)

Mosfet aspect ratio was same ie, **L= 180.1nm, W =2.4858537µm**

for mosfet M1 & M2:

Vocm = 1.70025v

ViCM = 1.6V

Id= 0.4375 mA

Vtn = 0.489v

VGS = 1.6 - 0.593613 = 1.01V

VDD = IdRd + VDS +Vp

VDS = 1.11


The Q-point of both the mosfets are **(1.1V, 0.4375mA)**.

---
## Transient Analysis:

>>The below graph represents the transient analysis between the differential input and the differential output of the mos differential amplifier 

![freq](https://github.com/shivaanii33/LIC-Lab/blob/253335854b7c7ae88f716d3c47b3826d3bf1f9f3/images/Screenshot%202025-03-07%20014236.png)

>* The value of the diff gain is given by **Avdiff=326.61m/99m**
- **Avdiff=3.366V/V**


>>From the graph ,we can observe the 180 degree phase shift in the output signal and the output voltage (at Vocm node) is amplified .

![freq](https://github.com/shivaanii33/LIC-Lab/blob/6578a86f8dac16bf131040adc53522e4e11eed9d/images/Screenshot%202025-03-07%20014001.png)


From the above observation 
- **Gain Av=Vout(peak)/Vin(peak)**
- **Av=1.863/1.65=1.129V/V**

Overall gain = **gm*rd**
- **Av(overall)= 3.83V/V**

---

## Frequency analysis 

![freq](https://github.com/shivaanii33/LIC-Lab/blob/573fb0c43a2040d4c812b998d814b5c9a12f8e19/images/Screenshot%202025-03-07%20014650.png)

From the graph , the gain in dB scale is **10.45dB - 3dB =7.45db**

---

# Circuit 3 

This circuit is obtained by replacing the current source of 2nd circuit by the nmos 

The value for Vb is given by **Vb=Vtn+Vp=0.489+0.6=1.089V**


![freq](https://github.com/shivaanii33/LIC-Lab/blob/a6d2bec98b3daa89a74ce6792fc8a530452596f7/images/Screenshot%202025-03-07%20025703.png)


In this circuit, an NMOS transistor (M3) is used in place of the current source (Iss) and resistor (Rss). However, to maintain the same operating point, the drain current of M3 must still be equal to Iss = 0.875mA.

Since the circuit remains symmetrical, the values of Rd1 and Rd2 remain unchanged at 3428Ω. This is because the same drain currents (Id1 and Id2) continue to flow through the differential pair, and the voltage conditions remain the same.

Also,

Vds = Vocm - Vp = 1.1V

Vgs = Vicm - Vp = 1V

But we have to set the voltage Vg of M3 for drain current 0.875mA to flow. 

For this :-

- Set up the circuit and give the value for the resistors based on the above analysis.
- Set the voltage of Vg = {V}'.
- Go to the Spice directive and write ".lib tsmc018.lib" and ".step param V 0V 5V".
- Now right click on the MOSFET, set the value of the channel length and width of the MOSFET same as previous circuit i,e L=180nm and W=2.525µ.
- Then run the simulating in DC op pnt mode, a co-ordinate plane will popup now bring the cursor on the wire near the drain of MOSFET M3 and select the current.
- On the graph right click, select "Add Traces" and give the value of the drain current of MOSFET M3 (0.875mA) there.
- Use "Place_Cursor on Active Trace" using the cursor we find the intesection of this two line as 1.432V, which is the gate voltage Vg of MOSFET M3.
- Set the Vg = 0.875mA for the M3 MOSFET.
- Then click on the run icon, you will get :-

![freq](https://github.com/shivaanii33/LIC-Lab/blob/1116e0b6857c22374a9a1c17b55ab437d419b384/images/Screenshot%202025-03-07%20025920.png)


Here we can see Id = 0.437425mA , Vds = 1.70051-0.5991 = 1.1V (Vds = Vd-Vs), Id(M3)=0.874851V Vp = 0.5991V and Vocm = 1.70051V ,which is equal to the analysis we have done.

## Transient Analysis.
Procedure for Transient analysis in LTSpice

- Remove the ".op".
- Right click on the Vicm1 and select "Advanced".
- Then on the function select "SINE".
- Set DC offset = 1.6V, Amplitude = 50mV and Frequency = 1kHz.
- Then click "ok".
- Run the simulation by selecting "Transient" mode and setting Stop time as 5ms (Since freq = 1kHz, time period = 1ms and this 5ms simulation time allows you to capture 5 full cycles of the sine wave.
- You will get:-

![freq](https://github.com/shivaanii33/LIC-Lab/blob/35d42d2d0460f207eac10fb980b74a230f25c6d4/images/Screenshot%202025-03-07%20024628.png)

Here we can see that the amplitude of the output waveform is 1.7901093-1.6971968 = 0.0929125V. The input amplitude is 50mV so Gain, Av = -Vout/Vin = -0.0929125V/50mV = -1.85825. Therefore, Gain,Av = -1.85825.

---

## AC Analysis.

Procedure for AC analysis in LTSpice

- Right click on the Vicm1 and on the Small signal AC Analysis set Amplitude = 1.
- (Amplitude = 1 is a standard practice because Gain, Av = -Vout/Vin and Vin (AC Amplitude) = 1V, then Gain=Vout
- Click on the run icon and select the AC Analysis mode.
- Set Type of sweep = Decade, Number of points per decade = 20 and Start frequency = 1Hz and Stop frequency = 2THz.
- Click "ok".
- Then you will get :-

![freq](https://github.com/shivaanii33/LIC-Lab/blob/0eac1932cae830babdadadf5e18cef37dc3fde30/images/Screenshot%202025-03-07%20024809.png)

---


# Inference 


In a **MOS differential amplifier**, the choice of the tail current source significantly impacts **gain, output swing, and common-mode rejection ratio (CMRR)**. This document compares three configurations: using a **resistor (Rss)**, an **ideal current source (Iss)**, and an **NMOS current source**.

---

##  Using a Resistor (Rss) as Tail Current Source

### Differential Gain: **Moderate**
- The gain is limited because the resistor sets the tail current passively.
- Gain equation:
  ```math
  A_d = \frac{g_m R_D}{1 + g_m R_{SS}}
  ```

###  Output Voltage Swing: **Limited**
- The resistor causes a voltage drop, reducing the available output swing.

###  Common-Mode Rejection Ratio (CMRR): **Low**
- The low impedance of the resistor allows common-mode noise to affect both transistors in the differential pair.

**Reason:**
- The resistor does not actively control current flow, so it limits performance in gain, swing, and noise rejection.

---

## Using an Ideal Current Source (Iss) as Tail Current Source

###  Differential Gain: **Higher**
- The ideal current source provides a **fixed** tail current, improving gain.
- Gain equation:
  ```math
  A_d \approx g_m R_D
  ```

###  Output Voltage Swing: **Improved**
- Since the current source doesn’t introduce a voltage drop, more supply voltage is available for the output swing.

###  Common-Mode Rejection Ratio (CMRR): **Better**
- High impedance isolates the differential pair from common-mode signals.

**Reason:**
- A stable current improves amplifier efficiency and noise rejection.

---

## Using an NMOS Current Source as Tail Current Source

### Differential Gain: **Highest**
- The NMOS current source provides high output resistance, leading to maximum gain.

### -  Output Voltage Swing: **Best**
- The NMOS current source minimizes voltage loss in the tail, allowing a **wider** output swing.

###  Common-Mode Rejection Ratio (CMRR): **Maximum**
- The highest impedance results in superior isolation from noise and power fluctuations.

**Reason:**
- The NMOS current source actively adjusts to maintain a steady current, optimizing performance.

---

##  Summary of Performance Comparison

| Tail Current Source  | Gain | Output Swing | CMRR |
|----------------------|------|-------------|------|
| **Resistor (Rss)**  | Moderate | Limited | Low |
| **Ideal Current Source (Iss)**  | Higher | Improved | Better |
| **NMOS Current Source**  | Highest | Best | Maximum |

###  **Key Takeaways:**
- **A resistor limits performance** due to voltage drop and low impedance.
- **An ideal current source improves gain, output swing, and CMRR.**
- **An NMOS current source gives the best performance** in all aspects.
 **For high-performance differential amplifiers, replacing Rss with an NMOS current source is the best choice!**









































