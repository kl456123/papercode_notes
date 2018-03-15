


principal axis:
vertical with image plane(film)

pinhole

Focal length:
distance between hole pin and film

intrinsic matrix:
    fx,s,x0
K = 0,fy,y0
    0, 0, 1

principal point:
vertix of principal axis and image plane

principal point offset:
principal point relate to origin of film

axis skew

extrinstic matrix:
E = (R|RT)(R refers to rotation,T refers to 3D coordinations of camera)

rotation matrix and offset matrix

distortion coefficients

camera resectioning to estimate the parameters of len


coordination system:
z axis: forward
x axis: up
y axis: coming out of image plane to viewer

# camera calibration
1. geometric calibration
calibration matrix = KR(I|T) = C(3x4)
2. color calibration

# some factor
- image center
the foucs of expansion and the cneter of perspective projection
- scaling factors
- skew factor
- lens distortion

optical axis: the axis passes through the center of curvature of each surface
mechanical axis: centerline of the outer cylinderical edge of the lens
tolerance between them is called decentration


* retinal plane(image)
* virutla image or virtual retinal plane
(placed between center and the 3D object at a distance f from O)
* camera refernece system
centered at the pinhole O such that the axis k is perpendicular 
to the image plane and points toward it
* aperture size
as the aperture size decreases ,the image gets sharper but darker


# How to transform from 3D point in an arbitrary world reference system to the image plane
1. translation vector
2. pixels to physical measurements
3. camera reference system to world reference system
* 11 degrees of freedom
5 from the intrinsic camera matrix,
3 from extrinsic rotation and
3 from extrinsic translation
equation
P' = K[R T]P_w = MP_w

combine translation with rotation matrix multiplication
[v'] = [R t][v]
[1]  = [0 1][1]

scale a vector
* affine transformation
T = [RS t]
    [0 1]
* projective transformation
final row of T is not [0 0 0 1]
* isometric transformation
preserve distances, can be described as a rotation R and translation t
* affine transformation
preserve points ,straight lines,and parallelism.

point(a,b,0) and line([0,0,1]^T) at infinity

* vanishing point
v = Kd

* baseline
O1 and O2

* Eight-Point algorithm and the Normalized version

# How to image rectification
1. find as many possible matches between two images to find the fundamental matrix
use SIFT descriptors with FLANN based matcher
2. find the Fundamental Matrix
3. find epilines(epilines corresponding to the points in first image is drawn on second image)

note that images with good resolution and many non-planar points sould be used
