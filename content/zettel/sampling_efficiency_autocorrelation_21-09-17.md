---
title: Sampling efficiency / autocorrelation
date: 2021-09-17 11:17
draft: false
tags: ["Monte Carlo", "Langevin Dynamics", "sampling", "error metric", "autocorrelation"]
---

How do we estimate "good" sampling? Typically I have assessed not the sampling directly but only some estimates from the sampling (for example the free energy surface or some observable) via error metrics such as an RMSD or the Kullback-Leibler divergence.

Some papers have used the "effective sample size" to measure the quality of sampling (see e.g. [^invernizzi_unified_2020]).

For MC simulations some papers [^skeel_choice_2021],[^fang_quasi_2020] talk about how the "effective sample size" is not a good metric (see beginning of Sec 3 of Fang (2020)[^fang_quasi_2020]) but rather the "Integrated autocorrelation time"



## Footnotes
[^invernizzi_unified_2020]: [M. Invernizzi, P. M. Piaggi, and M. Parrinello, “Unified approach to enhanced sampling,” Phys. Rev. X, vol. 10, no. 4, Nov. 2020](https://doi.org/10.1103/PhysRevX.10.041034)
[^skeel_choice_2021]: [R. D. Skeel and C. Hartmann, “Choice of damping coefficient in Langevin dynamics,” Eur. Phys. J. B, vol. 94, no. 9, p. 178, Sep. 2021](https://doi.org/10.1140/epjb/s10051-021-00182-z)
[^fang_quasi_2020]: [Y. Fang, Y. Cao, and R. D. Skeel, “Quasi-reliable estimates of effective sample size,” IMA Journal of Numerical Analysis, p. draa077, Oct. 2020](https://doi.org/10.1093/imanum/draa077)
