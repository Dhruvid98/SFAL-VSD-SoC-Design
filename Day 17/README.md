# Day 17: Static Behavior Evaluation: CMOS Inverter Robustness and Noise Margin

Introduction to Noise Margin:
* Noise margin is the amount of noise that a CMOS circuit could withstand without any logical errors.

![img1](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2017/Images/img1.png)

Based on the above graph, the following points can be inferred
* Any input voltage level between 0 and VIL, the output voltage will be high
* Any input voltage level between VIH and Vdd, the output voltage will be low or VOL
    * Where VOL is any value between 0 to VIL
* In an ideal case, an inverter with infinite slope switches abruptly at Vdd/2. Whereas practical inverters have a finite slope, creating a **transition region**.

**Realistic VTC inverter** 

![img2](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2017/Images/img2.png)

Based on the above graph, the following points can be inferred
* Any input voltage between 0 to V(IL), output is expected high
* Any input voltage level between V(IH) and Vdd, the output voltage will be low
* V(OL) (valid output low level) : when the input lies between V(IH) and Vdd, we can expect the output to be close to V(OL). And V(OL) value will be less than V(IL).
    * Detected as logic = 0
* V(OH) (valid output high level) : when input voltage is between 0 and V(IL), output is expected to be V(OH) and above. And V(OH) value will be greater than V(IH).
    * Detected as logic = 1
* VIL: Input Low Threshold Voltage (slope = −1)
* VIH: Input High Threshold Voltage (slope = −1)  

![img3](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2017/Images/img3.png)  

**Noise Margin**
* `Noise margin high (NMH)`: Any voltage level that lies between the range of V(OH) and V(IH), either input or output side, will be detected as logic 1.
* `Noise margin low (NML)`: Any voltage level that lies between the range of V(IL) and V(OL), either input or output side, will be detected as logic 0.
* `NMH = VOH − VIH`: tolerance for noise on logic 1
* `NML = VIL − VOL`: tolerance for noise on logic 0

**Undefined Region**
* Between VIL and VIH, the input is undefined. i.e. the value of voltage can either be 1 or 0.
* Noise in this zone may cause unstable or invalid outputs.  

![img4](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2017/Images/img4.png)

**Noise Margin Robustness against variations in Device Ratio**
![img5](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2017/Images/img5.png)  
![img6](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2017/Images/img6.png)  

### Lab: Noise Margin - sky130 Inverter
* File: day4_inv_noisemargin_wp1_wn036.spice

```
*Model Description
.param temp=27


*Including sky130 library files
.lib "sky130_fd_pr/models/sky130.lib.spice" tt


*Netlist Description


XM1 out in vdd vdd sky130_fd_pr__pfet_01v8 w=1 l=0.15
XM2 out in 0 0 sky130_fd_pr__nfet_01v8 w=0.36 l=0.15


Cload out 0 50fF

Vdd vdd 0 1.8V
Vin in 0 1.8V

*simulation commands

.op

.dc Vin 0 1.8 0.01

.control
run
setplot dc1
display
.endc

.end
```

![img7](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2017/Images/img7.png)  

* VTC curve waveform for Noise margin. 
