---
title: Wavelets
date: 2019-03-15 10:31
draft: false
tags: ["wavelets", "basisfunction", "basis"]
math: true
---

# Mixed thoughts on Wavelets

- Daubechies wavelets: Family of orthogonal wavelets with smallest support for a given "number of vanishing moments" --> good representation properties for piecewise polynomials
- Symlets are the "least asymmetric" variant: Slightly less regular but the filter with a near-linear phase results in more symmetric wavelets


### Quick lookup of some math terms:
#### Spaces / Bases
- Riesz basis: generalization of orthonormal bases (all orthonormal bases are Riesz bases)
- $l^p$ space: space of all sequences satisfying $\sum_n \vert x_n \vert_p < \infty$  
    -> Sum of norms is finite.  
    example: $l^2$ is all square summable sequences
- $L^p$ space: same with functions, e.g. $L^2$ is space of all square integrateable functions (= finite energy), called "Lebesgue space"
- Sobolev space $W^k_p$: Subset of functions $f \in L^p$ whose weak derivatives up to order $k$ have finite $L^p$ norm  
    Important special case: $p=2$: Forms Hilbert space, short notation often $W^k_2 = H^k$
- Schauder basis: countable basis (can have infinite sum to represent element instead of finite in ordinary Hamel basis)


#### Misc
- Monoic polynomial: polynomial with leading coefficient (highest order) equal to 1
- Hyperbolic wavelet basis: linear approximation via "sparse grid-type bases"
- Smoothness: $C^n$ means function has $n$ continous derivatives
- Parseval's theorem: analogue of Pythagoras' theorem for functions and proofs completeness (see notebook)


#### Splines
- $C^n$ is continuity:
  - $C^1$: continuity of the tangent vector: "continuous derivative"
  - $C^2$: continuity of the slope
- Knots: how many points "coalesce"
  - simple knot: knot with $C^n-1$ continuity
  - double knot: knot with $C^n-2$ continuity
