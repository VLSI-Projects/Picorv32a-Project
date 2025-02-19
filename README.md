# Introduction
The inside of an FPGA board here the block level diagram of an arduino board is visualized.
FPGA Board : 
<p align="center">
<img src="https://github.com/user-attachments/assets/ab1bcdf6-311a-4047-8c65-83c5b1d61bc0" 
alt="alt text" width = 553 height = 358  >
<p/>

<br/>
The inside block level diagram of an arduio board:
<p align="center">
<img src="https://github.com/user-attachments/assets/9b20eb0b-deb8-4f1c-a5c9-23adef6f73ca" 
alt="alt text" width = 553 height = 358  >
<p/>
# IC Design Components and Terminologies
**IC** or **Integrated circuit** is basically an electronic circuit consisting of large number of transistors, resistors and capacitors etc inside a single semiconductor chip. They come in a variety of packages and sizes. Some of the commonly used ICs include Timer 555 ic, 741 operational amplifiers, 78xx series of voltage regulators and 74xx series of logic gates.<br/>
**SOC - System on Chip** is also a type of IC which has the capabilities of a computer built inside the chip. It typically consists of a CPU, memory , input and output ports, analog IPs and other units integrated within itself.SoCs can be applied to any computing task. They are typically used in mobile computing such as tablets, smartphones, smartwatches and netbooks as well as embedded systems.<br/>
<p align="center">
<img src="https://github.com/user-attachments/assets/56a566c8-0ac2-47d0-a9df-e67ba9ee9deb" 
alt="alt text" width = 553 height = 358  >
<p/>

## Packages ##
Integrated circuits are put into protective packages to allow easy handling and assembly onto printed circuit boards and to protect the devices from damage. A very large number of different types of package exist. Through-hole packages, Surface mount, Chip carrier, Pin grid arrays, Flat packages and ball grid array are some of the most common packages. In this workshop we deal with a variant of Flat package called QFN-48 ( Quad Flat No leads with 48 pins)
<p align="center">
<img src="https://github.com/user-attachments/assets/9ba33401-ea5b-4d7e-9735-0a76a31cf407" 
alt="alt text" width = 553 height = 358  >
<p/>

## Core,Die and Pad cells ##
* **Pads** help transmit signals between the outside world and the interior of the package.
* **Core** is the area where the digital logic circuits are placed.
* **Die** refers to the size of the silicon chip itself, excluding the surrounding packaging material.
<p align="center">
<img src="https://github.com/user-attachments/assets/08a9b9f7-8890-4496-a439-46ed54dcc708" 
alt="alt text" width = 553 height = 358  >
<p/>
  
## Foundry IPs and Macros ##
PLLs, DAC, ADC and SRAMs come under the category of foundry IP. They have to be manually designed or need some human interference (or intelligence) essentially to define and create them. IPs(Intellectual property) are targeted on a particular technology nodes. Macros are basically digital blocks which are made up of purely digital logic.
<p align="center">
<img src="https://github.com/user-attachments/assets/ab22cee7-dce9-4f85-8002-fc95ce990c3b" 
alt="alt text" width = 553 height = 358  >
<p/>

## RISC V Instruction Set Architecture ##
• Instruction Set Architecture (ISA) is essentially the language that allows communication between a program and computer hardware.
    
• When a C program is executed, it is first compiled into assembly language, which is then translated into machine language (binary code) that the hardware understands.
    
• The binary code, made of ones and zeros, is processed by the hardware to perform the required task, such as adding two numbers.
    
• A key interface between the ISA and hardware is the, used to implement the architecture specifications.
    
• For example, in a system with a 32-core CPU, RTL is used to implement and translate the ISA specifications into a physical layout for execution.
    
<p align="center">
<img src="https://github.com/user-attachments/assets/b71ae209-68e2-4c59-82b1-4c6371d58551" 
alt="alt text" width = 553 height = 358  >
<p/>
  
## Basic Mapping from Applications to Hardware ## 
Explaining about the stack. 
<p align="center">
<img src="https://github.com/user-attachments/assets/5961ec02-c024-418f-acb5-0e18b82e223a" 
alt="alt text" width = 553 height = 358  >
<p/>

