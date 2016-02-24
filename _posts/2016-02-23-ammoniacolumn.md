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
\frac{Q_{rot}}{g_J g_K g_I} \frac{\exp{E_u/k_B T_{ex}}}{\exp{h \nu/k_B T_{ex}} - 1} \left[\frac{\int T_{\mathrm{rot}} dv}{f\left(J_\nu(T_ex)-J_\nu{T_B}\right) }\right]$$

I think the right way to approach this is to throw back all the way to Rybicki and Lightman style to model the formation of the line.  Our previous work fits the optical depth and then infers a column density.  Now we are using the column as a free parameter and then determining the optical depth from the column and excitation conditions.  

First, there are three temperatures in play:

*  $$T_K$$ is the kinetic temperature of the system, which is what we really care about.
*  $$T_{\mathrm{rot}}$$ is the rotation temperature which is the excitation temperature / what you plug into Boltzmann to get the level population between the (1,1) and (2,2) states.
*  $$T_{\mathrm{ex}}$$ is the radiative excitation temperature of the lines in question, i.e. between the symmetric ($$l$$) and antisymmetric ($$u$$) state of the line or the upper/lower levels of the individual $$(J,K)$$ states.  

Going all the way back in time to Rybicki and Lightman Equation 1.80 (LTE), we have the opacity coefficient as defined by radiative properties and statistical mechanical considerations as

$$ \alpha_\nu = \frac{h\nu_0}{4\pi} n_l B_{lu} \left[1-\exp\left(-\frac{h\nu_0}{kT_{\mathrm{ex}}}\right)\right] \phi(\nu)$$

plus some things that are always true

$$ g_l B_{lu} = g_u B_{ul}$$

and 

$$ A_{ul} = \frac{2 h \nu_0^3}{c^2} B_{ul}.$$

Cramming this together in terms of quantum coefficients gives:

$$ \alpha_\nu = \frac{c^2}{8\pi} \frac{1}{\nu_0^2} \frac{g_u}{g_l} n_{l} A_{ul} \left[1-\exp\left(-\frac{h\nu_0}{kT_{\mathrm{ex}}}\right)\right] \phi(\nu),$$

where $$\phi(\nu)$$ is the line profile function such that $$\int \phi(\nu)d\nu=1$$.  Integrating over line of sight and frequency gives the total column density of the _lower_ (symmetric) state of the (1,1) line:

$$ \tau = \int \alpha_\nu\, ds\, d\nu  =\frac{c^2}{8\pi} \frac{1}{\nu_0^2} \frac{g_u}{g_l} N_{l} A_{ul} \left[1-\exp\left(-\frac{h\nu_0}{kT_{\mathrm{ex}}}\right)\right]$$

Because the excitation temperature defines the ratio of the lower to the upper state, we can correct $$N_l$$ to $$N_{(1,1)}$$.

$$\frac{N_u}{N_l}=\frac{g_u}{g_l}\exp\left(-\frac{h\nu_0}{kT_{\mathrm{ex}}}\right)$$

so 

$$N_l=\frac{N_{(1,1)}}{1+\frac{g_u}{g_l}\exp\left(-\frac{h\nu_0}{kT_{\mathrm{ex}}}\right)}$$

and 

$$ \tau_{(1,1)} = \int \alpha_\nu\, ds\, d\nu  =\frac{c^2}{8\pi} \frac{1}{\nu_0^2} \frac{g_u}{g_l} N_{(1,1)} A_{ul} \frac{1-\exp\left(-\frac{h\nu_0}{kT_{\mathrm{ex}}}\right)}{1+\frac{g_u}{g_l}\exp\left(-\frac{h\nu_0}{kT_{\mathrm{ex}}}\right)}.$$

This is neatly linked to the Friesen et al. (2009) formulation above noting that $$g_u = g_l = 1$$.

Note that the Einstein $$A$$ values are given in terms of the dipole moments (c.g.s.) as (Rybicki and Lightman 10.28b):

$$A_{ul} = \frac{64 \pi^4 \nu_0^3}{3 h c^3} \frac{1}{g_u} |\mu_{ul}|^2$$

and Mangum and Shirley (2015), Equation 62 gives 

$$ |\mu_{ul}|^2 = \mu^2 \frac{K^2}{J_u(J_u+1)}$$

