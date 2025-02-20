## Design library cell using Magic Layout and ngspice characterization 
### Implementation

* Tasks:-
1. Clone the custom standard cell design from github the github repository.
2. Spice extraction of inverter in magic.
3. Editing the spice model file for analysis through simulation.
4. ngspice simulations.
5. Explore the DRC section of the old magic tech file for the skywater process and fix them.


### <h3 id="header-3_1_1">SPICE deck creation for CMOS inverter</h3>

**VTC- SPICE simulations**:-Here first part is to create SPICE deck, it's the connectivity information about the netlist so basically it's a netlist.It has input that are provided to the simulation and the deck points which will take the output.

**Component connectivity**:- In this we need to define the connectivity of the substrate pin. Substrate pin tunes the threshold voltage of the PMOS and NMOS.
<p align="center">
<img src="https://github.com/user-attachments/assets/fbe71fd3-9678-4539-ae75-9cbb6fd8a845" 
alt="alt text" width = 553 height = 358  >
<p/>



**Component values**:- Values for the PMOS nad NMOS. We have taken the same size of both PMOS and NMOS.

<p align="center">
<img src="https://github.com/user-attachments/assets/1d40eaee-8be1-4080-8bea-15d7e255ff3b" 
alt="alt text" width = 553 height = 358  >
<p/>



**Identify the nodes**:- Node mean the points between which there is a component.These nodes are required to define the netlist.
<p align="center">
<img src="https://github.com/user-attachments/assets/f43fd56f-a764-4b7d-8780-e9fca6b7ec11"
alt="alt text" width = 553 height = 358  >
<p/>


**Name the nodes**:- Now we name nodes as Vin, Vss, Vdd, out.
<p align="center">
<img src="https://github.com/user-attachments/assets/fb5a9a82-1de5-41f1-876f-272430aa1511"
alt="alt text" width = 553 height = 358  >
<p/>



Now we will start writing the SPICE deck. It's written like shown below

Drain- Gate- Source-  Substrate

For M1 MOSFET drain is connected to out node, gate is connected to in node, PMOS transistor substrate and Source is connected to Vdd node. 

For M2 MOSFET drain is connected to out node, gate is connected to in node, NMOS source and substrate are connected to 0.
<p align="center">
<img src="https://github.com/user-attachments/assets/fb5a9a82-1de5-41f1-876f-272430aa1511"
alt="alt text" width = 553 height = 358  >
<p/>


### <h3 id="header-3_1_2">SPICE simulation lab for CMOS inverter</h3>
<p align="center">
<img src="https://github.com/user-attachments/assets/05523cc7-08d9-4eb6-834d-7e969887de64"
alt="alt text" width = 553 height = 358  >
<p/>

Till now we have described the connectivity information about CMOS inverter now we will describe the other components connnectivity information like load capacitor, source. Let's seee the connectivity of output load capacitor.

It is connected between out and the node 0. And it's value is 10ff. Supply voltage(Vdd) which is connected between Vdd and node 0 and value of it is 2.5 , Similarly we have input voltage which is connected between Vin and node 0 and its value is 2.5.



Now we have to give the simulation commands in which we are swiping the Vin from 0 to 2.5 with the stepsize of 0.05. Because we want Vout while changing the Vin.

Final step is to model files. It has the complete description about NMOS and PMOS.

Now we will do the SPICE simulation for the particular values. And will get the graph.

<p align="center">
<img src="https://github.com/user-attachments/assets/dce6d5a0-7b70-488f-945d-5b32107ba1a6"
alt="alt text" width = 553 height = 358  >
<p/>

Now, doing other simulation in which we change the PMOS width to 3 times of NMOS width. and after diong the simulation, we get the graph like this shown below

<p align="center">
<img src="https://github.com/user-attachments/assets/fecfbdcd-a55a-41fd-af79-d81e8835d8dc"
alt="alt text" width = 553 height = 358  >
<p/>
The difference between these two graphs is that in the second graph the transfer charactoristic is lies in the exact middle of the graph where in the first graph it is lies left from the middle of the graph.


### <h3 id="header-3_1_3"> Switching Threshold Vm</h3>

These both model of different width has their own application. By comparing this both waveform, we can see that the shape of the both waveform is same irrespective of the voltage level.It tells that CMOS is a very roboust device. when Vin is at low, output is at high and when Vin is at high, the output is at low. so the charactoristic is maintain at all kind of CMOS with different size of NMOS or PMOS. That is why CMOS logic is very widely used in the design of the gates.

