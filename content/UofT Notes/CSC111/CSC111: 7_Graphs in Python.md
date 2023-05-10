# Graphs in Python

## Representing Graphs in Python

### The `_Vertex` class

- Implement graph as a *node-based* data structure
    - **vertex** - node; **edge** - implicit as a variable in the vertex node
- Restrictions on edges: cannot have a vertex with an edge to itself AND all edges are symmetric


```Python
from __future__ import annotations
from typing import Any

class _Vertex:
    """A vertex in a graph

    Instance Attributes:
        - item: The data stored in this vertex
        - neighbours: The vertices that are adjacent to this vertex
    
    Representation Invariants:
        - self not in self.neighbours
        - all(self in u.neighbours for u in self.neighbours)
    """
    item: Any
    neighbours: set[_Vertex]

    def __init__(self, item: Any, neighbours: set[_Vertex]) -> None:
        """Initialize a new vertex with the given item and neighbours"""
        self.item = item
        self.neighbours = neighbours
```

> ##### Example of using this class:
> ```python
> >>> v1 = _Vertex('a', set())
> >>> v2 = _Vertex('b', set())
> >>> v3 = _Vertex('c', set())
> >>> v1.neighbours = {v2, v3}
> >>> v2.neighbours = {v1, v3}
> >>> v3.neighbours = {v1, v2}
> ```

- Similar to `Tree_subtree` attribute, but this case treats the class as representing a single element, not the whole graph itself.
- This collection is **unordered** (no left-to-right) ordering like trees


### The `Graph` class

```Python
class Graph:
    """A graph"""
    # Private Instance Attributes:
    #    - _vertices: A collection of the vertices contained in this graph. 
    #                 Maps item to _Vertex instance
    _vertices: dict[Any, _Vertex]

    def __init__(self) -> None:
        """Initialize an empty graph (no vertices or edges)"""
        self._vertics = {}
```

- This would only great empty graphs. The mutating method is here:
    ```Python
    class Graph:
        def add_vertex(self, item: Any) -> None:
            """Add a vertex with the given item to this graph

            The new vertex is not adjacent to any other vertices.

            Preconditions:
                - item not in self._vertices
            """
            self._vertices[item] = _Vertex(item, set())

        def add_edge(self, item1: Any, item2: Any) -> None:
            """Add an edge between the two vertices with the given items in this graph

            Raise a ValueError if item1 and item2 do not appearas vertices in this graph

            Preconditions:
                - item1 != item2
            """
            if item1 in self._vertices and item2 in self.vertices:
                v1 = self._vertices[item1]
                v2 = self._vertices[item2]

                # Add the new edge
                v1.neighbouts.add(v2)
                v2.neighbouts.add(v1)
            else:
                raise ValueError
    ```

    > ##### Create `Graph` objects and populate them with vertices and edges
    > ```Python
    > >>> g = Graph()
    > >>> g.add_vertex('a')
    > >>> g.add_vertex('b')
    > >>> g.add_vertex('c')
    > >>> g.add_edge('a', 'b')
    > >>> g.add_edge('a', 'c')
    > >>> g.add_edge('b', 'c')
    > ```

### Checking adjacency

- Implement 2 `Graph` methods to check adjacency of a vertex


```Python
class Graph:
    def adjacent(self, item1: Any, tiem2: Any) -> bool:
    """Return whether item1 and item2 are adjacent vertices in this graph.

    Return False if item1 or item2 do not appear as vertices in this graph
    """
    if item1 in self._vertices and item2 in self._vertices:
        v1 = self.verticies[item1]
        return any(v2.item == item2 for v2 in v1.neighours)
    else:
        return False


    def get_neighbours(self, item: Any) -> set:
        """Return a set of the neighbours of the given item

        Note that the *item* are returned, not the _Vertex objects themselves

        Raise a ValueError if item does not appear as vertex in this graph
        """
        if item in self._vertices:
            v = self._vertices[item]
            return {neighbour.item for neighbour in v.neighbours}
        else:
            raise ValueError
```

> ##### Create `Graph` objects and populate them with vertices and edges
>
> ```Python
> >>> g = Graph()
> >>> g.add_vertex('a')
> >>> g.add_vertex('b')
> >>> g.add_vertex('c')
> >>> g.add_vertex('d')
> >>> g.add_edge('a', 'b')
> >>> g.add_edge('b', 'c')
> 
> >>> g.adjacent('a', 'b')
> True
> >>> g.adjacent('a', 'd')
> False
> >>> g.get_neighbours('b') == {'a', 'c'}
> True
> >>> g.get_neighbours('d') == set()
> True
> ```

