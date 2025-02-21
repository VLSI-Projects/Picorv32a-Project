# RTL to GDS II flow  using tritonRoute and openSTA
### <h5 id="header-5_1_1">Introduction to Maze Routing – Lee’s Algorithm</h5>
**Maze-Routing(Lee's Algorithm):-** Therse should not be zig-zag lines of connections most of the connections should be in L shape or in Z shape. So according to algorithm first it create some grids and grids are routing at the backend. It's called as routing grid. There are some numbers of grids on this routig having some dimensions. SO here we are having two points one is 'Source' and the other is 'Target'. With the help of this routing grid algorithm has to find out the best possible way between them.

First step is algorithm tries to lable all of the grids surrounded. Only the adjacent horizontal and vertical grids are labeled not the digonal one as shown in the image below.Lee’s Algorithm i.e. Maze Routing, is, perhaps, the most widely used algorithm to find path between 2 points. Let’s have a glimpse of the algorithm using below images: Assume, we have to connect cell1 with cell2, as shown in below image:
![image](https://github.com/user-attachments/assets/ed12c972-6562-4628-a44d-b9437b57a03e)


The 3 steps to do this are:

*To identify the ‘Source’ and ‘Target’ pins for cell1 and cell2 and create Routing grid as shown below.
![image](https://github.com/user-attachments/assets/25d342a5-dc79-4fc0-bf0c-b2b254574149)


Now since, the data flows from cell1 to cell2, the output of cell1 becomes source ‘S’ and the input of cell2, becomes target ‘T’
The shortest and the least detoured path is back-traced from ‘T’ to ‘S’, shown in below images
![image](https://github.com/user-attachments/assets/f4007a26-8df0-4d46-9834-d6bf93a53c27)







### <h5 id="header-5_1_3">Design Rule Check</h5>

So in order to go to DRC we need to follow some steps which are called drc cleaning.

Let's take the example of the  circuit. Let's we have two parallel wires so the rule says that whenever we choose two wires there should be minimum distance between these two wires.

![image](https://github.com/user-attachments/assets/cf7a72d6-8745-4c3e-8396-aa05b5ae9d04)


**Rule 1) Wire width:-** Width of the wire should be minimum that derived from the optical wavelenth of lithography technique applied.

**Rule 2) Wire Pitch:-** The minimum pitch between two wire 

**Rule 3) Wire Spacing:-** The wire spacing between two wires should be minimal.

Let's take the other part for design rule check from the same example .

![image](https://github.com/user-attachments/assets/fded284e-27d4-44d3-8d6e-69ac571d4245)


Solution of this signal short problem is take one of the wire and put it on the other metal layer. usually upper metal is wider than the lower metal.

After this solution, we add two new DRC rules should be check.

**Rule 4) Via Width:-** via width should be some minimum value.

**Rule 5) Via Spacing:-** Via spacing should be minimum value.

After routing and DRC the next step is Parasitic extraction. Resistance and capacitance present on every wire should be extracted and use for further process.

![image](https://github.com/user-attachments/assets/363827c9-6e7d-4643-8215-82747966ca76)








## <h5 id="header-5_3">TritonRoute Features</h5>
### <h5 id="header-5_3_1">TritonRoute feature 1 - Honors pre-processed route guides</h5>

<ul>
	<li><a>Performs initial detailed route</a></li>
	</ul>

 <ul>
	<li><a>Hounors the prepocessed route guides(obtained after fast route)</a></li>
	</ul>


**Requirements of preprocessed guides**

1) Should have unit width

2) Should be in preferred direction

 <ul>
	<li><a>Assumes route guides for each net satisfy inter-guide connectivity</a></li>
	</ul>

 **Two guides are connected if**

 1) They are on the same metal layer with touching edges.

 2) They are on neighbouring metal layers with a non-zero vertically overlapped area.

 <ul>
	<li><a>Works on proposed MILP-based panel-routing scheme with intra-layer parallel and inter-layer sequential routing framework</a></li>
	</ul>

 
# LABS
1) Perform generation of Power Distribution Network (PDN) and explore the PDN layout.

Commands to perform all necessary stages up until now

