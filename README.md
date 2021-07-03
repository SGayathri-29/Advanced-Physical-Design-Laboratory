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

***FOR SYNTHESIS***

**Yosys**     - Performs synthesis of our RTL design.

**abc**        - Performs abc mapping  to map the  technology files  to the standard cells following the description in PDK.dff mapping also does the  same function.

**OpenSTA** -  Performs the static timing analysis of our obtained netlist.

**Fault**   –  Performs testing of the faults, insertion of scanchains and fault modelling can be performed here.

***FOR FLOORPLANNING:***

**Ioplacer**- Performs the Placing of the input and output ports

 **Init_fp** - Performs the definition of the core area in our chip.

  **RePLace** - Performs global placement
  
  **OpenDP**  - Performs Detailed Placement
  
 **Resizer** - Performs Optimisation of the design which can be optional.
 
 ***FOR CTS***
 
 **TritonCTS** -  Performs Synthesis of the Clock tree that is present all over the design.
 
 ***Routing***
 
 **SPEF-Extractor** - Performs extraction SPEF . 
 
 **FastRoute**      - Performs Global routing.
 
 
***GDSII FILE GENARATION***

**Magic**         -   It provides us the final GDSII layout file 



## **STARTING WITH OPENLANE**(invoking openlane)

The following steps are performed for the invoking of openlane,every time we perform our physical design we are supposed to invoke openlane by performing the following steps.We have to give ```docker``` command before starting .

```cd openLANE```

 This command is used in calling our required directory,in this case it is openlane directory 
 
![image](https://user-images.githubusercontent.com/86550945/124228983-929ffd00-db2a-11eb-8d6a-a99e9bae1e3c.png)

```./flow.tcl -interactive ```

We basically have two modes for running our openlane flow ,they are interactive and automated,we are using interactive flow ,we give the above mentioned keyword for running in interactive mode.

![image](https://user-images.githubusercontent.com/86550945/124228779-5076bb80-db2a-11eb-9b43-cea0de4599e6.png)

Every design folder contains a src folder , library files and config files in it,we have considered picorv32a for our synthesis ,so the following are the files present in the picorv32a design folder.

![image](https://user-images.githubusercontent.com/86550945/124230974-55893a00-db2d-11eb-8502-7620b848353d.png)

![image](https://user-images.githubusercontent.com/86550945/124352349-631ded00-dc1d-11eb-9fc1-404b566c4357.png)

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

## **SYNTHESIS:

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

## *timing report*
                                         

![image](https://user-images.githubusercontent.com/86550945/124233815-de55a500-db30-11eb-99a6-585f96ce5401.png)

## *slew report*


![image](https://user-images.githubusercontent.com/86550945/124233893-fa594680-db30-11eb-917e-548e6c8b5594.png)


# **DAY 2**

## *Floor Planning and Library Cells*

CHIP FLOOR PLANNING CONSIDERATIONS

1.Definition of core and die width and height

2.Locations of preplaced cells

3.Placement of decoupled capacitors

4.Pin placement

5.Logical cell placement blockage

Definition of core and die width and height: The core and die area depends on the dimensions of logic gates,hence the dimensions of the chip.The dimensions of the core and die is also dependent on the standard cell dimensions.The wires doesn't contribute to these dimensions.

Utilization factor :Utilization factor is defined as the area occupied by the netlist defined circuit in the core.Itt can be calculated as

 Utilizaion factor = Area occupied by the netlist
                    --------------------------------
                     Total area of the core
                     


Aspect ratio : Aspect ratio can specify the shape of the chip. An aspect ratio of 1 discribes the chip as a square else it is a rectagle.Aspect ratio can be calcuated by

 ![image](https://user-images.githubusercontent.com/86550945/124356204-68396700-dc32-11eb-8b9a-55bb78619f93.png)
 
 ![image](https://user-images.githubusercontent.com/86550945/124356259-adf62f80-dc32-11eb-92d1-fbb8e0f91971.png)



```run_floorplan```

This command is used for running the floorplan

![image](https://user-images.githubusercontent.com/86550945/124354710-ef82dc80-dc2a-11eb-8594-69df02098faa.png)

Our final floorplan looks like this:

![image](https://user-images.githubusercontent.com/86550945/124355185-8bade300-dc2d-11eb-8ba7-4b134396d8b1.png)

We have to click on the floorplan -> press 'S' 2 times -> right and left click on the mouse ->Press 'Z',then we can zoom our floorplan

![image](https://user-images.githubusercontent.com/86550945/124355356-4d64f380-dc2e-11eb-80fa-06a706cfdd02.png)

Tckn console that appears when we open our floorplan ,we can view the parameters we desire by giving some keywords in this console,

![image](https://user-images.githubusercontent.com/86550945/124355413-974dd980-dc2e-11eb-8de8-af94bed86b04.png)








