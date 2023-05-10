---
title: "MAT223: 2_Vector, Lines, and Planes"
tags: [Note]
date: [2021-01-31]
---

# Vectors, Lines, and Planes

## Row Reduction (Gauss-Jordan Elimination)

> Augmented matrix: $\begin{bmatrix}
>  1 & 2 & 1 & 0\\
>  2 & 3 & 1 & 1\\
>  3 & 1 & 2 & 0
> \end{bmatrix}$ from the System: $\left\{\begin{matrix} & x+2y+z = 0 \\ 
> & 2x+3y+z = 1 \\ 
> & 3x+y+2z = 0\end{matrix}\right.$  

- First phase: **work down from top, from left from right**

  - Top row stays the same (as the tool row) that contains the pivot column

  > $\begin{bmatrix}
  >  1 & 2 & 1 & 0\\
  >  0 & -1 & -1 & 1\\
  >  0 & -5 & -1 & 0
  > \end{bmatrix}$ $Row 2 - 2 \cdot Row1 \\
  > Row3 - 3 \cdot Row1$ 
  >
  > $\begin{bmatrix}
  >  1 & 2 & 1 & 0\\
  >  0 & -1 & -1 & 1\\
  >  0 & 0 & 4 & -5
  > \end{bmatrix}$ $ (-)\\
  > Row3 - 5 \cdot Row2$ 

- Pause to figure out if there is inconsistent cases 

  - $[0~ 0~ 0~ -5]$ For the last row would give ***no solution***
  - $[0~ 0~ 0~ 0]$ Would give ***many solutions***
  - Or else, there is a ***single solution***

  > $\begin{bmatrix}
  >  1 & 2 & 1 & 0\\
  >  0 & 1 & 1 & -1\\
  >  0 & 0 & 1 & -5/4
  > \end{bmatrix}$ $ (-)\\
  > \frac{1}{4} $ 

- Second phase: **work from bottom up, left to right (use last row as tool row)**

  > $\begin{bmatrix}
  >  1 & 2 & 0 & 5/4\\
  >  0 & 1 & 0 & 1/4\\
  >  0 & 0 & 1 & -5/4
  > \end{bmatrix}$ $\begin{matrix}
  >   Row1 - Row3 \\
  >   Row2 - Row3 \\
  >   \
  > \end{matrix}$
  >
  > $\begin{bmatrix}
  >  1 & 0 & 0 & 3/4\\
  >  0 & 1 & 0 & 1/4\\
  >  0 & 0 & 1 & -5/4
  > \end{bmatrix}$ $\begin{matrix}
  >   Row1 - 2 \cdot Row2 \\
  >   \ \\
  >   \
  > \end{matrix}$

  >  $\left\{\begin{matrix} & x = 3/4 \\ 
  > & y = 1/4 \\ 
  > & z = -5/4\end{matrix}\right.$  As the solution of this system of equations

## Vector Lines

- Let $\ell$ be a line and let $\vec{d}$ and $\vec{p}$ be vectors (needs 2 distinct vectors)

  $$
  \ell = \{\vec{x} \mid \vec{x} = t\vec{d} + P~ \text{for some}~ t \in \mathbb{R} \}
  $$

- The vector equation: 
  $$
  \vec{x} = t\vec{d} + \vec{p}~~ \text{where}~ t \in \R
  $$

- $\vec{d}$ Is the **directional vector** for $\ell$, "*for some*" indicates that the **parameter variable** $t$ would be different, but *specific* for each line.

  - $\forall$ This would make the statement false because x cannot be the same for all t in R

- Parameter variable is a dummy variable, does not need to solve it. But if if appears in 2 different vector forms, it **doesn't mean they are equal**

  - Use different parameter variable when comparing different vector forms

- $\left\{\begin{matrix} & \vec{x} = t \vec{d} + \vec{p} \quad \text{for some} \quad t \in \mathbb{R} \\ 
  & \vec{x} = t \vec{d} + \vec{p} \quad \text{for all} \quad t \in \mathbb{R}\end{matrix}\right.$     $\begin{matrix}
    \text{are either True or False} \\
    \text {they did not specify}~ \ell~ \text{in vector form}
  \end{matrix}$

- Vector lines is a **set**, but a vector (it contains many vectors). Vector form is a shorthand for a set, but it is not equivalent to a set

  - Therefore for two vector lines to be equal, iff $\ell_1 \subseteq \ell_2~ \and~ \ell_2 \subseteq \ell_1$ is True

  > ##### Show $\ell_1 $ and $\ell_2$ are the same line (vector forms $\vec{x}=t\begin{bmatrix} 1 \\ 1 \end{bmatrix} + \begin{bmatrix} 2 \\ 1 \end{bmatrix}$  and $\vec{x} = t\begin{bmatrix} 2 \\ 2 \end{bmatrix} + \begin{bmatrix} 4 \\ 3 \end{bmatrix}$ )
  >
  > WTS: $\forall \vec{x} \in \ell_1 \Rightarrow \vec{x} \in \ell_2$ (in another words, if $\ell_1 = \ell_2$ always has a solution)
  >
  > Set parameter variables as $t$ and $s$
  >
  > $$
  > t\begin{bmatrix} 1 \\ 1 \end{bmatrix} + 
  > \begin{bmatrix} 2 \\ 1 \end{bmatrix} = \vec{x} = 
  > s\begin{bmatrix} 2 \\ 2 \end{bmatrix} + 
  > \begin{bmatrix} 4 \\ 3 \end{bmatrix}
  > $$
  > Solving this vector equation:
  >
  > $$
  > \begin{bmatrix} -2 \\ -2 \end{bmatrix} = 
  > s\begin{bmatrix} 2 \\ 2 \end{bmatrix} - 
  > t\begin{bmatrix} 1 \\ 1 \end{bmatrix} = \quad 
  > \vec{0} \quad = (s+1 - \frac{t}{2}) 
  > \begin{bmatrix} 2 \\ 2 \end{bmatrix}
  > $$
  > Since $s$ always has a solution for any $t$ AND $t$ always has a solution for any $s$, $\ell_1$ and $\ell_2$ is equal

## Vector Form in Higher Dimensions

- <u>Skew</u> - lines that does not intersect even if their directional vectors are different
- <u>Overdetermined system</u> - there are **more** equations than the number of unknown variables
- <u>Underdetermined system</u> - there are **less** equations than the number of unknown variables

### Vector Plane

- Needs **3 distinct points which are not on the same line** to define a plane

- For some vectors $\vec{d}_1$ and $\vec{d}_2$ and point $\vec{p}$
  $$
  \mathcal{P} = \{\vec{x} \mid \vec{x} = t\vec{d}_1 + s\vec{d}_2 + \vec{p}~ 
  \text{for some}~ t,s \in \mathbb{R} \}
  $$

- $\vec{d}_1$ And $\vec{d}_2$ are both the directional vectors for $\mathcal{P}$, extended out of the same point

- $\vec{x} = t\vec{d}_1 + s\vec{d}_2 + A \quad = \quad
  t(\overrightarrow{AB}) + s(\overrightarrow{AC}) + A \quad = \quad t(\vec{b} - \vec{a}) + s(\vec{c} - \vec{a}) + \vec{a}$

  > ##### Find the Line of Intersection between $\mathcal{P}_1$ and $\mathcal{P}_2$ with planes: $\vec{x} = t\begin{bmatrix} 1 \\ 1 \\0 \end{bmatrix} + s\begin{bmatrix} -1 \\ 0 \\1 \end{bmatrix} + \begin{bmatrix} 1 \\ 2 \\3 \end{bmatrix}$ And $\vec{x} = t\begin{bmatrix} -1 \\ 0 \\ 2 \end{bmatrix} + s\begin{bmatrix} 1 \\ 2 \\ 1 \end{bmatrix} + \begin{bmatrix} 0 \\ 0 \\ 3 \end{bmatrix}$
  >
  > Line of Intersection means that $\mathcal{P}_1 = \mathcal{P}_2$, and set the parameter variables as $t, s$ and $n, m$ 
  >
  > $$
  > \vec{x} = \quad \begin{bmatrix} 1 \\ 2 \\ 0 \end{bmatrix} = 
  > -t\begin{bmatrix} 1 \\ 1 \\ 0 \end{bmatrix} -
  > s\begin{bmatrix} -1 \\ 0 \\ 1 \end{bmatrix} +  
  > n\begin{bmatrix} -1 \\ 0 \\ 2 \end{bmatrix} + 
  > m\begin{bmatrix} 1 \\ 2 \\ 1 \end{bmatrix}
  > $$
  > Equivalent to the system: 
  >
  > $\left\{\begin{matrix} 
  > & -n+m-t+s &= 1 \\ 
  > & \quad ~~2m-t \quad &= 2 \\ 
  > & 2~n+~m \quad~~ -s &= 0  \end{matrix}\right.$          Thus:         $\begin{bmatrix} t \\ s \\ n \\m \end{bmatrix} = \begin{bmatrix} 2(r-2) \\ r-2 \\ -1 \\r \end{bmatrix}$ 
  >
  > Substitute the values back to vector form in $\mathcal{P}_2$
  >
  > $$
  > \vec{x} = r\begin{bmatrix} 1 \\ 2 \\ 1 \end{bmatrix} + 
  > \begin{bmatrix} 1 \\ 0 \\ 1 \end{bmatrix}
  > $$
  > This is the vector form for the line of intersection between $\mathcal{P}_1$ and $\mathcal{P}_2$ 

  > ##### Describe the plan $\mathcal{P} \subseteq \R^3$ with equation $z=2x+y+3$ in vector form
  >
  > Get points on $\mathcal{P}$, 	$A=\begin{bmatrix} 0 \\ 0 \\3 \end{bmatrix} \quad 
  > B=\begin{bmatrix} 1 \\ 0 \\5 \end{bmatrix} \quad
  > C=\begin{bmatrix} 0 \\ 1 \\4 \end{bmatrix}$
  >
  > Thus, the directional vectors are,
  > $$
  > \vec{d}_1 = B-A = \begin{bmatrix} 1 \\ 0 \\2 \end{bmatrix} \quad 
  > \text{and}\quad
  > \vec{d}_2 = C-A = \begin{bmatrix} 0 \\ 1 \\1 \end{bmatrix}
  > $$
  > Since these vectors are not parallel, $\mathcal{P}$ can be expressed in vector form as
  > $$
  > \vec{x}= t\vec{d}_1 + s\vec{d}_2 = 
  > t\begin{bmatrix} 1 \\ 0 \\2 \end{bmatrix} +
  > s\begin{bmatrix} 0 \\ 1 \\1 \end{bmatrix}+
  > \begin{bmatrix} 0 \\ 0 \\3 \end{bmatrix}
  > $$

## Restricted Linear Combinations

- Sets can be restricted to display rays, segments, and different shapes
- Different shapes of vectors on the graph can be made with restricting the coefficients of their linear combinations

### Non-negative linear combination

- Let $\vec{w} = \alpha_{1}\vec{v}_{1} + \alpha_{2}\vec{v}_{2}...+\alpha_{n}\vec{v}_{n}$, it would be a **non-negative** linear combination of $\vec{v}_1, \vec{v}_2 ... \vec{v}_n$ if $\alpha_1, \alpha_2 ... \alpha_n \ge 0$ (all parameters are bigger or equal to 0)
- Vectors that can only displacing "forward"

### Convex linear combination

- Let $\vec{w} = \alpha_{1}\vec{v}_{1} + \alpha_{2}\vec{v}_{2}...+\alpha_{n}\vec{v}_{n}$ , it would be a **convex** linear combination of $\vec{v}_1, \vec{v}_2 ... \vec{v}_n$ if
  $$
  \alpha_1, \alpha_2 ... \alpha_n \ge 0 \quad 
  \land \quad \alpha_1 + \alpha_2 + ... + \alpha_n = 1
  $$

- The weighted averages of

-  vectors (the average of $\vec{v}_1, ... \vec{v}_n$ would be convex linear combination with coefficients $\alpha_i = \frac{1}{n}$)s
