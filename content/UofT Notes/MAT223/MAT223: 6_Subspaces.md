---
title: "MAT223: 6_Subspaces"
tags: [Note]
date: [2021-01-31]
---

# Subspaces and Bases

## Subspace

- A subspace is a smaller set within a vector space. It is similar to the set contains its subset. In other words, **subspace is the non-empty subset of a vector space**.

- A non-empty subset $V \subseteq \R^n$ is called a **<u>subspace</u>** if for all $\vec{u}, \vec{v} \in V$ and all scalars $k$:

  $\vec{u} + \vec{v} \in \mathcal{V} \quad \and \quad k\vec{u} \in \mathcal{V}$ 

- Subspaces generalize the idea of *flat* spaces **through the origin**, include lines, planes, volume...
  
  - A translated span cannot be represented as a subspace because it does not pass through the origin
- **Every subspace is a span** and every span is a subspace. $\mathcal{V} \subseteq \R^n$ Is a subspace if and only if $\mathcal{V} = \text{span}~ \mathcal{X}$ for some set $\mathcal{X}$.
  - Spans and subspaces are two different ways of talking about the same objects (points, lines, planes etc.) through the origin
  - **An empty set has a span defined by the zero vector**: 
    $\mathcal{X} \neq \{\}$, implies $\mathcal{V}$ is non-empty because $\mathcal{X} \subseteq \mathcal{V}$ and $\mathcal{X} = \{\}$ then $\mathcal{V} = \{\vec{0}\}$ is still non-empty

> In my understanding if V' = spanV, it means that the set V' would contains more elements than V itself. (Ex. V contains [1,1], spanV would contain [5,5],[0.5,0,5]... and also [1,1] as well] Therefore taking a span of the set would only enlarge the number of the vectors in the set. 

> ##### Let $\mathcal{V} \subseteq \R^2$ be the complete solution to $x + 2y =0$. Show that $\mathcal{V}$ is a subspace
>
> Let $\vec{u} = \begin{bmatrix} u_1 \\ u_2 \end{bmatrix}$ and $\vec{v} = \begin{bmatrix} v_1 \\ v_2 \end{bmatrix}$ be in $\mathcal{V}$, and let $k$ be a scaler. By definite, get:
> $$
> u_1 + 2u_2 = 0 \\
> v_1 + 2v_2 =0
> $$
> WTS: $\mathcal{V}$ is nonempty and that $\vec{u} + \vec{v} \in \mathcal{V} ~ \and~ k\vec{u} \in \mathcal{V}$ :
>
> First, $\vec{u} + \vec{v} = \begin{bmatrix} u_1 + v_1 \\ u_2 + v_2 \end{bmatrix}$, and the coordinates satisfy $(u_1 + v_1) + 2(u_2 + v_2) = 0 + 0 = 0$. Since $\vec{u} + \vec{v}$ satisfies the equation, therefore have shown that $\vec{u} + \vec{v} \in \mathcal{V}$ 
>
> Then, $k\vec{u} = \begin{bmatrix} ku_1 \\ ku_2 \end{bmatrix}$ and the coordinates satisfy $(ku_1) + 2(ku_2) = k0 = 0$ , show have shown that  $k\vec{u} \in \mathcal{V}$. 
>
> Since $\vec{0} = \begin{bmatrix} 0 \\ 0 \end{bmatrix}$ satisfies the equation as well. Then $\vec{0} \in \mathcal{V}$ so $\mathcal{V}$ is nonempty
>
> Thus, by definition, have shown that $\mathcal{V}$ is a subspace

- <u>Trivial subspace</u>: the subset $\{\vec{0} \} \subseteq \R^n$ is a subspace
  - T**he trivial subspace would be a subset consisting only the zero vector**. However the trivial subspace $\{ \vec{0} \}$ is different with the span$\{ \vec{0} \}$. From the previous definitions: span {} = ,span$\{ \vec{0} \}$ But the trivial subspace is not equal to the subspace of an empty set.

## Bases and Dimensions

