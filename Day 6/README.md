# Day 6: Basics of Static Time Analysis (STA)

## Introduction to STA.
### Minimum and Maximum delay constraints
![min_max_delay](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%206/Images/min_max_delay_constraint.png)  
* Setup time: Propagation delay helps make sure data arrives in time for setup.
* Hold time: Contamination delay helps make sure data doesn’t arrive too early, violating hold time.

### Water Bucket Analogy for Delay
1. The inflow of water translates to the inflow of current. Fast current sourcing (fast rise time of input) => less delay.
2. Delay is directly proportional to load capacitance

So, delay is a function of **input transition (inflow)** and **load capacitance (the size of the bucket)**.

![water_a_1](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%206/Images/water_a_1.png)  
![water_a_2](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%206/Images/water_a_2.png)  
![delay](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%206/Images/delay.png)  

### Timing Arcs
* Timing arcs provide delay information

![combi_delay](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%206/Images/timing_Arc_combi.png)  
![seq_delay](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%206/Images/timing_arc_seq.png)  
![diff](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%206/Images/timiing_arc_latch_ffp.png)

## What are constraints? 
The `critical path` determines the maximum achievable clock frequency in a design. The critical path is used to determine the clock frequency. If the critical path delay is reduced, a better frequency can be achieved. We need to tell the tools to pick library cells with specific delays. This is defined through constraints.  

![timing_Arc](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%206/Images/Constraints/timings_arc.png)  
![img2](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%206/Images/Constraints/img2.png)  
![img3](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%206/Images/Constraints/img3.png)  

* How much delay is acceptable? How to control that?

- Assuming a clock frequency of 500 MHz (corresponding to a 2 ns clock period), and considering that each flip-flop introduces a delay of 0.5 ns, the total sequential element delay would be 1 ns. This leaves only 1 ns available for the combinational logic within the clock cycle. As illustrated in the screenshot below, it is ultimately the clock period that constrains the allowable delay for the combinational logic in the timing path.  

![img4](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%206/Images/Constraints/img4.png)  

**Constraints that can be specified**  

*1. The constraint given to the synthesis tool is the `acceptable clock period as constraint`. So the tool will pick appropriate cells for the combinational logic.*  

*2. Input constraint* 

![img5](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%206/Images/Constraints/img5.png) 

*3. REG3 drives its output to an external flip-flop, REG_EXT_3, through the Output Logic, with both flip-flops clocked by the same clock signal, CLK. This forms a synchronous timing path. To ensure proper timing, the delay introduced by the Output Logic must be kept within allowable limits. Therefore, it is essential to apply appropriate constraints on the output path to control its timing behavior.* 

![img6](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%206/Images/Constraints/img6.png)  

![img7](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%206/Images/Constraints/img7.png)  

*4. We can constrain the I/O logic by specifying input external delay and output external delays relative to the associated `clock (CLK)`. This helps ensure timing requirements are met at the interface boundaries.*

Sources of I/O Delay Modeling:

* Standard Interface Specifications:
    - Delays defined by communication standards such as I2C, SPI, etc.

* I/O Budgeting:
    - Delay allocation based on interaction and timing alignment with other functional modules in the system.
![img8](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%206/Images/Constraints/img8.png)

## Input Transition and Output Load

#### Is IO Delay Modeling Sufficient?

The screenshot below represents the clock period at the rising edge of `EXT_1`, accounting for external delay but assuming ideal signals.  
![img9](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%206/Images/Constraints/img9.png)  

The setup violation, observed with practical signals, is shown in the screenshot below.  
![img10](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%206/Images/Constraints/img10.png)  
![img11](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%206/Images/Constraints/img%2011.png)
![img12](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%206/Images/Constraints/img12.png)  

As a thumb rule, 70% of the clock period is allocated for external delays and 30% for internal delays.  

![img13](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%206/Images/Constraints/img13.png)  

## Lab5 : Timing .Libs

### Contents present in .lib file

* Technology: CMOS
* PVT condition
    - Process, Voltage and Temperature information
  
#### Max Transition 
```
Example 
default_max_transition : 1.5000000000;
```

The **Output** has an `output pin capacitance`, `net capacitance`, and there is `input capacitance` at the next gate or `sum of all input capacitance` for fan out. If the library has a max capacitance limit of 1.5pF, the DC will use this value to limit the maximum capacitance. And if the limit is violated, DC will divide the net and add a buffer in the path as shown in the green diagram.  

![img1](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%206/Images/.lib_file/img_1.png)  

#### Delay Model Look up Model 
```
delay_model : "table_lookup";
```
![img2](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%206/Images/.lib_file/img2.png)

* Pin attributes
    - Attributes associated with the pin such as whether it is clock or not, pin capacitance, direction, max_transition, rise_power/ fall power lookup tables and more  
  ![img3](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%206/Images/.lib_file/img3.png)

#### Unateness
```
timing_sense : "positive_unate";
timing_type : "combinational" (cmobinational timing arc)
```
* Why is unateness important?
    - Unateness is important because that's how the tool will understand how to propagate transitions.
    - By using unateness information, DC tool will generate a transition.
    - `timing_sense : "non_unate"` - non_unate means concerning clock Q may be rising or falling (called no unateness).

  ![img4](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%206/Images/.lib_file/img4.png)

## Lab6: Exploring .lib (Part 1)
* `CLK_N` is the active-low clock. The attribute clock is `true`
* Sequential timing arc
  - `timing_type : "falling_edge"` - (Negative edge clock)
  - `timing_type : "rising_edge"` - (Positive edge clock)  

![img1](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%206/Images/Lab2/img1.png)  
![img2](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%206/Images/Lab2/img2.png)  

* Unlike flip-flops, latches sample data at different points within the clock cycle, as shown in the screenshot below.

![img3](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%206/Images/Lab2/img3.png)
![img4](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%206/Images/Lab2/img4.png)  

## Lab6: Exploring .lib (Part 2)
