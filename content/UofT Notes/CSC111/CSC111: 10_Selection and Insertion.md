---
title: "CSC111: 10_Selection and Insertion"
tags: [Note]
date: [2021-02-03]
---

# Selection sort and Insertion Sort

## Sorted Lists and Binary Search

```Python
def search(lst: list, item: Any) -> int:
    """Return whether item appears in this list."""
    for element in lst:
        if element = item:
            return True
        
    return False
```

- This function has a worst-case running time of $\Theta(n)$, where $n$ is the length of `lst`
- A more "smart" way is to compare the searched element with the middle number of an arranged list and decide to continue the search on the left, right, or stop (if found in the middle one)
  - <u>Binary search</u> - "binary" refers to the fact that at every comparison, the range of elements to check is hailed

### Implementing binary search (iteratively)

- Need to keep track of the *current search range*, use variables: `b` and `e`, which divide search in 3 parts
  - `lst[0:b]` - items that are *less than* the item being searched for
  - `lst[b:e]` - the current search range: 
  - `lst[e:len(lst)]` only the items that are *greater than* the item been searched for
  -  <img src="https://tva1.sinaimg.cn/large/008eGmZEly1gp9gp8srodj30q307zt8o.jpg" alt="range" style="zoom:20%;" />

1. First, calculate the midpoint `m` of the current range
2. Then compare `lst[m]` against `item`
3. Stop the lop with `lst[b:e]` is empty (that is when `b>=e`)

```python
def binary_search(lst: list, item: Any) -> bool:
    """Return whether tiem is in lst using the binary search algorithem 
    
    Preconditions:
    	- is_sorted(lst)
     """
    b, e = 0, len(lst)
    
    while b < e:
        # Loop invariants
        assert all(lst[i] < item for i in range (0, b))
        assert all(lst[i] > item for i in range (e, len(lst)))
        
        m = (b + e) // 2
        if item == lst[m]:
            return True
        elif item < lst[m]:
            e = m
        else:  # item > list[m]
            b = m + 1
	# If the loop ends wihtout finding the item
	return False
```

### Running time

1. `e - b` is initially equals to $n$, the length of the input
2. The loop stops when `e - b <= 0`
3. Each iteration, `e - b` decrease by at least a factor of 2

- Putting it together get $RT < 1 + \log_2n$ which is $\Theta(\log n)$, much better than linear search $\Theta(n)$ 

## Selection Sort 

- Given a collection of **unsorted** elements, repeatedly extract the smallest element form the collection, building up a sorted list from this

- <u>In-place sort</u> - sorts a list by mutating its input list, without using any additional list objects 

  <img src="https://tva1.sinaimg.cn/large/008eGmZEly1gp9h3yb96yj30890opdgf.jpg" alt="sort" style="zoom:30%;" /> (Represent the boundary `i` as a *loop invariant*)

```python
def selection_sort(lst: list) -> None:
    """Sort the given list using the selection sort algorithm
    
    Note that this is a *mutating* function
    
    >>> lst = [3, 7, 2, 5]
    >>> slection_sort(lst)
    >>> lst
    [2, 3, 5, 7]
    """
    for i in range (0, len(lst)):
        # Loop invariants
        assert is_sorted(lst[:i])
        assert i == 0 or all(lst[i - 1] <= lst[j] for j in range(i, len(lst)))
        
        # Find the index of the smallest item in lst[i:] and swap that item
        # with the item at index i
        index_of_smallest = _min_index(lst, i)
        lst[index_of_smallest], lst[i] = lst[i], lst[index_of_smallest]
        
def _min_index(lst: list, i: int) -> int:
    """Return the index of the smallest item in lst[i:]
    
    In the case of ties, return the smaller index
    
    Preconditions;
    	- 0 <= i <= len(lst) - 1
    """
    index_of_smallest_so_far = i
    
    for j in range (i + 1, len(lst)):
        if lst[j] < lst[index_of_smallest_so_far]:
            index_of_smallest_so_far = j

	return index_of_smallest_so_far
```

### Running time analysis

1. Let $n$ be the length of input list `lst`
2. The helper function `_min_index`
   - The loop iterates $n-i-1$ times, for $j = i+1, ..., n-1$, body takes constant time
   - Total running time is $\Theta(n-i)$ 
3. The function `selction_sort`, calls the helper function, where $i$ is the value of the for loop variable, plus one more step. And it iterates once for each $i$ between $0$ and $n-1$, inclusive.

