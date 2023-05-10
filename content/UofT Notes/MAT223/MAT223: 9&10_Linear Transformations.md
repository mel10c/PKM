# Linear Transformations

- <u>Transformation (map)</u> - another word for a function, used to describe changing vectors
  $$
  F: R^n \to R^m \quad \text{defined by} \quad 
  \begin{bmatrix} x \\ y \end{bmatrix} \mapsto 
  \begin{bmatrix} x~(...) \\ y~(...) \end{bmatrix}
  $$
  For $n, m \in \N$, and $(...)$ are real number operations for the transformation

  - The transformation is a set of rules that assigns each vector $\vec{x}$ in $\R^n$ to a vector $T(\vec{x})$ in $\R^m$ 
  
  > ##### The transformation $T: \R^2 \to \R^2$ defined by $\begin{bmatrix} x \\ y \end{bmatrix} \mapsto \begin{bmatrix} x+3 \\ y \end{bmatrix}$
  >
  > <img src="https://tva1.sinaimg.cn/large/008eGmZEly1go2n2yhcagj30zu0fmn2a.jpg" alt="Screen Shot 2021-02-27 at 13.09.14" style="zoom:30%;" />
  
- <u>Image of a Set</u> - Let $L:\R^n \to \R^m$ be a transformation and let $X \subseteq \R^n$ be a set. The *image of the set $X$ under $L$*, denoted $L(X)$, is the set: 
  $$
  L(x) = \{\vec{y} \in \R^m : \vec{y} = L(X) \text{ for some } \vec{x} \in X \}
  $$

  - "The set of all outputs of $L$ when the inputs comes from $X$"
  - For $\vec{x}$ in $\R^n$, the vector $T(\vec{x})$ in $\R^m$ is the **image** of the set


  > ##### Let $R: \R^2 \to \R^2$ be rotation counter clockwise by $30^\circ$ and $X = \left\{ x\vec{e}_1 + y\vec{e}_2 : x, y \in [0, 1] \right\}$ be the filled-in unit squre. Then $R(X)$ is the filled-in unit squre that meets the axis at an angle of $30^\circ$ Describe this using set builder notation
  >
  > <img src="https://tva1.sinaimg.cn/large/008eGmZEly1gobd2hvtbij30ou0dcdh1.jpg" alt="Screen Shot 2021-02-27 at 21.19.19" style="zoom:25%;" /> 
  >
  > Use the vector $(0, 1), (1, 0)$ in $X$ to find a matrix that would transform $X$ into $R(X)$
  > Calculate the corresponding vector in $R(X)$ using $\sin (30)$ and $\cos (30)$
  > $$
  > A = \begin{bmatrix}a & c \\ b & d\end{bmatrix} \begin{bmatrix}0 \\ 1\end{bmatrix} =
  > \begin{bmatrix}1/2 \\ \sqrt{3}/2 \end{bmatrix} \\
  > A = \begin{bmatrix}a & c \\ b & d\end{bmatrix} \begin{bmatrix}1 \\ 0\end{bmatrix} =
  > \begin{bmatrix} \sqrt{3}/2 \\ 1/2 \end{bmatrix} \\
  > A = \begin{bmatrix}\sqrt[]{3}/2 & -1/2 \\ 1/2 & \sqrt[]{3}/2\end{bmatrix}
  > $$
  > It is mathematically incorrect to multiply a matrix to a set ($AX \neq R(X)$)
  > Get $R(X) = \left\{ A(x\vec{e}_1 + y\vec{e}_2) : x, y \in [0, 1] \right\}$

## Linear Transformation

