# Introduction
The inside of an FPGA board here the block level diagram of an arduino board is visualized.
FPGA Board : 
<p align="center">
<img src="https://github.com/user-attachments/assets/8f60753c-4887-4189-a404-e1d93f2b5497" 
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
alt="alt text"  >
<p/>

## Core,Die and Pad cells ##
**Core** is the section of the chip where the fundamental logic of the design is placed. **Die**   contains the core, it is the small semiconductor material specimen on which the fundamental circuit is fabricated. IC's are fabricated on a single 9 inch or 12 inch diameter silicon wafer, which contains hundreds of mirror images of the fundamental logic. This wafer is then cut into small pieces, each piece has similar functionality of the fundamental logic called Die. **Pad cells** surround the rectangular metal patches where external bonds are made. input,output and power pad cells are commonly used pad cells.
<p align="center">
<img src="https://github.com/user-attachments/assets/08a9b9f7-8890-4496-a439-46ed54dcc708" 
alt="alt text"  >
<p/>
  
## Foundry IPs and Macros ##
PLLs, DAC, ADC and SRAMs come under the category of foundry IP. They have to be manually designed or need some human interference (or intelligence) essentially to define and create them. IPs(Intellectual property) are targeted on a particular technology nodes. Macros are basically digital blocks which are made up of purely digital logic.
<p align="center">
<img src="https://github.com/user-attachments/assets/ab22cee7-dce9-4f85-8002-fc95ce990c3b" 
alt="alt text"  >
<p/>