```bash
cd Desktop/work/tools/openlane_working_dir/openlane
```
```bash
docker
```
```bash
./flow.tcl -interactive
```
```bash
package require openlane 0.9
```
```bash
prep -design picorv32a
```
![Screenshot from 2025-02-14 22-58-03](https://github.com/user-attachments/assets/19006744-c6b0-4fde-bf1e-59038d35c75d)


```bash
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
```
```bash
set ::env(SYNTH_STRATEGY) "DELAY 3"
```
```bash
set ::env(SYNTH_SIZING) 1
```


```bash
run_synthesis
```
![Screenshot from 2025-02-21 17-15-25](https://github.com/user-attachments/assets/318a74f9-e65a-4363-8431-8224dc075f5c)


```bash
init_floorplan
place_io
tap_decap_or
```
Running placement
```bash
run_placement
![Screenshot from 2025-02-21 17-21-26](https://github.com/user-attachments/assets/30c5d698-3a30-4de7-ba4b-3b165975004e)

```bash
unset ::env(LIB_CTS)
```
Running Clock Tree Synthesis (CTS)
```bash
run_cts
```
![Screenshot from 2025-02-21 17-20-53](https://github.com/user-attachments/assets/dbf3ad4d-9a4c-45ee-87c3-c8abf0d77423)
![Screenshot from 2025-02-21 17-21-26](https://github.com/user-attachments/assets/d389c660-779c-44ce-a251-1987dc654f16)

Generate the PDN
```bash
gen_pdn 
```
![Screenshot from 2025-02-21 17-41-40](https://github.com/user-attachments/assets/9d20eaeb-74ae-4e56-8d99-b16d347c4085)

Commands to load PDN def in magic in another terminal

```bash
# Change directory to path containing pdn def file
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/21-02-25/tmp/floorplan/
```
Open in magic
```bash
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read 14-pdn.def &
```
![Screenshot from 2025-02-20 21-13-09 (copy)](https://github.com/user-attachments/assets/d7770a27-5a29-439b-bee3-b159e3c6abab)

![image](https://github.com/user-attachments/assets/2ac06b50-24b6-4fa3-96eb-400ef054652d)



2) Perfrom detailed routing using TritonRoute and explore the routed layout.

Commands to run routing

```bash
# Check value of 'CURRENT_DEF'
echo $::env(CURRENT_DEF)

# Check value of 'ROUTING_STRATEGY'
echo $::env(ROUTING_STRATEGY)

# Command for detailed route using TritonRoute
run_routing
```
![image](https://github.com/user-attachments/assets/9a0b4d27-4a35-43ca-b462-414bf47218e2)



![image](https://github.com/user-attachments/assets/bc1b16c5-ecb4-425a-a29d-9e0db06f135f)


*Commands to load routed def in magic in another terminal*

Change directory to the one that contains the routing .def
```bash
# Change directory to path containing routed def
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/21-01_15-14/results/routing/
```
Open in magic.
```bash
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.def &
```
![image](https://github.com/user-attachments/assets/90189888-bbde-40c1-9eb4-07b3cca2afd0)

3) Post-Route parasitic extraction using SPEF extractor.

*Commands for SPEF extraction using external tool (not nescessary in new openlane)*
Github link: https://github.com/HanyMoussa/SPEF_EXTRACTOR
```bash
# Change directory to the one where you have cloned the github repo
cd Desktop/work/tools/SPEF_EXTRACTOR
```
```bash
# Extract the spef
python3 main.py /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/21-01_15-14/tmp/merged.lef /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/21-01_15-14/results/routing/picorv32a.def
```

4) Post-Route OpenSTA timing analysis with the extracted parasitics of the route.

Commands to be run in OpenLANE flow to do OpenROAD timing analysis with integrated OpenSTA in OpenROAD

```tcl
# Command to run OpenROAD tool
openroad
```
Read the .lef file we have created.
```bash
read_lef /openLANE_flow/designs/picorv32a/runs/21-01_15-14/tmp/merged.lef
```
![image](https://github.com/user-attachments/assets/3f0a8003-2e65-47dc-a77e-588ee7be1640)

read the .def file we have created.
```bash
read_def /openLANE_flow/designs/picorv32a/runs/21-02-2025/results/routing/picorv32a.def
```

```bash
write_db pico_route.db
```
```bash
read_db pico_route.db
```
Read the verilog file created in the synthesis step.
```bash
read_verilog /openLANE_flow/designs/picorv32a/runs/21-01_15-14/results/synthesis/picorv32a.synthesis_preroute.v
```
```bash
read_liberty $::env(LIB_SYNTH_COMPLETE)
```
```bash
link_design picorv32a
```


```bash
read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc
```


```bash
set_propagated_clock [all_clocks]
```
Read the spef file we just extracted(not nescessary in new openlane)
```bash
read_spef /openLANE_flow/designs/picorv32a/runs/21-01_15-14/results/routing/picorv32a.spef
```

```bash
report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4
```


# The final layout
![image](https://github.com/user-attachments/assets/4082fb14-dd93-4227-a6fe-9635cccb1609)
