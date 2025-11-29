---
layout: home
title: FPGA VGA Driver Project
tags: fpga vga verilog
categories: demo
---

For this project we have to demonstrate our understanding of VGA output using the BASYS 3 Xilinx board and the vivado software suite. Demonstrating a understanding of timers as well as how to display 12bit colours via VGA. 




## **My VGA Design Edit**

For my Project I wanted to combine both of the colour cycle and colour stripe template in order to create a program that cycles through a selection of National flags that I created. 

### **Schematic of project**

Here are my Schematic diagram of my project

<img src="https://github.com/Sighmantaneous/soc_d-v_project/blob/main/docs/assets/images/PinoutDiagram.jpg">

<img src="https://github.com/Sighmantaneous/soc_d-v_project/blob/main/docs/assets/images/TestBenchArch.jpg">

<img src="https://github.com/Sighmantaneous/soc_d-v_project/blob/main/docs/assets/images/SchematicArch.jpg">



And here is the Schematic that Vivado generated based on my design.
<img src="https://github.com/Sighmantaneous/soc_d-v_project/blob/main/docs/assets/images/SchematicWeek10.png">

### **Project Set-Up**

In setting up this project we had two sample templates, colourCycle and colourStripes we had to adapt the colourCycle to include the clk_wiz_0 another clock that operates at 25Mhz. For the ColourStripes I then had to update the VGATOP design to include the ColourStripes i_colour_stripes unit . From there after getting stripes displayed I altered the image to display just two colours by defining the rows and columns (x & y cords) 

I decided to use ColourCycle as my baseline for this project and incorperate in the pieces of colour stripes which I wanted. mainly the inclusion of row and column as well as changing the output from 12bit colour to the 3 separate 4bit RGB values. This allowed me to draw different colours within each cycle using colourstripes method. I encountered difficulty where I kept getting stuck in the first if statement of each cycle causing it to display the first colour instead of the complete flag. I eventually discovered that I did not include row and column in the VGA top file under the ColourCycle generator. After Including my project worked correctly. Before this the program had no idea what row and column were and so just defaulted to the first colour in the if statement.


<img src="https://github.com/Sighmantaneous/soc_d-v_project/blob/main/docs/assets/images/Week1SocProject.png">

<img src="https://github.com/Sighmantaneous/soc_d-v_project/blob/main/docs/assets/images/Week1SocProject2.png">

### **Code Adaptation**

This is the VGAsync file that was provided to us. It was not altered in anyway.
<img src="https://github.com/Sighmantaneous/soc_d-v_project/blob/main/docs/assets/images/Screenshot 2025-11-24 153452.png">

This file generates the horizontal and vertical sync as well as the pixel parameters required to display at 640 x 480 via VGA by using counters to compare to timing parameters.
vid_on is only on when display is with the visible pixels ( Horizontal 640 and vertical 480) the remaining pixels make up the front(VFP) and back porch( VLIM - (VDISP + VFP + VPW)


It is an implementation of the following diagram found in the Basys Reference Manual [1] 

<img src="https://github.com/Sighmantaneous/soc_d-v_project/blob/main/docs/assets/images/RasterProcess.png">


Here is the VGATOP file which is used It is a top level module that combines the clock generator the VgaSync generator, the colourCycle generator and the output pins. The only altering I done is just included row and column here as part of colourcycle.

<img src="https://github.com/Sighmantaneous/soc_d-v_project/blob/main/docs/assets/images/Screenshot 2025-11-24 153350.png">



Here is the  main code for my Project .

<img src="https://github.com/Sighmantaneous/soc_d-v_project/blob/main/docs/assets/images/Screenshot 2025-11-24 153621.png">


<img src="https://github.com/Sighmantaneous/soc_d-v_project/blob/main/docs/assets/images/Screenshot 2025-11-24 153841.png">

I had to alter the output wire from one called colour to the seperate green blue and red wires shown 
<img src="https://github.com/Sighmantaneous/soc_d-v_project/blob/main/docs/assets/images/Screenshot 2025-11-24 153807.png">

What is happening here is that every change of state which occurs I am drawing a flag using rows or columns to fill in the pixels with said colours. Mine include both horizontal and vertical flags in its display. Each state change is determined by the COUNT_TO variable which I could alter to increase or decrease the amount of time a flag was displayed for 
I found that I had to set a base colour in each of the states before drawing a flag in order for it to run correctly. Seems to be a quirk with Vivado or verilog as sometimes I didn't have to include and it would work but I decided to leave it in just incase 


### **Simulation**

When trying to capture a simulation of my project I ran into difficulty as the time it took for my images to change was too long to capture in the simulation tool. which is intended as simulation is a scaled down version of the actual operation of the hardware.

<img src="https://github.com/Sighmantaneous/soc_d-v_project/blob/main/docs/assets/images/SOCweek9.png">
We can see that everything is being updated on the rising edge of each clock cycle 
The hsync updates more often than vsync which would make sense as the way the frame is rastered it goes across the row first then wraps around and drops down a column as explain in code adaptation section when discussing vgaSync

In this scaled down version everything does seem to work and I am sure if I increase the simulation duration we would see changes on the row and col as well as changes to each of the 4bit colours.
I am happy with the simulation as it allows me to see that the clock and syncs are working correctly. I can correlate this with my output to determine that my project is functioning correctly.

A project of my size is difficult to simulate with the tool as the changes do not occur frequently enough to see it in simulation

### **Synthesis**

Synthesis is the process of turning my verilog code into a real hardware implementation using gates, flipflops and LUTS. Allowing a optimisation by combining logic and efficiently mapping.

We can see in my picture below the hardware that synthesis decided to use on the board for my project.
The orange blocks are .....

We can see that it is using alot more additional hardware than the templates with a notable cluster in the right middle of photo. 
Zoomed in on that cluster we can see that it is the hardware logic for a statemachine that uses registers and LUTs.
this cluster I assume is where the if/else conditionals for my flag display are occuring as its alot of combinational logic required with some repetition of results would make sense for it be located together as mentioned above synthesis combines logic if possible.
The orange blocks around the edges represent the I/O pins used by the VGA pinout (15 pins) 


Overview
<img src="https://github.com/Sighmantaneous/soc_d-v_project/blob/main/docs/assets/images/SynthisisZoomedOutWeek10.png">

Zoomed In 
<img src="https://github.com/Sighmantaneous/soc_d-v_project/blob/main/docs/assets/images/SynthisisWeek10.png">


### **Demonstration**

Press play to view gif of my projects output.

<img src="https://github.com/Sighmantaneous/soc_d-v_project/blob/main/docs/assets/VidSoC.gif">


### **References**

[1] Basys 3™ FPGA Board Reference Manual, 3rd ed. Digilent, Pullman, WA, USA, July 10, 2019. [Online]. Available: https://digilent.com/reference/programmable-logic/basys-3/reference-manual  (accessed Nov. 29, 2025).


## **More Markdown Basics**
This is a paragraph. Add an empty line to start a new paragraph
Font can be emphasised as *Italic* or **Bold**.

Code can be highlighted by using `backticks`.

Hyperlinks look like this: [GitHub Help](https://help.github.com/).

A bullet list can be rendered as follows:
- vectors
- algorithms
- iterators

Images can be added by uploading them to the repository in a /docs/assets/images folder, and then rendering using HTML via githubusercontent.com as shown in the example below.

<img src="https://raw.githubusercontent.com/melgineer/fpga-vga-verilog/main/docs/assets/images/">


