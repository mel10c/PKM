# Eigenvalues, Eigenvectors and Diagonalization

## Eigenvalues and Eigenvectors

- <u>Eigenvector</u> - Let $X$ be a linear transformation or a matrix. An *eigenvector* for $X$ is a non-zero vector that doesn't change the directions when $X$ is applied. That is $\vec{v} \neq \vec{0}$ is an eigenvector for $X$:
    $$
    X \vec{v} = \lambda \vec{v}
    $$
- <u>Eigenvalue</u> - is a scaler $\lambda$, of $X$ corresponding to the eigenvector $\vec{v}$


### Finding Eigenvectors

- Let $M$ be a square matrix. The vector $\vec{v} \neq \vec{0}$ is an eigenvector for $M$ if and only if there exist a scaler $\lambda$ so that
    $$
    M \vec{v} = \lambda \vec{v} \quad \Rightarrow \quad
    M \vec{v} - \lambda \vec{v} = (M - \lambda I)\vec{v} = \vec{0}
    $$
    Now have that $\vec{v}  \neq \vec{0}$ is an eigenvector for $M$ if and only if 
    $$
    E_{\lambda} \vec{v} = (M - \lambda I) \vec{v} = M \vec{v} - \lambda \vec{v} = \vec{0}\_,
    $$

## Characteristics Polynomial

- <u>Characteristic Polynomial</u> - for a matrix $A$, the *characteristic polynomial* of $A$ is
    $$
    \text{char}(A) = \text{dec}(A - \lambda I)
    $$
- For an $n \times n$ matrix $A$, $char(A)$ has some nice properties
    - $char(A)$ is a polynomial 
    - $char(A)$ has degree $n$
    - The coefficient of the $\lambda^n$ term in $char(A)$ is $\pm 1$; $+ 1$ if $n$ is even and $-1$ if $n$ is odd
    - $char(A)$ evaluated at $\lambda = 0$ is $det(A)$
    - The roots of $char(A)$ are precisely the eigenvalues of $A$


### Transformations without eigenvectors

- If $A$ is a square matrix, then $A$ always has an eigenvalue provided complex eigenvalues are permitted.


## Diagonalization

- <u>Diagonalization</u> - a matrix is *diagonalizable* if it is similar to a diagonal matrix
- A linear transformation $\mathcal{T}: \R^{n} \to \R^{n}$ can be represented by a diagonal matrix if and only if there exists a basis for $\R^n$ consisting of eigenvectors for $\mathcal{T}$. If $\mathcal{B}$ is such a basis, then $[\mathcal{T}]_\mathcal{B}$ is a diagonal matrix


### Non-diagonalizable matrices

- Not every matrices are diagonalizable, but can check if an $n \times n$ matrix is diagonalizable by determining whiter there is a basis of eigenvectors for $\R^n$
    - If a matrix $A$ does not have real roots for $char(A)$, then it has no real eigenvalues, so not diagonalizable
    - If a matrix $J$ has eigenvectors that is not contain the its domain, then $J$ is not diagonalizable 


## Geometric and Algebraic Multiplicities

- <u>Eigenspace</u> - Let $A$ be a $n \times n$ matrix with eigenvalues $\lambda_1, \dots,  \lambda_m$. The *eigenspace* of $A$ corresponding to he eigenvalues of $\lambda_i$ is the **null space** of $A - \lambda_i I$. That si the space spanned by all eigenvectors that have the eigenvalues $\lambda_i$
    - The <u>geometric multiplicity</u> of eigenvalues $\lambda_i$ is the dimension of the corresponding eigenspace. 
    - The <u>algebraic multiplicity</u> of $\lambda_i$ is the number of times $\lambda_i$ occurs as a root of the characteristic polynomial of $A$ 

    > ##### Let $D = \begin{bmatrix}5 & 0 \\ 0 & 5\end{bmatrix}$ and find the geometric and algebraic multiplicity of each eigenvalues of $D$
    > Computing, $char(D) = (5-\lambda)^2$, so 5 is an eigenvalue of $D$ with algebraic multiplicity of 2. The eigenspace of $D$ corresponding to 5 is $\R^2$. Thus, the geometric multiplicity of 5 is 2
    > ##### Let $J = \begin{bmatrix}5 & 1 \\ 0 & 2\end{bmatrix}$ and find the geometric and albegraic multiplicity of each eigenvalues of $J$
    > Computing $char(J) = (5-\lambda)(2-\lambda)$, so 5 and 2 are eigenvalues of $j$, both with algebraic multiplicity of 1. The eigenspace of $j$ corresponding to 5 is $span\left\{ \begin{bmatrix}1 \\ 0\end{bmatrix} \right\}$ and the eigenspace corresponding to 2 is $span\left\{ \begin{bmatrix}-1 \\ 3\end{bmatrix} \right\}$. Thus both 5 and 2 has a geometric multiplicity of 1.


- **<u>Fundamental Theorem of Allegra</u>** - Let $p$ be a polynomial of degree $n$. Then if complex roots are allowed, the sum of multiplicities of the roots of $p$ is $n$
- Let $\lambda$ be an eigenvalues of the matrix $A$. Then 
    $$
    \text{geometric mult}(\lambda) \le \text{algebraic multi }(\lambda)
    $$
    - An $n \times n$ matrix $A$ is diagonalizable if and only if the sum of its geometric multiplicities is equal to $n$. Further, provided complex eigenvalues are permitted, $A$ is diagonalizable if and only if all its geometric multiplicities equal its algebraic multiplicities.
