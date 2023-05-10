# Range and Nullspace of a Linear Transformation

## Range and Nullspace of a Linear Transformation

- <u>Range</u> - the **range** (or image) of a linear transformation $T: V \to W$ is the set of vectors $T$ can output, which is
    $$
    \text{range}(T) = \left\{ \vec{y} \in W: \vec{y} = T\vec{x}~ \text{ for some }~ \vec{x} \in V \right\} 
    $$
- The range of a linear transformation is the *exact same* as the definition of the range of a function
- The range of a linear transformation is always a subspace

- <u>Rank</u> a linear transformation $T: \R^{n} \to \R^{m}$, the **rank** of $T$, denoted $\text{rank}(T)$, is the dimension of the range of $T$
  
    > - Rank 0 transformation turns all vectors into $\vec{0}$ 
    > - Rank 1 transformation turns all vectors into lines etc...

> ##### Let $\mathcal{P}$ be the plane given by $x+y + z = 0$, and let $T: \R^{3} \to \R^{3}$ be projection onto $\mathcal{P}$. Find $\text{range}(T), \text{rank}(T)$
>
> First, find $\text{range}(T)$. Since $T$ is a projection onto $\mathcal{P}$, then $\text{range}(T) \subseteq \mathcal{P}$. And $T(\vec{p}) = \vec{p}$ for all $\vec{p} \in \mathcal{P}$. Then get $\mathcal{P} \subseteq \text{range}(T)$, which implies that $\text{range}(T) = \mathcal{P}$
> Since $\mathcal{P}$ is a plane, then $\text{dim}(\mathcal{P}) = 2 = \text{dim}(\text{range}(T)) = \text{rank}(T)$


- <u>Null space (kernel)</u> - of a linear transformation $T: V \to W$ is the set of vectors that get mapped to the zero vector under $T$. That is:
    $$
    \text{null}(T) = \left\{ \vec{x} \in V: T\vec{x} = \vec{0} \right\}
    $$
- The null space of a linear transformation is always a subspace
- Akin to the rank-range connection, there is a *special* number called the ***nullity*** which specifies the dimension of the null space. 
    - <u>Nullity</u> - a linear transformation $T: \R^{n} \to \R^{m}$, the **nullity** of $T$ denoted $\text{nullity}(T)$ is the dimension of the null space of $T$
    > ##### Let $\mathcal{P}$ be the plane given by $x + y + z = 0$, and let $T: \R^{3} \to \R^{3}$ be projection onto $\mathcal{P}$. Find null$(T)$ and nullity$(T)$
    >
    > Since $T$ is a projection onto $P$, (and because $\mathcal{P}$ passes through $\vec{0}$), then every normal vector for $\mathcal{P}$ will get sent to $\vec{0}$ when $T$ is applied. And besides $\vec{0}$ itself, these are the only vectors that get sent to $\vec{0}$. Then:
    > $$
    > \text{null}(T) = \{ \text{normal vectors}~ \cup \{ \vec{0} \} \} = \text{span} \left\{ \begin{bmatrix}1 \\ 1 \\ 1\end{bmatrix} \right\}
    > $$
    > Since null$(T)$ is a line, then nullity$(T) = 1$ 

## Fundamental Subspaces of a Matrix

- Every linear transformation has a range and a null space. Then, every matrix is associated with three fundamental subspaces
- <u>Fundamental Subspaces</u> - associated with any matrix $M$ are **3 fundamental subspaces**: the **<u>row space</u>**, denoted row$(M)$, is the span of the rows of $M$; the **<u>column space</u>**, denoted col$(M)$, is the span of the columns fo $M$; and the **<u>null space</u>**, denoted null$(M)$, is the set of solutions to $M\vec{x} = \vec{0}$ 
  - The columns of $A$ corresponding to **pivot columns** of rref$(A)$ form a basis of col$(A)$
  - The **non-zero rows** of rref$(A)$ form a basis for row$(A)$
- To find a basis for the column/row space of matrix $M$
  1. Assume to pick a basis for the span $\{v_1, v_2 , \dots \}$ where $v_1, v_2$ are columns/row of the matrix $M$
  2. Row reduce $M$ to get tis row-reducing-echelon-form
  3. Pick the pivot columns which are the original vectors form a *maximal linearly independent subset* (the independent vectors in this span) as the vectors in the span of column space $M$

