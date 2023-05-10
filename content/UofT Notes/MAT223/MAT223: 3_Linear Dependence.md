# Spans, Translated Spans, and Linear Independence/Dependence

## Span defintion

- <u>Span</u> - the **span** of a set of vectors $V$ is the **set of all linear combinations** of vectors in $V$.
  $$
  \text{span}V = \{\vec{v}: \vec{v} = \alpha_1 \vec{v}_1 + \alpha_2 \vec{v}_2 
  ~...~ + \alpha_n \vec{v}_n 
  ~\text{for some}~ \alpha_1, \alpha_2,~...~, \alpha_n \in \R
  \}
  $$

  - span$\{\} = \{\vec{0} \}$

  > ##### Let $\vec{a}=\begin{bmatrix} 1 \\ 2 \\ 1 \end{bmatrix}, \vec{b}=\begin{bmatrix} 0 \\ 1 \\ 0 \end{bmatrix}, \vec{c}=\begin{bmatrix} 1 \\ 1 \\ 2 \end{bmatrix}$. Show that $\R^3=$ span$\{\vec{a},\vec{b},\vec{c}\}$
  >
  > If the equation of these 3 vectors is always **consistent**, then any vector in $\R^3$ can be obtained as a linear combination of $\vec{a},\vec{b},\vec{c}$.
  > $$
  > \vec{x}=\begin{bmatrix} x \\ y \\ x \end{bmatrix} =
  > \alpha_1 \begin{bmatrix} 1 \\ 2 \\ 1 \end{bmatrix} +
  > \alpha_2 \begin{bmatrix} 0 \\ 1 \\ 0 \end{bmatrix} +
  > \alpha_3 \begin{bmatrix} 1 \\ 1 \\ 2 \end{bmatrix} =
  > \alpha_1 \vec{a} + \alpha_2 \vec{b} + \alpha_3 \vec{c}
  > $$
  > Get the system and solve it
  > $$
  > \begin{bmatrix}
  > \alpha_1 & 0 & \alpha_3 & x\\
  > 2\alpha_1 & \alpha_2 & \alpha_3 & y\\
  > \alpha_1 & 0 & 2\alpha_3 & z
  > \end{bmatrix} 
  > \quad \Rightarrow \quad
  > \left\{\begin{matrix} 
  > & 2x ~~~~-~~~~ z &= \alpha_1 \\ 
  > & -3x+y+z &= \alpha_2 \\ 
  > & -x ~~~~+~~~~ z &= \alpha_3  \end{matrix}\right.
  > $$
  > It, always have a solution (no matter the values of $x, y, z$). Therefore, span$\{\vec{a},\vec{b},\vec{c}\} = \R^3$

- Lines and planes that **passes through the origin** can be expressed as spans ($\vec{p} = \vec{0}$)

  - Lines
    $$
    \ell = \{\vec{x} \mid \vec{x} = t\vec{d} + \vec{0}~~ \text{for some}~ t \in \R \}
    = \text{span}\{\vec{d}\}
    $$
  
- Planes
    $$
    \mathcal{P} = \{\vec{x} \mid \vec{x} = t\vec{d}_1 + s\vec{d}_2 + \vec{0}~ 
    \text{for some}~ t,s \in \R \}
    = \text{span}\{\vec{d}_1, \vec{d}_2 \}
    $$

### Sets Addition

- If $A$ and $B$ are sets of vectors, then the <u>set sum</u> of $A$ and $B$ denoted $A+B$ is
  $$
  A + B = \{\vec{x}: \vec{x} = \vec{a} + \vec{b}~~ \text{for some}~ 
  a \in A ~~\text{and}~~ b \in B \}
  $$

  > ##### Let $C = \{\vec{x} \in \R^2: \left\| x \right\| \}$, $Y = \{C + \{3\vec{e}_1, \vec{e}_2 \} \}$
  >
  > $$
  > Y= \{\vec{x} + \vec{v}: \left\| x \right\|=1
  > ~~\text{and}~~ \vec{v} = 3\vec{e}_1, ~~\text{or}~~ \vec{v} = \vec{e}_2 \}
  > $$
  >
  > In another words, $Y$ is the union of two translated copies of $C$
  > $$
  > Y=(C+\{\vec{e}_1 \}) \cup (C+\{\vec{e}_2\})
  > $$

### Span Transformation

- Every point in $\ell_2$ can be obtained by adding $\vec{p}$ to corresponding point in $\ell_1$:    $\ell_2 = \ell_1 + \{\vec{p}\}$
  - Do not write $\ell_2 = \ell_1 + \vec{p}$ because $\ell_1$ is a set while $\vec{p}$ is a single vector

## Linear Independence & Linear dependence

- <u>Redundant vector</u> - not *needed* for the span (can be removed without changing the span)

- When writing an object in vector form, the directional vectors must always be **linearly independent**

- Geometric defintion

  - <u>**Linearly Independent**</u> for vectors $\vec{v}_1, \vec{v}_2 ... \vec{v}_n$ 

  $$
  \forall~ i \in \{1, 2,~ ...~ n\}, \quad
  \vec{v}_i \notin ~\text{span}~ \{\vec{v}_1, \vec{v}_2, ..., \vec{v}_n \}
  $$

  - <u>**Linearly Dependent**</u> for vectors $\vec{v}_1, \vec{v}_2 ... \vec{v}_n$ 
    $$
    \exists i \in \{1, 2,~ ...~ n\}~~ \text{s.t.}~~
    \vec{v}_i \in ~\text{span}~ \{\vec{v}_1, \vec{v}_2, ..., 
    \vec{v}_{i-1}, \vec{v}_{i+1}, ..., \vec{v}_n \}
    $$

  > ##### The planes $\mathcal{P}: \vec{x} = t\begin{bmatrix} 1 \\ 2 \\1 \end{bmatrix} +s\begin{bmatrix} 2\\ 2 \\1 \end{bmatrix}$ and $\mathcal{Q}:\vec{x} = t\begin{bmatrix} 3 \\ 4 \\2 \end{bmatrix} +s\begin{bmatrix} 2 \\ 2 \\1 \end{bmatrix} $ are given determine if they are the same plane
  >
  > Let $\vec{a}_1 = \begin{bmatrix} 1 \\ 2 \\1 \end{bmatrix}$ $\vec{a}_2 = \begin{bmatrix} 2\\ 2 \\1 \end{bmatrix}$ (from $\mathcal{P}$) and $\vec{b}_1= b\begin{bmatrix} 3 \\ 4 \\2 \end{bmatrix}$ $\vec{b}_2=\begin{bmatrix} 2 \\ 2 \\1 \end{bmatrix}$ (from $\mathcal{Q}$)
  >
  > For $\mathcal{P} = \mathcal{Q}$, all direction vector in $\mathcal{Q}$ must be linear combination of directional vectors in $\mathcal{P}$. In other words, $\{\vec{a}_1, \vec{a}_2,\vec{b}_1 \}$ and $\{\vec{a}_1, \vec{a}_2,\vec{b}_2 \}$ must all be linearly dependent sets.
  >
  > Since $\vec{a}_2 = \vec{b}_2$, so only need to verify if $\{\vec{a}_1, \vec{a}_2,\vec{b}_1 \}$ is linearly dependent. (If $\vec{b}_1$ can be written as a linear combination of $\vec{a}_1 + \vec{a}_2$)
  > $$
  > \begin{bmatrix} 3 \\ 4 \\2 \end{bmatrix} =
  > x\begin{bmatrix} 1 \\ 2 \\1 \end{bmatrix} 
  > +y\begin{bmatrix} 2\\ 2 \\1 \end{bmatrix}
  > $$
  > $\vec{b}_1 = \vec{a}_1 + \vec{a}_2$, so $\{\vec{a}_1, \vec{a}_2,\vec{b}_1 \}$ is linearly dependent. Therefore $\mathcal{P} = \mathcal{Q}$

- Algebraic Defintion

  - <u>Trivial Linear Combination</u> - The linear combination $\alpha_{1}\vec{v}_{1} + \alpha_{2}\vec{v}_{2}...+\alpha_{n}\vec{v}_{n}$ is called a **trivial** if $\alpha_1 = ... =\alpha_n = 0$, if $\exist~ \alpha_i \neq 0$, then the linear combination is called **non-trivial**
  - <u>**Linearly Independent**</u> for vectors $\vec{v}_1, \vec{v}_2 ... \vec{v}_n$ if all linear combinations are trivial
  - <u>**Linearly Dependent**</u> - vectors $\vec{v}_1, \vec{v}_2 ... \vec{v}_n$ if there is a non-trivial linear combination of $\vec{v}_1,... \vec{v}_n$ that equals the zero vector. 

  > ##### Let $\vec{u}=\begin{bmatrix} 1 \\ 2 \end{bmatrix}$, $\vec{v}=\begin{bmatrix} 2 \\ 3 \end{bmatrix}$, $\vec{w}=\begin{bmatrix} 4 \\ 5 \end{bmatrix}$. Use the algebraic definition fo linear independence to determine whether $\{\vec{u}, \vec{v},\vec{w} \}$ is linearly independent or not
  >
  > Need to determine if there is a non-trivial solution to $x\vec{u}+y\vec{v}+z\vec{w} = \vec{0}$ 
  >
  > This vector equation is equivalent to he system of equations
  > $$
  > \left\{\begin{matrix} 
  > & x+2y+4z &= 0 \\ 
  > & 2x+3y+5z &= 0  \end{matrix}\right.
  > $$
  > By substitution, $y=-3z$ and $x=2z$, let $z=t$ for $t \in \R$
  > $$
  > \begin{bmatrix} x \\ y \\z \end{bmatrix} =
  > t\begin{bmatrix} 2 \\ -3 \\1 \end{bmatrix}
  > $$
  > This is a non-trivial solution. Therefore $\vec{u}, \vec{v},\vec{w} \}$ is linearly dependent

- <u>Homogeneous</u> - system of linear equations for a vector equation in the variables in the form
  $$
  \alpha_{1}\vec{v}_{1} + \alpha_{2}\vec{v}_{2}...+\alpha_{n}\vec{v}_{n} = \vec{0}
  $$

  - Vector $\vec{v}_1,... \vec{v}_n$ are **linearly independent** iff the homogeneous equation has a unique solution

#### Proof

- (Geometric $\Rightarrow$ Algebraic) Assume $\vec{v}_1,... \vec{v}_n$ are linearly dependent by the geometric definition. This means that for some $i$, $\vec{v}_i \in ~\text{span}~ \{\vec{v}_1, ..., 
  \vec{v}_{i-1}, \vec{v}_{i+1}, ..., \vec{v}_n \}$. 

  - Fix such $i$. Then, by the definition of span:

  $$
  \begin{align*}
  \vec{v}_i &= \alpha_1\vec{v}_1 +~... +~
  \alpha_{i-1}\vec{v}_{i-1} + \vec{0} +\alpha_{i+1}\vec{v}_{i+1} +~
  ...+~ \alpha_n\vec{v}_n \\
  \vec{0} &= \alpha_1\vec{v}_1 +~ ...+~ 
  \alpha_{i-1}\vec{v}_{i-1} - \vec{v}_i + \alpha_{i+1}\vec{v}_{i+1}+~ 
  ...+~ \alpha_n\vec{v}_n
  \end{align*}
  $$

  - This must be a non-trivial linear combination because the coefficient of $\vec{v}_i$ is $-1 \neq0$, and so it is linearly dependent by the algebraic definition

- (Algebraic $\Rightarrow$ Geometric) Assume $\vec{v}_1,... \vec{v}_n$ are linearly dependent by the geometric definition. This means that there exist $\alpha_1,... \alpha_n$ not all zero, so $\vec{0} = \alpha_1\vec{v}_1 +~ ...+~ \alpha_n\vec{v}_n$
  - Fix $i$ so that $\alpha_i \neq 0$, rearrange
    $$
    -\alpha_i\vec{v}_i = \alpha_1\vec{v}_1 +~... +~
    \alpha_{i-1}\vec{v}_{i-1} +\alpha_{i+1}\vec{v}_{i+1} +~
    ...+~ \alpha_n\vec{v}_n \\
    $$

  - Since $\alpha_i \neq 0$, multiply both sides by $\frac{-1}{\alpha_i}$
    $$
    \vec{v}_i = \frac{-\alpha_1}{\alpha_i} \vec{v}_1 +~... +~
    \frac{-\alpha_{i-1}}{\alpha_i}\vec{v}_{i-1} +
    \frac{-\alpha_{i-1}}{\alpha_i}\vec{v}_{i+1} +~
    ...+~ \frac{-\alpha_1}{\alpha_n}\vec{v}_n \\
    $$

  - This shows that $\vec{v}_i \in ~\text{span}~ \{\vec{v}_1, ..., 
    \vec{v}_{i-1}, \vec{v}_{i+1}, ..., \vec{v}_n \}$, and so it is linearly dependent by the geometric definition.

### Testing if a set of vector is linearly dependent or not

1. Making them into a matrix, perform RREF, if its trivial, then its linearly independent
2. If the <u>rank</u> of the matrix is equal to the number of columns, then its linearly independent, if the rank is smaller, then its a linearly dependent set.

---

# Reduced Row Echelon Form

- <u>Pivots</u> - learning ones (first non-zero entry)
- <u>Pivot columns</u> - columns with leading ones

### A matrix is in RREF if it satisfies these 3 properties

1. The **pivots** in every row is 1
2. **Above and below** each leading one are zeros
3. The leading ones are **arranged in an echelon** (sarcasm pattern)

### Free variables and complete solutions

- System with an unique solution

  $\left\{\begin{matrix} 
  & x+2y &= 9 \\ 
  & 3x+5y &= 20  \end{matrix}\right.$.    Has a complete unique solution.    $\begin{bmatrix} x \\ y \end{bmatrix} = \begin{bmatrix} -5 \\ 7 \end{bmatrix}$

- System with not unique (infinitely many solutions) solutions

  $\left\{\begin{matrix} 
  & x+2y &= 9 \\ 
  & 2x+4y &= 18  \end{matrix}\right.$     Assigning $t=y$ to the **free variable**  $\left\{\begin{matrix} 
  & x+2y &= 9 \\ 
  & \quad~ y &= t  \end{matrix}\right.$ 

  Therefore every solution in this system can be written as $\begin{bmatrix} x \\ y \end{bmatrix} =
  \begin{bmatrix} 9 \\ 0 \end{bmatrix} + 
  t\begin{bmatrix} -1 \\ 1 \end{bmatrix}$ for $t \in \R$. 

  

  