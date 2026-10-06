# Towards Convex Formulations in Calibration

Technical report and associated Jupyter notebook about convex formulations for problems in camera calibration and geometric perception.

This repository uses a problem we term the __Similarity Registration under Known Correspondences__ (SRKC) to study a few convex formulations for problems in calibration.  We define SRKC as the registration of two point clouds in 3D under the assumption that they are related by a similarity transform in _Sim(3)_ and corrupted by isotropic Gaussian noise with unknown variance.

The technical report on convex formulations in calibration may be found at `report/calibration.pdf`.

The Jupyter notebook `towards-convex-calibration.ipynb` demonstrates two of the methods discussed: "vanilla" SRKC and quaternion SRKC (q-SRKC).  You may install the dependencies for the notebook from `requirements.txt`.

## Project Abstract

The following abstract is copied from the project report at [`report/calibration.pdf`](https://github.com/josephrhobbs/towards-convex-calibration/blob/master/report/calibration.pdf).

> Calibration is a critical step in building safe and reliable autonomous systems.  Cameras, LiDAR sensors, gyroscopes, inertial measurement units, and other devices give various information about the world around a system.  Effective algorithms for calibration can quickly give the user correct parameters that characterize those devices---previously unknown positions, scales, focal lengths, distortion coefficients, or orientations in space.  Many problems in calibration, however, suffer from various nonconvexities that make global estimation of these parameters difficult to determine correctly, certifiably, or in polynomial time.  Clever convex reformulations of these problems can often bypass these difficulties and achieve correct and certifiable solutions quickly.  Here, we study Similarity Registration with Known Correspondences (SRKC), a common problem in calibration and point cloud registration involving estimation over a Lie group under isotropic Gaussian noise.  We develop a convex formulation and show how it extends to two variants of the problem: quaternion SRKC (q-SRKC) and robust SRKC (R-SRKC).  We discuss applications of the methods developed here to real perception and calibration systems, and to preserve pedagogical value, we choose to implement the accompanying code in Python and release it as open-source.

## Measuring Error

The Jupyter notebook in this repository measures solver error using the __triple geodesic distance__ on the _Sim(3)_ manifold.  The equations below show the triple geodesic distance as the root-mean-square of geodesic distances on the positive reals (for scale), on _SO(3)_ (for rotation), and on 3-dimensional Euclidean space (for translation) respectively.

<p align="center">
<img src="https://github.com/josephrhobbs/towards-convex-calibration/blob/master/triple-geodesic.png" alt="Mathematical formulas for computing triple geodesic distance on the Sim(3) manifold." width="auto" height="200">
</p>

## Generative AI Statement

I believe that research, development, and writing are all deeply human processes that require human attention.  No part of this repository (including code, figures, or technical writing) was created or copyedited ("polished") using generative AI.
