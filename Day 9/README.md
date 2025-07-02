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
