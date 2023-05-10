# Binary Search Trees

- Define a new abstract data type (ADT) that is an extension of the Set ADT that allows for duplicates
- <u>Multiset</u>
  - Data: an unordered collection of values, allowing duplicates
  - Operations: get size, insert a value, remove one occurrence of a specified value, check membership in the multiset
- Using `list` to implement the Multiset ADT
  - Searching would have the $RT$ of $\Theta(n)$ if simply append new items to the list
  - Using <u>binary search</u> algorithm would improve the $RT$ to $\Theta(\log n)$

## Binary Search Tree definitions

- <u>Binary tree</u> is a tree in which every item has two (possibly empty) subtrees, which are labelled its *left* and *right* subtrees.
- **Binary search tree property** - its value $\ge$ all items of *left* subtree, and $\le$ all items of *right* subtree

- <u>**Binary search tree (BST)**</u>  - **every** item in the tree satisfies the *binary search tree property*
  - As a "sorted tree", efficient at insertion and deletion while painting the softness
  - Empty case: Tree class (`_root` is None, subtrees is []), BST class (`_root`, `_left`, `_right` are all None)
  - For non-empty BST, start by assigning at the `_root`, then sort into `_left` or `_right`
    - Leaf branches refer to **empty BST (NOT refer to None)**
    - For BST, the only case for any of the attributes to be None is for it to be empty

```python
class BinarySearchTree:
    """Binary Search Tree class.
    
    Representation Invariants:
      - (self._root is None) == (self._left is None)
      - (self._root is None) == (self._right is None)
      - (BST Property) if self._root is not None, then
          all items in self._left are <= self._root, and
          all items in self._right are >= self._root
    """
    # Private Instance Attributes:
    #   - _root:
    #       The item stored at the root of this tree, or None if this tree is empty.
    #   - _left:
    #       The left subtree, or None if this tree is empty.
    #   - _right:
    #       The right subtree, or None if this tree is empty.
    _root: Optional[Any]
    _left: Optional[BinarySearchTree]
	_right: Optional[BinarySearchTree]
```

- Based on the `Tree` class, the initializer and is_empty function:

  ```python
  class BinarySearchTree:
  
      def __init__(self, root: Optional[Any]) -> None:
          """Initialize a new BST containing only the given root value.
  
          If <root> is None, initialize an empty BST.
          """
          if root is None:
              self._root = None
              self._left = None
              self._right = None
          else:
              self._root = root
              self._left = BinarySearchTree(None)   # self._left is an empty BST
              self._right = BinarySearchTree(None)  # self._right is an empty BST
  
      def is_empty(self) -> bool:
          """Return whether this BST is empty.
          """
          return self._root is None
  ```

## Search for BST

- For BSTs *the initial comparison to the root tells you which subtree you need to check*. 
  - Check if its less than the root, search on left; greater than root, search right

```python
class BinarySearchTree:
    def __contains__(self, item: Any) -> bool:
        """Return whether <item> is in this BST.
        """
        if self.is_empty():
            return False
        elif item == self._root:
            return True
        elif item < self._root:
            return self._left.__contains__(item)
        else:
            return self._right.__contains__(item)
```

## Mutating BST

### Insertion

1. If BST is empty, make the new item the root of the tree
2. Otherwise, use binary search tree property, insert into either left or right subtree as a leaf

### Deletion

- Use recursion to find the item (similar to the `contains` function)

  ```python
  class BinarySearchTree:
      def remove(self, item: Any) -> None:
          """Remove *one* occurrence of <item> from this BST.
  
          Do nothing if <item> is not in the BST.
          """
          if self.is_empty():
              pass
          elif self._root == item:
              self._remove_root()  # refer to helper function
          elif item < self._root:
              self._left.remove(item)
          else:
              self._right.remove(item)
  ```

- Now as the root of a subtree (possibly a leaf), delete this root with a helper function

  - Set `self._root = None` if the tree consist *just* the root (no subtrees)
  - If at least one of the subtrees is empty, then "promote" the other subtree up
  - If both subtrees are non-empty, *replace* the root with another value and remove the replaced value from else where
    - This replacement value is either the **max** of the left or the **min** of the right subtree
    - Extract the replacement value using: `BinarySearchTree._extract_max`

  ```python
  class BinarySearchTree:
      def _remove_root(self) -> None:
          """..."""
          if self._left.is_empty() and self._right.is_empty():
              self._root = None
              self._left = None
              self._right = None
          elif self._left.is_empty():
              # "Promote" the right subtree.
              self._root, self._left, self._right = \
                  self._right._root, self._right._left, self._right._right
          elif self._right.is_empty():
              # "Promote" the left subtree.
              self._root, self._left, self._right = \
                  self._left._root, self._left._left, self._left._right
          else:
              self._root = self._left._extract_max()  # helper function
  ```

- Keep going to the right to bigger and bigger values until the end, then remove it. (Max has at most one child, therefore the process would be much easier)

  ```python
  class BinarySearchTree:
      def _extract_max(self) -> Any:
          """Remove and return the maximum item stored in this tree.
  
          Preconditions:
            - not self.is_empty()
          """
          if self._right.is_empty():
              max_item = self._root
              # Version 1: Like remove_root, "promote" the left subtree.
              self._root, self._left, self._right = \
                  self._left._root, self._left._left, self._left._right
              # Version: 2:
              # self._delete_root()
              return max_item
          else:
              return self._right._extract_max()
  ```

## Running time analysis (`__contains__`)

- Start with analyzing the non-recursive running time of the method
  - Assume that each recursive call takes constant time
  - The `self.is_empty()` and `item==self._root` and `item < self._root` and the return statements are constant time
  - Therefore, the non-recursive cost is 1 step per recursive call
- Analyzing the recursive calls
  - BST's contains method only recurse on *one* of its subtrees, so the number of recursive calls differences depending on the values stored in the tree and the searching value
  - So `__contains__` has a spread of running times, so Worst-case is focused here
  - The total number of recursive calls is *at most* the height of the BST plus 1 (longest possible search path is equal to the height of the BST, plus 1 is for recursing into an empty subtree)
  - Since each non-recursive call takes 1 step,T this gives a total of $h+1$ steps, where $h$ is the height of the BST. Thus worst-case running time is $\Theta(h)$ 

#### BST height vs size

- The height of a BST can be much smaller than its size
- A BST with $n$ items, its height can be as large as $n$. Or as small as $\log_2n$
  - The height of tree $h$ can have size at most $2^h -1$ items. If store $n$ item in a BST, need $h \ge \log_2(n+1)$ to store all of them
- If it can be guaranteed that BST always have height roughly $\log_2n$, then in fact all three BST's operations (search, insert, delete) have a worst-case running time of $\Theta(h)=\Theta(\log n)$. This is better than sorted list (search of $\Theta(\log n)$, with insert and delete at $\Theta(n)$
  - Under this assumption, BST are more efficient than Multiset ADT

