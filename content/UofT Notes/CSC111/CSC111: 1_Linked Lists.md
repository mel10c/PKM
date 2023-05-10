---
title: "CSC111: 1_Linked Lists"
tags: [Note]
date: [2021-02-03]
---

# Linked Lists

## Building Blocks of Linked Lists

- Python use **array-based** list implementations (elements are stored in consecutive locations)
  
- **Indexing fast** $\Theta(1)$, while inserting/deleting slow *worst-case running time* $\Theta(n)$
  
  - The python interpreter need find a memory space enough to store the consecutive datas
  
- <u>Linked List</u> - has the same *public itnerface* as a `list`, but have a different private implementation that do not have the long running time as lists. (Using nodes)

  - Indexing slow with *worst-case running time* $\Theta(n)$, but inserting/deleting fast.$\Theta(1)$

  ```python
  # Set up
  from __future__ import annotations  # Allow to write _Node annotation within the _Node class	
  from dataclasses import dataclass
  from typing import Any, Optional
  ```

- **Node** new class that does not need to store in a specific location. Instead, it stores a referene to the **next** element in the list

  - Represents a single element of the list
  - Note: `_Node` and`_Node.item` is **different**, one refers to an object while the other is a value
  - `_Node.next` is the *alias* of the next node object

  > `LinkedList` is the simplest application of nodes

  ```python
  @dataclass 
  class _Node:      
   	"""A node in a linked list.
  	Instance Attributes:       
  		- item: The data stored in this node. 
  		- next: The next node in the list, if any. 
  	"""      
  	item: Any     
  	# By default, this node does not link to any other node
  	next: Optional[_Node] = None  
  ```

-  `LinkedList` - a new class that represent the list itself

  - Contents a private attribute that **refers to the first node** in the list
  - `LinkedList._first` is an *alias* of the first node
  
  ```python
  class LinkedList:      
  	"""A linked list implementation of the List ADT."""      
  	# Private Instance Attributes:      
  	#   - _first: The first node in this linked list, 
  	# 						or None if this list is empty.
  	_first: Optional[_Node]
      
  	def __init__(self) -> None:          
  		"""Initialize an empty linked list."""          
  		self._first = None
  ```

### Building links manually

- By manually assigning private attributes to the new classes

  ```python
  # linky is an empty linked list
  linky = LinkedList() 
  # New nodes with items
  node1 = _Node(2)
  node2 = _Node(5)
  node3 = _Node(7) 
  # Linking nodes
  node1.next = node2
  node2.next = node3
  # Connect node to linked list
  linky._first = node1
  
  # Check list
  >>> node1
  _Node(item=2, next=_Node(item=5, next=_Node(item=7, next=None)))
  >>> linky._first.item
  2
  >>> linky._first.next.next.next  # return None(nothing)
  ```

## Traversing Linked Lists

- Aggregate over the different values

- Since the list size is unknown, a **while loop** would be a better choice than for loops.

  1. An initialized loop variable: that refers to the first node of the list (**node as loop variable**)
  2. Check if reached the end of the list or not with the **loop condition**
  3. Perform action on the visited node 
     - The loop variable refers to the `_Node` object, **needs to refer to its attribute** (`_Node.item`) to asses value

  4. Increment by **referring to the next node object**

  ```python
  curr = my_linked_list._first  # NODE loop variable
  while curr is not None:
  	# perform action with curr.item
  	curr = curr.next  
  ```

  > ##### Application of traversing (indexing into a linked list)
  >
  > Goal: get the value of the node with the index. Implicating as the `LinkedList` class function. (Using compound loop condition)
  >
  > ```python
  > def __getitem__(self, i: int) -> Any:
  >   	"""Return node value of the given index"""
  >   	curr = self._first
  >   	index_so_far = 0
  >   	while not (curr is None or index_so_far == i):
  >    		curr = curr.next
  >    		index_so_far += 1
  >   	# The loop with stop with 2 condition: (i ut of bound) or (reached i)
  >   	assert curr is None or index_so_far == i
  >   	if curr is None:
  >    		raise IndexError  # index out of buound
  >   	# else:  (perform actions if needed)
  >    	return curr.item
  >    ```
  > 
  >- Since `__getitem__` is a  special method in python. Therefore this LinkedList function could be assessed using the same indexing method as other lists
  > 
  >  ```python
  >   >>> linky[0]  # Equivalent ot linky.__getitem__(0)
  >   2
  >   >>> linky[1] + linky[2]
  >   12
  >  ```

> Appending item to LinkedLists and modification of LinkedList initializer (view  "prep2.py")

## Index-Based Mutation

1. Starting with linked list diagrams (representing the `linky` linked list)

<img src="https://tva1.sinaimg.cn/large/008eGmZEly1gnarcbrfzqj30o206odgk.jpg" alt="Screen Shot 2021-01-31 at 23.44.09" style="zoom:50%;" />

2. Goal: insert item `300` at index 2 in this list. First create a new node, by default, linked to `None`

<img src="https://tva1.sinaimg.cn/large/008eGmZEly1gnarca8mn4j30nw03kdga.jpg" alt="Screen Shot 2021-01-31 at 23.44.15" style="zoom:50%;" />

3. Modify `linky`, let he current node at index 1 to link to it

