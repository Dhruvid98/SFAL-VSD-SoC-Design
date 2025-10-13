# Day 18: CMOS inverter robustness and Power supply variation

* The section below explores how power supply variation and device variation affect the static robustness of CMOS inverters. Here, the effect of power supply scaling on the static behavior of the CMOS Inverter is examined.

## Power supply variation

* Scaling the supply voltage (Vdd) directly impacts the inverter’s static behavior by shifting the switching threshold Vm, reducing noise margin, and increasing overall robustness. 

![img1]()

![img2]()

**Power Performance**
* Lower supply saves static & dynamic power but reduces robustness.
* Higher supply: improves noise margins but increases power dissipation

## Lab: Supply Scaling - sky130 Inverter 

* File: day5_inv_supplyvariation_Wp1_Wn036.spice

![img3]()

**Key Observation**
* With a decrease in supply voltage, the gain values keep increasing. But once the supply voltage reaches voltage 1, the gain value starts to decrease. As it is not able to recharge fully. As a result, the gain of the inverter in the transition region increases with a reduction of the supply voltage.
