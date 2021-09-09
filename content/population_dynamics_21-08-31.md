---
title: population dynamics
date: 2021-08-31 11:04
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

Many related papers I found use Bayesian inference or varational inference as starting point -> maybe mention these "tags" for families of related works

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
  Feynman-Kac: Wiener-Process with added diffusion term, i.e. particles get "killed" over time\
- Probably a better paper for the algorithm by the same main author is the 2005 one:[^delmoral_2005]\
  The method is to estimate the "rare" parts of some problem, i.e. the parts that can't be easily sampled by plain MC\
  For their cloning they choose particles with high Gibbs measure, i.e. "rare" particles.\
  If I understand it correctly, they always "mutate" all particles, i.e. for every particle they choose one from the total set, with probability according to the Gibbs measure.


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
    There is also one from Hsiao-Ping (https://doi.org/10.1103/PhysRevE.68.021113) that uses a variant of the growth-based algorithm to get polymer conformations. I think this is not really similar to our work but might also be cited as an example of the "go-with-the-winners" strategy.
- "Adaptive Direction Sampling"[^gilks_1993]: MCMC technique with multiple particles, where moves are done along "lines" between the current and another random particle: brings particles closer together (?!) (*only read the abstract and first part*)
- Rotskoff et al (2019)[^rotskoff_2019] applies birth-death to the optimization process of a neural networks. This is mostly a mathy paper with proofs but the actual implementation in sec 5 uses exactly the same idea for the birth-death events than we do.
  So this contains a very similar idea to ours, just that they do not want the samples but just the solution of the PDE, which acts as a gradient descent (didn't fully read how the optimization works, this is just a quick summary).\
  This is only a conference paper, though. Maybe there is a better (newer) paper?
- Paper by Nemoto, Hidalgo and Lecomte (2017)[^nemoto_2017] that might be citeable instead of the PhD thesis:\
  (contains lots of refereces to population dynamics papers)\
  It's based on Giardina (2011)[^giardina_2011] and evaluates the stochastic errors of the method.
  It uses discrete states and assigns a "desired number of copies" to each state by a transition matrix (depending on all states), but the construction makes sure that the total population is kept fixed during the cloning steps.
  What exactly the transition matrix is (i.e. what configurations should be preferred) is left open in the general theory, and not too well explained in the simple example, so I didn't understand it when brushing over.

### new papers
- There is a new paper by Reich & Weissmann[^reich_2021] that somewhat mathy presents some approaches at solving the Fokker-Planck equation with multiple-particle approaches:\
  Doesn't really give algorithms but has a lot of the ideas (e.g. multiple interacting particles for solving the FPE) in it and describes a lot of things more explicitely than Lu, Lu, Nolen, (e.g. how the FPE can be reformulated with the KL divergence between the current and the target distribution).\
  It's too mathy and doesn't offer a clear "algorithm" section (and their practical examples are solving some differential equations), so it's hard to really understand what they are doing/proposing when just quickly brushing over it.\
  *this might be interesting for a closer read. Note: I only read the arXiv version, the other isn't available from the MPIP*
- Lindsey et al (2021)[^lindsey_2021] put a paper on the arXiv where they use birth-death steps together with Markov chain Monte Carlo.
  They only use a somewhat different approach to the "cloning" idea though:\
  1: uniformly select a random particle to clone and do a MCMC step with the new particle\
  2: select another one to delete according to weights depending on how likely it is that the next MCMC step will go to the position of any other particle.\
  Basically: clone random particle, delete particle close to other particles. Note that this is not named a KDE but as they use gaussians for the MCMC probabilities it is pretty similar.\
  They also deal with doing the birth-death only on some subset of the dimensions (sec 4), although they assume that splitting the target distribution is easily possible


### stuff that is not really related
- Papers that do probabilistic annihilation on collision, i.e. particles will either scatter elastically or be annihilated:
  - Hidalgo mentions Visco et al. (2008) [^visco_2008] as example for a constant population implementation on p. xxii, but I must have misunderstood that.\
    Upon collision the two particles are removed from the system with fixed probability p and do collision with 1-p
  - In the previously listed paper they mention Coppex et al. (2004) [^coppex_2004] as major inspiration, but that is also about ballistic annihilation and no cloning
- Mehl, Speck, Seifert (2008) [^mehl_2008]. *has nothing to do with population dynamics, I looked up the wrong citation*, but maybe something similar (but more relevant) might be good to cite in the thesis\
  Theoretical calculation of large deviation function for a single colloidal particle moving with overdamped Langevin dynamics
- Simpson et al. (2013)[^simpson_2013] is about birth-death dynamic models for e.g. biological cell system. It doesn't use multiple "imaginary" particles for sampling, but rather wants to get the time evolution of the particles itself

### ideas to look for
Parallel Tempering / multiple walkers metadynamics


## Footnotes

[^hidalgo_2018]: [E. Guevara Hidalgo, Cloning Algorithms: from Large Deviations to Population Dynamics, PhD thesis, Université Sorbonne Paris, 2018](https://arxiv.org/abs/1806.01943)
[^ellis_2007]: [R. S. Ellis, Entropy, large deviations, and statistical mechanics (Springer, 2007)](https://doi.org/10.1007/3-540-29060-5)
[^mehl_2008]: [J. Mehl, T. Speck, and U. Seifert, Phys. Rev. E 78, 011123 (2008)](https://doi.org/10.1103/PhysRevE.78.011123)
[^visco_2008]: [P. Visco, F. van Wijland, and E. Trizac, Phys. Rev. E 77, 041117 (2008)](https://doi.org/10.1103/PhysRevE.77.041117)
[^coppex_2004]: [Coppex et al., Phys. Rev. E 69, 11303 (2004)](https://doi.org/10.1103/PhysRevE.69.011303)
[^sherman_1986]: [A. Sherman, C. Peskin, SIAM J. Sci. and Stat. Comput. 1986, 7 (4), 1360–1372](https://doi.org/10.1137/0907090)
[^giardina_2011]: [C. Giardinà, J. Kurchan, V. Lecomte, and J. Tailleur, J. Stat. Phys. 145, 787 (2011)](https://doi.org/10.1007/s10955-011-0350-4)
[^anderson_1975]: [J. B. Anderson, The Journal of Chemical Physics 63, 1499 (1975)](https://doi.org/10.1063/1.431514)
[^aldous_1994]: [D. Aldous and U. Vazirani, in Foundations of Computer Science, 35th (IEEE, 1994), pp. 492–501.](https://doi.org/10.1109/SFCS.1994.365742)
[^grassberger_2002]: [P. Grassberger, Comp Phys Comm 147 (2002) 64–70](https://doi.org/10.1016/S0010-4655\(02\)00205-9)

[^delmoral_2006]: [P. Del Moral, A. Doucet, and A. Jasra: J. R. Stat. Soc., Ser. B, Stat. Methodol. 68, 411–436 (2006)](https://doi.org/10.1111%2Fj.1467-9868.2006.00553.x)

[^delmoral_2005]: [P. Del Moral and J. Garnier, Ann. Appl. Probab. 15, 2496 (2005)](https://doi.org/10.1214/105051605000000566)
[^liu_2016]: [Q. Liu, and D. Wang, Stein variational gradient descent: A general purpose Bayesian inference algorithm. In Advances In Neural Information Processing Systems, pp. 2378–2386, 2016.](https://dl.acm.org/doi/10.5555/3294996.3295071)
[^reich_2021]: [S. Reich, S. Weissmann: SIAM/ASA J. Uncertainty Quantification, 9(2), 446–482 (2021)](https://doi.org/10.1137/19M1303162) [arXiv](https://arxiv.org/abs/1911.10832)
[^lindsey_2021]: [M. Lindsey, J. Weare, and A. Zhang, “Ensemble Markov chain Monte Carlo with teleporting walkers,” arXiv:2106.02686](http://arxiv.org/abs/2106.02686)
[^gilks_1993]: [W. R. Gilks, G. O. Roberts, and E. I. George, “Adaptive Direction Sampling,” The Statistician, vol. 43, no. 1, p. 179, 1994](https://doi.org/10.2307/2348942)

[^simpson_2013]: [M. J. Simpson, J. A. Sharp, and R. E. Baker, Physica A: Statistical Mechanics and its Applications, vol. 395, pp. 236–246, (2014)](https://doi.org/10.1016/j.physa.2013.10.026)
[^rotskoff_2019]: [G. Rotskoff, S. Jelassi, J. Bruna, and E. Vanden-Eijnden, “Global convergence of neuron birth-death dynamics,” presented at the 36th International Conference on Machine Learning (ICML 2019), 2019.](http://statmech.stanford.edu/publication/rotskoff-global-2019-1/)
[^nemoto_2017]: [T. Nemoto, E. G. Hidalgo, and V. Lecomte, Physical Review E, vol. 95, no. 1, p. 012102 (2017)](https://doi.org/10.1103/physreve.95.012102)
