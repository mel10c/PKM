

# Divide and Conquer Algorithms

## Introduction to Divide-and-Conquer Algorithms

- <u>Divide-and-conquer algorithms</u>  - splitting the task up into subtasks can make it easier to manage

  1. Given the problem input, split it up into two or more smaller subparts with the same structure

     (Given a list to sort, *split* it up into two or more smaller lists)

  2. Recursively run the algorithm on each subpart separately

     (Recursively run the sorting algorithm on each smaller list separately)

  3. Combine the results of each recursive call into a single result, saving the original problem
     (*Combine* the sorted results of each recursive call into a single sorted lists)

## Mergesort

- <u>Mergesort</u> - first divide-and-conquer sorting algorithm (**Non-mutating** version) 
  1. Given an input list to sort, divide the input into the left half and right half
  2. Recursively sort each half
  3. Merge each sorted half together

1. First determine a base case (when can the algorithm not divide the list any further) 

   - When list has fewer than two elements

2. Recursive step, divided the list into halves, then sort each half, then **merge** it together

   - Inntuitively, we can use a similar idea as selection sort: build up a sorted list one element at a time, by repeatedly removing the next smallest element from `lst1` or `lst2`.

   | Unmerged items in `lst1` | Unmerged items in `lst2` | Comparison    | Sorted list            |
   | :----------------------- | :----------------------- | :------------ | :--------------------- |
   | `[-1, 3, 7, 10]`         | `[-3, 0, 2, 6]`          | `-1` vs. `-3` | `[-3]`                 |
   | `[-1, 3, 7, 10]`         | `[0, 2, 6]`              | `-1` vs. `0`  | `[-3, -1]`             |
   | `[3, 7, 10]`             | `[0, 2, 6]`              | `3` vs. `0`   | `[-3, -1, 0]`          |
   | `[3, 7, 10]`             | `[2, 6]`                 | `3` vs. `2`   | `[-3, -1, 0, 2]`       |
   | `[3, 7, 10]`             | `[6]`                    | `3` vs. `6`   | `[-3, -1, 0, 2, 3]`    |
   | `[7, 10]`                | `[6]`                    | `7` vs. `6`   | `[-3, -1, 0, 2, 3, 6]` |
   | `[7, 10]`                | `[]`                     | N/A           | `[-3, -1, 0, 2, 3, 6]` |

   - Then, simply concatenate the sorted list with the unmerged items from the remaining list, as the latter will all be `>=` the former. So the final result is `[-3, -1, 0, 2, 3, 6] + [7, 10]`, yielding the merged sorted list.

- The *important* part is the helper merge function

  ```python
  def _merge(lst1: list, lst2: list) -> list:
      """Return a sorted list with the elements in lst1 and lst2.
  
      Preconditions:
          - is_sorted(lst1)
          - is_sorted(lst2)
  
      >>> _merge([-1, 3, 7, 10], [-3, 0, 2, 6])
      [-3, -1, 0, 2, 3, 6, 7, 10]
      """
      i1, i2 = 0, 0
      sorted_so_far = []
  
      while i1 < len(lst1) and i2 < len(lst2):
          # Loop invariant:
          # sorted_so_far is a merged version of lst1[:i1] and lst2[:i2]
          assert sorted_so_far == sorted(lst1[:i1] + lst2[:i2])
  
          if lst1[i1] <= lst2[i2]:
              sorted_so_far.append(lst1[i1])
              i1 += 1
          else:
              sorted_so_far.append(lst2[i2])
              i2 += 1
  
      # When the loop is over, either i1 == len(lst1) or i2 == len(lst2)
      assert i1 == len(lst1) or i2 == len(lst2)
  
      # In either case, the remaining unmerged elements can be concatenated to sorted_so_far.
      if i1 == len(lst1):
          return sorted_so_far + lst2[i2:]
      else:
          return sorted_so_far + lst1[i1:]
  ```

```python
def mergesort(lst: list) -> list:
    """Return a new sorted list with the same elements as lst.

    This is a *non-mutating* version of mergesort; it does not mutate the input list.
    """
    if len(lst) < 2:
        return lst.copy()  # Use the list.copy method to return a new list object
    else:
        # Divide the list into two parts, and sort them recursively.
        mid = len(lst) // 2
        left_sorted = mergesort(lst[:mid])
        right_sorted = mergesort(lst[mid:])

        # Merge the two sorted halves. Using a helper here!
        return _merge(left_sorted, right_sorted)
```

### Running-time analysis

-  First we need to analyse the structure of the recursive calls made. 
  - At the start of the list of length $n$, where $n > 1$. (For simplicity, assume $n$ is a power of 2)
  - In the recursive step, divide the list, each sublist has length of $\frac{n}{2}$, then recurse on each one. Then this would result in a length of $\frac{n}{4}$
  - Following this pattern, for each call to `mergesort` with a list of length $\frac{n}{2^k}$ for some $k \in \N$, get 2 resultant sublist of length $\frac{n}{2^{k+1}}$. The base case is reached when the call has a list length of 1
-  For non-recursive running time. Consider a list `lst` with length $n$, where $n \ge 2$, assume $n$ is power of 2 (ignores floors and ceilings)
   -  The IF condition check `len(lst) < 2` and the calculation fo `mid` takes constant time
      - If $n < 2$ base case executes, which is constant time
   -  List slicing operations`lst[:mid]` and `list[mid:]` takes time proportional tot he length of the slice, which is $\frac{n}{2}$
   - So in the recursive step, `left_sorted` and `right_sorted` each have some $\frac{n}{2}$, running time of `_merge` is then $\frac{n}{2} + \frac{n}{2} = n$ steps
   - So the total is $1 + \frac{n}{2} + \frac{n}{2} + n = 2n + 1$ where $n \ge 2$

