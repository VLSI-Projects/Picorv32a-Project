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

 
