---
layout: posts
title:  "Physics sandbox engine"
description: "A solid mechanics simulation made in Python"
excerpt: "A solid mechanics simulation made in Python"
date:   2017-06-01 00:00:00 +0100
categories: projects

header:
  overlay_image: /pics/physics-engine/code-snapshot.PNG
  overlay_filter: 0.2
  actions:
  - label: "<i class='fas fa-file-code'></i> Code"
    url: "https://github.com/MightyBucket/experimental-physics"

---

## Summary

I developed this alongside learning my Solid Mechanics modules at university to solidify my understanding of the subject. This project significantly developed my programming skills. The engine was derived into a game also written in Python, which was then ported to C.

The objective of this project was to make a sandbox simulation environment that could be used to simulate a range of statics and dynamics problems. Users could create simple 2D shapes and attach forces to them. These forces could be described with simple equations.

In addition to the basic engine, I added many usability features like GUI controls and windows, all developed from scratch.

![Screenshot or GIF of engine in action](/pics/physics-engine/screenshot.PNG)

Overall, this project taught me a lot about three areas. 
<div class="notice--success" markdown="1">
 1. **Designing simulations in code** - this was extremely helpful later on when doing modelling and simulation modules in uni
 2. **UI design and implementation** - making UI elements from scratch really helped me to understand how they intuitively work and how program code should interact with them
 3. **Object oriented programming** - UI and core engine elements are implemented as class objects with polymorphism
</div>
## Core engine

Objects are made of simple rectangles. They all have linear and rotational momentum. The user can attach forces to them, either with constant values or using equations relating to other variables in the environment.

The motion of objects is calculated using the simple Euler method. Below is a snippet of the `move` method which handles this.

```python
def move(self, time=frame_time):
	# After forces are resolved, resolve kinematics.
	x = 0
	y = 0
	self.y_vel += self.y_acc * time
	self.x_vel += self.x_acc * time
	y = (self.y_vel * time) * metre
	x = (self.x_vel * time) * metre

	self.y += y
	self.x += x
	self.top_left = (self.top_left[0] + x, self.top_left[1] + y)
	self.top_right = (self.top_right[0] + x, self.top_right[1] + y)
	self.bottom_left = (self.bottom_left[0] + x, self.bottom_left[1] + y)
	self.bottom_right = (self.bottom_right[0] + x, self.bottom_right[1] + y)

	# Resolve rotational motion
	self.ang_vel += self.ang_acc * time
	d_angle = self.ang_vel * time
	self.angle += d_angle
	self.rotateObject(d_angle)
```

These objects are designed to interact on collision. Below is a snippet of the `checkCollisions` method.

```python
def checkCollisions(self):
	# self.colour = black
	v = [self.top_left, self.top_right, self.bottom_right, self.bottom_left, self.top_left]

	# "objects" is a list that contains all of the world objects
	# This checks through the list to see if this object has collided with another object
	for o in objects:

		if o.name == self.name:  # If the next object is itself, skip it
			continue
		if o.type == Object.platform or o.type == Object.oblong:
			object_v = [o.top_left, o.top_right, o.bottom_right, o.bottom_left, o.top_left]

			for j in range(4):  # Four edges for platforms and oblongs. Represents the object being intersected with
				intersections = []

				for i in range(4):  # One for each edge. Represents this object
					intersects = checkIntersection(v[i], v[i + 1], object_v[j], object_v[j + 1])

					if intersects:
						vrtx = [roundPoint(v[i]), roundPoint(v[i + 1]), roundPoint(object_v[j]),
								roundPoint(object_v[j + 1])]
						intersections.append(True)

						if highlight_intersections == True:
							pygame.draw.line(screen, bright_red, v[i], v[i + 1])
							pygame.draw.line(screen, bright_green, object_v[j], object_v[j + 1])
					else:
						intersections.append(False)
						pass
					pass

				intersections.append(intersections[0])
				for i in range(4):
					if intersections[i] and intersections[
								i + 1]:  # If two adjacent lines intersect with an outside edge
						normal = calculateNormal(object_v[j], object_v[j + 1])
						x = v[i + 1][0]
						y = v[i + 1][1]
						self.addForce("reaction", x, y, -normal, g)
```

## User interface

Alongside building the core engine, I also made a set of classes for implementing crude GUI objects. There are classes for buttons, input boxes, graphs, sliders and windows to name a few.

At the bottom is a slider that allows the user to scrub through the simulation timeline.

![Animation of the slider being used](/pics/physics-engine/timeline-slider.gif)

On the right is a tabbed sidebar containing controls for playing around with the sandbox. The user can add new objects with this, as well as pause or reset the simulation. The user can also graph variables over time to visualise their trajectories.

![Animation showing the different tab views](/pics/physics-engine/tabs.gif)

## Results



[panel-mockup]:	 https://image.shutterstock.com/image-vector/prohibited-signs-isolated-on-white-260nw-1890653254.jpg