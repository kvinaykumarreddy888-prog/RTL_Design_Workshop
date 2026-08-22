# 2:1 Multiplexer (MUX) – RTL Design, Synthesis and Simulation

## 📑 Index

Click on any topic below to directly jump to that section.

1. [About the Experiment](#1-about-the-experiment)
2. [What is a 2:1 MUX?](#2-what-is-a-21-mux)
3. [Tools Used](#3-tools-used)
4. [RTL Design](#4-rtl-design)
5. [Simulation Result](#5-simulation-result)
6. [GTKWave Output](#6-gtkwave-output)
7. [Synthesis Using Yosys](#7-synthesis-using-yosys)
8. [Synthesized Circuit](#8-synthesized-circuit)
9. [Generated Netlist](#9-generated-netlist)
10. [Overall Design Flow](#10-overall-design-flow)
11. [Project Files](#11-project-files)
12. [Result](#12-result)
13. [Key Takeaway](#13-key-takeaway)

---

## 1. About the Experiment

In this experiment, I designed and verified a **2:1 Multiplexer (MUX)** using Verilog.

The main aim was to understand the basic **RTL-to-netlist flow**. I first verified the design using simulation and GTKWave, and then synthesized the RTL using Yosys with the **Sky130 standard cell library**.

The final design was mapped to the Sky130 MUX cell:

```text
sky130_fd_sc_hd__mux2_1
```

---

## 2. What is a 2:1 MUX?

A **2:1 Multiplexer** is a digital circuit that selects one of two input signals based on a select signal.

| Signal | Description   |
| ------ | ------------- |
| `i0`   | Input 0       |
| `i1`   | Input 1       |
| `sel`  | Select signal |
| `y`    | Output        |

The operation is:

```text
sel = 0  →  y = i0
sel = 1  →  y = i1
```

The Boolean expression for the MUX is:

```text
y = (~sel & i0) | (sel & i1)
```

---

## 3. Tools Used

The following tools were used for this experiment:

* **Verilog** – RTL design
* **Yosys** – RTL synthesis
* **Sky130 Standard Cell Library** – Technology mapping
* **GTKWave** – Waveform analysis
* **Graphviz** – Circuit visualization
* **Oracle VirtualBox** – Linux/EDA environment

---

## 4. RTL Design

The 2:1 MUX was written as a simple combinational Verilog circuit.

```verilog
module good_mux (
    input i0,
    input i1,
    input sel,
    output y
);

assign y = sel ? i1 : i0;

endmodule
```

Since this is a combinational circuit, there is no clock or reset signal.

---

## 5. Simulation Result

After writing the RTL and testbench, I simulated the design and generated a VCD waveform file.

The waveform was opened in **GTKWave** to verify whether the output `y` correctly follows the selected input.

---

## 6. GTKWave Output

The following is the simulation waveform obtained from GTKWave.

![GTKWave Simulation Output](gtkwave_simulation_output.png)

### Observation

From the waveform:

* When `sel = 0`, the output `y` follows `i0`.
* When `sel = 1`, the output `y` follows `i1`.
* The output changes according to the selected input.

The waveform confirms that the **2:1 MUX is working as expected**.

[⬆️ Back to Index](#-index)

---

## 7. Synthesis Using Yosys

After verifying the functionality through simulation, I synthesized the RTL using **Yosys**.

The synthesis process included:

1. Reading the Verilog RTL.
2. Running synthesis and optimization.
3. Performing technology mapping.
4. Mapping the design to the Sky130 standard-cell library.
5. Generating the synthesized Verilog netlist.
6. Viewing the synthesized circuit using the Yosys `show` command.

The Yosys output showed:

```text
ABC RESULTS:
    internal signals:     0
    input signals:        3
    output signals:       1
```

The design was successfully mapped to:

```text
sky130_fd_sc_hd__mux2_1
```

---

## 8. Synthesized Circuit

The synthesized circuit was viewed using the Yosys `show` command.

### Yosys Synthesis Output

![Yosys Synthesized MUX](yosys_synthesis_output.png)

The schematic shows:

* `i0` connected to the first MUX input.
* `i1` connected to the second MUX input.
* `sel` connected to the select input.
* `y` connected to the output.

The terminal output and generated netlist visible in the screenshot also show the successful Yosys synthesis and technology mapping.

[⬆️ Back to Index](#-index)

---

## 9. Generated Netlist

After synthesis, Yosys generated a Verilog netlist containing the Sky130 standard-cell MUX:

```verilog
sky130_fd_sc_hd__mux2_1
```

This shows how the original RTL description was converted into a **technology-specific standard-cell implementation**.

---

## 10. Overall Design Flow

The complete flow followed in this experiment was:

```text
Verilog RTL
     ↓
Testbench
     ↓
Simulation
     ↓
GTKWave Verification
     ↓
Yosys Synthesis
     ↓
Technology Mapping
     ↓
Sky130 MUX Cell
     ↓
Synthesized Netlist
     ↓
Yosys Circuit View
```

---

## 11. Project Files

The GitHub repository can contain the following files:

```text
good-mux/
│
├── good_mux.v
├── tb_good_mux.v
├── tb_good_mux.vcd
├── good_mux_netlist.v
├── gtkwave_simulation_output.png
├── yosys_synthesis_output.png
└── README.md
```

> **Note:** Keep the two image files in the same folder as `README.md`. This is important because GitHub uses the image filenames in the README to display the screenshots.

---

## 12. Result

The **2:1 MUX was successfully designed, simulated, synthesized, and technology-mapped**.

The GTKWave waveform verified the functional behavior of the MUX, while the Yosys output confirmed that the RTL was mapped to the Sky130 standard cell:

```text
sky130_fd_sc_hd__mux2_1
```

The synthesized schematic also matched the expected MUX structure.

[⬆️ Back to Index](#-index)

---

## 13. Key Takeaway

This experiment gave me practical experience with the **RTL-to-netlist flow** using open-source EDA tools.

Starting with a simple Verilog MUX, I was able to:

* Write the RTL design.
* Simulate and verify its functionality.
* Analyze the waveform using GTKWave.
* Synthesize the RTL using Yosys.
* Perform technology mapping using Sky130.
* Generate a synthesized netlist.
* View the synthesized circuit.

This small experiment helped me understand how an RTL design is transformed into a **technology-specific standard-cell implementation**.

[⬆️ Back to Index](#-index)
