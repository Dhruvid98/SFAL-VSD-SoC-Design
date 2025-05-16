# Day 2: Timing libs, hierarchical vs flat synthesis and efficient flop coding styles

## Introduction to .lib file
* .lib file is a collection of standard cells. 
* Libraries are characterized based on PVT (Process, voltage, temperature)
- Process: Variation is due to fabrication
  * Process corners:- TT (typical), SS (Slow), FF (Fast)
- Voltage: Variation is due to a voltage
- Temperature: Variation due to temperature

Example of PVT by using the below file name.  
*tt* stands for typical in the .lib name  
*025C* stands for temperature of 25 C in the .lib name  
*1v80* stands for voltage of 1.8V in the .lib name  
![](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%202/Images/Lab1/Screenshot%202025-05-15%20215430.png)

- Cell keyword is used to define the cell.
- Information regarding the features of each cell that is present
   * Leakage power based on all combination inputs
   * Area
   * Power ports
   * Input capacitance
   * Power associated with the pin
   * Transition and Delay

 ## Hierarchical vs Flat Synthesis


