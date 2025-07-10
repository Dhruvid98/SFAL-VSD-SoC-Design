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

