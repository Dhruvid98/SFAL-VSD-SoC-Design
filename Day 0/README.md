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
* Describing hardware in HDL using Verilog, Bluespec, or Chisel.
* 
### Step 3: SoC Integration
### Step 4: RTL2GDS
### Step 5: Physical verification and Fabrication 
### Step 6: Post-Silicon Validation
* Hardware validation on evaluation boards
### Step 7: System Ingetration 
* Consumer electronics
* Chip integration to PCB/system, smart watch, smartphone