<img src="https://tva1.sinaimg.cn/large/008eGmZEly1gnarcao9btj30nk05kgmb.jpg" alt="Screen Shot 2021-01-31 at 23.44.21" style="zoom:50%;" />

4. Lastly, modify the (index - 1) node's link, connect to the new node

   <img src="https://tva1.sinaimg.cn/large/008eGmZEly1gnarcb5tg6j30na05wt9h.jpg" alt="Screen Shot 2021-01-31 at 23.44.26" style="zoom:50%;" />

- Using **parallel assignments** to avoid losing variables' values

  > ```python
  > curr.next, new_node.next = new_node, curr.next
  > ```

```python
def insert(self, i: int, item: Any) -> None:
        """..."""
        new_node = _Node(item)
        
        if i == 0:
            slef._first, new_node.next = new_node, self.first
        else: 
        	curr = self._first
            curr_index = 0

        	while not (curr is None or curr_index == i - 1):
            	curr = curr.next
            	curr_index = curr_index + 1

        	# After the loop is over, either we've reached the end of the list
        	# or curr is the (i - 1)-th node in the list.
        	assert curr is None or curr_index == i - 1

        	if curr is None:
            	raise IndexError  # i-1 is out of bound
        	else: # curr_index == i - 1
                curr.next, new_node.next = new_node, curr.next
```

- Always check if the operations is working on `Node` or is it performing in `None`
  - Add if statements to check when ever working with `curr.next` (never know if next exists)

```python
def pop(self, i: int) -> Any:
    """Remove and return item at index i.
    Preconditions:
        - i >= 0

    Raise IndexError if i >= the length of self.

    >>> lst = LinkedList([1, 2, 10, 200])
    >>> lst.pop(2)
    10
    >>> lst.pop(0)
    1
    >>> lst.to_list()
    [2, 200]
    """
    # 1. If the list is empty, you know for sure that index is out of bounds...
    if self._first is None:
        raise IndexError
    # 2. Else if i is 0, remove the first node and return its item.
    elif i == 0:
        curr_return, self._first = self._first.item, self._first.next
    # 3. Else iterate to the (i-1)-th node and update links to remove
    #    the node at position index. But don't forget to return the item!class LinkedList:
    else:
        curr = self._first
        curr_index = 0
        while not (curr is None or curr_index == i - 1):
            curr = curr.next
                curr_index += 1

        assert curr is None or curr_index == i - 1

        if curr or curr.next is None:
            raise IndexError
        else:  # curr_index == i
                curr_return, curr.next = curr.next.item, curr.next.next

    return curr_return
```

```python
# alternative way
def pop(self, i: int) -> Any:
    prev, cur = None, self._first
    curr_index = 0
	while not (curr is None or curr_index == i):
        prev, curr = curr, curr.next
        cur_index = curr_index + 1
	if curr is None:
        raise IndexError
    else:
        # curr_index is i, and curr is the node at index i
        # Either prev is None (and curr is self._first)
        # Or prev is a node, and its acutally the node at index i-1
        item = curr.item
        if prev is None:  # curr si self._first
            self._first = curr.next
        else:
            prev.next = curr.next
     return item
```

> Refers to "prep2.py" for the `remove` function, that is very similar to this `pop`

## Running-Time Analysis

$Running~Time~Analysis$ Of `LinkedList.insert` (view code above)

- Let $n$ be the length (number of items) of `self`
- Since the code is split into two different cases with the outer if statement, the $RT$ analysis would be organized into cases as well

1. Case 1: **Assume `i == 0`**
   - If the first `if` branch would execute, which takes constant time $RT = \Theta(1)$
2. Case 2: **Assume** `i>0`
   - The declaration statements (`curr = self._first, curr_index = 0`) takes constant time
   - The `while` loop iterates until either it reaches the end of the list (`curr is None`) or until it reaches the correct index (`curr_index == i-1`)
     - Case A: the loop will iterate $n$ iterations
     - Case B: the loop with iterate $i-1$ iterations, since `curr_index` starts at 0 and increases by 1 each iteration
     - Each iteration takes 1 steps, the total $RT$ for the while loop is $\min(n, i-1)$
   - The total running time for this case is $RT= \min(n, i-1)+2= \Theta(\min(n,i-1))$

**Therefore:**

- Since in Case 2, the expression would becomes $\Theta(1)$ when $i=0$, and the overall running time of `LinkedLIst.insert` is $RT= \Theta(\min(n, i))$

- *Assume* $0 \le i < n$,(not including the case where the index is the last) then $RT= \Theta(i)$ 

### Comparing `LinkedList` and `list` running times

| *Operation (assuming $0 \le i < n $*) | `List` RT     | `LinkedList` RT |
| ------------------------------------- | ------------- | --------------- |
| Indexing (`lst[i]`)                   | $\Theta(1)$   | $\Theta(i)$     |
| Inserting into index $i$              | $\Theta(n-i)$ | $\Theta(i)$     |
| Removing item at index $i$            | $\Theta(n-i)$ | $\Theta(i)$     |

- For list indexing, linked list have a worse performance
- For insertion and deletion, linked list has the exact opposite $RT$ with list
  - Want constant indexing mainly add/remove at the end of the list -- prefer a `list`
  - Mainly add/remove element at the front of the list -- prefer a `Linkedlist`