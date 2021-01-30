# VSD-IAT Physical Design Workshop

<!-- TABLE OF CONTENTS -->
<details open="open">
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
         <li><a href="#installation">Installation</a></li>
      </ul>
    </li>
    <li>
      <a href="#about-the-workshop">About the workshop</a>
      <ul>
        <li>
          <a href="#basics">Basics</a>
          <ul>
            <li><a href="#rtl2gds">RTL2GDS</a></li>
            <li><a href="#openlane-flow">Openlane Flow</a></li>
          </ul>
        </li>
      </ul>
    </li>
    <li>
      <a href="#day-1-inception-of-open-source-eda">Day 1 Inception of Open Source EDA</a>
      <ul>
        <li><a href="#skywater-pdk-files">Skywater PDK Files</a></li>
        <li><a href="#invoking-openlane">Invoking OpenLANE</a></li>
        <li><a href="#package-importing">Package Importing</a></li>
        <li><a href="#design-folder">Design Folder</a></li>
        <li><a href="#design-folder-hierarchy">Design Folder Hierarchy</a></li>
        <li><a href="#configuration-files">Configuration Files</a></li>
        <li><a href="#prepare-design">Prepare Design</a></li>
        <li><a href="#synthesis">Synthesis</a></li>
      </ul>
    </li>
    <li>
      <a href="#day-2-chip-floorplanning-and-standard-cells">Day 2 - Floorplanning and Standard Cells</a>
      <ul>
        <li><a href="#aspect-ratio-and-utilization-factor">Aspect Ratio and Utilization Factor</a></li>
        <li><a href="#preplaced-cells">Preplaced Cells</a></li>
        <li><a href="#decoupling-capacitors">Decouping Capacitors</a></li>
        <li><a href="#power-planning">Power Planning</a></li>
        <li><a href="#pin-placement">Pin Placement</a></li>
        <li><a href="#floorplanning-with-openlane">Floorplanning with OpenLANE</a></li>
        <li><a href="#viewing-floorplan-in-magic">Viewing Floorplan in Magic</a></li>
        <li><a href="#placement">Placement</a></li>
        <li><a href="#viewing-placement-in-magic">Viewing Placement in Magic</a></li>
        <li><a href="#standard-cell-design-flow">Standard Cell Design Flow</a></li>
        <li><a href="#standard-cell-characterization">Standard Cell Characterization</a></li>
      </ul>
    </li>
    <li>
      <a href="#day-3-design-library-cell">Day 3 - Design Library Cell</a>
      <ul>
        <li><a href="#spice-simulations">Spice Simulations</a></li>
        <li><a href="#switching-threshold-of-a-cmos-inverter">Switching Threshold of a CMOS Inverter</a></li>
        <li><a href="#16-mask-cmos-process-steps">16 Mask CMOS Process Steps</a></li>
        <li><a href="#magic-layout-view-of-inverter-standard-cell">Magic Layout View of Inverter Standard Cell</a></li>
        <li><a href="#magic-key-features">Magic Key Features</a></li>
        <li><a href="#device-inference">Device Inference</a></li>
        <li><a href="#drc-errors">DRC Errors</a></li>
        <li><a href="#pex-extraction-with-magic">PEX Extraction with Magic</a></li>
        <li><a href="#spice-wrapper-for-simulation">Spice Wrapper for Simulation</a></li>
      </ul>
    </li>  
    <li>
      <a href="#day-4-layout-timing-analysis-and-cts">Day 4 Layout Timing Analysis and CTS</a>
      <ul>
        <li><a href="#an-introduction-to-lef-files">An Introduciton to LEF Files</a></li>
        <li><a href="#standard-cell-pin-placement">Standard Cell Pin Placement</a></li>
        <li><a href="#lef-generation-in-magic">LEF Generation in Magic</a></li>
        <li><a href="#including-custom-cells-in-openlane">Including Custom Cells in OpenLANE</a></li>
        <li><a href="#fixing-slack-violations">Fixing Slack Violations</a></li>
        <li><a href="#clock-tree-synthesis">Clock Tree Synthesis</a></li>
        <li><a href="#viewing-post-cts-netlist">Viewing Post-CTS Netlist</a></li>
        <li><a href="#post-cts-sta-analysis">Post-CTS STA Analysis</a></li>
      </ul>
    </li>
    <li>
      <a href="#day-5-final-steps-in-rtl-to-gdsii">Day 5 Final Steps in RTL to GDSII</a>
      <ul>
        <li><a href="#power-distribution-network-generation">Power Distribution Network Generation</a></li>
        <li><a href="#global-and-detailed-routing">Global and Detailed Routing</a></li>
        <li><a href="#spef-extraction">SPEF Extraction</a></li>
      </ul>
    </li>
    <li><a href="#contact">Contact</a></li>
    <li><a href="#acknowledgements">Acknowledgements</a></li>
  </ol>
