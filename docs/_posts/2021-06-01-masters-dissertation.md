---
layout: project
title:  "Master's Thesis"
description: "To develop a CAD plugin that uses Generative Design and AI to empower designers to improve their designs for 3D printing and Additive Manufacturing"
excerpt: "Leveraging Generative Design in Design for Additive Manufacturing (DfAM)"
date:   2021-06-01 00:00:00 +0100
categories: projects
header:
  overlay_image: /misc/clip.gif
  overlay_filter: 0.2
  actions:
    - label: "<i class='fas fa-file-code'></i> Code"
      url: "http://www.example.com"
    - label: "<i class='fas fa-file-alt'></i> Thesis"
      url: "/misc/FYP_rj457_reduced.pdf"
    - label: "<i class='fas fa-image'></i> Poster"
      url: "/misc/FYP_poster.pdf"

case_studies:
  - image_path: /pics/masters-dissertation/case-study-1.png
    url: /pics/masters-dissertation/case-study-1.png
    alt: "Case Study 1"
  - image_path: /pics/masters-dissertation/case-study-4.png
    url: /pics/masters-dissertation/case-study-4.png
    alt: "Case Study 4"
  - image_path: /pics/masters-dissertation/case-study-5.png
    url: /pics/masters-dissertation/case-study-5.png
    alt: "Case Study 5"
---


## Summary

For my Master's project, I developed a CAD plugin that uses Generative Design to improve existing part designs so they are better suited to 3D printing.


Using a range of case studies, I successfully demonstrated that the tool is:
 - Intuitive to use
 - Guides the user's creative process
 - Produces improved designs

Below is my poster which showcases the process and results. PDF can be seen [here][poster-pdf].

![Poster](/pics/masters-dissertation/poster.jpg)

The project was a big success. The feedback from my supervisor and assessor was extremely positive. My supervisor suggested this work could be used as a foundation for many other student projects.

I received a mark of 73 on the project, which ensured a first-class honours in my degree overall.

## Background

*Additive Manufacturing* and *3D printing* are rapidly growing industries. The proliferation of inexpensive 3D printing hardware in the past five to ten years has accelerated progression for both industry and hobbyist applications. 

There are many opportunities for better manufacturing workflows to be exploited, however these have yet to be fully realised.

![Photo of 3D printing](/pics/masters-dissertation/3d-printing.jpg)

[comment]: <> (Source: https://unsplash.com/photos/HsefvbLbNWc)

*Generative Design* is another novel technology that has attracted significant attention in the past ten years. This involves using an algorithm to iteratively regenerate an existing part design to find improvements. 

This is strongly linked to Machine Learning and Artificial Intelligence which has garnered significant attention from the broader community, however this technology is still far from prevalence as it is still being explored and developed.

![Pic of Generative Design](/pics/masters-dissertation/generations.gif)

## Existing products and research

There are some commercial solutions for Generative Design, and some promising ones for leveraging Design for Additive Manufacturing (DfAM). However, none are commercially available that combine both techniques. A few combined solutions do exist in academic literature, which this project uses as a baseline.

Autodesk Fusion 360 is a popular lightweight CAD package. It is constantly updated with new tools and features, including a Generative Design tool. It is quite powerful and easy to use, but it is closed-source so it doesn't leverage well the power of new technologies.


## Software choices

I chose *FreeCAD* as my CAD platform to build the plugin on top of. It is a popular free and open source package that includes modelling environments for several engineering disciplines.

All scripting and coding was done in Python using the PyCharm IDE. Every function and entity in FreeCAD is well abstracted as an interface or object in Python, which make scripting and macros extremely powerful. It is mainly for this readon that FreeCAD was chosen.

![Screenshot of PyCharm](/pics/masters-dissertation/pycharm.png)

FreeCAD's graphical user interface (GUI) is developed in Qt, so plugin interfaces are implemented using Qt objects. Because of this, I was able to rapidly develop and prototype the plugin GUIs using Qt Designer.

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

{% include gallery id="case_studies" caption="Slides of case studies" %}
 

## Conclusions and future work

The most prominent achievement of this project is that a solid foundation is established for a plugin that combines *Generative Design* and *Design for Additive Manufacturing (DfAM)*. At the time of completion, there is no other solution like this that exists commercially or academically.

These key requirements were met:
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

My supervisor was very happy with my work. Because he was also supervising other projects from students with similar themes, a seminar was held with the other students to present our work.

[panel-mockup]:	 https://image.shutterstock.com/image-vector/prohibited-signs-isolated-on-white-260nw-1890653254.jpg
[poster-pdf]: 	/misc/FYP_poster.pdf