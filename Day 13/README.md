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

