---
layout: post
title: The Elliptical Exegesis
---

In interferometry, deconvolving the image replaces the interferometer's ugly point spread function (PSF) with a nice well-behaved Gaussian.  The original PSF is formally the transform of where the samples are found in the Fourier ($uv$) plane.  Since changes in frequency and the relative weights of antennas can affect the importance or even presences of certain samples in the $uv$ plane, the interferometer PSF varies across an image mosaic and with frequency.  This means that, once deconvolved, the cleaned up beam is _also_ a function of frequency and position.  [CASA](https://casa.nrao.edu) does an excellent job of tracking all these effects in detail.  However, it means that the resolution of the image varies through an image.  This can be non-ideal.  In theory, you can deconvolve the image with a `restoringbeam='common'` call, but current versions of CASA are buggy.  My student Eric K. found the following code snippet.  It builds a fake image with elliptical resolution elements.  The beam position angle rotates and the order of the beams varies in the cube... but the cube has the same resolution elements.

```
im1 = ia.newimagefromarray(pixels=ia.makearray(0, [4, 4, 1, 4]))
for i, pa in enumerate([0, 20, 40, 60]):
    im1.setrestoringbeam(channel=i, major='4arcsec', minor='3arcsec',
                         pa="{}deg".format(pa))

im2 = ia.newimagefromarray(pixels=ia.makearray(0, [4, 4, 1, 4]))
for i, pa in enumerate([0, 60, 20, 40]):
    im2.setrestoringbeam(channel=i, major='4arcsec', minor='3arcsec',
                         pa="{}deg".format(pa))

print(im1.commonbeam())
print(im2.commonbeam())
```

This yields the following results, which should be identical but are not.
```
{'major': {'value': 4.211865471480522, 'unit': 'arcsec'}, 'pa': {'value': 29.99999999999998, 'unit': 'deg'}, 'minor': {'value': 3.658232394188034, 'unit': 'arcsec'}}
{'major': {'value': 4.343317398689631, 'unit': 'arcsec'}, 'pa': {'value': 29.25631919084969, 'unit': 'deg'}, 'minor': {'value': 3.5897767228849267, 'unit': 'arcsec'}}
```

This should be yielding a common beam that encompasses each of the contributing beams.  Then, each image could be convolved up to a larger resolution. However, this beam should be as small as possible to ensure a minimal loss of resolution.  Something is wrong and I suspect that the CASA solution applies a pairwise solution that is not robust in general.  

To that end, we should find another solution.  Since the argument of the exponential in a Gaussian has the form of an ellipse (or, as I recently learned a "quadratic form"), the problem reduces to finding finding the properties of ellipses which are the level sets of a Gaussian. The problem that needs solving is:

_Given a set of ellipses indexed with $i$ and having major axes $a_i$, minor axes $b_i$ and angles of rotation with respect to the $x$-axis $\phi_i$, find the minimum area ellipse enclosing all the ellipses. Assume that the ellipses have a common centre at the origin._