</details>

## GETTING STARTED

   These are some of the things you would need to get started with the tools locally

### INSTALLATION
   For all the necessary information needed to get the latest version of the standalone OPENLANE build or the VSDflow build
   please visit https://github.com/nickson-jose/openlane_build_script
   
   #### OTHER RESOURCES
   1. Virtual Machine ---> e.x VirtualBox (Assuming you do not have Linux on your device)
   2. Linux based OS  ---> e.x Ubuntu OS
   3. 25GB+ Disk Space

<!-- ABOUT THE WORKSHOP -->
## ABOUT THE WORKSHOP
   PDKs are essentially files that decribe the fabrication process for the tools and they are closed-source. With the release of PDKs by Google and Skywater
   has lead to the advent of open-source ASIC design. OpenLANE is an automated RTL to GDSII flow based on several components including OpenROAD, Yosys, 
   Magic, Netgen, Fault, OpenPhySyn, SPEF-Extractor and custom methodology scripts for design exploration and optimization. OPENLANE rc6 version strives to
   complete the entire ASIC design flow with minimal human intervention. The goal is to make human-in-the-loop parameter to zero. This 5 day workshop aims at
   exploring the entire ASIC design flow using the OpenLANE tool along with the Skywater 130nm PDK. 
   
### BASICS
  One Day 1 we begin by understanding the entire RTL2GDS flow along with understanding the inner workings of Openlane flow
  
  Let's Review the RTL2GDS Flow
   #### RTL2GDS
  
  ![](/Images/RTL2GDS.png)
  
  1. Chip Specification:
     This step basically involves engineers creating an RTL/custom design based on the functionalities their system wishes to achieve. These specifications
     could be in the areas of Power, Area, Speed, etc
     
  2. Functional Verification:
     This process involves making sure the correctness of the RTL design/logic by performing behavioural simulation by passing an exhaustive list of test 
     vectorsvarious means of coverage like statement, expression, toggle, etc
     
  3. Synthesis:
     Synthesis generates a gate-level netlist of the RTL code generated in the first step keeping in mind all the timing constraints
  
  4. Chip Partitioning:
     Dividing the entire design into multiple functional blocks for performing hierarchical integration considering multiple factors like Power, Area, Speed
  
  5. DFT Insertion:
     Design for Test Insertion. It includes scan path insertion, built-in Self-Test, automatic test pattern generation
  
  6. Post-Synthesis STA Analysis:
     Performs setup and hold time analysis on different path groups.
  
  7. Floorplanning:
     It process of determining the position of the blocks around the entire layout of the chip. A good floorplan will have minimum area and easy routing paths
     
  8. Placement:
     Process for placing the standard cells 
  
  9. Clock Tree Synthesis:
     Clock tree synthesis is a process of building the clock tree and meeting the defined timing, area and power requirements. It helps in providing the 
     clock connection to the clock pin of a sequential element in the required time and area, with low power consumption.
     
 10. Routing: 
     It consists of global and detailed routing. In global routing, calculates the values for each net by determining the delay associated with the wire. 
     In detailed routing, the actual delays of wire is calculated by methods like timing optimization, clock tree synthesis, etc.
     
 11. Final Verification and GDS:
     Final verification includes checks like DRC(Design rule check), LVS(Netlist vs Schematic). GDSII is the file produced and used by the semiconductor
     foundries to fabricate the chip
  
  
   #### OPENLANE FLOW
  
  ![](/Images/openlane.flow.1.png)  
 
   OpenLANE flow consists of several stages. By default, all flow steps are run in sequence.
  
   1. Synthesis

  <ul>
      <li> Yosys - Performs RTL synthesis using GTech mapping</li>
      <li>abc - Performs technology mappin to standard cells described in the PDK. We can adjust synthesis techniques using different integrated abc scripts to get desired results</li>
      <li>OpenSTA - Performs static timing analysis on the resulting netlist to generate timing reports</li>
      <li>Fault – Scan-chain insertion used for testing post fabrication. Supports ATPG and test patterns compaction</li>
  </ul>

  2. Floorplan and PDN

  <ul>
      <li>Init_fp - Defines the core area for the macro as well as the rows (used for placement) and the tracks (used for routing)</li>
      <li>Ioplacer - Places the macro input and output ports</li>
      <li>PDN - Generates the power distribution network</li>
      <li>Tapcell - Inserts welltap and decap cells in the floorplan</li>
      <li>Placement – Placement is done in two steps, one with global placement in which we place the designs across the chip, but they will not be legal placement with some standard cells overlapping each other, to fix this we perform a detailed placement which legalizes the design and ensures they fit in the standard cell rows</li>
      <li>RePLace - Performs global placement</li>
      <li>Resizer - Performs optional optimizations on the design</li>
      <li>OpenPhySyn - Performs timing optimizations on the design</li>
      <li>OpenDP - Perfroms detailed placement to legalize the globally placed components</li>
  </ul>
  
  3. CTS

  <ul>
      <li>TritonCTS - Synthesizes the clock distribution network</li>
  </ul>

  4. Routing

  <ul>
      <li>FastRoute - Performs global routing to generate a guide file for the detailed router
      </li>
      <li>TritonRoute - Performs detailed routing from global routing guides</li>
      <li>SPEF-Extractor - Performs SPEF extraction that include parasitic information</li>
  </ul>

  5. GDSII Generation

  <ul>
      <li>Magic - Streams out the final GDSII layout file from the routed def</li>
  </ul>

  6. Checks

  <ul>
      <li>Magic - Performs DRC Checks & Antenna Checks</li>
      <li>Netgen - Performs LVS Checks </li>
  </ul>

