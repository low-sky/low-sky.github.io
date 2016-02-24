---
layout: post
title: Fitting through RADEX
---

A stumbling block for fitting ammonia via RADEX is that RADEX doesn't account for hyperfine structure.  The RADEX fitter for $$\mathrm{N_2 H}^+$$ has all this built in, but we will assume a decoupled system where all the hyperfine states are uniformly coupled.  The wrinkle that emerges is then than the line width of a complex of hyperfines isn't the same as the line width of a Gaussian since the optical depth is then split into a multitude of lines.  We can simulate this effect and make a correction between the RADEX line width and the underlying line width that typifies the optical depth.  RADEX is interested in the peak optical depth that typifies the line and assumes a Gaussian profile for ammonia.  We want to modify the line width so that we have the same peak optical depth as is appropriate for a (1,1) line with hyperfine splitting.  Thus,

$$
\tau_{max} \sqrt{2\pi}\sigma^\prime_{v} = \tau_{\max} 
$$