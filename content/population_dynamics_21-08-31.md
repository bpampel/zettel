---
title: population dynamics
date: 2021-08-31 11:04
tags: ["birth-death", "population dynamics"]
draft: false
---


## Some terms/definitions from PhD Thesis by Esteban Guevara Hidalgo

- Algorithms that do population control in a rare event setting are called **cloning algorithms**.
- Two variants: **non-constant** and **constant total population**: In his opinion the first is advantageous:
  - uniform **pruning**/**cloning** induces correlations into the dynamics
  - when populations are very fluctuating, finite-population effects cause problems (risk of population being wiped out by single clone)

### Large deviations
> The mathematical theory of large deviations is concerned with the exponential decay of the probability of extreme events while the number of observations grows.[^mehl_2008]

Generally, the Ellis book[^ellis_2007] seems to be the main entry point for the theory of large deviations



## collection of papers from different sources


### from Lu, Lu & Nolen
The Lu, Lu & Nolen paper doesn't seem to have much good literature:
 - 3 papers on Stein variational gradient descent (SVGD)

### from Hidalgo's PhD thesis
- Giardinà et al (2011) [^giardina_2011]. Sample "rare" trajectories via population dynamics\
  Use (infinitely many) clones with the same dynamics but uncorrelated noise.\
  (nb: the dynamics looks strange on first sight, v = f + noise, so not quite overdamped langevin as in our case. Eq. 3.2 looks nevertheless very similar to the Fokker-Planck operator that we have)\
  "Change of basis" to modify the importance of the drift and diffusion term (or simply a different cloning rate) -> "dynamic importance sampling"
  After some time delta t, each clone is either duplicated or killed such it is on average replaced by exp(alpha A delta t) clones

#### stuff that is not really related
- Papers that do probabilistic annihilation on collision, i.e. particles will either scatter elastically or be annihilated:
  - Hidalgo mentions Visco et al. (2008) [^visco_2008] as example for a constant population implementation on p. xxii, but I must have misunderstood that.\
    Upon collision the two particles are removed from the system with fixed probability p and do collision with 1-p
  - In the previously listed paper they mention Coppex et al. (2004) [^coppex_2004] as major inspiration, but that is also about ballistic annihilation and no cloning
- Mehl, Speck, Seifert (2008) [^mehl_2008]. *has nothing to do with population dynamics, I looked up the wrong citation*, but maybe something similar (but more relevant) might be good to cite in the thesis\
  Theoretical calculation of large deviation function for a single colloidal particle moving with overdamped Langevin dynamics



### misc
- Sherman & Peskin (1986) [^sherman_1986] paper that does things surprisingly close to what we do: "create and destroy" some "elements" with certain probability (depending on the time step) at every time step and do a random walk in between. Does not keep the total population constant! (from Burkhard)

Parallel Tempering / multiple walkers metadynamics


## Footnotes

[^ellis_2007]: [R. S. Ellis, Entropy, large deviations, and statistical mechanics (Springer, 2007)](https://doi.org/10.1007/3-540-29060-5)
[^mehl_2008]: [J. Mehl, T. Speck, and U. Seifert, Phys. Rev. E 78, 011123 (2008)](https://doi.org/10.1103/PhysRevE.78.011123)
[^visco_2008]: [P. Visco, F. van Wijland, and E. Trizac, Phys. Rev. E 77, 041117 (2008)](https://doi.org/10.1103/PhysRevE.77.041117)
[^coppex_2004]: [Coppex et al., Phys. Rev. E 69, 11303 (2004)](https://doi.org/10.1103/PhysRevE.69.011303)
[^sherman_1986]: [A. Sherman, C. Peskin, SIAM J. Sci. and Stat. Comput. 1986, 7 (4), 1360–1372](https://doi.org/10.1137/0907090)
[^giardina_2011]: [C. Giardinà, J. Kurchan, V. Lecomte, and J. Tailleur, J. Stat. Phys. 145, 787 (2011)](https://link.springer.com/article/10.1007%2Fs10955-011-0350-4)
