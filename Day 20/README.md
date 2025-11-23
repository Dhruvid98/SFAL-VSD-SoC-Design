# Floorplan and Placement of VSDBabySoC in OpenROAD
* Below steps where perfomed to for Floorplan and placement of VSDBabaySoC.
    * Creating a directory vsdbabysoc inside OpenROAD-flow-scripts/flow/designs/sky130hd
    * Create a directory vsdbabysoc inside OpenROAD-flow-scripts/flow/designs/src and include all the verilog files here.
        * The verilog files conents : copy the folders gds, include, lef and lib from the VSDBabySoC folder, copy of constraints file(vsdbabysoc_synthesis.sdc) and copy the files(macro.cfg and pin_order.cfg) from VSDBabySoC folder.
* Creating below config.mk file:
```

```
