# Week 1  task completion
# Icarus Verilog Workflow

```
iverilog design.v tb_for_design.v
./a.out
```
This is where we'll get the vcd file

## GTKWave

```
gtkwave vcd_file.vcd
```

## What a Synthesizer Does

It uses our design files along with `read_verilog` and `.lib` files with `read_liberty`, feeds them to **Yosys**, and produces a **netlist** — a representation of the design mapped to standard cells.

## Verifying the Synthesis

1. Feed the synthesized **netlist** and the **testbench** to Icarus Verilog (iverilog).
2. Run simulation and generate a **VCD** file.
3. Open the VCD in **GTKWave**.
4. The waveform should match the RTL simulation.

## Why Different Flavours of Gates Are Required

* **Fast cells**: Required to meet timing (higher max frequency). Trade-off: more area and power consumption.
* **Slow cells**: Sometimes used to fix hold-time issues. Trade-off: larger propagation delay.
* These trade-offs are influenced by **capacitances**.

## Yosys Workflow

```
read_liberty -lib ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog good_mux.v
synth -top good_mux
abc -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```

## To Write the Netlist

```
write_verilog -noattr good_mux_netlist.v
```

## PVT in Design

**PVT** = Process, Voltage, Temperature.

`.lib` files provide technology data (e.g., CMOS), delay models, and units for timing/power, etc.,.

## Hierarchical vs Flat Synthesis

* **Hierarchical synthesis**: synthesize submodules separately. Advantage: repeated submodules synthesized once.
* **Flat synthesis**: flattens hierarchy before synthesis — may increase compile time and resource use.

## Why Flip-Flops Are Used

Combinational logic can produce **glitches** that propagate unpredictably. Flip-flops register signals between stages, preventing glitch propagation and stabilizing outputs.

### Initializing Flip-Flops

Use **set** or **reset** inputs: They may be asynchronous or synchronous

* **Synchronous**: reset/set takes effect on a clock edge.
* **Asynchronous**: reset/set takes effect immediately, independent of clock.
