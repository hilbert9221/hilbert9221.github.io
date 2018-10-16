---
layout: post
title:  Introduction to Information Theory
categories: PRML Notes
use_math: True
---
* TOC
{:toc}
Chapter 1.6
# Two ways to introduce entropy
## A heuristic motivation
Intuition: Information increases as uncertainty increases. Thus, we model an event as a random variable $X$ and look for a quantiy $h(x)$ to measure the uncertainty.

Required Properties:
- $h$ must be nonnegative
- $h$ is monotonic w.r.t. $p$
- $X\perp Y\Rightarrow h(x,y)=h(x)+h(y)$

Induced form: $h$ must be the negative logarithm of $p$.
w.l.o.g., set $h(x)=-\ln p(x)$.

$h(x)$ measures the uncertainty of event $X=x$. To measure the uncertainty of $X$, we use the mathematical expectation of $h$, i.e., ${\rm H}[X]=\mathbb{E}[h]$.

## A measure of disorder in statistical mechanics
Problem. Given $N$ objects and $K$ bins, find the best way of arrangement that minimize the effect of rearrangements. That is, we aim to minimize the _multiplicity_

$$W=\frac{N!}{\prod^K_i n_i!},{\rm s.t.}, \sum n_i=N.$$

By taking logarithm and scaling with $N^{-1}$, we get the entropy

$${\rm H}=\frac{1}{N}\ln W=\frac{1}{N} N!-\frac{1}{N}\sum\ln n_i!.$$

We are to show that this definition is consistent with the heuristic definition above by considering the limit of ${\rm H}$ as $N\to \infty$.

Recalling Stirling's approximation

$$\ln N!=N\ln N - N + O(\ln N),$$

the entropy can be rewritten as

$$
\begin{align}
{\rm H}
&=\frac{1}{N}\sum_i n_i(\ln N - 1 + O(\ln N))-\frac{1}{N}\sum_i (n_i\ln n_i - n_i + O(\ln n_i))\\
&=-\sum_i\frac{n_i}{N}\ln \frac{n_i}{N}+\frac{O(\ln N)}{N} - \frac{1}{N}\sum_i O(\ln n_i).
\end{align}
$$

Taking $N\to\infty$, we have

$$\lim_{N\to\infty}{\rm H}=-\sum_{i}p_i\ln p_i,\,{\rm where}\,p_i=\lim_{N\to\infty}\frac{n_i}{N}.$$

Definition of entropy can be applied to conditional cases. Suppose that we have 2 sets of variables, $X$ and $Y$, where $Y$ is already known. Then then the additional information needed to specify w.r.t. $Y$ is $\ln p(Y\|X)$. Thus, we define the _conditonal entropy_ of $Y$ given $X$ as 

$${\rm H}[Y\vert X]=-\int p(Y,X)\ln p(Y\vert X).$$

# Find maximum entropy probability distribution
Naturally, we hope to maximize the entropy w.r.t. p. Note that this is contraint by the normalization constraint on the probabilities. By adding a Lagrange multiplier, we convert it to be an uncontaint optimization problem. That is, we turn to maximize

$${\rm \widetilde{H}}[p]={\rm H}[p]+\lambda\left(\int p(x)\,{\rm d}x-1\right).$$

By taking gradient w.r.t. $p$, it is easy to show that uniform distribution minimize the entropy in discrete case. While in continuous case, we have to deal with the derivative w.r.t. $p$, a continuous function, a subject in [calculus of variations](https://en.wikipedia.org/wiki/Calculus_of_variations). A detailed dsicussion of calculus of variations is out of scope of this blog. Instead, we just introduce the concept of [functional derivative](https://en.wikipedia.org/wiki/Functional_derivative) and the simple calculation rule.

Defnition. Functional derivative
- $M$: a [manifold](https://en.wikipedia.org/wiki/Manifold) representing functions $\rho$
- $F:M\to\mathbb{R}$: a real valued [funtional](https://en.wikipedia.org/wiki/Functional_(mathematics))

The functional derivative of $F[\rho]$, denoted as $\frac{\delta F}{\delta \rho}$, is defined by

$$\int \frac{\delta F}{\delta \rho}\phi(x)\,dx=\lim_{\epsilon\to 0}\frac{F[\rho+\epsilon\phi]-F[\rho]}{\epsilon},\forall\phi\in M.$$

Usually, $F$ is  expressed in terms of an integral of a fucntion, say $L$. If $L$ is a function of $x,\rho,\,{\rm and\,}\rho'$, we obtain simple explicit forms of the functional derevative, i.e.,

$$
F[\rho]=\int L[x,f,f'], \frac{\delta F}{\delta \rho}=\frac{\partial L}{\partial \rho}-\frac{d}{dx}\frac{\partial L}{\partial \rho'}.
$$

In order for this maximum to be well defined, it will be necessary to constrain the first and second moments of $p$ as well as preserving the normalization constraint. 
(Indeed, I don't understand why adding these two addtional constraints.)Therefore, we turn to maximize

$$
{\rm H}[p; \mathbf{\lambda}]={\rm H}[p] + \mathbf{\lambda}^T\left(\int p - 1, \int xp-\mu,\int(x-\mu)^2p-\sigma^2\right), \mathbf{\lambda}\in\mathbb{R}^3.
$$

Using the computation rule of functional derivative, we have

$$
\frac{\delta H}{\delta p}=-(1+\ln p)+\mathbf{\lambda}^T(1,x,(x-\mu)^2).
$$

$H$ is maximized when its functional derivative is zero. (Maybe igorous argument can be found in texts on calculus of variations.) Thus, we obtain

$$p(x)={\rm exp}\lbrace-1+\mathbf{\lambda}^T(1,x,(x-\mu)^2)\rbrace.$$

By careful computation, we find that $p$ is the p.d.f. of the Gaussian. And the corresponding entropy is ${\rm H}[X]=\frac{1}{2}\left(1+\ln(2\,\pi\sigma^2)\right)$, indicating that the larger the variance, the larger the entropy (of Gaussian). Note that the entropy can be negative if the variance is small enough, which different from dicrete case.

# Relative entropy and mutual information
Problem. Given an unkown distribution $p$, we approximate it with $q$. The difference between them is the additional information. We can quantify it as

$${\rm KL}(p\|q)=-\int p\ln q - \left(-\int p\ln p\right)=-\int p\ln\frac{q}{p}.$$

This is called _Kullback-Leibler divergence_ or _relative entropy_. Note that this quantity is asymmetric. It is notable to show that relative entropy is nonnegative through convexity.

$$
{\rm KL}(p\|q)=-\int p\ln\frac{q}{p} = \mathbb{E}\left[-\ln \frac{q}{p}\right]
\geq -\ln \mathbb{E}\left[\frac{q}{p} \right]=0.
$$

The equality holds iff $q=p,\forall x\in\mathbb{R}$.

Furthermore, we can use Kullback-Leibler divergence to measure the independence or _mutual information_ between two sets of variables, $X$ and $Y$. That is,

$$
{\rm I}[X, Y]=-\int p(X,Y)\ln \frac{p(X)p(Y)}{p(X,Y)}.
$$

Interestingly, this quantity is symmetric, and it turns out to be the difference of entropy of $X$ and the conditonal entropy of $X$ given $Y$, i.e.,

$${\rm I}[X, Y]={\rm H}[X]-{\rm H}[X|Y]={\rm H}[Y|X]-{\rm H}[Y].$$
