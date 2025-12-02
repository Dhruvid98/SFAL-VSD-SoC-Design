# Advanced Physical Design using OpenLane

#### Open Source implementation 
For open-source ASIC design implementation, the following enablers are required. They are:- RTL Designs, EDA Tools and PDK Data. 

The interface between the designers and the fab has become a set of data files and documents, which are referred to as the "Process Design Kits (PDKs)".
The PDK includes Device Models, Technology Information, Design Rules, Digital Standard Cell Libraries, I/O Libraries and many more.  
![img2]()  

#### ASIC flow
ASICs (Application-Specific Integrated Circuits) are chips designed for a specific purpose, unlike general-purpose processors. An example in cars, the airbag controller is often an ASIC that continuously monitors sensors and triggers airbag deployment within microseconds, designed for reliability and safety rather than flexibility. Designing an ASIC is a complex process supported by Electronic Design Automation tools and typically takes several months to complete. 

**The standard flow:**

* Design Entry:  Describe the logic in an HDL (Verilog/SystemVerilog) at the RTL or behavioral level.

* Functional Verification:  Validate correctness through simulation or formal methods, both at RTL and netlist levels.

* Synthesis: Convert the RTL code into a gate-level netlist using standard logic cells.

* Physical Implementation (PnR):  Transform the netlist into a chip layout with steps like floorplanning, powerplanning, placement, clock tree synthesis, and routing. 

* Signoff:  Final checks for functionality, timing, power, and manufacturability before fabrication.

Additional DFT steps, such as scan chain insertion and test pattern generation, are essential for testing the fabricated chip against defects.

#### OpenLANE ASIC design flow:  
![img1]()  

OpenLane is an open-source framework that transforms RTL designs into manufacturable layouts by integrating all major stages of the digital IC design process.

* Front-End: RTL synthesis is performed using Yosys and ABC, followed by static timing analysis (STA) with OpenSTA. Design for Testability (DFT) is implemented to ensure fault coverage, and Yosys also supports Logic Equivalence Checking (LEC) for correctness verification.  
![img3]()  

* Physical Design: The OpenROAD App handles floorplanning, powerplanning, placement, clock tree synthesis (CTS), optimization, and global routing. TritonRoute performs detailed routing, while custom scripts manage the insertion of antenna diodes.
  * In global placement provide approximate locations for all cells based on connectivity but in this stage the cells may be overlapped on each other and in detailed placement the positions obtained from global placements are minimally altered to make it legal (non-overlapping and in site-rows)

![img4]()  
![img5]()  
![img6]()  
![img7]()  
![img8]()  
![img9]()  
![img10]()  

* Signoff: STA includes RC extraction, with STA re-run to confirm timing. Magic and Netgen provide physical verification through Design Rule Checking (DRC) and Layout vs. Schematic (LVS) comparisons.  
![img11]()  

* Output: The design flow ultimately generates GDSII and LEF files, leveraging the SkyWater PDK for process-specific libraries and technology data.

Additional design exploration and synthesis exploration steps are essential to choose the best configuration and correct synthesis strategy for the ASIC. 

#### OpenLANE Synthesis Flow Commands for picorv32a design:

* Clone the project setup:
```
git clone https://github.com/fayizferosh/soc-design-and-planning-nasscom-vsd
```

* Build and install the OpenPDKs for the Sky130:
```
git clone https://github.com/RTimothyEdwards/open_pdks.git
cd open_pdks
./configure --enable-sky130-pdk
make
sudo make install
```
