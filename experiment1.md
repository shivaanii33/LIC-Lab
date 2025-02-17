 EXPERIMENT 1: CS Amplifier 

**AIM**: To simulate the CS amplifier circuit of the MOSFET in the LTspice and obtain DC analysis, AC analysis, transient analysis and determining DC operating point, gain, bandwidth, power also observing the variations of current by varying width and length of the channel.



**OVERVIEW**:A Common Source (CS) Amplifier is a widely used circuit in analog electronics, employing a **MOSFET** for signal amplification. It features a common source, producing a high voltage gain with a 180° phase shift between input and output. The amplifier’s performance is analyzed through DC analysis (t#o determine the biasing point), AC analysis (to study gain and frequency response), and transient analysis (to observe signal behavior over time). Due to its efficient signal amplification, it is commonly found in audio processing, RF applications, and integrated circuits.



**COMPONENTS**:

- TSMC 180nm nmos-4
- Resistor (1K)
- Voltage source VDD = 1.8V
- Voltage source VGG = 0.9V

**CIRCUIT DIAGRAM**

![**CIRCUIT DIAGRAM**](https://github.com/user-attachments/assets/6a264d54-8c24-48e5-b80f-b56bb802bf07)

 
 **PROCEDURE**:
 
 - Set up the circuit in the LTspice
 - From the spice director attach the library file 
 - Specify the values for the parameters as resistor (1K), VGG(0.9), VDD(1.8).
- For MOSFET choose model name- CMOSN, at first instance consider length=180nm and width=1um 
- Configure the analysis for *DC operating* point and observe the value of drain current ID and output voltage VDS
- By using the values of current verify that the mos is operating in the saturation region 
- Change the values of channel width and the lenght and observe the variation in the value of the current.
- Given the power budget as 50uW now we have **P=VDD x ID**, since VDD is fixed we get the value of ID 
- Now assume the suitable values for lenth and width such that the resulting current value should be almost nearer to the above calculated value.
---
### *Transient analysis*: - 
- set input voltage sine wave 1khz 50mv and dc offset value 0.9v 
- simulate-> transient, set stop time 5ms and run simulation 
### *AC analysis*
- set AC amplitude as 1v and configure for ac analysis tyoe of sweep- decade,no of points per decade-20, start frequency 0.1hz, stop frequency - 1T .
- from this obtain gain and bandwidth 


## **Results**

**DC analysis**:


![**DC Analysis**](https://github.com/shivaanii33/LIC-Lab/blob/a2e7792216f34f35c2d6729522f7ddca4c611f78/Screenshot%202025-02-16%20223019.png)



*Result when the width is changed to 2u*

![**DC Analysis**](https://github.com/shivaanii33/LIC-Lab/blob/91b65bb995e31e59b2d61a9a07c9a5c22f928099/Screenshot%202025-02-17%20193234.png)


*since power budget is 50uW and vdd is given as 1.8v the current is expected to be around 27.7uA so,*

![**DC Analysis**](https://github.com/shivaanii33/LIC-Lab/blob/90c1ae5e4dcf181c45f5ba8f60c76defa849c150/images/Screenshot%202025-02-17%20195210.png)


![**DC Analysis**](https://github.com/shivaanii33/LIC-Lab/blob/cef8cb52a5b539df14a1e15b32d7279f91930f54/images/Screenshot%202025-02-17%20195159.png)


**transient analysis**

![**Transient Analysis**](https://github.com/shivaanii33/LIC-Lab/blob/3b5fd6be15d3d642b0dec34118fb002b744bec7e/images/Screenshot%202025-02-17%20195936.png)


![**Transient Analysis**](https://github.com/shivaanii33/LIC-Lab/blob/6a66d9d98ce1d1d78b31a285663990adff9e5979/images/Screenshot%202025-02-16%20224337.png)


![**Transient Analysis**](https://github.com/shivaanii33/LIC-Lab/blob/53b9756304a5671c2cc261bb2e2c17c8f2365143/images/Screenshot%202025-02-17%20183019.png)


**frequency analysis**

![**ac  Analysis**](https://github.com/shivaanii33/LIC-Lab/blob/02d000ddcff2812b2899f742c7bd16ddf72aca53/images/Screenshot%202025-02-17%20200800.png)


![**ac  Analysis**](https://github.com/shivaanii33/LIC-Lab/blob/c5aa1ec3d8c2e7e695befa5d8ccf85bf4950575a/images/Screenshot%202025-02-17%20185727.png)


## INFERENCE 
- Since here we have used the MOSFET working as an amplifier, the region of the Mosfet should be the saturation region
So during each analysis, and while assigning the values for the parameters, such as width and length, we have to ensure that the transistor is working in the saturation region Once we obtained the current that is (VGD<Vth) 
And VGD= VG -VD
- From the DC analysis of the CS amplifier, it was observed that with increase in the value of width, the value of the current will also increase is directly proportional to width and inversely proportional to the length 
Id= 1/2(kn.W/L.VOV^2) 
When the value of the width is increased to twice of it, the current will not exactly increase to 2 times of it, but a little lesser than that this is because of the channel length modulation
- CALCULATION:
Power = 50uW

Loop Equation: Vdd=Vds+Id*Rd

P=I*V (Id=27.08uA , Vdd=1.8V)
- The transient response graph confirms that the circuit transitions smoothly over time. The circuit responds effectively to input variations, indicating stable operation.
- The AC response graph confirms that the circuit maintains stability over the tested frequency range.
- The gain(4 dB) and phase shift (which is nearly 180deg) align with theoretical expectations.The circuit functions as expected under AC conditions.


# Design 2:


Replacing the resistor of design 1 by another pmos:

**CIRCUIT DIAGRAM**:


![**CIRCUIT DIAGRAM**](https://github.com/shivaanii33/LIC-Lab/blob/cfe6b32fc53bf6aff9e46231e061ccf20323a67d/images/Screenshot%202025-02-17%20231924.png )

---

**COMPONENTS**:

- TSMC 180nm nmos-4
- TSMC 180nm pmos-4
- Voltage source VDD = 1.8V
- Voltage source VGG = 0.9V
---
**PROCEDURE**:

- Make the circuit connection as show above.
- Connect DC power supply to the gate terminal of each mos
- Connect the source terminal of nmos to the ground.
- Connect the source terminal of pmos to VDD 1.8V
- Connect the drain terminals of each mosfet.
- Proceed with different analysis and find the required parameters.
---

## DC Analysis:


Our approach in conducting DC analysis involves identifying the quiescent operating point (ID) and node voltages that are required to operate the MOSFET.

- **Supply Voltage (VDD)**: 1.8V  
- **Gate Voltage (VG)**: 0.9V  
- **Power Budget (P)**: 50μW  

*The Figure below shows the Values obtained from the DC Analysis :*

![**DC Analysis**](https://github.com/shivaanii33/LIC-Lab/blob/cfe6b32fc53bf6aff9e46231e061ccf20323a67d/images/Screenshot%202025-02-17%20225416.png)



---
## Transient Analysis


By examining the transient response of the amplifier, it is possible to determine its behavior over time when subjected to the sinusoidal input.

**Parameters**

- Stop Time: 5m (5 milliseconds)

The transient analysis provides information about the amplifier's time-domain behavior, such as distortion, settling time, and waveform reproduction.

 *The Graph below shows the Transient Response of the Given Design;*
 
![**Transient Analysis**](https://github.com/shivaanii33/LIC-Lab/blob/cfe6b32fc53bf6aff9e46231e061ccf20323a67d/images/Screenshot%202025-02-17%20225536.png)


--- 
## AC Analysis

A sinusoidal input is included in the AC analysis through a modification of gate voltage.

**Sinusoidal Input Voltage**

- DC Offset: 0.9V  
- Amplitude: 50mV  
- Frequency: 1kHz

**Frequency Sweep Parameters**

- Type: Decade  
- Sweeps per Decade: 20  
- Start Frequency: 0.1Hz  
- Stop Frequency: 1THz  

By analyzing the AC, one can determine gain, bandwidth, phase, and other characteristics of the amplifier's frequency response.

*The Graph below shows the AC Analysis of the Given Design;*

![**AC Analysis**](https://github.com/shivaanii33/LIC-Lab/blob/cfe6b32fc53bf6aff9e46231e061ccf20323a67d/images/Screenshot%202025-02-17%20230423.png)

---

# Inference:
**DC Analysis**
- The drain current (ID) is around 27.78A, ensuring that the MOSFET operates in the desired region.
- Proper biasing conditions provide a stable and reliable amplification setup.

**AC Analysis**
- The gain and bandwidth were analyzed using an AC sweep, helping to understand frequency response.
- The amplifier performs well across a range of frequencies, including cutoff frequencies and phase behavior, making it suitable for various applications.

**Transient Analysis**
- The amplifier accurately reproduces the input signal without distortion, proving its effectiveness.
- The design meets the expected performance criteria and follows theoretical predictions, demonstrating its feasibility in practical applications.



