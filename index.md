---
layout: home
title: FPGA VGA Driver Project
tags: fpga vga verilog
categories: demo
---

For this project we have to demonstrate our understanding of VGA output using the BASYS 3 Xilinx board and the vivado software suite. Demonstrating a understanding of timers as well as basic rasterisation to display 8bit colours by altering templetes provided to us. 



### **Schematic of project**


Here was my schematic before I realised that I had forgotten to add row and column to the colour cycle unit
<img src="https://github.com/Sighmantaneous/soc_d-v_project/blob/main/docs/assets/images/Week1SocProject3.png">
Not including row and col in VGATOP results in two different schematics
<img src="https://github.com/Sighmantaneous/soc_d-v_project/blob/main/docs/assets/images/Schematicweek9.png">
### **Template Code**
Outline the structure and design of the Verilog code templates you were given. What do they do? Include reference to how a VGA interface works. Guideline: 2/3 short paragraphs, consider including screenshot(s).
### **Simulation**
<img src="https://github.com/Sighmantaneous/soc_d-v_project/blob/main/docs/assets/images/SOCweek9.png">
### **Synthesis**
Describe the synthesis and implementation processes. Consider including 1/2 useful screenshot(s). Guideline: 1/2 short paragraphs.
### **Demonstration**
Perhaps add a picture of your demo. Guideline: 1/2 sentences.

## **My VGA Design Edit**
Introduce your own design idea. Consider how complex/achievabble this might be or otherwise. Reference any research you do online (use hyperlinks).
For my Project I wanted to combine both of the colour cycle and colour stripe template in order to create a program that cycles through a selection of National flags that I created. 

### **Project Set-Up**

In setting up this project we had two sample templates, colourCycle and colourStripes we had to adapt the colourCycle to include the clk_wiz_0 another clock that operates at 25Mhz. For the ColourStripes I then had to update the VGATOP design to include the ColourStripes i_colour_stripes unit . From there after getting stripes displayed I altered the image to display just two colours by defining the rows and columns (x & y cords) 

<img src="https://github.com/Sighmantaneous/soc_d-v_project/blob/main/docs/assets/images/Week1SocProject.png">

<img src="https://github.com/Sighmantaneous/soc_d-v_project/blob/main/docs/assets/images/Week1SocProject2.png">
### **Code Adaptation**
Briefly show how you changed the template code to display a different image. Demonstrate your understanding. Guideline: 1-2 short paragraphs.
### **Simulation**


A project of my size is difficult to simulate with the tool as the changes do not occur frequently enough to see it in simulation 

### **Synthesis**
Describe the synthesis & implementation outputs for your design, are there any differences to that of the original design? Guideline 1-2 short paragraphs.
### **Demonstration**
If you get your own design working on the Basys3 board, take a picture! Guideline: 1-2 sentences.

## **More Markdown Basics**
This is a paragraph. Add an empty line to start a new paragraph.

Font can be emphasised as *Italic* or **Bold**.

Code can be highlighted by using `backticks`.

Hyperlinks look like this: [GitHub Help](https://help.github.com/).

A bullet list can be rendered as follows:
- vectors
- algorithms
- iterators

Images can be added by uploading them to the repository in a /docs/assets/images folder, and then rendering using HTML via githubusercontent.com as shown in the example below.

<img src="https://raw.githubusercontent.com/melgineer/fpga-vga-verilog/main/docs/assets/images/VGAPrjSrcs.png">


