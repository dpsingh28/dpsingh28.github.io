---
layout: page
title: Neural Radiance Fields (NeRF)
description: <ul> <li>In this project, I implemented 3D volume and surface rendering pipelines, using NeRF</li> <li>The project was implemented in Python3. I also extended the baseline to improve surface reconstruction with realistic light shading using Phong Relighting and improved radiance computation using heirarchical point sampling </li>  </ul>
img: assets/img/projects/l3d_projects/nerf/crane_highres.gif
importance: 1
category: Academic
---

This project is an implementation of the ground-breaking 3D volumetric reconstruction work by Ben Mildenhall, [NeRF](https://www.matthewtancik.com/nerf) and was written in Python3 and made use of the following libraries- PyTorch, NumPy, Hydra, and Matplotlib. This project was implemented as a part of my Spring 2023 course at CMU, [Learnig for 3D Vision](https://learning3d.github.io/), taught by [Prof. Shubham Tulsiani](http://shubhtuls.github.io/).

# Volume Reconstruction

### Ray Sampling
First part in the process to generate a NeRF is to desgn a ray sampler, capable of producing 3D rays in the world space, from a given set of image co-ordinates. This is done by generating a normalized meshgrid over the image dimensions, using ***Pytorch.meshgrid*** and using this to project rays into 3D space. These rays, currently in camera space, are then transformed into world space using appropriate camera extrinsics. The image below shows an exmaple of a meshgrid and the resulting rays visualized from the origin location.

<div class="row justify-content-sm-center">
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/l3d_projects/nerf/coord_grid.png" title="Image Coordinates Visualization" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/l3d_projects/nerf/coord_rays.png" title="Image Rays Visualization" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The left figure shows a visualization of the image coordiantes. The right image shows a visualization of the projected rays from the origin
</div>

### Point Sampling
The second step involves sampling points, using the rays generated in the previous section. Points are sampled along the rays generated, at stratified intervals, up until a maximum threshold. This gives us a semicircular point cloud of samples along the rays, which can be seen visualized in the image below.

<div class="row justify-content-sm-center">
    <div class="col-sm-0 mt-0 mt-md-0">
        {% include figure.html path="assets/img/projects/l3d_projects/nerf/points_sampled.png" title="Sampled Points" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Sampled points in a bundle of rays
</div>

### Volume Rendering
Now, a volume rendering function is designed, which would take *input* the *sampled points* defined in the previous section, and an *implicit volume function* for an object and use the transmittance equations defined below to produce a volume rendering for that object. The equations can be underestood from the figure below which shows a point sampling inside an object. The first equation is a recursive equation, that calulates the emission (color) for the segment ***i***, shown in red below. The second equation calculates the transmittance of this segment with respect to the point-of-view (eye in the figure), based on the object absorption and emission coefficients. Please visit [this page](https://taiya.github.io/pubs/tagliasacchi2022volume.pdf) for detailed explanation on transmittance calculations in volume rendering

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-0 mt-md-0">
        {% include figure.html path="assets/img/projects/l3d_projects/nerf/transmittance_fig.png" title="Transmittance Concept" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

<font size="+2">
$$ L(x,w)= \sum_{i=1}^{N} T(x, x_{t_i})(1 - e^{-\sigma_{t_{i}} \Delta t_i }) L_e(x_{t_i}, w) $$

$$ T(x, x_{t_i}) = T(x, x_{t_{i-1}})e^{-(\sigma_{t_{i-1}} \Delta t_{i-1})} $$
</font>

A sample rendering using this renderer, for a cube is shown in the animation below.

<div class="row justify-content-sm-center">
    <div class="col-sm-0 mt-0 mt-md-0">
        {% include figure.html path="assets/img/projects/l3d_projects/nerf/cube_render.gif" title="Cube Render" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Cube render using the Volume Renderer
</div>

### Designing NeRF
A neural radiance field is a neural network used to approximate the implicit function for any given object. It is trained on multiple images of this object and is capable of producing continuous volume renders. The multi-layered perceptron (MLP) network used by me for this purpose is shown below

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-0 mt-md-0">
        {% include figure.html path="assets/img/projects/l3d_projects/nerf/nerf_mlp.png" title="NeRF MLP" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    MLP used for NeRF
</div>

This MLP was trained on the multi-view images of a bulldozer. The hyperparamters used for this training are listed in the table below. The results of the volume rendering can be seen in the image below.


<div class="row justify-content-sm-center">
    <table style="shrink;">
    <tr>
        <th>Hyperparameter</th>
        <th>Value</th>
    </tr>
    <tr>
        <td>Learning rate</td>
        <td>1e-4</td>
    </tr>
    <tr>
        <td>Epochs</td>
        <td>250</td>
    </tr>
    <tr>
        <td>Batch Size</td>
        <td>1024</td>
    </tr>
    <tr>
        <td>Number of Sampled Rays</td>
        <td>32768</td>
    </tr>
    <tr>
        <td>Number of Points per Ray</td>
        <td>128</td>
    </tr>
    <tr>
        <td>Image Resolution</td>
        <td>600X600</td>
    </tr>
    </table>
</div>
<br>
<div class="row justify-content-sm-center">
    <div class="col-sm-0 mt-0 mt-md-0">
        {% include figure.html path="assets/img/projects/l3d_projects/nerf/crane_highres.gif" title="NeRF final results" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    NeRF volume rendering results for bulldozer
</div>


<div class="row justify-content-sm-center">
    <div class="col-sm-4 mt-md-0">
        {% include figure.html path="assets/img/projects/l3d_projects/nerf/progress/1.gif" title="50 epochs" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-md-0">
        {% include figure.html path="assets/img/projects/l3d_projects/nerf/progress/2.gif" title="100 epochs" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-md-0">
        {% include figure.html path="assets/img/projects/l3d_projects/nerf/progress/4.gif" title="250 epochs" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    NeRF progression through training. From left to right - 50 epochs, 100 epochs, 250 epochs
</div>

# Surface Reconstruction

The implementation of NeRF was extended to include Surface Reconstruction, using Neural Implicit Surfaces. Here, we implement a Neural SDF which is basically an approximation of the [signed distance function](https://en.wikipedia.org/wiki/Signed_distance_function) (SDF) for any object using a neural network. SDF is the signed orthogonal distance of a given point to the boundary of an object. The sign determines whether the point lies inside or outside the boundary. The function has positive values for points inside the boundary.