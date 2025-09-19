# SPICE overview and CMOS fundamentals

## What is SPICE
SPICE (Simulation Program with Integrated Circuit Emphasis) is an industry-standard Circuit Simulator. It takes a circuit description in the form of a netlist: transistors, resistors, capacitors, sources, etc., and mathematically solves how voltage and current behave over time in that circuit.

## Why is SPICE needed? 
SPICE serves as the foundation in digital VLSI design, providing accurate modeling and characterization of standard cells and macros, which is essential for timing, power, variation, noise, and signal integrity analyses.

## CMOS Fundamentals

### Inverter 
An inverter uses PMOS and NMOS transistors. The PMOS connects to VDD and the NMOS to GND. The gates are tied to the input, and the drain is tied to the output.  
![img1](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2014/Images/Intro/img1.png)

### Analysis of Inverter using SPICE
Simulating a CMOS inverter in SPICE verifies its functionality, measures propagation delay, and calculates dynamic and static power. Designers obtain voltage transfer characteristics as well as Id–Vout plots for NMOS and PMOS devices under different input conditions.  
![img2](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2014/Images/Intro/img2.png)

### Delay 
The cell delays depend on input slew and output load. Delay information is stored in a 2D lookup table, where the delay is mapped as a function of input slew and output load.  
![img3](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2014/Images/Intro/img3.png)

### NMOS Transistor
![img5](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2014/Images/Intro/img5.png)
![img4](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2014/Images/Intro/img4.png)

### Threshold Voltage
* Cut off region of operation 
* The NMOS is currently turned off. So there is no conducting path between the source and drain  
![img6](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2014/Images/Intro/img6.png)
![img7](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2014/Images/Intro/img7.png)
* In a P–N junction diode, when a reverse bias is applied, a depletion region forms, which is depleted of majority carriers.
![img8](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2014/Images/Intro/img8.png)
![img9](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2014/Images/Intro/img9.png)
![img10](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2014/Images/Intro/img10.png)

* As VGS increases further, a point is reached where enough electrons are attracted to invert the surface from p-type to n-type. This condition defines the threshold voltage (Vth).  
![img11](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2014/Images/Intro/img11.png)

### Body Effect
When the source-to-body voltage is zero, surface inversion occurs under the gate. However, when the source-to-body voltage is greater than zero, the threshold voltage increases due to the reverse bias across the body–source junction. This widens the depletion layer, requiring a higher Vgs to achieve strong inversion. This phenomenon is known as the body effect.  
![img12](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2014/Images/Intro/img12.png)  
![img13](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2014/Images/Intro/img13.png)
![img14](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2014/Images/Intro/img14.png)
![img15](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2014/Images/Intro/img15.png) 

## Resistive/ Linear Region of Operation 
* Considering the Vgs >= Vth and small Vds(drain to source) applied across the channel.
![img1](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2014/Images/Linear%20operation/img1.png)

### Drain Current Equation  
![img2](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2014/Images/Linear%20operation/img2.png)
![img3](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2014/Images/Linear%20operation/img3.png)
![img4](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2014/Images/Linear%20operation/img4.png)
![img5](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2014/Images/Linear%20operation/img5.png)
![img6]()  
* For all the values of Vds if `Vds < = Vgs -Vt` the MOSFET (device) will operate in a linear/ resistive region of operation.  
![img7]()

## Saturation Region
