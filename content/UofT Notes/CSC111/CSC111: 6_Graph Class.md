# The Graph Class

## Terminologies

- <u>Graph</u> - **a pair of sets** $G = (V, E)$, where $G$ is the graph itself, $V$ is the vertex and $E$ is the edge set

  - <u>Vertex</u> $V$ - a **set of objects**, each element is called a *vertex* of the graph, while the set $V$ itself is called the set of *vertices* of the graph [rep collection of points]
  - <u>Edge</u> $E$ - a **set of pairs of objects** from $V$, where each pair $\{v_1, v_2\}$ is a set of distinct vertices, called the *edge* of the graph ($v_1, v_2 \in V, ~~\and~~ v_1 \neq v_2$) [rep relationships]
    - Order does not matter in the pairs, ($\{v_1, v_2\} = \{v_2, v_1\}$)

  > Ex. Use the terminology of graphs to describe Facebook
  >
  > - Each Facebook user is a *vertex*
  > - Each friendship between two Facebook users is an *edge* between the vertices.

- <u>Adjacent</u> (neighbours) - if there **exists a edge between two vertices**
  
- Let $G = (V, E)$ and $v_1, v_2 \in V$ $v_1$ and $v_2$ are neighbours iff $\{v_1, v_2\} \in E$
  
- <u>Degree</u> of a vertex $d(v)$ - the number of neighbours $v$ has

- <u>Path</u> - sequences of **distinct** vertices that "**connects**" the vertices and satisfies the these: 

  - Let $G = (V, E)$ and $v_0, v_k \in V$, and $v_0, v_1, v_2, \dots, v_k \in V$
  - Each consecutive pair are adjacent ($v_1, v_2$ are adjacent, $v_2, v_3$ are adjacent...)
  - $k$ could be zero, in which the path is only a single vertex $v_0$

- <u>Length</u> of a path - **one less** than the **number of vertices in the sequence** 

  - The number of *edges* used by this path sequence
  - Allow 0 length paths, a vertex is always *connected* to itself