and the fiducial dipole moment is $$\mu = 1.468\times 10^{-18}\mathrm{~esu~cm}$$.  We are happily in the $$J=K$$ state, so 

$$ |\mu_{ul}|^2 = \mu^2 \frac{J^2}{J(J+1)}.$$

We can use the exact same formulation for the $$(J,J)$$ line _mutatis mutandis_ and get a column density for each, but the trick is to relate the entire para-NH$$_3$$ column to the column in an individual state.  To get to the optical depths of the other lines, we usually scale from the (1,1) line.  For example:

$$
\begin{eqnarray}
\frac{\tau_{(2,2)}}{\tau_{(1,1)}} &=&\frac{\nu^2_{(1,1)}}{\nu^2_{(2,2)}} \frac{N_{(2,2)}}{N_{(1,1)}} \frac{A_{(2,2)}}{A_{(1,1)}} \frac{f_{22}}{f_{11}},\\
& = & \frac{\nu^2_{(1,1)}}{\nu^2_{(2,2)}} \frac{N_{(2,2)}}{N_{(1,1)}} \frac{2^2}{2\cdot 3} \frac{2}{1}  \frac{f_{22}}{f_{11}}.
\end{eqnarray}
$$

where the numerical factors arise from the Einstein A values and for compactness I use

$$
f_{JJ}\equiv \frac{1-\exp\left(-\frac{h\nu_{(J,J)}}{kT_{\mathrm{ex}}}\right)}{1+\exp\left(-\frac{h\nu_{(J,J)}}{kT_{\mathrm{ex}}}\right)}.
$$

Our fitting usually proceeds under the assumption that the (1,1) and the (2,2) line have the same radiative excitation temperature and that the frequencies are approximately equal (and much less than $$kT_{\mathrm{ex}}/h$$).  In this regime, we set $$f_{22}/f_{11}=1$$.  The former assumption is isn't necessarily the case.  Using RADEX for $$n=10^4~\mathrm{cm}^{-3}$$ and $$T_{K} = 15~\mathrm{K}$$ and $$N(\mathrm{p-NH}_3)=10^{14}~\mathrm{cm^{-2}}$$  gives $$T_{\mathrm{ex},(1,1)} = 8.5~\mathrm{K}$$ and $$T_{\mathrm{ex},(2,2)} = 6.9~\mathrm{K}$$.

Currently, we engage in a deceit.  We assume a two-level system so that we can define $$T_{\mathrm{rot}}$$ such that

$$ N_{(2,2)} = N_{(1,1)} \frac{5}{3} \exp\left(-\frac{\Delta E}{kT_{\mathrm{rot}}}\right)$$

where the 5/3 is the ratio of the rotational statistical weights of the states ($$g_J = 2J+1$$). From here we have that $$T_{\mathrm{rot}}$$ can be related to the kinetic temperature using the work of Swift (the man, the myth, the legend) et al. (2005):

$$
T_{\mathrm{rot}} = T_K \left\{1+\frac{T_{K}}{T_{0}} \ln \left[1+\frac{3}{5} \exp\left(\frac{-15.7~\mathrm{K}}{T_K}\right)\right]\right\}.
$$

Here $$T_0=41.5~\mathrm{K}$$, which is the energy difference between the (2,2) and the (1,1) states. The deceit arises because we calculate all the other level populations based on this rotation temperature.  Then, we use this to infer a (1,1) column density and immediately scale that to a total column via the _kinetic temperature_.  Really, this should be the rotational temperature since that defines the partition of the molecules among the different rotational states.  Unfortunately, the rotational temperature should be different for every pair of rotational metastable states.  This should definitely _not_ be the excitation temperature as that defines the level populations of the individual parts of each inversion transition.  To be self consistent, we should calculate $$N_{(J,J)}$$ as functions of $$T_K, n,\mathrm{~and}~N$$.  The easiest way to do this might be to wrap the RADEX grids, but we might be able to do this using the full coefficients from LAMDA and do the detailed balance solution and an eigenvalue problem.  

Recommendation: we could make the partition function for the para states be calculated from the rotation temperature rather than the kinetic temperature, which would include only small deviations arising from the (4,4) states at 200 K.  