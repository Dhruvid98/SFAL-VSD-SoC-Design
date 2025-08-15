# Day 12: Post-Synthesis Simulation

## Introduction 
Gate-Level Simulation (GLS) verifies both functionality and timing of the design after synthesis.  Pre-synthesis simulations (RTL simulations), which validate logic without any delays, GLS incorporates gate delays and timing information extracted from the synthesized netlist. This helps in catching issues like timing violations, race conditions, functionality verification, dynamic circuit behavior, or glitches. 

The initial step in the design flow is to synthesize the generated RTL code, followed by simulating the synthesized output. This process helps identify potential issues in the code. In this section, we will synthesize the RTL and then perform a post-synthesis simulation to detect any discrepancies. Ideally, the results of the post-synthesis simulation should match those from the pre-synthesis (modeling) phase, confirming that synthesis has not altered the original design behavior.

##  Pre-Synthesis and Post-Synthesis

  1. Pre-Synthesis
      * Focuses only on verifying the functionality of the code.
      * It helps to detect and correct logical errors, such as incorrect operator usage or unintended latch inference.
      * Events occur on the active clock edge; therefore, there is a zero-delay environment. 

  2. Post-Synthesis
      * Focuses only on verifying both the functionality and timing of the design using a synthesized netlist
      * Identifies timing violations and potential mismatches. It also helps verify dynamic circuit behavior.

These simulations ensure a robust and reliable digital design.

## Steps for Conversion of .lib to .db Files

