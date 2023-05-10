---
title: "MAT223: 7_Matrix"
tags: [Note]
date: [2021-01-31]
---

# Matrix

## Coefficient matrix

- Every system (or single) of linear equations can be rewritten as a matrix equation of the form

  $A\vec{x} = \vec{b}$, where $A$ is a coefficient matrix, $\vec{x}$ is a column vector of variables, and $\vec{b}$ is a column vector of constants

  > $$
  > A: \quad \left\{\begin{matrix} 
  > x+2y-2z = -15 \\ 
  > 2x+y-5zz = -21 \\ 
  > x-4y+z = 18\end{matrix}\right.
  > \quad \text{can be writen as} \quad
  > \begin{bmatrix}
  > 1 & 2 & -2\\
  > 2 & 1 & -5 \\
  > 1 & -4 & 1
  > \end{bmatrix}
  > \begin{bmatrix} x \\ y \\ x \end{bmatrix} =
  > \begin{bmatrix} -15 \\ -21 \\ 18 \end{bmatrix}
  > $$

## The column Picture

- Using the column interpretation of matrix to rewrite system $A$:
  $$
  \begin{bmatrix}
  1 & 2 & -2\\
  2 & 1 & -5 \\
  1 & -4 & 1
  \end{bmatrix}
  \begin{bmatrix} x \\ y \\ x \end{bmatrix} =
  x \begin{bmatrix}1 \\ 2 \\ 1\\ \end{bmatrix} +
  y \begin{bmatrix}2 \\ 1 \\ -4\\ \end{bmatrix} +
  z \begin{bmatrix}-2 \\ -5 \\ 1\\ \end{bmatrix} =
  \begin{bmatrix} -15 \\ -21 \\ 18 \end{bmatrix}
  $$

- This interpretation is mostly used to find the solutions to the system $A$ 
  
  - What **linear combinations** of the columns of $A$ would give the constant vector

## The Row Picture

- Let $\vec{r}_1, \vec{r}_3, \vec{r}_3$ be the rows of the coefficient matrix for $A$:
  $$
  \begin{bmatrix}
  1 & 2 & -2\\
  2 & 1 & -5 \\
  1 & -4 & 1
  \end{bmatrix}
  \begin{bmatrix} x \\ y \\ x \end{bmatrix} =
  \begin{bmatrix} \vec{r}_1 \\ \hline \vec{r}_2 \\ \hline \vec{r}_3 \end{bmatrix}
  \vec{u} = 
  \begin{bmatrix} \vec{r}_1 \cdot \vec{u} \\ 
  \vec{r}_2 \cdot \vec{u} \\ \vec{r}_3 \cdot \vec{u} \end{bmatrix} =
  \begin{bmatrix} -15 \\ -21 \\ 18 \end{bmatrix}
  $$

- This interpret the solutions to the system $A$ as vectors whose dot product with $\vec{r}_1$ is $-15$,  $\vec{r}_2$ is $-21$, $\vec{r}_3$ is $18$. This perspective is useful with the additional geometric definition of the dot product.

  - Especially when the right side of the equations is all zeros

### Homogeneous Systems

$$
B: \quad \begin{matrix} 
x+2y-2z &= 0 \\ 
2x+y-5zz &= 0 \\ 
x-4y+z &= 0\end{matrix} 
\quad \Longleftrightarrow \quad
\begin{bmatrix}
1 & 2 & -2\\
2 & 1 & -5 \\
1 & -4 & 1
\end{bmatrix}
\begin{bmatrix} x \\ y \\ x \end{bmatrix} =
\begin{bmatrix} 0 \\ 0 \\ 0 \end{bmatrix}
$$

- This relates to whether the column of vectors of the coefficient matrix are **linearly independent**
- Let $\vec{r}_1, \vec{r}_3, \vec{r}_3$ be the rows of the coefficient matrix for $B$, *what vectors are orthogonal to them*

> ##### Find all vectors orthogonal to $\vec{a}=\begin{bmatrix} 1 \\ 1 \\ 1 \end{bmatrix}$ and $\vec{b}=\begin{bmatrix} 1 \\ 2 \\ 1 \end{bmatrix}$ 
>
> To find all vectors orthogonal to $\vec{a}$ and $\vec{b}$ we need to find vectors $\vec{x}$ satisfying $\vec{a} \cdot \vec{x}=0$ , $\vec{a} \cdot \vec{x}=0$. This is equivalent to solving the matrix equation
> $$
> \begin{bmatrix} \vec{a} \\ \hline \vec{b} \end{bmatrix} \vec{u} =
> \begin{bmatrix} \vec{a} \cdot \vec{x} \\ \vec{b} \cdot \vec{x} \end{bmatrix} =
> \begin{bmatrix} 1 & 1 & 1 \\ 1 & 2 & 1 \end{bmatrix} 
> \begin{bmatrix} x \\ y \\ x \end{bmatrix} =
> \begin{bmatrix} 0 \\ 0 \end{bmatrix}
> $$
> By row reducing $A$, we get
> $$
> \text{rref} (A) = \begin{bmatrix} 1 & 0 & 1 \\ 0 & 1 & 0 \end{bmatrix}
> $$
> And so the complete solution expressed in vector form is 
> $$
> \vec{x} = t\begin{bmatrix} 1 \\ 0 \\ 1 \end{bmatrix}
> $$

> ##### Let $\mathcal{Q}$ be the hyperplane specified in vector form by $\vec{x} = t \begin{bmatrix}1 \\ 1 \\ -1 \\ 1 \end{bmatrix} + s \begin{bmatrix}0 \\ 1 \\ 0\\1 \end{bmatrix} + r \begin{bmatrix} 2 \\ 0 \\ 0\\0 \end{bmatrix} + \begin{bmatrix} 1 \\ 2 \\ 3 \\4 \end{bmatrix}$, find a normal vector for $\mathcal{Q}$ and write $\mathcal{Q}$ in normal form
>
> Like the above example, since normal vectors for $\mathcal{Q}$ need to be orthogonal to 
> $\vec{d}_1 = \begin{bmatrix}1 \\ 1 \\ -1 \\ 1 \end{bmatrix}$, $\vec{d}_2 = \begin{bmatrix}0 \\ 1 \\ 0 \\ 1 \end{bmatrix}$, $\vec{d}_3 = \begin{bmatrix}2 \\ 0 \\ 0 \\ 0 \end{bmatrix}$, find the normal vectors by solving
> $$
> \begin{bmatrix}
> 1 & 1 & -1 & 1\\
> 0 & 1 & 0 & 1\\
> 2 & 0 & 0 & 0
> \end{bmatrix}
> \begin{bmatrix} x \\ y \\ x \\w \end{bmatrix} =
> \begin{bmatrix} 0 \\ 0 \\ 0 \end{bmatrix}
> $$
> By row reducing $A$, we get
> $$
> \text{rref} (A) =
> \begin{bmatrix}
> 1 & 0 & 0 & 0\\
> 0 & 1 & 0 & 1\\
> 0 & 0 & 1 & 0
> \end{bmatrix}
> $$
> And so we get that the complete solution expressed in vector form is 
> $$
> \vec{x} = t\begin{bmatrix} 0 \\ -1 \\ 0 \\1 \end{bmatrix}
> $$