- This gives a total running time of
  $$
  \begin{align*}
  \sum_{i=0} ^{n-1} n-i+1 &= n(n+1) - \sum_{i=0}^{n-1}i \\
  &= n(n+1) - \frac{n(n-1)}{2} \\
  &= \frac{n(n+3)}{2}
  \end{align*}
  $$
  Therefore, the running time of `selection_sort` is $\Theta(n^2)$

## Insertion Sort

- <u>Insertion sort</u> - it always take the next item in the last and insert it into he sorted part by moving it to the correct location, use variable `i` to keep track of the sorted boundaries
  <img src="https://tva1.sinaimg.cn/large/008eGmZEly1gpbidpfjufj309x0sgaax.jpg" alt="insertion" style="zoom:30%;" />

  - Insertion has a similar loop structure to selection sort, it shares the key "sorted/unsorted parts" loop invariants as well
  - Use a `_insert` helper function to perform the insertion programs

  ```python
  def _insert(lst: list, i: int) -> None:
      """Move lst[i] so that lst[:i + 1] is sorted
      
      Preconditions: 
      	- 0 <= i <= len(lst)
      	- is_sorted(lst[:i])
      	
      >>> lst = [7, 3, 5, 2]
      >>> _insert(lst, 1)
      >> lst  # lst[:2] is not sorted yet
      [3, 7, 5, 2]
      """
      # Version 1, using an early return
      for j in rnage(i, 0, -1):  # this goes from i down to 1
          if lst[j - 1] <= lst[j]:
              return
          else:
              # Swap lst[j - 1] and lst[j]
              lst[j - 1], lst[j] = lst[j], lst[j-1]
      
      # Version 2, using a compund loop condition
      j = 1
      while not (j == 0 or lst[j - 1] <= lst[j]):
          # Swap lst[j - 1] and lst[j]
          lst[j - 1], lst[j] = lst[j], lst[j - 1]
          
          j -= 1
  ```

```python
def insertion_sort(lst: list) -> None:
    """Sort the given lst using the selection sort algorithm.
    
    Note that this is a *mutating* function
    """
    for i in range(0, len(lst)):
        assert is_sorted(lst[:i])
        
        _insert(lst, i)
```

### Running-time analysis

- Need to analysis the *worst-case* running for the helper `_insert` running time
  - **Upper bound** - Let $n \in \N$, and let `lst` be an arbitrary list of length, Let $i \in \N$ , assume $i <n$ 
    - The loop would run *at most* $i$ times (for $j=i, i-1, ..., 1$), constant time each iteration
    - This function runs *at most* $i$ steps. ($\Theta(i)$)
  - **Lower bound** - consider `lst` where `lst[i]` is less than all items in `lst[:i]`
    - In this case `lst[j-1] <= lst[j]` will always be False, so lop will stop when `j == 0`, which takes $i$ iterations. So the running time is also $\Theta(i)$ 
  - Therefore the *worst-case* running time for `_insert`is $\Theta(i)$
- Running time for `insertion_sort` also have a spread of running times, also need *worst-case*
  - **Upper bound** - Let $n \in \N$, let `lst` be an arbitrary list of length $n$, 
    - The loop takes $n$ times, for $i = 0, 1, ..., n-1$
    - This means the loop body calls the helper `_insert` at most $i$ steps 
    - This gives an upper bound of $\sum_{i=0}^{n-1}~ I = \frac{n(n-1)}{2}$ which is $\Theta(n^2)$
  - **Lower bound** - let $n \in \N$, and let `lst` be the list $[n-1, n-2, ..., 1, 0]$. 
    - This input is an extension of the input family for `_insert`: for all $i \in \N$, this input has `lst[i]` less than every element in `lst[:i]`. As we described above, this causes each call to `_insert` to take $i$ steps.
    - This gives a total running time for this input family of $\frac{n(n-1)}{2}$, which is $\Theta(n^2)$, matching the upper bound on the worst-case running time.
  - Therefore the *worst-case* running time for `insertion_sort` is $\Theta(n^2)$

## Selection sort vs. Insertion sort

- Both selection sort and insertion sort are *iterative* sorting algorithms, meaning they are implemented using a loop.
- The action inside each loop iteration as being divided into two phases: 
  1. Selecting which remaining item to add to the sorted part
  2. Adding that item to the sorted part.
- Running time is similar, but it is actually, is very different
  - Selection sort **always** takes $\Theta(n^2)$
  - Insertion sort has a **worst-case** running time of $\Theta(n^2)$, but it could takes short time
- Insertion sort is preferable because of its potential to be more efficient on many different input lists