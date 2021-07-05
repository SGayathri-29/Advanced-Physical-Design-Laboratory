# **Advanced-Physical-Design-Workshop-using-openlane**
![image](https://user-images.githubusercontent.com/86550945/124319708-425f8400-db98-11eb-8584-fb76342d90d7.png)


## ABOUT THIS WORKSHOP

#### This workshop is about the physical design flow right from the RTL netlist to the GDS II and this is done with the help of opensource software **openlane**. The tool uses the Google Skywater 130nm PDK files for its implementation.
---
##  TABLE OF CONTENTS 

##  **Day1**  -  *Foundation Of Opensource EDA,openLANE and sky130 PDK*
```
1.How to talk to computers
2.Interface of the software applications to the hardware
3.Asic Design Flow
4.Openlane flow
5.Starting with openlane.
6.Synthesis
```
##  **Day2**  -  *Floor plan and Library cells*
```
1.Chip Floorplanning consideration.
2.Placement
```
##  **Day3**  -  *Design Layout cell using Magic and ngspice characterisation*
```
1.Cell Design Flow
2.Spice Deck
3.16 MASK CMOS process
4.Simulation of a CMOS inverter using ngspice
5.Checking of DRC errors
6.PEX Extraction
```
##  **Day4**  -  *Prelayout Timing Analysis and importance of good clock tree*
```
1.Extraction of LEF files
2.Fixing of slack violations
3.Clock Tree Synthesis
4.Timing Analysis using openSTA
```

##  **Day5**  -  *Final steps for RTL2GDS using tritonRoute and openSTA*
```
1.Power Distribution Network
2.Routing
3.SPEF Extraction
4.GDSII
```

# **DAY 1**
## *Foundation Of Opensource EDA,openLANE and sky130 PDK*

### **HOW TO TALK TO COMPUTERS**

 IC (Integrated Circuit) is a unit  where all the electronics components which are needed for a certain function is present. The electronic  components  including   resistors, transistors, capacitors, and diodes are interconnect to perform a given function.This single integrated circuit can have millions of such circuits inside    it depending upon the computational power.

![image](https://user-images.githubusercontent.com/86550945/124346052-458b5c00-dbfa-11eb-9317-0e62b3744908.png)

 For example, we take an `Arduino board `  which is a microcontroller based board which has in it power port, microcontroller, analog input pins,digital pins and IC and so on, So the important thing which we need to concentrate on is the IC which is present inside the board.It is this IC which can be  consisdered as the brain of the board,i.e,it is responsible for all the functions.

And generally it somewhat looks like as shown in the below figure,wherein it consists of seversl foundry IP's ,macros etc.

![image](https://user-images.githubusercontent.com/86550945/124346725-0828cd80-dbfe-11eb-8ea5-c248473f895b.png)


### **INTERFACE OF THE SOFTWARE APPLICATIONS TO HARDWARE**

Inorder to interface software and hardware i.e to run an application software on a hardware we have to tarnslate the highlevel language which is understandable by humans to a machine level code which machines can understand.This is done by system software which comprises of:
```
1.Operating System
2.Compiler
3.Assembler
```
![image](https://user-images.githubusercontent.com/86550945/124347216-0e6c7900-dc01-11eb-94c2-ac739f6309a8.png)

The Operating System does the process of conversion of  high level applications  into assembly language program and also takes care of input, output functions.The compiler converts the codes written in  programming language such as(java ,R,etc.) to hardware instructions and saves them as an .exe file.Finally,the Assembler converts the compiler instructions to a machine language which the machine can understand.

### **ASIC DESIGN FLOW**

ASIC- Application Specific Integrated circuit is a IC where the chip is customised according to the application,it involves a design flow for attaining the final expected module.For this flow three components are very important which are EDA tool,RTL design and PDK information.

![image](https://user-images.githubusercontent.com/86550945/124347464-97d07b00-dc02-11eb-80e0-588e67e11800.png)

**The steps of the ASIC Design flow are as follows:**

```Step 1: Synthesis```: It is the  process where our RTL code is converted to netlist,where the desired circuit behaviour is turned into a design implementable form.

```Step 2: Floor Planning and Power Planning``` : In this step the area,i.e the silicon area which is ocuupied by the chip is planned ,it involves preplacing of cells,it also decides the location of IO pads.Power planning is basically how much power to provide for every macros, standard cells, and all other cells that are present in the design.

```Step 3: Placement``` : Placement is  process of defining correct positions to predesigned cells on the chip .It involves placing the gate level netlist cells on the virtual rows,the cells are placed closely inorder to avoid delay and to acheive optimization.

```Step 4: Clock Tree Synthesis```: The clock is distributed allover the module, the CTS involves routing of the clock to all the sequential elements properly such that it avoids clock skew.

```Step 5: Routing```: Routing is distributing of  wires in the routing space that connects the nets in the netlist by following the design rules for the metals and vias.
which are specified in the respective PDKS.

### OpenLANE FLOW - ASIC 

Openlane is an opensource tool which is developed for the Physical design flow.Openlane is dependent on various tools such as  GTK wave,Yosys,abc,Klayout,magic etc,. Here the entire flow from RTL Design synthesis and  to the final GDSII is performed . The PDKs are being introduced to support the flow of the total design . 

The complete flow of the openLANE tool is as follows:

![image](https://user-images.githubusercontent.com/86550945/124348595-6490ea80-dc08-11eb-8b07-c0cde954cfc3.png)

Opensource tools that are used in our flow and its definitions:

```FOR SYNTHESIS```

**Yosys**     - Performs synthesis of our RTL design.

**abc**        - Performs abc mapping  to map the  technology files  to the standard cells following the description in PDK.dff mapping also does the  same function.

**OpenSTA** -  Performs the static timing analysis of our obtained netlist.

**Fault**   –  Performs testing of the faults, insertion of scanchains and fault modelling can be performed here.

``` FOR FLOORPLANNING ```

**Ioplacer**- Performs the Placing of the input and output ports

 **Init_fp** - Performs the definition of the core area in our chip.

  **RePLace** - Performs global placement
  
  **OpenDP**  - Performs Detailed Placement
  
 **Resizer** - Performs Optimisation of the design which can be optional.
 
 ``` FOR CTS ```
 
 **TritonCTS** -  Performs Synthesis of the Clock tree that is present all over the design.
 
 ``` ROUTING ```
 
 **SPEF-Extractor** - Performs extraction SPEF . 
 
 **FastRoute**      - Performs Global routing.
 
 
``` GDSII FILE GENARATION ```

**Magic**         -   It provides us the final GDSII layout file 



## **STARTING WITH OPENLANE**(invoking openlane)

The following steps are performed for the invoking of openlane,every time we perform our physical design we are supposed to invoke openlane by performing the following steps.We have to give ```docker``` command before starting .

```cd openLANE```

 This command is used in calling our required directory,in this case it is openlane directory 
 
![image](https://user-images.githubusercontent.com/86550945/124228983-929ffd00-db2a-11eb-8d6a-a99e9bae1e3c.png)

```./flow.tcl -interactive ```

We basically have two modes for running our openlane flow ,they are interactive and automated,we are using interactive flow ,we give the above mentioned keyword for running in interactive mode.

![image](https://user-images.githubusercontent.com/86550945/124228779-5076bb80-db2a-11eb-9b43-cea0de4599e6.png)

Every design folder contains a src folder , library files and config files in it,we have considered picorv32a for our synthesis.

![image](https://user-images.githubusercontent.com/86550945/124396016-de1dfb00-dd24-11eb-9f45-eba46156e9bd.png)


**configuration file** :

This file bypasses any configuration that has been already done into the plane.The below image is how a config file looks like,

![image](https://user-images.githubusercontent.com/86550945/124233183-36d87280-db30-11eb-9889-17dfaff181a8.png)

```package require openlane```

This command inputs the packages that are required to run the flow.

![image](https://user-images.githubusercontent.com/86550945/124229597-794b8080-db2b-11eb-9ffe-6e8aea438a93.png)

```prep -design design name```

   eg: for our design it is ```prep  -design picorv32a```
  
  This command is given for merging cell level LEF files and Tech level LEF files
  
![image](https://user-images.githubusercontent.com/86550945/124229736-b283f080-db2b-11eb-9d73-a19d896c89fc.png)

We can see that our design is mapped with the techfiles i.e abc libmapping is done over here.

![image](https://user-images.githubusercontent.com/86550945/124230484-b06e6180-db2c-11eb-8fca-17fee5047f75.png)

## **SYNTHESIS** :

```run_synthesis```

![image](https://user-images.githubusercontent.com/86550945/124353460-4a650580-dc24-11eb-8a61-4e104d7c81af.png)

 
 This command runs the synthesis of our design and this done with the help of yosys
 
The Synthesis has been completed successfully

![image](https://user-images.githubusercontent.com/86550945/124353802-623d8900-dc26-11eb-948a-bf954126cd69.png)


After the entire synthesis is complete we can check our timing ,dff and slew and many reports along with the netlist are present  in runs folder which is present in our design folder

The synthesised netlist looks like this:
![image](https://user-images.githubusercontent.com/86550945/124353609-2b1aa800-dc25-11eb-900e-6f1aae7059ad.png)

We can find our reports in the reports folder which is shown below

![image](https://user-images.githubusercontent.com/86550945/124353747-eba08b80-dc25-11eb-9080-7e540833fc68.png)

## *dff stats*                                                                                            

![image](https://user-images.githubusercontent.com/86550945/124354024-851c6d00-dc27-11eb-969b-a95e56dfb222.png)

     Flop ratio = No. of D flipflops 

                ----------------------
          
                  Total No. Cells  
              
 Now,the flop ratio present in our design can be calculated as
 
 S0 ,we see that our dflipdlop count is 1613

 ![image](https://user-images.githubusercontent.com/86550945/124356204-68396700-dc32-11eb-8b9a-55bb78619f93.png)
 
  and the no.of cells present in the design are 14876
  
 ![image](https://user-images.githubusercontent.com/86550945/124356259-adf62f80-dc32-11eb-92d1-fbb8e0f91971.png)
 
 So by, dividing both we get, 1613/14876 =0.108 ,Hence our flop ratio is 0.108

## *timing report*
                                         

![image](https://user-images.githubusercontent.com/86550945/124233815-de55a500-db30-11eb-99a6-585f96ce5401.png)

## *Max slew report*


![image](https://user-images.githubusercontent.com/86550945/124233893-fa594680-db30-11eb-917e-548e6c8b5594.png)


# **DAY 2**

## *Floor Planning and Library Cells*

## CHIP FLOOR PLANNING CONSIDERATION:

Floorplan in simple terms is basically transforming our design netlist into a layout.There are somefactors that we need to consider before we do floorplanning

```1.Definition of core and die width and height```: The dimensions of the chip The core and die area depends on the dimensions of the basic logic gates present in the design.


*Utilization factor* : Utilization factor is given as the area occupied by the netlist defined circuit in the core.It is basically the ratio of the  Area occupied by the netlist and total area of the core.

    Utilizaion factor =  Area occupied by the netlist   
 
                        -----------------------------
                  
                          Total area of the core 
                         
                     
*Aspect ratio* : Aspect ratio basically tells us about the shape of the chip,If the ratio is 1 then it is considered as square shaped one,anything other that 1 is considered to be in the shape of a rectangle.

    Aspect ratio =   Height 

                    --------
                 
                     Width

```2.Defining location of the preplaced cells:```

In Electronic circuits, some part of the circuit,a smaller module can be implemented once and instantiated many times,so basically the logic of that smaller module is functionally implemented only once. These logic has its corresponding input and output and they are blackboxed and a part of the toplevel netlist.Since the logic of these cells are implemented only and done before placement and routing it is called as **preplaced cells**

```3.Using Decoupling capacitors```

In our design some cells may be physically faraway from the supplyvoltage,so we may not get the expected ouput and also we can get a problem of crosstalk. This happens becuase it does not receive the entire voltage as it travels along a long path which contains an inbuilt resistance .To avoid this, we  use a decoupling capacitor.
The decoupling capacitors are fully charged capacitors and that are almost equal to that of the supply voltage.These decaps are placed closed to the circuit .These decaps prevents the circuit from entering into the grey area.

```4.Powerplanning```

We have to make sure that the power is being transmitted properly to the blocks without any delay or disruption. During power planning, power lines and ground straps are laid in  a way that they form a mesh structure and each cell can tap power to respective rails.

```5.Pin Placement```

The connectivity information is given in the form of netlist,which specifies the RTL connectivity ,and the pins are placed accordingly.Here the clock ports are larger than others as they drive the entire circuit in the chip and also they need the least resistance path.

```6.Logical cell placement blockage```

In the outerarea of the logic cells are blocked since it is reserved only for the input ,output pins .This blockage ensures that no other elements other than input,output and clockports are present there.

 The next step after synthesis  is the floorplan, and the command is;

```run_floorplan```

This command is used for running the floorplan

![image](https://user-images.githubusercontent.com/86550945/124354710-ef82dc80-dc2a-11eb-8594-69df02098faa.png)

We use magic for viewing the floorplan,

To view the floorplan on Magic,the following inputs are needed:

1.Magic technology file
2.def file of floorplan 
3.Merged LEF file
```
magic -T /home/Desktop/username/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef/ def read picorv32a.floorplan.def &
```

Our final floorplan looks like this:

![image](https://user-images.githubusercontent.com/86550945/124355185-8bade300-dc2d-11eb-8ba7-4b134396d8b1.png)

We have to click on the floorplan -> press 'S' 2 times -> right and left click on the mouse ->Press 'Z',then we can zoom our floorplan

![image](https://user-images.githubusercontent.com/86550945/124355356-4d64f380-dc2e-11eb-80fa-06a706cfdd02.png)

Tkcon console that appears when we open our floorplan ,we can view the parameters we desire by giving some keywords in this console,

![image](https://user-images.githubusercontent.com/86550945/124396753-1fb0a500-dd29-11eb-8209-b4efaf6941e2.png)



## **PLACEMENT**

After floorplanning, the placement of standard cells is done. The synthesized netlist OpenLANE does placement in two stages:

Global Placement - This is for generating  a rough placement that may violate some placement constraints.and is it not legal.It determines the routing resgion for each net.It minimizes the area and timing.

Detailed Placement - Determines exact route and layers of each net,it validates routing ,timing and area .The input for this is given by the global placement.

```run_placement```

![image](https://user-images.githubusercontent.com/86550945/124356457-b307ae80-dc33-11eb-956e-8d91a1dc22e4.png)


This command performs placement.

 Successful completion of placement
 
![image](https://user-images.githubusercontent.com/86550945/124356403-7b006b80-dc33-11eb-8750-2dc75def7c1a.png)

After placement we can check the placement.def file using magic as we did for the floorplan and it looks like this:

![image](https://user-images.githubusercontent.com/86550945/124431450-fd9d3e00-dd8d-11eb-9aca-eaa8ffbf033f.png)


# **DAY 3**

## *Design Layout cell using Magic and ngspice characterisationK*

## CELL DESIGN FLOW:

A cell as small as an inverter has to undergo many steps in the cell design flow.The important steps are as follows;

```
1.Read in the model files and tech files
2.Read extracted spice netlist.
3.Recognise the behaviour of the buffer.
4.Read the subscircuit.
5.Attach necessary power sources .
6.Stimulus application.
7.Give the necessary output capacitors.

```

## SPICE DECK

For simulation of the  standard cells, **Deck wrappers** are required to be generated with respect to the model files.Output waveform of the spice deck is plotted using ngspice . The steps followed to run the spice deck is as follows ,Source the .cir spice deck file using the  ```source spicedeck.cir```command .To run the spice file ```run``` command is used.  ```setplot``` allows to view plots .By entering the name of the simulation in the terminal display we do our desired simulation.The typical ngspice terminal looks like this where we have to enter our commands..

![image](https://user-images.githubusercontent.com/86550945/124397092-6e5f3e80-dd2b-11eb-8d6f-883e5dab453f.png)

## 16-mask CMOS process

_**Select a substrate**_ - Selection of a substrate  for our base .The whole chip is fabricated on this.This can be either p or n substrate.

_**Create active region**_ -Creation of  an insulating  layer by depositing SiO2 and Si3N2.Pockets are created using photoresist and lithography process.This photolithography process takes place from this.

_**Formation of N-well and P-well formation**_ - Both of n-well and p-well has to been grown simultaneously. Ion Implantation is used for this purpose,so ion implantation is basically forcing of the desired particles with  energy as high as 200 keV over that area creating an active layer .

_**Creating Gate terminal**_ - Gate terminal is an important terminal responsible for controlling our transistor and for turning it on .For the attaining  Desired threshold,doping Concentration and oxide thickness needs to be set which is taken care in this step.

_**Lightly Doped Drain  formation**_- A thin layer of n -implant or p -implant are deposited usch that they donot penetrate into the substrate.It is done to avoid short channel effect and hot electron effect.

_**Source and Drain formation**_- Drain and source are formed in this stage.

_**Contacts and local interconnect creation**_- Contacts and interconnects are important since only throught this the entire build can be controlled .In this we remove the thin screen oxide SiO2 layer which we used to avoid channeling is removed  using HF etching. Titanium is deposited using sputtering.

_**Higher Level metal layer formation**_- Upper metal layers are formed.Depositon of SiO2 in the first layer and in the second layer Aluminium is used and the contact holes are drilled.

After the entire 16 MASK CMOS fabrication process it looks like as follows:

![image](https://user-images.githubusercontent.com/86550945/124398081-686c5c00-dd31-11eb-9575-7460efe501c4.png)


## **SIMULATION OF A CMOS INVERTER USING ngspice** 

The inverter cell what we are trying to simulate a lot of time to build from scratch so we are downloading it from github and after layout simulation and characterizing this design is plugged into our main design that is ```picorv32a```

the file it gitcloned from:
```git clone https://github.com/nickson-jose/vsdstdcelldesign.git```

The tech file for the magic that is inside  the pdk directory is copied to the vsdstdcelldesign directory.

![image](https://user-images.githubusercontent.com/86550945/124429602-b746df80-dd8b-11eb-8786-c5ff831947d7.png)

After copying we can we that file in the vsdstdcelldesign directory:

vsdstdcelldesign directory

To view the layout using the opensource tool the following command is used:

![image](https://user-images.githubusercontent.com/86550945/124429748-e3626080-dd8b-11eb-9215-4a0e4de13f6b.png)

```magic -T sky130A.tech sky130_inv.mag &```

The layout looks like this:

![image](https://user-images.githubusercontent.com/86550945/124429846-042ab600-dd8c-11eb-8826-416281d9af39.png)

We can click on the layout at any point we want and if we press S the region gets selected ,if we press S for three times the entire port is selected as shown below

![image](https://user-images.githubusercontent.com/86550945/124430346-af3b6f80-dd8c-11eb-9f85-94478dc1bf7b.png)

If we select a certain block and type ```property``` in tkcon console which rightly appears when the magic is invoked ,it gives us the property of that particular cell we have selected

![image](https://user-images.githubusercontent.com/86550945/124430811-4274a500-dd8d-11eb-87a9-3003d079e610.png)

Similarly we can use a command ```box``` for viewing the cell's coordinates.

![image](https://user-images.githubusercontent.com/86550945/124431843-8ddb8300-dd8e-11eb-968e-e41329c40b19.png)

## CHECKING OF DRC ERRORS

DRC is basically Design Rule Check , and we can have drc errors if we donot follow the design rules, and the following picture shows us that we have not follwed the DRC rules,we can check that errors by clicking on DRC.

![image](https://user-images.githubusercontent.com/86550945/124431985-b5325000-dd8e-11eb-8e53-bc0ecd314782.png)

## PEX Extraction using Magic

For extract our inverter layout in spice ,use the command ```extract all ``` in the tkcon window

![image](https://user-images.githubusercontent.com/86550945/124433009-de9fab80-dd8f-11eb-8abf-1ff564279376.png)


Now  we can see that the files are extracted to our vsdstdcelldesign directory

![image](https://user-images.githubusercontent.com/86550945/124432658-7f419b80-dd8f-11eb-9941-4adb5a2952a2.png)

After this we use the following commands in the tkcon console :

```
ext2spice cthresh 0 rthresh 0
ext2spice
```
This ext file is for creating the spice file that is compatible with the ngspice tool.The parasitic capacitances have been removed and the file is extraced to spice.


![image](https://user-images.githubusercontent.com/86550945/124433611-90d77300-dd90-11eb-855e-6f11a91de6c6.png)

Now we can see that the spice file has also been added

![image](https://user-images.githubusercontent.com/86550945/124433755-bbc1c700-dd90-11eb-9e6b-9f9ad093dc6e.png)

Now we obtain the SPICE deck and it  is editted accordingly ,Since we are running transient analysis we edit the netlist obtained accordingly

![image](https://user-images.githubusercontent.com/86550945/124434379-6fc35200-dd91-11eb-8ce8-1ee90bec5c1e.png)

We use the following command for invoking ngspice 

``` ngspice sky130Ainv.spice```

![image](https://user-images.githubusercontent.com/86550945/124434580-a9945880-dd91-11eb-950b-afe12ca18460.png)

After this command is given we can view our output i.e the output we have obtained is the output of the inverter,and for plotting the transient analysis, we use the following command

```    plot y vs time a  ```

![image](https://user-images.githubusercontent.com/86550945/124461336-1fa6b880-ddae-11eb-994f-82a00afc89c5.png)

The following timing parameters are calculated.They are;

1.```Rise transition delay``` = It is the  time taken for the output signal to reach from 20% to 80% of maximum value.

2.```Fall transition delay``` = It is the  Time taken for the output signal to reach from 80% to 20% of maximum value.

3.```Cell rise delay```   = It is the time difference between 50% of rising output and 50% of falling output

4.```Cell fall delay``` = It is the time difference between 50% of falling output and 50% of rising output

We can calculate the rise transition delay for this circuit,for which we have to calculate 20% and 80% of the maximum value.

by zooming it in we can calculate  80%  of the maximum value.

![image](https://user-images.githubusercontent.com/86550945/124460278-cdb16300-ddac-11eb-8ae8-e2b64089eb21.png)

 and thereby 20% of the maximum value also,
  
![image](https://user-images.githubusercontent.com/86550945/124460090-8a56f480-ddac-11eb-8a5d-4232eb8680f3.png)

If we just click on that particular point we can view the coordinates;

![image](https://user-images.githubusercontent.com/86550945/124461230-fe45cc80-ddad-11eb-80ea-1ac979820c29.png)

# **DAY 4**

## *Prelayout Timing Analysis and importance of good clock tree*

## EXTRACTING  LEF FILES AND PLUGGING IT INTO OUR DESIGN.

The LEF contains basically the information of the input ,output ports,power line and grid lines.Extract LEF file out of .mag file. The extracted LEF file will be plugged into picorv32a flow.

Guidelines need to be followed while making standard cell set,such as ;

```1.The io ports must lie on the intersection of horizontal and vertical tracks.
   2.Width of the standard cells is the odd multiple of horizontal tracks pitch. 
   3.Height must be odd multiple of vertical tracks.
```

By its name Tracks are used during routing stage, Only over these routes the PNR tool can do routing.We can get the track information from the track.info file which is in the PDK files

![image](https://user-images.githubusercontent.com/86550945/124463610-c12f0980-ddb0-11eb-9a95-37e75fe01356.png)
 
For example,

li1 layer (X) -> the horizontal track's  offset is  0.23 and  pitch is 0.46

li1 layer (Y) -> the vertical track's  offset is 0.17 and  pitch is 0.34

and for metal1 both pitch and offset are same.

We have to converge the grid definiton according to the track definiton,for ensuring that we can reach the design from X and Y direction.The below tckcon console explains us how we can change the value of the grid .

![image](https://user-images.githubusercontent.com/86550945/124464478-de180c80-ddb1-11eb-9a64-6f110fa37594.png)

This is the layout of our inverter,we can see that it is surrounded with lots of boxes which are nothing but the grids.

![image](https://user-images.githubusercontent.com/86550945/124465077-9a71d280-ddb2-11eb-9afa-675232a6b7e6.png)

If we zoom it, we can see that, the input and output port A and Y are on the intersection of horizontal and vertical tracks as denoted by the arrow marks in the following figure.

![image](https://user-images.githubusercontent.com/86550945/124465570-33a0e900-ddb3-11eb-894c-8eb3b7bee32c.png)

Width of the standard cells is the odd multiple of horizontal tracks pitch , we can see that this rule is also satisfied as here it is calculated to be 3 which is an odd multiple.

![image](https://user-images.githubusercontent.com/86550945/124467199-284ebd00-ddb5-11eb-9eb6-11f1880e4643.png)

The ports will be considered as pins ,while extracting the LEF file 

To extract the lef file, the command used is ``` lef write```

![image](https://user-images.githubusercontent.com/86550945/124468002-36510d80-ddb6-11eb-9308-57e06c6db7d5.png)

And we can see that a new lef file is created in the vsdstdcelldesign directory.

![image](https://user-images.githubusercontent.com/86550945/124468447-bf684480-ddb6-11eb-9165-3f17550d94fb.png)

The below image is the generated LEF file .In the lef file we can see   that the ports is assigned as pins and the changes that were made in magic is reflected here

![image](https://user-images.githubusercontent.com/86550945/124468586-e888d500-ddb6-11eb-94e5-2966d93bc3c6.png)

Inorder to plugin this LEF file into picorv32a flow,  lef file and the library files has to be copied into the source folder of our design.

![image](https://user-images.githubusercontent.com/86550945/124469356-e410ec00-ddb7-11eb-952d-2051cb918c40.png)


In the config.tcl file The config.tcl file some modifications are made ,location of the LEF file and other files is given, and it looks like this,

![image](https://user-images.githubusercontent.com/86550945/124470226-fc353b00-ddb8-11eb-83a4-e180a89b31d3.png)

Now we run the entire flow again,

![image](https://user-images.githubusercontent.com/86550945/124475160-06f2ce80-ddbf-11eb-966c-e5e738f9161a.png)

To include the lef cells make sure we add the follwing commands

``` set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
    add_lefs -src $lefs 
```

 ##  FIXING OF SLACK VIOLATIONS
 
 Inorder to avoid negative slack as it is not ideal to our design, we optimize the slack values and maintain a positive value.Inorder to do this we set various environmental variables and check if the slack is changing or not as given in the following image.We can do the modifications in the ```README.md``` file present in the configuration directory
 
 These are the changes which has to been done to the environment variables and now the flow is run again
 
 ![image](https://user-images.githubusercontent.com/86550945/124478252-a2397300-ddc2-11eb-983d-66e6eb28c5c2.png)
 
 Now after doing this we can observe certain changes in the slack time.
 
  After this the floor plan is run and this is the floorplan we can observe that sky130_vsdinv is added to our design.
 
 ![image](https://user-images.githubusercontent.com/86550945/124475455-5cc77680-ddbf-11eb-8028-849abe03c510.png)

Move the cursor to sky130_vsdinv,press 'S' and in the tkcon window enter ```what```,we can see that it displays sky130_vsdinv

![image](https://user-images.githubusercontent.com/86550945/124475678-9bf5c780-ddbf-11eb-8d9a-10a5858a7731.png)

 and in the tkcon window enter `expand`. We can see how that particular cell has established connection to its adjacent cells.
 
 ![image](https://user-images.githubusercontent.com/86550945/124476066-0dce1100-ddc0-11eb-8f9f-2e8ace5771a5.png)
 

## CLOCK TREE SYNTHESIS.

Clock tree synthesis is a process which ensures that the clock signal gets distributed to all the sequential elements in the design to reduce the skew and latency.
During CTS, clock buffers are added to the clock signal path which  are different from normal buffers since they  have equal rise and fall times.After CTS one can observe that the slack value is increased.The below method shows how the clock is distributed for a small design.

![image](https://user-images.githubusercontent.com/86550945/124481400-dbbfad80-ddc5-11eb-81d9-a21a8360a561.png)


we use ```run_cts``` command for the clock tree synthesis in openlane.

![image](https://user-images.githubusercontent.com/86550945/124480008-74552e00-ddc4-11eb-949d-65efec1e92d9.png)

## TIMING ANALYSIS USING OPENSTA

The definition of our sta configuration file has to be done and run it for finding the timing parameters.

Conifg file:

![image](https://user-images.githubusercontent.com/86550945/124481563-07db2e80-ddc6-11eb-8ae1-27e603a21772.png)

The openSTA configuration file is invoked as follows;

![image](https://user-images.githubusercontent.com/86550945/124481850-5c7ea980-ddc6-11eb-8d07-0b47a47c4782.png)


# **DAY 5**

## *Final steps for RTL2GDS using tritonRoute and openSTA*

Commands for the entire flow:
```
1.run_synthesis 

2.init_floorplan 

3.place_io

4.global_placement_or

5.detailed_placement 

6.tap_decap_or detailed_placement

7.gen_pdn

8.run_routing
```

## POWER DISTRIBUTION NETWORK

Power Distribution network is basically a network for distributing the power across the entire circuit.By this it ensures that it carry current from the pads to the internal circuitry ,provide current return path and to maintain stable voltage.

``` % gen_pdn``` - command used for generating PDN.

![image](https://user-images.githubusercontent.com/86550945/124482733-3ad1f200-ddc7-11eb-8705-3b532f899bfa.png)

After completion:

![image](https://user-images.githubusercontent.com/86550945/124482853-5806c080-ddc7-11eb-8d93-b9c5002775be.png)

In the below image we see that the power and ground rails are built which is denoted by the blue lines,

![image](https://user-images.githubusercontent.com/86550945/124482988-7f5d8d80-ddc7-11eb-975f-c7a5751852af.png)

##  ROUTING

In this stage the interconnections  are made by determining the specific path for connecting the nets.We have many routing algorithms for determing the path for connecting the nets such as maze routing and steiner tree routing algorithms.As the routing process is very complex, routing is divided into two stages which are global routing and detailed routing

![image](https://user-images.githubusercontent.com/86550945/124483442-fa26a880-ddc7-11eb-8db0-56537a80e4df.png)

1.Global routing:
Here the routing region is divided into rectangular gridcells,It forms routing guides for the further routing .It basically forms a rough path of connection.

2.Detailed routing:
The detailed route determines the vias and segments accordingly with the global route solution.This ensures that routing happens within the routing guides.

In the below image we can see that there many routing guides which are used in the flow.

![image](https://user-images.githubusercontent.com/86550945/124484873-9604e400-ddc9-11eb-8536-2fc2eb75fe45.png)

So if we look into one of the routing guide it contains the following information.We can see that routing guides are basically rectangles and for one net there can be many routing guides.So the below file contains the four coordinates of the routing guides.

![image](https://user-images.githubusercontent.com/86550945/124485032-c77daf80-ddc9-11eb-8594-69b662638c8e.png)

To run routing in OpenLANE execute the command``run routing``

Now we can invoke magic and see our result

```
magic -T /home/Desktop/username/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef/ def read picorv32a.def &
```

![image](https://user-images.githubusercontent.com/86550945/124485892-a79abb80-ddca-11eb-9158-2c84f1bfff30.png)

if we select and expand we get the following image,which shows us that all the cells are connected and fillers are added

![image](https://user-images.githubusercontent.com/86550945/124485699-77ebb380-ddca-11eb-905d-894b583fee6f.png)

Now we can see that our final design contains sky130_vsdinv

![image](https://user-images.githubusercontent.com/86550945/124486279-0b24e900-ddcb-11eb-951b-4899a92a02ee.png)

## SPEF EXTRACTION


SPEF is Standard Parasitic Exchange Format.So once the routing is completed the interconnect parasitics are extraced using an SPEF generator .It performs sign-off post-route STA analysis. It consists of R,L,C in the ASCII format which can be seen in the below file.It is done after placement and routing.

![image](https://user-images.githubusercontent.com/86550945/124487252-1c222a00-ddcc-11eb-84c2-a30d11257d15.png)

## GDSII

GDSII is abbreviated as  "Geometrical data base standard for information interchange". Its the final  output file of the layout which will be sent to the fabs.


## Acknowledgements:

Kunal Ghosh, Co-founder (VSD Corp. Pvt. Ltd)

Nickson P Jose, Teaching Assistant (VSD Corp. Pvt. Ltd)

































  






























