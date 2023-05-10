# Dot Products & Normal Forms

## Dot Product

Sometimes called as the "scaler product" because it produces a scaler

- Let $\vec{a}, \vec{b}$ be vectors rooted at the same point and let $\theta$ denote the **smaller** of the two angles between them ($0 \le \theta \le \pi$), the geometric definition of **<u>dot product</u>** is
  $$
  \vec{a} \cdot \vec{b} = \left\|\vec{a}\right\| \left\|\vec{b}\right\| \cos \theta
  $$

  > $\vec{x}= (2,3), \quad \left\|\vec{x}\right\|=\sqrt{2^2 + 3^2} =\sqrt{13}$
  
- The algebraic definition in terms of coordinates
  $$
  \begin{bmatrix} a_1 \\ a_1 \\ \vdots \\ a_n \end{bmatrix} \cdot
  \begin{bmatrix} b_1 \\ b_2 \\ \vdots \\ b_n \end{bmatrix} =
  a_1 b_1 + a_2 b_2 + ... + a_n b_n
  $$

- By equating the geometric and algebraic definition of the dot product
  $$
  \cos \theta = \frac{\vec{p} \cdot \vec{q}}
  {\left\|\vec{p}\right\| \left\|\vec{q}\right\|}
  \quad \Rightarrow \quad
\theta = \arccos\big( \frac{\vec{p} \cdot \vec{q}}
  {\left\|\vec{p}\right\| \left\|\vec{q}\right\|} \big)
  $$
  
  > ##### Find the angle between the vectors $\vec{v}=(1, 2, 3)$ and $\vec{w} = (1, 1, -2)$
  >
  > From the algebraic definition of the dot product, get: 
  > $$
  > \vec{v} \cdot \vec{w}=1(1) + 2(1) + 3(-2) = -3
  > $$
  > From the geometric definition, get:      
  > $$
  > \vec{v} \cdot \vec{w}=\left\|\vec{v}\right\| \left\|\vec{w}\right\| \cos \theta
  > = \sqrt{14} \sqrt{6} \cos \theta = 2 \sqrt{21} \cos \theta
  > $$
  > Equating the two definitions, get:
  > $$
  > \cos \theta = \frac{-3}{2 \sqrt{21}}
  > $$
  > Therefore $\theta = \arccos (\frac{-3}{2 \sqrt{21}})$ 
- Dot products can be used to compute the length of vectors $\vec{a} \cdot \vec{a} =\left\|\vec{a}\right\| \left\|\vec{a}\right\| \cos 0= \left\|\vec{a}\right\|^2$

- Dot products has the same distributive laws as other variables [ex. $a \cdot (b + c) = ab + ac$  etc.]

- The **<u>distance</u>** between two vectors $\vec{u}$ and $\vec{v}$ is $\left\|\vec{v} - \vec{u} \right\|$

- <u>**Unit vector**</u> - a vector $\vec{v}$ is called a unit vector if $\left\|\vec{v}\right\| = 1$
  $$
  \left\|\hat{u}\right\| = 1 \quad \Rightarrow \quad
  \hat{u} = \frac{\vec{v}}{\left\|\vec{v}\right\|}
  $$

### Orthogonality

- <u>Orthogonal</u> - Two vectors $\vec{u}, \vec{v}$ are **orthogonal** (perpendicular) to each other if $\vec{u} \cdot \vec{u} = 0$
  - The definition of orthogonal encapsulates *both* the idea of two vectors forming a right angle and the idea of one of them being $\vec{0}$
- <u>Direction</u> - The vector $\vec{u}$ points in the **direction** of the vector $\vec{v}$ if $k\vec{u} = \vec{v}$ for some scalar $k$. The vector $\vec{u}$ points in the **positive direction** of $\vec{v}$ if $k\vec{u} = \vec{v}$ for some *positive* scalar $k$

## Normal Vector

- <u>Normal vector</u> to a line (or plane or hyperplane) is a non-zero vector that is orthogonal to all direction vectors for the line (or plane or hyperplane)

