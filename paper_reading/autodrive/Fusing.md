# main

fusion image view and BEV
1. use non-homogeneous pooling layer to transform features
between bird view map and front view map
2. use fusion features to do region proposal





# How to

sparse matrix M(for transformation)
feature map H_fxW_fxC
B=MF
where B is L_bxW_bxC
(some confusion)

cancat with target feature map for further processing
note that fusion should be applied to deeper layer
so that most info can be used except for sky or out of th range of view


# others
something about 2D detection


# experiment
fusion can help for detecting pedestrians


# math
the support of a real-valued function f is the subset of the domain containing 
those elements which are not mapped to zero
