# Combinational and Sequential Optimization 

## Introduction to Optimization 
### Combinational Optimization
* Why does the combination logic need optimization?
  - Mainly to squeeze the logic into the most optimized design.
  - Optimized designs are efficient in terms of *Area and Power* saving.

* Techniques for optimization:-
    - Constant Propagation
        * Directly simplifying logic paths when input constants are known
![const](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%203/Images/Introduction/Constant.png)
    - Boolean logic optimization
        * K- Map ((Karnaugh Map))
        * Quine McKluskey Algo.
![bool](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%203/Images/Introduction/boolean.png)

### Sequential logic Optimization

* Techniques used:
  - Basic
  - Advanced
      * State Optimization: Reduces the number of states in Finite State Machines (FSMs), thereby minimizing area usage and transition overhead.
      * Retiming: Rearranging registers across combinational logic without altering the circuit's functioning to balance the logic delay and improve timing performance.
      * Sequential Logic Cloning (Floor Plan-Aware Synthesis): This technique improves timing and physical implementation by replicating/ cloning sequential elements (registers) across the chip layout.

Example of sequential constant propagation shown below in a D flip flop with asynchronous reset, where the D input is grounded. The output of Q is always constant i.e. 0.. Whereas the same technique cannot be applied to D flip flop with the asynchronous set because while Q=1 when Set=1, but Q=0 at Set=0 at the next CLK pulse. Q is dependent not only on Set but also on the clock edge. 
![basic](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%203/Images/Introduction/sequen_basic.png)
