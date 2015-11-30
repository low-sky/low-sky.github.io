---
layout: post
title: Degeneracy Pressures 
---

In ASTRO 320, we motivated a cartoon view of degeneracy pressure based on filling states of phase space.  We argued that a one-dimensional phase space can be separated into cells of phase volume equal to Planck's constant $$h$$.  Into each cell, we can pack at most 2 fermions (usually electrons), where the 2 comes from the two spin states of the electron.  This means that in a three dimensional phase space, the cell volumes are $$h^3 = \Delta x \Delta y \Delta z \Delta p_x \Delta p_y \Delta p_z$$, and each cell can hold the two electrons.  

Now, we ask the question "What is the maximum momentum found in a gas of fermions given a volume density of fermions $$N_e$$?"  If the system is hot, then this question is answered by the Maxwell-Boltzmann velocity distributions and can be figured out in terms of statistical mechanics.  However, if the thermal energy is negligible, this question will be "what is the maximum density in phase space we can achieve by packing the particles in at their smallest possible momenta?"  (In the intermediate case, we turn to [Fermi-Dirac statistics](https://en.wikipedia.org/wiki/Fermi%E2%80%93Dirac_statistics) for the answer).

Focusing on the no-thermal-energy case, we start filling states from $$p=0$$ up to some $$p_{\mathrm{max}}$$.  If $$N_{\mathrm{tot}}$$ particles fill a volume $$V$$ and cover up to this maximum momentum, they occupy a volume of phase space equal to
$$
\frac{4\pi}{3} p_{\mathrm{max}}^3 V.
$$
The minimum possible value for $$p_{\mathrm{max}}$$ occurs when this phase volume equals the minimum possible value, which is
$$
\frac{h^3}{2} N_{\mathrm{tot}},
$$
where the 2 accounts for the two spin states. Equating these two expressions and solving for $$p_\mathrm{max}$$ gives
$$
\begin{eqnarray*}
\frac{4\pi}{3} p_{\mathrm{max}}^3 V & = &\frac{h^3}{2} N_{\mathrm{tot}}\\
p_{\mathrm{max}}^3 & = & \frac{3 h^3}{8\pi} \frac{N_{\mathrm{tot}}}{V} \\
p_{\mathrm{max}}^3 & = & \frac{3 h^3}{8\pi} N_e \\
p_{\mathrm{max}} & = & \left[\frac{3 h^3}{8\pi} N_e \right]^{1/3}.
\end{eqnarray*}
$$
Here, we have replaced $$N_{\mathrm{tot}}/{V}$$ with the electron volume density $$N_e$$.  




To turn this into an equation of state for the degeneracy pressure, we have to understand how the mo

