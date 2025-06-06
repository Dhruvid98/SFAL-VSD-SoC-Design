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

What will be the correct implementation based on different implementation 
![implement option](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%205/Image/Intro/different_implement.png)  

Standard cell details for each cell.
![std_cell_details](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%205/Image/Intro/std_Cell_detail.png)  

Implementation 3 is the best scenario based on below screen shot.
![implement]()  

* But will implementation 3 will always the best case?
   - No. It depends on if the logic is present in the hold-sensitive path or if additonal buffers are added then it will add to both power and area.  

All three implementations are valid, and the choice will be made depending on the requirements. The *constraints* define these needs. The synthesizer is guided by constraints to choose the library cells that are most suited for the design.