<!-- Day 1 Inception of Open Source EDA -->
## Day 1 Inception of Open Source EDA

![](/Images/LAB1_ss4.png)
### Skywater PDK Files

We make sure that the PDK files are included and invoked by running the docker. 
**docker run -it -v $(pwd):/openLANE_flow -v $PDK_ROOT:$PDK_ROOT -e PDK_ROOT=$PDK_ROOT -u $(id -u $USER):$(id -g $USER) openlane:rc6**

### Invoking OpenLane

We invoke openlane by going to the /path_to_openlane_dir and typing in **./flow.tcl**. By passing the flag **-interactive** we can running it manually. To run the
entire flow automatically we pass the design along with it.

### Package Importing

Different software dependencies are needed to run OpenLANE. We import these by typing in the package command seen in the above picture.

### Design Folder

All designs run within OpenLANE are extracted from the openlane/designs folder.

### Prepare Design

Prep is used to make file structure for our design. We prepare the design by using the command prep as seen in the above image.
After running it a new directory structure created under the runs folder so to enable OpenLANE flow. This process merges the technology LEF and cell LEF
information. 

### Synthesis

Run Synthesis by typing in the **run_synthesis** command. STA should also be performed after the synthesis process. You should be able to see timing reports
inside the synthesis folder inside each run.  

