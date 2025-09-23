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
![img6](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2014/Images/Linear%20operation/img6.png)  
* For all the values of Vds if `Vds < = Vgs -Vt` the MOSFET (device) will operate in a linear/ resistive region of operation.  
![img7](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2014/Images/Linear%20operation/img7.png)

## Saturation Region
* When Vgs - Vds > Vth, then a conducting channel will be formed and current will be induced.
* **Pinch-off Region Condition**
As Vds increases, the inversion charge is strong at the source end since Vgs - Vds > Vth. But toward the drain end, the effective gate voltage Vgs - V(x)
reduces. When it falls to equal or less than Vt, the channel is said to be pinched off at the drain side. In this region, the inversion charge density is minimal, and the channel narrows, but current continues to flow due to carrier drift in the high-field depletion region.  
  
![img8](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2014/Images/Linear%20operation/img8.png)
![img9](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2014/Images/Linear%20operation/img9.png)
![img10](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2014/Images/Linear%20operation/img10.png)
* When  Vgs - Vds < Vth, at this point, the conducting channel disappears or is pinched off starting from the Drain end.  
![img11](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2014/Images/Linear%20operation/img11.png)

### Drain current model for Saturation Region
* By increasing the Vds beyond Vds sat, i.e. the value of (Vgs- Vth) has no effect on the channel shape and charge. Thus, the current through the channel remains constant at the value reached for Vds = Vgs -Vth. The MOSFET is said to have entered saturation/ pinch-off region at: Vds sat = Vgs - Vth
* Any increase in Vds above Vds sat appears as a voltage drop across the depletion region. 

![img12](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2014/Images/Linear%20operation/img12.png)
![img13](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2014/Images/Linear%20operation/img13.png)
![img14](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2014/Images/Linear%20operation/img14.png)

## Lab: ID vs. VDS for different VGS  
#### Running day1_nfet_idvds_L2_W5.spice file
```
*** Model Description ***
.param temp=27

*** Including sky130 library files ***
.lib "sky130_fd_pr/models/sky130.lib.spice" tt

*** Netlist Description ***
XM1 vdd n1 0 0 sky130_fd_pr__nfet_01v8 w=5 l=2
R1 n1 in 55
Vdd vdd 0 1.8
Vin in 0 1.8

*** Simulation Commands ***
.op
.dc Vdd 0 1.8 0.1 Vin 0 1.8 0.2

.control
run
display
setplot dc1
.endc

.end
```
* Plotting vdd#branch shows (ID) vs VDS characteristics of an NMOS device.
![img15](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2014/Images/Linear%20operation/img15.png)
