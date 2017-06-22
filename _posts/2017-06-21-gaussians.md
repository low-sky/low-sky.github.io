---
layout: post
title: Ellipses and Convolutions
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

In researching this problem, we discovered that this problem reduces to a classic [convex optimization problem](http://cvxopt.org/examples/book/ellipsoids.html), though that solution really only matters for the case where the centres of the ellipses are not 

I have a proposed solution this problem.  I have not proven rigorously that this solution is minimum area but it is a bounding ellipse that is robust against order changes in the contributing Gaussians. The solution works like this.

From $\{a_i\}$ find the maximum semi-major axis $a_{\mathrm{max}}$ and the position angle corresponding to this ellipse $\phi_{\mathrm{max}}$.  By construction, the circle with radius $a_{\mathrm{max}}$ encloses all the ellipses.

For each of the remaining ellipses, consider where the ends of the semi-major axes of the over ellipses fall in the frame rotated such that the major axis of the largest ellipses lies along the $x$-axis.  Specifically, we need to consider the points

$$
\begin{eqnarray}
x_i' = & a_i \cos \Delta \phi_i \\
y_i' = & a_i \sin \Delta \phi_i
\end{eqnarray}
$$

where $\Delta \phi_i = \phi_i - \phi_{\mathrm{max}}$.  We want to identify the ellipse with major axis $a_{\mathrm{max}}$ and minor axis $b_i'$ that goes through this point.  By the definition of an ellipse, we know that 

$$
\frac{x_i'^2}{a_{\mathrm{max}}^2} + \frac{y_i'^2}{b'_i^2} = 1
$$

so that 

$$
b'_i = \left(\frac{a_i^2 \sin^2 \Delta \phi_i}{1 - \frac{ a_i^2 \cos^2 \Delta \phi_i}{a_{\mathrm{max}}^2}}\right)^{1/2}.
$$

Then, the minimum bounding ellipse is constructed as the maximum over the $b'_i$: $b_{\mathrm{max}} = \max b'_i$.