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
![img1]()
Simulation Commands: .dc, .tran, .op, and technology model include statements.
