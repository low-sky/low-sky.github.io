---
layout: post
title: Units in UNWISE images
---

This is a small fragment developed by Adam Leroy for the data of [UNWISE](unwise.me).

IRSA ALLWISE mosaics are hard to use for building large images but do have well defined units.  UNWISE has vaguely specified units but Adam's sleuthing found that it is flux density per pixel with 1 count being 1 is a 22.5 Vega magnitudes in each band.  

WISE gives offsets in [Table 5 here](http://wise2.ipac.caltech.edu/docs/release/prelim/expsup/sec4_3g.html#WISEZMA).  Since we care about W4 images, the offset is 6.604.  

$$
m_{\mathrm{AB}} = m_{\mathrm{Vega}} + 6.604
$$

Using the [definitions of magnitudes](https://en.wikipedia.org/wiki/AB_magnitude) in both cases we get
$$
\begin{eqnarray}
-2.5\log_{10} \left(\frac{F_{22}}{\mathrm{Jy/pix}}\right) + 8.90 & = & -2.5\log_{10} (I) +22.5 + 6.604 \\ 
\log_{10} \left(\frac{F_{22}}{\mathrm{Jy/pix}}\right) &= &\log_{10} (I) -0.4(22.5+6.604-8.90) \\
\frac{F_{22}}{\mathrm{Jy/pix}} & = & 8.287\times 10^{-9} I \\
\frac{F_{22}}{\mathrm{MJy/sr}} & = & 8.287\times 10^{-15} \frac{I}{\Omega_{\mathrm{pix}}.
\end{eqnarray}
$$


