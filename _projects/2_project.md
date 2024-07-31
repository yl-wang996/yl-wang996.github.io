---
layout: page
title: BEV View Transform - IPM
description: Self-study project
img: assets/img/IPM_result.png
importance: 1
category: work
related_publications: true
---
<h2>
    BEV View Transform of ADS - Inverse Pespective Mappling(IPM)
</h2>
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
