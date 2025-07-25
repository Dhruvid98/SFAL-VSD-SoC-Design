# Day 12: Post-Synthesis Simulation

## Introduction 
Gate-Level Simulation (GLS) verifies both functionality and timing of the design after synthesis.  Pre-synthesis simulations (RTL simulations), which validate logic without any delays, GLS incorporates gate delays and timing information extracted from the synthesized netlist. This helps in catching issues like timing violations, race conditions, or improper use of blocking/non-blocking assignments that may not be visible during RTL simulation.

##  Pre-Synthesis and Post-Synthesis

  1. Pre-Synthesis
      * Focuses only on verifying the functionality of the code.
      * Events occur on the active clock edge; therefore there is a zero-delay environment. 

  2. Post-Synthesis
      * Focuses only on verifying both the functionality and timing of the design using a synthesized netlist
      * Identifies timing violations and potential mismatches. It also helps verify dynamic circuit behavior.

## Steps for Conversion of .lib to .db Files

*  **Synopsys Library Compiler** (lc_shell) is used to convert  .lib to .db
* `.db` files are genrated for `avsddac`, `avsdpll`, and `sky130_fd_sc_hd__tt_025C_1v80` libraries.
  * `sky130_fd_sc_hd__tt_025C_1v80` is avaliable for download at [Skywater GitHub repository.](https://github.com/efabless/skywater-pdk-libs-sky130_fd_sc_hd/tree/master/timing)

## Converting `avsddac.lib` to `avsddac.db`

Path `cd /home/dhruvi/VSDBabySoC/src/lib `
![img1]()    

Launching library compiler 
```
$lc_shell
```
![img2]()  

Reading the `avsddac.lib` file and converting it into `avsddac.db`

```
read_lib avsddac.lib
write_lib avsddac -format db -output avsddac.db
```
![img3]()  
![img4]()  

## Converting avsdpll.lib to avsdpll.db

Commands to convert avsdpll.lib to avsdpll.db
```
cd /home/dhruvi/VSDBabySoC/src/lib
lc_shell
read_lib avsdpll.lib
write_lib avsdpll -format db -output avsdpll.db
```
![img5]()
![img6]()  

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
![img7]()
![img8]()  
