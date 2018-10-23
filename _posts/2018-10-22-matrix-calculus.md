---
layout: post
title:  Matrix Derivative
categories: Analysis
use_math: True
---
* TOC
{:toc}
Matrix derivative appears naturally in multivariable calculus, and it is widely used in deep learning. Since doing element-wise calculus is messy, we hope to find a set of compact notations and effective computation rules. Unfortunately, a complete solution requires arithmetic of [tensors](https://en.wikipedia.org/wiki/Tensor). For example, taking matrix derivative of a matrix-valued function gives rise to a fourth-rank tensor, while we are more familiar with linear algebra. A remedy is to vetorize matrices and consider only vector-by-vector derivative. Although this may introduces tensor product and some tricky computation rules, as shown below, all we have to deal with is linear algebra. 

We are to briefly introduce the definition of derivative and some useful computation rules, and illustrate it through some examples. For a complete introduction, readers may refer to [Matrix Calculus](https://en.wikipedia.org/wiki/Matrix_calculus) in wiki. For tricks in taking derivative w.r.t. matrices, readers may refer to [MatCalc](http://www4.ncsu.edu/%7Epfackler/MatCalc.pdf). Both are important reference for this blog.

# Basics
Conventions
- scalar: greek letter in lower case, e.g. $\alpha$.
- vector (in column): lower case letter, e.g. $x$.
- matrix: upper case letter, e.g. $A$.
- component of vector or matrix: letters with subscript, e.g. $x_1$.

First, we introduce the definition of derivative of a column vector w.r.t. a row vector, which is a matrix.

Defnition. Vector-by-vector derivative
- $f:\mathbb{R}^n\to\mathbb{R}^m, y=f(x)$
- $\frac{\partial f}{\partial x^T}=\frac{\partial y}{\partial x^T}=\left(\frac{\partial y_i}{\partial x_j}\right)\in\mathbb{R}^{m\times n}$

Remark. Scalar-by-vector derivative (gradient) and vector-by-scalar derivative are special cases of this definition.

Differential is a more general concept than derivative and they are closely connected. 

Definition. Differential

${\rm d}x=({\rm d}x_1,\dots,{\rm d}x_n)^T$

Property.

${\rm d}y=\frac{\partial f}{\partial x^T}{\rm d}x$

Remark. The form is consistent with univariate case.

For matrix, we introduce vectorization, and treat a matrix as a column vector.

Definition. Vectorization of matrix (stacking matrix in columns)
- $A\in\mathbb{R}^{m\times n}$
- ${\rm vec}(A)=(a_{1,1},\dots,a_{m,1},\dots,a_{n,1},\dots,a_{m,n})^T$

Remark.
- Vectorization is a linear operator.
- We can vectorize the vector-by-vector derivative and compute higher order derivatives.

Now we turn to point out some useful rules for taking derivatives. Obviously, the linearity of derivative and the chain rule are the most essential ones.

Linearity.
- $f_i:\mathbb{R}^n\to\mathbb{R}^m, y_i=f_i(x),i=1,2$
- $\frac{\partial (\alpha y_1+\beta y_2)}{\partial x^T}=\alpha\frac{\partial y_1}{\partial x^T}+\beta\frac{\partial y_2}{\partial x^T},\alpha,\beta\in\mathbb{R}$

Chain rule.
- $f:\mathbb{R}^n\to\mathbb{R}^m, y=f(x)$
- $g:\mathbb{R}^m\to\mathbb{R}^p, z=g(y)$
- $\frac{\partial z}{\partial x^T}=\frac{\partial z}{\partial y^T}\frac{\partial y}{\partial x^T}$

Remark. If we define the vector-by-vector derivative in form of row-to-column, the order of the terms in the chain rule should be reversed after taking the transpose.

# Properites of vectorization
Rules above are insufficient when it comes to vectorize a matrix-valued function. Therefore, we are to introduce some properties of vectorization, especially when the matrix-valued function is linear.

The most common case is matrix multiplication, while Kronecker product provides the best solution.

Definition. Kronecker product
- $A\in\mathbb{R}^{m\times n}, B\in\mathbb{R}^{p\times q}$
- $A\otimes B = (a_{ij}B)\in\mathbb{R}^{mp\times nq}$

Properties.
- ${\rm vec}(AXB)=(B^T\otimes A){\rm vec}(X)$
- ${\rm vec}(AX)=(I\otimes A){\rm vec}(X), {\rm vec}(XB)=(B^T\otimes I){\rm vec}(X)$

Another common linear operator is taking transpose. Define a matrix $T_{m,n}$ such that $T_{m,n}{\rm vec}(A)={\rm vec}(A^T),A\in\mathbb{R}^{m\times n}$. It can be verified that $T_{m,n}$ is a permutation matrix and thus, an orthogonal matrix.

Readers interested in the derivative of Kronecker product may refer to Page 7-8 in [MatCalc](http://www4.ncsu.edu/%7Epfackler/MatCalc.pdf).

# Useful rules for element-wise functions
If $f$ is a univariate real-valued function, and $x\in\mathbb{R}^n$ is a vector, we define $f(x)$ to be $(f(x_1),\dots,f(x_n))^T$. Obviously, $\frac{\partial f}{\partial x^T}={\rm diag}\left((f'(x_1),\dots,f'(x_n))^T\right)$, where ${\rm diag}: \mathbb{R}^n\to\mathbb{R}^{n\times n}$ maps a vector to a matrix whose diagonal entries starting in the upper left corner are $x_1,\dots,x_n$.

For element-wise product, a.k.a. Schur product or Hadamard product, product rule in univariate case can be easily generalized to multivariate case.

Definition. Schur product/Hadamard product
- $A, B\in\mathbb{R}^{m\times n}$
- $A\circ B=(a_{ij}b_{ij})\in\mathbb{R}^{m\times n}$

Property.

$A, B\in\mathbb{R}^{m\times n},{\rm d}(A\circ B)={\rm d}A\circ B+A\circ {\rm d}(B)$

# Examples

## Softmax Regression
The first example is [softmax regression](http://ufldl.stanford.edu/tutorial/supervised/SoftmaxRegression/), a widely used in multiclass classification probelm. We only consider the loss of a single sample to illustrate the rules above.

Model
- linear mapping: $z=\Theta x,\Theta\in\mathbb{R}^{k\times(n+1)},x\in\mathbb{R}^{n+1}$
- softmax: $a=\frac{e^z}{\mathbf{1}^T e^z}$
- loss: $C=-\mathbf{1}^T(y\circ \log(a)),y\in\mathbb{R}^k$ is the one-hot representation of the label.

Derivatives

- $\frac{\partial C}{\partial a^T}
=-\frac{\partial(y\circ \log(a))}{\partial a^T}
=-y^T\circ \frac{\partial\log(a)}{\partial a^T}
=-\left(\frac{y}{a}\right)^T$
- $\frac{\partial a}{\partial z^T}
=\frac{1}{\mathbf{1}^T e^z}\frac{\partial e^z}{\partial z^T}+e^z\frac{\partial (\mathbf{1}^T e^z)}{\partial z^T}
=\frac{ {\rm diag}(e^z)}{\mathbf{1}^T e^z}
-\frac{e^z{e^z}^T}{(\mathbf{1}^T e^z)^2}
={\rm diag}\left(\frac{e^z}{\mathbf{1}^T e^z}\right)-\frac{e^z}{\mathbf{1}^T e^z}\frac{ {e^z}^T}{\mathbf{1}^T e^z}
={\rm diag}(a)-aa^T$
- $\frac{\partial a}{\partial {\rm vec}(\Theta)^T}
=x^T\otimes I\Leftarrow{\rm vec}(\Theta x)=(x^T\otimes I){\rm vec}(\Theta)$

Combining the formulas above, we obtain 

$\frac{\partial C}{\partial {\rm vec}(\Theta)^T}
=-\left(\frac{y}{a}\right)^T\left({\rm diag}(a)-aa^T\right)\left(x^T\otimes I\right)
=y^T(\mathbf{1}a^T-I)\left(x^T\otimes I\right).$


## Multilayer Perceptron
When considering the loss of multiple samples, i.e., our input is a matrix with each column as the feature of a sample, we have to deal with matrix-by-matrix derivatives and that requires more tricks related to Kronecker product. We will take [multilayer perceptron](https://en.wikipedia.org/wiki/Multilayer_perceptron) as an example. For the case of single sample, [Micheal Nielsen's blog](http://neuralnetworksanddeeplearning.com/chap2.html) provides an excellent derivation.

Model
- number of layers: $L$
- parameters in $l$-th layer: $W^l, B^l,l=0,\dots,L$
- loss: $C=\frac{1}{2}\left\Vert Y-A^L\right\Vert^2_F$
- activation: $A^l=\sigma\left(Z^l\right)$
- linear layer: $Z^l=W^lA^{l-1}+B^l$

Derivatives
- $\frac{\partial C}{\partial {\rm vec}(A^L)^T}={\rm vec}\left(Y-A^L\right)^T$
- $\frac{\partial C}{\partial {\rm vec}(Z^l)^T}
=\frac{\partial L}{\partial {\rm vec}(Z^{l+1})^T}\frac{\partial {\rm vec}(Z^{l+1})}{\partial {\rm vec}(A^l)^T}\frac{\partial {\rm vec}(A^{l})}{\partial {\rm vec}(Z^l)^T}
=\frac{\partial L}{\partial {\rm vec}(Z^{l+1})^T}\left(I\otimes W^{l+1}\right)
{\rm diag}\left({\rm vec}\left(\sigma'(Z^l)\right)\right)$
- $\frac{\partial C}{\partial {\rm vec}(B^l)^T}=\frac{\partial C}{\partial {\rm vec}(Z^l)^T}\frac{\partial {\rm vec}(Z^l)}{\partial {\rm vec}(B^l)^T}=\frac{\partial C}{\partial {\rm vec}(Z^l)^T}$
- $\frac{\partial C}{\partial {\rm vec}(W^l)^T}
=\frac{\partial C}{\partial {\rm vec}(Z^l)^T}\frac{\partial {\rm vec}(Z^l)}{\partial {\rm vec}(W^l)^T}
=\frac{\partial C}{\partial {\rm vec}(Z^l)^T}\left({A^{l-1}}^T\otimes I\right)$

Denote ${\delta^l}^T=\frac{\partial C}{\partial {\rm vec}(Z^l)^T}$. We can compute ${\delta^l}^T$ recursively and obtain $\frac{\partial C}{\partial {\rm vec}(B^l)^T}$ and $\frac{\partial C}{\partial {\rm vec}(W^l)^T}$.

# Postscript
Although the method above simplifies some expressions of derivatives, computing the intermediate derivatives may require more memory, which can be impractical. For example, to derive a scalar-by-matrix derivative $\frac{\partial C}{\partial {\rm vec}(W^l)^T}$ in MLP (usually our objective is a real-valued function), we may have to compute a matrix-by-matrix derivative that requires Kronecker product, like ${A^{l-1}}^T\otimes I$, which is sparse and large, making the computation less efficient. Maybe I should read the source code of automatic differentiation in some deep learning frameworks, such as [PyTorch](https://pytorch.org/) to find a compromise between compact expression and efficient implemetation. This remains to be done.
