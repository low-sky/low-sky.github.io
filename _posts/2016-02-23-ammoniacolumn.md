---
layout: post
title: Ammonia column densities
---

In the continuing quest for ammonia column densities, we return to the question of how to turn observables into the total optical depth for a line.  We have several options in front of us, all of which are nominally equivalent.

Friesen et al. (2009):

$$N(1,1) = \frac{8\pi\nu^2}{c^2} \frac{g_1}{g_2} \frac{1}{A_{1,1}} \frac{1+\exp\left(-h\nu_0/k_B T_{ex}\right)}{1-\exp\left(-h \nu_0/k_B T_{ex}\right)} \int \tau(\nu) d\nu$$

Rosolowsky et al (2008):

$$N(1,1) = \frac{8 \pi k \nu_0^2}{h c^3} \frac{1}{A_{1,1}} \sqrt{2\pi}\sigma_\nu (T_{ex}-T_{bg})\tau$$

Mangum and Shirley (2015):

$$N_{tot} = \frac{3 h}{8 \pi \mu^2 R_i} \frac{J_u(J_u+1)}{K^2}
\frac{Q_{rot}}{g_J g_K g_I} \frac{\exp{E_u/k_B T_{ex}}}{\exp{h \nu/k_B T_{ex}} - 1} \left[\frac{\int T_R dv}{f\left(J_\nu(T_ex)-J_\nu{T_B}\right) }\right]$$

I think the right way to approach this is to throw back all the way to Rybicki and Lightman style to model the formation of the line.  Note that there really are several temperatures in play:

*  $$T_K$$ is the kinetic temperature of the system, which is what we really care about.
*  $$T_R$$ is the rotation temperature which is the excitation temperature / what you plug into Boltzmann to get the level population between the (1,1) and (2,2) states.
*  $$T_{\mathrm{ex}}$$ is the radiative excitation temperature of the lines in question, i.e. between the symmetric ($$\ell$$) and antisymmetric ($$u$$) state of the line or the upper/lower levels of the individual $$(J,K)$$ states.  We will usually be referring to the (1,1) line in this case.

Going all the way to the blast from the past, we have the opacity coefficient as defined by radiative properties and statistical mechanical considerations as

$$ \kappa_\nu = \frac{c^2}{8\pi} \frac{1}{\nu_0^2} \frac{g_u}{g_\ell} n_{\ell} A_{u\ell} \left[1-\frac{h\nu_0}{k T_{\mathrm{ex}}}\right] \phi(\nu),$$

where $$\phi(\nu)$$ is the line profile function such that $$\int \phi(\nu)d\nu=1$$.  Integrating over line of sight and frequency gives the total column density of the  lower state of the (1,1) line:

$$ \tau = \int \kappa_\nu ds d\nu  =\frac{c^2}{8\pi} \frac{1}{\nu_0^2} \frac{g_u}{g_\ell} N_{\ell} A_{u\ell} \left[1-\frac{h\nu_0}{k T_{\mathrm{ex}}}\right]$$
