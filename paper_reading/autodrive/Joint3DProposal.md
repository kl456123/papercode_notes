# main idea
exploit features from both point cloud and RGB data to generate region proposals.

# some problem
1. the gap between the 2D and 3D
(low resolution of 3D input data and the deterioration of its quality as 
a function of distance)
2. descriptive performance metrics
- 3D and BEV AP
- the average error in distance
- the average error in estimating the centroid
all fail to penalize the global orientation angle estimate

# How to deal with those
1. a novel RPN that can handle features from multiple input modes
2. use Aveage Heading Similarity(AHS) to inplace of Average orientation Similarity(AOS)

# Recent work
1. use hand-crafted geometric features to score 3D sliding windows,select top K as region proposals
2. projects LIDAR point cloud to the front view which is used as an input to a FCN to generate bboxes
3. VoxelNet leverages point-wise features extracted on a 3D voxel grid(slower)
4. 2D object detectors for proposals generation, followed by amodal 3D extent regression(Frustum-based PointNet)
(poorly in low light)
5. 3D RPN(MV3D) too small to extract informative features


# details
- two feature extractors,one for each input view(based VGG + 4xbilinear upsampling)
- generate anchors in 3D and extract feature crops using crop and resize(the equal-sized)
- dimemsionality reduction via 1x1 conv
- 3D proposal Generation(3D RPN-based)
background anchors are determined by calculating the 2D IoU in BEV(diff class has diff threshold)
2D NMS(diff class has diff num of proposals)
- bbox encoding
four corners and two height values representing the top and bottom corner offsets
(closest match for corners)
- orientation vector regression
extract four possible orientations of the bounding box and then choose the closest to the regressed vector
(How to do regression?)
- Generate final detctions
crop and resize by using proposals(different from using anchors before)
then do some prediction like RPN(bbox smoothL1 loss,orientation loss CE loss for cls)
(note that calculate IoU in BEV due to spare space)

# Training
two networks,one for the car and the other for pedestrian and cyclist classes,trained jointly

# AHS
like ap(VOC2008)
s(r) = 1/....(both localization and global orientation estimation are considered)


# experiments
1. using the regressed orientation vector can help
2. early fusion is not better than other but is faster at inference time





question:
what is \theta,why we use four corner to estimate it?
