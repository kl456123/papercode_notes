

1. camera x=right ,y = down,z= forward
2. Velodyne: x =forward, y=left,z=up
3. GPU/IMU: x=forward,y=left,z=up


rectification




directory:
1. velo cloud points
2. image_00,image_01,image_02,image_03
translation between camera_0 and camera_x



Epipolar Geometry(对极几何)
Epipolar line
Epipolars
Epipolar plane
Fundamental Matrix:txR

Epipolar Constraint
Each pixel's match in another image can only be found on a line called
the epipolar line
# How to estimate the pose of camera
1. Get Esential Matrix from multiple correspondence match
2. extract rotation matrix and translation matrix

All rectified images satisfy the following two properties
1. All epipolar lines are parallel to the horizontal axis
2. Corresponding points have identical vertical coordinates