- <u>**Linear Transformation**</u>, Let $V, W$ be **subspaces**. Function $T: V \to W$ is linear transformation if:
  $$
  T(\vec{u}, \vec{v}) = T(\vec{u}) + T(\vec{v}) \quad \text{and} \quad
  T(\alpha \vec{v}) = \alpha T(\vec{v})
  $$
  For all vectors in $\vec{u}, \vec{v} \in V$  and all scalars $\alpha$

  - $T(\text{span} \{\vec{u} \}) = \text{span} \{ T(\vec{u})\}$ 

  - If $T: \R^n \to \R^m$ is a linear trarnsformation, then $T$ takes subspaces to subspaces

  - If $T: \R^n \to \R^m$ is a linear transformation, then $T(\vec{0}) = \vec{0}$  (because $T(\vec{0}) = T(0\vec{v}) = \vec{0}$ )
  - If $T: \R^n \to \R^m$ is a linear transformation, then $T$ takes parallel lines to parallel lines (or points)

  > ##### Let $S: \R^2 \to \R^2$ and $T: \R^2 \to \R^2$ be defined by $\begin{bmatrix} x \\ y \end{bmatrix} \xmapsto{S} \begin{bmatrix} 2x \\ y \end{bmatrix} \quad \text{and} \quad\begin{bmatrix} x \\ y \end{bmatrix} \xmapsto{T} \begin{bmatrix} x \\ y+4 \end{bmatrix}$, for each $S, T$, determine whether the transformation is linear
  >
  > Let $\vec{u}=\begin{bmatrix} u_1 \\ u_2 \end{bmatrix}, \vec{v}=\begin{bmatrix} v_1 \\ v_2 \end{bmatrix}$ be vectors, and let $\alpha$ be a scaler 
  >
  > Consider $S$, need to verify that $S(\vec{u} + \vec{v}) = S(\vec{u}) + S(\vec{v})$  and $S(\alpha \vec{v}) = \alpha S(\vec{v})$, computing:
  > $$
  > S(\vec{u} + \vec{v}) = 
  > S \left( \begin{bmatrix} u_1 + v_1 \\ u_2 + v_2 \end{bmatrix} \right) =
  > \begin{bmatrix} 2u_1 + 2v_1 \\ u_2 + v_2 \end{bmatrix} =
  > \begin{bmatrix} 2u_1 \\ u_2 \end{bmatrix} +
  > \begin{bmatrix}2v_1 \\ v_2\end{bmatrix} = 
  > S(\vec{u}) + S(\vec{v})
  > $$
  > Then
  > $$
  > S(\alpha \vec{u}) = 
  > \begin{bmatrix}2\alpha u_1 \\ \alpha u_2\end{bmatrix} =
  > \alpha \begin{bmatrix}2u_1 \\ u_2\end{bmatrix} = \alpha S(\vec{u})
  > $$
  > So $S$ satisfies all the properties of a linear transformation.
  > Considering $T$, notice that $T(\vec{u} + \vec{v}) \begin{bmatrix}u_1 + v_1 \\ u_2 + v_2 +4\end{bmatrix}$ dooes not look like $T(\vec{u}) + T(\vec{v}) = \begin{bmatrix}u_1 + v_1 \\ u_2 + v_2 + 8\end{bmatrix}$. Therefore, $T$ is not linear.
  > Since $T$ violated a linear transformation property, then $T$ cannot be a linear transformation


### Function Notation vs. Linear Transformation Notation
- In linear transformations: $T: \R^n \to \R^m$, $T(\vec{x}) = T\vec{x}$
- While, $f(x) \neq$ *the number* $f(x)$ in linearly algebra (it is **only** a number, does not rep. function anymore)

#### Linear Transformation with Proofs

- Starting with a linearity proof with **"let $\vec{x}, \vec{y} \in \R^n$ and let $\alpha$ be a scalar"** allows the argument about all vectors and scalars be developed simultaneously
- Then prove that 2 definitions are satisfied

> ##### Let $T: \R^n \to \R^n$ be defined by $T(\vec{x}) = \vec{x} + \vec{e}_1$, Show that $T$ is not linear
>
> *Proof* 	Show that $T$ does not distribute with respect to scalar multiplication 
> $$ T(2\vec{0}) = T(\vec{0}) = \vec{e}_1 \neq 2\vec{e}_2 = 2T(\vec{0}) $$
> Therefore, $T$ cannot be a linear transformation. $\quad \Box$


## Matrix Transformations
- Let $M$ be a matrix, for a vector $\vec{v} \in \R^2$, $M\vec{v}$ is another vector in $\R^2$. Then multiplication of $M$ can be interpreted as a transformation:
    $$ T: \R^2 \to \R^2 \quad \text{by} \quad T(\vec{x}) = M\vec{x}$$
- **All** matrix transformations are linear transformations, BUT, **only most** linear transformations are matrix transformations (closely related, but not the same thing)
- Correct way to specify a linear transformations
    - The transformations $T$ defined by $T(\vec{x}) = M\vec{x}$
    - The transformation given by multiplication by $M$
    - The transformation induced by $M$
    - The matrix transformation given by $M$
    - The linear transformation whose matrix is $M$
