---
layout: post
title:  Theoretical Computer Science
categories: nothing
use_math: True
---
* TOC
{:toc}
# Computable functions
def. URM \(Unlimited Register Machine\)
+ Representation:
$\lbrace R_n=r_n\,\|\,r_n\in\mathbb{N},n\in\mathbb{Z}^+\rbrace$
+ 4 instructions:
    - Zero $Z(n)$: set $r_n:=0$
    - Successor $S(n)$: $r_n:=r_n+1$
    - Transfer $T(m,n)$: $r_n:=r_m$
    - Jump $J(m,n,q)$: if $r_m=r_n$, proceed to the $q$th instruction; else, the next.

def. Computations 
A sequence of instructions, $\lbrace I_i\|i=1,\dots,s\rbrace$ operating on an initial configuration of URM.

Notations
+ initial configuration: $\mathbf{a}=(a_1,a_2,\dots)$
+ convergence: $P(\mathbf{a})\downarrow$
+ divergence: $P(\mathbf{a})\uparrow$

def. URM-computable
+ $f:\mathbb{N}^n\to\mathbb{N}$
+ $P$ URM-computes $f$: $\forall\,\mathbf{a}\in\mathbb{N}^n,b\in\mathbb{N},P(\mathbf{a})\downarrow b\quad iff\quad\mathbf{a}\in{\rm Dom}(f) \wedge f(\mathbf{a})=b$
+ $f$ is URM-computable if there is a program that URM-computes $f$.
+ $\mathscr{C}:=\lbrace$URM-computable functions$\rbrace$
+ $\mathscr{C}_n:=\lbrace$n-ary URM-computable functions$\rbrace$

def. Decidable
+ n-ary predicate: $M(\mathbf{x}),\mathbf{x}\in\mathbb{N}^n$
+ characteristic function:
$$c_M(\mathbf{x}):=
{\begin{cases}1&{\rm if}\,M(\mathbf{x})\,{\rm holds,}\\
0&{\rm otherwise.}
\end{cases}}$$
+ $M$ is decidable if $c_M$ is computable, otherwise, undecidable.

# Generating computalbe functions
Basic computable functions
+ zero function 
+ successor function
+ projection function $U^n_i(\mathbf{x})=x_i$

Remark. The functions above correspond to $Z(1),S(1)$ and $T(i,1)$, which are basic instructions of URM.

def. standard form if a program
+ $P=\lbrace I_k\rbrace^s_1$
+ $\forall\,J(m,n,q),q\leq s+1$

Operations preserving computability
+ Concatenation: 
    - $PQ=\lbrace I_i\rbrace^s_1+\lbrace I_i\rbrace^{s+t}_{s+1}$
    - Replace $J(m,n,q)$ with $J(m,n,q+s)$ in $Q$.
+ Substitution:
    - $f: \mathbb{N}^k\to\mathbb{N}$
    - $g_i: \mathbb{N}^n\to\mathbb{N},i=1,\dots,k$
    - $h(\mathbb{x}):=f(g_1(\mathbb{x}),\dots,g_k(\mathbb{x}))$
+ Recursion:
    - $f(\mathbb{x}),g(\mathbb{x},y,z)$
    - $h(\mathbb{x},0):=f(\mathbb{x})$
    - $h(\mathbb{x},y+1):=g(\mathbb{x},y,h(\mathbb{x},y))$
+ Minimization:

$$g(\mathbb{x},y)=\mu z < y(f(\mathbb{x},z)=0)=
\begin{cases}
\min\lbrace z\,|\,z < y, f(\mathbb{x},z)=0\rbrace &{\rm if\,such}\,z\, {\rm exists,} \\
y &{\rm otherwise.}
\end{cases}$$

# Church's thesis
def. Partial recursive functions $\mathscr{R}$
+ $Z,S,U^n_i\in\mathscr{R}$
+ $\mathscr{R}$ is closed under substitution, recursion and minimalization.
+ $\mathscr{R}$ is the smallest class of partial functions that satisfies the conditions above.

