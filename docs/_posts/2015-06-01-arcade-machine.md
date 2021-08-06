---
layout: posts
title:  "Arcade machine"
description: "A small arcade machine powered by a Raspberry Pi"
date:   2015-06-01 00:00:00 +0100
categories: projects
---

# A small arcade machine powered by a Raspberry Pi

## Summary

I made this alongside two other friends in Robotics Club at my sixth form. This was a fun side project that I did alongside my first year of A-levels.

We wanted to make something out of the spare pieces and materials that were lying around in the Computing and DT departments.

> Picture of the arcade machine?

In the end it was massively successful. It was good enough for playing a large variety of games, and proved very popular around the school.

## Design and conception

The idea began in January 2015 when I was in Robotics Club with two friends trying to come up with a fun project to do.

We had the following materials at our disposal:

* Raspberry Pi
* GPIO expander
* Arcade buttons and joystick from eBay
* 7" LCD screen
* Plywood panels
* Breadboards and jumper wires

Making an arcade machine out of these parts was an obvious choice. We also chose this because it was a popular Raspberry Pi project so there was lots of information online to help us if we needed.

To get an idea of proportions and dimensions, we mocked up a model out of cardboard and tape.

> Picture of cardboard model

## Electronics

The arcade machine is composed of six buttons, and a joystick with four microswitches for up, down, left, right. This meant that ten digital input pins were needed.

This also meant that ten pull-down resistors were needed. Thankfully, the chip used for the GPIO expander was the MCP23017, which has configurable pull-down resistors built in.

Connecting these together was very simple. Single core wires were soldered to the buttons and joystick, which were connected to a breadboard and connected to the Raspberry Pi via jumper cables. We felt this was the best compromise between upgradeability and robustness.

> Picture of connected electronics

## Software

### Input driver

Much of the time taken on software development was spent on trying to get the buttons and joystick to work.

### Operating System

We used a version of the Raspbian linux distro that came with RetroPie installed. RetroPie is a software project that makes it easy to play retro games on a Raspberry Pi through a set of emulators. 

> Screenshot of RetroPie?

When the system starts up, the user is presented with a menu for a range of game systems. Once selected, the user can choose from a range of games for that system. 

When the user launches a game, RetroPie automatically launches the relevant emulator and configures the controls. It also returns gracefully to the game selection menus when the player quits a game.

> Screenshots of menus?

Games are added by copying game ROM files to a directory in the system. In addition to a few game ROMs, I also added some games that I developed in Python.

[panel-mockup]:	 https://image.shutterstock.com/image-vector/prohibited-signs-isolated-on-white-260nw-1890653254.jpg