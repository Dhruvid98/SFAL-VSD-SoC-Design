# CMOS Switching Threshold and Dynamic Simulations
- This section demonstrates CMOS inverter static and dynamic analysis using SPICE simulations. Focusing on Voltage Transfer Characteristics (VTC), transient response, and switching threshold voltage (Vm).

## CMOS Inverter SPICE Deck 

**Defining the SPICE deck of CMOS:**  
- Component Connectivity:
    * PMOS (M1), NMOS (M2), supply (Vdd), ground (Vss), input (Vin) and output (Vout).
- Component Values:
   * Transistor dimensions (W/L), supply voltage and load capacitance (Cload). 
- Identifying and Node Naming :
    * vdd, vss, in, out
- Simulation Commands:
    * .dc, .op, and including the technology model file   
      
![img1](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2016/Images/SPICE%20Deck/img1.png)
![img2](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2016/Images/SPICE%20Deck/img2.png)  

## Labs Sky130 SPICE simulation for CMOS
* VTC characteristics of the CMOS inverter
* SPICE file : day3_inv_vtc_Wp084_Wn036.spice

```
*Model Description
.param temp=27


*Including sky130 library files
.lib "sky130_fd_pr/models/sky130.lib.spice" tt


*Netlist Description


XM1 out in vdd vdd sky130_fd_pr__pfet_01v8 w=0.84 l=0.15
XM2 out in 0 0 sky130_fd_pr__nfet_01v8 w=0.36 l=0.15


Cload out 0 50fF

Vdd vdd 0 1.8V
Vin in 0 1.8V

*simulation commands

.op

.dc Vin 0 1.8 0.01

.control
run
setplot dc1
display
.endc

.end
```

![img3](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2016/Images/SPICE%20Deck/img3.png)  

* Rise delay and Fall delay in transient analysis. 
   - Below output waveform of the transient analysis of a CMOS inverter, illustrating the rise time delay and the fall time delay of the inverter. 
* SPICE file : day3_inv_tran_Wp084_Wn036.spice

```
*Model Description
.param temp=27


*Including sky130 library files
.lib "sky130_fd_pr/models/sky130.lib.spice" tt


*Netlist Description


XM1 out in vdd vdd sky130_fd_pr__pfet_01v8 w=0.84 l=0.15
XM2 out in 0 0 sky130_fd_pr__nfet_01v8 w=0.36 l=0.15


Cload out 0 50fF

Vdd vdd 0 1.8V
Vin in 0 PULSE(0V 1.8V 0 0.1ns 0.1ns 2ns 4ns)

*simulation commands

.tran 1n 10n

.control
run
.endc

.end
```

![img4](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2016/Images/SPICE%20Deck/img4.png)  

## Static Behavior Evaluation - CMOS Inverter Robustness and Switching Threshold

The Key characteristics to define the robustness of CMOS inverters:   
* Switching Threshold Voltage (Vm)
* Noise Margins
* Power Supply Variation Tolerance

### Switching Threshold Voltage 

* The Switching Threshold Voltage (Vm) is the point at which the input voltage and the output voltage are equal i.e. Vin = Vout
*  At Vm point, PMOS and NMOS are in the saturation region. That means both are turned on. Because of that, there is a chance of a short.
*  This point corresponds to maximum voltage gain in the inverter transfer curve.

![img1]()  

*  The different regions of operations for the curve correspond to the transistor operating regions: PMOS Linear / NMOS OFF, PMOS Linear / NMOS Saturation,  PMOS Saturation / NMOS Saturation (where Vm is located), PMOS Saturation / NMOS Linear,  PMOS OFF / NMOS Linear.  

![img2]()  

### Analytical expression of Vm as a function of (W/L)p and (W/L)n

![img3]()  

### Static and dynamic simulation of CMOS inverter

**Effect of varying Wp/Wn Ratio on Inverter with increased PMOS width**    
* Key Parameters that get affected
     * Rise Delay
     * Fall Delay
     * Switching Threshold Voltage
     
* Rise Delay means the time it takes for an output capacitance to charge completely.
* 

 