![](/Images/LAB1_ss6.png)

<!-- Day 2 Chip Floorplanning and Standard Cells-->
##  Day 2 Chip Floorplanning and Standard Cells

![](/Images/LAB1_ss9.png)

### Aspect Ratio and Utilization Factor

The area of the die core taken up by standard cells are taking up is called utilization.Optimum values for utilization factors were found to be somwhere between 0.5 - 0.7. Aspect ratio can specify the shape of your chip by the height of the core area divided by the width of the core area. An aspect ratio of 1 discribes the chip as a square. Similarly, if the ratio is little off then the shape is a rectangle. 

### Preplaced Cells

Preplaced cells enable VLSI engineers to granularize a larger design. In floorplanning, position and blockages are decided for preplaced cells. Blockages are needed to ensure no standard cells are mapped where the placeplaced cells are located. Designer can the change the position of the preplaced block based on 
convenience or efficiency of the overall layout

### Decoupling Capacitors

Voltage drops associated with interconnect wires can affect noise margin. It can also cause cross-talk or see undershoot or oveershoot volatges occuring. Decoupling capacitor is a big capacitor located next to the macros to fix this problem. The capacitor will charge up to the power supply voltage and it will work as a charge reservoir whenever there are occurances of drops. It is not always possible to have capacitors along near all the macros. 

### Power Planning

When a transition occurs on a net, charge associated with coupling capacitors may be dumped to ground. If there are not enough ground taps charge will accumulate at the tap and the ground line will act like a large resistor, raising the ground voltage and lowering our noise margin. To bypass this problem a robust PDN with many power strap taps are needed to lower the resistance associated with the PDN. Also, it is important to have a good

### Pin Placement

Pin placement is an essential part of floorplanning to minimize buffering and improve power consumption and timing delays. The goal of pin placement is to use the connectivity information of the HDL netlist to determine where along the I/O ring a specific pin should be placed. In many cases, optimal pin placement will be accompanied with less buffering and therefore less power consumption. After pin placement is formed we need to place logical cell blockages along the I/O ring to discriminate between the core area and I/O area.

### Floorplanning with OpenLANE

To run floorplan in OpenLANE type in the command **run_floorplan**. As with all other stages, the floorplanning will be run according to configuration settings 
in the design specific config.tcl file. The output the the floorplanning phase is a DEF file which describes core area and placement of standard cell

![](/Images/LAB1_ss5.png)

### Viewing Floorplan in Magic

Floorplan can be viewed by using a tool called Magic inside the openlane flow. To view the floorplan we need sky130A.tech file, Merged LEF file and Def file of floorplan

### Placement

Placement is run by typing in the command **run_placement**.The synthesized netlist has been mapped to standard cells and floorplanning phase has determined the 
standard cells rows, enabling placement. OpenLANE does placement in two stages. In Global Placement optimizations are done to reduce wirelength by reducing half
parameter wirelength and for Detailed Placement legalizes placement of cells into standard cell rows. Overflow value conerges to zero during the placement run.
In rc6 version, along with placemnet the power distribution is also performed which was not the case for earlier versions. Also see the post placement stats in
the picture below. 

![](/Images/LAB2_ss6.png)

### Viewing Placement in Magic

To view placement in Magic the command is as follows 

![](/Images/LAB2_ss9.png)

![](/Images/LAB2_s10.png)

### Standard Cell Design Flow

Standard cell design is made up of three parts

1. Inputs - PDKs (Process design kits), DRC & LVS rules, SPICE models, library & user-defined specs.
2. Design Steps - Design steps of cell design involves Circuit Design, Layout Design, Characterization. GUNA is used for characterization. 
   The characterization can be classified into Timing, Power and Closure.
