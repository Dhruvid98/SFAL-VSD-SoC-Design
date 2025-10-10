# Day 17: Static Behavior Evaluation: CMOS Inverter Robustness and Noise Margin

Introduction to Noise Margin:
* Noise margin is the amount of noise that a CMOS circuit could withstand without any logical errors.

![img1]()

Based on the above graph, the following points can be inferred
* Any input voltage level between 0 and VIL, the output voltage will be high
* Any input voltage level between VIH and Vdd, the output voltage will be low or VOL
    * Where VOL is any value between 0 to VIL
* In an ideal case, an inverter with infinite slope switches abruptly at Vdd/2. Whereas practical inverters have a finite slope, creating a **transition region**.

**Realistic VTC inverter** 

![img2]()

Based on the above graph, the following points can be inferred
* Any input voltage between 0 to V(IL), output is expected high
* Any input voltage level between V(IH) and Vdd, the output voltage will be low
* V(OL) (valid output low level) : when the input lies between V(IH) and Vdd, we can expect the output to be close to V(OL). And V(OL) value will be less than V(IL).
    * Detected as logic = 0
* V(OH) (valid output high level) : when input voltage is between 0 and V(IL), output is expected to be V(OH) and above. And V(OH) value will be greater than V(IH).
    * Detected as logic = 1
* VIL: Input Low Threshold Voltage (slope = −1)
* VIH: Input High Threshold Voltage (slope = −1)