In researching this problem, we discovered that this problem reduces to a classic [convex optimization problem](http://cvxopt.org/examples/book/ellipsoids.html), and unfortunately that makes the problem fairly tricky. I have a proposed solution this problem.  I have not proven rigorously that this solution is minimum area but it is a bounding ellipse that is robust against order changes in the contributing Gaussians. The solution is an optimization.  I tried a few different construction approaches, but it seems like those are not terribly robust.  For simplicity, consider a ellipse in Cartesian coordinates.  The ellipse can be written as 

$$
\alpha x^2 + 2 \gamma xy + \beta y^2 = 1
$$

In terms of our previous notation for ellipses, we have

$$
\begin{eqnarray}
\alpha & = \frac{\cos^2 \phi}{a^2} + \frac{\sin^2 \phi}{b^2} \\
\beta  & = \frac{\sin^2 \phi}{a^2} + \frac{\cos^2 \phi}{b^2} \\
\gamma & = \cos \phi \sin \phi \left(\frac{1}{a^2} - \frac{1}{b^2} \right)
\end{eqnarray}
$$

The equation for an ellipse can then be written in snazzy "quadratic form" notation with $ \mathbf{x}^T \mathbf{A} \mathbf{x} = 1,$ 

where 

$$
\mathbf{x} = \left[\begin{array}{c} x \\ y \end{array}\right] \quad \mathrm{and}
\quad \mathbf{A} = \left[\begin{array}{cc} \alpha & \gamma \\ \gamma & \beta \end{array}\right].
$$

The power of this notation comes from the truism that point $\mathbf{x}_1$ is inside the ellipse defined by $\mathbf{B}$ if and only if $ \mathbf{x}_1^T \mathbf{B} \mathbf{x}_1 < 1. $ Thus, for a set of points that satisfies the equation of the ellipse for ellipse $\mathbf{A}$, these points are inside the ellipse defined by $\mathbf{B}$ iff $ \mathbf{x}^T \mathbf{B} \mathbf{x} < 1.$  Hence, we can test if one ellipse is inside another if, for the same point $\mathbf{x}$ has 

$$
\begin{eqnarray}
\mathbf{x}^T \mathbf{A} \mathbf{x} -  \mathbf{x}^T \mathbf{B} \mathbf{x} & \ge 0 \\
\mathbf{x}^T (\mathbf{A-B}) \mathbf{x}  & \ge 0.
\end{eqnarray}
$$ 

This particular form is familiar to linear algebraists since it is one of the conditions for the array $\mathbf{A-B}$ to be _non-negative_.  This must be true for all $\mathbf{x}$.  An array satisfies this form, then all its eigenvalues are non-negative or equivalently it hss a Cholesky decomposition.  Using this linaer algebra based test, we have a quick check on one ellipse being inside another.  

This constraint gives us a handle for performing an optimization.  We can minimize the area of the ellipse defined by $\mathbf{B}$ subject to the condition that the matrix $\mathbf{A-B}$ has a Cholesky decomposition.  If we have a set of $\mathbf{A}_i$ we check that this condition is true for each $\mathbf{A}_i$.  The area of the ellipse is just $\det \mathbf{B}$, so we aim to minimize $(\det \mathbf{B})^{-1}$.

This can be accomplished in `scipy.optimize.minimize`.  There are nominally constrained optimization algorithms such as `COBYLA`, but they were not functioning as intended.  Instead, I opted for the simpler method `Nelder-Mead` and put on a term that caused the objective function to jump to infinity if the non-negative matrix constraint is not satisfied.  The code seems to perform well.  For our use case, we are only optimizing over of-order 100 ellipses.  For an initial condition, I selected the bounding circle with radius equal to the maximum semi-major axis across the set of ellipses.

It turns out this is an area where we need work.  Finding the global minimum is tricky since it depends on the position angle (i.e., the optimization algorithms I tried do not really give a good convergence).  I've posed my first attempts [here](http://nbviewer.jupyter.org/gist/low-sky/1eba1ebebe3606d400da030d2024970f).

Now that we have a major and minor axis, the usual workflow is to then convolve by ellipses so that all planes / parts of the image have the same beam.  Having the maximum bounding ellipse ensures that every Gaussian can be convolved up to reach this elliptical size.  This takes advantage of the convolution of two elliptical Gaussians is a third elliptical Gaussian.  We can figure out the convolution kernel parameters that are needed to reach the target resolution. The math of this has been worked out and is already in the package `radio_beam` right about [here](https://github.com/radio-astro-tools/radio_beam/blob/master/radio_beam/beam.py#L316).

We can thus find the convolution kernel, and we usually then proceed with a digital convolution using fast Fourier transforms.  Another issue arises when the required convolution kernel is thin along one direction.  Consider, for example, convolving an ellipse with major axis of 1 unit, minor axis of 0.5 unit and an angle of $0^\circ$ to a round beam.  Nominally, the convolution kernel in the major axis direction has a width of zero and the convolution only needs to be carried out in one direction.  This causes problems under the usual work flow: normally, you construct a digital representation of the kernel and use the FFTs, but this kernel will not be Nyquist sampled in the major axis direction.  This will lead to terrible artifacts on convolution.

To avoid this problem we can go ahead an construct these thin kernels in the Fourier domain.  This is also formally incorrect.  Since the kernel is not Nyquist sampled in the original domain, the kernel should formally extend out to the edge of the Fourier domain without going to zero.  This is formally problematic since the Fourier domain has a toroidal topology (i.e., like a Pac-Man board) where moving off one side of the board wraps to the other side.  The convolution kernel runs right up to the edge of that domain.  However, I claim we can get away with this horrible feature as long as the original image data are Nyquist sampled.  In that case, there is no information in the image at high spatial frequencies, so the non-zero values of the kernel's Fourier transform will be multiplied by low amplitude values in the image Fourier transform.

[Here's my attempt to code this.](https://github.com/low-sky/py-low-sky/blob/master/ftplane_convolution.py)

Now we have a complete framework: find the minimal bounding ellipse, all beams up to it using the Fourier domain as necessary. 