*  **Synopsys Library Compiler** (lc_shell) is used to convert  .lib to .db
* `.db` files are genrated for `avsddac`, `avsdpll`, and `sky130_fd_sc_hd__tt_025C_1v80` libraries.
  * `sky130_fd_sc_hd__tt_025C_1v80` is avaliable for download at [Skywater GitHub repository.](https://github.com/efabless/skywater-pdk-libs-sky130_fd_sc_hd/tree/master/timing)

## Converting `avsddac.lib` to `avsddac.db`

Path `cd /home/dhruvi/VSDBabySoC/src/lib `  

![img1](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2012/Images/img1.png)    

Launching library compiler 
```
$lc_shell
```

![img2](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2012/Images/img2.png)  

Reading the `avsddac.lib` file and converting it into `avsddac.db`

```
read_lib avsddac.lib
write_lib avsddac -format db -output avsddac.db
```

![img3](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2012/Images/img3.png)  
![img4](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2012/Images/img4.png)  

## Converting avsdpll.lib to avsdpll.db

Commands to convert avsdpll.lib to avsdpll.db
```
cd /home/dhruvi/VSDBabySoC/src/lib
lc_shell
read_lib avsdpll.lib
write_lib avsdpll -format db -output avsdpll.db
```

![img5](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2012/Images/img5.png)  
![img6](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2012/Images/img6.png)  

## Converting sky130_fd_sc_hd__tt_025C_1v80.lib to sky130_fd_sc_hd__tt_025C_1v80.db  

* Downloading the .lib file
`wget https://raw.githubusercontent.com/efabless/skywater-pdk-libs-sky130_fd_sc_hd/master/timing/sky130_fd_sc_hd__tt_025C_1v80.lib`

Commands to convert sky130_fd_sc_hd__tt_025C_1v80.lib to sky130_fd_sc_hd__tt_025C_1v80.db
```
cd /home/dhruvi/VSDBabySoC/src/lib
lc_shell
read_lib sky130_fd_sc_hd__tt_025C_1v80.lib
write_lib sky130_fd_sc_hd__tt_025C_1v80 -format db -output sky130_fd_sc_hd__tt_025C_1v80.db
```

![img7](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2012/Images/img7.png)  
![img8](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2012/Images/img8.png)  

## Running Synthesis and GLS
* After generating the .db files, running the synthesis and GLS

### Synthesis 

```
cd /home/dhruvi/VSDBabySoC/src/lib
dc_shell
set target_library /home/dhruvi/VSDBabySoC/src/lib/sky130_fd_sc_hd__tt_025C_1v80.db
set link_library {* /home/dhruvi/VSDBabySoC/src/lib/sky130_fd_sc_hd__tt_025C_1v80.db /home/dhruvi/VSDBabySoC/src/lib/avsdpll.db /home/dhruvi/VSDBabySoC/src/lib/avsddac.db}
```

![img9](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2012/Images/img9.png)  

```
set search_path {/home/dhruvi/VSDBabySoC/src/module}
read_file {sandpiper_gen.vh  sandpiper.vh  sp_default.vh  sp_verilog.vh clk_gate.v rvmyth.v rvmyth_gen.v vsdbabysoc.v} -autoread -top vsdbabysoc
link
compile_ultra
write_file -format verilog -hierarchy -output /home/dhruvi/VSDBabySoC/output/vsdbabysoc_net.v
report_qor > report_qor.txt
````

![img10](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2012/Images/img10.png)  
![img11](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2012/Images/img11.png)  
![img12](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2012/Images/img12.png)  
![img13](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2012/Images/img13.png)  
![img14](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2012/Images/img14.png)  
![img15](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2012/Images/img15.png)  
![img16](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2012/Images/img16.png)  
![img17](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2012/Images/img17.png)  
![img18](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2012/Images/img18.png)  
![img19](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2012/Images/img19.png)  
![img20](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2012/Images/img20.png)  
![img21](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2012/Images/img21.png)  
![img22](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2012/Images/img22.png)  

## Post-Synthesis Simulation

Command
```
iverilog -DFUNCTIONAL -DUNIT_DELAY=#1 -o ./output/post_synth_sim.out ./src/gls_model/primitives.v ./src/gls_model/sky130_fd_sc_hd.v ./output/vsdbabysoc_net.v ./src/module/avsdpll.v ./src/module/avsddac.v ./src/module/testbench.v
./a.out
```

* `-DFUNCTIONAL`: Defines `FUNCTIONAL` to use behavioral models instead of detailed gate-level timing.
* `-DUNIT_DELAY=#1 ` : Assigns a unit delay of #1 to all gates for post-synthesis simulation.

![img23](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2012/Images/img23.png)
![img24](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2012/Images/img24.png)

```
gtkwave dump.vcd
```

![img25](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2012/Images/img25.png)

### Verify Pre-Synthesis vs Post-Synthesis

![img26](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2012/Images/img26.png)


**Errors** 

* Errors during avsdpll.db conversion of avsdpll.lib lib file.

![error2](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2012/Images/error2.png)

* Errors during GLS simulation 

![error1](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2012/Images/error1.png)


## Synthesizing the design with yosys

### Reading the main vsdbabysoc.v RTL file in yosys
```
$yosys
$read_verilog src/module/vsdbabysoc.v 
```
![img1](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2012/Images/yosys/img1.png)

### Reading the rvmyth.v file
```
read_verilog -I ~/VSDBabySoC/src/include/ ~/VSDBabySoC/src/module/rvmyth.v
```
![img2](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2012/Images/yosys/img2.png)  

### Reading the clk_gate.v file
```
read_verilog -I ~/VSDBabySoC/src/include/ ~/VSDBabySoC/src/module/clk_gate.v
```
![img3](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2012/Images/yosys/img3.png)

### Loading the Liberty Files for Synthesis
```
read_liberty -lib ~/VLSI/VSDBabySoC/src/lib/avsdpll.lib 
read_liberty -lib ~/VLSI/VSDBabySoC/src/lib/avsddac.lib 
read_liberty -lib ~/VLSI/VSDBabySoC/src/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
![img4](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2012/Images/yosys/img4.png)

### Running Synthesis
```
synth -top vsdbabysoc
```
![img5](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2012/Images/yosys/img5.png)

### Mapping DFF with standard cells
```
dfflibmap -liberty src/lib/sky130_fd_sc_hd__tt_025_1v80.lib //standard-cell lib used for logic mapping
opt
abc -liberty src/lib/sky130_fd_sc_hd__tt_025_1v80.lib //standard-cell lib used for logic mapping
```
![img6](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2012/Images/yosys/img6.png)
![img7](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2012/Images/yosys/img7.png)
![img8](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2012/Images/yosys/img8.png)

### Clean up and renaming
```
$flatten 
$setundef -zero
$clean -purge
$rename -enumerate
```
* `Flatten`: Flattens the entire design hierarchy into a single-level netlist.
* `setundef -zero`: Replaces all undefined (x) logic values with logical 0 to avoid simulation issues
* `clean -purge`: Removes all unused wires, cells, and modules; -purge makes it more aggressive.
* `rename -enumerate`: Renames internal wires and cells to unique, numbered names for consistency.

### Stats
```
$ stat
```
```
=== vsdbabysoc ===

   Number of wires:               4736
   Number of wire bits:           6210
   Number of public wires:        4736
   Number of public wire bits:    6210
   Number of ports:                  7
   Number of port bits:              7
   Number of memories:               0
   Number of memory bits:            0
   Number of processes:              0
   Number of cells:               5920
     $scopeinfo                      8
     avsddac                         1
     avsdpll                         1
     sky130_fd_sc_hd__a2111oi_0     10
     sky130_fd_sc_hd__a211o_2        1
     sky130_fd_sc_hd__a211oi_1      26
     sky130_fd_sc_hd__a21boi_0       4
     sky130_fd_sc_hd__a21o_2         1
     sky130_fd_sc_hd__a21oi_1      672
     sky130_fd_sc_hd__a221o_2        1
     sky130_fd_sc_hd__a221oi_1     163
     sky130_fd_sc_hd__a22o_2         4
     sky130_fd_sc_hd__a22oi_1      123
     sky130_fd_sc_hd__a311oi_1       4
     sky130_fd_sc_hd__a31o_2         1
     sky130_fd_sc_hd__a31oi_1      344
     sky130_fd_sc_hd__a32oi_1        2
     sky130_fd_sc_hd__a41oi_1       26
     sky130_fd_sc_hd__and2_2        12
     sky130_fd_sc_hd__and3_2         1
     sky130_fd_sc_hd__clkinv_1     597
     sky130_fd_sc_hd__dfxtp_1     1144
     sky130_fd_sc_hd__lpflow_inputiso0p_1      1
     sky130_fd_sc_hd__mux2i_1       12
     sky130_fd_sc_hd__nand2_1      839
     sky130_fd_sc_hd__nand3_1      249
     sky130_fd_sc_hd__nand3b_1       1
     sky130_fd_sc_hd__nand4_1       41
     sky130_fd_sc_hd__nor2_1       403
     sky130_fd_sc_hd__nor3_1        35
     sky130_fd_sc_hd__nor4_1         2
     sky130_fd_sc_hd__o2111ai_1     20
     sky130_fd_sc_hd__o211a_1        1
     sky130_fd_sc_hd__o211ai_1      49
     sky130_fd_sc_hd__o21a_1         6
     sky130_fd_sc_hd__o21ai_0      866
     sky130_fd_sc_hd__o21ba_2        1
     sky130_fd_sc_hd__o21bai_1      18
     sky130_fd_sc_hd__o221a_2        1
     sky130_fd_sc_hd__o221ai_1       7
     sky130_fd_sc_hd__o22ai_1      155
     sky130_fd_sc_hd__o2bb2ai_1      1
     sky130_fd_sc_hd__o311ai_0       2
     sky130_fd_sc_hd__o31ai_1        3
     sky130_fd_sc_hd__o32ai_1        1
     sky130_fd_sc_hd__o41ai_1        1
     sky130_fd_sc_hd__or2_2         12
     sky130_fd_sc_hd__or3_2          1
     sky130_fd_sc_hd__or4_2          1
     sky130_fd_sc_hd__xnor2_1       13
     sky130_fd_sc_hd__xor2_1        32
```

### Writing Synthesized Netlist
```
$write_verilog -noattr ~/VSDBabySoC/output/post_synth_sim/vsdbabysoc.netlist.v
```
![img9](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2012/Images/yosys/img9.png)

### Compiling the testbench and running the simulation:
```
$ iverilog -o output/post_synth_sim/post_synth_sim.out -DPOST_SYNTH_SIM -DFUNCTIONAL -DUNIT_DELAY=#1 -I src/include -I /src/module /src/module/testbench.v
```
![img10](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2012/Images/yosys/imh10.png)

* TO resolve the issue, update the syntax in the file sky130_fd_sc_hd.v at or around line 74452.

From 
```
`endif SKY130_FD_SC_HD__LPFLOW_BLEEDER_FUNCTIONAL_V
```

To 
```
`endif // SKY130_FD_SC_HD__LPFLOW_BLEEDER_FUNCTIONAL_V
```

### Running the Simulation in gtkwave
```
cd output/post_synth_sim/
./post_synth_sim.out
gtkwave post_synth_sim.vcd
```
![img11](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2012/Images/yosys/img11.png)
