---
layout: page
title: Documentation
permalink: /doc/
---


# Source Code Overview
<!-- This section should include information to describe the organization of the code base and highlight how the code connects. -->

The source code for the project is located in the Github repository [here](https://github.com/dherreravicioso/e205-robot-in-a-box/tree/v3/packages/my_package/src).

# Duckietown Frustrations
The bulk of the time spent on this project was wrestling with the Duckietown libraries to get sensors up and running. Duckietown has infrastructure to run ROS nodes with little hassle, but there are some glaring flaws. Using the default ```dts devel build``` and ```dts devel run``` commands to run ROS nodes works great, unless you are trying to access low level device drivers. **Unfortunately**, these ROS nodes using these commands do not have access to drivers such as ```/dev/i2c``` and ```/dev/ttyUSB0```, both necessary to interface with our extra sensors. Countless hours were poured into finding a way to make this work, and we almost gave up until we found a workaround that was not documented anywhere on the internet. Since everything in Duckietown runs in Docker containers, the containers used in ```dts devel``` had limited access to the host machine. There is no way (at least that we could find, and trust me we did some digging) to give elevated permissions to these ROS containers using the Duckietown shell.

 The workaround that we eventually discovered ourselves was running the ```docker run -H hostname``` commands to load a Docker image onto the Duckiebot manually, without using the DTS shell, and giving it the ```--privileged``` flag so that it could access low level I2C and serial drivers. However, by running a container like this, it is not interactive from the host Ubuntu machine. So, one must go into the containers section in the Duckietown Dashboard hosted on the Duckiebot's web socket, open the container that was just run, and open the ROS terminal _from there_. This, combined with long build times for ROS systems, led to some of the most frustrating development experience we have ever run into. For future reference, the Duckietown platform is great for following the provided MOOC and examples. Writing your own ROS nodes that veer away from the basic functionality of the Duckiebot requires far too much setup time to be worth it. 