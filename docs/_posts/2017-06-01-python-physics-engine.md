---
layout: posts
title:  "Physics sandbox engine"
description: "A solid mechanics simulation made in Python"
date:   2017-06-01 00:00:00 +0100
categories: projects
---

# A solid mechanics simulation made in Python

## Summary

I developed this alongside learning learning my Solid Mechanics modules at university to solidify my understanding of the subject. This project significantly developed my programming skills. The engine was derived into a game also written in Python, which was then ported to C.

The objective of this project was to make a sandbox simulation environment that could be used to simulate a range of statics and dynamics problems. Users could create simple 2D shapes and attach forces to them. These forces could be described with simple equations.

In addition to the basic engine, I added many usability features like GUI controls and windows, all developed from scratch.

> Screenshot or GIF of engine in action

## Core engine

Objects are made of simple rectangles. They all have linear and rotational momentum. The user can attach forces to them, either with constant values or using equations relating to other variables in the environment.

These objects are designed to interact on collision.

## User interface

Alongside building the core engine, I also made a set of classes for implementing crude GUI objects. There are classes for buttons, input boxes, graphs, sliders and windows to name a few.

At the bottom is a slider that allows the user to scrub through the simulation timeline.

> Animation of the slider being used

On the right is a tabbed sidebar containing controls for playing around with the sandbox. The user can add new objects with this, as well as pause or reset. The user can also graph variables over time to visualise their trajectories.


[panel-mockup]:	 https://image.shutterstock.com/image-vector/prohibited-signs-isolated-on-white-260nw-1890653254.jpg