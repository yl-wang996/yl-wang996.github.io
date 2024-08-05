---
layout: page
title: BEV View Transform for Autonomous Driving
description: Self-study project
img: assets/img/IPM_result.png
importance: 1
category: work
related_publications: true
---


# 1. Inverse Pespective Mappling(IPM)

<div class="row">
    <div class="col-md-8 col-md-offset-2">
        <h3>
            1. Theory
        </h3>
        <p class="text-justify">
            Inverse perspective transformation (IPM) is a method of converting the camera perspective into a bird's-eye view. 
        </p>
        <p class="text-justify">
            The projection from camera pixels(u,v) to 3D points in camera frame:
            $$
                \mathbf{r}(\lambda) = \lambda  \mathbf{K}^{-1} \begin{pmatrix} u \\ v \\ 1 \end{pmatrix}, ~ \lambda \in \mathbb{R}_{>0} \tag{1}
            $$
        </p>
        <p>
        The road norm in camera frame is:
            $$
                \mathbf{n_c} = \mathbf{R_{rc}} (0,1,0)^T \tag{2}
            $$
        And we assume:
        $$
        \mathbf{r}_0 = h \mathbf{n_c} \tag{3}
        $$
        </p>
        <p class="text-justify">
            The constrain of the road plane:
            $$
                \mathbf{n}^T (\mathbf{r} - \mathbf{r}_0) = 0 \tag{4}
            $$ 
        </p>
        <p>
        Combine (3) and (4), we have:
        $$
            0= \mathbf{n_c}^T (\mathbf{r} - \mathbf{r}_0) = \mathbf{n_c} ^T \mathbf{r} - h \Leftrightarrow~  h=\mathbf{n_c}^T\mathbf{r} \tag{5}
        $$
        </p>
        <p class="text-justify">
            Combine (1) and (5), we can get the camera depth:
            $$
                h = \mathbf{n_c}^T \lambda \mathbf{K}^{-1} (u,v,1)^T ~ \Leftrightarrow~ \lambda = \frac{h}{ \mathbf{n_c}^T \mathbf{K}^{-1} (u,v,1)^T} \tag{6}
            $$
        </p>
        <p class="text-justify">
            Then since we have the depth formula, together with (1), we can get the entire IPM formula:
            $$
                \begin{pmatrix} X_c \\ Y_c \\Z_c \end{pmatrix} = \frac{h}{ \mathbf{n_c}^T \mathbf{K}^{-1} (u,v,1)^T} \mathbf{K}^{-1} \begin{pmatrix} u \\ v \\ 1 \end{pmatrix} \tag{7}
            $$ 
            And this is the points in camera frame, and it can be simply converted to the world frame with the camera extrinsics. 
        </p>
        <p class="text-justify">
        </p>
    </div>
</div>

<div class="row">
    <div class="col-md-8 col-md-offset-2">
        <h3>2. Example</h3>
        The camera image:
        {% include figure.liquid loading="eager" path="assets/img/IPM_origin.png" title="example image" class="img-fluid rounded z-depth-1" %}
        The mapped points in workd frame:
        {% include figure.liquid loading="eager" path="assets/img/IPM_result2.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

-------------------------------------------------------------------------------------------------------------
# 2. [Lift, Splat, Shoot: Encoding Images From Arbitrary Camera Rigs by Implicitly Unprojecting to 3D](https://github.com/nv-tlabs/lift-splat-shoot/tree/master?tab=readme-ov-file)

<div class="row justify-content-sm-center">
    <div class="col-sm-14 mt-0 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/project3_pipeline.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

## 1. Abstract
The goal of perception for autonomous vehicles is to extract semantic representations from multiple sensors and fuse these representations into a single "bird's-eye-view" coordinate frame for consumption by motion planning. We propose a new end-to-end architecture that directly extracts a bird's-eye-view representation of a scene given image data from an arbitrary number of cameras. The core idea behind our approach is to "lift" each image individually into a frustum of features for each camera, then "splat" all frustums into a rasterized bird's-eye-view grid. By training on the entire camera rig, we provide evidence that our model is able to learn not only how to represent images but how to fuse predictions from all cameras into a single cohesive representation of the scene while being robust to calibration error. On standard bird's-eye-view tasks such as object segmentation and map segmentation, our model outperforms all baselines and prior work. In pursuit of the goal of learning dense representations for motion planning, we show that the representations inferred by our model enable interpretable end-to-end motion planning by "shooting" template trajectories into a bird's-eye-view cost map output by our network. We benchmark our approach against models that use oracle depth from lidar. Project page: https://nv-tlabs.github.io/lift-splat-shoot/.

## 2. Theory
It mainly consist of three steps:
- Lift: extract the image feature with NN, and the estimate the depth distribution of each feature pixel.
    - Estiamte the depth distribution of each image.
    - Generate the frustum of each camera.
        - It is based on the camera frame with shape [D, H, W, 3], D is the number of the depth grid, and 3 means (h,w,d).
    - Convert each frustum to ego coordinates system.
<div class="row justify-content-sm-center">
    <div class="col-sm-10 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/project3_depth_estimation.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>  
    <div class="col-sm-10 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/project3_frustums_to_ego.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/project3_geom.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
- Splat:  The purpose of Splat is to project context features into the BEV grid and construct BEV features.
    - First, filter out the frustum points at ego-vehicle coordinate system that fall outside the boundary of the BEV grid after translation.
    - Since there may be multiple points falling into the same cell, each point is assigned a rank value. Points with the same rank value are represented in the same cell of the same batch.
    - Finally, the context features falling in the same cell are summed and pooled(aroud z-axis) to obtain the BEV features.
- Shoot
    - Use the BEV feature for the downstream tasks.

## 3. Exmaple

<div class="row justify-content-sm-center">
    <div class="col-sm-6 mt-3 mt-md-0">
        <h4>3.1 Raw image<h4>
        {% include figure.liquid loading="eager" path="assets/img/project3_raw_image.png" title="example image" class="img-fluid rounded z-depth-1" %}
        <h4>3.2 BEV feature<h4>
        {% include figure.liquid loading="eager" path="assets/img/project3_bev.png" title="example image" class="img-fluid rounded z-depth-1" %}
        <h4>3.3 Apply segmentation encoder to BEV feature<h4>
        {% include figure.liquid loading="eager" path="assets/img/project3_out.png" title="example image" class="img-fluid rounded z-depth-1" %}
        <h4>3.4 Extract segmentation with sigmoid<h4>
        {% include figure.liquid loading="eager" path="assets/img/project3_car_seg.png" title="example image" class="img-fluid rounded z-depth-1" %}



