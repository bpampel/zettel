---
title: population dynamics
date: 2021-08-31 11:04
tags: ["birth-death", "population dynamics"]
draft: false
---


## Some terms/definitions

PhD Thesis by Hidalgo:[^hidalgo_2018]
- Algorithms that do population control in a rare event setting are also referred to as **cloning algorithms**.
- Two variants: **non-constant** and **constant total population**: In his opinion the first is advantageous:
  - uniform **pruning**/**cloning** induces correlations into the dynamics
  - when populations are very fluctuating, finite-population effects cause problems (risk of population being wiped out by single clone)

selection of alternative terms for the "birth/death" events:
- kill / replicate
- create / destroy
- kill / duplicate

alternative terms for the "particles":
- clones
- walkers (have actually not yet read this in a paper in the context of population dynamics)

Many related papers I found apply their method to Bayesian inference problems

### Large deviations
many papers with population dynamics mention large deviations
> The mathematical theory of large deviations is concerned with the exponential decay of the probability of extreme events while the number of observations grows.[^mehl_2008]

Generally, the Ellis book[^ellis_2007] seems to be the main entry point for the theory of large deviations



## collection of papers from different sources


### from Lu, Lu & Nolen
The Lu, Lu & Nolen paper doesn't seem to have many citations of "related work"
- 3 papers on Stein variational gradient descent (SVGD) by roughly the same people\
  In Liu (2016) [^liu_2016] an algorithm called "Bayesian Inference via Variational Gradient Descent" is proposed.\
  It uses a set of particles whose movements depend on the positions of all particles.\
  The idea is to minimize the KL divergence from the current to a target distribution while preventing that all particles collapse together\
  The two terms of the interaction can be interpreted as\
  1: drive the particles towards the high probability regions of the target distribution p(x)\
  2: act as repulsive force between the particles via the gradient of a kernel\
  The first term alone would result in typical gradient ascent for maximizing log p(x)\
  The second term has a similar idea than our KDE term, it also vanishes for the bandwidth -> 0\
  To summarize: *movement of interacting particles, idea of KL divergence between "current" and "target" distribution, usage of a kernel to drive particles away from each other. No birth-death*
- also mentioned in [^giardina_2011]: Del Moral et al (2006)[^delmoral_2006] use "clouds of weighted random samples" to sample *sequentially* from different probability distributions.\
  Applications are e.g. if the distributions are updated after more information (data) becomes available: "Alternatively, we may want to move from a tractable (easy-to-sample) distribution pi_1 to a distribution of interest, pi_n, through a sequence of artificial intermediate distributions"\
  proposes a Sequential Monte Carlo Sampling (SMC) method, that moves from the current "particle" positions obtained from sampling pi_{n-1} to the next distribution by applying a Markov kernel.\
  Only brushed through the paper but it seems to me that this is not doing population dynamics but just "moves" particles around when switching the "target" distribution. There is a sentence saying that the "algorithms can be interpreted as interacting particle approximations of a Feynman-Kac flow in distribution space", but not sure about the exact algorithm and the particle interpretation (generally a very "mathy" paper, so hard to understand what they are exactly doing).\
  Feynman-Kac: Wiener-Process with added diffusion term, i.e. particles get "killed" over time


### from Hidalgo's PhD thesis
- Giardinà et al (2011) [^giardina_2011]. Sample "rare" trajectories via population dynamics\
  Use (infinitely many) clones with the same dynamics but uncorrelated noise.\
  (nb: the dynamics looks strange on first sight, v = f + noise, so not quite overdamped langevin as in our case. Eq. 3.2 looks nevertheless very similar to the Fokker-Planck operator that we have)\
  "Change of basis" to modify the importance of the drift and diffusion term (or simply a different cloning rate) -> "dynamic importance sampling"\
  At each time interval delta t, each clone is either killed or replicated such it is on average replaced by exp(alpha A delta t) clones -> not just one but several clones are possible (alpha is "bias factor", "A" is some desired quantity). Enforcement of constant number by duplicating or killing random clones *after* the birth-death step in the algorithm.\
  Application to Monte Carlo problems (discrete space), but also to one example with Hamilton dynamics where they call the algorithm "Lyapunov weighted dynamics": can force more "chaotic" or "integrateable" trajectories



### misc
- Sherman & Peskin (1986) [^sherman_1986] paper that does things surprisingly close to what we do: "create and destroy" some "elements" with certain probability (depending on the time step) at every time step and do a random walk in between. Does not keep the total population constant! (from Burkhard)
- Anderson (1975) [^anderson_1975], presents an early method of solving a quantum mechanical diffusion problem by the simulation of "random movement of imaginary particles […] subject to a variable chance of multiplicating or disappearance"\
  Interesting to read, already has the idea of running multiple particles with some random displacement and killing/duplicating them. Modifies the probabilities after each step to keep the total number of particles approximately fixed.
- "Go with the winner" papers:
  - Aldous & Vazirani (1994) [^aldous_1994] review "Go with the winners" schemes, similar to genetic schemes but without mating\
    This is mostly for tree-based schemes. The two presented algorithms either redistribute the "bad" particles to the "good" branches or kill all bad particles and create a "random" number of clones at the good particle positions\
    Also has a short excurse to combine it with simulated annealing
    In essence, while this has some cloning it's not that much related to our work.
  - Grassberger (2002) [^grassberger_2002] uses population control for Monte Carlo simulations of polymer systems\
    Starting with sequential importance sampling: Duplicate configurations with MC weights above some threshold and assign half weight. Kill population below some threshold with 0.5 probability, if it survives double the weight.\
    (Maybe read also one with Hsiao-Ping (https://doi.org/10.1103/PhysRevE.68.021113) )


### new papers
- There is a new paper by Reich & Weissmann[^reich_2021] that somewhat mathy presents some approaches at solving the Fokker-Planck equation with multiple-particle approaches:\
  Doesn't really give algorithms but has a lot of the ideas (e.g. multiple interacting particles for solving the FPE) in it and describes a lot of things more explicitely than Lu, Lu, Nolen, (e.g. how the FPE can be reformulated with the KL divergence between the current and the target distribution).\
  It's too mathy and doesn't offer a clear "algorithm" section (and their practical examples are solving some differential equations), so it's hard to really understand what they are doing/proposing when just quickly brushing over it.\
  *this might be interesting for a closer read.*
- Lindsey et al (2021)[^lindsey_2021] put a paper on the arXiv where they use birth-death steps together with Markov chain Monte Carlo.
  They only use a somewhat different approach to the "cloning" idea though:\
  1: uniformly select a random particle to clone and do a MCMC step with the new particle
  2: select another one to delete according to weights depending on how likely it is that the next MCMC step will go to the position of any other particle.
  Basically: clone random particle, delete particle close to other particles. Note that this does not require a KDE but just the MCMC probabilities.


### stuff that is not really related
- Papers that do probabilistic annihilation on collision, i.e. particles will either scatter elastically or be annihilated:
  - Hidalgo mentions Visco et al. (2008) [^visco_2008] as example for a constant population implementation on p. xxii, but I must have misunderstood that.\
    Upon collision the two particles are removed from the system with fixed probability p and do collision with 1-p
  - In the previously listed paper they mention Coppex et al. (2004) [^coppex_2004] as major inspiration, but that is also about ballistic annihilation and no cloning
- Mehl, Speck, Seifert (2008) [^mehl_2008]. *has nothing to do with population dynamics, I looked up the wrong citation*, but maybe something similar (but more relevant) might be good to cite in the thesis\
  Theoretical calculation of large deviation function for a single colloidal particle moving with overdamped Langevin dynamics
Parallel Tempering / multiple walkers metadynamics


## Footnotes

[^hidalgo_2018]: [E. Guevara Hidalgo, Cloning Algorithms: from Large Deviations to Population Dynamics, PhD thesis, Université Sorbonne Paris, 2018](https://arxiv.org/abs/1806.01943)
[^ellis_2007]: [R. S. Ellis, Entropy, large deviations, and statistical mechanics (Springer, 2007)](https://doi.org/10.1007/3-540-29060-5)
[^mehl_2008]: [J. Mehl, T. Speck, and U. Seifert, Phys. Rev. E 78, 011123 (2008)](https://doi.org/10.1103/PhysRevE.78.011123)
[^visco_2008]: [P. Visco, F. van Wijland, and E. Trizac, Phys. Rev. E 77, 041117 (2008)](https://doi.org/10.1103/PhysRevE.77.041117)
[^coppex_2004]: [Coppex et al., Phys. Rev. E 69, 11303 (2004)](https://doi.org/10.1103/PhysRevE.69.011303)
[^sherman_1986]: [A. Sherman, C. Peskin, SIAM J. Sci. and Stat. Comput. 1986, 7 (4), 1360–1372](https://doi.org/10.1137/0907090)
[^giardina_2011]: [C. Giardinà, J. Kurchan, V. Lecomte, and J. Tailleur, J. Stat. Phys. 145, 787 (2011)](https://link.springer.com/article/10.1007%2Fs10955-011-0350-4)
[^anderson_1975]: [J. B. Anderson, The Journal of Chemical Physics 63, 1499 (1975)](https://doi.org/10.1063/1.431514)
[^aldous_1994]: [D. Aldous and U. Vazirani, in Foundations of Computer Science, 35th (IEEE, 1994), pp. 492–501.](https://doi.org/10.1109/SFCS.1994.365742)
[^grassberger_2002]: [P. Grassberger, Comp Phys Comm 147 (2002) 64–70](https://doi.org/10.1109/SFCS.1994.365742)

[^delmoral_2006]: [Del Moral, P., Doucet, A., Jasra, A.: J. R. Stat. Soc., Ser. B, Stat. Methodol. 68, 411–436 (2006)](https://doi.org/10.1111%2Fj.1467-9868.2006.00553.x)
[^liu_2016]: [Liu & Wang (2016) Liu, Q. and Wang, D. Stein variational gradient descent: A general purpose Bayesian inference algorithm. In Advances In Neural Information Processing Systems, pp. 2378–2386, 2016.](https://dl.acm.org/doi/10.5555/3294996.3295071)
[^reich_2021]: [S. Reich, S. Weissmann: SIAM/ASA J. Uncertainty Quantification, 9(2), 446–482 (2021)](https://doi.org/10.1137/19M1303162) [arXiv](https://arxiv.org/abs/1911.10832)
[^lindsey_2021]: [M. Lindsey, J. Weare, and A. Zhang, “Ensemble Markov chain Monte Carlo with teleporting walkers,” arXiv:2106.02686](http://arxiv.org/abs/2106.02686)
