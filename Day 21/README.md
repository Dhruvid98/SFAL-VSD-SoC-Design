# Advanced Physical Design using OpenLane

#### Open Source implementation 
For open-source ASIC design implementation, the following enablers are required. They are:- RTL Designs, EDA Tools and PDK Data. 

The interface between the designers and the fab has become a set of data files and documents, which are referred to as the "Process Design Kits (PDKs)".
The PDK includes Device Models, Technology Information, Design Rules, Digital Standard Cell Libraries, I/O Libraries and many more.  
![img2](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2021/Images/img2.png)  

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
![img1](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2021/Images/img1.png)  

OpenLane is an open-source framework that transforms RTL designs into manufacturable layouts by integrating all major stages of the digital IC design process.

* Front-End: RTL synthesis is performed using Yosys and ABC, followed by static timing analysis (STA) with OpenSTA. Design for Testability (DFT) is implemented to ensure fault coverage, and Yosys also supports Logic Equivalence Checking (LEC) for correctness verification.  
![img3](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2021/Images/img3.png)  

* Physical Design: The OpenROAD App handles floorplanning, powerplanning, placement, clock tree synthesis (CTS), optimization, and global routing. TritonRoute performs detailed routing, while custom scripts manage the insertion of antenna diodes.
  * In global placement provide approximate locations for all cells based on connectivity but in this stage the cells may be overlapped on each other and in detailed placement the positions obtained from global placements are minimally altered to make it legal (non-overlapping and in site-rows)

![img4](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2021/Images/img4.png)  
![img5](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2021/Images/img5.png)   
![img6](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2021/Images/img6.png)  
![img7](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2021/Images/img7.png)  
![img8](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2021/Images/img8.png)  
![img9](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2021/Images/img9.png)  
![img10](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2021/Images/img10.png)  

* Signoff: STA includes RC extraction, with STA re-run to confirm timing. Magic and Netgen provide physical verification through Design Rule Checking (DRC) and Layout vs. Schematic (LVS) comparisons.  
![img11](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2021/Images/img11.png)  

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
* Exporting the PDK_ROOT variable to point to sky130A PDK
```
export PDK_ROOT=/home/saad/soc-design-and-planning-nasscom-vsd/Desktop/work/tools/openlane_working_dir/pdks
```
![img12]()  

* Change directory to the OpenLANE flow working directory and running openlan interractive shell.
```
cd OpenLane ( this is where Docker is installed)
make mount
./flow.tcl -interactive -design designs/picorv32a

```
![img13]()   

* Prep the design
```
prep -design picorv32a
```
![img14]()  

* Run Synthesis
```
run_synthesis
```
![img15]()  
![img16]()  


#### Calculate the flop ratio.
![img17]()   
![img18]()  

* Flop Ratio and DFF % Calculation from Synthesis Statistics Report File  
Total Cells = 16885   
DFF Cells = 1613  

 $$
\text{Flop Ratio} = \frac{\text{DFF Cells}}{\text{Total Cells}}
= \frac{1613}{16885}
= 0.095528
$$
 
$$
\text{Percentage of DFFs}
= \text{0.095528} * 100
= 9.55\%
$$


#### Run Floorplan 
```
run_floorplan
```
![img19]()  
![img20]()  

#### View Floorplan DEF in Magic

