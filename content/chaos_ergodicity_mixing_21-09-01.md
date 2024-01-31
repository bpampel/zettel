---
title: Chaos, ergodicity, and mixing
date: 2021-09-01 10:45
draft: false
---

## Ergodicity and mixing

In Coveney & Wan (2016) [^coveney_2016] there is some descriptive explanation of some of the terms related to **ergodicity** and **mixing**.

**Ergodicity** is colloquially defined as: "given infinite time, the system passes through all points of the phase space"
For a more mathematical definition, see e.g. [Birkhoff ergodic theorem](https://encyclopediaofmath.org/wiki/Birkhoff_ergodic_theorem)

A **mixing** system is there defined as one where there is a sensitivity to initial conditions, i.e. the late behavior of the system is totally uncorrelated with its early time properties.
In mathematic terms the system has at least one positiv definite Lyapunov exponent.
It says that colloquially this is the same as a "chaotic" system.
I'm not fully sure about their definitions.
Elsewhere I read that the positive definite Lyapunov exponent comes from the chaotic property: the distance between two trajectories has to strictly increase over time

A mixing system is ergodic and additionally has an approach to equilibrium.

I.e. just ergodicity alone does not mean that the system will really go to an equilibrium state, which is important for statistical estimates.

---

## Gallavotti-Cohen theorem

More mathy theory related to this, I found it through a reference for "small noise limit".
I think it is mostly relevant when employing thermostats for forced dynamics in the microcanonical ensemble (and deterministic systems), so it's here only for future reference, without any guarantees for correctness.


Gallavotti-Cohen theorem (*Chaotic hypothesis*):
> A reversible many-particle system in a stationary state can be regarded as a transitive Anosov system for the purpose of computing the macroscopic properties of the system. [^gallavotti_1995]

I didn't fully follow the math to understand *what exactly* Anosov systems are, but I think besides the positiv Lyapunov exponent it also requires "hyperbolic dynamics" (I think this means a special case of "forced" and deterministic), time-reversibility and more, i.e. it is for very specific systems. (might have gotten this totally wrong but it's a lot of math)


Based on this Kurchan (2007)[^kurchan_2007] presented some requirements for when a system has this chaotic property in a steady state. Here is how he describes the Gallavotti-Cohen theorem
> For a purely deterministic case, a forced system converges to an ‘attractor’ set, while the time-reversed dynamics converges to a ‘repellor’ set.
> Loosely speaking, the Gallavotti– Cohen theorem is then based on two types of hypotheses:
> (i) that the attractor is sufficiently chaotic, and (ii) that the attractor and repellor are interwoven fractals with sufficiently overlapping closures. As the forcing is increased, attractor and repellor tend to separate, and even if the attractor remains chaotic the Fluctuation Relation no longer holds in general.
> For macroscopic systems at reasonable levels of forcing, one can assume that the hypotheses  above are effectively (if not always strictly) satisfied, leading to the Chaotic Hypothesis.


The paper gives citations where the Fluctuation relation trivially holds in many cases, and proves that it actually holds in most macroscopic cases. From the introduction:\
It trivially holds for (i) systems starting from an equilibrium configuration (ii) systems in contact with a thermal
bath involving stochastic noise that guarantees ergodicity.
For deterministic thermostats this is not as clear, although the paper only talks about thermostats that are energy-conserving noise.

It discusses weak-noise and small-noise limits and shows that in the "small noise limit" the Gallavotti-Cohen theorem is always satisfied

In Giardinà (2011) [^giardina_2011], there is also some discussion about the theorem and it's implications.



## Footnotes

[^coveney_2016]: [P. Coveney, S. Wan, Phys. Chem. Chem. Phys., 2016, 18, 30236-30240](https://doi.org/10.1039/C6CP02349E)
[^gallavotti_1995]: [Gallavotti, G., Cohen, E.G.D. Dynamical ensembles in stationary states. J Stat Phys 80, 931–970 (1995)](https://doi.org/10.1007/BF02179860)
[^kurchan_2007]: [J. Kurchan, Gallavotti–Cohen Theorem, Chaotic Hypothesis and the Zero-Noise Limit. J Stat Phys 128, 1307–1320 (2007)](https://doi.org/10.1007/s10955-007-9368-z)
[^giardina_2011]: [C. Giardinà, J. Kurchan, V. Lecomte, and J. Tailleur, J. Stat. Phys. 145, 787 (2011)](https://link.springer.com/article/10.1007%2Fs10955-011-0350-4)
