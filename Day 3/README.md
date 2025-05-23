# Combinational and Sequential Optimization 

## Introduction to Optimization 
### Combinational Optimization
* Why does the combination logic need optimization?
  - Mainly to squeeze the logic into the most optimized design.
  - Optimized designs are efficient in terms of *Area and Power* saving.

* Techniques for optimization:-
    - Constant Propagation
        * Directly simplifying logic paths when input constants are known
![const](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%203/Images/Introduction/Constant.png)
    - Boolean logic optimization
        * K- Map ((Karnaugh Map))
        * Quine McKluskey Algo.
![bool](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%203/Images/Introduction/boolean.png)

### Sequential logic Optimization

* Techniques used:
  - Basic
  - Advanced
      * State Optimization: Reduces the number of states in Finite State Machines (FSMs), thereby minimizing area usage and transition overhead.
      * Retiming: Rearranging registers across combinational logic without altering the circuit's functioning to balance the logic delay and improve timing performance.
      * Sequential Logic Cloning (Floor Plan-Aware Synthesis): This technique improves timing and physical implementation by replicating/ cloning sequential elements (registers) across the chip layout.

Example of sequential constant propagation shown below in a D flip flop with asynchronous reset, where the D input is grounded. The output of Q is always constant i.e. 0.. Whereas the same technique cannot be applied to D flip flop with the asynchronous set because while Q=1 when Set=1, but Q=0 at Set=0 at the next CLK pulse. Q is dependent not only on Set but also on the clock edge. 
![basic](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%203/Images/Introduction/sequen_basic.png)  

## Combinational logic optimization

```
yosys
read_liberty -lib ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog opt_check.v 
synth -top opt_check
opt_clean -purge # to optimize / to remove redundant logic 
abc -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```
### Optimization for opt_check.v
```
module opt_check (input a , input b , output y);
        assign y = a?b:0;
endmodule
```

For opt_check.v, the assigned y = a?b:0. i.e. if a=1, y = b else y =0. The above logic is reduced to y = ab.  
![opt_check](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%203/Images/Optimization/check_1.png)
After synthesis, we can find only AND gate in opt_check.v
![show_check](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%203/Images/Optimization/opt_check_2.png)  

### Optimization for opt_check2.v
```
module opt_check2 (input a , input b , output y);
        assign y = a?1:b;
endmodule
```
For opt_check2.v, the assigned y = a?1:b. i.e. if a=1, y = 1 else y =b. The above logic is reduced to y = a+b. 
![check2_logic](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%203/Images/Optimization/check2_1.png)  
After synthesis, we can find only OR gate.
![check2_show](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%203/Images/Optimization/check2_2.png)  

### Optimization for opt_check3.v
```
module opt_check3 (input a , input b, input c , output y);
	assign y = a?(c?b:0):0;
endmodule
```
For opt_check3.v, the assigned y = a?(c?b:0):0. i.e. if a=1, y = c?b:0 else y =0. The above logic is reduced to y = ABC.  
![logic3](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%203/Images/Optimization/check3_1.png)
After synthesis, we can find one AND gate with 3 inputs a,b, and c.
![synth3](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%203/Images/Optimization/check3_2.png)  

### Optimization for opt_check4.v
```
module opt_check4 (input a , input b, input c , output y);
	assign y = a?(b?(a & c): c):(!c);
endmodule
```
For opt_check4.v, the assigned y = a?(b?(a & c): c):(!c). The above logic is reduced to y = a ⊙ c.
![logic4](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%203/Images/Optimization/check4_1.jfif)
After synthesis, we can find one XNOR gate with a and c inputs.
![show4](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%203/Images/Optimization/check4_2.png)  

### Optimization for multiple_module_opt.v
```
module sub_module1(input a , input b , output y);
 assign y = a & b;
endmodule

module sub_module2(input a , input b , output y);
 assign y = a^b;
endmodule

module multiple_module_opt(input a , input b , input c , input d , output y);
wire n1,n2,n3;

sub_module1 U1 (.a(a) , .b(1'b1) , .y(n1));
sub_module2 U2 (.a(n1), .b(1'b0) , .y(n2));
sub_module2 U3 (.a(b), .b(d) , .y(n3));

assign y = c | (b & n1); 
endmodule
```
The logic implementation after synthesis for multiple_module_opt.v. (Need to flatten the design before opt_clean -purge step)
![showmul](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%203/Images/Optimization/mult_1.png)

## Sequential logic optimization

### Optimization for dff_const1.v
dff_const1.v
```
module dff_const1(input clk, input reset, output reg q);
always @(posedge clk, posedge reset)
begin
	if(reset)
		q <= 1'b0;
	else
		q <= 1'b1;
end

endmodule
```
![logic_here](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%203/Images/Sequence%20Opt/L1_logic.png)

For ddf_const1, as long as the reset is held high (reset = 1), the output q will remain low (q = 0). When the reset = 0, the value of q will not immediately transition to 1. Instead, it will wait for the next rising clock edge to update its value. So that's the reason **optimization can't be applied here**.  

**Simluation**

![waveform](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%203/Images/Sequence%20Opt/L1_gtkwave.png)

**Synthesis**

```
read_liberty -lib ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_const1.v
synth -top dff_const1
dfflibmap -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```
![show](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%203/Images/Sequence%20Opt/L1_show_stat.png)  

