

* extend PointsNet for the purpose of 3D object detection


# Recent work:

1. convert 3D point cloud to images by projection(image CNN) 
2. or to volumetric girds by quantization(voxel 3D CNN)

* disadvantages:
may obscure natural 3D  patterns and invariances of the data


# How to do

1. extract the 3D bounding frustum of an object by extruding 2D bounding boxes from image
detectors .
2. within the 3D space trimmed by each of the 3D frustums , we consecutively perform 3D object
instance segmentation and 3D bounding box regression using two variants of PointNet.

* advantages:
1. 3D-centric view(WHY: more naturally parameterized and captured by learners)


# 3D object detection from RGB-D Data
- Front view image based methods
- Bird's eye view based methods
(cons:
1. lags behind in detecting small objects,
2. cannot easuly adapt to scenes with multiple objects in vertical direction)
- 3D based methods(expensive cost)
- Deep Learning on Point Clouds
(some still require quantitization of point clouds with certain voxel resolution)
(so extend PointNets by using point clouds directly)

each object is represented by a class and an amodal 3D bounding box
a class: one hot encode
a amodal box: size(h,w,l),center(cx,cy,cz),orientation(\theta,\phi,\x)(just \theta is considered here)

# details

## Frustum Proposal
1. Due to the low resolution of data produced by most 3D sensors,
we leverage mature 2D object dete tor to propose 2D object regions
in RGB images asd well as to classify objects
(camera projection matrix)
(Y ~CX)
(y1,y2) = -f/x3(x1,x2)

2. Normalize the frustums by rotating them toward a center view

## 3D instance segmentation
- segment instances in 3D point cloud instead of in 3D image or depth map
using binary classification like MaskRCNN
(concatenate the one-hot vector to the intermediate point cloud features for instance segmentation)
(using PointNets++)

- Normalize its coordinates to boost the translational invariance
(just by subtracting XYZ values by its centroid)
(note that do not scale the point cloud)
(those transforms are critical)

## Amodal 3D Box Estimation

1. Learning-based 3D alignment by T-Net
just a light-weight regression PoitnNet to estimate the true center of the complete object
and then transform the coordinate such that the predicted center becomes the origin
(note that using C_pred = C_mask+\delta{C_{t-net}}+ \delta{C_{box-net}} to recover the origin)

2. Amodal 3D box estimation PointNet
like object classification ,the output is parameters for a 3D bounding box
pre-define NS size templates and NH equally split angle bins.
classify size/heading(NS scores for size,NH scores for heading)
residual dimensions for each category
(3xNS residual dimensions for height,width,length,
NH residual angles for heading)

output(3+4xNS+2xNH)

## Trainingn with multi-task losses
instance segmentation PointNet: L_seg
T-Net: L_{c1-reg}
amodal box estimation PiontNet: L_{c2-reg}
(softmax is used for all classification tasks and smooth-l1 is for regression cases)
L_{multi-task} = L_seg + \lambda(+..+..+L_corner)

- Corner Loss
the loss make all loss jointy optimize for best 3D box estimation
L_corner = \sum\sum...
(what is residual regression approach for heading and size regression?)


# Disadvantages:
1. inaccurate pose and size estimation in a sparse point cloud(should combine image with point cloud)
2. multiple instance from the same category in a frustum
3. sometimes 2D detector misses objects due to dark lighting or strong occlusion


# supplementary

1. the framework can be extended proposals to bird's eye view prpoposals and how combining BV and
RGB proposals can further imporve detection performance.

2. data augmentation
- 2D box augmentation
random translation and scaling
- frustum point cloud augmentation
randomly sample a subset of points
randomly flip the frustum point cloud(after rotating the frustum to the center)
shifting the entire frustum point cloud in Z-axis direction to augment the depth of points


confusion(TODO):
1. set abstraction layers and Point feature propagation layers in PointNet
2. hybrid of classification and regression formulations
3. read code
4. amodal 2D and 3D box annotations


