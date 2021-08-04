# Graph Terminology

### Mother Vertex

A Mother vertex in a graph G, is a vertex v such that all other vertices in G can be reached by a path from v. There can be more than one mother vertices in a graph. To find mother vertex, use this [link](../../problem-solutions/graph-problems/find-a-mother-vertex-in-a-graph.md)

![](../../.gitbook/assets/image%20%2811%29.png)

### Directed Acyclic Graph \(DAG\)



### Bipartite Graph

A Bipartite Graph is a graph whose vertices can be divided into two independent sets, U and V such that every edge \(u, v\) either connects a vertex from U to V or a vertex from V to U. In other words, for every edge \(u, v\), either u belongs to U and v to V, or u belongs to V and v to U. We can also say that there is no edge that connects vertices of same set. \(Implementation to check is graph bipartite \)

![](../../.gitbook/assets/image%20%2817%29.png)

### Strongly Connected Components

A directed graph is strongly connected if there is a **path between all pairs of vertices**. A strongly connected component \(SCC\) of a directed graph is a maximal strongly connected sub-graph. For eg., there are 3 SCCs in the following graph.

![Strongly Connected Components](../../.gitbook/assets/image%20%281%29.png)

We can find all strongly connected components in \(V+E\) time using [kosaraju's algorithm](graph-algorithms/kosarajus-algorithm.md).

### Transitive Closure of a Graph

Given a directed graph, find for all vertex pairs \(u,v\) if there is a path exists between them. The reach-ability matrix of \[v\]\[v\] is called transitive closure of a graph. This can be done using [Floyd Warshall Algorithm](graph-algorithms/floyd-warshall-algorithm-for-transitive-closure.md) in O\(V^3\) or using another algorithm in O\(v^2\) discussed [here](../../problem-solutions/graph-problems/graph-based-problems/transitive-closure-of-graph-using-dfs.md)





