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

The following steps are performed for the invoking of openlane,every time we perform our physical design we are supposed to invoke openlane by performing the following steps

```cd openLANE```

 This command is used in calling our required directory,in this case it is openlane directory 
 
![image](https://user-images.githubusercontent.com/86550945/124228983-929ffd00-db2a-11eb-8d6a-a99e9bae1e3c.png)

```./flow.tcl -interactive ```

We basically have two modes for running our openlane flow ,they are interactive and automated,we are using interactive flow ,we give the above mentioned keyword for running in interactive mode.

![image](https://user-images.githubusercontent.com/86550945/124228779-5076bb80-db2a-11eb-9b43-cea0de4599e6.png)

Every design folder contains a src folder , library files and config files in it,we have considered picorv32a for our synthesis ,so the following are the files present in the picorv32a design folder.

![image](https://user-images.githubusercontent.com/86550945/124230974-55893a00-db2d-11eb-8502-7620b848353d.png)

![image](https://user-images.githubusercontent.com/86550945/124231099-79e51680-db2d-11eb-8e95-575ab573a9ac.png)


## config.tcl file
![image](https://user-images.githubusercontent.com/86550945/124233183-36d87280-db30-11eb-9889-17dfaff181a8.png)





##package require openlane
![image](https://user-images.githubusercontent.com/86550945/124229597-794b8080-db2b-11eb-9ffe-6e8aea438a93.png)
##prep -design
![image](https://user-images.githubusercontent.com/86550945/124229736-b283f080-db2b-11eb-9d73-a19d896c89fc.png)



##abc libmap
![image](https://user-images.githubusercontent.com/86550945/124230484-b06e6180-db2c-11eb-8fca-17fee5047f75.png)


##Synthesis is complete...![image](https://user-images.githubusercontent.com/86550945/124227549-7dc26a00-db28-11eb-8769-85caa3b94f13.png)

## dff stats
![image](https://user-images.githubusercontent.com/86550945/124233688-b8300500-db30-11eb-83df-340ec6c8ed25.png)
## timing report
![image](https://user-images.githubusercontent.com/86550945/124233815-de55a500-db30-11eb-99a6-585f96ce5401.png)
## slew report
![image](https://user-images.githubusercontent.com/86550945/124233893-fa594680-db30-11eb-917e-548e6c8b5594.png)




