---
title: bayesian interference
date: 2021-08-31 11:04
draft: true
---

Some introductory notes about Bayesian statistics / interference.

Start out with the basics:

- The probability of observing some event $A$ is given by $p(A)$.
- The conditional probability of observing $A$ given that $B$ holds is denoted by $p(A|B)$

Then Bayes' theorem is given by

  $$ p(B|A) = \frac{ p(A|B) p(B) } { p(A) } $$

Here the terms typically have the following names:
- $p(B|A)$: posterior probability
- $p(A|B)$: likelihood
- $p(A)$: prior probability
- $p(B)$: evidence

We'll now turn this into the typical description for machine learning:

- The probability of observing a specific dataset $\mathbf{X}$ given the (unknown) parameters $\mathbf{w}$ is denoted by $p(\mathbf{X}|\mathbf{w})$.
- Also there is the prior distribution (often only shortened to just *prior*) of the parameters $p(\mathbf{w})$

Entering this into Bayes' theorem yields

  $$ p(\mathbf{w}|\mathbf{X}) = \frac{ p(\mathbf{X}|\mathbf{w}) p(\mathbf{w}) } { p(\mathbf{X}) } $$

Some notes about the terms: The prior reflects how the model is trained by samples from the $\mathbf{w}$s.
The likelihood probability refers to the model's knowledge in classifying the sample $\mathbf{X}$ as the class $\mathbf{w}$.
The evidence term shows how much the model knows about the sample.
Typically we will not know this term and replace the denominator by the partition function

  $$ p(\mathbf{w}|\mathbf{X}) = \frac{ p(\mathbf{X}|\mathbf{w}) p(\mathbf{w}) } { \int p(\mathbf{X}|\mathbf{w}) p(\mathbf{w}) } $$

The integral is often also not easily computable because of the large space to cover.


## The prior

The prior takes in the information that we have about the model.
If we do not know anything we can use an uninformative prior, but often some knowledge about the model is available.
Common choices for an informative prior are

- a **Gaussian prior**: This assumes that many of the model parameters will be small
- a **Laplace prior**: This assumes that many of the model parameters will be zero


## Footnotes
