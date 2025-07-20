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

2. Cloning the VSDBabySoC repository
```
$ cd ~
$ git clone https://github.com/manili/VSDBabySoC.git
```

3. Make the `pre_synth_sim.vcd`:
```
$ cd VSDBabySoC
$ make pre_synth_sim
```
* Here `make pre_synth_sim` internally calls `sandpiper-saas -i src/module/rvmyth.tlv -o rvmyth.v --bestsv --noline -p verilog --outdir output/compiled_tlv` which is ued to convert TLV RVMYTH processor into verilog.
* The simulation result is stored in `output/pre_synth_sim` directory i.e. `pre_synth_sim.vcd`
![img1]()

4. Analyzing `pre_synth_sim.vcd` waveforms by following the command:
```
$ gtkwave output/pre_synth_sim/pre_synth_sim.vcd
```

![img2]()

   </details>
