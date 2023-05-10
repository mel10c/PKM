# Induction and Recursion

## Proof by Induction

<img src="https://tva1.sinaimg.cn/large/008eGmZEly1gnq194pfj6j318e0omwhy.jpg" alt="Screen Shot 2021-02-16 at 15.27.01" style="zoom:35%;" />

- The induction principle applies to **universal** statements over the **natural** numbers 

  - Using chain of implications

- The <u>base case</u> is a poof that the stamens is *True* for the first natural number $n=0$, i.e. prove that $P(n)$ holds

- The <u>inductive step</u> is a poof that for all $k \in \mathbb{N}$ if $P(k)$ is *True* then $P(k+1)$ is also *True*
  $$
  \forall k \in \mathbb{N},~ P(k) \quad \Rightarrow \quad P(k+1)
  $$

  > ##### Prove that $\forall n \in \mathbb{N},~ f(n) = \frac{n(n+1)}{2}$
  >
  > *Proof*. Prove this statement by induction on $n$
  >
  > - <u>Base case</u>: Let $n=0$, then
  >   $f(0) = \sum_{i=0}^0 i =0$ And, $\frac{0(0+1)}{2} = 0$. This proves the two sides of the equation are equal
  >
  > - <u>Induction step</u>: Let $k \in \N$ and assume that $f(k) = \frac{k(k+1)}{2}$. WTS that $f(k+1)=\frac{(k+1)(k+2)}{2}$  
  >   $$
  >   \begin{align*}
  >   f(k+1) &= \sum^{k+1}_{i=0} i \tag{defintion of $f$} \\
  >   &= \left(\sum^k_{i=0} i \right) + (k+1) \tag{taking out last term} \\
  >   &= f(k) + (k+1) \tag{definition of $f$} \\
  >   &= \frac{k(k+1)}{2} + (k+1) \tag{by the I.H} \\
  >   &= \frac{(k+1)(k+2)}{2}
  >   \quad \quad \quad \blacksquare
  >   \end{align*}
  >   $$

## Recursively-Defined Functions

$$
\forall k \in \N,~ f(k+1) = f(k) + (k+1) \quad \Leftrightarrow \quad
\begin{cases}
   0,&\text{ if } n=0 \\
   f(n-1) +n &\text{ if } n>0
\end{cases}
$$

```python
def f(n: int) -> int:
    """Return the sum of the numbers between 0 and n, inclusive.
    
    Preconditions:
    	- n >= 0
    
    >>> f(4)
    10
    """
    if n == 0:  # base case
        return 0
    else:  # recursie step
        return f(n - 1) + n
```

- <u>Recursive</u> definition (self-referential definition) - $f$ is defined in terms of itself 

  - The term <u>recursive call</u> is used to describe the inner `f(n-1)` call 
  - <u>Recursive step</u> is the step that contains the recursive call
  - Recursive function are not limited to going "from $n$ to $n-1$", its valid as long as it always uses "smaller" argument values to the function in the recursive call

  > ##### The Euclidean algorithm as recursive functions
  >
  > Use $\gcd(a, b)=\gcd(b, a\%b)$ plus the fact that $\gcd(a, 0)=a$ for all $a\in \N$, get
  > $$
  > \begin{cases}
  >    a,&\text{ if } b=0 \\
  >    \gcd(b, a\%b) &\text{ if } b>0
  > \end{cases}
  > $$
  > Translate the recursive function into python
  >
  > ```python
  > def euclidean_gcd_rec(a: int, b: int) -> int:
  >     """Return the gcd of and b(using recursion!)
  >     
  >     Preconditions:
  >     	- a >= 0 and b>= 0
  >     """
  >     if b == 0:
  >         return a
  >     else: 
  >         return euclidean_gcd_rec(b, a % b)
  > ```

## Nested Lists

- When performing operation in nested lists, it is hard to write a uniform function using `for loops` that works for random nested layers of lists

