---
layout: post
title: Structures and Correlations
---

With a student, I've been working of developing structure function and correlation function approach to analyzing spectral line data cubes.  First, we've been working with the structure function of order $$p$$:

$$
S_p(\mathbf{\delta r},\delta v) = \left\langle \left|I(\mathbf{r},v)-I(\mathbf{r}+\mathbf{\delta r},v+\delta v) \right|^p\right\rangle_{\mathbf{r}}
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

based on the work of [Landy & Szalay (1983)](http://adsabs.harvard.edu/abs/1993ApJ...412...64L).  Here, $$DD(\mathbf{\delta r})$$ is notation that means the number of galaxies (of $$n$$ total) found in the actual data with separations of $$\mathbf{\delta r}$$.  This must be a binned estimator where you consider the number in a small interval around $$\mathbf{\delta r}$$.  $$RR$$ is number of the separation between pairs of galaxies in a randomized set of $$r$$ galaxies, with the same selection volume as the original survey producing $$DD$$.  The term $$DR$$ is a mix term where one point is drawn from the original data list and one from the randomized sample.  Terms with random samples can be generated from multiple realizations and then averaged.

We are interested in the relationship between $$\xi(\mathbf{\delta r})$$ and $$S_2(\mathbf{\delta r})$$ (ignoring for the moment the $$\delta v$$ component).  Furthermore, we want to consider a field, i.e., not a bunch of point-like galaxies but rather a continuous function.  We are specifically considering the case of images of molecular emission.  Instead of partitioning the emission into molecular clouds, we are instead going to calculate the correlation function between positions in an image. If we consider a pixelated image with intensity values $$I$$, we define the correlation function between two pixels using the geometry described in this figure:

![Correlation Function](/images/CorrelationFunc.png)

If we were considering these pixels as being regions filled with galaxies and the number of galaxies in the pixels are $$I(\mathbf{r}_1)$$ and $$I(\mathbf{r}_2)$$ respectively, then the correlation function with have a contribution from this pair of pixels that is equal to the number of possible data pairs that could be formed between these two values: $$I(\mathbf{r}_1) \cdot I(\mathbf{r}_2)$$.  Then, the $$DD$$ term of the correlation function would look like:

$$
DD(\mathbf{\delta r}) = \langle I(\mathbf{r}) \cdot I(\mathbf{r+\delta r}) \rangle_{\mathbf{r}}.
$$

Similarly, the $$RR$$ term would look a lot like the average product of a bunch of random draws from the pixels $$I(\mathbf{r})$$.

$$
RR(\mathbf{\delta r}) = \frac{1}{n_i n_j} \sum_{i,j} I(\mathbf{r}_i) \cdot I(\mathbf{r}_j).
$$

Since the averages represent random draws from the image values, there is no correlation between the draws.  Thus, we get that the average value of the product is the product of the averages:

$$
RR(\mathbf{\delta r}) = \frac{1}{n_i} \sum_{i} I(\mathbf{r}_i) \cdot \frac{1}{n_j}\sum_j I(\mathbf{r}_j) = \left[\langle I(\mathbf{r}) \rangle_{\mathbf{r}}\right]^2.
$$

Or, this is the mean value of the image, squared.  Because Monte Carlo beats actually thinking any day, I verified this by doing many random draws from an image and calculating the average product.  It checks out.  By similar reasoning, I think that $$DR==RR$$ for images, but I haven't checked this.

Finally, the connection to structure functions comes from expanding the square in the structure function:

$$
\begin{eqnarray}
S_2(\mathbf{\delta r}) & = & \left\langle \left[I(\mathbf{r})-I(\mathbf{r}+\mathbf{\delta r}) \right]^2\right\rangle_{\mathbf{r}} \\
& = &  \left\langle \left[I(\mathbf{r}) \right]^2 \right\rangle + \left\langle \left[I(\mathbf{r+\delta r}) \right]^2 \right\rangle - 2 \left \langle I(\mathbf{r}) I(\mathbf{r+\delta r})\right\rangle \\
& = &  \left\langle \left[I(\mathbf{r}) \right]^2 \right\rangle + \left\langle \left[I(\mathbf{r+\delta r}) \right]^2 \right\rangle - 2  \left[\langle I(\mathbf{r}) \rangle\right]^2 \xi(\mathbf{\delta r})
\end{eqnarray}
$$