### Optimization for dff_const2.v
dff_const2.v
```
module dff_const1(input clk, input reset, output reg q);
always @(posedge clk, posedge reset)
begin
	if(reset)
		q <= 1'b1;
	else
		q <= 1'b1;
end

endmodule
```
![logic](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%203/Images/Sequence%20Opt/L2_logic.png)  

**Simluation**

![gtkwave](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%203/Images/Sequence%20Opt/L2_gtkwave.png)  

**Synthesis**

```
read_liberty -lib ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_const2.v
synth -top dff_const2
dfflibmap -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```
![show](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%203/Images/Sequence%20Opt/L2_show.png)  

### Optimization for dff_const3.v  
dff_const3.v
```
module dff_const3(input clk, input reset, output reg q);
reg q1;

always @(posedge clk, posedge reset)
begin
	if(reset)
	begin
		q <= 1'b1;
		q1 <= 1'b0;
	end
	else
	begin
		q1 <= 1'b1;
		q <= q1;
	end
end

endmodule
```
In this scenario, we have two D flip-flops, Q1 and Q. When `reset = 1`, Q1 is set to 0. When `reset = 0`, Q1 will wait for the next rising clock edge to transition to 1, with some propagation delay. The output of Q1 is then fed as the input to Q. When `reset = 1`, Q will be set to 1, acting as a set operation rather than a reset. When `reset = 0`, Q will remain low for one clock cycle due to the propagation delay. At the next clock edge, Q will sample the value of Q1, which will be 1. **Due to this optimization can't be applied.**  
![logic](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%203/Images/Sequence%20Opt/L3_logic.png)  

**Simluation** 

![simulation](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%203/Images/Sequence%20Opt/L3_gtkwave.png)

**Synthesis**

```
read_liberty -lib ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_const3.v
synth -top dff_const3
dfflibmap -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```
![show](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%203/Images/Sequence%20Opt/L3_show.png)

### Optimization for dff_const4.v  
dff_const4.v
```
module dff_const4(input clk, input reset, output reg q);
reg q1;

always @(posedge clk, posedge reset)
begin
	if(reset)
	begin
		q <= 1'b1;
		q1 <= 1'b1;
	end
	else
	begin
		q1 <= 1'b1;
		q <= q1;
	end
end

endmodule
```

**Simulation**

![gtkwave](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%203/Images/Sequence%20Opt/L4_gtkwave.png)

**Synthesis**

```
read_liberty -lib ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_const4.v
synth -top dff_const4
dfflibmap -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```
![show](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%203/Images/Sequence%20Opt/L4_show.png)  

### Optimization for dff_const5.v  
dff_const5.v
```
module dff_const5(input clk, input reset, output reg q);
reg q1;

always @(posedge clk, posedge reset)
begin
	if(reset)
	begin
		q <= 1'b0;
		q1 <= 1'b0;
	end
	else
	begin
		q1 <= 1'b1;
		q <= q1;
	end
end

endmodule
```
In this scenario, we have two D flip-flops, Q1 and Q. When `reset = 1`, Q1 is set to 0. When `reset = 0`, Q1 will wait for the next rising clock edge to transition to 1, with some propagation delay. The output of Q1 is then fed as the input to Q. When `reset = 1`, Q will be set to 0. When `reset = 0`, Q will remain low for one clock cycle due to the propagation delay. At the next clock edge, Q will sample the value of Q1, which will be 1. **Due to this optimization can't be applied.**   

**Simluation** 

![simulation](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%203/Images/Sequence%20Opt/L5_gtkwave.png)

**Synthesis**

```
read_liberty -lib ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_const5.v
synth -top dff_const5
dfflibmap -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```
![show](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%203/Images/Sequence%20Opt/L5_show.png)

## Sequential Optimisations for Unused Outputs
### Optimization for 3-bit up counter with q[0] used (counter_opt.v)
```
module counter_opt (input clk , input reset , output q);
reg [2:0] count;
assign q = count[0];

always @(posedge clk ,posedge reset)
begin
	if(reset)
		count <= 3'b000;
	else
		count <= count + 1;
end

endmodule
```
The logic of the counter uses only q[0]. So the **optimization can be applied here**, which is explained in the image below. 
![logic1](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%203/Images/Unused%20output/L1_logic.png)  

**Synthesis**
```
read_liberty -lib ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog counter_opt.v
synth -top counter_opt
dfflibmap -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```
Only one flop is seen after the synthesis process. 
![sythn](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%203/Images/Unused%20output/L1_show.png)

### Optimization for 3-bit up counter (counter_opt2.v)
Example of a counter where all the bits are used. 
```
module counter_opt (input clk , input reset , output q);
reg [2:0] count;
assign q = (count[2:0] == 3'b100);

always @(posedge clk ,posedge reset)
begin
	if(reset)
		count <= 3'b000;
	else
		count <= count + 1;
end

endmodule
```
**Synthesis**
```
read_liberty -lib ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog counter_opt2.v
synth -top counter_opt
dfflibmap -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```
![stats](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%203/Images/Unused%20output/L2_stat.png)
![show](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%203/Images/Unused%20output/L2_show.png)
![proof](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%203/Images/Unused%20output/L2_proff.png)