3. Outputs - Outputs of the Design are CDL (Circuit Description Language), GDSII, LEF, extracted Spice netlist (.cir), timing, noise, power.libs, function.

### Standard Cell Characterization

The process of characterizing a standard cell involves specifying the timing corner, cell delay, slew threshold, etc. It also involves reading the parasitic
extracted netlist and providing necessary simultaion.  

<!-- Day 3 Design Library Cell -->
## Day 3 Design Library Cell

OpenLANE allows changing many ASIC design flow parameters on the fly by using the command set. This allows users to play around with floorplanning and placement without having to reinvoke the tool.

### Spice Simulations

To simulate standard cells spice deck wrappers will need to be created around our model files. Spice deck basically includes the mosfet model information, connection between components, load capapcitances, component values, simulation commands(like .tran). The output waveform is plot by using ngspice. Use the .cir file as source and run it. Use the command plot to see the desired waveforms.

### Switching Threshold of a CMOS Inverter 

Threshold voltage decides the mode of operation of the MOS device. It is a function of the W/L ratio and therefore varying the ratio has a different impact on 
its output. To enable efficient description of the varying waveforms a single parameter called switching threshold is used. Switching threshold is exactly at the intersection of Vin = Vout. A perfectly symmetrical device will have a switching threshold of Vin = Vout = VDD/2. 

### 16 Mask CMOS Process Steps

First we begin by selecting a substrate on which the base layers will form. SiO2 and Si3N2 deposition is done for creating active regions of the transistors.
Pockets are created using photolithography. Doping changes the mobility of the ions inside the structure. Pwell is created by diffusing Boron in a high 
temperature furnace and Nwell is created by diffusing Phosphorous in a high temperature furnace. These are done seperately and preeautions are taken to protect
the other during diffusion by using masks etc. The gate terminal is then etched. The drain is lightly doped to avoid phenomenons such as hot electron effect 
and short channel effect.The next step is the formation of source and drain followed by contacts and local interconnect. The additional SiO2 that was added during 
the process is cleaned off by using HF solution. Titatnium is deposited using sputtering to create the contacts as such. It is followed by deposition of upper
layer metals.

### Magic Layout View of Inverter Standard Cell

![](/Images/LAB3_ss1.png)

Refer to: https://github.com/nickson-jose/vsdstdcelldesign for cell files.

To invoke Magic use .mag file specified in the said directoory

![](/Images/LAB3_ss2.png)

![](/Images/LAB3_ss3.png)

### Magic Key Features:

One of the most important aspects of Magiic is that it performs DRC check on the fly. It also includes 
  1. Color Palette - Defines layers and associated colors
  2. Device Inference - Automatic recognition of NMOS and PMOS devices
  
### Device Inference

Select the specific layer/device by hovering over the object and pressing, s, iteratively, until you traverse the hierarchy to the specified object or you see the 
entire connection getting selected. For e.x if you hover over Y and click s multiple(3) times it will select the entire drain to drain path.

Run the **what** command in the tkcon window to see the information about the selected object

![](/Images/LAB3_ss6.png)

### DRC Errors

DRC checks are continuous in Magic, therefore the designer may ensure the design is DRC free during creation instead of performing the iterative DRC checks when the cell layout is completed. We can check by typing in why at the tkcon window to know the exact rule it violates

For more information on DRC errors plase refer to: https://skywater-pdk--136.org.readthedocs.build/en/136/
For more information on how to fix these DRC errors using Magic please refer to: http://opencircuitdesign.com/magic/

### PEX Extraction with Magic

Extract the parasitics from the layout by performing the following
![](/Images/LAB3_ss4.png)

After generating the extracted file we need to output the .ext file to a spice file:

![](/Images/LAB3_ss5.png)

### Spice Wrapper for Simulation

![](/Images/LAB3_ss7.png)

