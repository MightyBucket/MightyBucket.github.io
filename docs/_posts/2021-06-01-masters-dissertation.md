---
layout: post
title:  "Master's Thesis: Leveraging Generative Design in Design for Additive Manufacturing (DfAM)"
description: "To develop a CAD plugin that uses Generative Design and AI to empower designers to improve their designs for 3D printing and Additive Manufacturing"
date:   2021-06-01 00:00:00 +0100
categories: jekyll
---

## Summary

Topic: Leveraging Generative Design in Design for Additive Manufacturing (DfAM)
Goal: To develop a CAD plugin that uses Generative Design and AI to empower designers to improve their designs for 3D printing and Additive Manufacturing
Outcome: Successfully demonstrated that the tool is intuitive to use and guides the user's creative process with case studies on a bike pedal and bike saddle.

This plugin has been tested for FreeCAD 0.18 and 0.19. The code can be downloaded here.

> Some pictures and screenshots of the tool in use

![brokenpic](/pics/broken.png)

## Background

Additive manufacturing and 3D printing are rapidly growing industries. The proliferation of inexpensive 3D printing hardware for industry and hobbyists has helped to accelerate attention in the past five to ten years. There are many opportunities for better manufacturing workflows to be exploited but these have yet to be fully realised.

> Photo of 3D printing

Generative design is another novel technology that has attracted significant attention in the past ten years. This involves using an algorithm to regenerate an existing part design so that it is more optimised from some sort of criteria. This is strongly linked to machine learning and artificial intelligence which has garnered significant attention from the broader community, however this technology is still far from prevalence as it is still being explored and developed.

> Pic of Generative Design

## Existing products and research

There are some promising commercial solutions for Generative Design, and some good ones for Design for Additive Manufacturing (DfAM). However, there are none commercially available that combine both techniques. A few combined solutions do exist in academic literature, which this project uses as a baseline.

Autodesk Fusion 360 is a popular lightweight CAD package. It is constantly updated with new tools and features, including a Generative Design tool. It is quite powerful and easy to use, but it is closed-source so it doesn't leverage well the power of new technologies.


## Software choices

I chose FreeCAD as my CAD platform to build the plugin on top of. It is a popular free and open source package that includes modelling environments for several engineering disciplines. Additionally, a lot of academic literature that I found also used FreeCAD.

The language used for scripting is Python, and macros and plugins can be written in either C++ or Python. Every entity in FreeCAD is accessible through code as objects in Python and C++ which makes the macro and scripting system very powerful. It is mainly for this reason that I chose this CAD package.

All of the code that comprises the plugin is written in Python. I used the PyCharm IDE for writing all scripts and modules. FreeCAD's graphical user interface (GUI) is developed in Qt, so plugin interfaces are implemented using Qt objects. Because of this, I was able to rapidly develop and prototype the plugin GUIs using Qt Designer.

> Screenshots of FreeCAD, PyCharm, Qt Designer etc.

## Features

### Parametric randomisation

### Voxelisation

### Part volume calculation

### Support structure generation

### Metric comparisons

## Procedure

To prepare a part for generative design, the user has to label some parameters in the design that will be changed and varied. These can be dimensions in sketches and features.

For mechanical analysis, the user marks where forces and constraints are on the part using FreeCAD's FEA workbench.

> Pic of sketch with labelled parameters

> Pic of FEA workbench with marked forces and constraints

Once these are done, the user is ready to start using the plugin. It is implemeneted as a "workbench" toolbar. The user selects the "AM Generation" workbench from a drop-down menu in the FreeCAD interface. From there, they are shown a toolbar with five buttons - one for each stage of the whole generation process.

> Pic of workbench toolbar with labels

Clicking on **Initiate** will bring up a panel listing the parameters that the user labelled. In this area, the user can input the ranges that they will be varied between. Clicking OK will save the ranges for the next stage.

> Pic of Initiate panel

The next step is the generation stage, which is started by clicking **Generate**. Inside the panel, the user can choose how many generations to produce, then commence by clicking the *Generate* button.

This usually takes a few minutes to complete. Once complete, the table below shows the values given to the parameters in each generation. The user can then view a generation by selecting from the drop-down box and clicking *View*.

> Pic of Generate panel

Next, the user can start the Analysis stage if they want to optimise mechanical performance. This assumes that the user has already marked the forces and constraints as described before.

Clicking on **Analyse** brings up the interface below. The user starts analysis by clicking *Start FEA* which performs the analyses on each generation. This is usually the most time consuming part and can take several minutes.

On completion, the table displays whether each generation was successfully analysed or not.

> Pic of Analyse panel

The Refinement stage is also optional and involves operations for optimising for additive manufacturing. The user clicks **Refine** brings up the interface below.

The user can choose whether to calculate build volume, generate support structures and adjust the scanning resolution. All of the generations are then refined by clicking *Refine*.

On completion, the table displays the volumes of part material and support structure material in each generation.

> Pic of Refine panel

Lastly, the user compares all of the generations in the **Results** stage by clicking on *Results* which brings up the interface below.

If it's the first time, the plugin will take a minute to calculate the results metrics for each generation. Then the table will display all of the metrics calculated for each generation with a colour gradient scale.

Metrics that are displayed include maximum and mean stresses and displacements, part volume, and support structure volumes. This provides the user with enough information to make an educated guess about which generation is best.

> Pic of Results panel

## Case studies

Five case studies were produced to test the effectiveness of the plugin in key areas.

### Case Study 1 - Headphones Frame

The connecting arch for a pair of headphones was designed in FreeCAD as a single part. It is designed to bend open as a simple compliant mechanism made from ABS.

> Pictures of headphones in FreeCAD

### Case Study 2 - Bicycle Seat

bla bla bla

### Case Study 3 - Bicycle Pedal

blablabla

### Case Study 4 - Connecting rod with lattice structure

blablabla

### Case Study 5 - GE Jet Engine Bracket

blablabla

## Conclusions and future work

The most prominent achievement of this project is that a solid foundation is established for a plugin that combines *Generative Design* and *Design for Additive Manufacturing (DfAM)*. At the time of completion, there is no other solution like this that exists commercially or academically.

The following key requirements have been met:

 - **Modular** - can redo just the necessary stages instead of the whole process
 - **Transparent** - easily see the changes that different stages make
 - **Practical** - convenient for a designer to use in their workflows
 - **Unique** - no other solution providing all these benefits simultaneously
 - **Extensible** - open-source and easily modifiable
 
Additionally, there is a lot of scope for future work. Some major features for consideration include:

 - **Process optimisation** using Genetic Algorithms or Simulated Annealing
 - **Lattice generation** which automatically lattices solid regions
 - **Spatial grammars** for part generation rules
 - **Computational offloading** to GPU or computing cluster for large generation tasks
 - **User-defined fitness function** for more complicated optimisations


[lmnc-channel]:	https://www.youtube.com/channel/UCafxR2HWJRmMfSdyZXvZMTw
[sequencer-vid]: https://www.youtube.com/watch?v=9oGlCfwCoCw

[panel-mockup]:	 https://image.shutterstock.com/image-vector/prohibited-signs-isolated-on-white-260nw-1890653254.jpg