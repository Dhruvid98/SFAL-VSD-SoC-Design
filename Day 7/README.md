# Day 7 - Advanced Constraints

<details>
    <summary>1. Clock Tree Modelling and IO Delays </summary>

## Clock Tree Modelling and Uncertainty

* Basic constraints
    - Reg2Reg - Clock period
    - Input to Reg - Clock period, Input delay and Input transition
    - Reg to Output - Clock period, Output delay and Output transition

### What needs to be constrained for the clock ?
Clock period. As the clock period limits the time taken. 

* Will the clock arrive at the same time to the flop?
    - In a real scenario, definitely **NO**. The clock is built only during CTS; before that, the clock is an ideal network. But the clock doesn't reach all the flops at the same time. During synthesis, logic is optimized considering an ideal clock network. Should synthesis consider the practicality of the clock network?
      
![img1](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/Clock_tree_uncertainty/img1.png)

### Clock Generation and Jitter

* **Jitter**: Stochastic variations of the clock generator.
![img2](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/Clock_tree_uncertainty/img2.png)

### Clock Distribution and Skew

* **Skew**: The Timing difference between when a clock signal arrives at one flip-flop versus another within the same clock domain.
![img3](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/Clock_tree_uncertainty/img3.png)

![img4](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/Clock_tree_uncertainty/img4.png)  

### Factors for Clock Modelling  

![img5](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/Clock_tree_uncertainty/img5.png)  
![img6](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/Clock_tree_uncertainty/img6.png)  

## IO delays. 

![img1](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/IO%20delays/img1.png)

### Getting the Ports and Clock in DC

![img2](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/IO%20delays/img2.png)
![img3](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/IO%20delays/img3.png)

### Querying the cells in the design 
- Hierarchical pins are nets

![img4](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/IO%20delays/img4.png)  

### Clock Distribution 

![img5](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/IO%20delays/img5.png)  
![img6](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/IO%20delays/img6.png)

### Creating Clock 
- Here DC: Duty Cycle.
  
![img7](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/IO%20delays/img7.png)

### Constraining IO Paths

![img8](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/IO%20delays/img8.png)  
![img9](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/IO%20delays/img9.png)  

</details>

<details>
    <summary>2. Labs 8–12: Design Loading, Clock Creation & Timing Characterization </summary>
	
## Lab 1 - Loading design, get_cells, get_ports and get_nets
 lab8_circuit.v (verilog code)
    
 ```
module lab8_circuit (input rst, input clk , input IN_A , input IN_B , output OUT_Y , output out_clk);
reg REGA , REGB , REGC ; 

always @ (posedge clk , posedge rst)
begin
	if(rst)
	begin
		REGA <= 1'b0;
		REGB <= 1'b0;
		REGC <= 1'b0;
	end
	else
	begin
		REGA <= IN_A | IN_B;
		REGB <= IN_A ^ IN_B;
		REGC <= !(REGA & REGB); 
	end
end

assign OUT_Y = ~REGC;

assign out_clk = clk;

endmodule
 ```

The corresponding circuit for lab8_circuit.v.  
![img1](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/Lab1/img1.png)  

Syntax to run the command in DC under /verilog_files folder. ($target_lib and $link_lib are set to .db)

```
csh
dc_shell
read_verilog lab8_circuit.v
link
compile_ultra
```

* Reading the Verilog file should not throw any errors.
    - A useful message for that `Presto compilation completed successfully`: RTL does not have any errors or loading issues. It got loaded successfully.
* The file has inferred 3 registers, 1-bit wide, asynchronous reset type as shown below.

 ![img2](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/Lab1/img2.png)

* The compilation shouldn't throw any errors.
![img3](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/Lab1/img3.png)

### Commands with get ports
![img4](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/Lab1/img4.png)

### Commands with get_cells
![img5](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/Lab1/img5.png)

* Reference name of the cell in the library
![img6](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/Lab1/img6.png)

The output obtained is sky130_fd_sc_hd__dfrtp_1, where `dfrtp` means `df`: DFF, `r`: asynchronous reset, `p`: positive triggered and `t`: true output (Q).  

* Syntax to know the reference name of a cell or all the cells in the design.
![img7](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/Lab1/img7.png)

Command to write DDC of the design
```
write -f ddc -out lab8_circuit.ddc
```

Commands to open design_vision and read ddc file of design in Design Vision GUI.

```
csh
design_vsion
read_ddc lab8_circuit.ddc
```
![img8](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/Lab1/img8.png)

```
get_nets * // get all nets of the design in Design Vision
all_connected N1 // to know were is N1 net is connected
```
![img9](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/Lab1/img9.png)

* In design digital net can only be driven by **one** driver
  - If there are multiple driver nets -> Logcial level corrupted (inconclusive).
* Latch is a multidriven net because it is working within the standard cell called LATCH. As sizing of cells such as invertor will be taken care of.

![img10](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/Lab1/img10.png)

</details>
