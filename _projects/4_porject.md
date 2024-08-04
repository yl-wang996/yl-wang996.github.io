---
layout: page
title: Robot Arm Teleoperation in Sim and Real
description: Self-study project
img: assets/img/project4_teleop_overview.png
importance: 1
category: work
related_publications: true
---

## 1. Introduction
- For reading the frames as control command: 
    - I use the Meta Quest VR Headsets for reading the frame of the controller, and pass through the frame and button event to the robot for the control.
- For the teleoperation in mujoco enviroment:
    - I use the Operational Space control in the mujoco with the diana7 robot, the OSC is an complaint control with work at the cartesian space and much safer than the pure position control. The OSC is based on the inverse Jacobian to calculate the joint velocity from the TCP velocity, and combine the energy-based gravity compensitation and it's mess to finally calculate the effort of each joint.  
- For the teleoperation in the real enviroment:
    - I use the diana7 robot for the real world experiment, since it has a force-torque sensor at each joint, so I can control it in the cartesian impedance mode, that is the impedance configuration can be apply on each dimension of the TCP.
- For the communication of each part:
    - I just simply used the ROS 1 for the communication of above three nodes, the rviz for the visualization.

<h3>Video of Simulation in Mujoco</h3>
<div class="row">
    <div class="col-md-8 col-md-offset-2">
        <div>
            {% include video.liquid path="assets/video/project4_mujoco_diana7_teleop_OSC.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=true %}
        </div>
    </div>
</div>

<h3>Video of Real world manipulatioin</h3>
<div class="row">
    <div class="col-md-8 col-md-offset-2">
        <div>
            {% include video.liquid path="assets/video/project4_real_diana7_teleop.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=true %}
        </div>
    </div>
</div>





