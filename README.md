# SFAL-VSD SoC Design Program
Welcome to the repository documenting my journey through the SoC Design. This repository documents my hands-on progress, key takeaways, and daily explorations in digital hardware design. It covers topics from tool installation to advanced SoC design and implementation.

<details>
  <summary><a href="https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%200/README.md" target="_blank">Day 0 - Tools Installation</a></summary>
  
  #### Environment Setup & Tools Installed
  * Gained a high-level understanding of the complete chip development flow from specification to system integration.
  * Learned functional verification checkpoints at each stage (O0 to O4)
  * Installed open-source tools:
      * Yosys (Synthesis)
      * Icarus Verilog (Simulation)
      * GTKWave (Waveform viewer)
      * OpenSTA (Static Timing Analysis)
      * Ngspice (Simulation)
      * Magic (Layout editing)
      * OpenLane (RTL-to-GDSII flow)
</details>

<details>
  <summary><a href="https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%201/README.md" target="_blank">Day 1 - Introduction to Verilog RTL Design and Synthesis</a></summary>
  
  #### RTL Design & Synthesis Concepts
  * Simulated a 2:1 MUX RTL design using Icarus Verilog and visualized waveforms with GTKWave.
  * Synthesized the design using Yosys, linking it to a standard cell library.
  * Generated and reviewed the gate-level netlist for the synthesized MUX.
  * Gained hands-on experience with the flow: from HDL simulation to gate-level synthesis
</details>

<details>
  <summary><a href="https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%202/README.md" target="_blank">Day 2 - Timing Libraries, Hierarchical vs Flat Synthesis, Efficient Flop Coding Styles</a></summary>
  
  #### Library Modeling & Timing Learnings
  * Explored standard cell timing libraries (.lib files) and understood PVT-based behavior modeling.
  * Compared hierarchical vs. flat synthesis flows and analyzed structural outcomes.
  * Practiced submodule-level synthesis for modular design and reuse.
  * Simulated and synthesized flip-flops with both async/sync resets and sets.
  * Implemented ×2 and ×9 multipliers using bit manipulation to avoid combinational logic
</details>

<details>
  <summary><a href="https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%203/README.md" target="_blank">Day 3 - Combinational and Sequential Optimizations </a></summary>
  
  #### Optimization Strategies Explored
  * Applied combinational optimization techniques like constant propagation, Boolean logic simplification, and Karnaugh mapping to minimize area and gate count.
  * Practiced sequential logic optimization, including retiming, state minimization, and logic cloning to improve performance and layout efficiency.
  * Demonstrated optimization limits using flip-flop designs with specific reset/set behaviors and interdependencies.
  * Identified and optimized unused outputs in sequential blocks (e.g., 3-bit counter using only q[0]), leading to fewer synthesized flops.
</details>

<details>
  <summary><a href="https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%204/README.md" target="_blank">Day 4 - GLS, Blocking vs Non-Blocking, Synthesis-Simulation Mismatch </a></summary>
  
  #### Synthesis-Simulation Insights
  * Learned Gate-Level Simulation (GLS) using synthesized netlists with timing annotations
  * Identified critical causes of synthesis-simulation mismatches:
      * Missing sensitivity lists
      * Improper use of blocking `(=)` vs. non-blocking `(<=)` assignments
      * Non-standard Verilog coding practices
  * Demonstrated how incorrect sensitivity `(@sel instead of @(*))` leads to latch-like behavior
  * Analyzed functional differences between RTL and GLS outputs using GTKWave.
  * Validated synthesis behavior and mismatches across multiple modules.

</details>

<details>
  <summary><a href="https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%205/README.md" target="_blank">Day 5 - Introduction to Logic Synthesis </a></summary>
  
  #### RTL-to-Gate Synthesis Learnings
  * Understood RTL-to-Gate-Level synthesis using Synopsys Design Compiler with Sky130 standard cell libraries (.db format).
  * Explored timing-aware synthesis with constraints to optimize area, power, and performance.
  * Compared multiple synthesis implementations to evaluate trade-offs in timing and physical design.
  * Gained familiarity with .lib and .db formats and their roles in timing and library linking.
  * Built netlists using both generic (gtech) and Sky130-specific libraries.
  * Created and used .synopsys_dc.setup to streamline DC setup.
  * Practiced GUI navigation in Design Vision and automated flow using TCL scripting
</details>

<details>
  <summary><a href="https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%206/README.md" target="_blank">Day 6 - Basics of Static Time Analysis (STA) </a></summary>
  
  #### Timing Analysis Concepts
  * Learned STA fundamentals: setup/hold times, propagation/contamination delays, and their impact on timing.
  * Explored .lib timing models, including delay lookup tables, max transitions, and pin attributes.
  * Studied constraints like clock period, input/output delays, and their impact on critical paths.
  * Investigated unateness, timing sense, and pin-level attributes relevant for synthesis tools.
  * Practiced querying .lib cells and attributes using Design Compiler (DC) shell commands.
  * Analyzed sequential vs. combinational arcs and modeled IO delays for interface timing closure
