# Graph Terminology

### Directed Acyclic Graph \(DAG\)



### Bipartite Graph

A Bipartite Graph is a graph whose vertices can be divided into two independent sets, U and V such that every edge \(u, v\) either connects a vertex from U to V or a vertex from V to U. In other words, for every edge \(u, v\), either u belongs to U and v to V, or u belongs to V and v to U. We can also say that there is no edge that connects vertices of same set. \(Implementation to check is graph bipartite \)

![](../../.gitbook/assets/image%20%2814%29.png)

### Strongly Connected Components

A directed graph is strongly connected if there is a **path between all pairs of vertices**. A strongly connected component \(SCC\) of a directed graph is a maximal strongly connected sub-graph. For eg., there are 3 SCCs in the following graph.

![Strongly Connected Components](../../.gitbook/assets/image%20%281%29.png)

We can find all strongly connected components in \(V+E\) time using [kosaraju's algorithm](../../algorithms/kosarajus-algorithm.md).





