---
jupytext:
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.11.5
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---

# 1 - Gaussian processes and PDEs

The objective of this article is to illustrate how solving PDE constrained inverse problems and doing Gaussian process regression are not so different after all (atleast for some priors). 
To illustrate this connection, we will consider the case of a linear, elliptic, second order partial differential equation.

```{admonition} Definition: Second order linear elliptic PDE
:class: tip
d
```

```{admonition} Definition: Gaussian process
:class: tip
d
``` 

```{admonition} Definition: Gaussian process regression
:class: tip
d
```

```{admonition} Definition: Source estimation of elliptic PDE
:class: tip
d
``` 
It is clear from this juxtaposition, that these two problems are the same after all.
So, at this point we inquire : How to make this connection explicit?
To do so, we will consider the integral representation of the solution to the ellptic PDE.

$$u(x) = \int_{\Omega} d\mu(y) \; K(x,y) \; a(y). $$
Furthermore, assume that the measure $\mu$ is empirical. That is,

$$d\mu(y) := \frac{1}{M}\sum_{i=1}^M \delta(x-\hat{\Omega}_i). $$
Then, we can show that the solution to the elliptic PDE is:

$$u(x) = \sum_{i=1}^M \frac{a(\hat{\Omega}_i)}{M} K(x, \hat{\Omega}_i).$$
Notice that, this is just the RKHS-optimal solution given by the [representer theorem](https://en.wikipedia.org/wiki/Representer_theorem). Notice that the point evaluations of $a$, defined by:

$$
    a(\hat{\Omega}_i) := \int_{\Omega} dx \; a(x) \; \delta(x,\hat{\Omega}_i), 
$$
have to be estimated by solving a regularized linear least squares problem. Denoting by $A := \{ \frac{1}{M}a(\hat{\Omega}_i)\}_{i=1}^M$, this problem is given by 

$$
    A = \arg \min_{S \in \mathbb{R}^M} \frac{1}{2}\| K(\hat{\Omega}, \hat{\Omega}) S - u(\hat{\Omega})\|_2^2 + \lambda \|S\|_2^2.
$$

The corresponding solution is known in closed form:

$$
    A = (K(\hat{\Omega}, \hat{\Omega}) + \lambda I)^{-1} u(\hat{\Omega}).
$$
Therefore,

$$
    u(x) = \sum_{i=1}^M K(x,\hat{\Omega}_i) [(K(\hat{\Omega}, \hat{\Omega}) + \lambda I)^{-1} u(\hat{\Omega})]_i. 
$$
Notice, that this is equal to the expectation of a conditioned Gaussian process. 

To make this equivalance stronger, we have to redefine $a$ as an $L^2$ Gaussian random  field. 
```{admonition} Definition: Gaussian random field
:class: tip
d
```