- **Incorrect** way to specify a linear transformation: $ T: \R^2 \to \R^2 \quad \text{by} \quad T = M$

### Finding a Matrix for a Linear Transformation

- Know: for $T: \R^n \to \R^m$ as a linear transformation, matrix for $T$ must be $m \times n$
    $$
    T: \R^{n} \to \R^{m} \Rightarrow T(\vec{x}) = A_T \vec{x}, \quad A_T = \begin{bmatrix}T(\vec{e}1) & \dots & T(\vec{e}_n)\end{bmatrix} 
    $$
    

Let the linear transformation to be $T(\vec{e}_1) = \vec{v}_1, T(\vec{e}_2) = \vec{v}_2$. Find a matrix $A_T$ such that $T(\vec{x}) = A_T \vec{x}$
1. Write $\vec{x}$ in the form of unit vectors ($x_1 \vec{e}_1 + x_2 \vec{e}_2$)
2. Then $T(\vec{x}) = T(x_1 \vec{e}_1 + x_2 \vec{e}_2) = x_1T(\vec{e}_1), x_2T(\vec{e}_2) = x_1 \vec{v}_1 + x_2 \vec{v}_2$ 
3. Then $T(\vec{x}) = \begin{bmatrix}\vec{v}_1 & \vec{v}_2\end{bmatrix} \begin{bmatrix}x_1 \\ x_2\end{bmatrix} = \begin{bmatrix}\vec{v}_1 & \vec{v}_2\end{bmatrix} \vec{x}$
4. Which means that $T(\vec{x}) = A_T \vec{x}$, where $A_T = \begin{bmatrix}\vec{v}_1 & \vec{v}_2\end{bmatrix} = \begin{bmatrix}T(\vec{e}_1) & T(\vec{e}_2)\end{bmatrix}$ _