## Connectivity and Recursive Graph Traversal

- Goal: Implement a generalization method that checks whether two vertices are connected
- This method follows a similar structure where it first finds a vertex that correspond to the input `item1`
- But checking connectivity is much harder than checking adjacencies. Use a helper function in the `_Vertex` class called `check_connected`, write down the code so far:
    ```Python
    class Graph:
        def connected(self, item1: Any, item2: Any) -> bool:
            """Return whether item1 and item2 are connected vertices in this graph
    
            Return False if item1 or item2 does not appear as vertices in the graph
    
            >>> g = Graph()
            >>> g.add_vertex(1)
            >>> g.add_vertex(2)
            >>> g.add_vertex(3)
            >>> g.add_vertex(4)
            >>> g.add_edge(1, 2)
            >>> g.add_edge(2, 3)
            >>> g.add_edge(1, 3)
            >>> g.connected(1, 3)
            True
            >>> g.connected(1, 4)
            False
            """
            if item1 in self._vertices and item2 in self._vertices:
                v1 = self.vertices[item1]
                return v1.check_connected(item2, set())  # pass in an empty "visited" set
            else:
                return False
    ```
- Given 2 vertices $v_1$ and $v_2$, they are connected when:
    
    - $v_1 = v_2$ or there exist a neighbour $u$ of $v_1$ such that $u, v_2$ are connected
- This has a basic recursive definition, but does not strictly follows the recursive structure. 
    - It does not **break down the datatype** (graph into a smaller instance)
    - This leads to a new type of error `RecursionError`


### `RecursionError` and the danger of infinite recursion

- To understand this, do a manual tracing 
- Let a graph `g` have 3 vertices, containing the items `1, 2, 3`. If call `g.connected(1, 3)`, the program will first find the vertex corresponding to `1`, which can be called $v_1$. **Then the code would call `_Vertex.check_connected` on $v_1$ and `3`**. This is the problem
    <img src="https://tva1.sinaimg.cn/large/008eGmZEly1goxzgscwhkj309w03cdfo.jpg" alt="infinite-recursion" style="zoom:38%;" />
    1. For $v_1$, `self.item ==1`, which is not `3`. This enters the recursive branch. 
    2. The only neighbour for $v_1$ is the vertex containing `2`, which can be called as $v_2$. Then the code would make a recursive call to `_Vertex.check_connected` of $v_2$ and `3`
    3. For $v_2$, `self.item == 2`, which is not `3`. This again, enters the recursive branch. The only neighbour of $v_2$ is $v_1$, then it would make a recursive call on $v_1$ and `3` 
    4. For $v_1$ ...
- <u>Infinite recursion</u> - a code has expression a recursion computation that does not stop by reaching the base case
    - In the above case, the Python interpreter alternates between calling the `Vertex.check_connected` with $v_1$ and `3` and with $v_2$ and `3`, and never stops
    - This keeps adding a *stack frame* onto the function call stack, which at then would reach the limit the Python interpreter has set, and leads to a `RecursionError`


### Fixing the recursion error
- Modify the recursive condition: Given 2 vertices $v_1$ and $v_2$, they are connected when:
    - $v_1 = v_2$ or 
    - There exists a neighbour $u$ of $v_1$ such that $u$ and $v_2$ are connected by a path **that does not use $v_1$**
    - Achieve this by adding a `visited` parameter (which is already in the `Graph` code above)


```Python
class _Vertex:
    def check_connected(self, target_item: Any, visited: set[_Vertex]) -> bool:
        """Return whether this vertex is connected to a vertex corresponding to the target_item,
        WITHOUT using any of the vertices in visited

        Preconditions:
            - set not in visited
        """
        if self.item == target_item:
            return True
        else:
            visited.add(self)  # add self to the set of visited vertices 
            for u in self.neighbours:
                # only recursive on vertices that haven't been visited
                if u not in visited and u.check_connected(target_item, visited):
                    return True

            return False
```
> But even though this implementation is correct, and much more efficient than the previous one, it does come with an important warning we want you to remember for the future. Whenever you use recursion with a mutable argument, be very careful when choosing whether to mutate that argument or create a modified copy—if you choose to mutate the argument, know that all recursive calls will mutate it as well!
