Yes. You mean the **README structure and headings should look professional and clean on GitHub**, not like a long report.

Use clear GitHub-style sections such as **Overview, Tools & Technologies, Design Configuration, OpenLane Setup, Synthesis Flow, Results, Timing Analysis, Output Files, Conclusion, Future Work**.

Here is a cleaner version you can copy directly:

````markdown
# PicoRV32A ASIC Synthesis using OpenLane and Sky130A

## Overview

This project demonstrates the synthesis of the **PicoRV32A RISC-V processor** using the **OpenLane ASIC design flow** with the **Sky130A PDK**.

The experiment was carried out from RTL preparation through synthesis, technology mapping, synthesized netlist generation, and static timing analysis.

---

## Tools & Technologies

- **OpenLane v0.21**
- **Yosys 0.9+3621**
- **OpenSTA 2.3.0**
- **Sky130A PDK**
- **sky130_fd_sc_hd** standard-cell library
- **Verilog**
- **Linux / Ubuntu**

---

## Design Configuration

| Parameter | Value |
|---|---|
| Design | PicoRV32A |
| Design Name | `picorv32a` |
| Clock Port | `clk` |
| Clock Period | `5.000 ns` |
| PDK | `sky130A` |
| Standard Cell Library | `sky130_fd_sc_hd` |

### Design Configuration Screenshot

![Design Configuration](images/conflict_tcl_picorv32a.png)

---

## OpenLane Setup

I started the OpenLane flow in **interactive mode** and prepared the PicoRV32A design for synthesis.

### OpenLane Interactive Mode

```bash
flow.tcl -interactive
```

### Preparing the Design

```tcl
package require openlane 0.9
prep -design picorv32a
```

![OpenLane Interactive Flow](images/flow_tcl_interatives.png)

---

## Synthesis Flow

The PicoRV32A RTL was processed through the following synthesis stages:

```text
PicoRV32A RTL
      ↓
Yosys Synthesis
      ↓
Logic Optimization
      ↓
ABC Technology Mapping
      ↓
DFF Legalization
      ↓
Sky130 Standard-Cell Mapping
      ↓
Synthesized Netlist
```

### Synthesis Execution

![Synthesis Run](images/run_sysnthesis_piscrv32a.png)

---

## Technology Mapping

After synthesis, the design was mapped to the **Sky130 high-density standard-cell library**.

```text
sky130_fd_sc_hd
```

The synthesis output also shows the mapping of flip-flop cells to the corresponding Sky130 standard cells.

### Technology Mapping Results

![Technology Mapping](images/less_merge.png)

![Technology Mapping Details](images/less_merge2.png)

![Technology Mapping Output](images/less_merge3.png)

---

## Synthesized Netlist

The synthesis process generated the technology-mapped Verilog netlist:

```text
picorv32a.synthesis.v
```

### Netlist Output

![Synthesized Netlist](images/picorv32a_synthesis_netlist.png)

---

## Synthesis Statistics

The Yosys synthesis reports were used to check the size and structure of the synthesized design.

### Main Synthesis Statistics

| Parameter | Result |
|---|---:|
| Wires | 14,596 |
| Wire Bits | 14,978 |
| Public Wires | 1,565 |
| Public Wire Bits | 1,947 |
| Memories | 0 |
| Processes | 0 |
| **Cells** | **14,876** |

### Yosys Statistics

![Yosys Synthesis Statistics](images/less_yosys_synthesis_stat.png)

### PicoRV32A Statistics

![PicoRV32A Statistics](images/picorv32a_stats.png)

![PicoRV32A Statistics 2](images/picorv32a_stats.1png.png)

![PicoRV32A Statistics 3](images/picorv32a_stats3.png)

---

## Static Timing Analysis

After synthesis, timing information was checked using **OpenSTA**.

The design was configured with a clock period of:

```text
5.000 ns
```

The generated OpenLane reports contain timing information from the synthesized design.

### Timing / Synthesis Report

![Synthesis Report](images/synthesis_report.png)

---

## Key Results

| Parameter | Result |
|---|---|
| Design | PicoRV32A |
| Total Cells | **14,876** |
| Total Wires | **14,596** |
| Clock Period | **5.000 ns** |
| PDK | **Sky130A** |
| Standard Cell Library | **sky130_fd_sc_hd** |
| Synthesized Netlist | `picorv32a.synthesis.v` |

---

## Project Outputs

The main outputs obtained from the experiment include:

- Synthesized Verilog netlist
- Yosys synthesis statistics
- Technology mapping results
- OpenSTA timing reports
- DFF mapping results

---

## Conclusion

This experiment gave me practical experience with the **OpenLane ASIC synthesis flow** using the **Sky130A PDK**.

I worked through the synthesis process, observed technology mapping to standard cells, generated the synthesized netlist, and examined the synthesis and timing reports.

It helped me understand how a **Verilog RTL design moves toward ASIC implementation** using an open-source EDA flow.

---

## Future Work

The next stages I plan to explore are:

- Floorplanning
- Placement
- Clock Tree Synthesis (CTS)
- Routing
- Design Rule Checking (DRC)
- Layout Versus Schematic (LVS)
- Post-route timing analysis
- GDSII generation

---

## Author

**A. Vidyasagar**  
B.Tech – Electronics and Communication Engineering  
Anurag University
````

This is much more suitable for a **GitHub project README**: clean hierarchy, proper section labels, tables where useful, and all **12 of your exact image filenames** are included.
