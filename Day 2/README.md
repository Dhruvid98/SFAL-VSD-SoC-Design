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
![show](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%202/Images/sub_modules/Screenshot%202025-05-17%20002035.png)  
![net](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%202/Images/sub_modules/Screenshot%202025-05-17%20001938.png)  

## Various Flop Coding Styles and Optimization.
### Why is a flip-flop needed?  
In digital design, combinational circuits are prone to glitches, i.e. unintended transitions in output values. These occur when multiple input signals arrive at slightly different times due to unequal propagation delays, causing the logic to temporarily settle to incorrect states. Flip-flops, which are storage components, are utilized in between stages of combinational logic to stop such unstable outputs from influencing downstream logic.  
* Issues
    - If these glitches are usually harmless in isolation. However, if another part of the circuit captures these unstable outputs, it can lead to functional failures or incorrect data being latched.
![flops basic](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%202/Images/Flop%20basic/1.png)
* Solution
    - Flip-flop captures and holds the stable input value from the preceding combinational logic at a specific clock edge (rising or falling). It then passes this stable value to the next combinational stage. Because flip-flops only update their output on clock edges, they effectively filter out any glitches or transients that occur outside the clock transition window. This clocked behavior ensures that only stable and valid data is propagated through the design, resulting in a more reliable and predictable output.
 
### Different types of flops.   
To initialize flops, we need to set and reset, which can be synchronous or asynchronous.  
- Asynchronous: Change is immediately activated
   * Reset: It forces output to 0.  
      - R= 0 -> denpends on d , R= 1 -> q = 0  
   * Set: It forces output at 1.
      - S= 0 -> depends on d, S= 1, -> q = 1
 - Synchronous: Change is observed from the upcoming rising edge of the clock
![diff](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%202/Images/Flop%20basic/2.png)

The below screenshot shows DFF with asynchronous reset simulation in Iverilog and waveform display in GTKwave. Irrespective of the clock and d, as soon as async_reset=1, q=0.
![async_reset](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%202/Images/DFF_simulation/async_reset.png)  
The below screenshot shows DFF with asynchronous reset simulation in Iverilog and waveform display in GTKwave. Irrespective of the clock and d, as soon as async_set=1, q=1.  
![async_set](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%202/Images/DFF_simulation/async_set.png)  
The below screenshot shows DFF with asynchronous reset simulation in Iverilog and waveform display in GTKwave. With the rising edge of the clock and d, sync_reset=1, q=0.  
![sync_reset](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%202/Images/DFF_simulation/sync_reset.png)  

### Synthesizing flops
Commands:-
```
read_liberty -lib ..my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_asyncres.v
synth -top dff_asyncres
dfflibmap -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib <!-- used to map only dff. Sometimes flip-flop lib can be different or the same. -->
abc -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```
Below is the image of synthesizing DFF with an asynchronous reset  
![async_reset_syn](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%202/Images/DFF%20Synthesis/async_reset.png)  
Below is the image of synthesizing DFF with asynchronous set  
![async_set_syn](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%202/Images/DFF%20Synthesis/async_set.png)  
Image of synthesizing DFF with synchronous reset   
![sync_resey_syn](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%202/Images/DFF%20Synthesis/sync.png)  

