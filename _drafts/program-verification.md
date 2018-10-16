---
layout: post
title:  The Foundations of Program Verification
categories: nothing
use_math: True
---
# Mathematical Preliminaries
def. Relations
+ relation between $S$ and $T$: $R\subset S\times T$
+ relation on $S$: $S=T$
+ image of $A\subset S$ under $R$: 
$R(A):=\lbrace t\in T\,|\,(s,t)\in R, s\in A\rbrace$
+ pre-image of  $B\subset T$ under $R$:
$R^{-1}(B):=\lbrace s\in S\,|\,(s,t)\in R,t\in B\rbrace$
+ closure of $R$ on $S$: the smallest reflexive, tansitive relation which contains $R$, denoted as $R^*$.

def. Partial Orders
+ partial order $(P,\sqsubseteq)$: $\sqsubseteq$ is reflexive, antisymmetric and transitive. $P$ is also called a _poset_.
+ monotonic function: $f:P_1\to P_2,a\sqsubseteq_1 b \Rightarrow f(a)\sqsubseteq_2 f(b)$

def. Inductive Definitions of Sets
+ universe: $U$
+ basis set: $B\subset U$
+ constructor set: $K=\lbrace r\subset U^n\times U\,\|\,r\,{\rm satisfies\,some\,conditions}\rbrace$
+ $S$:
    - $B\subset S$
    - $\forall\,r\in K,r(S^n)\subset S$
+ $A:=\min (S,\subset)$
$A\subset U$ is called _inductively defined_ by $B$ and $K$.

def. Alternative definition
+ a constrruction sequence for $u$: $\lbrace u_i\rbrace^m_1,u_m=u$
+ $u_i\in B$
+ $\exists\,r\in K,i_1,\dots,i_n < i,{\rm s.t.},((u_{i_1},\dots,u_{i_n}),u_i)$

def. Free Inductive Definitions

$\forall\,a\in A,a\in B\,{\rm or}\,\exists !\mathbb{a}\in A^n,{\rm s.t.},(\mathbb{a},a)\in r$

def. Well-founded Sets (WFS)
+ $(W,\sqsubseteq)$
+ $\forall\,S\subset W,\exists\,\min S$

Remark. $(W,\sqsubseteq)$ is a well-founded set iff $\nexists \lbrace a_i\,\|\,a_{i+1}\sqsubset a_i,i\in\mathbb{N} \rbrace\subset W$.

thm. The Principle of Noetherian Induction
+ Induction basis: $\forall\,x\in \min W,P(x)=1$.
+ Induction step: $\forall\,x\notin \min W,\forall\,y\in W,y\sqsubset x,P(y)=1\Rightarrow P(x)=1$.  

# Predicate Logic
def. logical symbols
+ connectives: $\neg,\wedge,\vee,\supset,\equiv$
+ equality symbol: $=$
+ existential quantifier: $\exists$, universal quantifier: $\forall$
+ 4 punctuation marks: ., (, ) and ,
+ variables ($V$)
+ truth symbols: $true$ and $false$

def. extralogical symbols
+ the set of function symbols: $F$
+ the set of predicate symbols: $P$
+ constants: $0$-ary function
+ propositional constants: $0$-ary predicate

def. terms
+ basis: $B=(F,P)$
+ set of terms: $T_B$
+ inductive definition:
    - $V\subset T_B,{\rm const}(F)\subset T_B$
    - $\mathbb{t}\in T_B^n,f\in F \Rightarrow f(\mathbb{t})\in T_B$

def. well-formed formuals 
+ denotation: $WFF_B$
+ $\lbrace true,false \rbrace\subset WFF_B$
+ ${\rm const}(P)\subset WFF_B$
+ $t_1,t_2\in T_B \Rightarrow (t_1=t_2) \in WFF_B$
+ $\mathbb{t}\in T_B^n,p\in P\Rightarrow p(\mathbb{t})\in WFF_B$
+ $w\in WFF_B\Rightarrow \neg w\in WFF_B$
+ $w\in WFF_B,x\in V \Rightarrow (\forall\,x.w),(\exists\,x.w)\in WFF_B$
+ $w_1,w_2\in WFF_B\Rightarrow (w_1\wedge w_2),(w_1\vee w_2),(w_1\supset w_2),(w_1 \equiv w_2)\in WFF_B$

def. Interpretation
+ denotation: $\mathscr{I}=(D,\mathscr{I}_0)$
+ domain: $D$
+ $\mathscr{I}_0({\rm const}(F))\subset D$
+ $\mathscr{I}_0(f):D^n\to D$
+ $\mathscr{I}_0({\rm const}(P))\subset {\rm Bool}$
+ $\mathscr{I}_0(p):D^n\to {\rm Bool}$