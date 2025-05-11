# Day 1: Introduction to RTL design and Synthensis. 

## Introduction to simulator Iverilog and GTKWave. 
* **Iverilog** is an open-source simulator tool used to verify whether an RTL design adheres to the specified requirements by simulating the design's functionality.
* **GTKWave** is used to view the waveform.
* Iverilog based simulation flow
![image](https://github.com/user-attachments/assets/91202d92-99b0-4e1f-8d3f-ea9025417d07)

Git folder structre sky130 RTL Design & Synthesis
* my_lib/lib - standard cell library for sky130
* my_lib/verilog_models - contains standard cell verilog models
* verilog_files - contains verilog source and testbench files for the lab.

Example : Design of good_mux.v (source code)
```
module good_mux (input i0 , input i1 , input sel , output reg y);
always @ (*)
begin
	if(sel)
		y <= i1;
	else 
		y <= i0;
end
endmodule
```
Testbench tb_good_mux.v 
```
`timescale 1ns / 1ps
module tb_good_mux;
	// Inputs
	reg i0,i1,sel;
	// Outputs
	wire y;

        // Instantiate the Unit Under Test (UUT)
	good_mux uut (
		.sel(sel),
		.i0(i0),
		.i1(i1),
		.y(y)
	);

	initial begin
	$dumpfile("tb_good_mux.vcd");
	$dumpvars(0,tb_good_mux);
	// Initialize Inputs
	sel = 0;
	i0 = 0;
	i1 = 0;
	#300 $finish;
	end

always #75 sel = ~sel; // chaning the sel for 0 and 1 
always #10 i0 = ~i0;
always #55 i1 = ~i1;
endmodule
```
