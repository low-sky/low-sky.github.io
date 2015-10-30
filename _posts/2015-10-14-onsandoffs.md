---
layout: post
title: ONs and OFFs
---
The question came up as to whether you can do beam nodding on a telescope that doesn't explicitly support beam nodding.  Under some assumptions, it seems possible to do it with the calibrated scans alone.  If we define $$N$$ to be the ON scan, $$F$$ to be the OFF scan then the usual calibration gives

$$
\left(\frac{N-F}{F}\right)T_{\mathrm{sys}} = T_{A,0}
$$

or equivalently

$$
\left(\frac{N}{F}-1\right)T_{\mathrm{sys}} = T_{A,0}.
$$

If the scans are made intentionally or otherwise so that the source is in the OFF position rather than ON position, this would give a different spectrum, where the emission would appear in absorption.  In this case, a new antenna temperature would be derived:

$$
\left(\frac{F-N}{N}\right)T_{\mathrm{sys}} = T_A.
$$

Given this, we'd like to restore the spectrum that would be seen under the "normal" circumstances:

$$
\begin{eqnarray}
\left(\frac{F}{N}-1\right)&=&\frac{T_A}{T_{\mathrm{sys}}} \\
\frac{F}{N} & = & 1+ \frac{T_A}{T_{\mathrm{sys}}}\\
\frac{N}{F} & = & \left(1+ \frac{T_A}{T_{\mathrm{sys}}}\right)^{-1} \\
T_{A,0} = \left(\frac{N}{F}-1\right) T_{\mathrm{sys}} & = &  T_{\mathrm{sys}}
\left(\frac{1}{1+\frac{T_A}{T_{\mathrm{sys}}}}-1\right).
\end{eqnarray}
$$

Thus, if $$T_{\mathrm{sys}}$$ for every scan is known, the intended antenna temperature measurements for each scan can be recovered if the emission is processed in the OFF component of the scan.  As such, an ad hoc observing strategy that uses an OFF position where the ON position can be used to recover the original spectrum and a second spectrum from the OFF.  
