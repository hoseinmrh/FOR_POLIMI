# FOR Algorithms

## Chapter 2. Graph Optimization

1. **Graph Reachability**

-   Given a directed graph $G = (N,A)$ and a node $s$, determine all the nodes that are reachable from $s$.
-   **Input**: $G = (N,A)$, described by the successor lists, and $s \in N$.
-   **Output**: Subset $M \subseteq N$ of nodes of $G$ reachable from $s$.
-   **Complexity**: Since each node $u$ is inserted in $Q$ at most once and each arc $(u,v)$ is considered at most once, the overall complexity is:

$$
O(n+m), where \ \ n = |N|, \ m = |A|
$$

---

2. **Prim's Algorithm**

-   Iteratively build a spanning tree.
-   **Input**: Connected $G=(N, E)$ with edge costs.
-   **Output**: Subset $T \subseteq E$ of edges of $G$ such that $G_T=(N,T)$ is a minimum cost spanning tree of $G$.
-   **Complexity**: Using to sets $C_j$ and $closest_j$ we can reach the time complexity of:

$$
O(n^2)
$$

-   **Optimiality Condition**: Check for cost decreasing edges. If exists, not optimal, otherwise, optimal!

---

3. **Dijkstra**:

-   Consider the nodes in increasing order of length (cost) of the shortest path from $s$
    to any one of the other nodes.
-   **Input**: $G = (N,A)$ with non-negative arc costs, $s \in N$
-   **Output**: Shortest path from $s$ to all nodes of $G$
-   **Complexity**:

$$
O(n^2)
$$

---

4. **Floyd-Warshall**:

-   Detects the presence of circuits with negative cost (identifies ill-definedness). Provides a set of shortest paths between all pairs of nodes, even when there are arcs with negative cost.
-   **Input**: Directed $G=(N,A)$ with an $n \times n$ cost matrix, $C=[c_{ij}]$.
-   **Output**: For each pair of nodes $i,j \in N$, the cost $d_{ij}$ of the shortest path from $i$ to $j$.
-   **Complexity**:

$$
O(n^3)
$$

-   **Triangular Operation**: For each pair of nodes $i, j$ with $i \neq u$ and $j \neq u$ (including the case $i=j$), check whether when going from $i$ to $j$ it is more convenient to go via $u$:

$$
if \ \ d_{iu} + d_{uj} \lt d_{ij} \ \ then \ \ d_ij \leftarrow d_{iu} + d{uj}
$$

---

5.  **Topological Sort**:

-   **Complexity**:

$$
O(n+m)
$$

---

6. **Shortest Path in DAG**:

-   First sort the graph in the topological order and then find the shortest path with a DP approach.
-   **Input**: DAG $G(N,A)$ and $s \in N$
-   **Output**: Shortest path from $s$ to other nodes.
-   **Complexity**: The topological sort is in order of $O(n+m)$ and in the DP part, each node and arc is considered only once so again, $O(n+m)$. Overall:

$$
O(n+m)
$$

---

7. **Critical Path Method**:

-   It determines: a schedule (specifying the order and the alotted time for the activities) that minimizes the overall project duration. the slack of each activity, i.e., the amount of time by which its execution can be delayed, without a ecting the overall minimum project duration.

-   **Input**: Graph $G = (N,A)$, with $n = |N|$ , $m = |A|$ and the duration $d_{ij}$
    associated to each $(i,j) \in A$.
-   **Output**: $(T_{min}, T_{max})$ for $i = 1, 2, ..., n \in N$
-   **Complexity**: This algorithm has 3 parts. First is topological sort which has the order of $O(m+n)$, then the last two parts which are for calculating $T_{min}$ and $T_{max}$ are also in order of $O(m+n)$ since each node/arc is only considered once. So the overall complexity is:

$$
O(n+m)
$$

---

8. **Ford-Fulkerson**:

-   Start from a feasible flow $\underline{x}$ and try to iteratively increase its value $\varphi$ by sending,at each iteration, an additional amount of product along a(n undirected) path from $s$ to $t$ with a strictly positive residual capacity.
-   **Input**: Graph $G=(N,A)$ with capacity $k_{ij} \gt 0$ for every $(i,j) \in A, \ \ s,t \in N$.
-   **Output**: Feasible flow $\underline{x}$ from $s$ to $t$ of maximum value of $\varphi^*$

-   **Complexity**:

1. Since $\delta > 0$, the value $\varphi$ increases at each iteration (cycle).
2. If all $k_{ij}$ are integer, $\mathbf{x}$ and $\overline{k}_{ij}$ are integer, and $\delta \geq 1$, then there are at most $\varphi^*$ increases.
3. Since

$$
\varphi^* \leq k(\{s\}) \leq m \, k_{\text{max}},
$$

where $m = |A|$ and $k_{\text{max}} = \max\{k_{ij} : (i,j) \in A\}$, and each cycle is $O(m)$, the overall complexity is

$$
O(m^2 k_{\text{max}})
$$

---
