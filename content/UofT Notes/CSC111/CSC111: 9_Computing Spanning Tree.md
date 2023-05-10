---
title: "CSC111: 9_Computing Spanning Tree"
tags: [Note]
date: [2021-02-03]
---

# Computing Spanning Trees

## Spanning trees and the problem specification

- Let $G = (V, E)$ be a *connected* graph. Let $G' = (V, E')$ be another graph with the same vertex set as $G$, and where $E' \subset E$. 
    - <u>Spanning tree</u> - in the above case, $G'$ is a *spanning tree* of G
- Gaol: Implement the `Graph` method that computes a spanning tree for the graph.


### 1. Printing out connected vertices

```Python
class _Vertex:
    def print_all_connected_indented(self, visited: set[_Vertex], d: int) -> None:
        """Print all items that this vertex is connect to, WITHOUT using any of the vertices
        in visited.

        Preconditions: 
            - self not in visited
            - d >= 0
        """
        print('    ' * d + str(self.item))

        visited.add(self)
        for u in self.neighbours:
            if u not in visited:  # Only recourse on vertices that haven't been visited
                u.print_all_connected_indented(visited)
```

### 2. Spanning Tree Algorithm

- There are 2 key changes needed to make
    1. Each recursive call will now return a list of edges, so need an accumulator to keep track of them
    2. To "handle the root", need to add edges between `self` and each vertex where we make a recursive call

```Python
class _Vertex:
    def spanning_tree(self, visited: set[_Vertex]) -> list[set]:
        """Return a list of edges that form a spanning tree of all vertices that are
        connected to this vertex WITHOUT using any of the vertices in visited.

        The edges are returned as a list of sets, where each set contains the two
        ITEMS corresponding to an edge.

        Preconditions:
            - self not in visited
        """
        edges_so_far = []

        visited.add(self)
        for u in self.neighbours:
            if u not in visited:  # Only recourse on vertices that haven't been visited
                edges_so_far.append({self.item, u.item})
                edges_so_far.extend(u.spanning_tree(visited))

        return edges_so_far
```
```Python
>>> # Using same graph g as above
>>> g._vertices[0].spanning_tree(set())
[{0, 3}, {0, 1}, {1, 4}, {2, 4}]
```
### 3. Combining it together 
```Python
class Graph: 
    def spanning_tree(self) -> lst[set]:
        """Return a subset of the edges of this graph that forms a spanning tree.
        
        The edges are returned as a list of sets, where each set contains the two
        ITEMS corresponding to an edge. Each returned edge is in this graph
        (i.e., this function doesn't create new edges!).

        Preconditions:
            - this graph is connected
        """
        # Pick a vertex to start
        all_vertices = list(self._vertices.values())
        start_vertex = all_vertices[0]

        # Use our helper _Vertex method
        return start_vertex.spanning_tree(set())
```
