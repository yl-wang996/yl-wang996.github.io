---
layout: page
title: Simplify Tool Manipulation of Shadowhand based on 6D Pose Estimation
description: Student reseach assistant project
img: assets/img/project0_tooleenet_overview.png
importance: 1
category: work
related_publications: true
---
The related paper([ToolEENet: Tool Affordance 6D Pose Estimation](https://tooleenet-iros2024.github.io/)) has been accepted at IROS 2024.

## 1. Introduction
The goal of this work is to explore how to use the 6D pose estimation to simplify the manipulation of the multi-fingered hand robot, that is the Shadow Hand robot. Since it has 24-DoF and plus the 6-Dof of UR robot arm , the manipulation under 30-DOf is extremly hard and complecated even under learning-based control method. So my idea is, if we can know the pose of the tool's end-effector, e.g. the pose of the hammer head, then we can simply build the transformation between the hammer head and the robot arm base, and the motion of the tool(hammer) can be transform to the motion of the arm base, that we only move the UR robot arm, in that way the 30 DoF motion can be simplify to 6-Dof, and it can even done by the simple motion planning metohd. Moreover, we assume there are no movement of each finger while holding the hammer, which is also intuitive since human rarely move the fingure when using the hammer. 
<h3>Video of Real World experiemnt</h3>
<div class="row">
    <div class="col-md-8 col-md-offset-2">
        <div>
            {% include video.liquid path="https://tooleenet-iros2024.github.io/img/experiment.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=true %}
        </div>
    </div>
</div>