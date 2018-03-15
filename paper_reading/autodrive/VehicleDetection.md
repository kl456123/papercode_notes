# main
FCN detect and localize the object


# some others
1. azimuth angle and elevation angle
2. cylinder project


# details

1. Data Preparation
\theta = atan2(y,x)
\phi = arcsin(z/sqrt(x*x+y*y+z*z))
r = floor(\theta/\delta{\theta})
c = floor(\phi/\delta{\phi})
* note that 
    - the point nearer to the observer is kept
    - elements in 3D positions where no 3D points are projected into are filled with zero

2. Network architecture
* FCN and two branch for predicting box and classes
* down-sampled by 4 horizontally and 2 vertically to make resolutions along any direction same 

3. Prediction Encoding
...
c'_p = R^T(c_p-P)

4. Traning Phase
- Data Augmentation
randomly zooming or rotating the original images to synthesis more training samples

- Multi-Task Training
- Training strategies
re-weighting
randomly discarding redundant negative losses
- balancly vehicle samples at differenet distances