> ##### Let $T: \R^2 \to \R^2$ be defined by $T\begin{bmatrix}x \\ y\end{bmatrix} = \begin{bmatrix} 2x + y \\ x\end{bmatrix}$. Find a matrix, $M$, for $T$
>
> Because $T$ is a transformation for $\R^2 \to \R^2$, $M$ will be a $2 \times 2$ matrix. Let $M = \begin{bmatrix}a & b \\ c & d\end{bmatrix}$ 
> Use input-output paris to "calibrate" $M$
> $$
> T \begin{bmatrix}1 \\ 1\end{bmatrix} = \begin{bmatrix}3 \\  3\end{bmatrix} \quad \text{and} \quad T\begin{bmatrix}0 \\ 1\end{bmatrix} = \begin{bmatrix}1 \\ 0\end{bmatrix}
> $$
> Since $M$ is a matrix for $T$, then $T\vec{x}$ for all $\vec{x}$ and so
> $$
> M\begin{bmatrix}1 \\ 1\end{bmatrix} = \begin{bmatrix}a & b \\ c & d\end{bmatrix} \begin{bmatrix}1 \\ 1\end{bmatrix} = \begin{bmatrix}a+b \\ c+d\end{bmatrix} = \begin{bmatrix}3 \\ 1\end{bmatrix}
> $$
> and
> $$
> M \begin{bmatrix}0 \\ 1\end{bmatrix} = \begin{bmatrix}a & b \\ c & d\end{bmatrix} \begin{bmatrix}0 \\  1\end{bmatrix} = \begin{bmatrix}b \\  d\end{bmatrix} = \begin{bmatrix}1 \\  0\end{bmatrix}
> $$
> This gives the system of equations
> $$
> \left\{\begin{matrix} 
> a+b & & =3 \\ 
> &c+d & =1 \\
> b & & =1 \\ 
> & d & =0 \\ 
> \end{matrix}\right.
> $$
> and solving this system get: 
> $$M = \begin{bmatrix}a & b \\ c & d\end{bmatrix} = \begin{bmatrix}2 & 1 \\ 1 & 0\end{bmatrix}$$

## The Composition of Linear Transformations

- <u>**Composition of Functions**</u> - let $f: A \to B$ and $g: B \to C $ The **composition** of $g$ and $f$, notated $g \circ f$ the function $h: A\to C$ defined by  $h(x) = g \circ f = g \left( f(x) \right) $
  
> ##### Let $h: \R^{2} \to \R^{2}$ be the transformation given by $M = \begin{bmatrix}\sqrt[]{2}/2 & -\sqrt[]{2}.2 \\ 0 & 0\end{bmatrix}$, let $f: \R^{2} \mapsto \R^{2}$ be rotation counter clockwise by $45^\circ$ and let $g: \R^{2} \mapsto \R^{2}$ be projection onto the x-aixs. Write $h$ as the composition (in some order) of $f, g$
  >
  > Use $\vec{e}_1, \vec{e}_2$ to determine whether $h$ is $f \circ g$ or $g \circ f$
  > $$
  > h(\vec{e}_1) = \begin{bmatrix}\sqrt[]{2}/2 \\ 0\end{bmatrix} \quad \text{and} \quad 
  > h(\vec{e}_2) = \begin{bmatrix}-\sqrt[]{2}/2 \\ 0\end{bmatrix}
  > $$
  >
  > For $f \circ g$: $\quad f \circ g(\vec{e}_1) = \begin{bmatrix}\sqrt[]{2}/2 \\ \sqrt[]{2}/2\end{bmatrix}$ and $f \circ g (\vec{e}_2) = \begin{bmatrix}0 \\ 0\end{bmatrix}$
  >
  > For $g \circ f$; $\quad g \circ f(\vec{e}_1) = \begin{bmatrix}\sqrt[]{2}/2 \\ 0\end{bmatrix}$ and $g \circ f (\vec{e}_2) = \begin{bmatrix}-\sqrt[]{2}/2 \\ 0\end{bmatrix}$
  >
  > Since the answer of $g \circ f$ agrees with $h$ , then $h = g\circ f$

### Compositions and Matrix Products

- If $\mathcal{P}: \R^{a} \to \R^{b}$ and $\mathcal{Q}: \R^{c} \to \R^{a}$ are matrix transformations with matrices $M_P$ and $M_Q$, then $\mathcal{P} \circ \mathcal{Q}$ is a matrix transformation whose matrix is given by the matrix product $M_P M_Q$


> ##### Find entries of the matrix $A$ below, assuming the equation must be true $\forall x_1, x_2, x_3$. For $A \begin{bmatrix}x_1 \\ x_2 \\ x_3\end{bmatrix} = \begin{bmatrix}3x_1 - x_3 \\ -2x_1 + 4x_2 \\  6x_2 - 3x_3\end{bmatrix}$.
> Let $v_1, v_2, v_3$ represent the columns of matrix $A$ Then:
> $$
x_1 v_1 + x_2 v_2 + x_3 v_3 = \begin{bmatrix}3x_1 & & - x_3 \\ -2x_1 & + 4x_2 & \\  & 6x_2 & - 3x_3\end{bmatrix}
> $$
> Extracting the coefficients, then $v_1 = (3, -2, 0) v_2 = (0, 4, 0) v_3 = (-1, 0, -3)$, combining to form the matrix $A$:
> $$
A = \begin{bmatrix}3 & 0 & - 1 \\ -2 & 4 & 0 \\ 0 & 6 & - 3\end{bmatrix}
> $$

#### An application would be linear transformations with respect to basis. Let $T: \R^{n} \to \R^{n}$

- $T(\vec{x}) = A \vec{x}$ where $A$ is the transformation matrix for T **with respect to the standard basis**
- Let $B= \left\{ \vec{v}_1, \dots \vec{v}_n \right\}$ be a basis for $\R^n$. Then $[T(\vec{x})]_B = D [\vec{x}]_B$ where $D$ is the transformation matrix for $T$ with **with respect to the basis $B$**
- Let $C$ be the change of basis matrix for the basis $B$, then $C [\vec{x}]_B = \vec{x}$ and $[\vec{x}]_B = C ^{-1} \vec{x}$

$$
\begin{align*}
D [\vec{x}]_B &= [T(\vec{x})]_B \
\tag{Using $D [\vec{x}]_B =[T(\vec{x})]_B$} \\
&= [A \vec{x}]_B \tag{Using $T(\vec{x}) = A \vec{x}$} \\
&= C^{-1} (A \vec{x}) \tag{Using $[\vec{x}]_B = C ^{-1} \vec{x}$} \\
&= C^{-1} A~(C [\vec{x}]_B) \tag{Using $\vec{x} = C [\vec{x}]_B$}
\end{align*}
$$

- $D$ is the transformation matrix for $T$ with respect to the basis $B$. And $C$ is the change of basis matrix for $B$. And $A$ is the transformation matrix for $T$ with respect to the standard basis. Then $D = C^{-1} A~C$
