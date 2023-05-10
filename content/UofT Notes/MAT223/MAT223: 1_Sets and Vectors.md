# Week 1

## Sets and sets-builder notation

- <u>**Set**</u> -- An unordered collection of distinct objects
    - <u>Elements</u> -- things inside a set, use the symbol $\in$ to represent that some specific element is inside a set; and uses $\notin$ to show that the element is not inside the set
    - Sets can contain mixture of objects, and is named with capital letters
    - An <u>empty set</u> contains no elements, and is written with $\emptyset$
- Sets and Interval notation
    - Close bracket: $[a, b] = \{x \in \mathbb{R} \mid a \le x \le b\}$, Open bracket: $(a, b) = \{x \in \mathbb{R} \mid a < x < b\}$

#### Set operations

- <u>**Subsets** & Superset</u> -- if set $B$ is a subset of $A$, its written as $B \subset A$
    - $\subsetneq$ means a subset of, but maynot be equal; while $\subseteq$ means that its a set of & equal
    - In $B \subseteq A$, if all $b \in B$ and $b \in A$, then $A$ is a <u>superset</u> of $B$ 
- <u>Set equality</u> -- $A = B$ if and only if $A \subseteq B$ and $B \subseteq A$
    - *Prove*: $(\forall a \in A,  a \in B) \quad \and \quad (\forall b \in B, b \in A)$ 

#### Set-builder notation

- If $X$ is a set, define a subset: $Y = \{a \in X:\text{some rule involving}~ a\}$
- <u>Union</u> -- $X \cup Y = \{a : a \in X~ \text{or}~ a \in Y\}$
- <u>Intersection</u> -- $X \cap Y = \{a : a \in X~ \text{and}~ a \in Y\}$

## Vectors

- <u>**Vector**</u> - An **arrow** inside a coordinate system, **rooted at the origin**, associated with a **set** of coordinates
    - Vector coordinates notation: $\vec{v}=\begin{bmatrix} \alpha\\\beta \end{bmatrix}$ (column vector)
    - It models a relationship between pointsssssssss
- <u>Scalar</u> -- numbers that modules a relationship between quantities
- The $\left \| \vec{a} \right \|$ represents the magnitude of the vector $\vec{a}$ (norm of $\vec{a}$). Its a scaler
- Vectors is **not he same as a line segment** and a vector by itself has no "origin"
- Vectors and points will be treated interchangeably
- <u>Zero vector</u> -- notated as $\vec{0}$, is the vector with no magnitude
- **<u>Standard Basis Vector</u>**, the vector $\vec{e}_1$ and $\vec{e}_2$ always points ONE unit in the direction of $x$ and $y$ axis

### Vector addition

- **Adding from top to tail**
  $$
  \vec{v} + \vec{u} = \vec{w}
  $$

