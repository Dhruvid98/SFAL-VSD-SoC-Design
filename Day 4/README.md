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

### 1. Missing Sensitivity list. 

Screenshot below of RTL code for a 2:1 multiplexer (MUX2:1) uses the sensitivity list always @(Sel), the output Y will only respond to changes in the `sel`. This means any changes to the data inputs i0 and i1 will be ignored unless. As a result, the design behaves potentially like a latch or a double-edge triggered flip-flop. However, when we use always @(*) the code on the right side, the sensitivity list automatically includes all signal changes. This ensures that any change in any of the inputs will trigger the block.  

![logic](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%204/Images/Missing%20sensitivity%20list/logic.png)  

### 2. Blocking and Non-blocking statements in Verilog 

Blocking and Non-blocking statements will come into picture when we are using **always** block. 

* Blocking statements 
   - Represented by **=**
   - Executes the statements in the order it is written inside always block
   - The first statement is evaluated before the second statement

 * Non blocking statements
   - Represented by **<=**
   - Executes all the RHS when always block is entered and assigns to LHS
   - Parallel execution (order doesn't matter)

![blocking issue](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%204/Images/Blocking/Logic.png)  
The left side of the screenshot below gives us the correct execution. While the right side can lead to serious issues as d is assigned to q directly. So, choosing non-blocking statements is better.

## Labs on GLS and Synthesis-Simulation Mismatch

### Ternary operator mux :- ternary_operator_mux.v

```
module ternary_operator_mux (input i0 , input i1 , input sel , output y);
	assign y = sel?i1:i0;
	endmodule
```

Commands to run HDL simulation 

```
iverilog ternary_operator_mux.v tb_ternary_operator_mux.v
./a.out
gtkwave tb_ternary_operator_mux.vcd
```
The waveform illustrates the simulation results of the RTL code for ternary_operator_mux.v. 
![rtl_simulation]()  

Command to run synthesis 
```
read_liberty -lib ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog ternary_operator_mux.v
synth -top ternary_operator_mux
abc -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
write_verilog ternary_operator_mux_net.v
```

Synthesis for ternary_operator_mux.v.

![synth_waveform]()

Commands to run GLS for ternary_operator_mux.v 
```
iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v ternary_operator_mux_net.v tb_ternary_operator_mux.v
./a.out
gtkwave tb_ternary_operator_mux.vcd
```

The GLS output is shown in the screenshot below. 

![gls_waveform]()