To run the simulation with ngspice, invoke the ngspice tool with .cir file as the input i.e by following the command **ngspice sky130_inv.spice**

The plot can be viewed by plotting the output vs time while sweeping the input, the command for which is as follows **plot y vs time a**
You should be able to see another window with waveform shown below

![](/Images/LAB3_ss8.png)

Some of the other calculation results like rise transition, fall transition, rise propagation delay and fall propagagtion delay are displayed in order. 
Transistion is calculated by measuring the times associated with 20% and 80% of the Max voltage of the output waveform.
Propagation is calculated by measuring the times associated from 50% to 50% of the input and output voltage waveform. 

![](/Images/LAB3_ss9_riset.png)

![](/Images/LAB3_ss10_fallt.png)

![](/Images/LAB3_ss11_risep.png)

![](/Images/LAB3_ss12_fallp.png)

<!-- Day 4 Layout Timing Analysis and CTS -->
##  Day 4 Layout Timing Analysis and CTS

Place and routing (PnR) is performed using an abstract view of the GDS files generated by Magic. The abstract information includes metal and pin information.
The PnR tool will use the abstract view information, formally defined as LEF, to perform interconnect routing keeping in mind the routing guides generated 
from the PnR flow.

### An Introduction to LEF Files

Technology LEF - Contains layer information, via information, and restricted DRC rules. Cell LEF - Abstract information of standard cells. Tracks are used 
during the routing stage, routes can go over the track. Based on the information from the lef files we create a grid for the inverter as shown below by typing 
in the **grid** command 

![](/Images/LAB4_ss3.png)

### Standard Cell Pin Placement

For the DRC to be zero it is important that the cells are on track. Pins must align with the li1 and met1 preferred routing directions like horizontal/vertical.
During standard cell creation this concept must be accounted for. To ensure a cell is aligned with routing grids in Magic we can display a grid on top of the gds file.

To display the grid in magic we again use the command **grid**

![](/Images/LAB4_ss1.png)

### LEF Generation in Magic

Magic allows users to generate cell LEF information directly from the TKcon terminal. To generate the cell LEF file from Magic use the command **lef write**

![](/Images/LAB4_ss4.png)

Generated cell LEF file looks something like this

![](/Images/LAB4_ss5.png)

### Including Custom Cells in OpenLANE

In order to include the new cells in OpenLANE we will have to characterize the specified cell for particular corners, include the cell level max and min liberty
file and change parameters to perform synthesis again with this newly included cell in the **config.tcl** file. The configuration changes are as follows
 
![](/Images/LAB4_ss6.png)

Use the **-Overwrite** flag to include new configuration switches:
 
![](/Images/LAB4_ss7.png)

Add additional statements to include extra cell LEFs. The commands are as shown in the picture above
  
Check synthesis logs to ensure cell has been integrated correctly. As shown in the picture, it has been correctly included

![](/Images/LAB4_ss8.png)

### Fixing Slack Violations

System specifications defined in the architecture phase determine a required frequency of operation. Circuit's timing performance is analyzed using static 
timing analysis tools (STA). From the STA reports we can see worst negative slack (WNS) and total negative slack (TNS). These refer to the worst path delay
and total path delay in regards to our setup timing restraint. Slack violations can be fixed through STA analysis with OpenSTA inside the openlane tool. We
need Design configuration files (.conf) and Design Synopsys design constraint (.sdc) files for the performing the analysis.

For the design to be complete, the worst negative slack needs to be above or equal to 0. If the slack is lesser than that then we can do some of these things like
changing the synthesis strategy, enabling cell_buffering, manually changing the buffers that are causing longr slews or maybe changing the max fan out on some of
the nodes. 

To invoke OpenSTA with the configuration file use thee following command **sta pre_sta.conf** The pre_sta.conf file looks something like this

![](/Images/LAB4_ss16.png)

### Cell Fanout Example:

![](/Images/LAB4_ss17.png)

