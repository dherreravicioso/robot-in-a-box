---
layout: page
title: Data & Results
permalink: /data-and-results/
order: 2
---

The below video shows the estimator in action on the robot. 
{% include youtube.html id="GZ6B9tkkImc" %}

The ROS shell shows the state estimate of the robot in [x, y, theta] coordinates, where \[0, 0, 0\] corresponds to the center of the box facing the top.

More pictures of the Duckiebot are shown below.
Top view of robot in box:
![duckie_top](./assets/img/duckie_top.jpeg)
Front view of Duckiebot:
![duckie_front](./assets/img/duckie_front.jpeg)


We see that the state estimator responds to the robot being moved, and reflects the correct coordinates of its pose in the box. 