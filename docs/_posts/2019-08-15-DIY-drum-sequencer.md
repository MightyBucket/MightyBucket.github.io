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


[lmnc-channel]:	https://www.youtube.com/channel/UCafxR2HWJRmMfSdyZXvZMTw
[sequencer-vid]: https://www.youtube.com/watch?v=9oGlCfwCoCw
[pic-tr808]:	 https://i1.wp.com/www.rolandus.com/blog/wp-content/uploads/2014/02/tr-808.png
[panel-mockup]:	 https://image.shutterstock.com/image-vector/prohibited-signs-isolated-on-white-260nw-1890653254.jpg