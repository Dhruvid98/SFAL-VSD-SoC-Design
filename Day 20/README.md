
# Floorplan and Placement of VSDBabySoC in OpenROAD
* Below steps where perfomed to for Floorplan and placement of VSDBabaySoC.
    * Creating a directory vsdbabysoc inside OpenROAD-flow-scripts/flow/designs/sky130hd
    * Create a directory vsdbabysoc inside OpenROAD-flow-scripts/flow/designs/src and include all the verilog files here.
        * The verilog files conents : copy the folders gds, include, lef and lib from the VSDBabySoC folder, copy of constraints file(vsdbabysoc_synthesis.sdc) and copy the files(macro.cfg and pin_order.cfg) from VSDBabySoC folder.
* Creating below config.mk file(path : sky130hd/vsdbabysoc/):
```
export DESIGN_NICKNAME = vsdbabysoc
export DESIGN_NAME = vsdbabysoc
export PLATFORM    = sky130hd
export DESIGN_HOME = $(FLOW_HOME)/designs
# export VERILOG_FILES_BLACKBOX = $(DESIGN_HOME)/src/$(DESIGN_NICKNAME)/IPs/*.v
# export VERILOG_FILES = $(sort $(wildcard $(DESIGN_HOME)/src/$(DESIGN_NICKNAME)/*.v))
# Explicitly list the Verilog files for synthesis
export VERILOG_FILES = $(DESIGN_HOME)/src/$(DESIGN_NICKNAME)/vsdbabysoc.v \
                       $(DESIGN_HOME)/src/$(DESIGN_NICKNAME)/rvmyth.v \
                       $(DESIGN_HOME)/src/$(DESIGN_NICKNAME)/clk_gate.v \
                       $(DESIGN_HOME)/src/$(DESIGN_NICKNAME)/stubs.v

export SDC_FILE      = $(DESIGN_HOME)/src/$(DESIGN_NICKNAME)/vsdbabysoc_synthesis.sdc

export vsdbabysoc_DIR = $(DESIGN_HOME)/$(PLATFORM)/$(DESIGN_NICKNAME)

export VERILOG_INCLUDE_DIRS = $(wildcard $(vsdbabysoc_DIR)/include/)
# export SDC_FILE      = $(wildcard $(vsdbabysoc_DIR)/sdc/*.sdc)
export ADDITIONAL_GDS  = $(wildcard $(vsdbabysoc_DIR)/gds/*.gds.gz)
export ADDITIONAL_LEFS  = $(wildcard $(vsdbabysoc_DIR)/lef/*.lef)
export ADDITIONAL_LIBS = $(wildcard $(vsdbabysoc_DIR)/lib/*.lib)
# export PDN_TCL = $(DESIGN_HOME)/$(PLATFORM)/$(DESIGN_NICKNAME)/pdn.tcl

# Clock Configuration (vsdbabysoc specific)
# export CLOCK_PERIOD = 20.0
export CLOCK_PORT = CLK
export CLOCK_NET = $(CLOCK_PORT)

# Floorplanning Configuration (vsdbabysoc specific)
export FP_PIN_ORDER_CFG = $(wildcard $(DESIGN_DIR)/pin_order.cfg)
# export FP_SIZING = absolute

export DIE_AREA   = 0 0 1600 1600
export CORE_AREA  = 20 20 1590 1590
# Placement Configuration (vsdbabysoc specific)
export MACRO_PLACEMENT_CFG = $(wildcard $(DESIGN_DIR)/macro.cfg)
export PLACE_PINS_ARGS = -exclude left:0-600 -exclude left:1000-1600: -exclude right:* -exclude top:* -exclude bottom:*
# export MACRO_PLACEMENT = $(DESIGN_HOME)/$(PLATFORM)/$(DESIGN_NICKNAME)/macro_placement.cfg

export TNS_END_PERCENT = 100
export REMOVE_ABC_BUFFERS = 1

# Magic Tool Configuration
export MAGIC_ZEROIZE_ORIGIN = 0
export MAGIC_EXT_USE_GDS = 1

# CTS tuning
export CTS_BUF_DISTANCE = 600
export SKIP_GATE_CLONING = 1

# export CORE_UTILIZATION=0.1  # Reduce this value to allow more whitespace for routing.
```

### Command for synthesis:
```
util/docker_shell make DESIGN_CONFIG=./designs/sky130hd/vsdbabysoc/config.mk PLATFORM=sky130hd synth
```
![img1]()  
![img2]()

* **Synthesis netlist:**
![img3]()

* **Synthesis Log file:**
![img4]()

* **Synthesis Stats:**
![img5]()

* **Synthesis check:**
![img6]()

### Commands for floorplan:
```
util/docker_shell make DESIGN_CONFIG=./designs/sky130hd/vsdbabysoc/config.mk floorplan
```
![img7]()  
![img8]()  

```
util/docker_shell make gui_floorplan DESIGN_CONFIG=./designs/sky130hd/vsdbabysoc/config.mk
```
![img9]()  

### Run Placement:
```
util/docker_shell make DESIGN_CONFIG=./designs/sky130hd/vsdbabysoc/config.mk place
```
![img10]()  

### Placement Result in GUI

```
util/docker_shell make gui_place DESIGN_CONFIG=./designs/sky130hd/vsdbabysoc/config.mk
```
![img11]()

* Placement Density Heatmap:
![img12]()

*  Pin Density Heatmap:
![img13]()  
