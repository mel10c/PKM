# Coordinates & Change of Basis

- <u>Basis</u> for a subspace $\mathcal{V}$ is a **linearly independent spanning subspace**
- <u>Dimension</u> of a subspace $\mathcal{V}$ is the **size of a basis** for $\mathcal{V}$ (number of basis vectors)


> ##### Find a basis and the dimension of $W = \text{span} \left\{ \begin{bmatrix}0 \\ 0 \\ 0\end{bmatrix}, \begin{bmatrix}1 \\ -2 \\ -1\end{bmatrix}, \begin{bmatrix}2 \\ -4 \\ -2\end{bmatrix}, \begin{bmatrix}-2 \\ 5 \\ 3\end{bmatrix}, \begin{bmatrix}3 \\ -6 \\ -2\end{bmatrix} \right\}$
>
> Find a maximal linearly independent subset using matrix
> $$
> \begin{bmatrix}
> 0 & 1 & 2 &-2 &3 \\ 0 & -2 & -4 & 5 & -6 \\0 & -1 & -2 & 3 & -2
> \end{bmatrix} \quad \text{RREF} \quad
> \begin{bmatrix}
> 0 & 1 & 2 &0 &0\\ 0 & 0 & 0 & 1 & 0 \\0 & 0 & 0 & 0& 1
> \end{bmatrix} 
> $$
> Column 2, 4, 5 are linearly independent
> $$
> \mathcal{B}=\left\{ \begin{bmatrix}1 \\ -2 \\ -1\end{bmatrix}, \begin{bmatrix}-2 \\ 5 \\ 3\end{bmatrix}, \begin{bmatrix}3 \\ -6 \\ -2\end{bmatrix} \right\}
> $$
> $\mathcal{B}$ is a basis of $W$ and dim$(W) = 3$, then $W = \R^3$

## Representation in Basis