- <u>Connected</u> - when there exist a path between $v_0$ and $v_k$ (or $u, u'$) 

- A graph $G$ is <u>connected</u> when **for all pairs of vertices** $u, v \in V$, $u, v$ are connected

  > ##### Ex. Proof that this graph is not connected
  >
  >  <img src="https://tva1.sinaimg.cn/large/008eGmZEly1gox5h72s31j30d70bcjri.jpg" alt="graph-terminology-2" style="zoom:25%;" />
  >
  > *Poof*.   Let $G = (V, E)$ be the above graph, let $u, v$ be the vertices labelled $E, B$ respectively. 
  >
  > *Want to show that there does not exist a path between $u, v$, thus the graph is not connected* 
  > $$
  > \text{Assume contradiation}~
  > \exists \text{ a path } v_0, v_1, \dots, v_k \text{ between } u, v, 
  > \text{ where } v_0 = E, v_k = B\\
  > $$
  >
  > - Since $v_0, v_2$  must be adjacent, and $C$ is the only vertex adjacent to $E$, get that $v_1 = C$. 
  >
  > - Now $v_k = B$, get that $k \ge 2$ 
  > - By definition of *path*, know that $v_2$ must be adjacent of $C$ (but not $E$). However, no such vertex exist. Therefore $v_2$ does not exist. 
  > - This proves the contradiction, in which shows that this graph does not exist $\Box$

## Properties of Graphs

1. Prove that about the **maximum possible number of edges a graph** follows an equation

    - *Translation*: $\quad G = (V, E), |E| \le \frac{|V|~(|V|-1)}{2}$
    - *Proof* Using induction on $n$, 
        $$
        \quad P(n): \forall G = (V, E),\quad |V| = n~ \Rightarrow~ |E| \le \frac{n~(n - 1)}{2}, 
        \quad \text{ where } \forall n \in \N
        $$
    - **Base Case**: Let $n=0$, need to prove that $P(0)$
        - Let $G=(V, E)$ be an arbitrary graph, assume that $|V| = 0$ (the graph have no vertices). 
        - In this case, the graph is not able to have any edges. Therefore $|E| = 0$ which satisfies $|E| = \frac{0(0-1)}{2}$
    - **Induction step**: Let $k \in \N$ and assume that $P(k)$ holds (every graph with $k$ vertices has at most $\frac{k(k-1)}{2}$) edges.
        - Let $G= (V, E)$ be an arbitrary graph, assume that $|V| = k+1$ want to show that $|E| \le \frac{k(k-1)}{2}$.
        - Let $v$ be a vertex in $V$, divide the edges of $G$ into 2 groups
            - $E_1$ - the set of edges that contain $v$. There are at most $k$ other vertices in $V$ that $v$ could be adjacent to: $|E| \le k$. 
            - $E_2$ - the set of edges that do not contain $v$. Suppose remove $v$ from the graph, get $G'$. Then $E_2$ is the set of edges in the new graph $G'$ 
            - Putting them together get:
                $$
                |E| = |E_1| + |E_2| \le k + \frac{k(k-1)}{2} = \frac{k(k+1)}{2}
                $$
        - This is exactly what I wanted to show $\Box$

1. Prove **if 2 vertices in a graph are both connected to a third vertex, then they are also connected to each other.**
   <img src="https://tva1.sinaimg.cn/large/008eGmZEly1goxzfyo0yoj30k20act8s.jpg" alt="transitivity-1" style="zoom:38%;" />
   
   
    - *Translation*: Use the predicate $Conn (G, u, v)$ for "$u$ and $v$ are connected vertices in $G$"
        $$
        \forall G = (V, E),~ \forall u, v, w \in V, \quad (Conn(G, u, v) \and Conn(G, v, w)) \quad \Rightarrow \quad Conn(G, u, w)
        $$
    - *Proof*: Let $G = (V, E)$ be a graph, and $u, v, w \in V$. Assume that $u, v$ are connected, and $v, w$ are connected, want to show that $u, w$ are connected
    - Let $P_1$ be a path between $u, w$ and $P_2$ be a pth between $u, w$. By definition, they exist
    - Strategy: To avoid common vertices that is in both $P_1, P_2$, find the first POV between $P_1, P_2$, and join them at the vertex $v'$
    - Let $S \subseteq V$ tbe the set of all vertices that are both in $P_1, P_2$. This set would never be empty because at least $v \in S$
- Let $v'$ be the vertex in $S$ that is the closest vertex to $u$ in $P_1$. Since $v'$ in $S$, then this means that it is also in $P_2$. 
    - Finally, let $P_3$ be the path of vertices from $u$ to $v'$ in $P_1$, joined with vertices from $u'$ to $w$ in $P_2$. Therefore, the path $P_3$ is a valid path (no duplicates) and is indeed a path between $u, w$ $\Box$
    
3. Prove that for all graphs $G = V, E$, if $|V| \ge 2$ then **there exist 2 vertices in $V$ with the same degree**

    - *Translation*: $\quad \forall G = (V, E),~ |V| \ge 2 \quad \Rightarrow \quad 
      (\exists v_1, v_2 \in V,~ d(v_1) = d(v_2))$
    - *Proof*: Assume for a **contradiction** that this statement is False. Let $n = |V|$, want to show:
        $$
        \exists G = (V, E),~ |V| \ge 2 \quad \Rightarrow \quad \forall v_1, v_2 \in V,~ d(v_1) \neq d(v_2)
        $$
    - Let $v$ be an arbitrary vertex in $V$. Know that $d(v) \ge 0$. For potential neighbours of $v$, there are $n-1$ possibilities, therefore, get $d(v) \le n-1$. So this show that:
        $$
        \forall v \in V, \quad 0 \le d(v) \le n-1
        $$
    - Since there are $n$ different vertices in $V$ and each has a different degree. Then every element in the set in $\left\{ 0, 1, \dots, n-1 \right\}$ must *be the degree* associated with some vertex $v$:
        $$
        \exists v_1, v_2 \in V, \quad s.t. \quad d(v_1) = 0,~~ d(v_2) = n-1
        $$
    - (1) $d(v_1) = 0$ so this vertex is not adjacent to any other vertex: $\left\{ v_1, v_2 \right\} \notin E$
    - (2) $d(v_2) = n-1$, then it is adjacent to *every* other vertex, so $\left\{ v_1, v_2 \right\} \in E$
    - Since both $\left\{ v_1, v_2 \right\} \notin E$ and $\left\{ v_1, v_2 \right\} \in E$ are True, then the contradiction is true. $\Box$
