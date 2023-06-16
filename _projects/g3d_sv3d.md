---
layout: page
title: Absolute Conic-based Single View to 3D
description: <ul><li>This project deals with single view to 3D reconstruction using classical geometric vision concepts. Here, we first design a single image-based intrinsics calculation module, using the concepts of Image of Absolute Conic</li><li>Using this baseline calibration technique, we design the 3D reconstruction pipeline, using manual plane annotations</li></ul>
img: assets/img/projects/g3d_projects/gsv3d/gsv3d_icon.gif
importance: 3
category: Academic
---

### Absolute Conic and Intrinsics

[Absolute Conic](https://www.cse.iitd.ac.in/~suban/vision/geometry/node45.html) is an entity of the 3D projective space, $$\mathbb{P}^3$$, and is represented by $$\Omega_\infty$$. All spheres in $$\mathbb{P}^3$$ intersect the plane at infinity, $$\pi_\infty = (0,0,0,1)^T$$, at the absolute conic. It is a conic of purely imaginary points on $$\pi_\infty$$. It is given as,

$$
\Omega_\infty = (X_1,X_2,X_3,X_4)^T
$$

$$
X_1^2+X_2^2+X_3^2 = 0; \hspace{0.5cm} X_4 = 0
$$

The image of the absolute conic (IAC), $$\omega$$, is the image of the absolute conic in a camera and it relates to the intrinsics matrix as,

$$
\omega = (KK^T)^{-1}
$$


### Camera Calibration using Vanishing Points
Here, we design a camera intrinsics calibration method, using parallel lines annotations. A triplet of parallel lines in an image has the ability to extract the matrix for the Image of Absolute Conic. This matrix can in turn be used to retrieve the camera intrinsic matrix.<br>


<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/1.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/3.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/5.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Caption photos easily. On the left, a road goes through a tunnel. Middle, leaves artistically fall in a hipster photoshoot. Right, in another hipster photoshoot, a lumberjack grasps a handful of pine needles.
</div>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/5.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    This image can also have a caption. It's like magic.
</div>


<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.html path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.html path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    You can also have artistically styled 2/3 + 1/3 images, like these.
</div>