- <u>Normal form of a line</u> - a line $\ell \subseteq \R^2$ is expressed in **normal form** if $\ell$ is the solution set to equation:
  $$
  \vec{n} \cdot (\vec{x} - \vec{p}) = 0
  $$
  Where $\vec{n}$ and $\vec{p}$ are fixed vectors

  > ##### Find vector form and normal form of the plane $\mathcal{P}$ passing through the points $A=(1, 0, 0), B=(0, 1, 0), C=(0, 0, 1)$ .
  >
  > Get the 2 directional vectors from these 3 points
  > $$
  > \vec{d}_1 = \overrightarrow{AB} = \begin{bmatrix} -1 \\ 1 \\ 0 \end{bmatrix}
  > \quad \quad \quad
  > \vec{d}_2 = \overrightarrow{AC} = \begin{bmatrix} -1 \\ 0 \\ 1 \end{bmatrix}
  > $$
  > Using point $A$ and the directional vectors, get the expression of $\mathcal{P}$
  > $$
  > \begin{bmatrix} x \\ y \\ x \end{bmatrix} = 
  > t\begin{bmatrix} -1 \\ 1 \\ 0 \end{bmatrix} +
  > s\begin{bmatrix} -1 \\ 0 \\ 1 \end{bmatrix} +
  > \begin{bmatrix} 1 \\ 0 \\ 0 \end{bmatrix}
  > $$
  > Use $\vec{n} \cdot \vec{d}_1 = 0 = \vec{n} \cdot \vec{d}_2$     
  > $$
  > \vec{n} \cdot (\begin{bmatrix} -1 \\ 1 \\ 0 \end{bmatrix} + 
  > \begin{bmatrix} -1 \\ 0 \\ 1 \end{bmatrix}) 
  > \quad \Rightarrow \quad 
  > \vec{n} \cdot \begin{bmatrix} -2 \\ 1 \\ 1 \end{bmatrix} = 0
  > \quad \Rightarrow \quad
  > -2\vec{x} + \vec{y} + \vec{z} = 0
  > $$
  > So $\vec{n} = (1, 1, 1)$, therefore the normal form of $\mathcal{P}$ can be expressed as
  > $$
  > \begin{bmatrix} 1 \\ 1 \\ 1 \end{bmatrix} \cdot \left(
  > \begin{bmatrix} x \\ y \\ z \end{bmatrix} - 
  > \begin{bmatrix} 1 \\ 0 \\ 0 \end{bmatrix} \right) = 0
  > $$

- <u>Hyperplane</u> - the set $X \subseteq \R^n$ is called a **hyperplane** if there exists $\vec{n} \neq \vec{0}$ and $\vec{p}$ so that $X$ is the set of solutions to the equation $\vec{n} \cdot (\vec{x} - \vec{p}) = 0$ 

  - $\vec{n} \cdot (\vec{x} - \vec{p}) = 0$ If and only if  $\vec{n} \cdot \vec{x} = \vec{n} \cdot \vec{p} = \alpha$ Since $\vec{n}$ and $\vec{p}$ are fixed, $\alpha$ is a constant then:
    $$
    \vec{n} \cdot (\vec{x} - \vec{p}) = \vec{n} \cdot \vec{x} -\alpha =
    n_x x + n_y y + n_z z - \alpha = 0
    $$
    Therefore, $\mathcal{P}$ is the set of solutions to     $n_x x + n_y y + n_z z = \alpha$ (\*)

  - This (\*) equation is called the *scalar form* of a plane. 

  > ##### Let $\mathcal{Q} \subseteq \R^3$ be the plane passing through $\vec{p}=(1,1,0)$ and with normal vector $\vec{n}=(1,1,1)$, write $\mathcal{Q}$ in vector form
  >
  > $\mathcal{Q}$ Is the set of solutions to $\vec{n} \cdot (\vec{x} - \vec{p}) = 0$ , where $\alpha = 1(1)+1(1)+0(1)=2$, then
  > $$
  > \vec{n} \cdot (\vec{x} - \vec{p}) = \vec{n} \cdot \vec{x} -\alpha =
  > x + y + z - 2= 0
  > $$
  > Rearranging, get $\mathcal{Q}$ as the set of all solutions to $x + y + z = 2$
  >
  > Using row reduction algorithm to write the complete solution, get 
  > $$
  > \begin{bmatrix} x \\ y \\ x \end{bmatrix} = 
  > t\begin{bmatrix} -1 \\ 1 \\ 0 \end{bmatrix} +
  > s\begin{bmatrix} -1 \\ 0 \\ 1 \end{bmatrix} +
  > \begin{bmatrix} 2 \\ 0 \\ 0 \end{bmatrix}
  > $$

---

# Matrices

- <u>Matrix</u> - grid of numbers surrounded by round or square brackets
  $$
  \begin{bmatrix}
      a_{11} & a_{12}  & \dots  & a_{1n} \\
      a_{21} & a_{22}  & \dots  & a_{2n} \\
      \vdots & \vdots  & \ddots & \vdots \\
      a_{m1} & a_{m2}  & \dots  & a_{mn}
  \end{bmatrix} = 
  \begin{pmatrix}
      a_{11} & a_{12}  & \dots  & a_{1n} \\
      a_{21} & a_{22}  & \dots  & a_{2n} \\
      \vdots & \vdots  & \ddots & \vdots \\
      a_{m1} & a_{m2}  & \dots  & a_{mn}
  \end{pmatrix}
  $$