#### Putting it together

<img src="https://tva1.sinaimg.cn/large/008eGmZEly1gpbk4z7qnrj30ny0g3mxg.jpg" alt="mergesort-recursion-tree-full" style="zoom:38%;" />

1. The initial `mergesort` call on a list of length $n$ takes $n$ steps
2. Each of the recursive calls on a list of length $\frac{n}{2}$ takes $\frac{n}{2}$ steps. Then each of the call on a list of length $\frac{n}{4}$ takes $\frac{n}{4}$ steps
3. This pattern continues, until reach the base case, which takes 1 step

- Adding up all the numbers (key observation, each *level* in the tree has nodes with the same running time, and since this is binary tree, the number of nodes at any depth is easy to find)
  - At depth $d$ in the tree, there are $2^d$ nodes, and each node contains the number $\frac{n}{2^d}$
  - When adding the nodes at at each depth , get $2^d \cdot \frac{n}{2^d}=n$. 
  - In other words, ***each level* in the tree, it has the same total running time**
- There are a total of $\log_2 (n)+1$ levels in total. Get the total running then is $n \cdot (\log_2 (n)+1$
- **This result in $\Theta(n \log n)$,** this is much better then worst case  $\Theta(n^2)$ for selection and insertion sort

## Quicksort

- <u>Quicksort</u> - second divide-and-conquer sorting algorithm (**Non-mutating** version) 
  1. First pick one one element from the input list, which we call the **pivot**. Then, we split up the list into two parts: the elements less than or equal to the pivot, and those greater than the pivot. This is traditionally called the *partitioning* step.
  2. Next, we sort each part recursively.
  3. Finally, we concatenate the two sorted parts, putting the pivot in between them.

```python
def quicksort(lst: list) -> list:
    """Return a sorted list with the same elements as lst.

    This is a *non-mutating* version of quicksort; it does not mutate the
    input list.
    """
    if len(lst) < 2:
        return lst.copy()
    else:
        # Divide the list into two parts by picking a pivot and then partitioning the list.
        # In this implementation, we're choosing the first element as the pivot, but
        # we could have made lots of other choices here (e.g., last, random).
        pivot = lst[0]
        smaller, bigger = _partition(lst[1:], pivot)

        # Sort each part recursively
        smaller_sorted = quicksort(smaller)
        bigger_sorted = quicksort(bigger)

        # Combine the two sorted parts. No need for a helper here!
        return smaller_sorted + [pivot] + bigger_sorted
```

- Using a helper partition function

  ```python
  def _partition(lst: list, pivot: Any) -> tuple[list, list]:
      """Return a partition of lst with the chosen pivot.
  
      Return two lists, where the first contains the items in lst
      that are <= pivot, and the second contains the items in lst that are > pivot.
      """
      smaller = []
      bigger = []
  
      for item in lst:
          if item <= pivot:
              smaller.append(item)
          else:
              bigger.append(item)
  
      return (smaller, bigger)
  ```

### Running time analysis

- The non-recursive part of `quicksort` is $\Theta(n)$, where $n$ is the length of the input list. (This for the list slicing part, other statements takes constant time)

- `quicksort` also always makes two recursive calls, on its two partitions. (Also result in binary tree)

- However, the two partitions does not always have the same length, it **depends of the choice of pivot** 

  - If pivot is median of the list, 2 partitions has a size $\frac{n}{2}$, which results in $\Theta(n \log n)$ (**minimum**)

  - If the pivot is the smallest element, then the `smaller` partition has no elements whereas the `bigger` partition have all remaining of $n-1$ elements. (This is the **maximum** running time)

     <img src="https://tva1.sinaimg.cn/large/008eGmZEly1gpbkhrxrwnj30me0jk0t1.jpg" alt="quicksort-unbalanced-tree" style="zoom:38%;" /> $\left(\sum_{i = 1}^n  i\right) + (n-1) = \frac{n(n+1)}{2} + n-1 
    \Rightarrow \Theta(n^2)$

  - **This means `quicksort` has a running time range from $\Theta(n \log n)$ to $\Theta(n^2)$**

## Mergesort vs. Quicksort

- Both mergesort and quicksort are recursive sorting algorithms based on the *divide-and-conquer* paradigm.
  - For mergesort, the “divide” step is simple, since the input list is simply split in half. **The “combine” step is the hard part**, where we use a clever `_merge` helper to merge the two sorted lists together.
  - For quicksort, **the “divide” step is the complex one**, where the input list is partitioned into two parts based on comparing the items to a chosen pivot value. But once that’s done, the “combine” step is simple: we cna just concatenate the results.
- The asymptotic Theta notion simplifies the running-time analysis, which also *flattens* the reported running times.
  - In practice, an *in-place* implementation of quicksort can be significantly faster than mergesort
  - For most inputs, quicksort has “smaller constants” than mergesort, and performs fewer primitive machine operations than mergesort does.
  - **Simply put, for most inputs quicksort is faster than mergesort, even though its worst-case running time is larger.**

> **What sorting algorithm do Python’s built-in `sorted` and `list.sort` functions use?!****
>
> It turns out that Python uses a sorting algorithm known as [**Timsort**](https://en.wikipedia.org/wiki/Timsort), which was invented by Tim Peters in 2002 specifically for the Python programming language. You might be disappointed that we didn’t cover that algorithm in this course, but in fact, Timsort is essentially a highly optimized version of mergesort. Timsort uses the same basic idea of merging sorted sublists, but does so in a much smarter and more efficient way than our `mergesort` implementation, and adds a few tweaks based on empirical tests. One of those tweaks is switching to *insertion sort* to sort small sublists, which again reveals how our asymptotic worst-case running time doesn’t tell the full story.