Switching thresold, Vm (the point at which the device switches the level) is the one of the parameter that defined the robustness of the Inverter. Switching thresold is a point at which Vin=Vout.
<p align="center">
<img src="https://github.com/user-attachments/assets/ab10dbc2-8bf0-4ea8-a38e-80b4f6ad1a62"
alt="alt text" width = 553 height = 358  >
<p/>


In this figure, we can see that at Vm~0.9v, Vin=Vout. This point is very critical point for the CMOS because at this point there is chance that both PMOS and NMOS are turned on. If both are turned on then there are high chances of leakage current(Means current flow direcly from power to ground).



### <h3 id="header-3_1_4"> Static and dynamic simulation of CMOS inverter</h3>

In Dynamic simulation we will know about the raise and fall delay of CMOS inverter and how does it varying with Vm. In this simulation everything else will remian same except the input which is provided will be a pulse and simulation command will be .tran

The graph Time vs Voltage will be plotted here from where we can calculate the rise and fall delay.
<p align="center">
<img src="https://github.com/user-attachments/assets/79b76800-0a31-4baf-a614-f852b223a9d4"
alt="alt text" width = 553 height = 358  >
<p/>





## <h3 id="header-3_2">Inception of layout ̂A CMOS faabrication process</h3>
### <h3 id="header-3_2_1">Create Active regions</h3>

**1) selecting a substrate**:- we have a p-type silicon substrate having high resistivity(5-50ohm) well dopped, and orintation(100).

**2) creating active region for transistor**:- Region where you see PMOS and NMOS. On p-type substrate we are going to create some small pockets which will be called as active region and in these pockets we are going to create PMOS and NMOS transistor. Will cretae isolation between each and every pockets. 