The delay of a cell is large due to a high load capacitance due to high fanout. We fixed this problem by setting MAX_OUT parameter on the fly.

### Cell Replacement Example:

![](/Images/LAB4_ss18.png)

To determine what loads our net is driving in OpenSTA we can report net connecitons by using the command **report_net_connections**

To increase the drive strength we replace a net by a buffer, because the signal from this net could potentially get degraded along the way
![](/Images/LAB4_ss20.png)

After performing this optimization we can use the **write_verilog** command to get the improved netlist and use this improved netlist to run_floorplan and
run_placement.


### Clock Tree Synthesis

After floorplanning and placement we can now add clock tree inside our design. Two of the main concerns with generation of the clock tree are Clock skew and  
Delta delay. Clock skew is difference in clock arrival latencies between different FFs on the same path. Delta skew is introduced by coupling.

To run clock tree synthesis (CTS) in OpenLANE run the command **run_cts**

### Viewing Post-CTS Netlist

OpenLANE will generate a new .def file containing information of our design after CTS is performed. To view this netlist we need to invoke the .def file with the Magic tool

### Post-CTS STA Analysis

OpenLANE has the OpenROAD application integrated into its flow. The OpenROAD application has OpenSTA integrated into its flow. Therefore, we can perform STA analysis from within OpenLANE by invoking OpenROAD.

To invoke OpenROAD from OpenLANE type in **openroad**

![](/Images/LAB4_ss25.png)

In OpenROAD the timing analysis is done by creating a .db database file. This database file is created from the post-cts LEF and DEF files. To generate the .db files within OpenROAD

After .db generation users can perform tool configuration followed by reporting the propagated clock timing analysis:

![](/Images/LAB4_ss25.png)

OTHER RESULTS FROM LAB
![](/Images/LAB4_ss34_skew.png)

![](/Images/LAB4_ss32_hold.png)

![](/Images/LAB4_ss33_setup.png)


<!-- Day 5 Final Steps in RTL to GDSII -->
##  Day 5 Final Steps in RTL to GDSII

After generating our clock tree network and verifying post routing STA checks we are ready to generate the power distribution network in OpenLANE by using command
**gen_pdn**

### Power Distribution Network Generation

To generate the PDN in OpenLANE:

![](/Images/LAB5_ss3.png)

The PDN feature within OpenLANE will create:
  1. Power ring global to the entire core
  2. Power halo local to any preplaced cells
  3. Power straps to bring power into the center of the chip
  4. Power rails for the standard cells
  
Note: The pitch of the metal 1 power rails defines the height of the standard cells

### Global and Detailed Routing

OpenLANE uses TritonRoute as the routing engine for physical implementations of designs. Routing consists of two stages:

  1. Global Routing - Routing guides are generated for interconnects on our netlist defining what layers, and where on the chip each of the nets will be reputed
  2. Detailed Routing - Metal traces are iteratively laid across the routing guides to physically implement the routing guides

### To run routing in OpenLANE:

![](/Images/LAB5_ss4.png)

If DRC errors persist after routing the user has two options:
  1. Re-run routing with higher QoR settings
  2. Manually fix DRC errors specific in tritonRoute.drc file

### SPEF Extraction

![](/Images/LAB5_ss5.png)

After routing has been completed interconnect parasitics can be extracted to perform sign-off post-route STA analysis. The parasitics are extracted into a SPEF file. The SPEF extractor is not included within OpenLANE as of now. 


<!-- ACKNOWLEDGEMENTS -->
## Acknowledgements
* [Kunal Ghosh - Co-founder (VSD Corp. Pvt. Ltd)](https://github.com/kunalg123)
* [Nickson Jose - VSD VLSI Engineer](https://github.com/nickson-jose)
* [OPENALNE] (https://github.com/efabless/openlane)
* [Grant Brown](https://gitlab.com/gab13c/openlane-workshop/-/blob/master/README.md)
