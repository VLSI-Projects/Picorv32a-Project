# Pre-layout timing analysis and importance of good clock tree

   
### <h4 id="header-4_1_4">Power aware clock tree synthesis</h4>

**Power Aware CTS**:- If we make enable pin at logic '1' in the AND gate, then clock will propagate and if we make it 'logic 0' it will block the clock. Similarly in 'OR' gate if we make enable as 'logic 0' it will propagate and on making it 'logic 1' it will block the clock.

So the advantage of this blocking period is that we can save lot of power in clock tree.

![image](https://github.com/user-attachments/assets/81752cee-6f9f-44b8-b976-325945c1e925)

Let's say we have a clock tree, The buffer present at the first input is driving the load of second two buffers. We have splited the buffer and in clock gating technique we have just swaped the buffer with and gate so now will all the other characteristic will be same or will get changed will see in coming steps.

![image](https://github.com/user-attachments/assets/4110bbd6-cb54-410b-98c6-bbcf51bb6fcc)


Before swaping the buffer with gate we have made some assumptions which are follows

![image](https://github.com/user-attachments/assets/9848e654-2ae9-4683-9073-c1c19d5bd0aa)


<ul>
	<li><a> Assume c1=c2=c3=c4=25fF</a></li>
	</ul>
<ul>
	<li><a>Assume Cbuf1=Cbuf2=30fF</a></li>
	</ul>
<ul>
	<li><a>Total Cap at node 'A'=> 60fF</a></li>
	</ul>
<ul>
	<li><a>Total Cap at node 'B'=> 50fF</a></li>
	</ul>
 <ul>
	<li><a>Total Cap at node 'C'=> 50fF</a></li>
	</ul>
 
 We have made some observations from here which are as follows

 <ul>
	<li><a>2 levels of buffering</a></li>
	</ul>
<ul>
	<li><a>At every level,each node driving same load</a></li>
	</ul>
 <ul>
	<li><a>Identical buffer at same level</a></li>
	</ul>

So the output capacitance of the buffer for the entire circuit is not constant, load at the output will be varying and since the load is varying so input transition is also varying. 

So becuase of this variation in output and input we will have varity of delays so how to capture that delay we will see with delay tables

**How delay tables are prepared?**

For this purpose we have carried out the one buffer from the circuit and and seperately varying its input transition within some range of let's say 10ps-100ps than the output load will also vary so we willl characterise the delay and put the data in tabular format.

![image](https://github.com/user-attachments/assets/6ab037e9-64a0-475a-b65f-4087791c2645)

### <h4 id="header-4_1_5">Delay table usage Part 1</h4>

Let's take the example for other buffers.

![image](https://github.com/user-attachments/assets/13421b69-dea4-412a-b225-514f7c3970cf)
Assuming a slew of ’40ps’ for the first buffer and capacitance of 60fF on node ‘A’, the delay of the first buffer can be easily evaluated using below NLDM table and it comes out to be x9′


For practical example let's say we have the input transition of 40ps of buffer1 the output capacitance of this particular buffer is 60ff. The delay of the cell in this case is lies between x9-x10.

So the values which are not available in the delay table those are extrapolated from the given data so we can take the range in that case.
And similarly, for the second level of buffering, the delay of the buffers ‘2’ and ‘3’ comes out to be y15 assuming a slew of ’60ps’ and capacitance of ’50fF’ at node ‘B’ and ‘C’ (as I have built a close-to-perfect clock tree:))
![image](https://github.com/user-attachments/assets/67dc54ff-dce6-41cb-a460-8af79813b34f)
This in turn results to ‘zero’ skew at clock endpoints





## <h4 id="header-4_2">Timing analysis with ideal clocks using openSTA</h4>
### <h4 id="header-4_2_1">Setup timing analysis and introduction to flip-flop setup time</h4>
Setup timing analysis is a crucial part of digital circuit design that examines the minimum time required for a data input to be stable before a clock edge arrives at a flip-flop, ensuring the flip-flop accurately captures the data; this minimum time is called the "setup time" of the flip-flop, and is a critical parameter for reliable circuit operation

**Timing analysis (with ideal clock)**:- Let's start the setup analysis with the ideal clock(single clock). specifications of the clock is

clock frequency =1 GHz

clock period =1 ns

Now will do the analysis between '0' and 'T' clock period. We sent at edge to the launch flop at '0' clock period and at T=1ns period the second edge reached to capture flop.

Let's say here we have combinatonal delay of theta and set up timing analysis says that this combinational delay should be less than the T for system to work properly.

![image](https://github.com/user-attachments/assets/6ad9ff4f-40a1-41a3-a2ca-f2b329ce9b1c)

 Now let's open the capture flop and we will see some combinational circuit there it has several MOSFETs , several logics,resistances and capacitances inside it.Also have the time graph for this particular flop

![image](https://github.com/user-attachments/assets/135bdb5e-5549-4a86-b586-0dfd0b176cb8)


When there is logic '0' or logic '1' of clock 1 the delay of MUX1 and MUX2 will restrict or effect the combinational delay requirement.

So there is some finite amount of time which is required to the D input to settle and this amount of time is reffered to as **SET UP TIME**.

Hence finite time 's' required before clk edge for 'D' to reach Qm.

So, we can write that the internal delay of the MUX1 = set up time(S).

So, now θ<T becomes θ<(T-S).

### <h4 id="header-4_2_2">Introduction to clock jitter and uncertainty</h4>
In VLSI design, "clock jitter" refers to the random variations in the timing of a clock signal, causing unpredictable deviations from its ideal periodicity, while "clock uncertainty" is a broader term encompassing jitter along with other factors like clock skew, which collectively represent the potential variation in the clock signal's arrival time at different points in a circuit, essentially describing the "uncertain window" within which a clock edge might occur. 
So in Jitter the clock is being created by PLL(phase-locked loops) and the clk source is expected to sent the clk signal at exactly 0,T,2T,....But that clk source might or might ot be able to generate the clk exactly at 0 or any other certain time because of it's inbuilt variations that is called **jitter.** Jitter is refered as temporary variation of the clk pulse.

![image](https://github.com/user-attachments/assets/89575b87-94bb-463e-810b-e6540f0ec277)

Let's consider this uncertantity time(US) in consideration. So, now equation will become θ<(T-S-US). Now assuming  'S'=0.01ns and 'US'=0.09ns. by taking this, Let's identify the timing path in our circuit stage 1 and stage 3 logic path has single clock.

Now,we have to identify the combinational path delay for the both logics.

![image](https://github.com/user-attachments/assets/01064d54-d2cf-4dcc-b327-eb654b17340b)

![image](https://github.com/user-attachments/assets/fb7c52a9-9d13-415c-a272-7cc7b862ee80)




# Clock tree synthesis TritonCTS and signal integrity</h4>
Clock Tree Synthesis using TritonCTS" refers to a method for optimizing the clock distribution network within an integrated circuit by utilizing the TritonCTS tool, which aims to minimize clock skew and ensure signal integrity by strategically placing buffers and inverters along the clock paths, thereby achieving balanced clock delays across all circuit components. 
unction:
The primary goal of Clock Tree Synthesis (CTS) is to evenly distribute the clock signal throughout the design, minimizing the difference in arrival times (skew) at different clock pins, which is crucial for proper circuit operation and timing integrity. 
TritonCTS Tool:
TritonCTS is a widely used open-source tool for performing Clock Tree Synthesis, employing advanced algorithms to generate an efficient clock tree structure with minimal skew and power consumption. 
Signal Integrity Considerations:
Signal integrity in this context refers to maintaining the quality of the clock signal throughout the circuit, ensuring that the clock signal remains relatively clean and free from noise or distortion, which can be affected by factors like long clock paths, high fanout, and impedance mismatches. 

###  Clock tree routing and buffering using H-Tree algorithm</h4>

**Clock tree synthesis:-**  Let's connect clk1 to FF1 & FF2 of stage 1 and FF1 of stage 3 and FF2 of stage 4 with physical wire.

![image](https://github.com/user-attachments/assets/48078187-2d5c-4ba9-9d6c-ec0ad8b631d5)


Now let's see what is the problem with this? Let's consider some physical distance from clk to FF1 and FF2 , so due to this t2>t1. 

Skew= t2-t1,  and skew should be 0ps

![image](https://github.com/user-attachments/assets/e0ab845b-ae99-4e1f-b2b8-fe21167fce4c)


Previously we have build bad tree now we will try to modify that in a smarter way. Hrre clk will come in somewhere mid points with this clk will reach to every flip flop at almost same time. In the same way we will connect the clk2 with flip flops like midpoint manner.
 
![image](https://github.com/user-attachments/assets/4dfe2068-d0ae-475f-964c-46c1a1f6d022)

Now will se clock tree synthesis(Buffering), Let's we have some clock route through which it has to reach to particular locations and clock end points and in the path many capacitance, resitors are there.

![image](https://github.com/user-attachments/assets/d672934d-5295-4631-b38e-8ea492f8802d)

Because of the wire length we did not get the same wave form at ouput as input and bcz of RC networks , so to resolve this problem we use repeaters.
The only difference between the repeaters we use for clock or for data path is that clock repeaters repeaters will have equal rise and fall time.

First step is we will remove the clock route and place 2 repeaters and allow the clock to go through this particular repeater, in this case whatever wave form is generated here will go to the output. So we can as many as repeaters we want to make the continuous flow of th clock till the output.

![image](https://github.com/user-attachments/assets/63f57776-6953-476c-b51d-d906a147d695)

### <h4 id="header-4_3_2">Crosstalk and clock net shielding</h4>

**Clock Net Shielding:-** Till now we have built the clk tree in such a fashion that the skew between the launch flop and capture flop  is 0. Skew means the latency difference between clk ports of the flop pins.
Clk net shielding is the critical net scene in the design. We take the particular clk net and shield it means we protect the clk from the outside world, it's like house for tha clk. 

![image](https://github.com/user-attachments/assets/e0e2c89b-72d9-48c0-9ca4-7649480a653e)


If we do not protect the clk then two types of problem we can face **Glitch** and **Delta delay**

Let's consider on of the clk net. So whenever there is switching activity happening at the aggraser because of the coupling capacitance between the wires and this capacitance is so strong that any activity happening at the aggraser will directly impact the net which is close. 

![image](https://github.com/user-attachments/assets/cb5ddeff-7443-4659-a39e-2a4f1778b4bc)

The shielding is the technique, by which we can protect the net from these problems. In a shielding, we put wire between the either two wire where coupling capacitance is generate. This extra wire is grounded or connected to VDD.

We see the amount of delta delay because of the bump when we are switching from logic '1' to logic '0'. And skew is not anymore 0 here. So the impact of crosstalk delta delay is that it make the skew value non-zero.

![image](https://github.com/user-attachments/assets/4342f7dc-3fd4-42b0-9586-dea16c53a3c8)

By shielding we are breaking the coupling capacitance between the aggraser and victim. Shields don't switch.


## Timing analysis with real clock using openSTA
### <h4 id="header-4_4_1">Setup timing analysis using real clocks</h4>

Circuit tree looks little bit different than ideal clock with real clock here we have buffers,wires etc Clock reach to launch flop and capture flop through a set of buffers.So clock signal will not reach to the buffer at t=0 time due to these buffers. So the combinational circuit equation will be  (θ+1+2)<(T+1+3+4). Initially it was θ<T.

![image](https://github.com/user-attachments/assets/015efdc7-c2c8-4e4d-abdb-8db827d3ab90)


Let's called "1+2"=∆1 and "1+3+4"=∆2 and (∆1-∆2)=skew

![image](https://github.com/user-attachments/assets/5c02e340-e81e-41aa-ba53-885db276b5d8)

And here also, we have to consider the propogation skew (s) and uncertainty delay (US). so final equaltion becomes like, (θ+∆1)<(T+∆2-S-US).

we can also say that (θ+∆1)= data arrival time and (T+∆2-S-US)=data required time.
If (Data required time)- (Data arrival time) = +ve then it is fine. If it is -Ve then it is called 'slack'.

**Hold timing analysis:-** It is littel bit different then setup timing analysis. here we are sending the first pulse to the both launch FLop and capture flop.

Hold condition state that, Hold time (H)< combinational delay (θ). So, (θ>H).

![image](https://github.com/user-attachments/assets/43349698-0cdf-425d-a14b-7b3199c13257)


Hence, finite time 'H' required for 'Qm' to reach Q i.e., internal delay of mux2= hold time.

Now, if we add the real time clock, the equation will be change. now equation becomes (θ+∆1)>(H+∆2).

![image](https://github.com/user-attachments/assets/dde0cba3-e922-4bc5-83e3-4609ee238bd4)

### <h4 id="header-4_4_2">Hold timing analysis using real clocks</h4>

Combinational delay should be grater then the hold time of the capture flip flop. Once the clk reaches the launch flop it takes ariund 2buffer delay(∆1) and when it reaches to the capture flip flop it takes around 3 buffer delay(∆2). Uncertainity will be same for both the flip flops becaiuse clock applied to both the flops from the same edge only. Now let's add the uncertainity value to it.



Slack= Data ariival time - data required time. Slck either should be positive or 0. If slack goes to negative  it is refer to as voilation



Let's identify the timing paths from design, with single clock 

![image](https://github.com/user-attachments/assets/3a48e049-1ac0-4a29-9387-40bf6d6cf85b)

# LABS
1. Fix up small DRC errors and verify the design is ready to be inserted into our flow.
```bash
cd Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign

magic -T sky130A.tech sky130_inv.mag &
```
Conditions to be verified before moving forward with custom designed cell layout:

Condition 1: The input and output ports of the standard cell should lie on the intersection of the vertical and horizontal tracks.
Condition 2: Width of the standard cell should be odd multiples of the horizontal track pitch.
Condition 3: Height of the standard cell should be even multiples of the vertical track pitch.

```bash
# To understand the syntax
help grid
```
```bash
# Setting grid values
grid 0.46um 0.34um 0.23um 0.17um
```
Grid

![Screenshot from 2025-02-20 20-46-16](https://github.com/user-attachments/assets/a44886f7-8faa-478a-b993-d8b35cbb6173)



```math
Horizontal\ track\ pitch = 0.46\ um
```
```math
Width\ of\ standard\ cell = 1.38\ um = 0.46 * 3
```
```math
Vertical\ track\ pitch = 0.34\ um
```
```math
Height\ of\ standard\ cell = 2.72\ um = 0.34 * 8
```
```bash
save sky130_vsdinv.mag
```
Open the newly saved layout using
```bash
magic -T sky130A.tech sky130_vsdinv.mag &
```

![Screenshot from 2025-02-20 20-50-26](https://github.com/user-attachments/assets/2a9ef929-28b1-4fa5-837c-d33e4ffc4237)

2. Generate lef from the layout.

![Screenshot from 2025-02-20 20-51-25](https://github.com/user-attachments/assets/e32d7666-f549-4d07-9ef8-0c10ba674988)

```bash
lef write
```
3. Copy lef and lib files to /Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/
```bash
cp sky130_vsdinv.lef ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/
```
```bash
ls ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/
```
```bash
cp libs/sky130_fd_sc_hd__* ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/
```
```bash
ls ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/
```
![Screenshot from 2025-02-20 20-52-55](https://github.com/user-attachments/assets/3f766eee-fbba-4df1-a848-ffaab8fd874a)


Open picorv32A/config.tcl with GVIM


Edit config.tcl to this 

![image](https://github.com/user-attachments/assets/d4b70c89-4bae-4bbc-bd49-6037279e24a8)


Now perform steps to open OPENLane and prep picorv32a.

Include newly added lef to flow using
```bash
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
```
Run synthesis

![Screenshot from 2025-02-20 21-05-21](https://github.com/user-attachments/assets/4e4719e7-4da3-49ab-a35e-3ee122e2447c)

Perform these modifications
```bash
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
echo $::env(SYNTH_STRATEGY)
set $::env(SYNTH_STRATEGY) "DELAY3"
echo $::env(SYNTH_BUFFERING)
echo $::env(SYNTH_SIZING)
set $::env(SYNTH_SIZING)1
echo $::env(SYNTH_DRIVING_CELL)
run_synthesis

```


Run synthesis

Negative slack becomes 0

![image](https://github.com/user-attachments/assets/2ea9d87c-7f73-407a-8e0c-3dbdd4e30ae0)

```bash
run_floorplan
```

![Screenshot from 2025-02-20 21-09-01](https://github.com/user-attachments/assets/16a2babe-6a22-4c7a-90dc-4b675513106f)


Next we run placement


Open placements results using
```bash
cd /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/21-01_15-14/results/placement/

# Command to load the placement def in magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
```
![Screenshot from 2025-02-20 21-13-09](https://github.com/user-attachments/assets/8c2999e8-03b6-463d-ba16-573b2c753e45)


Expand to view internal activity of layers

![Screenshot from 2025-02-20 21-13-24](https://github.com/user-attachments/assets/0b137b11-24ee-4c96-ba11-47afb8567abe)


