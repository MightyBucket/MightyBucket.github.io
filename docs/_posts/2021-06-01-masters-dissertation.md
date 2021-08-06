---
layout: posts
title:  "Master's Thesis"
description: "To develop a CAD plugin that uses Generative Design and AI to empower designers to improve their designs for 3D printing and Additive Manufacturing"
date:   2021-06-01 00:00:00 +0100
categories: projects
header:
  overlay_image: /misc/clip.gif
  overlay_filter: 0.2
  actions:
    - label: "View Code"
      url: "http://www.example.com"
    - label: "Download Thesis"
      url: "/misc/FYP_rj457_reduced.pdf"
    - label: "View Poster"
      url: "/misc/FYP_poster.pdf"
---

# Leveraging Generative Design in Design for Additive Manufacturing (DfAM)


## Summary

For my Master's project, I developed a CAD plugin that uses Generative Design to improve existing part designs so they are better suited to 3D printing.


Using a range of case studies, I successfully demonstrated that the tool is:
 - Intuitive to use
 - Guides the user's creative process
 - Produces improved designs

Below is my poster which showcases the process and results. PDF can be seen [here][poster-pdf].

![Poster](/pics/masters-dissertation/poster.jpg)

## Background

*Additive Manufacturing* and *3D printing* are rapidly growing industries. The proliferation of inexpensive 3D printing hardware in the past five to ten years has accelerated progression for both industry and hobbyist applications. 

There are many opportunities for better manufacturing workflows to be exploited, however these have yet to be fully realised.

![Photo of 3D printing](/pics/masters-dissertation/3d-printing.jpg)

