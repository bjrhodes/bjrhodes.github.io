---
title: LEPE - Custom Interactive Exhibition
subtitle: A local installations company required some unusual custom software for a one-off project and we were able to assist them with planning and build.
permalink: /portfolio/lepe/
meta-description: A local installations company required some unusual custom software for a one-off project and I was able to assist them with planning and build.
primary_colour: "#11998e"
secondary_colour: "#38ef7d"
hero_image: "/assets/portfolio/lepe-hero.jpg"
hero_opacity: 0.2
layout: post
---

## Problem

The project was to install a large periscope onto a subterranean bunker, allowing the public to view the interior without climbing dangerously into the depths. A traditional periscope proved infeasible and so a technical alternative was sought.

### Solution

Photography was commissioned to capture the stage-dressed bunker, and a rotatable periscope-like housing was assembled. I then developed software which would detect the orientation of the periscope and display the appropriate area of the bunker on a screen inside the housing. The effect is a compelling augmented-reality view of the bunker beneath your feet. A button on the side of the housing allows the viewer to trigger context-aware information about the area of the bunker currently being viewed.

### Approach

The software was completed in nodejs, interfacing with electronics composed of a 3-axis accelerometer, a digital magnetometer and a physical button. Data from these devices is fed into a low-power, stand-alone server running nodejs. We then translate the raw data into a simple JSON package and push it over a websocket into a full-screen browser running a custom javascript-powered renderer.

![Technical Project Lead, Barry on site](/assets/portfolio/lepe.jpg "Technical Project Lead, Barry on site")

Weatherproofing, off-grid installation and low-power performance considerations made this project quite an interesting challenge, but the end result is an enjoyable, unique and informative experience.