- Let $\mathcal{B} = \{\vec{b}_1, \dots, \vec{b}_n \}$ be a basis for a subspace $V$ and let $\vec{v} \in V$. The <u>representation of $\vec{v}$ in the $\mathcal{B}$ basis</u>, **notated $[\vec{v}]_\mathcal{B}$** is the column matrix
  $$
  [\vec{v}]_\mathcal{B} = 
  \begin{bmatrix} \alpha_a \\ \vdots \\ \alpha_n \end{bmatrix}
  $$
  Where $\alpha_1, \dots, \alpha_n$ uniquely satisfy $\vec{v}= \alpha_{1}\vec{v}_{1} + \dots +\alpha_{n}\vec{v}_{n}$, conversely,
  $$
  \begin{bmatrix} \alpha_a \\ \vdots \\ \alpha_n \end{bmatrix}_\mathcal{B} =
  \alpha_{1}\vec{v}_{1} + \dots +\alpha_{n}\vec{v}_{n}
  $$
  Is notation for the linear combination of $\vec{b}_1, \dots, \vec{b}_n$ with coefficients $\alpha_1, \dots, \alpha_n$.

  > ##### Let $\mathcal{E} = \{\vec{e}_1, \vec{e}_2 \}$ be the standard basis for $\R^2$ and let $\mathcal{C} = \{\vec{c}_1, \vec{c}_2 \}$ where $\vec{c}_1 = \vec{e}_1 + \vec{e}_2$, and $\vec{e}_2 = 3\vec{e}_2$ be nother basis for $\R^2$. Given that $\vec{v} = 2\vec{e}_1 - \vec{e}_2$, find $[\vec{v}]_\mathcal{E}$ and $[\vec{v}]_\mathcal{C}$
  >
  > Since $\vec{v} = 2\vec{e}_1 - \vec{e}_2$, get that $[\vec{v}]_\mathcal{E} = \begin{bmatrix} 2 \\ -1 \end{bmatrix}$ 
  >
  > To find $[\vec{v}]_\mathcal{C}$, need to write $\vec{v}$ as a linear combination of $\vec{c}_1, \vec{c}_2$: 	let $\vec{v} = x\vec{c}_1 + y\vec{c}_2$ then
  > $$
  > \vec{v} = x\vec{c}_1 + y\vec{c}_2 = x(\vec{e}_1 + \vec{e}_2) + 3y\vec{e}_2 
  > = x\vec{e}_1 + (x + 3y)\vec{e}_2
  > $$
  > Using $\vec{v} = 2\vec{e}_1 - \vec{e}_2$, and the equation above, get
  > $$
  > 2\vec{e}_1 + \vec{e}_2 = x\vec{e}_1 + (x + 3y)\vec{e}_2
  > $$
  > So than
  > $$
  > (x-2) \vec{e}_1 + (x +3y +1)\vec{e}_2 = \vec{0}
  > $$
  > Since $\vec{e}_1$ and $\vec{e}_2$ are linearly independent, the only way for the above equation to be satisfied:
  > $$
  > \left\{\begin{matrix} 
  > x & &= 2 \\ 
  > x & +3y &= -1  \end{matrix}\right.
  > $$
  > Solving, and get $\vec{v} = 2\vec{c}_1 - \vec{c}_2$ so $[\vec{v}]_\mathcal{C} = \begin{bmatrix} 2 \\ -1 \end{bmatrix}$ 

#### Procedure to find a basis for a set of vectors

- From standard to other basis
    $$
    \text{from } [\vec{x}]_\mathcal{E} = M [\vec{x}]_\mathcal{B} \quad \quad \quad
    \text{solve for}(x, y, z): \quad
    \begin{bmatrix}x_1 \\ x_2 \\x_3 \end{bmatrix}
    = \begin{bmatrix}
    \dots & \dots & \dots\\ \dots & \dots & \dots \\ \dots& \dots& \dots
    \end{bmatrix}
    \begin{bmatrix}x \\ y \\ z\end{bmatrix} \\ 
    
    \text{or } M^{-1}[\vec{x}]_\mathcal{E} = [\vec{x}]_\mathcal{B} \quad \quad \quad
    \text{solve for}(x, y, z): \quad
    \begin{bmatrix}
    \dots & \dots & \dots\\ \dots & \dots & \dots \\ \dots& \dots& \dots
    \end{bmatrix}
    \begin{bmatrix}x_1 \\ x_2 \\x_3 \end{bmatrix}
    = 
    \begin{bmatrix}x \\ y \\ z\end{bmatrix}
    $$


- From basis to standard basis
    $$
    \text{from } [\vec{x}]_\mathcal{E} = M [\vec{x}]_\mathcal{B} \quad \quad \quad
    \text{solve for}(x, y, z): \quad
    \begin{bmatrix}x \\ y \\ z\end{bmatrix} =
    \begin{bmatrix}
    \dots & \dots & \dots\\ \dots & \dots & \dots \\ \dots& \dots& \dots
    \end{bmatrix}
    \begin{bmatrix}x_1 \\ x_2 \\x_3 \end{bmatrix}
    $$

- Let $X, Y$ be matrices such that $X[\vec{x}]_\mathcal{E} = [\vec{x}]_\mathcal{B}$ and $Y[\vec{x}]_\mathcal{B} = [\vec{x}]_\mathcal{E}$ then for all $\vec{x}$, $XY = YX$

> ##### Consider the basis: $\mathcal{B}=\left\{ \begin{bmatrix}2 \\ 2 \\ 4\end{bmatrix}, \begin{bmatrix}-1 \\ 0 \\ 3\end{bmatrix}, \begin{bmatrix}1 \\ 1 \\ 1\end{bmatrix} \right\}$ and $[\vec{x}]_\mathcal{B} = \begin{bmatrix}2 \\ 1 \\ -3\end{bmatrix}$ Find $\vec{x}$ in standard basis
>
> $$
> \vec{x} = 2 \begin{bmatrix}2 \\ 2 \\ 4\end{bmatrix}
> + 1 \begin{bmatrix}-1 \\ 0 \\ 3\end{bmatrix}
> -3\begin{bmatrix}1 \\ 1 \\ 1\end{bmatrix}
> = \begin{bmatrix}4 \\ 4 \\ 4\end{bmatrix}
> + \begin{bmatrix}-1 \\ 0 \\ 3\end{bmatrix}
> + \begin{bmatrix}-3 \\ -3 \\ -3\end{bmatrix}
> = \begin{bmatrix}0 \\ 1 \\ 8\end{bmatrix}
> $$
> Therefore $\vec{x} = (0, 1, 8)$ in standard basis
>
> ##### Consider the basis: $\mathcal{B}=\left\{ \begin{bmatrix}2 \\ 2 \\ 4\end{bmatrix}, \begin{bmatrix}-1 \\ 0 \\ 3\end{bmatrix}, \begin{bmatrix}1 \\ 1 \\ 1\end{bmatrix} \right\}$ and $\vec{x} = \begin{bmatrix}2 \\ 3 \\ 4\end{bmatrix}$ Find $[\vec{x}]_\mathcal{B}$
>
> $[\vec{x}]_\mathcal{B}$ has the coordinates $(c_1, c_2, c_3)$
> $$
> \begin{bmatrix}2 \\ 3 \\ 4\end{bmatrix} = c_1 \begin{bmatrix}2 \\ 2 \\ 4\end{bmatrix} + 
> c_2 \begin{bmatrix}-1 \\ 0 \\ 3\end{bmatrix} + 
> c_3 \begin{bmatrix}1 \\ 1 \\ 1\end{bmatrix} \Longrightarrow 
> \begin{bmatrix}
> 2 & -1 & 1 & 2 \\ 2 & 0 & 1 & 3 \\ 4 & 3 & 1 & 4
> \end{bmatrix} \quad \text{RREF}
> \begin{bmatrix}
> 1 & 0 & 0& 2 \\ 0& 1 & 0& 1 \\ 0& 0& 1 & 5
> \end{bmatrix}
> $$
> Then $\vec{x} = (-1, 1, 5)$ in standard basis

## Notation Conventions

- If a problem involves only one basis, then write $\begin{bmatrix} x \\ y \end{bmatrix}$ means $\begin{bmatrix} x \\ y \end{bmatrix}_\mathcal{E}$ where $\mathcal{E}$ is the standard basis

- If there are multiple basis, then always write $\begin{bmatrix} x \\ y \end{bmatrix}_\mathcal{X}$ to specify a vector relative to basis $\mathcal{X}$

- $\vec{x} \neq [\vec{x}]_\mathcal{E} = \begin{bmatrix} a \\ b \end{bmatrix}
  ,~
  \begin{bmatrix} a \\ b \end{bmatrix}_\mathcal{E} = 
  \vec{x} \neq [\vec{x}]_\mathcal{E}$

  - *Left* sides of the two non-equal signs is a **true vector**, where as the *right* side is a meaningless **list of numbers**.  (Unit it has been assigned a basis)
    $$
    [\text{true vector}]_\mathcal{X} = \text{list of numbers},~
    [\text{list of numbers}]_\mathcal{X} = \text{true vector}
    $$

## Orientation of a Basis

- <u>Orthonormal bases</u> - bases consisting of unit vectors that are orthogonal to each other

  - Not all bases are orthonormal

- The ordered basis $\mathcal{B}$ is <u>Right-handed (positively oriented)</u> if it can be **continuously transformed** to the standard basis ($\vec{b}_i \mapsto \vec{e}_i$) while remaining **linearly independent** throughout the transformation. Otherwise, $\mathcal{B}$ would be <u>left-handed (negatively oriented)</u> 

  - By convention, the standard basis is right-handed

  > ##### For the two basis here: <img src="https://tva1.sinaimg.cn/large/008eGmZEly1gnzg1b6jtrj30dh04uaad.jpg" alt="Screen Shot 2021-02-24 at 18.49.08" style="zoom:75%;" />
  >
  > The $\mathcal{A}$ basis can be rotated to get to $\mathcal{E}$ while remaining the order ($\vec{a}_1 \mapsto \vec{e}_1$ and $\vec{a}_2 \mapsto \vec{e}_2$), then it has the *same* orientation as the standard basis (*positive*)
  >
  > The $\mathcal{B}$ basis cannot be rotated to get to $\mathcal{E}$ while remaining the order, then it has a *different* orientation as the standard basis (*negative*)

  > ##### For $\mathcal{X}$  <img src="https://tva1.sinaimg.cn/large/008eGmZEly1gnzg7u4sypj311e0csjtj.jpg" alt="Screen Shot 2021-02-24 at 18.54.58" style="zoom:35%;" />
  >
  > Keep $\vec{x}_1$ in place and transform $\vec{x}_2$ smoothly along the dotted line. During the entire transformation, $\vec{x}_1, \vec{x}_2$ is *linearly independent*, therefore, $\mathcal{X}$ is positively oriented
  >
  > #####  For $\mathcal{Y}$   <img src="https://tva1.sinaimg.cn/large/008eGmZEly1gnzg8mdwihj31dw0m243h.jpg" alt="Screen Shot 2021-02-24 at 18.55.04" style="zoom:30%;" />
  >
  > This time, along the route of $\vec{y}_2$'s transformation, the set $\vec{y}_1$ and $\vec{y}_2$ would become *linearly dependent* at some point. Therefore, $\mathcal{Y}$ is negatively oriented

### Reversing Orientation

1. Reflect $\mathcal{E} = \{\vec{e}_1, \vec{e}_2 \}$ with the line $y=x$, this sends $\{\vec{e}_1,\vec{e}_2 \}  \mapsto \{\vec{e}_2, \vec{e}_1 \}$
   <img src="https://tva1.sinaimg.cn/large/008eGmZEly1gnzggdqriqj314g0dydhz.jpg" alt="Screen Shot 2021-02-24 at 19.03.21" style="zoom:35%;" /> 

2. Reflect $\mathcal{E} = \{\vec{e}_1, \vec{e}_2 \}$ with he line $x=0$, this sends $\{\vec{e}_1,\vec{e}_2 \}  \mapsto \{-\vec{e}_1, \vec{e}_2 \}$ 
   <img src="https://tva1.sinaimg.cn/large/008eGmZEly1gnzgj77aduj30ze0dqq4v.jpg" alt="Screen Shot 2021-02-24 at 19.03.27" style="zoom:40%;" />
   - This has the *opposite* orientation as $\mathcal{E}$, it is **negatively oriented**

$$
\begin{bmatrix} 2 & 0 \\ 1 & 1 \end{bmatrix}
\begin{bmatrix} 2 \\ 3 \end{bmatrix}_\mathcal{E} =
\begin{bmatrix} 2 \\ 3 \end{bmatrix}
$$

