---
title: "MAT223: 12_Inverse Functions and Matrices"
tags: [Note]
date: [2021-01-31]
---

# Inverse Functions and Inverse Matrices

## Invertible functions

- <u>Identity Function</u> - Let $X$ be a set the *identity function* with domain and codomain $X$, notated $id: X \to X$, is the function satisfying, for all $x \in X$
  $$
  \text{id}(x) = x
  $$
  - Identity function is the function that nodes nothing to tis input

- A function is invertible if **it can be undone**. (If there exists an inverse function that when composed with the original function produces the identity function and vice versa)

- <u>Inverse function</u> - Let $f: X \to Y$ be a function, $f$ is *invertible* if there exist a function $g: Y \to X$ so $f \circ g = id$ and $g \circ f = id$. In this case, call $g$ an *inverse* of $f$ and write
  $$
  f^{-1} = g
  $$

- **Every invertible function is both one-to-one and onto and every one-to-one and onto functions is invertible**
  - <u>One-to-one</u> - Let $f: x \to Y$ be a fiction, say $f$ is *one-to-one* (or ***injective***) if distinct inputs to $f$ produces distinct outputs.. That is $f(x) = f(y)$ implies $x=y$
  - <u>Onto</u> - Let $f:X\to Y$ be a function. We say $f$ is *onto* (or ***surjective***) if every point in the codomain of $f$ gets mapped to. That is $range(f) = Y$.

### Invertibility and Linear Transformations

- $\mathcal{T}: \R^n \to \R^m$ Is invertible if and only if $nullity(\mathcal{T}) = 0$ and $rank{\mathcal{(T)}}=m$

- $\mathcal{T}: \R^n \to \R^m$ Is invertible if and only if $m =n$ and $nullity(\mathcal{T}) = 0$

- $\mathcal{T}: \R^n \to \R^m$ Is invertible if and only if $m = n$ and $rank{\mathcal{(T)}}=m$

  > ##### Let $\mathcal{P}: \R^2 \to \R^2$ be projection onto the x-axis and let $\mathcal{R}: \R^2 \to \R^2$ be rotation counter-clockwise by $15^{\circ}$. Classifty each of $\mathcal{P}$ and $\mathcal{R}$ as invertible or not
  >
  > Notice that $\mathcal{P}(\vec{e}_2) = P(2\vec{e}_2) = \vec{0}$ , therefore $\mathcal{P}$ is not one-to-one and so it is not invertible
  >
  > Let $\mathcal{Q}: \R^2 \to \R^2$ be rotation clockwise by $15^{\circ}$. $\mathcal{R}$ And $\mathcal{Q}$ will undo each other. Thus:
  > $$
  > \mathcal{R} \circ \mathcal{Q} = id \quad \text{and} \quad 
  > \mathcal{Q} \circ \mathcal{R} = id
  > $$
  > Therefore, $\mathcal{Q}$ is an inverse of $\mathcal{R}$ and so $\mathcal{R}$ is invertible

- Let $\mathcal{T}$ be an invertible linear transformation, then $\mathcal{T}^{-1}$ is also a linear transformation.


### Investability and Matrices

- <u>Identity matrix</u> - an *identity matrix* is a square matrix with ones on the diagonal and zeros everywhere else. Then $n \times n$ identity matrix is denoted $I_{n \times n}$ or just $I$ when its size is implied
- <u>Matrix inverse</u> - the *inverse* of a matrix $A$ is a matrix $B$ such that $AB = I$ and $BA=I$. In this case, $B$ is called the inverse of $A$ and is notated $A^{-1}$
- An $n \times m$ matrix $A$ is invertible if and only if $nullity(A) = 0$ and $rank(A) = n$
- An $n \times m$ matrix $A$ is invertible if and only if $nullity(A) = 0$
- An $n \times m$ matrix $A$ is invertible if and only if $rank(A) = n$


> ##### Determine whether the matrices $A = \begin{bmatrix}2 & 5 \\ -3 & -7\end{bmatrix}$ and $B = \begin{bmatrix}-7 & -5 \\ 3 & 2\end{bmatrix}$ are inverse of each other
> $$
    AB = \begin{bmatrix}2 & 5 \\ -3 & -7\end{bmatrix} \begin{bmatrix}-7 & -5 \\ 3 & 2\end{bmatrix} = 
    \begin{bmatrix}1 & 0 \\ 0 & 1\end{bmatrix} = I \\
    BA = \begin{bmatrix}-7 & -5 \\ 3 & 2\end{bmatrix} \begin{bmatrix}2 & 5 \\ -3 & -7\end{bmatrix} = 
    \begin{bmatrix}1 & 0 \\ 0 & 1\end{bmatrix} = I
> $$
> Therefore, $A, B$ are inverses of each other


### Matrix Algebra

- Suppose $A$ is invertible, then
    $$
    A \vec{x} = \vec{b} \quad \Rightarrow \quad A^{-1} A \vec{x} = A^{-1}\vec{b} \quad \Rightarrow \quad
    \vec{x} = A^{-1}\vec{b}
    $$
    Thus, if having a inverse of a matrix handy, can use it to solve system of equations.

    > ##### Use th efact that $\begin{bmatrix}2 & 5 \\ -3 & 7\end{bmatrix}^{-1} = \begin{bmatrix}-7 & -5 \\ 3 & 2\end{bmatrix}$ to solve the system $\left\{\begin{matrix}2x + 5y  & =2 \\ -3x-7y & =1\end{matrix}\right.$ 
    > The system can be rewritten as
    > $$
    \begin{bmatrix}2 & 5 \\ -3 & -7\end{bmatrix} \begin{bmatrix}x \\ y\end{bmatrix} = \begin{bmatrix}2 \\ 1\end{bmatrix}
    > $$
    > Multiplying both sides by $\begin{bmatrix}2 & 5 \\ -3 & -7 \end{bmatrix}^{-1}$ gives
    > $$
    \begin{bmatrix}x \\ y\end{bmatrix} = \begin{bmatrix}2 & 5 \\ -3 & -7 \end{bmatrix}^{-1} \begin{bmatrix}2 \\ 1\end{bmatrix} = \begin{bmatrix}-7 & -5 \\ 3 & 2\end{bmatrix}\begin{bmatrix}2 \\ 1\end{bmatrix} = \begin{bmatrix}-19 \\ 8\end{bmatrix}
    > $$
    > Therefore $x = -19$ and $y=8$

- Finding a matrix inverse (==write example here==)


## Elementary Matrices
- <u>Elementary matrix</u> - is an identity matrix with a single elementary row operation applies
- Elementary row operations are
    - Multiply a row by a non-zero constant
    - Add a multiple of one row to another
    - Swap two rows
- A matrix $M$ is invertible if and only if there are elementary matrices $E_1, \dots E_k$ so that
    $$
    E_k \dots E_2E_2M = I
    $$
    - Let $Q = (E_k \dots E_2 E_1)$, then $MQ = I$, then $Q$ is the **inverse of $M$**
- If $A$ is a square matrix and $AB = I$ for some matrices $B$, then $BA = I$
    - ==Write example of using this method to find inverse of a matrix==


### Decomposition int elementary matrices

- A matrix $M$ is invertible if and only if it can be written as the product of elementary matrices