- <u>Nested list of integers</u> as one of two types of values

  - For all $n \in \N$, the single integer $n$ is a nested list of integers
  - For all $k \in \N$ and nested lists of integers $a_0, a_1 \dots, a_{k-1}$, the list $[a_0, a_1 \dots, a_{k-1}]$ is also a nested list of integers
    - Each of the $a_i$ is called a <u>sublist</u> of the outer list

  $$
  nested\_sum(x) =
  \begin{cases}
     x,&\text{ if } x \in \Z \\
     \sum_{i=0}^{k-1}nested\_sum(a_i) &\text{ if } x=[a_0, a_1 \dots, a_{k-1}]
  \end{cases}
  $$

### Recursive function design recipe for nested lists

1. Write a doctest example for the *base case* of the function (when function called on `int` value)

2. Write a doctest example for the *recursive step* of the function

   - Pick a nested list with around 3 sublists AND another sublist is a `list` that contains other lists
   - Show the correct return value of the function for this input nested list

3. Use the following *nested list recursion code template* to follow the recursive structure of nested list

   ```python
   def f(nested_list: Union[int, list]) -> ...:
       if isinstance(nested_list, int):
           return (...)
       else:
           accumulator = (...)
           
           for sublist in nested_list:
               rec_value = f(sublist)
               accumulator = (...) accumulator (...) rec_value (...)
               
           return accumulator
   ```

4. Implement the function's base case, using the first doctest example to test

5. Implement the function's recursive step 

   - Use the second doctest example to write down the relevant sublists and recursive function calls. Fill the recursive call output based on the function specification, not any code you wrote
   - Analyse the output of the recursive calls and determine how to combine them to return the correct value of original call

## Recursive List

```python
class RecursiveList:
    """A recursive implementation of the List ADT.
    
    Representation Invariants:
    	- (self._first is None) == (self._rest is None)
    """
    # Private Instance Attributes:
    #	- _first: The first item in the list, or None if this list is empty
    #	- _rest: A list contianing the items that come after the first one, 
    #			 or None if this list is empty
    _first: Optional[Any]
    _rest: Optional[RecursiveList]
        
    def __init__(self, first: Optional[Any], rest:Optional[RecursiveList]) -> None:
        """Initialize a new recursive list."""
        self._first = first
        self._rest = rest
```

- Recursive definition of list

  - The empty list `[]` is a list

  - If `x` is a value and `r` is a list, then a new list `lst` whose first element is `x` and whose other elements are the elements of `r` can be constructed

    - `x` is the **first** element of `lst` and `r` the **rest** of `lst`

    ```python
    [1, 2, 3, 4] == ([1] + ([2], [3], [4], []))
    ```

  > ##### Calculating the sum of a list of integers
  >
  > - Let `lst` be an empty list, then its sum is $0$
  > - Let `lst` be an non-empty list of integers. Decompose: first element $x$ and rest of its element $r$. 
  >
  > $$
  > sum(lst) = 
  > \begin{cases}
  >    0, &\text{ if } lst \text{ is empty} \\
  >    (\text{first of }lst) + sum(\text{rest of }lst) 
  >    &\text{ if } lst \text{ is non-empty }
  > \end{cases}
  > $$
  >
  > Translate into python using `RecursiveList` class
  >
  > ```python
  > class RecursiveList:
  >     def sum(self) -> int:
  >         """Return the sum of the elements in this list.
  >         
  >         Preconditions:
  >         	- every element in this list is an int
  >         """
  >         if self._first is None:  # Base Case
  >             return 0
  >         else:
  >             return self._first + self._rest.sum()
  > ```

- `RecursiveList` and `_Node` classes have the same structure (`_Node` is a recursive class as well)

