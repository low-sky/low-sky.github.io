---
layout: post
title: Structures and Correlations
---

With a student, I've been working of developing structure function and correlation function approach to analyzing spectral line data cubes.  First, we've been working with the structure function of order $$p$$:

$$
S_p(\mathbf{\delta r},\delta v) = \left\langle \left|I(\mathbf{r},v)-I(\mathbf{r}+\mathbf{\delta r},v+\delta v) \right|^p\right\rangle_{\mathbf{x}}
$$

where $$p=2$$ usually.  We've investigated a set of properties including the noise behaviour of the structure function and the maximum value attainable.  The final thing to consider is the relationship between the structure function and the correlation function $$\xi(\delta r)$$.  In cosmology, the [correlation function](https://ned.ipac.caltech.edu/level5/March04/Jones/Jones5_2.html) is defined as the excess probability of finding a galaxy within a distance $$\delta \mathbf{r}$$ of another galaxy:

$$
dP = n \left[ 1+\xi(\delta \mathbf{\delta r}) \right] dV,
$$  

where $$n$$ is the volume density of galaxies and $$dV$$ is a volume element.  In a totally random universe, the probability of finding a galaxy would just be density integrated over the volume considered, so $$\xi(\delta r)=0$$.

If we were going to calculate the correlation function from a set of point masses, we would have to evaluate an estimator of the form 

$$
\xi(\mathbf{\delta r}) = \frac{r(r-1)}{n(n-1)} \frac{DD(\mathbf{\delta r})}{RR(\mathbf{\delta r})} - \frac{(r-1)}{n} \frac{DR(\mathbf{\delta r})}{RR(\mathbf{\delta r})} +1,
$$

based on the work of [Landy & Szalay (1983)](http://adsabs.harvard.edu/abs/1993ApJ...412...64L).  
Here, $DD$ is notation that means the 

We are interested in the relationship between $$\xi(\mathbf{\delta r})$$ and $$S_2(\mathbf{\delta r})$$ (ignoring for the moment the $$\delta v$$ component).  Furthermore, we want to consider a field, i.e., not a bunch of point-like galaxies but rather a continuous function.  We are specifically considering the case of images of molecular emission.  Instead of partitioning the emission into molecular clouds, we are instead going to calculate the correlation function between positions in an image. If we consider a pixelated image with intensity values $$I$$, we define the correlation between

![Correlation Function](/images/CorrelationFunc.png)

