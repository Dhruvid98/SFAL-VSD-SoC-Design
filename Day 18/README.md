# Day 18: CMOS inverter robustness and Power supply variation

* The section below explores how power supply variation and device variation affect the static robustness of CMOS inverters. Here, the effect of power supply scaling on the static behavior of the CMOS Inverter is examined.

## Power supply variation

* Scaling the supply voltage (Vdd) directly impacts the inverter’s static behavior by shifting the switching threshold Vm, reducing noise margin, and increasing overall robustness. 

![img1](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2018/Images/img1.png)

![img2](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2018/Images/img2.png)

**Power Performance**
* Lower supply saves static & dynamic power but reduces robustness.
* Higher supply: improves noise margins but increases power dissipation

### Lab: Supply Scaling - sky130 Inverter 

* File: day5_inv_supplyvariation_Wp1_Wn036.spice

![img3](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2018/Images/img3.png)

**Key Observation**
* With a decrease in supply voltage, the gain values keep increasing. But once the supply voltage reaches voltage 1, the gain value starts to decrease. As it is not able to recharge fully. As a result, the gain of the inverter in the transition region increases with a reduction of the supply voltage.

## Static Behavior Evaluation — CMOS Inverter Robustness and Device Variation

* The device variation is a critical factor that influences the robustness of a CMOS inverter.
* While gates are designed based on nominal operating conditions and typical device parameters, real-world conditions often differ significantly. Operating temperatures can vary across a wide range, and post-fabrication device parameters often deviate from the nominal values used during design. These variations are primarily due to fabrication non-idealities such as etching inconsistencies and oxide thickness variations which can affect the effective dimensions and performance of transistors.

## Source of Etching variation 

### 1. Etching Process Variations
* `Poly-silicon layer`: defines channel length `L`. That helps to link with technology node. Eg 28nm, 65nm etc.
* `P-diffusion region`: sets PMOS gate width
* `N-diffusion region`: sets NMOS gate width
* Layout layers in an inverter:
    * Poly (Gate)
    * P-Diffusion
    * N-Diffusion
    * VDD and VSS rails

![img4](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2018/Images/img4.png)  

**Impact**
* The area of W and L will differ.i.e. Actual W and L differ from intended values
* Drain current value `(Id  ∝  W/L)` changes.
* Drain current value changes as it is directly dependent on oxide thickness variation. 

**Inverter Chain Example**

* The chain of inviter is usually used to understand the Propagation delay and Cumulative variation effects.
  
![img6](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2018/Images/img6.png)
![img5](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2018/Images/img5.png)

### 2. Oxide Thickness Variation

* The second key source of variation comes from oxide thickness (tox) of the MOS gate.
  
![img7](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2018/Images/img7.png)
![img8](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2018/Images/img8.png)

## Lab: Spice Simulation 
* File: day5_inv_devicevariation_wp7_wn042.spice

![img9](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2018/Images/img9.png)
