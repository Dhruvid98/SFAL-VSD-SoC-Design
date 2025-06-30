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
	
## Lab 8 - Loading design, get_cells, get_ports and get_nets
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


## Lab 9 - get_pins, get_clocks, querying_clocks.

Syntax to get and read all the pins
```
get_pins * // get all pins
foreach_in_collection my_pin [get_pins *] {
set pin_name [get_object_name $my_pin];
echo $pin_name;
}
```
Below is the output. 
![img1](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/Lab2/img1.png)  

Command for different attributes of a pin 
* To check direction of a pin

```
get_attribute [get_pins REGC_reg/RESET_B] direction 
```
* To check whether a pin is clock pin or not.
 - This attibute should only be queried on **input pins**

```
get_attribute [get_pins REGC_reg/RESET_B] clock
```

* To know direction of all pin

```
foreach_in_collection my_pin [get_pins *] {
set my_pin_name [get_object_name $my_pin];
set dir [get_attribute [get_pins $my_pin_name] direction];
echo $my_pin_name $dir;
}
```

Below is the output.  
![img2](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/Lab2/img2.png)  

Synatx of query_clk.tcl
* Here we are qureing all the clock pins who's direction is `in`.

```
foreach_in_collection my_pin [get_pins *] {
	set my_pin_name [get_object_name $my_pin];
        set dir [get_attribute [get_pins $my_pin_name] direction];                                                                                              
	if { [regexp $dir in] } {
		if { [get_attribute [get_pins $my_pin_name] clock ] } { 
 			echo $my_pin_name;

		}
	}
}
```

Below is the output. 
![img3](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/Lab2/img3.png) 

* Difference betwwen clock and clocks in get_attribute.
  - get_attribute [get_pins $my_pin_name]**clock** : Will tell us whether that pin is meant to receive the clock as per the standard cell library or not.
  - get_attribute [get_pins $my_pin_name]**clocks** : Will tell us what is the name of the clock reaching there. 

![img4](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/Lab2/img4.png)  

## Lab 10 - Create_clock waveform.
* The command `current_design` tells the name of top module we are working on.  

Syntax to create a clock and get it's attributes. 
* Here clock is generated with period (per) of 10ns\
* If the `get_attribute [get_clocks MYCLK] is_generated` is false then it is a master clock.

```
create_clock -name MYCLK -per 10 [get_ports clk] // generate the clock
get_clocks * // to know clocks
get_attribute [get_clocks MYCLK] period // period of clock
get_attribute [get_clocks MYCLK] is_generated // to check whether the clock is generated or not
report_clocks * // to know the information about all clock
```
![img1](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/Lab10/img1.png)  

* Query the attributes of all clock pin

```
foreach_in_collection my_pin [get_pins *] {
	set my_pin_name [get_object_name $my_pin];
        set dir [get_attribute [get_pins $my_pin_name] direction];                                                                                              
	if { [regexp $dir in] } {
		if { [get_attribute [get_pins $my_pin_name] clock ] } { 
			set clk [get_attribute [get_pins $my_pin_name] clocks];
			set clk_name [get_object_name $clk];
 			echo $my_pin_name $clk_name;

		}
	}
}
```

![img2](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/Lab10/img2.png)

* The clock should be created only on **clock port** (on the external port which is meant to receive the clock) or on **clock generator**.
* Do not create a clock on the pin. The clock created on the pin will not reach to any clock pin of any flop

Syntax to remove the clock. (BAD_CLK is clock name)
```
remove_clock BAD_CLK 
```

Syntax to create a clock with different rising/falling time and different duty cycle. 
- The order of command doesn't matter when creating a clock.

```
create_clock -name MYCLK -period 10 [get_ports clk] -wave {5 10} // first_rise:5, first_fall : 10
create_clock -name MYCLK -period 10 -wave {0 2.5} [get_ports clk] // different duty cycle
```
![img3](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/Lab10/img3.png)  

## Lab 11 : Clock Network Modelling - Uncertainty, report_timing

![img1](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/Lab11/img1.png)  
![img2](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/Lab11/img2.png)

Syntax to model different latency
```
set_clock_latency -source 1 [get_clocks MYCLK] // source latency
set_clock_latency 1 [get_clocks MYCLK] // network latency
set_clock_uncertainty 0.5 [get_clocks MYCLK] // max delay or setup
set_clock_uncertainty -hold 0.1 [get_clocks MYCLK] // min delay or hold. 
```
* *By default*, model uncertainty is applied to the maximum delay or setup
  
* If no clock is present, report_timing shows **path is unconstrained**.
![img3](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/Lab11/img3.png)

Syntax to report clock to register
```
report_timing -to REGC_reg/D
```
As of now, a latency constraint has not been defined.  

![img5](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/Lab11/img5.png)
![img4](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/Lab11/img4.png) 

After modeling the clock, setting the clock latency using below commands. 
```
set_clock_latency -source 2 [get_clocks MYCLK]
set_clock_latency 1 [get_clocks MYCLK]
set_clock_uncertainty 0.5 [get_clocks MYCLK]
set_clock_uncertainty -hold 0.1 [get_clocks MYCLK]
```
![img6](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/Lab11/img6.png)  

* **What are we checking?**
  - data required time **>** data arrival time
  - slack =  data required time - data arrival time
  
*  Why uncertainity and skew are subtracted from the clock period ?
![img7](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/Lab11/img7.png)

Calculations for hold, uncertainty, and skew
- For setup, check happens across one period. 
- For hold, 0 cycle check happens.

![img8](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/Lab11/img8.png)  

Syntax to check report_timing for hold/min 
```
report_timing -to REGC_reg/D -dealy -min
```
![img9](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/Lab11/img9.png)

#### All Reg2Reg paths are constraints by clock. 

## Lab 12 : IO Delays
The input and output paths in the design have not been constrained yet. 
![img1]()  

Syntax to know the modeling of ports and pins
```
report_port verbose
```

* Report_timing shows **path is unconstrained** for Input and Output paths.

Syntax to see timing around port IN_A and OUT_Y. 
```
report_timing -from IN_A
report_timing -to OUT_Y
```
![img2]() 
![img3]() 

Syntax to model the input port delay
```
set_input_delay -max 5 -clock [get_clocks MYCLK] [get_ports IN_A]
report_timing -from IN_A
```

![img4]()

Syntax to model the transition in port IN_A and store it in a file.
```
report_timing -from IN_A -trans -net -cap -nosplit > a
```
![img5]()  

</details>
