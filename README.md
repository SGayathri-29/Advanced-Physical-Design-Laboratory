# **Advanced-Physical-Design-Workshop-using-openlane**
![image](https://user-images.githubusercontent.com/86550945/124319708-425f8400-db98-11eb-8584-fb76342d90d7.png)


## ABOUT THIS WORKSHOP

   This workshop is about the physical design flow right from the RTL netlist to the GDS II and this is done with the help of opensource software **openlane**.
   The tool uses the Google Skywater 130nm PDK files for its implementation.
---

##  **Day1**  -  *Foundation Of Opensource EDA,openLANE and sky130 PDK*
##  **Day2**  -  *Floor plan and Library cells*
##  **Day3**  -  *Design Layout cell using Magic and ngspice characterisation*
##  **Day4**  -  *Prelayout Timing Analysis and importance of good clock tree*
##  **Day5**  -  *Final steps for RTL2GDS using tritonRoute and openSTA*

# **DAY 1**

## *Foundation Of Opensource EDA,openLANE and sky130 PDK*
![image](https://user-images.githubusercontent.com/86550945/124321845-ff071480-db9b-11eb-991c-0a4d9d2d4c5b.png)



### 

## config.tcl file
![image](https://user-images.githubusercontent.com/86550945/124233183-36d87280-db30-11eb-9889-17dfaff181a8.png)


##every design contains...
![image](https://user-images.githubusercontent.com/86550945/124230974-55893a00-db2d-11eb-8502-7620b848353d.png)
![image](https://user-images.githubusercontent.com/86550945/124231099-79e51680-db2d-11eb-8e95-575ab573a9ac.png)


##cd ing openlane
![image](https://user-images.githubusercontent.com/86550945/124228983-929ffd00-db2a-11eb-8d6a-a99e9bae1e3c.png)


##.flow.tcl
![image](https://user-images.githubusercontent.com/86550945/124228779-5076bb80-db2a-11eb-9b43-cea0de4599e6.png)

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