We create the isolation layer by depositing the Sio2 layer (~40nm) on the substrate. Now, we are depositing the Si3N4 layer (~80 nm) on the Sio2 layer.
![image](https://github.com/user-attachments/assets/29af7999-f3b5-4e80-8226-79cfe73918b0)

Before creating the pocket identify the region where we need to crete the pocket. Now will deposite a layer of photoresist(~1um) on which we will create some mask1 using UV light.

![image](https://github.com/user-attachments/assets/156d954f-0ee3-4c89-9a90-6a9dfab20874)

Unwanted area has been exposed using UV light. And we get pattern the exposed area is getting washed away.

![image](https://github.com/user-attachments/assets/2667d500-2e00-4669-b0c3-8d26191f90c9)


In the next step mask will be removed and doing etching of Si3N4 layer on the exposed area.

![image](https://github.com/user-attachments/assets/13ccaf89-54af-4a4e-b4d4-37ac4e5ca8af)


Now, next step is to remove photoresist by chamical reaction, because now to Si3N4 layer itslef behaves like good protecting layer for Sio2 layer. now,We will place it in the oxidation furnace. if we do LOCOS (local oxidation of silicon) process, the exposed sio2 part will grow and bird break also form. This grown sio2 will provide the perfect isolation between two PMOS and NMOS. This is how we protect two transistor communicating with each other.

![image](https://github.com/user-attachments/assets/8100629d-db81-40ca-9513-ab265e62b225)


Next step is to remove the Si3N4 using hot phospheric acid.

![image](https://github.com/user-attachments/assets/5c6c79e9-40a7-44ec-a5c5-eb316087d244)


### <h3 id="header-3_2_2">Formation of N-well and P-well</h3>

![image](https://github.com/user-attachments/assets/6fd02b96-becc-4f69-b90d-b716c6715aca)

### <h3 id="header-3_2_3"> Formation of gate terminal</h3>
![image](https://github.com/user-attachments/assets/b71c8286-c16f-4026-8668-e3c3dc817cf2)




### <h3 id="header-3_2_4">Lightly doped drain (LDD) formation</h3>

**5) LDD formation**:- Here, we actully want P+,P-,N doping profile in the PMOS and N+,N-,P doping profile for NMOS. Reason for that is

Hot electron effect

short channel effect

For the formation of LDD, we again do ion implantation in P-well by using mask 7 and here we use phosphoros as a ion for light doping.

![image](https://github.com/user-attachments/assets/a0d66bea-e06e-4bfa-aa54-5b60ef62cfe5)



### <h3 id="header-3_2_5">Source ÃÂ drain formation</h3>

**6)source-drain formation**

Next step is deposite the very thin screen oxide layer to avoid the effect of channeling.

![image](https://github.com/user-attachments/assets/6e6b5127-b974-4522-8011-80589a523ba6)



### <h3 id="header-3_2_6">Local interconnect formation</h3>

**7)steps tp form contacts and local interconnects**:- First step is remove the thin screen oxide layer by etching. Then deposite the titanium (Ti) using sputtering. here Ti is used because Ti has very low resistivity.

![image](https://github.com/user-attachments/assets/a3aedf4e-e7ee-4ccd-b60b-6227d7d0cdae)


Next step is to create the reaction between Ti layer and source, gate, drain of CMOS. For that wafer is heated at about 650-700 degree temparature in N2 ambient for about 60 seconds. and after reaction, we can see the titanium siliside over the wafer. One more reaction is heppend there between Ti and N. and it results the TIN which is used for local communication.



### <h3 id="header-3_2_7"> Higher level metal formation</h3>

**8)Higher level metal formation**:- These steps are very semilar like previous steps. First thing that we are noticing is that the surface is non planner. it is not good to use this type of non planner serface for matel interconnects because of the problems regarding the metal disconinuty. so, we have to plannerize the surface by depositing the thick layer of sio2 with some impurity to make less resistive layer. and then we used CMP (chemical mechanical polishing) technique to plannerise the surface.

And finally our CMOS is looks like this after the fabrication.

![image](https://github.com/user-attachments/assets/bd538eac-6915-4d7a-84fe-804d910856c3)


#### 1. Clone custom inverter standard cell design from github repository

```bash
# Change directory to openlane
cd Desktop/work/tools/openlane_working_dir/openlane

# Clone the repository with custom inverter design
git clone https://github.com/nickson-jose/vsdstdcelldesign

# Change into repository directory
cd vsdstdcelldesign

# Copy magic tech file to the repo directory for easy access
cp /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech .

# Check contents whether everything is present
ls

# Command to open custom inverter layout in magic
magic -T sky130A.tech sky130_inv.mag &
```
<p align="center">
<img src="https://github.com/user-attachments/assets/51adc6da-7ab2-4c1e-b0d8-920fca0ff34d"
alt="alt text" width = 553 height = 358  >
<p/>
  
<p align="center">
<img src="https://github.com/user-attachments/assets/84dc153a-bcff-43aa-a258-4c270915f3a9"
alt="alt text" width = 553 height = 358  >
<p/>
  
## Sky130 Tech File Labs
<p align="center">
<img src="https://github.com/user-attachments/assets/6cab866b-a43a-40e2-ac49-1f604bf1aaba"
alt="alt text" width = 553 height = 358  >
<p/>
After running this file we get output of ngspice like this,
<p align="center">
<img src="https://github.com/user-attachments/assets/57a7e29c-b1c3-47b3-b170-d759439f8b16"
alt="alt text" width = 553 height = 358  >
<p/>
Now, ploting the graph here by command, plot y vs time a.

<p align="center">
<img src="https://github.com/user-attachments/assets/499f77e8-4e2e-40fd-bf64-a96dd5f78e5f"
alt="alt text" width = 553 height = 358  >
<p/>

![Screenshot from 2025-02-20 20-43-33](https://github.com/user-attachments/assets/efd7e81f-9176-4fcc-a492-9148b304a1e5)

![Screenshot from 2025-02-20 20-44-31](https://github.com/user-attachments/assets/fc5a51b3-b7bb-4e93-9abf-43ca53c20d77)

![Screenshot from 2025-02-20 20-46-16](https://github.com/user-attachments/assets/32284bfd-b6e0-497d-8c7d-11c7d64aab22)
![Screenshot from 2025-02-20 20-46-19](https://github.com/user-attachments/assets/4a511589-42ac-4872-a6cf-894184b83e96)
![Screenshot from 2025-02-20 20-51-25](https://github.com/user-attachments/assets/7ea7f966-647b-4ad7-ba98-ea42de96125d)
![Screenshot from 2025-02-20 20-52-55](https://github.com/user-attachments/assets/b882bcb4-f4f9-447e-bff5-875834ac78e5)
![Screenshot from 2025-02-20 20-53-06](https://github.com/user-attachments/assets/62e210f6-9e8d-4467-8d32-923c396754a3)
![Screenshot from 2025-02-20 21-05-21](https://github.com/user-attachments/assets/4314438f-1ab4-444e-a880-7fd71077c163)
![Screenshot from 2025-02-20 21-07-19](https://github.com/user-attachments/assets/1a5e1994-9496-45fc-b75a-9c3523268b02)
![Screenshot from 2025-02-20 21-09-01](https://github.com/user-attachments/assets/6058de99-d7e5-4a91-bfa9-559ad682146c)
![Screenshot from 2025-02-20 21-13-09](https://github.com/user-attachments/assets/7f63946b-476a-4769-a563-2e6c570f0ede)
![Screenshot from 2025-02-20 21-13-24](https://github.com/user-attachments/assets/54359daa-bb0e-4628-9b22-2808650f5b8b)






