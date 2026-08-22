Sure — you want the **same README structure as the previous one**, but written in a more **human/student style**, with the clickable index and your output pictures in the same suitable places.

You can copy this directly into GitHub:

# 2:1 Multiplexer (MUX) – RTL Design, Simulation and Synthesis

## 📑 Index

Click on any topic below to directly go to that section.

1. [About the Experiment](#1-about-the-experiment)
2. [What is a 2:1 MUX?](#2-what-is-a-21-mux)
3. [Tools Used](#3-tools-used)
4. [RTL Design](#4-rtl-design)
5. [Simulation](#5-simulation)
6. [GTKWave Output](#6-gtkwave-output)
7. [Synthesis Using Yosys](#7-synthesis-using-yosys)
8. [Synthesized Circuit](#8-synthesized-circuit)
9. [Generated Netlist](#9-generated-netlist)
10. [Design Flow](#10-design-flow)
11. [Project Files](#11-project-files)
12. [Result](#12-result)
13. [What I Learned](#13-what-i-learned)

---

## 1. About the Experiment

In this experiment, I worked on a simple **2:1 Multiplexer (MUX)** using Verilog.

The main purpose of this experiment was to understand how a small RTL design is developed and verified. I first wrote the Verilog code, then simulated it and checked the waveform using GTKWave. After making sure the design was working correctly, I synthesized it using Yosys.

I also used the **Sky130 standard cell library** to see how the RTL design gets converted into a standard-cell implementation.

The MUX was mapped to the following Sky130 cell:

```text
sky130_fd_sc_hd__mux2_1
```

---

## 2. What is a 2:1 MUX?

A **2:1 Multiplexer** is a simple digital circuit that selects one input from two available inputs and sends the selected input to the output.

The inputs used in this experiment are:

* `i0` – Input 0
* `i1` – Input 1
* `sel` – Select signal
* `y` – Output

The working of the MUX is:

```text
sel = 0  →  y = i0
sel = 1  →  y = i1
```

The Boolean expression is:

```text
y = (~sel & i0) | (sel & i1)
```

---

## 3. Tools Used

I used the following tools for this experiment:

* **Verilog** – for writing the RTL code
* **Yosys** – for synthesis
* **Sky130 Standard Cell Library** – for technology mapping
* **GTKWave** – for viewing simulation waveforms
* **Graphviz** – for viewing the synthesized circuit
* **Oracle VirtualBox** – for running the Linux/EDA environment

---

## 4. RTL Design

The 2:1 MUX was written using a simple Verilog `assign` statement.

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

This is a combinational circuit, so there is no clock or reset signal.

The output depends directly on the input signals and the select signal.

---

## 5. Simulation

After writing the RTL code, I created a testbench and simulated the design.

The simulation generated a waveform file, which I opened using **GTKWave**.

I mainly checked the following signals:

```text
i0
i1
sel
y
```

The purpose of the simulation was to make sure that the output was selecting the correct input for different values of `sel`.

---

## 6. GTKWave Output

The following is the waveform output obtained from the simulation:

![GTKWave Simulation Output](gtkwave_simulation_output.png)

### Observation

From the waveform, I observed that:

* When `sel = 0`, the output `y` follows `i0`.
* When `sel = 1`, the output `y` follows `i1`.

So the waveform matches the expected behavior of a 2:1 MUX.

This confirmed that the RTL design was working correctly before moving to the synthesis stage.

[⬆️ Back to Index](#-index)

---

## 7. Synthesis Using Yosys

After verifying the design through simulation, I moved on to synthesis using **Yosys**.

The basic synthesis process was:

1. Read the Verilog RTL.
2. Perform synthesis and optimization.
3. Map the design to the Sky130 standard cell library.
4. Generate the synthesized netlist.
5. View the synthesized circuit.

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

This shows that the simple MUX RTL was converted into a standard cell from the Sky130 library.

---

## 8. Synthesized Circuit

After synthesis, I used Yosys to view the synthesized circuit.

### Yosys Output

![Yosys Synthesized MUX](yosys_synthesis_output.png)

The synthesized circuit contains:

* `i0` – first data input
* `i1` – second data input
* `sel` – select input
* `y` – output

The screenshot also shows the Yosys synthesis information and the generated netlist.

The circuit structure matches the expected behavior of a 2:1 MUX.

[⬆️ Back to Index](#-index)

---

## 9. Generated Netlist

After synthesis, Yosys generated a Verilog netlist.

The important cell present in the synthesized design is:

```text
sky130_fd_sc_hd__mux2_1
```

This was one of the main things I wanted to observe in this experiment — how the simple RTL code gets converted into a technology-specific standard-cell implementation.

---

## 10. Design Flow

The complete flow I followed was:

```text
Verilog RTL
     ↓
Testbench
     ↓
Simulation
     ↓
GTKWave
     ↓
Waveform Verification
     ↓
Yosys Synthesis
     ↓
Sky130 Technology Mapping
     ↓
Synthesized Netlist
     ↓
Synthesized Circuit
```

---

## 11. Project Files

The GitHub repository can be organized like this:

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

> **Note:** Keep both `.png` files in the same folder as `README.md`. This is required for GitHub to display the screenshots correctly.

---

## 12. Result

The **2:1 MUX was successfully designed and verified**.

The GTKWave simulation confirmed that the output `y` correctly follows the selected input.

After simulation, the RTL was synthesized using Yosys and mapped to the Sky130 standard cell:

```text
sky130_fd_sc_hd__mux2_1
```

The synthesized circuit also showed the expected MUX structure.

So, the experiment was completed successfully.

[⬆️ Back to Index](#-index)

---

## 13. What I Learned

Through this experiment, I got a better understanding of the basic **RTL-to-netlist flow**.

I learned how to:

* Write a simple 2:1 MUX in Verilog.
* Create and run a testbench.
* Check the simulation waveform using GTKWave.
* Synthesize RTL using Yosys.
* Use the Sky130 standard cell library.
* Generate a synthesized netlist.
* View the synthesized circuit.

Overall, this experiment helped me understand how a simple Verilog design can move from **RTL code → simulation → synthesis → standard-cell implementation**.

[⬆️ Back to Index](#-index)
