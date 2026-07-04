# FlamApp Submission

## Final Result
"\left(t*\cos(30^\circ)-e^{0.03\left|t\right|}\cdot\sin(0.3t)\sin(30^\circ)+55,42+t*\sin(30^\circ)+e^{0.03\left|t\right|}\cdot\sin(0.3t)\cos(30^\circ)\right)"



## Process Explanation

### 1. Problem Analysis

The raw samples in `xy_data.csv` form a wave-shaped curve that has been moved away from the origin and rotated by an unknown angle. The shape is not random, it matches a parametric wave with an exponential envelope and sinusoidal modulation.

### 2. The Geometric Shortcut

After translating the data by $(-X, -42)$ and applying the inverse rotation by $-\theta$, the rotated x-coordinate becomes the parameter $t$. In that un-rotated coordinate system, the curve simplifies to a standard wave function:

$$x_{\mathrm{rot}} = t$$

$$y_{\mathrm{rot}} = e^{Mt}\sin(0.3t)$$

This is why the curve can be fit by optimizing only three parameters: the rotation angle $\theta$, the exponential factor $M$, and the horizontal shift $X$.

### 3. Optimization Setup

I used Python's `scipy.optimize.differential_evolution` to search the allowed parameter ranges: $0^\circ < \theta < 50^\circ$, $-0.05 < M < 0.05$, and $0 < X < 100$. The objective function computes the inverse transformation, predicts the rotated curve, and minimizes the L1 distance, also known as Mean Absolute Error, between the observed coordinates and the predicted curve.
