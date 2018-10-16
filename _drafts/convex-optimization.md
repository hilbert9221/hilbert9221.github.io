---
layout: post
title:  Convex Optimization
categories: nothing
use_math: True
---
# Convex Sets
def. convex sets
+ convex sets:
$\forall\,x_1,x_2\in C,\theta\in [0,1],\theta x_1 + (1-\theta)x_2 \in C$
+ convex hull of a  set $C$: ${\rm conv}\,C:=\lbrace \sum \theta_i x_i\,\|\,x_i\in C,\theta_i \geq 0,i=1,\dots,k,\sum \theta_i = 1\rbrace$, i.e., ${\rm conv}\,C$ is the closure of $C$ under convex combinations.
+ convex cone: $\forall\,x_1,x_2\in C,\theta_1,\theta_2\geq 0,\theta_1 x_1 + \theta_2 x_2 \in C$
+ conic hull: ${\rm conv}\,C:=\lbrace \sum \theta_i x_i\,\|\,x_i\in C,\theta_i \geq 0,i=1,\dots,k\rbrace$, i.e., ${\rm conv}\,C$ is the closure of $C$ under conic combinations.
+ hyperplane: $\lbrace x\,\|\,a^Tx=b\rbrace$
+ halfspace: $\lbrace x\,\|\,a^Tx\leq b\rbrace$
+ Euclidean ball: $B(x_c,r)=\lbrace x_c+r\mathbb{u}\,\|\,\lVert \mathbb{u}\rVert_2 \leq 1\rbrace$
+ ellipsoid: $B(x_c,r)=\lbrace x_c+A\mathbb{u}\,\|\,\lVert \mathbb{u}\rVert_2 \leq 1\rbrace$
+ norm cone: $C=\lbrace (x,t)\,\|\,\lVert x\rVert \leq t\rbrace$
+ polyhedra: $\mathcal{P}:=\lbrace x\,\|\,Ax\preceq b,Cx=d\rbrace$
+ symmetric matrices: $S^n:=\lbrace X\in M_{n\times n}(\mathbb{R})\,\|\,X=X^T\rbrace$
+ positive semidefinite matrices: $S^n_+:=\lbrace X\in S^n\,\|\,X\succeq 0\rbrace$
+ positive definite matrices: $S^n_{++}:=\lbrace X\in S^n\,\|\,X\succ 0\rbrace$

operations that preserve convexity
+ intersection
+ affine function: $f(x)=Ax+b$
+ perspective function: $P:\mathbb{R}^n\times\mathbb{R}^+,P(z,t)=\frac{z}{t}$
+ linear-fractional function: $P(Ax+b,c^Tx+d)$

def. proper cone $K$
+ convex cone
+ closed
+ solid, i.e., $K^{\circ}\neq \emptyset$.
+ pointed, i.e., $\forall\,x\in K,-x\in K\Rightarrow x=0$.

def. generalized inequalities
+ $x\preceq_K y \iff y-x \in K$
+ $x\prec_K y \iff y-x \in K^{\circ}$

properties of generalized inequalities
+ preserved under addition
+ transitive
+ preserved under nonnegative scaling
+ reflextive
+ antisymmetric
+ preserved under limits

minimum and minimal elements
+ minimum: $\forall\,y\in S,x\preceq_K y$, i.e., $S\subset x+K$
+ minimal: $y\preceq_K x\Rightarrow x=y$, i.e., $(x-K)\cap S=\lbrace x\rbrace$

thm. separating hyperplane theorem
+ convex sets: $C,D$
+ $C\cap D=\emptyset$

$\Rightarrow \exists\,a\neq 0,b,{\rm s.t.},\forall\,x\in C,a^Tx\leq b,\forall\,x\in D,a^Tx\geq b$