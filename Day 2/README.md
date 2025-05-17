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
![lib](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%202/Images/Lab1/Screenshot%202025-05-15%20215430.png)

- Cell keyword is used to define the cell.
- Information regarding the features of each cell that is present
   * Leakage power based on all combination inputs
   * Area
   * Power ports
   * Input capacitance
   * Power associated with the pin
   * Transition and Delay

## Hierarchical vs Flat Synthesis
### Hierarchical Synthesis
The synthesis of multiple_modules.v is performed hierarchically, where sub-module 1 (AND gate) and sub-module 2 (OR gate) are initialized. The synthesis stats show the number of cells present in each submodule.  
![stat](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%202/Images/Hierarchical%20Synthesis/Screenshot%202025-05-16%20225748.png)  

Here, the hierarchy is preserved in submodule 1 and submodule 2. Instead of an AND and OR gate, we have submodules (u1 and u2) when the **show multiple_modules** command is executed.   

![show](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%202/Images/Hierarchical%20Synthesis/Screenshot%202025-05-16%20231701.png)  

After generating the synthesis netlist for multiple_modules_hier.v, sub-module 2 does not use an OR gate as input. Instead, it is implemented with 2 INV gates and 1 NAND gate. This change is made because the OR gate has stacked PMOS transistors, which is undesirable in CMOS design due to the increased resistance, reduced mobility, and stronger body effect.  
![submodule](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%202/Images/Hierarchical%20Synthesis/Screenshot%202025-05-16%20231932.png)  

### Flat Synthesis

The design can be flattened using the command **flatten**.  
The images below show the flattened logical diagram and the synthesized netlist. In the flattened design, AND and OR gates can be observed.
![logical](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%202/Images/Flatten/Screenshot%202025-05-16%20234138.png)  
![netlist](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%202/Images/Flatten/Screenshot%202025-05-16%20234346.png)  

### Submodule synthesis 

Submodule synthesis refers to the process of synthesizing smaller, individual functional blocks or submodules of a larger design separately before integrating them into the final top-level design.   
Why is it needed?
- Reuseability: Synthesizing submodules allows for the reuse of pre-synthesized modules in different parts of the design.
- Optimized Performance: By synthesizing smaller submodules, the synthesis tool can apply specific optimizations to each submodule, potentially improving overall performance and turnaround time
- Resource Management: When working with complex designs, the synthesis tool might struggle to handle the entire design in one go. By breaking the design into submodules, each can be synthesized independently, making the process more manageable

Synthesize the sub-module only
read_libertiy -lib ../my_libs/libs/sky130_fd_sc_hd__tt_025C_1v80.lib  
read_verilog multiple_modules.v  
synth -top sub_module2  
show  

The images below show the synthesis report of submodule 2 (OR gate) and the logical diagram. 
![show](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%202/Images/sub_modules/Screenshot%202025-05-16%20234346.png)  
![net](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%202/Images/sub_modules/Screenshot%202025-05-16%20234138.png)  

 
