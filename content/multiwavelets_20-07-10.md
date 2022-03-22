---
title: Multiwavelets
date: 2020-07-10 22:36
draft: false
tags: ["Wavelets", "interpolating polynomial"]
---

Scaling function and wavelet functions are now vectors -> Coefficients become matrix (2d) instead of list

Paper "Adaptive Solution of Partial Differential Equations in Multiwavelet Bases"[^alpert_adaptive_2002]:
  - Constructed on bounded interval (here [0,1])
  - Proposes an interpolating basis (-> Coefficients are values) with *Lagrange interpolating polynomials*
  - Results in basis functions $R_j(x) = \frac{1}{\sqrt{w_j} l_j(x)$ with $l_j$ being the Lagrange polynomials
  - Opposite way: Scaling and wavelet functions are known, need to construct the coefficients _(not in our case?)_
  - -> Explicit expression for scaling function! (although a bit complicated)
  - Not sure about the exact properties, seem to be few coefficients on coarsest level
  - Explicit section about (first) derivative -> is not unique for discontinuous functions?

Interesting family suggested by Markus Bachmayr: Multiwavelets developed by Donovan, Geronimo, Hardin


[^alpert_adaptive_2002]: [B. Alpert, et al., J. Comp. Phys., 182(1), 2002](https://doi.org/10.1006/jcph.2002.7160)
