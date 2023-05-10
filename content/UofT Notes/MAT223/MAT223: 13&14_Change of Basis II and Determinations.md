---
title: "MAT223: 13&14_Change of Basis II and Determinations"
tags: [Note]
date: [2021-01-31]
---

## Change of Basis II

- <u>Change of Basis matrix</u> - Let $\mathcal{A}, \mathcal{B}$ be basis for $\R^n$. The matrix $M$ is called a *change of basis* matrix (which converts from $\mathcal{A}$ to $\mathcal{B}$) if for all $\vec{x} \in \R^n$
    $$
    M \left[ \vec{x} \right]_\mathcal{A} = \left[ \vec{x} \right]_\mathcal{B}
    $$
    Notationally, $[\mathcal{B} \gets \mathcal{A}]$ stands for the change of basis matrix converting from $\mathcal{A}$ to $\mathcal{B}$. Write $M = [\mathcal{B} \gets \mathcal{A}]$
    
    <img src="https://tva1.sinaimg.cn/large/008eGmZEly1gpij24mr1vj30fg06mdg8.jpg" alt="Screen Shot 2021-04-13 at 11.19.53" style="zoom:50%;" />
    
- An $n \times n$ matrix's invertible if and only if it is a change of basis matrix
    - let $M^{-1} = [\mathcal{A} \gets \mathcal{B}]$
        $$
        M^{-1}M = [\mathcal{A} \gets \mathcal{B}][\mathcal{B} \gets \mathcal{A}] = [\mathcal{A} \gets \mathcal{A}] = I \\
        MM^{-1} = [\mathcal{B} \gets \mathcal{A}][\mathcal{A} \gets \mathcal{B}] = [\mathcal{B} \gets \mathcal{B}] = I 
        $$
        

### Transformation and Bases

- <u>Linear transformation in basis</u> - Let $\mathcal{T}: \R^{n} \to \R^{n}$ be a linear transformation and let $\mathcal{B}$ be a basis for $\R^n$. The *matrix for $\mathcal{T}$ wiht respect to $\mathcal{B}$*, notated $[\mathcal{T}]_\mathcal{B}$ is the $n \times n$ matrix satisfying
    $$
    \left[ \mathcal{T}\vec{x} \right]\mathcal{B} = \left[ \mathcal{T} \right]_\mathcal{B} \left[ \vec{x} \right]_\mathcal{B}
    $$
In this case, say matrix $[\mathcal{T}]_\mathcal{B}$ is the representation of $\mathcal{T}$ in the $\mathcal{B}$ basis.


### Similar Matrices

- <u>Similar Matrices</u> - the matrices $A$ and $B$ are called *similar matrices*, denoted $A \sim B$, if $A$ and $B$ represent the same linear transformation but in **possibly different basis**. Equivalently, $A \sim B$ if there is an invertible matrix $X$ so that 
    $$
    A = XBX^{-1}
    $$

## Determinants

- <u>Determinant</u> - the number (which is associated with a linear transformation with the same domain and codomain) that tracks by how much a linear transformation changes area/volume

### Volumes

- <u>Unit $n$-cube</u> - the *unit n-cube* is the $n$-dimensional cube with sides given by the standard basis vectors and lower-left corner located at the origin. That is
  $$
  C_n = \left\{ \vec{x} \in \R^n : 
  \vec{x} = \sum_{i=1}^{n} \alpha_i \vec{e}_i \text{ for some } \alpha_1, \dots , \alpha_n \in [0, 1]
  \right\} = [0, 1]^n
  $$

  - <img src="https://tva1.sinaimg.cn/large/008eGmZEly1gpijkzcmimj30eo082t8u.jpg" alt="Screen Shot 2021-04-13 at 11.38.01" style="zoom:33%;" /> ($C_n$ always have volume 1)
  
- Let $Vol(X)$ stand for the volume of the set $X$. Given a linear transformation $\mathcal{S}: \R^{n} \to \R^{n}$, define a number 
    $$
    \text{Vol Change}(\mathcal{S}) = \frac{Vol(\mathcal{S}(C_n))}{Vol(C_n)} = 
    \frac{Vol(\mathcal{S}(C_n))}{1} = Vol(\mathcal{S}(C_n))
    $$
A priori, $\text{Vol Change}(\mathcal{S})$ only describes how $\mathcal{S}$ changes the volume of $C_n$. However, because $\mathcal{S}$ is a linear transformation, it actually describes how $\mathcal{S}$ changes the volume of any figure.
    
- Let $\mathcal{T}: \R^{n} \to \R^{n}$ be a linear transformation and let $X \subseteq \R^n$ be a subset with volume $\alpha$. Then the volume of $\mathcal{T}(X)$ is $\alpha \cdot \text{Vol Change}(\mathcal{T})$

