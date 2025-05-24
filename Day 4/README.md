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
* Non-standard verilog coding


