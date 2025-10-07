# SPICE Simulations CMOS Circuits
* To explore SPICE simulations of NMOS transistors and CMOS inverters across different technology nodes. And comparing the behaviors of long-channel and short-channel devices, as well as analyzing their current–voltage characteristics.

## NMOS Characteristics
* Device Parameters
  * Long Channel: W = 1.8 μm, L = 1.2 μm (W/L = 1.5)
  * Short Channel : W = 0.375 μm, L = 0.25 μm (W/L = 1.5)  

  ![img1](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2015/Images/Observations/img1.png)

### Operation Regions

* Cut of region
  * Vgs =< Vt
  * Area where the device is being cut off.

* Resistive region/ Linear region
    * Id ∝ Vds
    * Valid for Vds < (Vgs – Vt)
    * Drain current is a linear function of Vds

* Saturation region
    * Id ∝ function (1 + λ . Vds)
    * Valid for Vds ≥ (Vgs – Vt)


 ## Observation 1: Long channel vs short channel device
![img2](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2015/Images/Observations/img2.png)  
![img3](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2015/Images/Observations/img3.png)  

* Long Channel NMOS shows the Drain current (Id) quadratic dependence on Vgs. Whereas Short Channel NMOS Id is quadratic at low Vgs, but becomes linear at high Vgs due to velocity saturation.
* Velocity saturation at lower and higher electric fields
 * Velocity saturation means that when in the MOSFETs, the carriers’ speed quickly reaches a maximum value (saturation velocity) when the electric field is high. After this point, even if you increase the gate voltage Vgs further, the carriers cannot go faster because their speed has already reached its limit.
 
![img4](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2015/Images/Observations/img4.png)  
![img5](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2015/Images/Observations/img5.png)

* The following slides show how the unified model works in the different Regions of Operation of the MOS transistor: 

![img6](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2015/Images/Observations/img6.png)  
![img7](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2015/Images/Observations/img7.png)  
![img8](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2015/Images/Observations/img8.png)  
![img9](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2015/Images/Observations/img9.png)  

## Observation 2: Peak current Comparison
* Long Channel (W = 1.8 μm, L = 1.2 μm): Id_peak = 410 μA
* Short Channel (W = 0.375 μm, L = 0.25 μm): Id_peak = 210 μA

![img10](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2015/Images/Observations/img10.png)  

## Labs Simulation Sky130 Id-Vgs 
**Id–Vds Characteristics**
SPICE File: day2_nfet_idvgs_L015_W039.spice
```
Model Description
.param temp=27


*Including sky130 library files
.lib "sky130_fd_pr/models/sky130.lib.spice" tt


*Netlist Description

XM1 Vdd n1 0 0 sky130_fd_pr__nfet_01v8 w=0.39 l=0.15

R1 n1 in 55

Vdd vdd 0 1.8V
Vin in 0 1.8V

*simulation commands

.op
.dc Vin 0 1.8 0.1

.control

run
display
setplot dc1
.endc

.end

```
Below is the Id-Vgs curve for Vds = 1.8V
![img11](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2015/Images/Observations/img11.png)

## CMOS Voltage Transfer Characteristics

### MOSFET as a switch 

* ON State
  * Condition : |Vgs| > |Vth|
  *  MOSFET acts as a closed switch with a finite resistance.

* OFF State
  * Condition : |Vgs| < |Vth|
  * MOSFET acts as an open switch with infinite resistance.  
  
![img1]()

### CMOS Representation 

**Switch level extraction**  
* Circuit diagram of CMOS Inverter when Vin is high
   * Vin = Vdd → NMOS ON, PMOS OFF → Vout = 0
  
![img2]()

* Circuit diagram of CMOS Inverter when Vin is low
   * Vin = 0 → PMOS ON, NMOS OFF → Vout = Vdd
 
![img3]()

**Transistor-level Extraction** 
* The CMOS inverter at the transistor level 
  - NMOS
    * NMOS source connected to VSS
    * Vout taken at the common drain
    * Vin applied to both gates

  - PMOS
    * PMOS source connected to VDD
    * Vout taken at the common drain
    * Vin applied to both gates

![img4]()

### PMOS/NMOS drain current v/s drain voltage
* We are comparing the drain current (Id) versus drain voltage (Vds) characteristics of NMOS and PMOS transistors to gain a basic understanding of their behavior and how these characteristics affect the operation of an inverter.

![img5]()  

### Analysis of CMOS inverter
* Steps to derive Voltage-Transfer Characteristics (VTC) of a cell, which are only a function of Vin and Vout. 

**Step 1** : Convert PMOS gate-source-voltage to Vin
- Converting the PMOS gate-source voltage (VgsP) into an equivalent Vin. Replacing the internal node voltages with Vin and Vdd.
- Vgsp = Vin - Vdd

![img6]()    

**Step 2 and 3** : Convert PMOS and NMOS drain-source-voltage to Vout  
- Express PMOS and NMOS drain-source (Vdsp) voltages in terms of Vout.
    * For the CMOS inverter, when we see Vout =0, it means the load capacitance is discharged and we need to charge it. i.e. the load capacitance has been discharged by the NMOS. If you want the output to go high again, you must charge that capacitance through the PMOS.
- Step 2: converting PMOS to Vout

![img7]()

 - Step 3: Load curve for NMOS transistor 
 
![img8]()  
  
**Step 4**:  Merge PMOS and NMOS load curves and plot VTC  

![img9]()  

* Sweeping Vin and plotting Vout to obtain the inverter VTC curve, which shows the switching behavior of the inverter from logic HIGH to logic LOW.  

![img10]()
