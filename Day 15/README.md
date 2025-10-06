# SPICE Simulations CMOS Circuits
* To explore SPICE simulations of NMOS transistors and CMOS inverters across different technology nodes. And comparing the behaviors of long-channel and short-channel devices, as well as analyzing their current–voltage characteristics.

## NMOS Characteristics
* Device Parameters
  * Long Channel: W = 1.8 μm, L = 1.2 μm (W/L = 1.5)
  * Short Channel : W = 0.375 μm, L = 0.25 μm (W/L = 1.5)  

  ![img1](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2015/Images/Observations/img1.png)

### Operation Regions

* Cut of region
  * Vgs =< Vt
  * Area where the device is being cut off.

* Resistive region/ Linear region
    * Id ∝ Vds
    * Valid for Vds < (Vgs – Vt)
    * Drain current is a linear function of Vds

* Saturation region
    * Id ∝ function (1 + λ . Vds)
    * Valid for Vds ≥ (Vgs – Vt)


 ## Observation 1: Long channel vs short channel device
![img2](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2015/Images/Observations/img2.png)  
![img3](https://github.com/Dhruvid98/SFAL-VSD-SoC-Design/blob/main/Day%2015/Images/Observations/img3.png)  

* Long Channel NMOS shows the Drain current (Id) quadratic dependence on Vgs. Whereas Short Channel NMOS Id is quadratic at low Vgs, but becomes linear at high Vgs due to velocity saturation.
* 