</details>

<details>
  <summary><a href="https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/README.md" target="_blank">Day 7 - Advanced Constraints </a></summary>
  
  #### Constraint Modeling
  * Clock tree modeling: defined clock period, latency, uncertainty, jitter, and skew for STA precision.
  * Practiced clock creation, querying ports/cells/nets, and analyzing clock propagation using Design Compiler.
  * Learned to define generated clocks and relate them to master clocks for hierarchical clock domains.
  * Applied IO delay modeling: set input/output delays, transitions, and loads to constrain combinational paths.
  * Utilized report_timing, get_*, and TCL scripting to assess design constraints and slack.
  * Built automated constraint scripts for repeated synthesis runs with updated clock and IO specifications.
  * Constrained combinational paths using virtual clocks and set_max_delay to control timing paths
</details>

<details>
  <summary><a href="https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%208/README.md" target="_blank">Day 8 - Logic Optimizations </a></summary>
  
  #### Logic Optimization Techniques
  * Practiced combinational logic optimization techniques, including constant propagation, logic pruning, and redundancy elimination.
  * Analyzed logic simplifications visually using logic cone and waveform analysis.
  * Explored sequential logic optimization such as:
      * Sequential constant detection
      * Removal of unloaded outputs
      * Controlling the sequential optimization

Differentiated between optimizable and non-optimizable sequential patterns
</details>

<details>
  <summary><a href="https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%209/README.md" target="_blank">Day 9 - Report timing </a></summary>
  
  #### Timing Reports & Constraint Validation
  * Learned to use `report_timing` with advanced flags to analyze setup and hold violations at the path and endpoint level.
  * Differentiated timing modes (setup vs. hold) and interpreted waveform-based slack diagnostics.
  * Applied `check_timing`, `report_constraints`, and `report_timing` to validate timing and constraint coverage.
  * Analyzed fanout and capacitance issues in large mux designs using `set_max_capacitance`.
  * Modeled and resolved high fan-out nets (HFNs) with `set_max_transition` and observed impact on buffer tree synthesis
  * Understood how violations are prioritized during optimization using compile_ultra
</details>

<details>
  <summary><a href="https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2010/README.md" target="_blank">Day 10 - Fundamentals SoC Design </a></summary>
  
  #### SoC Architecture & BabySoC Introduction
  * Understood the fundamentals of SoC architecture.
  * Introduced the VSDBabySoC platform, integrating RVMYTH, PLL, and a 10-bit DAC

</details>

<details>
  <summary><a href="https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2011/README.md" target="_blank">Day 11 - VSD BabySoC Modelling Process </a></summary>
  
  #### BabySoC Modeling & Simulation
  * Modeled and simulated the VSDBabySoC, integrating RVMYTH, PLL, and DAC modules.
  * Used Sandpiper-SaaS to convert TL-Verilog RVMYTH into synthesizable Verilog
  * Conducted pre-synthesis simulation using Icarus Verilog; visualized output waveforms via GTKWave
  * Simulated DAC behavior using Verilog’s `real` datatype to represent analog like output
</details>

<details>
  <summary><a href="https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2012/README.md" target="_blank">Day 12 - Post-Synthesis Simulation </a></summary>
  
  #### Gate-Level Verification
  * Understood the importance of Gate-Level Simulation (GLS) in verifying both functionality and timing after synthesis
  * Converted .lib files (avsddac.lib, avsdpll.lib, sky130_fd_sc_hd.lib) to .db using Synopsys Library Compiler (lc_shell).
  * Ran post-synthesis simulation with unit delays using Icarus Verilog and validated functionality with GTKWave.
  * Compared pre-synthesis vs. post-synthesis behavior to confirm functional equivalence and detect synthesis-induced discrepancies
</details>

<details>
  <summary><a href="http://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2013/README.md" target="_blank">Day 13 - PVT Corners Timing Analyses </a></summary>
  
  #### PVT Corners Timing Analysis
  * Understood
</details>
<details>
  <summary><a href="http://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2014/README.md" target="_blank">Day 14 - CMOS Fundamentals </a></summary>
  
  #### CMOS Fundamentals
  * Understood
</details>

<details>
  <summary><a href="http://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2015/README.md" target="_blank">Day 15 - Velocity Saturation and basics of CMOS inverter VTC </a></summary>
  
  #### SPICE Simulations of NMOS and CMOS Circuits
  * Understood
</details>


