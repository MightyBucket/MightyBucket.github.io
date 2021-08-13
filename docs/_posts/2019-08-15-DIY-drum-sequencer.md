---
layout: posts
title:  "Drum synthesizer"
description: "A drum synthesizer panel made using an Arduino, Raspberry Pi, and an IKEA drawer."
excerpt: "A drum synthesizer panel made using an Arduino, Raspberry Pi, and an IKEA drawer."
date:   2019-08-15 20:06:19 +0100
categories: projects
header:
  overlay_image: /pics/drum-sequencer/panel.jpg
  overlay_filter: 0.2
---

## Summary

A project for making a custom MIDI instrument that is good for percussive music. I got inspiration for the idea from the Youtuber and artist [LOOK MUM NO COMPUTER][lmnc-channel] who produced a tutorial for an 8-step sequencer. 

In his tutorial the core functionality was implemented using an Arduino Nano, but I extended it to handle an array of buttons, knobs, and LEDs to try and cover a wide array of use cases.

The layout for the panel was particularly inspired by the classic Roland TR-808 drum synthesizer.

This project was particularly inspired by [this video][sequencer-vid].

![Picture of Roland TR-808][pic-tr808]

## Design and Specifications

These were the overall project goals

* Develop an integrated hardware/software solution
* Instrument is usable for producing percussion in Logic Pro X
* £100 budget
* Reuse parts and materials as much as possible

Below is an initial mock-up of how I envisioned the way these controls would be laid out. As mentioned above, the design mainly takes inspiration from the TR-808 drum machine.

![Mockup of controls layout on paper][panel-mockup]

It was decided that the project needed to have the following controls:

* Instrument pads (16 for a 16 step sequencer)
* Channel knobs and buttons for adjusting individual channels
* Master knobs and buttons (for volume, tempo, play/pause, record etc.)
* Storage bank controls (for saving and retrieving sequences in different banks)

The next step was to procure the hardware parts that would be suitable for this panel.

## Hardware choices

For the physical panel, I found an old IKEA drawer tucked up in my attic. This was perfect, 

Some digging around was done on electronics suppliers like RS components and Rapid electronics, as well as eBay. The criteria was to find parts that suited the purpose well but were also inexpensive.

| Item | Description | Image | Dimensions | Interface |
|--------------|-------------|-------|------------|-----------|
|Instrument pad|Very tactile click. Fairly deep travel.|<img src="/pics/drum-sequencer/instrument-pad.png" width="60" />|16mm x 16mm| 1 digital in|
|Channel knob|Small. High friction|<img src="/pics/drum-sequencer/small-knob.png" width="60" />|⌀ 10mm, depth 15mm|1 analog in|
|Button|Tactile click. Little travel|<img src="/pics/drum-sequencer/black-pushbutton.png" width="60" />|⌀ 2mm, depth 1mm|1 digital in|
|Master knob|Large. Low friction|<img src="/pics/drum-sequencer/big-knob.png" width="60" />|⌀ 35mm, depth 15mm|1 analog in|
|Master button|No tactility but deep travel	|<img src="/pics/drum-sequencer/red-pushbutton.png" width="60" />|⌀ 7mm, depth 10mm|1 digital in|
|Toggle switch|Tactile transition. Two-way throw|<img src="/pics/drum-sequencer/toggle-switch.png" width="60" />|⌀ 3mm, depth 10mm|2 digital in|
|LED|3mm and 5V. In red, yellow, green|<img src="/pics/drum-sequencer/leds.png" width="60" />|⌀ 3mm, depth 1mm|1 digital out|

Taking inspiration from the 8 step sequencer project from LMNC, I decided to use a single Arduino Nano to handle all I/O, sequencing, signal processing and MIDI output.

A pair of rows of female headers were soldered to some stripboard to use as a socket for the Arduino. This stripboard was then placed in the corner of the box, next to where the wire sockets would be for power and MIDI out.

![Image of stripboard with Arduino installed in box](/pics/drum-sequencer/arduino-with-pi.jpg)

After doing the maths on all of the required hardware I/O ports required for all the knobs, buttons and LEDs, it became very clear that the Arduino’s 16 digital I/O and 6 analog I/O wouldn’t be adequate.

> Table of hardware I/O with calculated number of required ports

As a result, some extra hardware was needed to provide additional ports.

The MCP23017 I/O expander chip was used for providing additional digital I/O ports. Each chip provides 16 GPIO pins each with their own configurable pull-up resistors. The chip communicates via the I2C bus which is ubiquitous and widespread. This was also a desirable choice for this project because I had previous experience with using this chip for polling buttons and powering LEDs.

![Image of MCP23017 chip](/pics/drum-sequencer/mcp23017_topview.jpg)

For additional analog inputs, the CD4015BE multiplexer chip was used. I decided to use this chip after seeing it in a few example sketches and projects for the Arduino. Using this chip was very simple. There are eight input pins which are multiplexed into a single output, with the input selected using three digital pins.

