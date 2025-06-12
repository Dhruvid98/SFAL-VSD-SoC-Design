# Introduction to Logic Synthesis 

- Tools used for the lab session  
  * Iverilog - Verilog compilation and simulation
  * GTKwave - Viewing the simulation output
  * Synopsys Design Compiler - Used for logic synthesis
  * Skywater 130nm Library - For standard cell library

## Digital Logic and Synthesis
* Digital logic is a **switching function** used in automation and decision-making processes
* The behavioral model of design is expressed in the HDL programming language known as Register Transfer Logic, which includes Verilog and VHDL.
* **Synthesis** is the process of converting RTL to gate-level translation.
![into_pic1](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%205/Image/Intro/Screenshot%202025-06-05%20222726.png)  

**.LIB file**
*.lib file is a collection of standard cells.
![.lib why](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%205/Image/Intro/Screenshot%202025-06-05%20223208.png)

### Why do we need different flavors of cells?
![why different](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%205/Image/Intro/Screenshot%202025-06-05%20223453.png)  
![slow](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%205/Image/Intro/Screenshot%202025-06-05%20223654.png)  
![diff_slow_fast](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%205/Image/Intro/Screenshot%202025-06-05%20223832.png)

### How to select cells 
* The guidance offered to the synthesizer in the form of  **CONSTRAINTS**
![synthesizer](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%205/Image/Intro/Screenshot%202025-06-05%20224145.png)

Example of synthesis 
![example of syn](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%205/Image/Intro/synth_exple.png)  

What will be the correct implementation based on the different implementations 

![implement option](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%205/Image/Intro/different_implement.png)  

Standard cell details for each cell.

![std_cell_details](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%205/Image/Intro/std_Cell_detail.png)  

Implementation 3 is the best scenario based on below.
![implement](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%205/Image/Intro/final_impl.png)  

* Will implementation 3 always be the best case?
   - No. It depends on whether the logic is present in the hold-sensitive path. If additional buffers are added, then it will impact both power and area.

* In digital circuit design, our goal is to ensure that the circuit is logically correct, electrically correct, and meets all timing requirements. 
* All three implementations are valid, and the choice will be made depending on the requirements. The *constraints* define these needs. The synthesizer is guided by constraints to choose the library cells that are most suited for the design.

## Introduction to Design Compiler (DC)

### What is Design Compiler 
![dc what](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%205/Image/DC/DC.png)  

### Terminologies associated with Design Compiler
![termi with dc](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%205/Image/DC/terminologies.png)  

### Synopsys Design Contraints 
![SDC](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%205/Image/DC/SDC.png)  

### Setting up Design Compiler (DC)
![DC setup](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%205/Image/DC/Dc%20setup.png)

### Implementation flow of ASIC 
* Steps in converting RTL to physical database (GDS)

![asic flow](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%205/Image/DC/ASIC%20flow.png)

### DC Synthesis flow 
* Linking the design means to know that all the information that is present in the design can be implemented in the form of standard cell libraries.

![dc syhntesis flow](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%205/Image/DC/DC_synthesis_flow.png)

## Lab 1 Invoking DC basic setup
DC is invoked in folder `/home/dhruvi/sky130RTLDesignAndSynthesisWorkshop`. Commands to invoke the Design compiler (DC compiler)
```
csh
dc_shell // invoke dc
echo $target_library // your_library.db
echo $link_library // * your_library.db 
read_verilog DC_WORKSHOP/verilog_files/lab1_flop_with_en.v
write -f verilog -out lab1_net_sky130.v
sh gvim lab1_net_sky130.v
```
Here **your_library.db** is imaginary non-existent library, its a dummy library invoked in the DC.  

Verilog code for `lab1_flop_with_en.v`(DFF with Asynchronous Reset)
```
module lab1_flop_with_en ( input res , input clk , input d , input en , output reg q);
always @ (posedge clk , posedge res)
begin
	if(res)
		q <= 1'b0;
	else if(en)
		q <= d;	
end
endmodule
```
![read_verilog](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%205/Image/Lab1/read_verilog.png)  

The screenshot above appears after executing the `read_verilog` command in Design Compiler (DC). This output includes several important messages related to the compilation and design understanding process. One of the key components mentioned is `gtech.db`, which is a virtual library used internally by DC to represent generic technology components. It plays a crucial role in helping the tool understand the design before mapping it to a specific technology library. The tool also invokes the HDL Compiler (or Presto HDL Compiler) to analyze and compile the provided Verilog source files.