- Suppose $\mathcal{T}: \R^{n} \to \R^{n}$ is a linear transformation, $X \subseteq \R^n$ is a subset, and the volume of $\mathcal{T}(X)$ is $\alpha$. Then for any $\vec{p} \in \R^n$, the volume of $\mathcal{T}(X + \left\{ \vec{p} \right\})$ is $\alpha$
    $$
    \mathcal{T}(X + \left\{ \vec{p} \right\}) = \mathcal{T}(X) + \mathcal{T}(\left\{ \vec{p} \right\}) = 
    \mathcal{T}(X) + \left\{ \mathcal{T}(\vec{p}) \right\}
    $$
    
- Fix $k$ and let $B_n$ be $C_n$ scaled to have side length $\frac{1}{k}$ and let $\mathcal{T}: \R^{n} \to \R^{n}$ be a linear transformation, then
    $$
    \text{Vol Change}(\mathcal{T}) = \frac{Vol(\mathcal{T}(B_n))}{Vol(\mathcal{B}_n)}
    $$
    
    <img src="https://tva1.sinaimg.cn/large/008eGmZEly1gpop0xnk7gj30xe0dumzd.jpg" alt="Screen Shot 2021-04-13 at 11.48.54" style="zoom:33%;" />
    
    The argument now gets to
    $$
    \text{Vol Change}(\mathcal{T}) = \frac{Vol(\mathcal{T}(C_n))}{Vol(C_n)} = 
    \frac{K^n Vol(\mathcal{T}(B_n))}{k^n Vol(\mathcal{B}_n)} = 
    \frac{Vol(\mathcal{T}(B_n))}{Vol(\mathcal{B}_n)}
    $$
    <img src="https://tva1.sinaimg.cn/large/008eGmZEly1gpop0wvthoj30xe0dumzd.jpg" alt="Screen Shot 2021-04-13 at 11.49.41" style="zoom:33%;" />


### The determinant

- <u>Determinant</u> - the *determinant* of a linear transformation $\mathcal{T}: \R^{n} \to \R^{n}$, denoted $det(\mathcal{T})$ or $|\mathcal{T}|$, is the **oriented volume** of the image of the unit $n$-cube. The determinant of a square matrix is the determinant of its induced transformation
- <u>Orientation Preserving Linear Transformation</u> - Let $\mathcal{T}: \R^{n} \to \R^{n}$ be a linear transformation. Say that $\mathcal{T}$ is *orientation preserving* if the ordered bassi $\left\{ \mathcal{T}(\vec{e}_1), \dots, \mathcal{T}(\vec{e}n) \right\}$ is positively orientated and say that $\mathcal{T}$ is *orientation reversing* if ordered basis $\left\{ \mathcal{T}(\vec{e}_1), \dots, \mathcal{T}(\vec{e}n) \right\}$ is not a basis of $\R^n$, then $\mathcal{T}$ is neither orientation preserving nor orientation reversing

  <img src="https://tva1.sinaimg.cn/large/008eGmZEly1gpop11hkttj30vg0jqmz8.jpg" alt="Screen Shot 2021-04-13 at 12.00.30" style="zoom:33%;" />
  
    - ==Write example here==


#### Determinants of composition

<img src="https://tva1.sinaimg.cn/large/008eGmZEly1gpop151a0uj30wo0dgq4w.jpg" alt="Screen Shot 2021-04-13 at 12.02.09" style="zoom:33%;" />

- Let $\mathcal{T}: \R^{n} \to \R^{n}$  and $\mathcal{S}: \R^{n} \to \R^{n}$ be linear transformation. Then
    $$
    \text{det}(\mathcal{S} \circ \mathcal{T}) = \text{det}(\mathcal{S}) \text{det}(\mathcal{T})
    $$
    

#### Determinants of matrices

- let $A$ and $b$ be $n \times n$ matrices, then
    $$
    \text{det}(AB) = \text{det}(A) \text{det}(B)
    $$
    
- <u>Volume Theorem I</u> - For a square matrix $M$, $det(M)$ is the oriented volume of the parallelepiped (the $n$-dimensional analog of a parallelogram) given by the column vectors
- The determinants of elementary matrices are all easy to compute and determinants of the most-used typ eof elementary matrix is 1


#### Determinants and invariability

- Let $A$ be an $n \times n$ matrix .$A$ is invertible if and only if $det(A) \neq 0$
    $$
    \text{det}(A) = \text{det}(E_1, \dots E_k) = \text{det}(E_1) \dots \text{det}(E_k)
    $$
    **elementary matrices have non-zero determinations**, so $det(A) \neq 0$


#### Determinants and transposes

- <u>Volume Theorem II</u> - The determinant of a square matrix $A$ is equal to the oriented volume of the parallelepiped by the rows of $A$

