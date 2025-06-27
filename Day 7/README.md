# Day 7 - Advanced Constraints

<details>
    <summary>1. Clock Tree Modelling and IO Delays </summary>

## Clock Tree Modelling and Uncertainty

* Basic constraints
    - Reg2Reg - Clock period
    - Input to Reg - Clock period, Input delay and Input transition
    - Reg to Output - Clock period, Output delay and Output transition

### What needs to be constrained for the clock ?
Clock period. As the clock period limits the time taken. 

* Will the clock arrive at the same time to the flop?
    - In a real scenario, definitely **NO**. The clock is built only during CTS; before that, the clock is an ideal network. But the clock doesn't reach all the flops at the same time. During synthesis, logic is optimized considering an ideal clock network. Should synthesis consider the practicality of the clock network?
      
![img1](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/Clock_tree_uncertainty/img1.png)

### Clock Generation and Jitter

* **Jitter**: Stochastic variations of the clock generator.
![img2](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/Clock_tree_uncertainty/img2.png)

### Clock Distribution and Skew

* **Skew**: The Timing difference between when a clock signal arrives at one flip-flop versus another within the same clock domain.
![img3](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/Clock_tree_uncertainty/img3.png)

![img4](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/Clock_tree_uncertainty/img4.png)  

### Factors for Clock Modelling  

![img5](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/Clock_tree_uncertainty/img5.png)  
![img6](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/Clock_tree_uncertainty/img6.png)  

## IO delays. 

![img1](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/IO%20delays/img1.png)

### Getting the Ports and Clock in DC

![img2](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/IO%20delays/img2.png)
![img3](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/IO%20delays/img3.png)

### Querying the cells in the design 
- Hierarchical pins are nets

![img4](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/IO%20delays/img4.png)  

### Clock Distribution 

![img5](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/IO%20delays/img5.png)  
![img6](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/IO%20delays/img6.png)

### Creating Clock 
- Here DC: Duty Cycle.
  
![img7](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/IO%20delays/img7.png)

### Constraining IO Paths

![img8](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/IO%20delays/img8.png)  
![img9](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%207/Images/IO%20delays/img9.png)  

</details>

<details>
    <summary>2. Labs 8–12: Design Loading, Clock Creation & Timing Characterization </summary>

</details>