> ##### Find the null space of $M = \begin{bmatrix} 1 & 2 & 5 \\ 2 & -2 & -2 \end{bmatrix}$
>
> Need to solve the homogeneous matrix equation of $M\vec{x} = \vec{0}$, first row reduce
> $$
> \text{rref} (M) =
> \begin{bmatrix} 1 & 0 & 1 \\ 0 & 1 & 2 \end{bmatrix}
> $$
> See that the $z$ column is a free variable column (let $t$ reps $z$)
> $$
> \begin{bmatrix} 1 & 0 & 1 \\ 0 & 1 & 2 \end{bmatrix} 
> \begin{bmatrix} x \\ y \\z \end{bmatrix} = 0 \\
> 
> \left\{\begin{matrix} x + z = 0 \\ y + 2z = 0\end{matrix}\right.
> 
> \quad \Rightarrow \quad 
> \left\{\begin{matrix} x = -z = -t \\ y = -2z = -2t\end{matrix}\right.
> $$
> Therefore the complete solution in vector form:
> $$
> \text{null} (M) = \text{span}
> \left\{ \begin{bmatrix} -1 \\ -2 \\1 \end{bmatrix} \right \}
> $$
>
> ##### For the same $M$ above, find a basis for the row space and the columns of $M$
>
> For column space: row reduce columns of $M$ and find its independent subsets
> $$
> \text{rrerf} \left(\begin{bmatrix} 1 & 2 & 5 \\ 2 & -2 & -2 \end{bmatrix}  \right)
> = \begin{bmatrix} 1 & 0 & 1 \\ 0 & 1 & 2 \end{bmatrix}
> $$
> $\therefore$  The first 2 columns are linearly independent, thus 
> $$
> \text{col}(M) = \text{span} 
> \left\{\begin{bmatrix} 1 \\2 \end{bmatrix}, 
> \begin{bmatrix} 2 \\-2 \end{bmatrix} \right\} = \R^2 
> \quad\text{and a basis is } \quad
> \left\{\begin{bmatrix} 1 \\2 \end{bmatrix}, 
> \begin{bmatrix} 2 \\-2 \end{bmatrix} \right\}
> $$
> For the row space: row reduce the rows of $M$ and find its independent subsets
> $$
> \text{rrerf} 
> \left(\begin{bmatrix} 1 & 2 \\ 2 & -2 \\5 & -2 \end{bmatrix}  \right)
> = \begin{bmatrix} 1 & 0 \\ 0 & 1 \\0 & 0 \end{bmatrix}
> $$
> $\therefore$ This span is already linearly independent, thus
> $$
> \text{row}(M) = \text{span} 
> \left\{\begin{bmatrix} 1 \\2 \\5 \end{bmatrix}, 
> \begin{bmatrix} 2 \\-2 \\-2 \end{bmatrix} \right\}
> \quad\text{and a basis is } \quad
> \left\{\begin{bmatrix} 1 \\2 \\5 \end{bmatrix}, 
> \begin{bmatrix} 2 \\-2 \\-2 \end{bmatrix} \right\}
> $$

### Transpose

- <u>Transpose</u>, notated $M^T$ is a matrix where the rows and columns of $M$ are swapped
  $$
  M = 
  \begin{bmatrix}
      a_{11} & a_{12} & a_{13}  & \dots  & a_{1m} \\
      a_{21} & a_{22} & a_{23}  & \dots  & a_{2m} \\
      \vdots & \vdots & \vdots  & \ddots & \vdots \\
      a_{n1} & a_{n2} & a_{n3}  & \dots  & a_{nm}
  \end{bmatrix}
  \quad \quad \quad
  M^T = 
  \begin{bmatrix}
      a_{11} & a_{21}  & \dots  & a_{n1} \\
      a_{12} & a_{22}  & \dots  & a_{n2} \\
      a_{13} & a_{23}  & \dots  & a_{n3} \\
      \vdots & \vdots  & \ddots & \vdots \\
      a_{1m} & a_{2m}  & \dots  & a_{nm}
  \end{bmatrix}
  $$
  
- For a matrix $A$, the **dimension of the row space equals the dimension of the column space**
  $$
  \text{col}(M) = \text{row} (M^T) \quad \text{and} \quad
  \text{row}(M) = \text{col} (M^T)
  $$
  Every pivot of rref$(A)$ *lies in exactly one row and one column.* Thus the number of basis vectors in row$(A)$ is the same as the number of basis vectors in col$(A)$ 

## Equations, Null Space, and Geometry

- Let $A$ be a matrix, $\vec{b}$ be a vector, and let $\vec{p}$ be a particular solution to $A\vec{x} = \vec{b}$. Then the set of all solutions to $A\vec{x} = \vec{b}$ is 
  $$
  \text{null}(A) + \{\vec{p} \}
  $$
  To right a complete solutions to $A\vec{x} = \vec{b}$, need ① nullspace of $A$  ② particular solution to $A\vec{x} = \vec{b}$

- Let $M$ be a matrix and let $\vec{r}_1, \dots, \vec{r}_n$ be the rows of $M$. Then the solutions to $M\vec{x} = \vec{0}$ is precisely the vectors which are **orthogonal to every row** ($\vec{r}$) of $M$. 

  - null$(M)$ consists of all vectors orthogonal to the rows of $M$
  - row$(M)$ consists of all vectors orthogonal to everything in null$(M)$ 

  > ##### Let $\vec{a} = \begin{bmatrix} 1 \\ 2 \\5 \end{bmatrix}$, and $\vec{b} = \begin{bmatrix} 2 \\ -2 \\-2 \end{bmatrix}$. Find all vectors orthogonal to both of them
  >
  > Let $M = \begin{bmatrix} 1 & 2 & 5 \\ 2 & -2 & -2 \end{bmatrix}$  be the matrix whose rows are $\vec{a}, \vec{b}$. Then, calculate null$(M)$ to get all vectors orthogonal to row$(M)$. Thus the solution is:
  > $$
  > \text{null} (M) = \text{span}
  > \left\{ \begin{bmatrix} -1 \\ -2 \\1 \end{bmatrix} \right \}
  > $$

## Transformations and Matrices

- <u>Induced Transformations</u> - Let $M$ be an $n \times m$ matrix. $M$ **induces** a linearly transformation $\mathcal{T}_M: \R^m \to \R^n$ defined by
  $$
  [\mathcal{T}_M \vec{v}]_\mathcal{E'} = M [\vec{v}]_\mathcal{E}
  $$
  
  Where $\mathcal{E}$ is the standard bassi for $R^m$ and $\mathcal{E'}$ is the standard basis for $\R^n$
  
  > ##### Let $\mathcal{T}$ be the transformation induced by the matrix $M = \begin{bmatrix} 1 & 2 & 5 \\ 2 & -2 & -2 \end{bmatrix}$, and let $\vec{v} = 3 \vec{e}_1 - 3\vec{e}_3$. Computer $\mathcal{T} (\vec{v})$
  >
  > Using the definition fo induced transformations:
  > $$
  > [\mathcal{T}_M \vec{v}]_\mathcal{E'} = M [\vec{v}]_\mathcal{E} =
  > \begin{bmatrix} 1 & 2 & 5 \\ 2 & -2 & -2 \end{bmatrix}
  > [\vec{v}]_\mathcal{E}
  > $$
  > The equation of $\vec{v}$ is given, calculate and substitute the values of $[\vec{v}]_\mathcal{E}$
  > $$
  > [\mathcal{T}_M \vec{v}]_\mathcal{E'} 
  > \begin{bmatrix} 1 & 2 & 5 \\ 2 & -2 & -2 \end{bmatrix}
  > \begin{bmatrix} 3 \\ 0 \\-3 \end{bmatrix}
  > = \begin{bmatrix} -12 \\12 \end{bmatrix}
  > $$
  > In other words $

- <u>Rank of a matrix</u> - let $M$ be a matrix, the **rank** of $M$, denoted rank$(M)$, is the rank of the linear transformation ***induced*** by $M$
- <u>Nullity of a matrix</u> - let $M$ be a matrix, the **nullity** of $M$, denoted nullity$(M)$, is the nullity of the linear transformation ***induced*** by $M$

## Range vs Column Space & Null Space vs. Null Space

- Let $M$ be a matrix and $\mathcal{T}$ a transformation. The column space of $M$ is the set of all linear combinations of the columns of $M$. **However, the columns of $M$ are numbers, not vectors**, so need to turn them into vectors first
  $$
  \text{col}(M) = \text{span} 
  \{[C_1]_\mathcal{E}, [C_2]_\mathcal{E}, \dots, [C_m]_\mathcal{E}, \}
  $$
  This gets $M[\vec{e}_i] = C_i$ by the definition of induced transformation, know
  $$
  [\mathcal{T}(\vec{e}_i)]_\mathcal{E} = M[\vec{e}_i]_\mathcal{E} = C_i
  \quad \Rightarrow \quad
  \mathcal{T}(\vec{e}_i) = [C_i]_\mathcal{E}
  $$
  Every **input** of $\mathcal{T}$ can be written as a linear combination of $\vec{e}_i$ (because $\mathcal{E}$ is a basis) and therefore, since $\mathcal{T}$ is linear, every **output** can be written as linear combinations of $[C_i]_\mathcal{E}$ Thus
  $$
  \text{range}(T) = \text{col}(M)
  $$

  > ##### Let $\mathcal{T}: \R^3 \to \R^2$ be defined by $\mathcal{T}\begin{bmatrix} x \\ y \\z \end{bmatrix} = \begin{bmatrix} 2x-z \\ 4x-2z \end{bmatrix}$. Find the range and rank of $\mathcal{T}$
  >
  > Let $M$ be a matrix for $\mathcal{T}$. And $M = \begin{bmatrix} 1 & 0 & -1 \\ 4 & 0 & -2 \end{bmatrix}$. From definitions, know:
  >
  > - $\text{range}(T) = \text{col}(M)$ 
  > - $\text{rank}(T) = \text{dim}(\text{range}(T)) = \text{dim}(\text{col}(M))$ 
  >
  > See that $\left\{\begin{bmatrix} 2\\4 \end{bmatrix} \right\}$ is a basis for col$(M)$ and its one diminutional then:
  > $$
  > \text{range}(\mathcal{T}) = \text{span} 
  > \left\{\begin{bmatrix} 2\\4 \end{bmatrix} \right\}
  > \quad \text{and} \quad 
  > \text{rank}(\mathcal{T}) = 1
  > $$

- Let $M$ be a matrix, the **rank** of $M$ is equal to the **number of pivots in rref**$(M)$
- Let $\mathcal{T}$ be a linear transformation and let $M$ be a matrix for $\mathcal{T}$. Then **nullity**$(T)$ is equal to the **number of free variable columns in rref$(M)$** 
- For a matrix $A$, $\text{rank}(A) = \text{rank}(A^T)$ 

## Rank-Nullity Theorem

- Define a matrix $A$
  $$
  \text{rank}(A) + \text{nullity}(A) = \text{# of columns in}A
  $$

  - Rank is the number of *pivots* of $A$ and Nullity is the number of *non-pivots* of $A$
  
- Define a transformation $\mathcal{T}$ 
  $$
  \text{rank}(\mathcal{T}) + \text{nullity}(\mathcal{T}) = 
  \text{dim}(\text{domain of }\mathcal{T})
  $$

> ##### Let $\mathcal{P} \subseteq \R^4$ be a plane in $\R^4$ given in vector form by $\vec{x} = t \begin{bmatrix} 1 \\ 2 \\2 \\2 \end{bmatrix} + s \begin{bmatrix} -1 \\1 \\-1 \\1 \end{bmatrix}$ How many normal vectors does $\mathcal{P}$ have
>
> The matrix $A = \begin{bmatrix} 1 & 2 & 2 & 2 \\ -1 & 1 & -1 & 1 \end{bmatrix}$ is rank 2, and so has nullity 2
>
> Therefore there exist  linear independent normal directions for $\mathcal{P}$

