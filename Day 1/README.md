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
	module good_mux (input i0 , input i1 , input sel , output reg y);
	always @ (*)
	begin
		if(sel)
			y <= i1;
		else 
			y <= i0;
	end
	endmodule

