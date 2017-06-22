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

This yields the following results, which should be identical.
```
{'major': {'value': 4.211865471480522, 'unit': 'arcsec'}, 'pa': {'value': 29.99999999999998, 'unit': 'deg'}, 'minor': {'value': 3.658232394188034, 'unit': 'arcsec'}}
{'major': {'value': 4.343317398689631, 'unit': 'arcsec'}, 'pa': {'value': 29.25631919084969, 'unit': 'deg'}, 'minor': {'value': 3.5897767228849267, 'unit': 'arcsec'}}
```

This should be yielding a common beam that encompasses each of the contributing beams.  Then, each image could be convolved up to a larger resolution. However, this beam should be as small as possible to ensure a minimal loss of resolution.  Something is wrong and I suspect that the CASA solution applies a pairwise solution that is not robust in general.  

To that end, we should find another solution.  The problem is:

_Given a set of ellipses indexed with $i$ and having major axes $a_i$, minor axes $b_i$ and angles of rotation with respect to the $x$-axis $\phi_i$, find the minimum area ellipse enclosing all the ellipses. Assume that the ellipses have a common centre at the origin._

In researching this problem, we discovered that this problem reduces to a classic [convex optimization problem](http://cvxopt.org/examples/book/ellipsoids.html), though that solution really only matters for the case where the centres of the ellipses are not 

I've attempted to solution this problem.  I have not proven that this solution is minimum area but it is robust against order changes in the contributing Gaussians.  

