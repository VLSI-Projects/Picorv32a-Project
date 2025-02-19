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
    * Instruction Set Architecture (ISA) is essentially the language that allows communication between a program and computer hardware.
    * When a C program is executed, it is first compiled into assembly language, which is then translated into machine language (binary code) that the hardware understands.
    * The binary code, made of ones and zeros, is processed by the hardware to perform the required task, such as adding two numbers.
    * A key interface between the ISA and hardware is the Hardware Description Language (HDL), used to implement the architecture specifications.
    * For example, in a system with a 32-core CPU, RTL (Register Transfer Level) is used to implement and translate the ISA specifications into a physical layout for execution.
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






