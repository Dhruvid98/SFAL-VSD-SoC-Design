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
  