- <u>Bases</u> - a basis for a subspace $\mathcal{V}$ is a **linearly independent set** of vectors, $\mathcal{B}$ so that $\text{span} \mathcal{B} = \mathcal{V}$ 

  1. Basis are **not unique**. Every subspace (except the trivial subspace) has multiple bases
  2. Given a basis for a subspace, every vector in the subspace can be written as a *unique* linear combination of vectors in that basis
  3. Any two bases for the same subspace have the same number of elements

  > In other words, for every non-zero subspace, it is possible to find any linearly independent vectors in the span as representations of its bases. However, different representation of the basis would be linearly dependent.

- <u>Dimension</u> - the dimension of a subspace $V$ is the number of elements in the basis of $V$ 

  - Tells the **maximum number of linearly independent vectors** that can exist in $V$
  - The dimension fo the single point is 0 (A 0 dimensional point has no extendable x or y axis. Therefore it only shows the position of a point, there is no other possible extension of it)

  > **Here the definition of "dimension" is conflict-able with the day-to-day usage of the word "dimension" it in the past.** Normally, the word "dimension" is used similarly with the concept of $\R^n$ space, while starting at this point, this non-rigorous definition is no longer valid in MAT223. Although the set A is in the $\R^4$ space (a vector containing 4 elements), but it is defined as two dimensional (by the definition: the dimension of a subspace V is the number of elements in a basis for V). Therefore needs to be extra cautious about this new interpretation of dimension starting from here. 

> ##### Let $A=\{(x_1, x_2, x_3, x_4) : x_1+2x_2 - x_3 = 0\}$ and $x_1+6x_4=0$, find a basis for and the dimension of $A$
>
> $A$ Is the complete solution to the system
> $$
> \left\{\begin{matrix} 
> x_1 & +2x_2 -x_3 & &= 0 \\ 
> x_1 & & +6x_4 &= 0  \end{matrix}\right.
> $$
> Which can be expressed in vector form as
> $$
> \begin{bmatrix} x_1 \\ x_2 \\x_3 \\ x_4 \end{bmatrix} =
> t\begin{bmatrix} 0 \\ 1/2 \\1 \\0 \end{bmatrix} 
> +s\begin{bmatrix} -6\\ 3 \\0 \\1 \end{bmatrix}
> $$
> Therefore $A=\text{span} \left\{ \begin{bmatrix} 0 \\ 1/2 \\1 \\0 \end{bmatrix} 
> +\begin{bmatrix} -6\\ 3 \\0 \\1 \end{bmatrix} \right \}$ , since this is a linearly indecent set, with 2 elements, then $A$ is two dimensional.

### Standard Basis

- The <u>standard basis</u> for $\R^n$ is the set $\{\vec{e}_1, \dots, \vec{e}_n \}$ where
  $$
  \vec{e}_1 = \begin{bmatrix} 1 \\ 0 \\0 \\ \vdots \end{bmatrix}, \quad 
  \vec{e}_2 = \begin{bmatrix} 0 \\ 1 \\0 \\ \vdots \end{bmatrix}, \quad
  \vec{e}_3 = \begin{bmatrix} 0 \\ 0 \\1 \\ \vdots \end{bmatrix}, \quad
  \dots
  $$

  - The notation $\vec{e}_1$ is **context specific**, if $\vec{e}_i \in \R^2$ then $\vec{e}_i$ must have exactly two coordinates, if $\vec{e}_1 \in \R^{25}$ then $\vec{e}_i$ must have exactly 25 coordinates

---

- First This plane is a **translated plane**. In order for a subspace to have a basis. 



By definition, a basis is a linearly independent subspace. In the definition of subspace, the vector space *must contain the zero vector.* In this case, this plane is a translated plane, which does not contain the zero vector. In order words, t**his plane does not have a straight forward basis.** 

To calculate the "basis" of this plane, and additional set containing its transforming vector is needed. Therefore the "basis" of this plane would be:
$$
B = \left\{\vec{a}, \vec{b} \right\} + \{\vec{c} \}
$$


Finn is correct about the linearly dependency property of the basis, and Darlene is right about the dimension of the basis. However, they both ignored the fact that this plane is a translated plane. It does not form a subspace, thus, does not have a basis.