- <u>Dimensions</u> (shape or size) of a matrix is the #rows $\times$ #columns

- <u>Entry</u> - the number in the row and column (ex. $(i, j)$ Is the $i$th row and $j$th column)

- Use capital letters to name the matrix

  > $A = \begin{bmatrix} 1 & 2 & -1 \\ 3 & 0 & 7 \end{bmatrix}$ Is a $2 \times 3$ matrix, the $(2, 1)$ entry of $A$ is $a_{21} = 3$

- Matrix terminology

  - Square matrix -- #rows = #columns
  - Diagonal matrix -- all off-diagonal entries are zero
  - Upper triangular -- all below-diagonal entries are zero
  - Lower triangular -- all above-diagonal entries are zero

- <u>Identity matrix</u> - a *square* *diagonal* matrix 
  $$
  I_{n \times n} = \begin{bmatrix}
      1 & 0  & \dots  & 0 \\
      0 & 1  & \dots  & 0 \\
      \vdots & \vdots  & \ddots & \vdots \\
      0 & 0  & \dots  & 1
  \end{bmatrix}
  $$

- <u>Zero matrix</u> - a matrix with entries all zero
  $$
  0_{n \times m} = \begin{bmatrix}
      0 & 0 & 0 & \dots  & 0 \\
      0 & 0 & 0 & \dots  & 0 \\
      \vdots & \vdots & \vdots & \ddots & \vdots \\
      0 & 0 & 0 & \dots  & 0
  \end{bmatrix}
  $$

### Matrix multiplication

- Column intrepretation<img src="https://tva1.sinaimg.cn/large/008eGmZEly1gnlah6x6hgj30da0akwfv.jpg" alt="Screen Shot 2021-02-12 at 12.52.33" style="zoom:30%;" />
  > $$
  > \begin{bmatrix} 1 & 0 & -2 \\ 0 & 3 & -1 \\ 1 & 2 & 1 \end{bmatrix} 
  > \begin{bmatrix} 3 \\ -1 \\ 4 \end{bmatrix} 
  >  = 3 \begin{bmatrix} 1 \\ 0 \\ 1 \end{bmatrix} 
  >  + (-1) \begin{bmatrix} 0 \\ 3 \\ 2 \end{bmatrix} 
  >  + 4 \begin{bmatrix} -2 \\ -1 \\ 1 \end{bmatrix} 
  >  = \begin{bmatrix} -5 \\ -7 \\ 5 \end{bmatrix}
  > $$

- Row Interpretation  $\begin{bmatrix}
  \rule[.2ex]{1em}{0.2pt}  \vec{r}_1 \rule[.2ex]{1em}{0.2pt} \\ 
  \rule[.2ex]{1em}{0.2pt}  \vec{r}_2 \rule[.2ex]{1em}{0.2pt} \\ 
      \vdots \\
  \rule[.2ex]{1em}{0.2pt}  \vec{r}_n \rule[.2ex]{1em}{0.2pt}
  \end{bmatrix} \cdot \vec{x}$ = $\begin{bmatrix}
      \vec{r}_1 \cdot \vec{x} \\ 
      \vec{r}_2 \cdot \vec{x} \\ 
      \vdots \\
      \vec{r}_n \cdot \vec{x}
  \end{bmatrix}$ 

  > $$
  > \begin{bmatrix} 1 & 0 & -2 \\ 0 & 3 & -1 \\ 1 & 2 & 1 \end{bmatrix} 
  > \begin{bmatrix} 3 \\ -1 \\ 4 \end{bmatrix} =
  > \begin{bmatrix}
  >     \vec{r}_1 \cdot \vec{x} \\ 
  >     \vec{r}_2 \cdot \vec{x} \\ 
  >     \vdots \\
  >     \vec{r}_n \cdot \vec{x}
  > \end{bmatrix} = 
  > \begin{bmatrix} -5 \\ -7 \\ 5 \end{bmatrix}
  > $$

- Matrix - matrix multiplication
   <img src="https://tva1.sinaimg.cn/large/008eGmZEly1gnlaplg262j312i0qmwok.jpg" alt="Screen Shot 2021-02-12 at 13.06.37" style="zoom:25%;" />
  - If C is $m \times n$ A is $n \times k$ then the resulted CA is $m \times k$ 
  - For matrix to multiply: matrix 1 dimension $a \times b$, and matrix 2 dimension $x \times y$, $b=y$ 