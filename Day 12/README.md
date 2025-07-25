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
![img11]()  
![img12]()  
![img13]()  
![img14]()  
![img15]()  
![img16]()  
![img17]()  
![img18]()  
![img19]()  
![img20]()  
![img21]()  
![img22]()  

## Post-Synthesis Simulation
Command
```
iverilog -DFUNCTIONAL -DUNIT_DELAY=#1 -o ./output/post_synth_sim.out ./src/gls_model/primitives.v ./src/gls_model/sky130_fd_sc_hd.v ./output/vsdbabysoc_net.v ./src/module/avsdpll.v ./src/module/avsddac.v ./src/module/testbench.v
./a.out
```
* `-DFUNCTIONAL`: Defines `FUNCTIONAL` to use behavioral models instead of detailed gate-level timing.
* `-DUNIT_DELAY=#1 ` : Assigns a unit delay of #1 to all gates for post-synthesis simulation.
![img23]()
![img24]()

```
gtkwave dump.vcd
```
![img25]()

### Verify Pre-Synthesis vs Post-Synthesis
![img26]()


**Errors** 
* Errors during avsdpll.db conversion of avsdpll.lib lib file.

![error2]()

* Errors during GLS simulation 

![error1]()
