# main
hierarchical PointNets


capture local structures 

# How to
1. partitioning of the point set
each partition is defined as a neighborhood ball in the underlying Euclidean space
whose parameters include centroid location and scale
centroid: selected by FPS algorithm 
scale:
2. abstract sets of poitns or local features through a local feature learner(PointNet)

# abstraction level
1. Sampling layer
2. Grouping layer
Ball query and KNN
3. PointNet Layer(or adaptive version)
normalize coordinates of points before PointNet layer

# Point Feature Propagation for Set segmentation
use KNN for interpolation,
the process is repeated until we have propagated features to the original set of points

# experiments
...


# addtion
* Farthest Point Sampling
select the farthest point in each time to add the set until the condition is match

