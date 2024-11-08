---
layout: page
title: Imitation Learning based on the diffusion policy
description: Master Thesis
img: assets/img/dp_real.png
importance: 1
category: work
related_publications: true
---

## 1. Introduction
- Data collection: 
    - In Simulation
      - We collect the 10 demonstrations in the simulation using on the VR controller, it built upon the ROS and Occulus Reader.
    - In Real World
      - We collect the 10 more demonstrations for co-training.
- Data Augmentation:
    - The dataset collected in the simulation is not sufficient for training a robust diffusion model, we apply the trajectory augumentation pipeline to increase the dataset, increse it to 200 demos with broader distribution.
- The model architacture
  - We use the diffusion policy, the input we choose to use the points cloud rather rgb, since the points cloud has smaller reality gap. For increase the precise manipulation capbilities, we try to tracking the pose of obejcts.


<!-- <h3>Video of Real world policy inference result(x2 sppedup)</h3>
<div class="row">
    <div class="col-md-8 col-md-offset-2">
        <div>
            {% include video.liquid path="assets/video/real_world_inference_x2_pcd_pose_compressed.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=true %}
        </div>
    </div>
</div> -->

<h3>Results of Real World Inference</h3>
<div class="row">
    <div class="col-md-8 col-md-offset-2">
        <div>
            {% include video.liquid path="assets/video/dp_real_rollout_pcd_pose.mp4" class="img-fluid rounded z-depth-1" controls=true autoplay=false %}
        </div>
    </div>
</div>