![Image of CD4051BE chip](/pics/drum-sequencer/cd4051be.jpg)

# Hardware Development

I was already quite familiar with the MCP23017 chip, so I went ahead and prototyped a piece of stripboard to accommodate eight of these chips, which happens to be the maximum number that can be used on a single I2C bus. Additionally, with eight chips there were 128 I/O ports which would be enough to accommodate all of the I/O with a few pins to spare.

![Image of prototype stripboard with MCP chips](/pics/drum-sequencer/old-stripboard.jpg)

Each chip was hardwired with its own address ranging between 0 and 7. All of these chips were connected on common SDA and SCL bus lines.

Although I was very meticulous while making and soldering the board, there were many bugs present that caused intermittent problems. Some of the chips would have all of their GPIO fully functional and addressable, but others would be non-responsive or might even sporadically respond to different addresses. These intermittent problems were extremely irritating to troubleshoot, which led me to instead use manufactured PCBs as an alternative.

I used the online EasyEDA designer, which I picked up easily despite having little PCB design experience. There was also a good library of part footprints.

![PCB design in EasyEDA and picture of finished PCB](/pics/drum-sequencer/pcb-design.PNG)

The only feasible option for manufacturing these PCBs was to have them manufactured from a batch service in China, which is most cost effective when ordered in large numbers. Because of this, I decided to try and make a board design that was as general as possible in the hope that they could be used in future projects.

Each board has space for three MCP23017 and two CD4051BE chips. This provides a total of 48 digital I/O pins and 16 analog pins per board.

Breakout holes were made for the GPIO and mux pins so that jumpers could be soldered. The address pins for each MCP chip are also exposed to allow for easy configuration. There are rows of 5V and GND lines at the bottom so that the user can easily solder wires to the address lines.

![Picture of PCB populated with chips](/pics/drum-sequencer/pcb-oblique.jpg)

The result was much better than the stripboard prototype – all of the chips responded reliably to their assigned addresses and each GPIO pin worked fine.

The 21 analog inputs from the potentiometers were spread across the three CD4051BE multiplexer chips, with the selector bits controlled directly from the Arduino’s digital pins. The multiplexers worked exactly as expected, switching to the expected inputs as the selector bits were changed. 

The Arduino ADC has a 10-bit resolution for 1024 discrete analogue values, which was too precise as the read values were quite unstable. Fortunately, when sending MIDI commands analogue values are represented by 7 bits or 128 discrete values so the instability disappears when these values are truncated.

## Connecting everything together

I considered several solutions for connecting all of the hardware together. This was a daunting task as nearly 200 electrical connections needed to be made, which needed to be accessible and reliable.

These were some ideas that I considered:

* Circuit traces cut from aluminium foil
* Wire from twisted-pair ethernet cable
* Enamel copper wire
* Single core insulated wire

In the end I settled on using enamelled copper wire to connect everything together. The result was positive - connections were very reliable, and cable management was easy.

![Picture of panel rear with wiring and soldered components](/pics/drum-sequencer/panel-rear.jpg)

Once all the hardware was connected to the multiplexer PCBs, everything could be controlled using just twelve electrical connections. These were connected to the Arduino/Raspberry Pi controller.

![Labelled diagram of electronics connected to Arduino/Raspberry Pi](/pics/drum-sequencer/electronics-and-pi.jpg)

# Software Development

To test and debug the individual buttons, knobs and LEDs, I made a graphical testing app that draws a representation of the panel and indicates when a button is pressed, an LED is on and when a knob is turned on.

> Screenshot/animation of diagnostics app

Additionally, to calibrate and test the knobs, I made another applet that graphs the outputs of the analogue knobs, giving the user the option to select the address and analogue input.

> Screenshot/animation of knob testing app

Next, I made a simple app that sends MIDI notes to the MIDI out port if the user presses one of the instrument pads. I connected the box to my Mac running Logic Pro with a MIDI cable, and notes were played successfully.

This program was extended into a simple 16 step sequencer. The panel plays the instrument LEDs in a regular 16-step beat. When the user presses an instrument pad on a certain beat, it is recorded into a small 'memory bank' and that instrument will be played on that beat.

> Recording of panel flashing LEDs in sequence?



> Animation of LEDs flashing individually


[lmnc-channel]:	https://www.youtube.com/channel/UCafxR2HWJRmMfSdyZXvZMTw
[sequencer-vid]: https://www.youtube.com/watch?v=9oGlCfwCoCw
[pic-tr808]:	 https://i1.wp.com/www.rolandus.com/blog/wp-content/uploads/2014/02/tr-808.png
[panel-mockup]:	 /pics/drum-sequencer/panel-mockup.jpg
[inst-pad]:	 /pics/drum-sequencer/instrument-pad.png