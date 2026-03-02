# Library Cell Design and Characterization Flows

## Cell Design and Characterization
* In an integrated circuit(IC), a **library** is a collection of standard cells defined by parameters such as size, functionality, threshold voltage, and other physical properties. These libraries are essential to the ASIC flow, supporting synthesis, placement, and timing analysis.
* A library consists of different drive strengths of the standard cell.  

![img1](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2022/Images/img1.png)  
![img2](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2022/Images/img2.png)  

### Inputs for cell design 
* Process Design kits (PDKs)
* DRC and LVS rules
* SPICE models
* Library & User-defined specs (e.g., cell height, supply voltage, number of metal layers, pin locations, drawn gate length, etc)
* User-defined specs example
  1. Cell Height: for a given standard-cell architecture, the distance between the power and ground rails directly defines the cell height.  
  2. Cell width: Depends on timing information (e.g., drive strength 1 to X)  
  3. Supply voltage: Specific voltage provided on the top level
  4. Metal layer: From which layer should be created
  5. Pin location: Where the pin location should be present (e.g., near power or ground)
  6. Drawn gate-length
 
### Design Steps
* **Circuit Design:** Develop the transistor-level schematic.
  * Implement the function itself ( Euler's path)
  * Model pmos and NMOS transistors such that they meet the library requirement.
  * **Output** of circuit design is **Circuit description language (CDL)**.

![img3](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2022/Images/img3.png)  

* **Layout Design:** Create the physical layout, adhering to DRC rules.
    * Step 1: Implement the function itself based on pmos and nmos transistors.
    * Step 2: Derive the pmos and NMOS network graph.
    * Step 3: Obtain Euler's path
    * Step 4: Create a stick diagram.
    * Output: GDSII, LEF, Extracted spice netlist (.cir)

![img4](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2022/Images/img4.png)

* **Parasitic Extraction:** Extract parasitics from the layout for accurate modeling.
* **Characterization:** Analyze performance (timing, power, noise).
    * Output: .lib – Characterized library files with timing, power, and noise data
---

### Standard Cell Design Flow

1. Circuit Design – Develop the transistor-level schematic.
2. Layout Design – Create the physical layout adhering to DRC rules.
3. Parasitic Extraction – Extract parasitics from the layout for accurate modeling.
4. Characterization – Analyze performance (timing, power, noise).

**Outputs:**

* CDL – Circuit Description Language (netlist from schematic)
* LEF – Library Exchange Format (abstract layout info for PnR)
* GDSII – Final layout database for fabrication
* .cir – Extracted SPICE netlist
* .lib – Characterized library files with timing, power, and noise data

---

## Standard Cell Characterization Flow
A typical characterization process involves:

 * Step 1: Reading SPICE models and technology files
 * Step 2: Loading the extracted SPICE netlist
 * Step 3: Recognizing functional behavior of the cell
 * Step 4: Identifying subcircuits
 * Step 5: Applying power sources
 * Step 6: Stimulating the cell with test vectors
 * Step 7: Setting output load capacitances
 * Step 8: Running simulations with proper commands (.tran for transient, .dc for dc simulation) 
    
![img6](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2022/Images/img6.png)  
![img5](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2022/Images/img5.png)  
![img7](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2022/Images/img7.png)  

Any input will have 2 kinds of delay. Rise delay and false delay. 

## Propagation Delay

The time difference between the input signal reaching 50% of its final value and the output reaching 50% of its final value.
* If slew is negative, there is a possibility of choosing bad threshold or huge wire delays.   

![img8](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2022/Images/img8.png)  

## Transition Delay

The time it takes for a signal to transition between logic states. Typically measured between 10–90% or 20–80% of the voltage levels (VDD as the reference).  

![img9](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2022/Images/img9.png)  
