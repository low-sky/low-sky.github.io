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
Note that we've used the idea that magnitude vector $$p = (p_x^2 + p_y^2 + p_z^2)^{1/2}$$, and then the similarity of the problem to kinematics to build up the idea of a momentum "volume."  The value $$p_{\mathrm{max}}$$ is just a radius of a sphere in momentum space and the volume of that sphere is $$ 4\pi p_{\mathrm{max}} / 3$$.  The minimum possible value for $$p_{\mathrm{max}}$$ occurs when this phase volume equals the minimum possible value, which is
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

To turn this into an equation of state for the degeneracy pressure, we have to understand how momentum is related to pressure.  This is a standard derivation in many statistical mechanics or modern physics texts, which is summarized here.  Pressure is the force per unit area.  We can compute the pressure in a gas by analyzing the force that gas exerts on a perfectly elastic barrier of area $$A$$.  Consider a beam of particles with (vector) momentum $$\mathbf{p}$$ travelling toward a barrier along a trajectory that makes an angle $$\theta$$ with respect to the normal.  We define the normal to be in the $$\hat{z}$$ direction.  If one of the particles strikes the barrier and rebounds off, it must have an impulse of magnitude $$ 2 \Delta p \cos \theta  = -2 p \cos \theta$$ exerted on it.  If the particles strike the wall with an time $$\Delta t$$ between collisions, the average force that the wall exerts on the particles must be equal to this momentum: $$ F \Delta t = -2 p \cos \theta $$.  

We can then express the typical time interval between collisions with the wall in terms of how fast the particles are travelling and the distance between particles in the $$z$$-direction ($$\Delta z$$):  $$\Delta t = 2 \Delta z / (v \cos \theta)$$.  Thus, the  force from this beam of particles is $$ F = 2 p v \cos^2 \theta /\Delta z$$.  We can then express this in terms of a force per unit area (or a pressure) as 
$$
\begin{eqnarray*}
P & = & \frac{F}{A} \\
& = & \frac{2 p v \cos^2 \theta}{A\Delta z}\\
& = & \frac{2 p v \cos^2 \theta}{V},
\end{eqnarray*}
$$

where $$V$$ is a volume with a single particle of the beam in it.  We can then identify $$1/V$$ as the volume density $$N$$ so $$P = 2 N p_v \cos^2 \theta$$.  

Now, gases of particles aren't perfect beams with a set of particles all having the same momentum.  Particles also strike the barrier from all different directions.  To account for these two effects, we need to extend this simple idea a bit.  Dealing with the direction component first, we need to consider the average value that $$\cos^2 \theta$$ term takes when looking over all possible angles that can hit the wall.  The formal version is to consider spherical-polar coordinates, and average over the portion of the sphere that is pointing toward the barrier, i.e., for $$0 \le \theta < \pi/2$$.  Then, this average [gives](http://www.wolframalpha.com/input/?i=Integrate%28cos%28x%29^2+sin%28x%29%2Cx%3D0..pi%2F2%29%2FIntegrate%28sin%28x%29%2Cx%3D0..pi%2F2%29)

$$
\begin{eqnarray*}
\langle \cos^2 \theta \rangle & = & \frac{\int_{0}^{2\pi} d \phi \int_0^{\pi/2} \cos^2 \theta \sin \theta d\theta }{\int_{0}^{2\pi} d \phi \int_0^{\pi/2}  \sin \theta d\theta}\\
& = & \frac{1}{3}.
\end{eqnarray*}
$$

Informally, the same result can be argued that $$p v \cos^2 \theta = p_x v_x $$. 