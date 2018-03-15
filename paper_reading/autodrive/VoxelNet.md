# main
divides a point cloud into equally spaced 3D voxels 
and get feat from voxel feature encoding layer(VFE)
then RPN ...


# problem
1. point cloud: accurate but sparse and non-uniform,
effective range of sensors
2. image-based 3D detection(the accuracy of depth estimation is not good)

so this approach close gap between point set feature learning
and RPN for 3D detection task


# VFE

point-wise features with a locally aggregated feature


# Recent work
1. multi-modal fusion methods
the need for an addional camera that is time synchronized 
and calibrated with LiDAR

# details
1. Feature Learning Network
- Voxel Partition(equally spaced)
- Grouping (do nothing)
- Random Sampling(max number of points in each voxel is T)
- VFE
[x,y,z,r,x-v_x,y-v_y,z-v_z] here (v_x,v_y,v_z) is centroid of voxel
point-wise feartures f from fcn(a linear layer ,RELU and BN)
locally aggregated feature from Maxpool element-wisely
concat them
- reshape(C,D,H,W)
2. Convolutional Middle Layers
3. RPN
a probability score map and a regression map
4. Loss function

# How to reduce computation and memory
construct voxel coordinate buffer via one pass
reorganize the computed sparse voxel-wise structures to the dense voxel grid

# Training
just set diff parameters for car and other small objects
# data augmentation
1. perturbation independently to each ground truth 3D bounding box(collision test)
2. global scale augmentation
3. rotation along Z-axis(vehicle make a turn)

# experiments
show that VFE is better than hand-crafted
RPN is effective