[comment]: <> (Source: https://unsplash.com/photos/HsefvbLbNWc)

*Generative Design* is another novel technology that has attracted significant attention in the past ten years. This involves using an algorithm to iteratively regenerate an existing part design to find improvements. 

This is strongly linked to Machine Learning and Artificial Intelligence which has garnered significant attention from the broader community, however this technology is still far from prevalence as it is still being explored and developed.

![Pic of Generative Design](/pics/masters-dissertation/generative-design.jpg)

## Existing products and research

There are some commercial solutions for Generative Design, and some promising ones for leveraging Design for Additive Manufacturing (DfAM). However, none are commercially available that combine both techniques. A few combined solutions do exist in academic literature, which this project uses as a baseline.

Autodesk Fusion 360 is a popular lightweight CAD package. It is constantly updated with new tools and features, including a Generative Design tool. It is quite powerful and easy to use, but it is closed-source so it doesn't leverage well the power of new technologies.


## Software choices

I chose *FreeCAD* as my CAD platform to build the plugin on top of. It is a popular free and open source package that includes modelling environments for several engineering disciplines.

All scripting and coding was done in Python using the PyCharm IDE. Every function and entity in FreeCAD is well abstracted as an interface or object in Python, which make scripting and macros extremely powerful. It is mainly for this readon that FreeCAD was chosen.

FreeCAD's graphical user interface (GUI) is developed in Qt, so plugin interfaces are implemented using Qt objects. Because of this, I was able to rapidly develop and prototype the plugin GUIs using Qt Designer.

![Screenshot of PyCharm](/pics/masters-dissertation/pycharm.png)
![Screenshot of Qt Designer](/pics/masters-dissertation/qt-designer.png)


## Features
<div class="notice" markdown="1">
 - Parametric randomisation
 - Voxelisation
 - Part volume calculation
 - Support structure generation
 - Metric comparisons
 
 </div>

## Procedure

A five-stage process was devised for the whole procedure.

![Diagram of five-stage process](/pics/masters-dissertation/process2.png)

Each stage in the procedure is implemented as a command in the workbench toolbar.

![Process commands in FreeCAD workbench](/pics/masters-dissertation/workbench.png)

## Case study results

Five case studies were produced to test the effectiveness of the plugin in key areas.

<div class="notice--info" markdown="1">
### Case Study 1 - Headphones Frame

A headphones frame was designed as a single part to be printed from ABS. It is designed to open and be placed on the user's head by bending elastically as a compliant mechanism.

<p float="left">
  <img alt="Headphones model with force arrows" src="/pics/masters-dissertation/case-study-1-1.png" width="250" />
  <img alt="Headphones model with displacement colourmap" src="/pics/masters-dissertation/case-study-1-2.png" width="300" /> 
</p>

**Task:** Find the optimal frame thickness

**Objectives:**
 - Minimise part volume
 - Target specific displacement ranges

**Results:**
 - Successful demonstration of module on a simple load case
 - Optimal design found in just 30 generations
</div>


<div class="notice--info" markdown="1">
### Case Study 2 - Bicycle Seat
A bicycle seat was designed from Bezier curves. These dimensions were parameterised and regenerated to explore the creative design space

<p float="left">
  <img alt="Bicycle shell model" src="/pics/masters-dissertation/case-study-2-1.png" width="175" />
  <img alt="Bicycle shell model" src="/pics/masters-dissertation/case-study-2-2.png" width="175" />
  <img alt="Bicycle shell model" src="/pics/masters-dissertation/case-study-2-3.png" width="175" />
</p>

**Task:** Try and find different designs for a bicycle seat shell

**Objective:**
 - Explore the creative design space
 
**Results:**
 - Good variety of designs produced successfully
 - Sucessful demonstration of the plugin's ease of use
 </div>

<div class="notice--info" markdown="1">
### Case Study 3 - Bicycle Pedal

A bicycle pedal was modelled as a frame of struts to find an optimal design that

<p float="left">
  <img alt="Bike pedal voxel model with supports" src="/pics/masters-dissertation/case-study-3-1.png" width="175" />
  <img alt="Bike pedal stress colourmap with force" src="/pics/masters-dissertation/case-study-3-2.png" width="175" />
  <img alt="Bike pedal model" src="/pics/masters-dissertation/case-study-3-3.png" width="175" />
</p>

**Task:** Design an optimal bike pedal that uses minimal material and supports 100kg load

**Objectives:**
 - Minimise part volume
 - Minimse support structures
 
**Results:**
 - 34% decrease in volume
 - Sucessful demonstration of the plugin aids the designer's creative process
</div>

<div class="notice--info" markdown="1">
### Case Study 4 - Connecting rod with lattice structure

A solid link was designed with a lattice structure to produce a load-bearing part with decreased part volume

<p float="left">
  <img alt="Connecting rod model with forces" src="/pics/masters-dissertation/case-study-4-1.png" width="275" />
  <img alt="Connecting rod stress colourmap" src="/pics/masters-dissertation/case-study-4-2.png" width="275" />
</p>

**Task:** Optimise the parameters for a lattice structure in a simple part

**Objectives:**
 - Minimise part volume
 - Minimse deflection of 3mm
 
**Results:**
 - Significant 38.7% decrease in volume compared to solid material
 - Demonstrates that module can optimise other features if implemented correctly
</div>
 
<div class="notice--info" markdown="1">
### Case Study 5 - GE Jet Engine Bracket

This was taken from the 2013 GE Jet Bracket competition to produce an optimal design for a jet bracket to be additively manufactured. Two of the best final designs were taken and their ideas were combined then regenerated to produce an even more optimal design.

<p float="left">
  <img alt="GE Bracket stress colourmap with force arrows" src="/pics/masters-dissertation/case-study-5-1.png" width="275" />
  <img alt="GE Bracket voxel model with support structures" src="/pics/masters-dissertation/case-study-5-2.png" width="275" />
</p>

**Task:** Take an existing optimised part design and improve it by combining other ideas

**Objectives:**
 - Minimise part volume
 - Maximise mean stress
 
**Results:**
 - Modest 4.3% decrease in part volume
 - Significant increase in mean stress
 - Low support volume ratio of 0.1
</div>
 

## Conclusions and future work

The most prominent achievement of this project is that a solid foundation is established for a plugin that combines *Generative Design* and *Design for Additive Manufacturing (DfAM)*. At the time of completion, there is no other solution like this that exists commercially or academically.

The following key requirements have been met:
<div class="notice--success" markdown="1">
 - **Modular** - can redo just the necessary stages instead of the whole process
 - **Transparent** - easily see the changes that different stages make
 - **Practical** - convenient for a designer to use in their workflows
 - **Unique** - no other solution providing all these benefits simultaneously
 - **Extensible** - open-source and easily modifiable
 </div>
Additionally, there is a lot of scope for future work. Some major features for consideration include:
<div class="notice--success" markdown="1">
 - **Process optimisation** using Genetic Algorithms or Simulated Annealing
 - **Lattice generation** which automatically lattices solid regions
 - **Spatial grammars** for part generation rules
 - **Computational offloading** to GPU or computing cluster for large generation tasks
 - **User-defined fitness function** for more complicated optimisations
</div>

[panel-mockup]:	 https://image.shutterstock.com/image-vector/prohibited-signs-isolated-on-white-260nw-1890653254.jpg
[poster-pdf]: 	/misc/FYP_poster.pdf