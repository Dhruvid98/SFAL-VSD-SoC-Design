# SFAL-VSD SoC Design Program
Welcome to the repository documenting my journey through the SoC Design. This repository documents my hands-on progress, key takeaways, and daily explorations in digital hardware design. It covers topics from tool installation to advanced SoC design and implementation.

<details>
  <summary><a href="https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%200/README.md" target="_blank">Day 0 - Tools Installation</a></summary>
  
  #### Key Takeaways
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
  
  #### Key Takeaways
  * Simulated a 2:1 MUX RTL design using Icarus Verilog and visualized waveforms with GTKWave.
  * Synthesized the design using Yosys, linking it to a standard cell library.
  * Generated and reviewed the gate-level netlist for the synthesized MUX.
  * Gained hands-on experience with the flow: from HDL simulation to gate-level synthesis
</details>

<details>
  <summary><a href="https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%202/README.md" target="_blank">Day 2 - Timing Libraries, Hierarchical vs Flat Synthesis, Efficient Flop Coding Styles</a></summary>
  
  #### Key Takeaways
  * Explored standard cell timing libraries (.lib files) and understood PVT-based behavior modeling.
  * Compared hierarchical vs. flat synthesis flows and analyzed structural outcomes.
  * Practiced submodule-level synthesis for modular design and reuse.
  * Simulated and synthesized flip-flops with both async/sync resets and sets.
  * Implemented ×2 and ×9 multipliers using bit manipulation to avoid combinational logic
</details>

<details>
  <summary><a href="https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%203/README.md" target="_blank">Day 3 - Combinational and Sequential Optimizations </a></summary>
  
  #### Key Takeaways
  * Applied combinational optimization techniques like constant propagation, Boolean logic simplification, and Karnaugh mapping to minimize area and gate count.
  * Practiced sequential logic optimization, including retiming, state minimization, and logic cloning to improve performance and layout efficiency.
  * Demonstrated optimization limits using flip-flop designs with specific reset/set behaviors and interdependencies.
  * Identified and optimized unused outputs in sequential blocks (e.g., 3-bit counter using only q[0]), leading to fewer synthesized flops.
</details>

<details>
  <summary><a href="https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%204/README.md" target="_blank">Day 4 - GLS, Blocking vs Non-Blocking, Synthesis-Simulation Mismatch </a></summary>
  
  #### Key Takeaways
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
  
  #### Key Takeaways
  * Set up Ngspice and Magic; configured environment for simulation and layout tools
</details>

<details>
  <summary><a href="https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%206/README.md" target="_blank">Day 6 - Basics of Static Time Analysis (STA) </a></summary>
  
  #### Key Takeaways
  * Set up Ngspice and Magic; configured environment for simulation and layout tools
</details>

<details>
  <summary><a href="https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/README.md" target="_blank">Day 7 - Advanced Constraints </a></summary>
  
  #### Key Takeaways
  * Set up Ngspice and Magic; configured environment for simulation and layout tools
</details>

<details>
  <summary><a href="https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%208/README.md" target="_blank">Day 8 - Logic Optimizations </a></summary>
  
  #### Key Takeaways
  * Set up Ngspice and Magic; configured environment for simulation and layout tools
</details>

<details>
  <summary><a href="https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%209/README.md" target="_blank">Day 9 - Report timing </a></summary>
  
  #### Key Takeaways
  * Set up Ngspice and Magic; configured environment for simulation and layout tools
</details>

<details>
  <summary><a href="https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2010/README.md" target="_blank">Day 10 - Fundamentals SoC Design </a></summary>
  
  #### Key Takeaways
  * Set up Ngspice and Magic; configured environment for simulation and layout tools
</details>

<details>
  <summary><a href="https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2011/README.md" target="_blank">Day 11 - VSD BabySoC Modelling Process </a></summary>
  
  #### Key Takeaways
  * Set up Ngspice and Magic; configured environment for simulation and layout tools
</details>

<details>
  <summary><a href="https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2012/README.md" target="_blank">Day 12 - Post-Synthesis Simulation </a></summary>
  
  #### Key Takeaways
  * Set up Ngspice and Magic; configured environment for simulation and layout tools
</details>