<p align="center">
<img src="https://github.com/user-attachments/assets/892a01d3-8e2b-4d46-918c-79689b0e0153" 
alt="alt text" width = 553 height = 358  >
<p/>

<p align="center">
<img src="https://github.com/user-attachments/assets/ce31bc29-9dec-478f-bd0b-4ca076b06745" 
alt="alt text" width = 553 height = 358  >
<p/>

## OpenSource Digital ASIC Design ## 
<p align="center">
<img src="https://github.com/user-attachments/assets/3d58e6f8-6b73-46b2-9bcc-abef47940f5b" 
alt="alt text" width = 553 height = 358  >
<p/>

• PDK = Process Design Kit

• Collection of files used to model a fabrication process for the EDA tools used to design an IC

Process Design Rules: DRC, LVS, PEX

• Device Models

• Digital Standard Cell Libraries

• I/O Libraries

## Simplified RTL to GDS flow ##
* **Synthesis:** This stage converts the HDL code (e.g., Verilog) into a gate-level netlist. The netlist represents the circuit's functionality using basic logic gates.
  
* **Floor and Power Planning:** In this stage, the chip layout is planned. The die area is divided into sections for different functional blocks and I/O pads. The power supply network is also designed to ensure proper power distribution throughout the chip.
 
* **Placement:** This stage involves positioning the logic cells from the netlist onto the chip layout. The goal is to find optimal locations for the cells considering factors like timing and area constraints. There are two main placement steps:

    * **Global placement:** This provides an initial placement for all cells, aiming for optimal positions but not necessarily following all layout rules. The placement in this step may not always be legal.
    * **Detailed placement:** This refines the initial placement to ensure all cells adhere to the design rules.

* **Clock Tree Synthesis (CTS):** A clock tree is a network of buffers and wires that distributes the clock signal to all sequential elements (flip-flops) in the design. CTS aims to minimize clock skew, which is the variation in arrival time of the clock signal at different flip-flops.

* **Routing:** This stage involves creating connections between the placed cells using metal layers available in the fabrication process. Routing is typically done in two steps:

    * **Global routing:** This defines the general paths for the connections between cells.
    * **Detailed routing:** This implements the actual wiring connections based on the global routing plan.

* **Sign-off:** This stage involves various checks to ensure the design meets the desired functionality and manufacturing requirements. Here are some common sign-off checks:

    * **Design Rule Checking (DRC):** This verifies if the layout adheres to the design rules specified by the PDK for the fabrication process.
    * **Layout vs Schematic (LVS):** This compares the final layout with the original gate-level netlist to ensure they are equivalent.
    * **Static Timing Analysis (STA):** This analyzes the timing delays in the design to ensure all signals meet the timing constraints and the circuit operates at the required frequency.


<p align="center">
<img src="https://github.com/user-attachments/assets/dc0006e9-3a01-430a-83f4-59e55669a88a" 
alt="alt text" width = 553 height = 358  >
<p/>

## OpenLANE ##

The OpenLANE ASIC Flow shown in the image consists of several steps in the digital design flow for ASIC implementation using the OpenROAD tool and the SKY130 PDK:
Below is the OpenLANE ASIC flow formatted similarly to your reference:

---

## Simplified RTL to GDS Flow for OpenLANE ##

* **RTL Design Input:**  
  - Begin with your design written in an HDL (e.g., Verilog or VHDL). This description represents your circuit’s intended behavior.

* **Synthesis:**  
  - Convert the RTL code into a gate-level netlist using tools like **Yosys + abc**.  
  - This netlist represents the circuit using standard logic gates and serves as the basis for physical implementation.  
  - **Static Timing Analysis (STA)** using **OpenSTA** is performed to ensure timing constraints are met.

* **Floorplanning and Placement:**  
  - **Floorplanning:**  
    - Define the chip's die area and plan the overall layout by allocating regions for different functional blocks, I/O pads, and power domains.
  - **Placement:**  
    - Position the synthesized standard cells on the chip.  
    - This step is often divided into two phases:  
      * **Global Placement:** Provides an initial rough placement of cells to optimize overall area and connectivity.  
      * **Detailed Placement:** Refines the placement to comply with physical design rules and improve timing.
  - **Clock Tree Synthesis (CTS):**  
    - Construct a clock distribution network that minimizes clock skew across sequential elements by inserting buffers and carefully routing the clock signals.

