---
layout: page
title: Learning-based Single View to 3D 
description: <ul> <li> Here, I designed a Single view to 3D reconstruction pipeline, for image-to-voxel, image-to-mesh, and image-to-point cloud generation</li> <li> I achieved an F1-score of <strong>0.88</strong> for the point cloud reconstruction and also extended the network for occupancy queries  </li> </ul>
img: assets/img/projects/l3d_projects/lsv3d/chair_index.gif
importance: 2
category: Academic
---

Single View to 3D reconstruction is a recent research topic in 3D vision. This involves building neural networks that are capable of producing a 3D representation of an object provided in an image. Thid project deals woth these kind of networks. I built three different models, aimed for image-voxel, image-mesh, and image-point cloud reconstruction. This project has been implemented in Python3 and uses packages - PyTorch, PyTorch3D, NumPy, and Matplotlib. This project was implemented as a part of my Spring 2023 course at CMU, [Learnig for 3D Vision](https://learning3d.github.io/), taught by [Prof. Shubham Tulsiani](http://shubhtuls.github.io/).

### Image to Voxel
The neural network used for this part can be seen in the image below. An input image is fed through a [ResNet Encoder](https://arxiv.org/abs/1512.03385) and an output 1D embedding of size 512 (shown in green) is recieved. This is passed through the decoder, which starts with an MLP (shown in orange). The output of this MLP (size 2048) is unflattened into a tensor of size (256,2,2,2). This is fed into multiple 3D deconvolutional layers, which give ouput a voxel grid of size (32,32,32) at the end (shown in red). Each of the MLPs and the deconvolutional layers, except the last one, have a Relu activation and BatchNorm in front of them.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/l3d_projects/lsv3d/vox/voxel_nn.png" title="Image-Voxel net" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Neural Network used for Image to Voxel Reconstruction
</div>

The model was trained on multiple images of multiple chair images for ~5000 epochs. The results can be seen below



<div class="row justify-content-sm-center">
    <div class="col-sm-0 mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/l3d_projects/lsv3d/vox/vox_chair1.png" title="Chair-1 Image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-3 mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/l3d_projects/lsv3d/vox/vox_rend1.gif" title="Chair-1 Voxel Render" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="row justify-content-sm-center">
    <div class="col-sm-0 mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/l3d_projects/lsv3d/vox/vox_chair2.png" title="Chair-2 Image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-3 mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/l3d_projects/lsv3d/vox/vox_rend2.gif" title="Chair-2 Voxel Render" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="row justify-content-sm-center">
    <div class="col-sm-0 mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/l3d_projects/lsv3d/vox/vox_chair3.png" title="Chair-3 Image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-3 mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/l3d_projects/lsv3d/vox/vox_rend3.gif" title="Chair-3 Voxel Render" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Input Image v/s Voxel Render results from the model
</div>


### Image to Point Cloud
The model used for this part is shown below. The initial structure of the decoder for this case is similar to the previous one, the voxel case. We use a ResNet Encoder and then put a multi-layer perceptron (MLP) as the decoder. The output of this decoder is a tensor of size *number of points X 3*. This ouput is then resized to *(number of points , 3)*. The reason for choosing an MLP instead of a deconvolutional layer is that point clouds are of discrete nature, rather than the continuous nature of voxels. 

<div class="row justify-content-sm-center">
    <div class="col-sm-7 mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/l3d_projects/lsv3d/pcl/pcl_nn.png" title="Image-Point Cloud net" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Neural Network used for Image to Point Cloud Reconstruction
</div>

The training was for this model was similar to that for the voxel case, with multiple chair images and ~5000 epochs. The results can be seen below.

<div class="row justify-content-sm-center">
    <div class="col-sm-0 mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/l3d_projects/lsv3d/pcl/pcl_chair1.png" title="Chair-1 Image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-3 mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/l3d_projects/lsv3d/pcl/pcl_rend1.gif" title="Chair-1 Point Cloud Render" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="row justify-content-sm-center">
    <div class="col-sm-0 mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/l3d_projects/lsv3d/pcl/pcl_chair2.png" title="Chair-2 Image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-3 mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/l3d_projects/lsv3d/pcl/pcl_rend2.gif" title="Chair-2 Point Cloud Render" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="row justify-content-sm-center">
    <div class="col-sm-0 mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/l3d_projects/lsv3d/pcl/pcl_chair3.png" title="Chair-3 Image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-3 mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/l3d_projects/lsv3d/pcl/pcl_rend3.gif" title="Chair-3 Point Cloud Render" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Input Image v/s Point Cloud Render results from the model
</div>


### Image to Mesh
The model used for this case is same as the one used for point cloud case, with the exception of the output tensor now being *number of mesh vertices X 3*. The output is resized to *(number of points , 3)* and then converted into a mesh using [PyTorch3D.structures.Meshes](https://pytorch3d.readthedocs.io/en/latest/_modules/pytorch3d/structures/meshes.html#Meshes).

<div class="row justify-content-sm-center">
    <div class="col-sm-7 mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/l3d_projects/lsv3d/mesh/mesh_nn.png" title="Image-Mesh net" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Neural Network used for Image to Mesh Reconstruction
</div>

The training was for this model was similar to that for the voxel case, with multiple chair images and ~5000 epochs. The results can be seen below.

<div class="row justify-content-sm-center">
    <div class="col-sm-0 mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/l3d_projects/lsv3d/mesh/mesh_chair1.png" title="Chair-1 Image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-3 mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/l3d_projects/lsv3d/mesh/mesh_rend1.gif" title="Chair-1 Mesh Render" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="row justify-content-sm-center">
    <div class="col-sm-0 mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/l3d_projects/lsv3d/mesh/mesh_chair2.png" title="Chair-2 Image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-3 mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/l3d_projects/lsv3d/mesh/mesh_rend2.gif" title="Chair-2 Mesh Render" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="row justify-content-sm-center">
    <div class="col-sm-0 mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/l3d_projects/lsv3d/mesh/mesh_chair3.png" title="Chair-3 Image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-3 mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/l3d_projects/lsv3d/mesh/mesh_rend3.gif" title="Chair-3 Mesh Render" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Input Image v/s Mesh Render results from the model
</div>

### Quantative Results
The quantitativce results of the models acn be seen below. Specifically, it shows the results of the F1-score for the 3 models at different thresholds. Left-to-Right the figures are for *Voxels, Point Clouds,* and *Meshes*.

<div class="row justify-content-sm-center">
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/l3d_projects/lsv3d/eval_vox.png" title="Voxel Model F1 scores" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/l3d_projects/lsv3d/eval_point.png" title="Point Cloud Model F1 scores" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/l3d_projects/lsv3d/eval_mesh.png" title="Mesh Model F1 scores" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    F1 scores for the models. Left-to-Right: <em>Voxels, Point Clouds,</em> and <em>Meshes</em>
</div>
