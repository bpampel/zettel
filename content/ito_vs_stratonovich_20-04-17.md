---
title: Itô vs Stratonovich
date: 2020-04-17 16:24
draft: false
---

## Itô and Stratonovich interpretation of stochastic integrals

This follows mostly chapter 3.2 of Pavlotis.

For a stochastic integral of the form

    I(t) = \int_0^t f(s) dW(s)

where we are interested in integrating some process `f(t)` up to some intermediate time `t ∈ in [0, T]` that depends only on the past of the Brownian motion `W(t)`.

We do a Riemann sum approximation of the integral:

The time is partitioned into small intervals of size `δt`, i.e.

    t_k = k * δt  for k=0,…,K-1

and we define with the parameter `λ ∈ [0,1]`

    \tau_k = (1 - \lambda) t_k + \lambda t_{k+1}

the stochastic integral as the `L^2` limit of the Riemann sum approximation

    I(t) := lim_{K \rightarrow \infty} \sum_k f(\tau_k) ( W(t_{k+1}) - W(t_k) )

The result depends on the choice of `\lambda`: Where do we evaluate `f(t)` for the "rectangles"? (Compare with the midpoint for a standard Riemann integral)

The most common choices are

- `\lambda = 0` (Itô): evaluate at left endpoint (advantage: no correlation to the current increment)
- `\lambda = 1/2` (Stratonovich): evaluate at the midpoint (advantage: standard chain rule)

Choice depends on interpretation, seldomly others than these two are used.
