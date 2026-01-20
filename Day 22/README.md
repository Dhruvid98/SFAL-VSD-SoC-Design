# Library Cell Design and Characterization Flows

## Cell Design and Characterization
* In an integrated circuit(IC), a **library** is a collection of standard cells defined by parameters such as size, functionality, threshold voltage, and other physical properties. These libraries are essential to the ASIC flow, supporting synthesis, placement, and timing analysis.
* A library consists of different drive strengths of the standard cell.

![img1]()
![img2]()

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
* Circuit Design:  Develop the transistor-level schematic.
  * Implement the function itself ( Euler's path)
  * Model pmos and nmos transistor such that they meet the library requirement.
  * Output of circuit design is circuit description language (CDL)
![img3]()
* Layout Design: Create the physical layout, adhering to DRC rules.
* Characterization 
