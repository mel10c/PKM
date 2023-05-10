---
title: "CSC111: 8_Cycles and Trees"
tags: [Note]
date: [2021-02-03]
---

# Cycles and Trees

### A "Lower Bound" for connectivity

- What is the *minimum* number of edges required in a connected graph.
- Any connected graph $G = (V, E)$ must have $|E| \ge |V| - 1$
- However, it is hard to prove this.


## Cycles

- <u>Cycle</u> - Let $G = (V, E)$ be a graph, a *cycle* in $G$ is a **sequence** of vertices $v_0, \dots, v_k$ satisfying the following conditions
    - $k \ge 3$
    - $v_0 = v_k$ and all other vertices are distinct from each other and $v_0$
    - Each consecutive pair of vertices is adjacent
- In other words, cycle is a path that starts and end at the same vertex
- The length of a cycle is the number of edges used by the sequence, which is also the number of distinct vertices in the sequence (the above notation describes a cycle of length $k$)
    
    - Length has to be at least 3
- <u>**Lemma**</u> - Let $G = (V, E)$ be a graph, and $e \in E$. If $G$ is connected and $e$ is in a cycle of $G$, then the graph obtained by removing $e$ from $G$ is still connected. 
    - Removing any vertex in a cycle, the rest of that cycle is till connected
    $$
    \forall G = (V, E),~ \forall e \in E,~ (G \text{ is connected } ~\and~ e \text{ is in a cycle of } G)
    \quad \Rightarrow \quad G - e \text{ is connected }
    $$
    - *Proof*: Let $G = (V, E)$ be a graph, and $e \in E$ be an edge in the graph. Assume that $G$ is connected and that $e$ is in a cycle. Let $G' = (V, E \setminus \{e\})$ be a graph formed from $G$ by removing edge $e$. Want to show that $G'$ is also connected.
    - Let $w_1, w_2 \in V$. By the assumption, know that $w_1, w_2$ are connected in $G$. Want to show that they are also connected in $G'$
    - Let $P$ be a path between $w_1, w_2$ in $G$ (exists due to the defintion of connectedness). Divide the proof into 2 cases
        - **Case 1**: $P$ does not contain the edge $e$. Then $P$ is a path in $G'$ as well 
        - **Case 2**: $P$ does contain the edge $e$. Let $u$ be the endpoint of $e$ which is closer to $w_1$ on the path $P$, and let $v$ be the other endpoint
    - This divides $P$ into 3 parts
        1. $P_1$: from $w_1$ to $u$
        2. The is the edge $\left\{ u, v \right\}$
        3. $P_2$: from $v$ to $w_2$
    - $P_1, P_2$ cannot use the edge $\left\{ u, v \right\}$ (no delicates), then they must be paths in $G'$. This means that $w_1$ is in $G'$ as well. Also, $w_2$ is connected to $v$ in $G'$
    - $u, v$ are also connected in $G'$, since they are part of the cycle. By the *transitivity of connectedness*, $w_1$ and $w_2$ are also connected in $G'$


### Graph with no cycle

- <u>Tree</u> -  Let $G = (V, E)$ be a graph, $G$ is a *tree*, when it is connected and has no cycles
    - Similar to the `Tree` class before, not **no root** element, don't have to draw from top down


- **<u>Lemma</u>** - Let $G$ be a graph. If $G$ does not have a cycle, then there does not exist an edge $e$ in $G$ such that $G-e$ is connected
    $$
    \forall G = (V, E),~ G \text{ does not have a cycle } \quad \Rightarrow \quad \neg (\exists e \in E,~ G - e \text{ is connected})
    $$
    - *Proof*: Let $G = (V, E)$ be a graph. Assume that there exists an edge $e \in $ such that $G - e$ is still connected.
    - Let $G' = (V, E \setminus \{e\})$ be the graph obtained by removing $e$ from $G$. Assume that $G'$ is connected
    - Let $u, v$ be the endpoints of $e$, by the definition of connectedness, there exists a path $P$ in $G'$ between $u, v$ (does not contain $e$). 
    - Taking the path $P$ and adding the edge $e$ to it is a cycle in $G$. $\Box$
- <u>Lemma</u> - Let $G$ be a **tree**. Then removing any edge from $G$ results in a graph that is not connected
    - *Proof*: Following the previous Lemma, by definition, $G$ does not have any cycles, and so there does not exist an edge that can be removed from $G$ without disconnected it. $\Box$
    - Tree is the "backbone" of a connected graph, While a connected graph may have many edges and many cycles, it is possible to identify an underlying tree structure in the graph. 
        - If this tree is unchanged, it ensures the graph remains connected


### Counting Tree Edges

- **Theorem** (Number of edges in a tree): Let $G = (V, E)$ be a tree. Then $|E| = |V| - 1$
    $$
    \forall G = (V, E),~ G \text{ is a tree } \quad \Rightarrow \quad |E| = |V| - 1
    $$
    - Want to show it is always possible to pick a degree 1 *leaf* whose removal from $G$ is still a tree
    - <u>Lemma</u> - Let $G = (V, E)$ be a tree. If $|V| \ge 2$, then $G$ has a vertex with degree one
        $$
        \forall G = (V, E),~ (G \text{ is a tree } \and |V| \ge 2) \quad \Rightarrow \quad (\exists v \in V,~ d(v) = 1)
        $$
