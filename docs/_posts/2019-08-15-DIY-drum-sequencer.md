---
layout: post
title:  "DIY Drum Sequencer"
date:   2019-08-15 20:06:19 +0100
categories: jekyll update
---

## Summary

A project for making a custom MIDI instrument that is good for percussive music. I got inspiration for the idea from the Youtuber and artist [LOOK MUM NO COMPUTER][lmnc-channel] who produced a tutorial for an 8-step sequencer. In his tutorial the core functionality was implemented using an Arduino Nano, but this is capable of handling much more than 8 knobs. Thus, I decided to design and make a sequencer control panel consisting of an array of buttons, knobs, and LEDs to try and cover a wide array of use cases.
The layout for the panel was particularly inspired by the classic Roland TR-808 drum synthesizer.

This project was particularly inspired by [this video][sequencer-vid].

![Picture of Roland TR-808][pic-tr808]

## Design and Specifications

These were the overall project goals

* Fulfil goal of an integrated hardware/software solution
* Instrument is usable for producing percussion in Logic Pro X
* £100 budget
* Reuse parts and materials as much as possible

It was decided that the project needed to have the following controls:

* Instrument pads (16 for a 16 step sequencer)
* Channel knobs and buttons for adjusting individual channels
* Master knobs and buttons (for volume, tempo, play/pause, record etc.)
* Storage bank controls (for saving and retrieving sequences in different banks)

Below is an initial mock-up of how I envisioned the way these controls would be laid out

![Mockup of controls layout on paper][panel-mockup]

The next step was to procure the hardware parts that would be suitable for this panel.

## Hardware choices

Some digging around was done on electronics suppliers like RS components and Rapid electronics, as well as eBay. The criteria was to find parts that suited the purpose well but were also inexpensive.

| Item | Description | Image | Dimensions | Interface |
|--------------|-------------|-------|------------|-----------|
|Instrument pad|Very tactile click. Fairly deep travel.|---|16mm x 16mm| 1 digital in|
|Channel knob|Small. High friction|---|⌀ 10mm, depth 15mm|1 analog in|
|Button|Tactile click. Little travel|---|⌀ 2mm, depth 1mm|1 digital in|
|Master knob|Large. Low friction|---|⌀ 35mm, depth 15mm|1 analog in|
|Master button|No tactility but deep travel	|---|⌀ 7mm, depth 10mm|1 digital in|
|Toggle switch|Tactile transition. Two-way throw|---|⌀ 3mm, depth 10mm|2 digital in|
|LED|3mm and 5V. In red, yellow, green|---|⌀ 3mm, depth 1mm|1 digital out|

Taking inspiration from the 8 step sequencer project from LMNC, I decided to use a single Arduino Nano to handle all I/O, sequencing, signal processing and MIDI output.

A pair of rows of female headers were soldered to some stripboard to use as a socket for the Arduino. This stripboard was then placed in the corner of the box, next to where the wire sockets would be for power and MIDI out.

> Image of stripboard with Arduino installed in box

After doing the maths on all of the required hardware I/O ports required for all the knobs, buttons and LEDs, it became very clear that the Arduino’s 16 digital I/O and 6 analog I/O wouldn’t be adequate.

> Table of hardware I/O with calculated number of required ports

As a result, some extra hardware was needed to provide additional ports.

The MCP23017 I/O expander chip was used for providing additional digital I/O ports. Each chip provides 16 GPIO pins each with their own configurable pull-up resistors. The chip communicates via the I2C bus which is ubiquitous and widespread. This was also a desirable choice for this project because I had previous experience with using this chip for polling buttons and powering LEDs.

> Image of MCP23017 chip

For additional analog inputs, the CD4015BE multiplexer chip was used. I decided to use this chip after seeing it in a few example sketches and projects for the Arduino. Using this chip was very simple. There are eight input pins which are multiplexed into a single output, with the input selected using three digital pins.

> Image of CD4051BE chip

# Hardware Development

I was already quite familiar with the MCP23017 chip, so I went ahead and prototyped a piece of stripboard to accommodate eight of these chips, which happens to be the maximum number that can be used on a single I2C bus. Additionally, with eight chips there were 128 I/O ports which would be enough to accommodate all of the I/O with a few pins to spare.

> Image of prototype stripboard with MCP chips

Each chip was hardwired with its own address ranging between 0 and 7. All of these chips were connected on common SDA and SCL bus lines.

Although I was very meticulous while making and soldering the board, despite my best efforts I was never able to get all chips to function to a desirable level. Some of the chips would have all of their GPIO fully functional and addressable, but others would be non-responsive or might even sporadically respond to different addresses. These intermittent problems were extremely irritating to troubleshoot, which led me to instead use manufactured PCBs as an alternative.

Despite having not much previous experience with PCB design, I picked up the process very quickly. I used the onling EasyEDA designer, which was easy to use with a concise interface. There was also a good library of part footprints.

> PCB design in EasyEDA and picture of finished PCB

The only feasible option for manufacturing these PCBs was to have them manufactured from a batch service in China. The manufacturing and shipping cost of producing just one PCB is quite high, but increases very little when ordering more units of the same board design. Because of this, I decided to try and make a board design that was as general as possible in the hope that they could be used in future projects.

Each board has space for three MCP23017 and two CD4051BE chips which was done for two reasons. Firstly, I thought this would provide a generous amount of I/O on just a single board for the large majority of project that I might use them in. Secondly, I found that it was better to have the chips distributed across the control board rather than having them all concentrated in one board, as this made wiring and cable management a lot easier.

Breakout holes were made for the GPIO and mux pins so that jumpers could be soldered. The address pins for each MCP chip are also exposed to allow for totally configurable addresses. There are two rows of 5V and GND lines at the bottom so that the user can easily solder wires to the address lines

> Picture of PCB populated with chips and headers?

The buttons and LEDs were connected to the I/O headers using enamelled copper wire. The result was much better than the stripboard prototype – all of the chips responded reliably to their assigned addresses and each GPIO pin worked fine. A few buttons and LEDs responded less than optimally but this was due to problems with wiring which were easily fixed.

> Animation of LEDs flashing individually

The 21 analog inputs from the potentiometers were spread across the three CD4051BE multiplexer chips, with the selector bits controlled directly from the Arduino’s digital pins. The multiplexers worked exactly as expected, switching to the expected inputs as the selector bits were changed. The Arduino ADC has a 10-bit resolution for 1024 discrete analogue values, which was too precise as the read values were quite unstable. Fortunately, when sending MIDI commands analogue values are represented by 7 bits or 128 discrete values so the instability disappears when these values are truncated.

# Software Development

[lmnc-channel]:	https://www.youtube.com/channel/UCafxR2HWJRmMfSdyZXvZMTw
[sequencer-vid]: https://www.youtube.com/watch?v=9oGlCfwCoCw
[pic-tr808]:	 https://i1.wp.com/www.rolandus.com/blog/wp-content/uploads/2014/02/tr-808.png
[panel-mockup]:	 https://image.shutterstock.com/image-vector/prohibited-signs-isolated-on-white-260nw-1890653254.jpg