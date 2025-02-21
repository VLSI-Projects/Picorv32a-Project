 # Digital VLSI Soc Desing and Planning for Picorv32a and complete RTL to GDS Flow
![Static Badge](https://img.shields.io/badge/OS-linux%2C_Windows-orange)
![Static Badge](https://img.shields.io/badge/EDA%20Tools-OpenLANE--Flow%2C_Yosys%2C_abc%2C_OpenROAD%2C_TritonRoute%2C_OpenSTA%2C_magic%2C_netgen-blue)
![Static Badge](https://img.shields.io/badge/Languages-verilog%2C_bash-purple)

# Introduction to Digital VLSI SoC Design and Planning
Digital VLSI (Very Large Scale Integration) design refers to the process of integrating a large number of electronic components, such as transistors, gates, and modules, into a single chip to create complex System on Chip (SoC) devices. These SoCs typically include a processor, memory, and peripherals, all on a single integrated circuit. SoC designs are fundamental to modern electronics and are found in everything from smartphones to embedded systems.

The PicoRV32A is a lightweight, open-source 32-bit RISC-V processor that is widely used in SoC designs, particularly for projects focused on low-power, resource-constrained systems. It is an example of a reduced instruction set computer (RISC) core, designed to be small and highly configurable, which makes it suitable for integration into custom SoC designs. The challenge in VLSI SoC design is to take this processor (or any other IP core) and combine it with other necessary system components, such as memory, peripherals, and communication interfaces, while also ensuring the design meets various requirements like performance, power, and area.

The RTL (Register Transfer Level) to GDSII (Graphic Data System) flow refers to the series of steps that take a design, described at the RTL level, and turn it into a physical chip layout ready for manufacturing. These steps include synthesis, placement, routing, verification, and sign-off, and each step involves sophisticated tools and methods. The design and verification of SoCs require careful planning, as they must meet stringent constraints related to timing, power, area, and functional correctness.

# VLSI SoC Design Flow for PicoRV32A and RTL to GDS
The RTL to GDS flow for designing an SoC based on the PicoRV32A processor core involves multiple stages, starting with the definition of the system's functionality and continuing through the final chip layout. Below, we break down each step in the process, focusing on the integration of PicoRV32A and other components.
The digital VLSI SoC design and planning icludes a complete RTL to GDSII flow.The implementation uses open-source EDA tools like OpenLANE and Sky130 technology.The results of various stages of the VLSI design flow, such as synthesis, floorplanning, placement, clock tree synthesis, routing, and timing analysis are included.
<br/>

# Table of Contents


1. **Day-1**-Inception of open-source EDA, OpenLANE and Sky130 PDK
    * How to talk to computers
    * SoC design and OpenLANE
    * Get familiar to open-source EDA tools
    * Lab Exercises 
2. **Day-2**- Good floorplan vs bad floorplan and introduction to library cells
    * Chip Floor planning considerations
    * Library Binding and Placement
    * Cell design and characterization flows
    * General timing characterization parameters
    * Lab Exercises 
3. **Day-3** - Design library cell using Magic Layout and ngspice characterization
    * Labs for CMOS inverter ngspice simulations
    * Inception of Layout CMOS fabrication process
    * Sky130 Tech File Labs
    * Lab Exercises
4. **Day-4**- Pre-layout timing analysis and importance of good clock tree
    * Timing modelling using delay tables
    * Timing analysis with ideal clocks using openSTA
    * Clock tree synthesis TritonCTS and signal integrity
    * Timing analysis with real clocks using openSTA
    * Lab Exercises
5. **Day-5**- Final steps for RTL2GDS using tritonRoute and openSTA
    * Routing and design rule check (DRC)
    * Power Distribution Network and routing
    * TritonRoute Features
    * Lab Exercises
<br/>

# Final Layout of Picorv32a

![image](https://github.com/user-attachments/assets/100b48c4-cd89-4e3a-a497-8a57f45591cf)

# Acknowledgements

* [Kunal Ghosh](https://github.com/kunalg123), Co-founder, VSD Corp. Pvt. Ltd.
