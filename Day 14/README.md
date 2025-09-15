# SPICE overview and CMOS fundamentals

## What is SPICE
SPICE (Simulation Program with Integrated Circuit Emphasis) is an industry-standard Circuit Simulator. It takes a circuit description in the form of a netlist: transistors, resistors, capacitors, sources, etc., and mathematically solves how voltage and current behave over time in that circuit.

## Why is SPICE needed? 
SPICE serves as the foundation in digital VLSI design, providing accurate modeling and characterization of standard cells and macros, which is essential for timing, power, variation, noise, and signal integrity analyses.

## CMOS Fundamentals

### Inverter 
An inverter uses PMOS and NMOS transistors. The PMOS connects to VDD and the NMOS to GND. The gates are tied to the input, and the drain is tied to the output. 
![img1]()

### Analysis of Inverter using SPICE
Simulating a CMOS inverter in SPICE verifies its functionality, measures propagation delay, and calculates dynamic and static power. Designers obtain voltage transfer characteristics as well as Id–Vout plots for NMOS and PMOS devices under different input conditions.
![img2]()

### Delay 
The cell delays depend on input slew and output load. Delay information is stored in a 2D lookup table, where the delay is mapped as a function of input slew and output load.
![img3]()

### NMOS Transistor
![img5]()
![img4]()

### Threshold Voltage
* The NMOS is currently turned off. So there is no conducting path between the source and drain 
![img6]()
![img7]()
