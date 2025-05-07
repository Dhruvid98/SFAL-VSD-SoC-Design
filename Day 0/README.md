# Day 0
## Summary of Chip development flow 
### Step 1: Chip Modelling 
* Application creation
  - Creating a software application in the C programming language.
  - Compiling and executing the application to generate output **O0**.
* Modeling specification
  - Creating/ modeling specs in any processor compiler architecture (RISCV-ISA, ARM-ISA, or x86-ISA).
  - Running the application on the modeled  hardware architecture to verify the specifications and generating the output **O1**.
* The goal here is to ensure **O0 = O1**, which can be considered a checkpoint for freezing the specifications.
### Step 2: RTL Architect
<!-- RTL is the abstraction level used to describe digital designs in terms of data flow between registers and the logic that operates on them. It defines the functional behavior of a design. -->
* Describing hardware in HDL using Verilog, Bluespec, or Chisel language.
* Running the same application on UUT and measuring the output **O2**.
* The goal is to verify **O1 =O2**, to make sure that we are maintaining the same functionality. 
### Step 3: SoC Design and Integration
* Using RTL code, we design synthesizable processors and macros, while analog IPs (PLLs and ADCs) are defined at the transistor level.
* SoC Designer integrates the IPs using GPIOs, and the UUT is tested on the integrated SoC to generate output **O3**.
* The output is then compared with O1 and O2 to ensure that the functionality is maintained. 
### Step 4: RTL2GDS
* This step involves floor and power planning, place and route, CTS, and power and signal integrity checks.
* The output of this step is the creation of a GDSII file (Graphic Data System Information Interchange).
### Step 5: Physical verification and Fabrication 
* Physical verification of the GDSII file is done using DRC and LVS checks.
* Later chip is sent for manufacturing to the foundries, also known as TAPOUT.
### Step 6: TAP IN
### Step 7: Post-Silicon Validation
* The chip on the evaluation board is then tested further by driving signals from the onboard peripherals and measuring the output, O4, at the output pin.
* The goal here is to ensure that O1 = O2 = O3 = O4, maintaining consistent functionality throughout. 
### Step 8: System Integration 
* Chip integration to PCB/system, smart watch, smartphone.

## Tool Installation. 
### 1. Ubuntu 24.04 LTS
![Linux image](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%200/Images/Screenshot%202025-05-06%20203035.png)
### 2. Yosys
![Yosys tool](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%200/Images/Screenshot%202025-05-06%20222113.png)
### 3. Iverilog
![Iverilog](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%200/Images/Screenshot%202025-05-06%20222333.png)
### 4. GTKWave
![gtkwave](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%200/Images/Screenshot%202025-05-06%20222831.png)
### 5. OpenSTA
![openSTA](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%200/Images/Screenshot%202025-05-06%20223210.png)
### 6. ngspice
![ngspice](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%200/Images/Screenshot%202025-05-06%20230225.png)
### 7. magic
![magic](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%200/Images/Screenshot%202025-05-06%20232524.png)
### 8. OpenLane
![openLane](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%200/Images/Screenshot%202025-05-07%20130008.png)
