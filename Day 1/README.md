# Day 1: Functional Verification and Synthesis of 2x1 MUX. 

## Introduction to simulator Iverilog and GTKWave. 
* **Iverilog** is an open-source simulator tool used to verify whether an RTL design adheres to the specified requirements by simulating the design's functionality.
* **GTKWave** is used to view the waveform.
* **Yosys** is a synthesizing tool used to convert RTL into a netlist. 
* Iverilog based simulation flow
![image](https://github.com/user-attachments/assets/91202d92-99b0-4e1f-8d3f-ea9025417d07)

## Process

**Step 1** : Passing RTL design and corresponding testbench to Iverilog simulator

![RTL iverilog](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%201/Mux%202%3A1%20Images/Functional%20Veri/Screenshot%202025-05-11%20205940.png)

**Step 2** : Generating vcd(value change dump) file

![vcd file](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%201/Mux%202%3A1%20Images/Functional%20Veri/Screenshot%202025-05-11%20205923.png)

**Step 3** : Visualizing the variables dumping into a VCD file with GTKwave

![running gtkwave](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%201/Mux%202%3A1%20Images/Functional%20Veri/Screenshot%202025-05-11%20205907.png)

**Step 4** : Simulation waveform

![simulation waveform](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%201/Mux%202%3A1%20Images/Functional%20Veri/Screenshot%202025-05-11%20205825.png)

**Step 5** : Reading standard cell library

![reading std](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%201/Mux%202%3A1%20Images/Design%20Synthesis/Screenshot%202025-05-13%20230733.png)

**Step 6** : Reading RTL Design

![rtl read](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%201/Mux%202%3A1%20Images/Design%20Synthesis/Screenshot%202025-05-13%20230753.png)

**Step 7** : Synthesizing Design (Top module that is getting synthesized)

![top module](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%201/Mux%202%3A1%20Images/Design%20Synthesis/Screenshot%202025-05-13%20230920.png)

![synthesizied design](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%201/Mux%202%3A1%20Images/Design%20Synthesis/Screenshot%202025-05-13%20231132.png)

**Step 8** : Linking synthesized design to standard cell library 

![link to std](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%201/Mux%202%3A1%20Images/Design%20Synthesis/Screenshot%202025-05-13%20231605.png)

![report](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%201/Mux%202%3A1%20Images/Design%20Synthesis/Screenshot%202025-05-13%20231619.png)

**Step 9** : View Synthesized 2x1 MUX using show command

![show command](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%201/Mux%202%3A1%20Images/Design%20Synthesis/Screenshot%202025-05-13%20231655.png)
![logic made](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%201/Mux%202%3A1%20Images/Design%20Synthesis/Screenshot%202025-05-13%20231713.png)

**Step 10**: Writing gate-level netlist to a file using the write_verilog command

![write gate level netlist](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%201/Mux%202%3A1%20Images/Design%20Synthesis/Screenshot%202025-05-13%20231759.png)

**Step 11** : Gate level Netlist file for 2x1 MUX

![netlist file](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%201/Mux%202%3A1%20Images/Design%20Synthesis/Screenshot%202025-05-13%20231759.png)