> ## Application: Fractals
>
> - <u>Fractal</u> - geometric figure that has been defined recursively (A figure that can be split into parts, each of which is a smaller copy of the original)
>
> - <u>The Sierpinski Triangle</u> - has the shape of an **equilateral triangle,** **subdivided into 4** smaller and congruent equilateral triangles. The smaller triangle in the **centre is "empty"**, while the **remaining smaller triangles are themselves smaller Sierpinski Triangles**
>
>   <img src="https://tva1.sinaimg.cn/large/008eGmZEly1gnq47l9zevj30m80m8q3d.jpg" alt="step2-og" style="zoom:25%;" /><img src="https://tva1.sinaimg.cn/large/008eGmZEly1gnvu0hvcasj30m80m80t3.jpg" alt="step3-og" style="zoom:25%;" /><img src="https://tva1.sinaimg.cn/large/008eGmZEly1gnq47pjgeij30m80m8q4b.jpg" alt="step4-og" style="zoom:25%;" />
>
> ### `pygame`
>
> - `pygame.Surface` object represents the surface to draw the given object
> - The origin of the coordinate system of `pygame`  is located in the top left corner
>   <img src="https://tva1.sinaimg.cn/large/008eGmZEly1gnq43aw5kij30ce0camxk.jpg" alt="Screen Shot 2021-02-16 at 17.05.29" style="zoom:25%;" />
>
> ### Implication
>
> <img src="https://tva1.sinaimg.cn/large/008eGmZEly1gnq48vdl6cj315d0u0my8.jpg" alt="labeled_vertices" style="zoom:15%;" />
>
> - Key insight: the side length of the triangle decreases by a factor of 2 at each call (use *midpoints*)
>
> ```python
> import pygame
> 
> # Define some colours using their RGB values
> FOREGROUND = (255, 113, 41)
> BACKGROUND = (46, 47, 41)
> 
> # The minimum number of pixels in the Sierpinski triangle
> MIN_SIDE = 3
> 
> 
> def sierpinski(screen: pygame.Surface, v0: tuple[int, int], v1: tuple[int, int],
>                v2: tuple[int, int]) -> None:
>     """Draw a Sierpinski Triangle on the given screen, with the given vertices.
> 
>     Each of v0, v1, and v2 is an (x, y) tuple representing a vertex of the triangle.
>     v0 is the lower-left vertex, v1 is the upper vertex, and v2 is the lower-right vertex.
>     """
>     if v2[0] - v0[0] < MIN_SIDE:
>         pygame.draw.polygon(screen, FOREGROUND, [v0, v1, v2])
>     else:
>         pygame.draw.polygon(screen, FOREGROUND, [v0, v1, v2])
> 
>         mid0 = midpoint(v0, v1)
>         mid1 = midpoint(v0, v2)
>         mid2 = midpoint(v1, v2)
> 
>         # Draw centre "sub-triangle"
>         pygame.draw.polygon(screen, BACKGROUND, [mid0, mid1, mid2])
> 
>         # Recursively draw other three "sub-triangles"
>         sierpinski(screen, v0, mid0, mid1)
>         sierpinski(screen, mid0, v1, mid2)
>         sierpinski(screen, mid1, mid2, v2)
> 
> 
> def midpoint(p1: tuple[int, int], p2: tuple[int, int]) -> tuple[int, int]:
>     """Return the midpoint of p1 and p2."""
>     return ((p1[0] + p2[0]) // 2, (p1[1] + p2[1]) // 2)
> 
> 
> if __name__ == '__main__':
>     # Initialize a pygame window
>     pygame.init()
>     window = pygame.display.set_mode((800, 800))
>     window.fill(BACKGROUND)
> 
>     # Draw the Sierpinski Triangle!
>     sierpinski(window, (100, 670), (400, 150), (700, 670))
> 
>     # Render the image to our screen
>     pygame.display.flip()
> 
>     # Wait until the user closes the Pygame window
>     while True:
>         if any(event.type == pygame.QUIT for event in pygame.event.get()):
>             break
>     pygame.display.quit()
>     pygame.quit()
> ```
>
> 