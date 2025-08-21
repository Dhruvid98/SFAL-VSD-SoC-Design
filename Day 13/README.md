# Day 13: PVT Corners Timing Analyses

This task involves performing synthesis, timing analysis, and reporting of post-synthesis simulations on the VSDBabySoC design with OpenSTA using SDC constraints across multiple Process, Voltage, Temperature corners. The goal is to validate the design across diverse operating conditions, ensuring it meets timing requirements for robust functionality. In industry, this is typically achieved by analyzing various PVT corners to guarantee optimal performance, power, and area (PPA) characteristics.

* PVT Corners: Represent the varying conditions under which a semiconductor device is tested to ensure reliable and consistent performance.
    * `Process`: Variations in manufacturing can lead to different transistor speeds.
        * T: Typical corner
        * F: Fast 
        * S: Slow
    * `Voltage`: Represents the different voltage levels of the design.
    * `Temperature`: Represents the range of temperatures the design might experience.

  ## SDC constraints and synthesizing the design
  
* `vsdbabysoc_synthesis.sdc` constraint file defines the design requirement of synthesis.
     * Timing and Area: It constrains to manage maximum area usage and ensures signal timings within a `10ns` clock period.
     * Clock Specifications: Configurations for clock latency, uncertainty, and input delays.
     * Input/Output Loads: Defines input/output transition and load value.

* **Download Libraries**: Obtain .lib files for different corners from [Skywater PDK timing libraries](https://github.com/efabless/skywater-pdk-libs-sky130_fd_sc_hd/tree/master/timing).
* The below TCL script `sta_across_pvt.tcl` can be run to perform the STA across the PVT corners for which the sky130 lib files are available.
```
set list_of_lib_files(1) "sky130_fd_sc_hd__tt_025C_1v80.lib"
set list_of_lib_files(2) "sky130_fd_sc_hd__ff_100C_1v65.lib"
set list_of_lib_files(3) "sky130_fd_sc_hd__ff_100C_1v95.lib"
set list_of_lib_files(4) "sky130_fd_sc_hd__ff_n40C_1v56.lib"
set list_of_lib_files(5) "sky130_fd_sc_hd__ff_n40C_1v65.lib"
set list_of_lib_files(6) "sky130_fd_sc_hd__ff_n40C_1v76.lib"
set list_of_lib_files(7) "sky130_fd_sc_hd__ss_100C_1v40.lib"
set list_of_lib_files(8) "sky130_fd_sc_hd__ss_100C_1v60.lib"
set list_of_lib_files(9) "sky130_fd_sc_hd__ss_n40C_1v28.lib"
set list_of_lib_files(10) "sky130_fd_sc_hd__ss_n40C_1v35.lib"
set list_of_lib_files(11) "sky130_fd_sc_hd__ss_n40C_1v40.lib"
set list_of_lib_files(12) "sky130_fd_sc_hd__ss_n40C_1v44.lib"
set list_of_lib_files(13) "sky130_fd_sc_hd__ss_n40C_1v76.lib"

for {set i 1} {$i <= [array size list_of_lib_files]} {incr i} {
read_liberty ~/VSDBabySoC/src/pvt_corners/skywater-pdk-libs-sky130_fd_sc_hd/timing/$list_of_lib_files($i)
read_liberty -min /home/dhruvi/VSDBabySoC/src/lib/avsdpll.lib
read_liberty -max /home/dhruvi/VSDBabySoC/src/lib/avsdpll.lib
read_liberty -min /home/dhruvi/VSDBabySoC/src/lib/avsddac.lib
read_liberty -max /home/dhruvi/VSDBabySoC/src/lib/avsddac.lib
read_verilog ../VSDBabySoC/output/post_synth_sim/vsdbabysoc.netlist.v
link_design vsdbabysoc
current_design
read_sdc /home/dhruvi/VSDBabySoC/src/sdc/basic.sdc
report_checks
check_setup -verbose
report_checks -path_delay min_max -fields {nets cap slew input_pins fanout} -digits {4} > ./sta_output/min_max_$list_of_lib_files($i).txt
exec echo "$list_of_lib_files($i)" >> ./sta_output/sta_worst_max_slack.txt
report_worst_slack -max -digits {4} >> ./sta_output/sta_worst_max_slack.txt

exec echo "$list_of_lib_files($i)" >> ./sta_output/sta_worst_min_slack.txt
report_worst_slack -min -digits {4} >> ./sta_output/sta_worst_min_slack.txt

exec echo "$list_of_lib_files($i)" >> ./sta_output/sta_tns.txt
report_tns -digits {4} >> ./sta_output/sta_tns.txt

exec echo "$list_of_lib_files($i)" >> ./sta_output/sta_wns.txt
report_wns -digits {4} >> ./sta_output/sta_wns.txt
}
```
## PVT Timing Report table

![img1]()

* Negative WHS: Indicates a need for hold-time buffers in cases like the fast-fast (ff) corners.
* Negative WNS: Indicates that the points to set up timing issues may benefit from optimizing the logic path or pipeline stages.

## Analysis 
* Slowest corners: The worst max path (Setup-critical) corners are the process nodes are usually: ss_LowTemp_LowVolt, ss_HighTemp_LowVolt
* Fastest corners: The worst min path (Hold-critical) corners being: ff_LowTemp_HighVolt,ff_HighTemp_HighVolt.

## Graph 

**Worst setup Slack vs PVT corners**   
![img2]()  

**Worst hold Slack vs PVT corners**   
![img3]()  

**TNS vs PVT corners** 
![img4]()


Debug
1. Make sure the sdc clock is for 10ns
2. 

