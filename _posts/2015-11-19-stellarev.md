---
layout: post
title: Stellar Evolution Primer
---

In teaching stellar evolution for third year students, there are a few things that link tightly to the physics covered earlier in the class, and are worth highlighting.

## Important Physics Reminder

The entire process of stellar evolution is playing out in self-gravitating spherical systems with mass $$M$$ and radius $$R$$, where there is a relationship between the gravitational self-energy of the system and the thermal energy in the gas.  Since these two energies are related through the virial theorem, we can note that 

$$
\begin{eqnarray}
U_g &=& -2 E_T\\
-\beta \frac{GM^2}{R} &=& -2 \frac{3}{2} \frac{M}{\mu m_{\mathrm{H}}} k T\\
T & = & \frac{3 \beta G M \mu m_{\mathrm{H}}}{k R}
\end{eqnarray}
$$

where we have used a general form for the gravitational self energy and the constant $$\beta$$ is a constant of order unity that depends on the density distribution of the object.  A uniform density sphere has $$\beta=3/5$$.  We have also expressed the number of particles in the system in terms of the mean particle mass $$\mu m_{\mathrm{H}}$$.

Note that the temperature is inversely proportional to the radius, so that as an object gets smaller, it will also get hotter.  Recall also that, in the absence of any source of support, the system will collapse.  The virial theorem gives that half of the gravitational energy will go into heating up the gas (as per above) and the other half is radiated away.  Since objects radiate energies at a rate given by their luminosities $$L$$, the time it takes for an object to contract substantially is set by the Kelvin-Helmholtz timescales $$\tau_{\mathrm{KH}}$$.

In general, as a stellar core contracts and heats up, one of two things will happen.  

1. The star will reach the threshold temperatures and densities require to ignite a higher stage of nuclear fusion.  For example, the temperatures could reach the $$T=10^8~\mathrm{K}$$ temperatures needed to start the fusion of He into C under the $$3\alpha$$ process.  

2.  Alternatively, the core could become supported by electron degeneracy pressure.  This source of pressure will provided the necessary support to keep the star in a hydrostatic equilibrium without nuclear fusion and the collapse will halt.  Note that the equation of state for (non-relativistic) degeneracy pressure is 

$$
P = K_1 \rho^{5/3}
$$

where $$K_1=3\times 10^{6}~\mathrm{Pa}$$ for $$\rho$$ in SI units.  Of note there is no temperature dependence on the equation of state.  This becomes important if the temperature of the gas becomes high enough to ignite fusion inside a degenerate gas.  Also of note, the mass-radius relationship for objects supported by degeneracy pressure has a negative index.  The pressure required to support an object of mass $$M$$ and radius $$R$$ is $$P \propto G M^2/R^4$$.  If this pressure is provided by electron degeneracy pressure, as above, where $$P\propto \rho^{5/3} \propto M^{5/3} / R^5, then

$$
\begin{eqnarray}
G M^2/R^4 & \propto & M^{5/3} / R^5,\\
R \propto M^{-1/3}/G.
\end{eqnarray}
$$

This result means that higher mass objects have smaller radii.  


## Evolution on the Main Sequence 

Stars on the main sequence are, by definition, fusing (1) hydrogen into helium (2) in their cores.  Low mass stars are fusing primarily through the _pp_ chain and medium and high mass stars are fusing primarily through the CNO cycle.  Either way, the net effect of this fusion is to change the chemical composition in the core of the star from H into He.  Or, in terms of mass fractions, $$X$$ decreases toward 0, $$Y$$ increases toward $$1-Z$$.  This means that the mean particle mass is increasing:

$$\mu^{-1} = 2X + \frac{3}{4}Y + \frac{1}{2}Z$$.

Each  fusion chain reaction replaces four protons in the core with only one helium nucleus.  Since the gas pressure in a star is

$$ P = \frac{\rho k T}{\mu m_{\mathrm{H}}}$$,

the amount of pressure provided by a gas at density $$\rho$$ and temperature $$T$$ will decrease.  This means that the density and temperature of the core must increase to provide the pressure to support the star, increasing the nuclear energy generation rate and thus the luminosity.  Thus, stars on the main sequence are getting more luminous over their lifetimes.  The Sun formed with $$L=0.7 L_{\odot}$$ and will increase to about $$L=1.4 L_{\odot}$$ before it evolves off the main sequence.

## Low mass Stellar Evolution

Here we mean stars with masses $$ 0.8 M_{\odot} < M < 2 M_{\odot}$$.  We base our discussion of stellar evolution on these stars, and then describe the changes with mass in terms of this basic evolutionary scheme.  

These stars have radiative cores and radiative-plus-convective envelopes.  For our purposes, the _core_ means the part of the star that is undergoing nuclear fusion and the _envelope_ is the inert outer layers that are not participating in the fusion process.  The radiative nature of the stellar cores means that the material is static and a given parcel of gas remains at the same radius in the star.  Since the temperature and density profiles in a star are highest in the centre $$(r=0)$$ and decreasing with radius, this means that the nuclear energy generation rate $$(\epsilon \propto \rho T_6^4)$$ will be strongly centrally peaked and it will remain so over the life of the star.  In terms of energy generation, this means that matter at the centre of the star is will fuse its hydrogen into helium at a faster rate, depleting the hydrogen content and arriving at a depleted state first $$(X=0,Y=0.98,Z=0.02)$$.  In this gas, fusion will shut off, but the gas will be hot and surrounded by a region of the core that is still fusing hydrogen.  This gas will also be isothermal since it is not producing any fusion within it.  Instead it will be held at a constant temperature set by the energy generating region around it.  

As the star continues to fuse, this inert, isothermal core will get larger and the fusing region move to progressively larger radii.  In this time, it transitions from being a core-burning star into a shell-burning fusion source.  There is a maximum mass for the isothermal helium core before it collapses under its own self-gravity.  This is called the Schönberg-Chandrasekhar limit and is about 10% of the star's mass.  At this point, the isothermal core contracts and heats up on the Kelvin-Helmholtz timescale.  





## Medium mass Stellar Evolution

For stars with masses $$ 2 M_{\odot} < M < 8 M_{\odot}$$, their evolution is similar to low mass stars, with the exception that there isn't the formation of a degenerate electron core and a proper red giant phase.  