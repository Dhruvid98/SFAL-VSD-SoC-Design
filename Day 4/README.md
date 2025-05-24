# GLS, Blocking vs Non-blocking and Synthesis-Simulation Mismatch

## Gate Level Simulation

**What is Gate level Simulation(GLS)?**
  * Running the test bench with Netlist as Design Under Test.
  * Same test bench aligns with the design as Netlist is logically the same as RTL code.

**Why is GLS necessary?**
  * To verify the logical correctness of the design after synthesis.
  * Ensure the timing of the design is met, which is done with delay annotation (timing aware)

*GLS flow using iVerilog*
![flow](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%204/Images/GLS%20flow/GLS_flow.png)  

## Synthesis Simulation Mismatches

It happens because of the following reasons:-
* Missing sensitivity list
* Blocking vs non-blocking assignments
* Non-standard Verilog coding

### Missing Sensitivity list. 

Screenshot below of RTL code for a 2:1 multiplexer (MUX2:1) uses the sensitivity list always @(Sel), the output Y will only respond to changes in the `sel`. This means any changes to the data inputs i0 and i1 will be ignored unless. As a result, the design behaves potentially like a latch or a double-edge triggered flip-flop. However, when we use always @(*) the code on the right side, the sensitivity list automatically includes all signal changes. This ensures that any change in any of the inputs will trigger the block.  
![logic](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%204/Images/Missing%20sensitivity%20list/logic.png)
