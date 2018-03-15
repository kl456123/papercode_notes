# main
use point cloud as input of CNN
for applications ranging from object classification and segmentation


# properties of Point sets

- Unordered
- interaction among points
- invarinace under transformation


# PointNet architecture

1. max pooling layer
symmetric for unorder set
2. local and global information combination structure
concat
3. two joint alignment netwroks that align both input points and point features
T-net , invariant to transformations
applied in input and feature map
due to higher dimension of feature map,regularization term is applied to constrain 
the feature transformation matrix to be close to orthogonal matrix
 L_reg = || I-AA^T||^2


