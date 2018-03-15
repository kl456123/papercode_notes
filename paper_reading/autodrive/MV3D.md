# main
encode the sparse 3D point cloud with a compact multi-view representation
proposal network generates 3D bbox from BEV and then fusion region-wise
features from multiple views


# Recent work
1. 3D object proposals 
3DOP designs some depth features in stereo point cloud to score 
a large set of 3D candidate boxes

Mono3D exploits the ground plane prior and utillizes 
some segmentation feature to generate 3D proposals
from a single image



# 3D point cloud representation

1. BEV representation
height:
discretize the proejcted point cloud into a 2D grid with resolution of 0.1m
height feature is computed as maximum height of the points in the cell
(point cloud is devided equally into M slices)

intensity:
reflectance value of the point which has maximum height in each cell

density:
the number of points in each cell
(normalize it using min(1.0,log(N+1)/log(64)))
(M+2)-channel features

2. Front View Representation
project pont cloud to a cylinder plane to generate a dense front view map
encode the front view map with three-channel features,which are height ,distance and intensity
(little confusion)

3. 3D proposal Network
use BEV to get bbox
(x,y,z,l,w,h)
x,y is the varying positions, z can be computed based on the camera height and object height
upsample using 2x bilinear upsampling after the last conv layer in the proposal network

4. Multi-View ROI Pooling
- three views
BV,FV(how to get),RGB
- Deep Fusion
early fusion
late fusion
deep fusion(fuses multi-view features hierarchically)
join operation(concatenation,summation)
5. Network Regularization
- drop-path training
- auxiliary losses
