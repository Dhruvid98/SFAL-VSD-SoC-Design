# Day 7 - Advanced Constraints

## 1. Clock Tree Modelling and IO Delays

### Clock Tree Modelling and Uncertainty

* Basic constraints
    - Reg2Reg - Clock period
    - Input to Reg - Clock period, Input delay and Input transition
    - Reg to Output - Clock period, Output delay and Output transition

#### What needs to be constrained for the clock ?
Clock period. As the clock period limits the time taken. 

* Will the clock arrive at the same time to the flop?
    - In a real scenario, definitely **NO**. The clock is built only during CTS; before that, the clock is an ideal network. But the clock doesn't reach all the flops at the same time. During synthesis, logic is optimized considering an ideal clock network. Should synthesis consider the practicality of the clock network?
      
![img1](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/Clock_tree_uncertainty/img1.png)

#### Clock Generation and Jitter

* **Jitter**: Stochastic variations of the clock generator.
![img2](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/Clock_tree_uncertainty/img2.png)

#### Clock Distribution and Skew

* **Skew**: The Timing difference between when a clock signal arrives at one flip-flop versus another within the same clock domain.
![img3](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/Clock_tree_uncertainty/img3.png)

![img4](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/Clock_tree_uncertainty/img4.png)  

#### Factors for Clock Modelling  
![img5](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/Clock_tree_uncertainty/img5.png)  
![img6](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/Clock_tree_uncertainty/img6.png)

