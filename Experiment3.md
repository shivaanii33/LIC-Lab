
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

Hence the required Qpoint for both the transistors are (*since both halk of circuits are mirror's of each other*)

- **M1 Q-Point(VDS1,Id1) -> (1.14V,0.4375mA)**
- **M2 Q-Point(VDS2,Id2) -> (1.14V,0.4375mA)**

---
### Procedure for the simulation in ltspice

- Create a new Experiment Workspace
- Enter a spice directive by clicking on .t option on the ribbon  .lib tsmc018.lib  This specifies the BSIM3 Model of the MOSFET, if you stored this file in some other location specify that in the command
- Add the transistor NMOS4 and Change the name of the transistor to CMOSN
- Assign the specified values for the voltages and the resistors
- Now we can start finding appropriate Aspect Ratio for our MOSFET, we will take a range and combination of values for W (width) and L (length) of the MOSFET
- After getting a suitable value we will perform Transient and AC Analysis.

  
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

- SPICE output log

![DC operating](https://github.com/shivaanii33/LIC-Lab/blob/b9f937da41d45a25a75f579fd065d40de742de77/images/Screenshot%202025-03-04%20010311.png)

**The valvue of Gm is 1.12e-03**

**The value of Vt=0.489V**

---

*Also we have to verify that the transistor is working in saturation region, this can be done by checking that whether VGD is greater than or lesser that Vt*

For VGD=VG-VD=1.6-1.70

VGD = -0.10 , but Vt=0.489V

Hence **VGD<Vt**; therefore mosfets are in saturation region.




















