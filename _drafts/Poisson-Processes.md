---
layout: post
title:  Poisson Processes
categories: nothing
use_math: True
---
Def. Arrival Process

There are 3 equivalent ways to define arrival processes:
+ arrival process: 
$\lbrace S_n\,\|\,0<S_n<S_{n+1},n\geq 1\rbrace$
+ interarrival times: 
$\lbrace X_n\,\|\,X_n=S_{n+1}-S_n\rbrace$
+ counting process: 
$\lbrace N(t)\,\|\,N(t)=n,t\in\left[S_n, S_{n+1}\right)\rbrace$

Remark. $S_n$, $X_n$ and $N(t)$ are rv s.

Def. Renewal Process

$$\lbrace X_n\,\|\,X_n>0,n\geq 1,{\rm i.i.d.}\rbrace.$$

Def. Poisson process \(subclass of renewal process\)

$$\forall\,n\geq 1, f_{X_n}(x)=\lambda e^{-\lambda x},x\geq 0.$$

Def. Memoryless rv

$$X>0, {\rm Pr}\lbrace X>t+x\rbrace={\rm Pr}\lbrace X>x\rbrace{\rm Pr}\lbrace X>t\rbrace, \forall\,x,t\geq 0$$

Remark. ${\rm Pr}\lbrace X>x\rbrace$ must be exponential in $x$ due to its memoryless property and monotonicity.

Thm. 
+ ${\rm Pr}\lbrace Z>z\,\|\,N(t)=n,S_n=\tau\rbrace={\rm Pr}\lbrace X_{n+1}>z\rbrace=e^{-\lambda z},X_{n+1}=z+(t-\tau)$
+ ${\rm Pr}\lbrace Z>z\,\|\,\lbrace N(\tau),\tau\in(0,t]\rbrace\rbrace$

Def. Stationary Increment Property

$\forall\,t'>t>0,\widetilde{N}(t,t')=N(t')-N(t)$ has the same CDF as $N(t'-t)$.

Def. Independent Increment Property

$\forall\,k\in\mathbb{Z}^+,\lbrace t_i\,\|\,0< t_i < t_{i+1},i=0,\dots,k-1 \rbrace,N(t_1),\widetilde{N}(t_1,t_2),\dots,\widetilde{N}(t_{k-1},t_k)$
are statistically independent.

Remark. Poisson processes have both properties defined above.

PDF of $S_n$, JPDF of $S_1,\dots,S_n$ and PMF of $N(t)$
+ $f_{S_n}(t)=\frac{\lambda^n t^{n-1}e^{-\lambda t}}{(n-1)!}$
+ $f_{S_1\cdots S_n}(s_1,\dots,s_n)=\lambda^n e^{-\lambda s_n},0\leq s_1\leq\cdots\leq s_n$
+ $f_{N(t)}(n)=\frac{(\lambda t)^n e^{-\lambda t}}{n!}$

Proofs. To be done.

