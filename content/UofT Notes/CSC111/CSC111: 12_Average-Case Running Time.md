# Average-Case Running Time

- In practice worst-case running time analysis can be misleading, with a variety of algorithms having a poor worst-case performance still yet performing well on the vast majority of inputs. 

- Let `func` be a program, for each $n \in \N$, define set $I_{func, n}$ to be the set of all inputs so `func` of size $n$.

  - $$
    WC_{func}(n) = \max \{\text{running time of executing } \texttt{func}(x)~
    |~ x \in I_{func, c} \}
    $$

- **<u>Average-case running time</u>** of `func` is defined as the function $Avg_{\texttt{func}}:  \N \to \R^+$ where

  - $$
    Avg_{\texttt{func}}(n) = \frac{1}{|I_{func, n}|}~ \times ~
    \sum_{x \in I_{func, n}} \text{ running time of } \texttt{func}(x)
    $$

  - Need to precisely define "all possible inputs of length $n$" for the given function
  - For infinite set of inputs is a common problem. To resolve it, choose a particular set of allowable inputs, and compute the average running time for that set

## Perform an average-case running time analysis

- Recall the *linear search* algorithm

  ```python
  def search(lst: list, x: Any) -> bool:
      """Return whether x is in lst."""
      for item in lst:
          if item == x:
              return True
      return False
  
  ```

  - Previously seen the worst-case running time of this function is $\Theta(n)$, where $n$ is the length of the list
  - Analysis the average running time using two different input sets

### A first example

- Let $n \in \N$, choose the input set to be set of inputs where

  - `lst` is always the list `[0, 1, 2, ..., n-1]`, `x` is an integer between `0` and `n-1` inclusive

- Use $I_n$ to denote this set, for this definition, know that $|I_n| = n$, combine with the definition, get
  $$
  Avg_{\texttt{search}}(n) = \frac{1}{n}~ \times ~
  \sum_{\texttt{lst,x} \in I_n} \text{ running time of } \texttt{search(lst, x)}
  $$

- Let $x \in \{0, 1, 2, ..., n-1 \}$, this includes all possible inputs, calculate running time in terms of $x$

  - Know that there will be exactly $x+1$ loop iterations until $x$ is found in the list
  - Each iterations takes constant time, the loop in total takes $x + 1$ steps

- So for the running time of `search(lst, x)` equals $x + 1$, calculate the average running time
  $$
  \begin{align*}
  Avg_{\texttt{search}}(n) &= \frac{1}{n}~ \times ~
  \sum_{\texttt{lst,x} \in I_n} \text{ running time of } \texttt{search(lst, x)} \\
  &= \frac{1}{n} ~\times~ \sum_{x = 0}^{n-1} (x + 1) \\
  &= \frac{1}{n} ~\times~ \sum_{x' = 1}^{n} x' \tag{$x' = x + 1$} \\
  &= \frac{1}{n} ~\times~ \frac{n(n+1)}{2} \\
  &= \frac{n+1}{2}
  \end{align*}
  $$
  And so the average-case running time for `search` on **this set of input** is $\frac{n+1}{2}$ which is $\Theta(n)$

  - Only true for this *specific* choice of inputs
  - The avenge-case running is asymptotically equal to that of the worst-case for this case

### A second example: search in binary lists

- Use the same function (`search`) but choose a different input set.
- Let $n \in \N$, and let $I_n$ be the set fo inputs `(lst, x)` where
  - `lst` is a list of length $n$ that contains **only $0$'s and $1$'s** , `x = 0`
  - This case, `x` is fixed, and `lst` has multiple possibilities. 

1. **Compute the number of inputs, $|I_n|$**

   - Since `x` is always $0$, the the size of $I_n$ is equal to the number of lists of $0$'s and $1$'s of length $n$.
   - Therefore the size of $I_n$ is $2^n$, since there are $n$ independent choice for each of the $n$ elements of the lists, and each choice has two possible values.

2. **Partition the inputs by their running time**

   - For the function `search`, if `lst` has a $0$ at index $i$, then the loop will take $i + 1$ iterations. 

   - So, divide up the lists based on the index of the first $0$ in the list, and treat the list `[1, 1, ..., ]` as a special case, since it has no $0$'s.

   - Formally, for each $i \in \{0, 1, ..., n-1 \}$, define $S_{n, i} \subset I_n$ to be the set of binary lists of length $n$ where their first $0$ occurs at index $i$ 

     > - $S_{n, 0}$ Is the set of binary lists `lst` where `lst[0] == 0` 
     >   - (every element in $S_{n, 0}$ takes 1 step for `search`)
     > - $S_{n, 1}$ Is the set of binary lists `lst` where `lst[0] == 0`  and `lst[1] == 0`
     >   - Every element in $S_{n, 1}$ takes 2 steps for `search`
     > - $S_{n, i-1}$ Is the set of binary lists `lst` where `lst[j] == 1`  for all natural numbers $j<i$ and `lst[i] == 0`
     >   - ​	Every element in $S_{n, i}$ takes $i + 1$ steps for `search`

   - Define a special set $S_{n, n}$ that contains just the list `[1, 1, ..., 1]`. That input causes `search` to take $n+1$ steps: $n$ steps for the loop, and then 1 step for the `return False` at the end 

3. **Compute the size of each partition**

   - For $S_{n, 0}$

4. Using Step 2 and 3, calculate the sum of the running time for all the inputs in $I_n$

5. Using Step 1 and 4, calculate the average-case running time for $I_n$

