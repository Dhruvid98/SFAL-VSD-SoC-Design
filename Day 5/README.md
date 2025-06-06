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
![into_pic1]()  

**.LIB file**
*.lib file is a collection of standard cells.
![.lib why]()

### Why do we need different flavors of cells?
![why different]()  
![diff between fast and slow]()

### How to select cells 
* The guidance offered to the synthesizer in the form of  **CONSTRAINTS**
![synthesizer]()

Example of synthesis 
![example of syn]()  

What will be correct implementation based on different implementation 
![implement option]()  

Standard cell details for each cell.
![std_cell_details]()  

Implementation 3 is the best scenario based on below screen shot.
![implement]()  

* But will implementation 3 will always the best case?
   - No. It depends on if the logic is present in the hold-sensitive path or if additonal buffers are added then it will add to both power and area.  

All three implementations are valid, and the choice will be made depending on the requirements. The *constraints* define these needs. The synthesizer is guided by constraints to choose the library cells that are most suited for the design.
