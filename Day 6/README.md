# Day 6: Basics of Static Time Analysis (STA)
## Introduction to STA.
### Minimum and Maximum delay constraints
![min_max_delay](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%206/Images/min_max_delay_constraint.png)  
* Setup time: Propagation delay helps make sure data arrives in time for setup.
* Hold time: Contamination delay helps make sure data doesn’t arrive too early, violating hold time.

### Water Bucket Analogy for Delay
1. The inflow of water translates to the inflow of current. Fast current sourcing (fast rise time of input) => less delay.
2. Delay is directly proportional to load capacitance  
So, delay is a function of input transition (inflow) and load capacitance (the size of the bucket).

![water_a_1](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%206/Images/water_a_1.png)  
![water_a_2](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%206/Images/water_a_2.png)  
![delay](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%206/Images/delay.png)  

### Timing Arcs
* Timing arcs provide delay information

![combi_delay](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%206/Images/timing_Arc_combi.png)  
![seq_delay](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%206/Images/timing_arc_seq.png)  
![diff](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%206/Images/timiing_arc_latch_ffp.png)
