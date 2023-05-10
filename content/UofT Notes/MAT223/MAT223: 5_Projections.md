# Projections and Vector Components

## Projection

- <u>Projection</u> - Let $X$ be a set, the *projection* of the vector $\vec{v}$ onto $X$, written $\text{proj}_X \vec{v}$ is the **closest point** in $X$ to $\vec{v}$

  - Intuitively, $\text{proj}_{xy} \vec{v}$ is the "shadow" that $\vec{v}$ would on $\text{proj}_{xy}$ if the sun were perpendicular to $X$

- If there are two points other as the closest point to $\vec{v}$, OR there are no closest point to $\vec{v}$, then $\text{proj}_X \vec{v}$ is *undefined*

- For a fixed set $X$, $P(\vec{v}) = \text{proj}_X \vec{v}$ is a function that inputs and outputs vectors. The domain of this function is exactly the vectors is which $P(\vec{v})$ is defined. 

  - If $X$ is a line or a plane in $\R^n$, then the domain of $P(\vec{v})$ is all of $\R^n$ (if projection exist)

  >##### Let $\vec{v}=(1, 2, 3)$, $\text{proj}_{xy} \subseteq \R^3$ be the xy-plane,  $\ell_y \subseteq \R^3$ by the y-axis
  >
  >Intuitively, or by the picture, it can be concluded that $\text{proj}_{P_{xy}} \vec{v}=\begin{bmatrix} 1 \\ 2 \\ 0 \end{bmatrix}$ <img src="https://tva1.sinaimg.cn/large/008eGmZEly1gnl79x9km6j30ho0egq46.jpg" alt="Screen Shot 2021-02-12 at 10.51.52" style="zoom:20%;" />
  >
  >By definition, every vector in $\ell_y$ takes the form $\vec{u}_t=(0, t, 0)$ for some $t \in \R$. The distance between $\vec{u}_t$ and $\vec{v}$ is
  >$$
  >\left\|\vec{u}_t - \vec{v} \right\| = 
  >\left\| 
  >\begin{bmatrix} 0 \\ t \\ 0 \end{bmatrix} - 
  >\begin{bmatrix} 1 \\ 2 \\ 3 \end{bmatrix}
  >\right\| = 
  >\sqrt{1^2 + (t-2)^2 + 3^2}
  >$$
  >Since $(t-2)^2$ would be always position, this whole expression would be minimized when $(t-2)^2 = 0$, thus when $t=2$. Therefore $\vec{u}_2$ is the closest vector in $\ell_y$ to $\vec{v}$. 
  >$$
  >\text{proj}_{\ell_y} \vec{v} = \vec{u}_2 = \begin{bmatrix} 0 \\ 2 \\ 0 \end{bmatrix}
  >$$