A notable warning in the output is:
**Warning: Can't read link_library file 'your_library.db'. (UID-3)**  
This means that the DC compiler is unable to locate or read the file your_library.db, that was created for dummy purpose. To resolve this, you need to update the link_library variable to point to the correct technology library. The message compiling source file`/home/dhruvi/sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/verilog_files/lab1_flop_with_en.v` indicates that DC is compiling the verilog source file, and it infers the registers or memory device which is 1-bit flip-flop with asynchronous reset. We need to link the design properly and point to the proper technology library.   

![write](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%205/Image/Lab1/write_verilog.png) 

When the above commands is executed to generate the netlist, the error **Can't read the link library 'your_library.db'** is found. This error occurs because no standard cell library was provided to the Design Compiler. As a result, the tool is using gtech cells, and the netlist is written using dummy cells.  
 
Below is the lab1_net.v is opened using the command sh gvim lab1_net.v looks like as shown below. The netlist is not in form of sky130 library cells.
```
module lab1_flop_with_en ( res, clk, d, en, q );
  input res, clk, d, en;
  output q;


  \**SEQGEN**  q_reg ( .clear(res), .preset(1'b0), .next_state(d), 
        .clocked_on(clk), .data_in(1'b0), .enable(1'b0), .Q(q), .synch_clear(
        1'b0), .synch_preset(1'b0), .synch_toggle(1'b0), .synch_enable(en) );
endmodule
```

 By setting correct target_library and link_library pointing to the std cell .db file, we can write the netlist in sky130 library cells. Below are the correct commands to create netlist in sky130 lib using DC compiler. 
 
 ```
csh
dc_shell
set target_library /home/dhruvi/sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/lib/sky130_fd_sc_hd__tt_025C_1v80.db
set link_library {* /home/dhruvi/sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/lib/sky130_fd_sc_hd__tt_025C_1v80.db}
read_db DC_WORKSHOP/lib/sky130_fd_sc_hd__tt_025C_1v80.db
read_verilog DC_WORKSHOP/verilog_files/lab1_flop_with_en.v
link
compile
write -f verilog -out lab1_net_sky130.v
sh gvim lab1_net_sky130.v
```

There may be multiple libraries in DC memory. * represents all the libraries already loaded in DC memory. So we are appending an additional library without overwriting the already loaded library. Below is the correct Verilog netlist generated with the skywater130 library. 

```
module lab1_flop_with_en ( res, clk, d, en, q );
  input res, clk, d, en;
  output q;
  wire   n2, n3;

  sky130_fd_sc_hd__dfrtp_1 q_reg ( .D(n3), .CLK(clk), .RESET_B(n2), .Q(q) );
  sky130_fd_sc_hd__mux2_1 U5 ( .A0(q), .A1(d), .S(en), .X(n3) );
  sky130_fd_sc_hd__clkinv_1 U6 ( .A(res), .Y(n2) );
endmodule
```

## Lab2 - Intro to DDC GUI with Design Vision
Command to write the DDC file after compilation
```
write -f ddc -out lab1.ddc
```

Commands to launch Design Vision 

```
csh
design_vision
```

Once the GUI is opened, the command to open DDC file
```
read_ddc lab1.ddc
```
When using the GUI, the `read_verilog` command reads only the Verilog source file into the tool. Whereas the read_ddc command loads both the design and the associated library information. A DDC file captures and stores all relevant design data, including technology libraries, within the tool's memory for use in that session.  

![design](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%205/Image/Lab2/design_v.png)  
![explain](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%205/Image/Lab2/pic2.png)  

## Lab 3 - Synopsys Design Compiler setup
`.synopsys_dc.setup` file is used to print all repetitive tasks that are used for setting up the tool. The user's DC tool invocation directory overwrites the default .synopsys_dc.setup that is installed under DC.  
![dc_setup](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%205/Image/Lab3/dc_setup.png)  

The setup file by gvim .synopsys_dc.setup and copy paste the target library and link library commands as below. 
```
set target_library /home/dhruvi/sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/lib/sky130_fd_sc_hd__tt_025C_1v80.db
set link_library {* $target_library}
```
