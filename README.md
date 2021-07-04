# **Advanced-Physical-Design-Workshop-using-openlane**
![image](https://user-images.githubusercontent.com/86550945/124319708-425f8400-db98-11eb-8584-fb76342d90d7.png)


## ABOUT THIS WORKSHOP

#### This workshop is about the physical design flow right from the RTL netlist to the GDS II and this is done with the help of opensource software **openlane**. The tool uses the Google Skywater 130nm PDK files for its implementation.
---

##  **Day1**  -  *Foundation Of Opensource EDA,openLANE and sky130 PDK*
##  **Day2**  -  *Floor plan and Library cells*
##  **Day3**  -  *Design Layout cell using Magic and ngspice characterisation*
##  **Day4**  -  *Prelayout Timing Analysis and importance of good clock tree*
##  **Day5**  -  *Final steps for RTL2GDS using tritonRoute and openSTA*

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

CHIP FLOOR PLANNING CONSIDERATION:

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

 The next step after synthesis  is the floorplan. For that the below command is used

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

![image](https://user-images.githubusercontent.com/86550945/124356655-b8192d80-dc34-11eb-820a-717a03182820.png)


# **DAY 3**

## *Design Layout cell using Magic and ngspice characterisationK*

CELL DESIGN FLOW:

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

SPICE DECK

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