* **Routing:**  
  - **Global Routing:**  
    - Establish approximate wiring paths between cells based on the placement, ensuring connectivity.
  - **Detailed Routing:**  
    - Generate exact routing paths for each connection according to the available metal layers and design rules.
  - **Antenna Diode Insertion and Swapping:**  
    - Run scripts (often “fake” ones during flow verification) to insert and adjust diode connections to protect transistors during fabrication.

* **Verification and Sign-off Checks:**  
  - **Logic Equivalence Check (LEC):**  
    - Ensure that the synthesized gate-level netlist is functionally equivalent to the original RTL design.
  - **RC Extraction & Timing Analysis:**  
    - Extract parasitic resistances and capacitances to refine timing analysis using **OpenSTA**.
  - **Design Rule Checking (DRC) and Layout vs. Schematic (LVS):**  
    - Verify that the layout complies with the PDK’s design rules using tools like **Magic & Netgen**.
    - Confirm that the final physical layout matches the gate-level netlist.

* **GDSII Generation:**  
  - Finalize the design by generating the GDSII file, which is the standard format for chip fabrication.


<p align="center">
<img src="https://github.com/user-attachments/assets/f51a48f3-18ea-482a-94d9-536721a57939" 
alt="alt text" width = 553 height = 358  >
<p/>
This structured flow encapsulates the OpenLANE process from RTL input to the final GDSII output, ensuring a fully verified ASIC design ready for manufacturing.

## LABS ##
* **Familliarization with open-source EDA tools**
  * **LAB tasks:-**
<p align="center">
<img src="https://github.com/user-attachments/assets/ead2d1ad-ce27-42ee-aa0c-97a0d3a7caea" 
alt="alt text" width = 553 height = 358  >
<p/>
  
####  Run 'picorv32a' design synthesis using OpenLANE flow.

Commands to invoke the OpenLANE flow and perform synthesis

```bash
# Change directory to openlane flow directory
cd Desktop/work/tools/openlane_working_dir/openlane

# The 'docker' command  can invoke the OpenLANE flow docker sub-system by just running this command
docker
```
```tcl
# OpenLANE flow contained docker  we can invoke the OpenLANE flow in the Interactive mode using the following command
./flow.tcl -interactive


# Input the required packages for the OpenLANE flow
package require openlane 0.9

# Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific design which in our case is 'picorv32a'
prep -design picorv32a


# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis


# Now we can run floorplan
run_floorplan

```


####  Results
<p align="center">
<img src="https://github.com/user-attachments/assets/5ebc1036-7407-4d4e-b568-dabee91a7776" 
alt="alt text" width = 553 height = 358  >
<p/>

<p align="center">
<img src="https://github.com/user-attachments/assets/2c22056f-b2aa-4e65-a9d9-6d527b5e3cdb" 
alt="alt text" width = 553 height = 358  >
<p/>

<p align="center">
<img src="https://github.com/user-attachments/assets/66c41a48-dbde-4d35-9b50-957ad6e5fbaa" 
alt="alt text" width = 553 height = 358  >
<p/>

<p align="center">
<img src="https://github.com/user-attachments/assets/86aa9f8b-3350-4a36-932b-c73cb5c91f59" 
alt="alt text" width = 553 height = 358  >
<p/>


#### 2. Calculate the flop ratio.

The Flip-flop ratio is calculated from the synthesis statistics file 

<p align="center">
<img src="https://github.com/user-attachments/assets/868f08d5-1c19-4f14-aa2c-4e87814a58a5" 
alt="alt text" width = 800 height = 500  >
<p/>

Calculation of Flop Ratio and DFF % from synthesis report file

```math
Flop\ Ratio = \frac{1613}{14876} = 0.108429685
```
```math
Percentage\ of\ DFF's = 0.108429685 * 100 = 10.84296854\ \%
```

