---
layout: post
title: Units in IPHAS images
---

To finish up extragalactic star formation rates, we need H$$\alpha$$ images of the Galactic plane.  Here, the [IPHAS survey](http://www.iphas.org/) does the best job of providing coverage thanks to the [VTSS](http://www.phys.vt.edu/~halpha/) going quietly into the night.  The latest release is [DR2](http://adsabs.harvard.edu/abs/2014MNRAS.444.3230B). The data are photometric, but they are in optical people units.  Specifically, every image has a well defined PHOTZP such that, in the usual way, 

$$
m_{\mathrm{Vega}} = -2.5\log_{10} I + \mathrm{PHOTZP}
$$ 

The [DR2 page](http://www.iphas.org/images/) gives that magnitude zero in the H$$\alpha$$ filter corresponds to 

$$
F_0 = 1.56\times 10^7~\mathrm{erg/s/cm^2}
$$

As such,

$$
\begin{eqnarray}
-2.5\log_{10} \left( \frac{F_{\mathrm{H}\alpha}}{F_0} \right) & = & -2.5\log_{10} I + \mathrm{PHOTZP} - 0.0 \\
F_{\mathrm{H}\alpha} & = & 10^{-0.4\mathrm{PHOTZP}} F_0 I 
\end{eqnarray}
$$

