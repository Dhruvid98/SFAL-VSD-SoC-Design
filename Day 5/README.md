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
