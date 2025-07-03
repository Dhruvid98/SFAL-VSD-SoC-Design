# Day 9: Report timing
![img1](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%209/Images/report_timing/img1.png)
![img2](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%209/Images/report_timing/img2.png)
![img3](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%209/Images/report_timing/img3.png)
![img4](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%209/Images/report_timing/img4.png)
![img5](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%209/Images/report_timing/img5.png)

* `report_timing -max_paths2`: This command will display the worst path for each endpoint. Per endpoint, it will pick only one path. It will display the two worst slacks.
* `report_timing -max_paths2 -nworst2`: The nworst command will display per end point 2 worst paths. 

![img6](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%209/Images/report_timing/img6.png)

## Lab report timing
Step 1. `read_verilog lab8_circuit_modified.v`'Verilog code lab8_circuit_modified.v 
```
module lab8_circuit (input rst, input clk , input IN_A , input IN_B , output OUT_Y , output out_clk , output reg out_div_clk);
reg REGA , REGB , REGC ; 

always @ (posedge clk , posedge rst)
begin
	if(rst)
	begin
		REGA <= 1'b0;
		REGB <= 1'b0;
		REGC <= 1'b0;
		out_div_clk <= 1'b0;
	end
	else
	begin
		REGA <= IN_A | IN_B;
		REGB <= IN_A ^ IN_B;
		REGC <= !(REGA & REGB);
		out_div_clk <= ~out_div_clk; 
	end
end

assign OUT_Y = ~REGC;

assign out_clk = clk;

endmodule
```

Step 2. Linking the file and sourcing the constraints file. `source lab8_cons_modified.tcl`  
Step 3. `compile_ultra` to optimize the design based on constraints   
Step 4. `report_timing -sig 4 -nosplit -trans -cap -nets -inp`.   
* Below are the clues to see if it is set up or hold time. 
![img1](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%209/Images/Lab/img1.png)
![img2](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%209/Images/Lab/img2.png)

Based on the above clues, it is a max path. 

Step 5. Worst delay for IN_A
```
report_timing -sig 4 -nosplit -trans -cap -nets -inp -from IN_A > xx
report_timing -rise_from IN_A -sig 4 -trans -cap -nets -inp > yy
```
![img3](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%209/Images/Lab/img3.png)
![img4](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%209/Images/Lab/img4.png)

Step 6. Timing report for min delay
```
report_timing -delay min -from IN_A
```
A clue that it is reporting hold time. (For slack time, look for just the difference in number. Don't go for sign.)
* hold = arrival -required
* setup = required - arrival 

![img5](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%209/Images/Lab/img5.png)

* `<-`: The arrow mark is used to indicate through which point we are reporting. 
![img6](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%209/Images/Lab/img6.png)

* The contribution from the cell can be min or max delay. It is not the contribution of the cell that matters; it is the **overall delay of the path that matters.**

## Design Load Check

* `check_timing`: Ensures that the design is constrained properly. It will check whether the design is constrained or not.
```
check_timing
```
![img1](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%209/Images/check_time_design/img1.png)

After sourcing `lab8_cons_modified.tcl`. 

![img3](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%209/Images/check_time_design/img3.png)

* 'report_constraints' : Displays the constraints applied to the design. If no user-defined constraints are present, it shows the default constraints stored in the tool's memory. Below is an example of default constraints

![img2](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%209/Images/check_time_design/img2.png)

After sourcing `lab8_cons_modified.tcl`.

![img4](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%209/Images/check_time_design/img4.png)
* `check_design` : To check the current design

Considering the mux_generate_128_1.v design. 
```
module mux_generate (input [127:0]i0 , input [6:0] sel  , output reg y);
integer k;
always @ (*)
begin
for(k = 0; k < 128; k=k+1) begin
	if(k == sel)
		y = i0[k];
end
end
endmodule
```


* For the above design, the number of fanout and the capacitance value a alot. Due to that, we will see a violation in the timing report 

![img5](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%209/Images/check_time_design/img5.png)

* `set_max_capacitance 0.025 [current_design]` : To control the maximum capacitance of the entire design.
![img6](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%209/Images/check_time_design/img6.png)

* `report_constraint -all_violators` : Command to know what all constraints are violating. 
![img7](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%209/Images/check_time_design/img7.png)

* After compilation, the timing is met and there are no violation 
  - report_constraints 
![img8](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%209/Images/check_time_design/img8.png)

  - report_timing 
![img9](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%209/Images/check_time_design/img9.png)

  - report_timing -net -cap -sig 4
![img10](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%209/Images/check_time_design/img10.png)

![img11](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%209/Images/check_time_design/img11.png)

Steps performed to set_max_capacitance. 
```
read_verilog mux_generate_128_1.v
check_design
link
compile_ultra
write -f verilog -out mux_generate_128_1_net.v
report_timing -net -cap -sig 4
set_max_delay -from [all_inputs] -to [all__outputs] 3.5
set_max_capacitance 0.025 [current_design]
report_constraint -all_violators
compile_ultra
report_constraints
report_timing
report_timing -net -cap -sig 4
```

### High Fan out 
![img1](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%209/Images/HFN/img1.png)

Creating en_128.v file
```
module en_128 (input [127:0] x , output [127:0] y , input en);
	assign y[127:0] = en ?x[127:0]:128'b0;
endmodule
```

`report_timing -from en -inp -nets -cap` 
![img2](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%209/Images/HFN/img2.png)

```
set_max_capacitance 0.03 [current_design]
report_constraints
```
![img3](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%209/Images/HFN/img3.png)

After compilation, `compile_ultra`. Below is the report timing `report_timing -from en -inp -nets -cap -sig 4`
![img4](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%209/Images/HFN/img4.png)

* Earlier single enable was driving all 128 pins. But now it has been a tree. It is driving only a few buffers. 
![img5](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%209/Images/HFN/img5.png)


![img6](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%209/Images/HFN/img6.png)
![img7](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%209/Images/HFN/img7.png)

```
set_max_transition 0.15 [current_design]
report_constraints
```
* When a violation is detected, Design Compiler assigns a higher cost to that specific area. As a result, only that portion of the design will be prioritized and optimized. 

![img8](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%209/Images/HFN/img8.png)

```
report_constraints -all_violators
```

![img9](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%209/Images/HFN/img9.png)

```
compile_ultra
report_constraints -all_violators
```
 
* After compilation, there is no transition violation. All transition violation is removed 
![img10](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%209/Images/HFN/img10.png)

```
report_timing -from en -inp -nets -cap -sig 4 -nosplit -from en -to y[116]
```
![img11](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%209/Images/HFN/img11.png)  

![img12](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%209/Images/HFN/img12.png)

![img13](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%209/Images/HFN/img13.png)
![img14](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%209/Images/HFN/img14.png)