- ![](https://www.math24.net/wp-content/uploads/2019/02/vector-addition.svg)
  $$
  \vec{OP} + \vec{OQ} = \begin{bmatrix} a \\ b \end{bmatrix} + \begin{bmatrix} c \\ d \end{bmatrix} 
  = \begin{bmatrix} ac \\ bd \end{bmatrix}
  $$

### Scaler multiplication

- **Multiplying by a number that scales the vector (stretch or compresses the vector)**

- Since the scaler coefficient increase the magnitude of the vector, therefore scaling the vector means multiplying each element of the vector set by that scaler
- $$-2\vec{OP} = -2 \begin{bmatrix} a \\ b \end{bmatrix} = \begin{bmatrix} -2a \\ -2b \end{bmatrix}$$
> `Answer question from lecture`
>
> $$\begin{bmatrix} a \\ b \end{bmatrix} + \begin{bmatrix} c \\ d 	\end{bmatrix} 
>      = \begin{bmatrix} ac \\ bd \end{bmatrix}$$
>
> - The vector would first move `a` spaces horizontally, **plus** `c` spaces horizontally, results as moving `ac`  units horizontally. After that, from that resultant point, the vector would now move `b` spaces vertically **plus** another `d` spaces verticallyl. The final result will then be `bd` spaces vertically in total

### <u>Linear Combination</u>

$$
\vec{w} = \alpha_{1}\vec{v}_{1} + \alpha_{2}\vec{v}_{2}...+\alpha_{n}\vec{v}_{n}
$$

- Linear combination vs union. 
  - Linear combination of **sum of vectors multiplied by some scaler** from $\mathbb{R}^2$, while union is just a *combination* of existing vectors, without any mutation with the vectors 
- The scalars are called the <u>coefficients</u> for the linear combination
- The vector is always a linear combination of vectors from any non-empty set.
  - $\forall S \neq \empty,~ \exist~ \vec{v}~ \text{s.t.}~ \vec{v}~ \text{is a linear combination of}~ S$
- Every vector in $\mathbb{R} ^{2}$ can be written uniquely as a linear combination of any two non-identical vectors
  - $\vec{v} = \alpha \vec{e}_1 + \beta \vec{e}_2$

> #### Example Question
>
> *We denote the restriction on the **hover board’s** movement by the vector $\begin{bmatrix} 3\\1 \end{bmatrix}$. By this we mean that if the hover board traveled “forward” for one hour, it would move along a “diagonal” path that would result in a displacement of **3 km East and 1 km North** of its starting location.*
>
> *We denote the restriction on the **magic carpet’s** movement by the vector $\begin{bmatrix} 1\\2 \end{bmatrix}$. By this we mean that if the magic carpet traveled “forward” for one hour, it would move along a “diagonal” path that would result in a displacement of **1 km East and 2 km North** of its starting location.*
>
> *Uncle Cramer tells you that Old Man Gauss lives in a cabin that is **107 km East and 64 km North** of your home.*
>
> **Task: Investigate whether or not you can use the hover board and the magic carpet to get to Gauss’s cabin. If so, how? If it is not possible to get to the cabin with these modes of transportation, why is that the case?**
>
> > `1. Translate the problem into math equations`
> >
> > Hover Board: $\begin{bmatrix} 3\\1 \end{bmatrix}$;  Magic Carpet: $\begin{bmatrix} 1\\2 \end{bmatrix}$;  Target Requires: $\begin{bmatrix} 107\\64 \end{bmatrix}$
> > 
> > Since Target cannot be divided equally among any single of the tools, therefore a combination is required to finish the task
>
> 
>
> > 2. `Set variables`
> >
> > let $x$ be the time spend on the hover board; let $y$ be the time spend on the magic carpet
>
> 
>
> > 3. `Create equations`
> >
> > According to vector's addition, 
> > $(\vec{board}) + (\vec{carpet}) =
> > \begin{bmatrix} 3\\1 \end{bmatrix} + \begin{bmatrix} 1\\2 \end{bmatrix}$
> > therefore:
> >
> > $$\begin{bmatrix} 3x \\ x \end{bmatrix} + \begin{bmatrix} y \\ 2y \end{bmatrix} 
> > = \begin{bmatrix} 107 \\ 64 \end{bmatrix}$$
>
> 
>
> > 4. `Solve the algebra`
> >
> > $$3x+y=107$$
> > $$y=107-3x$$
> > sub. in to the second equation
> > $$x+2(107-3x) = 64 $$
> > $$x=30$$
> >
> > sub. back to the first equation
> > $$(30) + 2y = 64$$
> > $$y=17$$
>

## Solving Systems

- <u>System of equations</u> -- a list of equations with common variables

  > $\left\{\begin{matrix} & x + 2y = 9 \\ 
  > & 3x + 5y = 20 \end{matrix}\right.$

- <u>Solution</u> -- a list of values, one for each variable, that satisfy every equation at once

  > $\left\{\begin{matrix} & (-5) + 2(7) = 9 \\ 
  > & 3(-5) + 5(7) = 20 \end{matrix}\right.$
  >
  > Therefore $x=-5$ and $y=7$ is a solution to this system of equations

##### Ways of solving equations

- <u>Substitution</u> -- isolate variables and substitute into reminding equations
- **<u>Elimination</u>** -- eliminate variables by adding multiples of one equation to another

    - The main method used in Linear Algebra

    > 1. Subtract $3~eq_1$ from $eq_2$:  $\left\{\begin{matrix} & x + 2y = 9 \\ 
    >    & (3x + 5y)-3(x+2y) = 20-3(9) \end{matrix}\right.$  = $\left\{\begin{matrix} & x + 2y = 9 \\ 
    >    & -y=-7 \end{matrix}\right.$ 
    >
    > 
    >
    > 2. Multiply $eq_2$ by $-1$:  $\left\{\begin{matrix} & x + 2y = 9 \\ 
    >    & (-1)(-y) = (-1)(-7) \end{matrix}\right.$ = $\left\{\begin{matrix} & x + 2y = 9 \\ 
    >    & y = 7 \end{matrix}\right.$
    >
    > 
    >
    > 3. Subtract $2~ eq_2$ from $eq_1$:  $\left\{\begin{matrix} & (x + 2y)-2(y) = 9-2(7) \\ 
    >    & y=7 \end{matrix}\right.$ = $\left\{\begin{matrix} & x= -5 \\ 
    >    & y=7 \end{matrix}\right.$ 

### Consistency of Linear Equations

- <u>Consistent</u> -- the system has **at least one solution** (example above is consistent)

  > $\left[\begin{array}{rr|r}
  >     1 & 0 & 7 \\
  >     0 & 1 & -2 
  >     \end{array}\right]$, $\left[\begin{array}{rr|r}
  >     1 & 0 & 8 \\
  >     0 & 1 & 10 \\ 
  > 	0 & 0 & 0 
  > \end{array}\right]$ These system has an unique solution
  >
  > $\left[\begin{array}{rrr|r}
  >     1 & 0 & 0 & 0 \\
  >     0 & 0 & 1 & -11 
  >     \end{array}\right]$ This system has infinitely man y solutions

- <u>**Inconsistent**</u> -- the system has **no solution** or infinitely many solutions

  > $\left[\begin{array}{rrr|r}
  >     1 & 0 & -15 & 0 \\
  >     0 & 1 & 0 & 0 \\ 
  > 	0 & 0 & 0 & 1 \\ 
  > 	0 & 0 & 0 & 0 \\ 
  >     \end{array}\right]$ This system has no solution