---
layout: post
title:  Chapter 2. Instructions Language of the Computer
categories: Priciples of Computer Organization
use_math: True
---
* TOC
{:toc}
# Syntax
Operations
- Arithmetic Operations: op destination, source, source
- Memory Operands
    - Assess Address: offset(base register)
    - Load Word: lw destination, source
    - Store Word: sw destination, source
![Memory Operands](/img/Memory Operands.png)
Design Principles
- Immediate Operands: addi destination, source, constant
- Conditional Operations: op source, source, instruction

> Simplicity favours regularity \\
> Smaller is faster \\
> Make the common case faster\\
> Good design demands good compromises\\

# Binary Representation 
## Representations of Integers
- Unsigned Integers: $x=\sum^{n-1}_{i=0}x_i2^i$
- Signed Integers: $x=-x_{n-1}2^{n-1}+\sum^{n-2}_{i=0}x_i2^i$

Properties:
- Complement $\bar{x}$: $x+\bar{x}=-1$
- Negation: $-x=\bar{x}+1$

## Representations of Instructions
![Register Usage](/img/Register Usage.png)
![R-format Instructions](/img/R-format.png)
![I-format Instructions](/img/I-format.png)