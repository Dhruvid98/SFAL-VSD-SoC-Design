# Day 11: VSD BabySoC Modelling Process

<details>
  <summary> BabySoC Modelling Process </summary>  

* We adjust the digital output value, either by increasing or decreasing it, and then feed it to the DAC model to observe the changes SoC output.

1. Script to install the packages.

* vsdbabysoc.v (Top-Level SoC Module)
```
   $ sudo apt install make python python3 python3-pip git iverilog gtkwave docker.io
   $ sudo chmod 666 /var/run/docker.sock
   $ cd ~
   # Install virtual environment package if not already available
   $ sudo apt install python3-venv -y
   # Create a virtual environment
   $ python3 -m venv myenv
   # Activate it virtual env
   $ source myenv/bin/activate
   # Installing the package
   $ pip install pyyaml click sandpiper-saas

```

2. Cloning this repository VSDBabySoC repository
```
$ cd ~
$ git clone https://github.com/manili/VSDBabySoC.git
```

   </details>
