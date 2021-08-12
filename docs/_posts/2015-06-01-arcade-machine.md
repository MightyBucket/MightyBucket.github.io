---
layout: posts
title:  "Arcade machine"
description: "Building a small arcade machine powered by a Raspberry Pi"
excerpt: "Building a small arcade machine powered by a Raspberry Pi"
date:   2015-06-01 00:00:00 +0100
categories: projects
header:
  overlay_image: /pics/arcade-machine/pac-man.jpg
  overlay_filter: 0.4
  
electronics_gallery:
  - image_path: /pics/arcade-machine/buttons-underside.jpg
    url: /pics/arcade-machine/buttons-underside.jpg
    alt: "Underside of buttons"
  - image_path: /pics/arcade-machine/joystick-underside.jpg
    url: /pics/arcade-machine/joystick-underside.jpg
    alt: "Underside of joystick"
  - image_path: /pics/arcade-machine/mcp23017.jpg
    url: /pics/arcade-machine/mcp23017.jpg
    alt: "MCP23017 chip on top of Raspberry Pi"

results_gallery:
  - image_path: /pics/arcade-machine/at-excel-2.jpeg
    url: /pics/arcade-machine/at-excel-2.jpeg
    alt: "Arcade machine on display at ExCeL exhibition booth"
  - image_path: /pics/arcade-machine/at-excel-1.jpeg
    url: /pics/arcade-machine/at-excel-1.jpeg
    alt: "Visitor playing with arcade machine at exhibition"
  - image_path: /pics/arcade-machine/minecraft-1.jpeg
    url: /pics/arcade-machine/minecraft-1.jpeg
    alt: "Model made by another student in Minecraft"
  - image_path: /pics/arcade-machine/in-classroom.jpeg
    url: /pics/arcade-machine/in-classroom.jpeg
    alt: "Arcade machine in the computing labs"
  - image_path: /pics/arcade-machine/gadget-show.jpeg
    url: /pics/arcade-machine/gadget-show.jpeg
    alt: "Arcade machine being played by Jason Bradbury, former presenter of The Gadget Show"
---

## Summary

I made this alongside two other friends in Robotics Club at my sixth form. This was a fun side project that I did alongside my first year of A-levels.

We wanted to make something out of the spare pieces and materials that were lying around in the Computing and DT departments.

![Picture of the arcade machine](/pics/arcade-machine/turned-off.jpg)

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

![Picture of cardboard model](/pics/arcade-machine/cardboard-model.jpeg)

## Assembly

We used our school's DT department to assemble the enclosure. We found some spare sheets of 5mm thick MDF in a scrap pile to use.

We made a schematic of the enclosure composed of five panel pieces. They all join together using PVA glue and finger joints.

> Schematic of enclosure panels?

We covered the top of the controls panel with blue acrylic. The holes for the buttons and joystick were CNC laser cut.

The rear had a sliding polystyrene board, which provided easy access to the internals.

## Electronics

The arcade machine is composed of six buttons, and a joystick with four microswitches for up, down, left, right. This meant that ten digital input pins were needed.

This also meant that ten pull-down resistors were needed. Thankfully, the chip used for the GPIO expander was the MCP23017, which has configurable pull-down resistors built in.

Connecting these together was very simple. Single core wires were soldered to the buttons and joystick, which were connected to a breadboard and connected to the Raspberry Pi via jumper cables. We felt this was the best compromise between upgradeability and robustness.

![Picture of connected electronics](/pics/arcade-machine/electronics-all-connected.jpg)

{% include gallery id="electronics_gallery" caption="Pictures of electronics" %}

The screen was a 7" 800 x 480 pixel LCD panel bought off of eBay. It came with its own controller board, which accepted a variety of video inputs including VGA, HDMI, and composite video. Connecting this to the Pi was easy as only an HDMI cable was needed.

![Pic of LCD screen (courtesy of Amazon)](/pics/arcade-machine/lcd-screen.jpg)

## Software

### Input driver

Much of the time taken on software development was spent on trying to get the buttons and joystick to work.

### Operating System

We used a version of the Raspbian linux distro that came with RetroPie installed. RetroPie is a software project that makes it easy to play retro games on a Raspberry Pi through a set of emulators. 

![EmulationStation home screen (courtesy of emulationstation.org)](/pics/arcade-machine/emulationstation.png)

When the system starts up, the user is presented with a menu for a range of game systems. Once selected, the user can choose from a range of games for that system. 

When the user launches a game, RetroPie automatically launches the relevant emulator and configures the controls. It also returns gracefully to the game selection menus when the player quits a game.

> Screenshots of menus?

Games are added by copying game ROM files to a directory in the system. In addition to a few game ROMs, I also added some games that I developed in Python.

## Testing

On the first power on of the completed product, the system booted successfully into the EmulationStation menu. However, the controls did not function at all.

This lead to a lot of trial and error debugging. I tried a wide range of things, including recompiling the driver, editing its source code, changing the Raspberry Pi and the MCP chip, using different wires etc.

In the end, I found that the Pi couldn't talk properly to the MCP chip because the I2C bus speed was set too fast. Finding this out was extremely frustrating and only came about after over two months of persistent debugging.

Once found, this problem was quickly solved by modifying a single variable in the driver.

## Results

Playing a range of games on the arcade machine was a pleasant experience. The controls were very responsive and the system could run nearly all relevant games at full speed.

The three of us were very excited to see this project to completion. The arcade machine was very popular in the department, with students playing on it constantly. A few had build their computing projects on top of it.

{% include gallery id="results_gallery"%}

[panel-mockup]:	 https://image.shutterstock.com/image-vector/prohibited-signs-isolated-on-white-260nw-1890653254.jpg