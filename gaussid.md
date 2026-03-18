# Gaussian Identities
**Author:** Sam Roweis
**Date:** Revised July 1999 (Corrected 2026 by Gemini 3.1 Pro)

---

### 0.1 Multidimensional Gaussian
A $d$-dimensional multidimensional gaussian (normal) density for $x$ is:

$$\mathcal{N}(\mu,\Sigma)=(2\pi)^{-d/2}|\Sigma|^{-1/2}\exp\left[-\frac{1}{2}(x-\mu)^{T}\Sigma^{-1}(x-\mu)\right]$$

It has entropy:

$$S = \frac{1}{2} \log_2 [(2\pi e)^d |\Sigma|] + \text{const bits}$$

*(where $\Sigma$ is a symmetric positive semi-definite covariance matrix and the (unfortunate) constant is the log of the units in which $x$ is measured over the "natural units")*

### 0.2 Linear Functions of a Normal Vector
No matter how $x$ is distributed,

$$E[Ax+y]=A(E[x])+y$$

$$\text{Covar}[Ax+y]=A(\text{Covar}[x])A^{T}$$

In particular this means that for normal distributed quantities:

$$x\sim\mathcal{N}(\mu,\Sigma)\Rightarrow(Ax+y)\sim\mathcal{N}(A\mu+y,A\Sigma A^{T})$$

$$x\sim\mathcal{N}(\mu,\Sigma)\Rightarrow\Sigma^{-1/2}(x-\mu)\sim\mathcal{N}(0,I)$$

$$x\sim\mathcal{N}(\mu,\Sigma)\Rightarrow(x-\mu)^{T}\Sigma^{-1}(x-\mu)\sim\chi_{d}^{2}$$

### 0.3 Marginal and Conditional Distributions
Let the vector $z=[x^{T}y^{T}]^{T}$ be normally distributed according to:

$$z=\begin{bmatrix}x\\ y\end{bmatrix}\sim\mathcal{N}\left(\begin{bmatrix}a\\ b\end{bmatrix},\begin{bmatrix}A&C\\ C^{T}&B\end{bmatrix}\right)$$

*(where $C$ is the (non-symmetric) cross-covariance matrix between $x$ and $y$ which has as many rows as the size of $x$ and as many columns as the size of $y$)*

Then the marginal distributions are:

$$x\sim\mathcal{N}(a,A)$$

$$y\sim\mathcal{N}(b,B)$$

And the conditional distributions are:

$$x|y\sim\mathcal{N}(a+CB^{-1}(y-b),A-CB^{-1}C^{T})$$

$$y|x\sim\mathcal{N}(b+C^{T}A^{-1}(x-a),B-C^{T}A^{-1}C)$$

### 0.4 Multiplication
The multiplication of two gaussian functions is another gaussian function (although no longer normalized). In particular,

$$\mathcal{N}(a,A)\cdot\mathcal{N}(b,B)\propto\mathcal{N}(c,C)$$

where

$$C=(A^{-1}+B^{-1})^{-1}$$

$$c=CA^{-1}a+CB^{-1}b$$

Amazingly, the normalization constant $z_{c}$ is Gaussian in either $a$ or $b$:

$$z_{c}=(2\pi)^{-d/2}|C|^{+1/2}|A|^{-1/2}|B|^{-1/2}\exp\left[-\frac{1}{2}(a^{T}A^{-1}a+b^{T}B^{-1}b-c^{T}C^{-1}c)\right]$$

$$z_{c}(a) \sim \mathcal{N}(b, A + B)$$

$$z_{c}(b) \sim \mathcal{N}(a, A + B)$$

### 0.5 Quadratic Forms
The expectation of a quadratic form under a gaussian is another quadratic form (plus an annoying constant).
In particular, if $x$ is gaussian distributed with mean $m$ and variance $S$ then,

$$\int_{x}(x-\mu)^{T}\Sigma^{-1}(x-\mu)\mathcal{N}(m,S)dx = (\mu-m)^{T}\Sigma^{-1}(\mu-m)+\text{Tr}[\Sigma^{-1}S]$$

If the original quadratic form has a linear function of $x$ the result is still simple:

$$\int_{x}(Wx-\mu)^{T}\Sigma^{-1}(Wx-\mu)\mathcal{N}(m,S)dx = (\mu-Wm)^{T}\Sigma^{-1}(\mu-Wm)+\text{Tr}[W^{T}\Sigma^{-1}WS]$$

### 0.6 Convolution
The convolution of two gaussian functions is another gaussian function (and is normalized if the inputs are probability densities). In particular,

$$\mathcal{N}(a,A)*\mathcal{N}(b,B)=\mathcal{N}(a+b,A+B)$$

This is a direct consequence of the fact that the Fourier transform of a gaussian is another gaussian and that the multiplication of two gaussians is still gaussian.

### 0.7 Fourier Transform
The (inverse) Fourier transform of a gaussian function is another gaussian function (although no longer normalized). In particular,

$$\mathcal{F}[\mathcal{N}(a,A)]\propto\mathcal{N}(jA^{-1}a,A^{-1})$$

$$\mathcal{F}^{-1}[\mathcal{N}(b,B)]\propto\mathcal{N}(-jB^{-1}b,B^{-1})$$

where $j=\sqrt{-1}$

### 0.8 Constrained Maximization
The maximum over $x$ of the quadratic form:

$$\mu^{T}x-\frac{1}{2}x^{T}A^{-1}x$$

subject to the $J$ conditions $c_{j}(x)=0$ (linear constraints $C^T x = 0$) is given by:

$$x = A\mu+AC\Lambda$$

$$\Lambda=-(C^{T}AC)^{-1}C^{T}A\mu$$
where the $j$th column of $C$ is $\partial c_{j}(x)/\partial x$

