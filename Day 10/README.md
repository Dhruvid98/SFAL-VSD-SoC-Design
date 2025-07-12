# Day 10: Fundamentals of SoC Design

## Problem Statement 
This project explores the design of a small, open-source System on Chip (SoC) built around RVMYTH (RISC-V processor). This SoC will leverage a Phase-Locked Loop (PLL) as a clock generator and controller, and a 10-bit Digital-to-Analog Converter (DAC) to help the chip interact with the real world. Devices like televisions and mobile phones that accept analog input can process the DAC output to deliver music or display video frames. In the end, the open-source SoC built using Sky130 technology offers a well-documented platform ideal for educational use and hands-on learning.

## What is SOC
An SoC is a single die that integrates multiple IP cores. These IPs could vary from microprocessors (digital) to 5G broadband modems (analog). 

### Key Components 
**1. CPU (Central Processing Unit) :**  The Brain  of the SoC, handling all main instructions and decisions.  
**2. Memory:** RAM (Random Access Memory) and ROM/Flash Storage.  
**3. I/O Ports (Input/Output):**  Connects the SoC to other parts or devices, eg USB.  
**4. Graphics Processing Unit (GPU):** Creates visuals on your screen.  
**5. Digital Signal Processor (DSP):** Used for processing audio and video signals.  
**6. Power Management:** Manages power consumption within the SoC to ensure efficient and optimized chip operation.  

### Types of SoC
  1. Microcontroller-based SoC : These SoCs are centered on a microcontroller and designed for basic control functions in common devices. They are recognized for their low power consumption and efficiency.
  2. Microprocessor-based SoC: This category includes a microprocessor that can manage more advanced tasks and operate full operating systems. These SoCs enable multitasking and run complex applications
  3. Application-Specific SoC: These SoC is designed specifically for high-performance tasks. The SoCs excel in fields such as graphics processing, network management, and multimedia applications. They are optimized for speed and efficiency.

* SoC Design flow  
![img1](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2010/Images/Intro/img1.png)

<details>
    <summary> Introduction to VSDBabySoC Modelling </summary>
  
## Introduction to VSDBabySoC
VSDBabySoC is a powerful RISCV-based SoC. The main purpose of designing such a small SoC is to test three open-source IP cores together for the first time and calibrate the analog part of it. It contains one `RVMYTH microprocessor`, an `8x-PLL` to generate a stable clock, and a `10-bit DAC` to communicate with other analog devices.  

![img2](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2010/Images/Intro/img2.png)  

### What is RVMYTH
* RVMYTH is an open-source RISC-V CPU design. Its a customizable CPU that performs processing tasks and interacts with other elements within the SoC.
* RVMYTH works as the brain of BabySoC

### What is PLL
* A Phase-Locked Loop(PLL) is a system that creates an output signal that stays in sync with an input signal. It's often used to keep clocks running at the correct speed and to ensure that different parts of a chip stay in sync with each other.
* The PLL generates a stable clock signal to keep all components in BabySoC synchronized. It aligns the SoC’s internal clock with a reference frequency, ensuring accurate timing for both the RVMYTH processor and the DAC.

### What is DAC
* A digital-to-analog converter(DAC) is a system that converts a digital signal into an analog signal.
* The DAC takes digital signals from the RVMYTH processor and turns them into analog signals, like sound or pictures. This lets BabySoC work with devices like speakers or screens that use analog signals.

### Modeling VSDBabySoC 

* Model and simulate the VSDBabySoC using iverilog, then we will show the results using gtkwave tool.
* Providing initial input signals to the vsdbabysoc module, which triggers the PLL to begin generating the appropriate clock (CLK) signal for the circuit.
* The clock signal will make the `RVMYTH` to execute instructions in its memory.
* As a result, the `r17` register is updated with new values on each clock cycle. These values are then used by the DAC core to generate the final output signal, `OUT`.

#### Modelling of RVMYTH
* RVMYTH is written in TL-Verilog, but we need to convert it to Verilog so that its results can be used SoC
* Here Sandpiper saas is used to translate into verilog. 

[Model the RVMYTH](https://github.com/shivanishah269/risc-v-core)


</details>
