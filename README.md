# Towards Convex Formulations in Calibration

Technical report and associated Python code detailing convex formulations for problems in camera calibration and geometric perception.

This repository uses a problem we call the __Similarity Registration under Known Correspondences__ (SRKC) to study a few convex formulations for problems in calibration.  We define SRKC as the registration of two point clouds in 3D under the assumption that they are related by a similarity transform in _Sim(3)_ and corrupted by isotropic Gaussian noise with unknown variance.

The technical report on convex formulations in calibration may be found at `report/calibration.pdf`.

The Jupyter notebook `code/towards-convex-calibration.ipynb` demonstrates two of the methods discussed: "vanilla" SRKC and quaternion SRKC (q-SRKC).  You may install the dependencies for the notebook from `requirements.txt`.

## Example Registration Result

The following shows a registration result on the Stanford bunny ([link to point cloud](https://gist.githubusercontent.com/bigsnarfdude/ac6b9911f34630d5b24508e628cfd0b1/raw/8b1ae1fa66b576bc780e7cbc3550da51ffdd80af/bunny.pcd)).  The "source" point cloud is shown in _blue_ and a "target" point cloud (translated by an unknown similarity transform and perturbed by isotropic Gaussian noise) is shown in _orange_.  We then estimate the similarity transform using a convex optimization and apply the estimated transform to the source point cloud to obtain the result shown in _green_.  This result is then translated two units to the right (+X) to show the reader the result more clearly.

<p align="center">
<img src="https://github.com/josephrhobbs/towards-convex-calibration/blob/master/images/srkc.png" alt="Registration result for the Stanford bunny" width="auto" height="500">
</p>

## Noise vs. Error Plot

We compare measurement noise (in decibels) and solver error (computed using _triple geodesic distance_, see below) in the plot below.  Measurement noise varies between -80 decibels and 20 decibels, in which +20 dB of measurement noise indicates 10 times the characteristic dimension.  We define the _characteristic dimension_ (mean distance of a point from the origin) of the point cloud under test to be unity.  On an Intel(R) Xeon(R) CPU (2.20GHz) the solver achieves a p95 (tail) latency of __38 milliseconds__.

<p align="center">
<img src="https://github.com/josephrhobbs/towards-convex-calibration/blob/master/images/noise-vs-error.png" alt="Noise versus solver error for the SRKC solver" width="auto" height="500">
</p>

## Project Abstract

The following abstract is copied from the project report at [`report/calibration.pdf`](https://github.com/josephrhobbs/towards-convex-calibration/blob/master/report/calibration.pdf).

> Calibration is a critical step in building safe and reliable autonomous systems.  Cameras, LiDAR sensors, gyroscopes, inertial measurement units, and other devices give various information about the world around a system.  Effective algorithms for calibration can quickly give the user correct parameters that characterize those devices---previously unknown positions, scales, focal lengths, distortion coefficients, or orientations in space.  Many problems in calibration, however, suffer from various nonconvexities that make global estimation of these parameters difficult to determine correctly, certifiably, or in polynomial time.  Clever convex reformulations of these problems can often bypass these difficulties and achieve correct and certifiable solutions quickly.  Here, we study Similarity Registration with Known Correspondences (SRKC), a common problem in calibration and point cloud registration involving estimation over a Lie group under isotropic Gaussian noise.  We develop a convex formulation and show how it extends to two variants of the problem: quaternion SRKC (q-SRKC) and robust SRKC (R-SRKC).  We discuss applications of the methods developed here to real perception and calibration systems, and to preserve pedagogical value, we choose to implement the accompanying code in Python and release it as open-source.

## Measuring Error

The Jupyter notebook in this repository measures solver error using the __triple geodesic distance__ on the _Sim(3)_ manifold.  The equations below show the triple geodesic distance as the root-mean-square of geodesic distances on the positive reals (for scale), on _SO(3)_ (for rotation), and on 3-dimensional Euclidean space (for translation) respectively.

<p align="center">
<img src="https://github.com/josephrhobbs/towards-convex-calibration/blob/master/images/triple-geodesic.png" alt="Mathematical formulas for computing triple geodesic distance on the Sim(3) manifold" width="auto" height="200">
</p>

## Generative AI Statement

I believe that research, development, and writing are all deeply human processes that require human attention.  No part of this repository (including code, figures, or technical writing) was created or copyedited ("polished") using generative AI.
