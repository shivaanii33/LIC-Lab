# CURRENT MIRROR <br>
A current mirror is an essential circuit used in analog electronics to copy a reference current from one active device to another while maintaining a stable and accurate current flow (Iref = Iout). It is widely employed in biasing circuits, active loads, and differential amplifiers<br>
![what is current mirror](https://github.com/user-attachments/assets/1768da11-0189-48ea-9dc7-6f677b3c4609)
<br>
## WORKING PRINCIPLE OF CURRENT MIRROR :<br>

#### 1. Reference Current Generation:<br>
* The first transistor (M1) is configured in a diode-connected manner (drain and gate shorted).<br>
* A reference current Iref is forced through M1 using a current source or resistor.<br>
* This sets the transistor’s gate-source voltage (Vgs1) which defines the operating point.<br>
<br>

#### 2. Mirroring the Current<br>

* The second transistor (M2) has its gate connected to M1’s gate.<br>
* Since both transistors share the same (Vgs) , they ideally conduct the same drain current, provided they have the same W/L ratio and are in saturation.<br>
* The mirrored current (Iout) is approximately equal to Iref.<br>
<br>

#### 3. Output Current Scaling <br>

* If the W/L ratio of M2 is different from M1, the output current is scaled<br>
* I<sub>out</sub>/I<sub>ref</sub> = (W/L)<sub>2</sub>/(W/L)<sub>1</sub> <br>
therefore,<br>
I<sub>out</sub> = (W/L)<sub>2</sub>/(W/L)<sub>1</sub> * I<sub>ref</sub> <br>
<br>

## Key Conditions for Proper Operation : <br>

#### Both transistors should be in saturation<br>

This ensures that the drain current depends only on V<sub>gs</sub> and not on V<sub>ds</sub> <br>

#### Matching of Transistors <br>

Fabrication variations can cause mismatch in threshold voltage (V<sub>th</sub>), affecting accuracy.<br>

#### Channel Length Modulation<br> 

Practical mirrors suffer from a small variation in I<sub>out</sub>due to V<sub>ds</sub> changes.<br>
Using a cascode current mirror reduces this effect by increasing output resistance.<br>

-----------------------------------------------------------------------------------------------------------------------------

## PMOS Current Mirror<br>

![image](https://github.com/user-attachments/assets/1a870006-1e99-448a-b5e7-c4ddd99f8417)
<br>
This shows the implementation of current mirror using the PMOS transistors. In PMOS current mirror, the source terminals for both transistors are connected to Supply voltage Vdd.<br>
The relation between the Iout and Iref can be given by the same expression.<br>
I<sub>out</sub> = (W/L)<sub>2</sub>/(W/L)<sub>1</sub> * I<sub>ref</sub> <br>
The only thing which needs to be ensured is that M1 should operate in the saturation region. Or in other words, VSD1 ≥ VSG – |VTP |, Where VTP is the threshold voltage of the PMOS transistor.<br>

-------------------------------------------------------------------------------------------------

## SIMULATION : NMOS current mirror circuit with a resistive load<br>
#### Circuit Components & Functionality:<br>
* V1 (1.8V Supply): Provides the operating voltage for the circuit.<br>
* Iref (100µA): Sets the reference current through M2.<br>
* M2 (Diode-Connected NMOS): Operates in saturation and sets the gate voltage Vx.<br>
*M1 (Mirroring NMOS): Copies the current from M2 to R1.<br>
*R1 (820Ω Load Resistor): Converts the output current into a voltage.<br>

![ckt dia](https://github.com/user-attachments/assets/f1a42946-8c17-4549-82df-3ef7a192b852)

#### OBSERVATION TABLE :<br>
For Iref = 100u<br>

|Iout (Expted)(A) |Iout(appeared)(A) |(W/L)<sub>2</sub> |(W/L)<sub>1</sub> | Vx (V) |Vout(V) |
|-----------------|------------------|------------------|------------------|--------|--------|
|100u             |103.5u            |180n/180n         |180n/180n         |1.27    | 1.71   |
|100u             |10.715u           |500n/500n         |500n/500n         |1.43    | 1.717  |
|100u             |100.648u          |1u/1u             |1u/1u             |1.39    | 1.7174 |
|200u             |197.6u            |1u/2u             |1u/2u             |1.397   |  1.63  | 
|100u             |101.5u            |1u/2u             |1u/2u             |1.087   | 1.716  | 
|100u             |102.131u          |1u/3u             |1u/3u             |0.95    |1.7172  |

* ##### Iout is slightly higher than the expected value in most cases.<br>
For W/L = 180n/180n , expected Iout=100uA, but appeared Iout = 103.5uA. This happens because as Vds increases, the effective channel length decreases, causing higher drain current.<br>
* ##### Higher W/L ratios (shorter channel lengths) show more deviation.<br>
For W/L = 500n/500n , Iout=100uA drops significantly (10.715μA), indicating increased channel length modulation effects.Shorter channel lengths mean higher λ, leading to larger variations in current.<br>
* ##### For longer transistors (L increased),Vx is lower, stabilizing Iout): <br>
Vx decreases as L increases .<br>

------------------------------------------------------------------------------------------------
## PART - A <br>
## SIMULATION : PMOS Current Mirror with NMOS Amplifier <br>

### Design a current mirror circuit which has a gain of AV = -10V/V, power supply of Vdd = 1.8V, and power of P <= 1mW. Find reference current (Iref), output current (Id), and total current (Itotal). Perform DC and AC analysis for mirror ratio 1:1, 1:2. Vary length from 180nm -> 500nm -> 1µm and do the analysis.<br>

### FOR 1:1 RATIO 

![main ckt diagram part1](https://github.com/user-attachments/assets/0975d4af-b847-4b85-8189-c35c5cf32b6d)

This circuit consists of a PMOS current mirror (M1 & M2) and an NMOS amplifier stage (M3). The purpose of this circuit is to generate a stable bias current and amplify an input signal.<br>

##### Calculation:<br>
Given , Vdd = 1.8V and P<=1mV <br>
for P= 1mV, <br>
Itot = P/Vdd = 1m / 1.8 = 0.55mA 
###### Iout = 0.55mA
Itot = Iref + Iout <br>
for 1:1 ratio Iref = Iout <br>
Therefore ,<br>
###### Iref = Iout = Itot/2 = 0.277mA <br>
for Vin,<br>
as Vin = Vgs3 , Vin>=Vth<br>
###### Vin>= 0.48V<br>
also,<br>
###### Vout = Vdd/2 = 0.90V <br>
###### Vout = Vx = 0.90V<br>

### DC ANALYSIS :<br>

#### For L = 180n <br>
![180n 1isto1 ](https://github.com/shivaanii33/LIC-Lab/blob/9346f5b8a0b04e459ae7f2dbf26056b99f726300/images/Screenshot%202025-04-04%20001653.png)

#### For L = 500n <br>
![500n 1isto 1 ratio](https://github.com/shivaanii33/LIC-Lab/blob/9346f5b8a0b04e459ae7f2dbf26056b99f726300/images/Screenshot%202025-04-04%20001708.png)

#### For L = 1u <br>
![1u 1isto 1 ratio](https://github.com/shivaanii33/LIC-Lab/blob/9346f5b8a0b04e459ae7f2dbf26056b99f726300/images/Screenshot%202025-04-04%20001720.png)

#### COMPARISION TABLE :<br>

|Iref (A)    |Iout (A)   |(W/L)<sub>1</sub> |(W/L)<sub>2</sub> |(W/L)<sub>3</sub> |  Vx (V) |Vout(V) |
|------------|-----------|------------------|------------------|------------------|---------|--------|
|0.277m      |0.277m     |7.3u/180n         |7.3u/180n         |117.94u/180n      | 0.90    |0.90    |
|0.277m      |0.277m     |22u/500n          |22u/500n          |119.6u/500n       | 0.90    |0.90    |
|0.277m      |0.277m     |44.24u/1u         |44.24u/1u         |234.254u/1u       | 0.90    |0.90    |

* The current mirror is highly stable with negligible variations in Iout.<br>
* Channel length modulation does not significantly impact the circuit, likely due to the long-channel MOSFETs used.<br>

### TRANSIENT ANALYSIS : <BR>
for Amplitude = 5m and f= 1kHz <br>
Vin is the gate voltage of m3 (nmos) <br>
(V)<sub>gs3</sub> = Vg - Vs (Vs=0V) <br>
###### Vin(min) = (V)<sub>gs3</sub> = 0.5V <br>
Now, <br>
Voutmax = Vdd - |Vov1 + Vov2 |<br>
Vov1 = Vx - Vth1 = 0.9 - 0.36 = 0.4V <br>
Vov3 = Vin - Vth3 = 0.5 - 0.36 = 0.14V <br>
###### Voutmax = 1.8 - (0.4 + 0.14) = 1.62V <br>

### CASE 1 : For L = 180n <br>
#### For Vin < 0.5V <br>
i.e Vin=0.45V<br>
![0 45V 1isto1 transient](https://github.com/user-attachments/assets/5905bec6-3d95-4d71-8b83-066b7eed67c6)

When Vin is below 0.5V in your circuit, the output gets distorted because MOSFET M3 Moves Out of Saturation. <br>
#### For Vin >= 0.5V <br>
i.e Vin=0.5V<br>
![0 5V Voutpp max 1isto1](https://github.com/user-attachments/assets/80f6e735-25fd-430b-b670-1cef862d4eb7)

Voutpp = 0.34+ 1.37 = 1.72 V <br>
|                |theoretical       | practical       |
|----------------|------------------|-----------------|
|Vinmin          | 0.5V             | 0.48V           |
|Voutmax         | 1.65V            | 1.72V           |

#### CASE2: For L = 500n <br>

![image](https://github.com/user-attachments/assets/b6d3cbf3-a7f9-415a-9f43-c9c397d51914)

Voutpp = 0.4 + 1.29 = 1.69V <br>

#### CASE 3: For L = 1u <br>

![image](https://github.com/user-attachments/assets/bd3ddf01-3c9b-4328-8dd9-2f1b575f5915)

Voutpp = 0.34 + 1.36 = 1.7V <br>


### AC ANALYSIS :<br>
### CASE 1 : For L = 180n <br>
![ac analysis 1isto1](https://github.com/user-attachments/assets/7515d0d7-5dba-4534-aa05-bb49a3aaac5d)

Av (dB) = 29.82 dB<br>
Av (in V/V) = 10^(29.82/20) = 30.97V/V
Now,<br>
3dB gain = 29.82-3 = 26.82 dB <br>
Bandwith = 104.06MHz <br>

#### CASE2: For L = 500n <br>

![image](https://github.com/user-attachments/assets/f18a3e2c-7312-4b35-8e32-6a7fc1cbaf78)

Av (dB) = 39 dB<br>
Now,<br>
3dB gain =39-3 = 38 dB <br>
Bandwith = 24.3 MHz <br>

#### CASE 3: For L = 1u <br>

![image](https://github.com/user-attachments/assets/12c16043-8ac6-4a3f-b31f-61b57d53df8c)

Av (dB) = 41 dB<br>
Av (in V/V) = 10^(41/20) = 112V/V
Now,<br>
3dB gain = 39-3 = 36 dB <br>
Bandwith = 41.1 MHz <br>


------------------------------------------------------------------------------------------------------------------------------

### FOR 1:2 RATIO <br>

![image](https://github.com/user-attachments/assets/4d695997-7f72-4c18-8b69-9c1e4956ee61)

This circuit consists of a PMOS current mirror (M1 & M2) and an NMOS amplifier stage (M3). The purpose of this circuit is to generate a stable bias current and amplify an input signal.<br>

##### Calculation:<br>
Given , Vdd = 1.8V and P<=1mV <br>
for P= 1mV, <br>
Itot = P/Vdd = 1m / 1.8 = 0.55mA 
###### Iout = 0.55mA
Itot = Iref + Iout <br>
for 1:2 ratio Iout = 2Iref <br>
Therefore ,<br>
###### Iref = Itot/3 = 0.183 mA <br>
###### Iout = 2Iref = 0.366 mA <br>
Now<br>
###### Vin>= 0.48V<br>
also,<br>
###### Vout = Vdd/2 = 0.90V <br>
###### Vout = Vx = 0.90V<br>

### DC ANALYSIS :<br>

#### For L = 180n <br>

![180n 1i2](https://github.com/shivaanii33/LIC-Lab/blob/9346f5b8a0b04e459ae7f2dbf26056b99f726300/images/Screenshot%202025-04-04%20001744.png)

#### For L = 500n <br>

![500n 1isto2](https://github.com/shivaanii33/LIC-Lab/blob/9346f5b8a0b04e459ae7f2dbf26056b99f726300/images/Screenshot%202025-04-04%20001754.png)

#### For L = 1u <br>

![1u 1isto 2 ](https://github.com/shivaanii33/LIC-Lab/blob/9346f5b8a0b04e459ae7f2dbf26056b99f726300/images/Screenshot%202025-04-04%20001805.png)

#### COMPARISION TABLE :<br>

|Iref (A)    |Iout (A)   |(W/L)<sub>1</sub> |(W/L)<sub>2</sub> |(W/L)<sub>3</sub> |  Vx (V) |Vout(V) |
|------------|-----------|------------------|------------------|------------------|---------|--------|
|0.183m      |0.366m     |5m/180n           |10m/180n          |155.82m/180n      | 0.90    |0.90    |
|0.183m      |0.366m     |14.28m/500n       |29.16m/500n       |263.88m/500n      | 0.90    |0.90    |
|0.183m      |0.37m      |29.2m/1u          |59.4m/1u          |314.86m/1u        | 0.90    |0.90    |

* The current mirror is highly stable with negligible variations in Iout.<br>
* Channel length modulation does not significantly impact the circuit, likely due to the long-channel MOSFETs used.<br>

### TRANSIENT ANALYSIS : <BR>
for Amplitude = 5m and f= 1kHz <br>
Vin is the gate voltage of m3 (nmos) <br>
(V)<sub>gs3</sub> = Vg - Vs (Vs=0V) <br>
###### Vin(min) = (V)<sub>gs3</sub> = 0.5V <br>
Now, <br>
Voutmax = Vdd - |Vov1 + Vov2 |<br>
Vov1 = Vx - Vth1 = 0.9 - 0.36 = 0.4V <br>
Vov3 = Vin - Vth3 = 0.5 - 0.36 = 0.14V <br>
###### Voutmax = 1.8 - (0.4 + 0.14) = 1.62V <br>

#### For Vin >= 0.5V <br>
i.e Vin=0.5V<br>
![1st2 transient](https://github.com/user-attachments/assets/14155830-9a1c-4fa1-ba7f-48b2d6eb9448)

Voutpp = 0.75+ 1.062 = 1.812 V <br>
|                |theoretical       | practical       |
|----------------|------------------|-----------------|
|Vinmin          | 0.5V             | 0.48V           |
|Voutmax         | 1.65V            | 1.812V          |

### AC ANALYSIS :<br>

![ac 1 isto 2](https://github.com/user-attachments/assets/8698ab31-545e-4384-9044-601b47b0adc6)

Av (dB) = 29.82 dB<br>
Av (in V/V) = 10^(29.82/20) = 30.97V/V
Now,<br>
3dB gain = 29.82-3 = 26.82V/V <br>
Bandwith = 104.06MHz <br>

#### Inference:
*Reference current is copied or mirrored for other two mosfets.The output currentis exactly equal to the reference current.
*The output current remains the same regardless of the connected load, as long as the transistor stays in the saturation region
*Vx and Vout will be same when current gets mirrored.
*As length increases Vx and Vout decreases.
*As gain increases bandwidth decreases.
*As the refence current is 0.277mA and doing 1:1 ratio of current mirroring the Current must be copied of the same that is 0.277mA.
*In transient analysis we see the maximum output swing caused.

------------------------------------------------------------------------------------------------------------------------------
## PART - B <br>
## SIMULATION : Differential Amplifier with Current Mirror Load <br>

### Design differential amplifie for following specifications Vdd=2.5V, P≤3mW, Vicm = 1.3V, Vocm = 1.4V, Vp = 0.5V. Perform DC analysis, transient analysis & frequency response and extract the required parameters.

![image](https://github.com/user-attachments/assets/d3d28dfb-8522-43b2-a0b6-ed6ff853c3c9)

This circuit is a CMOS Differential Amplifier with a Current Mirror Load, commonly used as the input stage of an Operational Amplifier (Op-Amp) or as a Comparator. It amplifies the difference between two input voltages (Vin1, Vin2) while rejecting common-mode signals<br>

### DC ANALYSIS :<br>

![image](https://github.com/shivaanii33/LIC-Lab/blob/a00ab8cf1dd6c01ae50a92310dbddcfa7b6979c6/images/Screenshot%202025-04-04%20002840.png)

| Parameter    | Theoretical value  | Practical value |
|--------------|--------------------|-----------------|
|Voutcm        | 1.40V              | 1.40V           |
|Vp            | 0.5V               | 0.62V           |
|Id1,Id2       | 0.5mA              | 0.48mA          |
|Iss           | 1mA                | 0.96mA          |
|Id3,Id4       |0.5mA               | 0.48mA          |
|Iref          |0.5mA               | 0.5mA           |

### TRANSIENT ANALYSIS : <BR>

#### For Vin < 1.3V <br>
i.e Vin(min) = 0V<br>

![0V](https://github.com/user-attachments/assets/82261936-55e7-462b-a3c2-827fed7602a0)

For Vin=0V also the amplification takes place with high output peak to peak.<br>

#### For Vin > 1.3V <br>

i.e Vin = 1.3V<br>

![image](https://github.com/user-attachments/assets/515200f5-8d67-4ac9-bbf2-6f2af429d284)

Voutpp = 1.39+1.40 = 2.79V 

i.e Vin = 3V<br>
![image](https://github.com/user-attachments/assets/7554c19d-2c68-4bdd-85f1-6657fd18782a)

there is a distortion in output wavwform <br>

Therefore <br>
|Parameter      |Theory value  | Practical value |
|---------------|--------------|-----------------|
|Vincm(min)     | 0.86V        | 0V              |
|Vincm(max)     | 1.76V        | 2.79V           |

### AC ANALYSIS :<br>

![ac ](https://github.com/user-attachments/assets/132c0fff-c2c5-486c-8498-45c254ff8361)

Av (dB) = 32.2 dB<br>
Av (in V/V) = 10^(32.2/20) = 40.7V/V
Now,<br>
3dB gain = 32.2 - 3 = 29.2V/V <br>
Bandwith = 7GMHz <br>

-------------------------------------------------------------------------------------------------------------------------------------------------------------------

#### Inference:<br>
* Differential Pair (M3 & M4) : Vin1 and Vin2 and generates a differential current.Operates in saturation for linear amplification.
* Current Mirror Load (M1 & M2) :Converts the differential current into a single-ended output.Provides high gain by increasing output resistance.
* Biasing Current Source (M6) : Ensures a constant bias current for stable operation.Determines the gain and bandwidth of the amplifier.
* Active Load (M5):Helps improve the circuit's linearity and output swing.
* Output Distortion for Vin <0.5V : If Vin is too low, M3 or M4 enter triode, causing distortion.Proper biasing is required to maintain transistors in saturation.
* Channel Length Modulation Effect: Causes a slight increase in drain current as Vds increases.
  Affects output voltage but is minimized by using longer channel lengths.




