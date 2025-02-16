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