- If $X$ is a line or plane and $\vec{v} \notin X$ is a vector, then $\vec{v}-\text{proj}_X \vec{v}$ is a **normal** vector for $X$

  - When projecting onto lines and planes, right angles appear in key places

  > ##### Let $\ell \subseteq \R^2$ be the line given in vector form by $\vec{x}=t \begin{bmatrix} 1 \\ 1 \end{bmatrix} + \begin{bmatrix} 3 \\ -2 \end{bmatrix}$, and let $\vec{v} = \begin{bmatrix} -1 \\ -1 \end{bmatrix}$. Use the fact that $\vec{v}-\text{proj}_\ell \vec{v}$ is a normal vector to $\ell$ to find $\text{proj}_\ell \vec{v}$
  >
  > Since $\vec{v}-\text{proj}_\ell \vec{v}$ is a normal vector to $\ell$, then its orthogonal to $\vec{d}=\begin{bmatrix} 1 \\ 1 \end{bmatrix}$. Let $\begin{bmatrix} x \\ y \end{bmatrix} = \text{proj}_\ell \vec{v}$ for some unknown $x, y \in \R$, get:
  > $$
  > (\vec{v}-\text{proj}_\ell \vec{v}) \cdot \vec{d} = 
  > \left( 
  > \begin{bmatrix} -1 \\ -1 \end{bmatrix} - \begin{bmatrix} x \\ y \end{bmatrix}
  > \right)
  > \cdot \begin{bmatrix} 1 \\ 1 \end{bmatrix} = 
  > \begin{bmatrix} -1-x \\ -1-y \end{bmatrix} \cdot 
  > \begin{bmatrix} 1 \\ 1 \end{bmatrix} =
  > -2-x-y = 0
  > $$
  > That is  $x+y = -2$ 	(*1)
  >
  > Since $\text{proj}_\ell \vec{v} \in \ell$ then this means:
  > $$
  > \text{proj}_\ell \vec{v} =\begin{bmatrix} x \\ y \end{bmatrix} = 
  > t \begin{bmatrix} 1 \\ 1 \end{bmatrix} + \begin{bmatrix} 3 \\ -2 \end{bmatrix}
  > = \begin{bmatrix} t+3 \\ t-2 \end{bmatrix}
  > $$
  > Combining with equation (*1) get the system of equations: 
  > $$
  > \left\{\begin{matrix}  \quad\quad 
  > x+y &= -2 \\ 
  > -t+x &= 3 \\ 
  > -t+y &= -2
  > \end{matrix}\right.
  > $$
  > Solving the system, to get $x, y$, the value of $t$ does not matter. Therefore $\text{proj}_\ell \vec{v} = \begin{bmatrix} 3/2 \\ -7/2 \end{bmatrix}$

### Projection onto sets

> ##### let $\mathcal{T} \subseteq \R^2$ be a filled in triangle with verticals $(0, 0), (1, 0), (0, 2)$ and let $\vec{a} = (1/4, 1/4), \vec{b}=(1, 1), \vec{c}=(3, 1/2)$ Find $\text{proj}_\mathcal{T} \vec{a},~ \text{proj}_\mathcal{T} \vec{b},~ \text{proj}_\mathcal{T} \vec{c}$
>
>   <img src="https://tva1.sinaimg.cn/large/008eGmZEly1gnl91evzkmj30ds0a8mxm.jpg" alt="Screen Shot 2021-02-12 at 12.04.59" style="zoom:50%;" />(Pic 1) <img src="https://tva1.sinaimg.cn/large/008eGmZEly1gnl91k9vrdj30es0biaat.jpg" alt="Screen Shot 2021-02-12 at 12.09.10" style="zoom:50%;" /> (Pic2)
>
> From the picture, $\vec{a} \in \text{proj}_\mathcal{T}$ so $\text{proj}_\mathcal{T}\vec{a} = \vec{a}$. 
>
> Then, $\vec{b}$ is closest to the hypotenuse of $\mathcal{T}$, so $\text{proj}_\mathcal{T} \vec{b}$ is the same as projection of $\vec{b}$ onto the line $y=-2x+2$, thus by doing calculations for the normal of this line,  $\text{proj}_\mathcal{T} \vec{b} = \begin{bmatrix} 3/5 \\ 4/5 \end{bmatrix}$ 
>
> Lastly, for $\vec{c}$, draw some concentric cycles (pic2), finds that it is closes to the lower-right corner, so $\text{proj}_\mathcal{T} \vec{c} = \begin{bmatrix} 1 \\ 0 \end{bmatrix}$

## Vector Components

- Let $\vec{u}$ and $\vec{v} \neq \vec{0}$ be vectors, the <u>vector component</u> of $\vec{u}$ in the $\vec{v}$ direction, written $ \text{vcomp}_\vec{v} \vec{u}$ is a vector in the direction of $\vec{v}$ so that $\vec{u} - \text{vcomp}_\vec{v} \vec{u}$ is orthogonal to $\vec{v}$
 <img src="https://tva1.sinaimg.cn/large/008eGmZEly1gnvtzjhq8lj30po0a8755.jpg" alt="Screen Shot 2021-02-12 at 12.13.35" style="zoom:30%;" />  $\vec{u} = \text{vcomp}_\vec{v} \vec{u} + (\vec{u} - \text{vcomp}_\vec{v} \vec{u})$
  
- Since by the definition, $ \text{vcomp}_\vec{v} \vec{u}$ is a vector in the direction of $\vec{v}$, then: 	 $ \text{vcomp}_\vec{v} \vec{u} = k\vec{v}$ 
  
- Since, $\vec{u} - \text{vcomp}_\vec{v} \vec{u}$ is orthogonal to $\vec{v}$ then: $\vec{v} \cdot (\vec{u} - \text{vcomp}_\vec{v} \vec{u}) = \vec{v} \cdot (\vec{u} - k\vec{v}) = \vec{v} \cdot \vec{u} - k\vec{v} \cdot \vec{v} = 0$ 
  
  - Since $\vec{v} \neq \vec{0}$ then $\vec{v} \cdot \vec{v} \neq 0$, solve for $k = \frac{\vec{v} \cdot \vec{u}}{\vec{v} \cdot \vec{v}}$, put it tougher: 
    $$
    \text{vcomp}_\vec{v} \vec{u} = 
    \left(\frac{\vec{v} \cdot \vec{u}}{\vec{v} \cdot \vec{v}} \right) \vec{v}
    $$

## **For vectors $\vec{u}$ and $\vec{v} \neq \vec{0}$, then    $\text{proj}_{\text{span}\{\vec{v}\}} \vec{u} =  \text{vcomp}_\vec{v} \vec{u}$**

- When projection onto the span of a single vector, vector components can be a computational shortcut, but if the set isn't a span, then this shortcut cannot work

> ##### Compute the projection of $\vec{a} = \begin{bmatrix} 3 \\ 7 \end{bmatrix}$ onto $\ell = \text{span} \left\{ \begin{bmatrix} 1 \\ -4 \end{bmatrix} \right\}$
>
> Let $\vec{b} = \begin{bmatrix} 1 \\ -4 \end{bmatrix}$ since $\ell = \text{span}\{\vec{b} \}$ and $\vec{b} \neq \vec{0}$, using vector components as a shortcut
> $$
> \text{proj}_\ell \vec{a} =  \text{vcomp}_\vec{b} \vec{a} = 
> \left(\frac{\vec{b} \cdot \vec{a}}{\vec{b} \cdot \vec{b}} \right) \vec{b} = 
> \frac{3-28}{1+16} \begin{bmatrix} 1 \\ -4 \end{bmatrix} = 
> \begin{bmatrix} -25/17 \\ 100/17 \end{bmatrix}
> $$