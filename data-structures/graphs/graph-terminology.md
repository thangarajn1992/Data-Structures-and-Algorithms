# Graph Terminology

### Types of Graphs

* [Directed Acyclic Graph](graph-terminology.md#directed-acyclic-graph-dag)
* [Bipartite Graph](graph-terminology.md#bipartite-graph)
* Biconnected Graph

### Special Nodes

* [Mother Vertex](graph-terminology.md#mother-vertex)
* [Articulation Point/Cut Vertex](graph-terminology.md#articulation-point-cut-vertex)

### Special Edges

* [Bridges](graph-terminology.md#bridges)

### Set of Nodes/Properties

* [Strongly Connected Components](graph-terminology.md#strongly-connected-components)
* [Transitive Closure of Graph](graph-terminology.md#transitive-closure-of-a-graph)



### Directed Acyclic Graph \(DAG\)



### Bipartite Graph

A Bipartite Graph is a graph whose vertices can be divided into two independent sets, U and V such that every edge \(u, v\) either connects a vertex from U to V or a vertex from V to U. In other words, for every edge \(u, v\), either u belongs to U and v to V, or u belongs to V and v to U. We can also say that there is no edge that connects vertices of same set. \(Implementation to check is graph bipartite \)

![](../../.gitbook/assets/image%20%2817%29.png)

### Biconnected Graph

An undirected graph is called Biconnected if there are two vertex-disjoint paths between any two vertices. In a Biconnected Graph, there is a simple cycle through any two vertices. A graph is said to be Biconnected if: 

1. It is connected, i.e. it is possible to reach every vertex from every other vertex, by a simple path. 
2. Even after removing any vertex the graph remains connected i.e there is no articulation point.

![](../../.gitbook/assets/image%20%2829%29.png)

![](../../.gitbook/assets/image%20%2828%29.png)

### Mother Vertex

A Mother vertex in a graph G, is a vertex v such that **all other vertices in G can be reached by a path from v**. There can be more than one mother vertices in a graph. To find mother vertex, use this [link](../../problem-solutions/graph-problems/find-a-mother-vertex-in-a-graph.md)

![](../../.gitbook/assets/image%20%2811%29.png)

### Articulation Point/Cut Vertex

A vertex in an undirected connected graph is an articulation point \(or cut vertex\) i**f removing it \(and edges through it\) disconnects the graph**. For a disconnected undirected graph, an articulation point is a vertex **removing which increases number of connected components.**

Articulation points represent vulnerabilities in a connected network – single points whose failure would split the network into 2 or more components. They are useful for designing reliable networks.

![Articulation Points](../../.gitbook/assets/image%20%2833%29.png)

### Bridges

An edge in an undirected connected graph is a bridge if **removing it disconnects the graph**. For a disconnected undirected graph, definition is similar, a bridge is an edge **removing which increases number of disconnected components**.

Like [Articulation Points](graph-terminology.md#articulation-point-cut-vertex), bridges represent vulnerabilities in a connected network and are useful for designing reliable networks. For example, in a wired computer network, an articulation point indicates the critical computers and a bridge indicates the critical wires or connections.

![Bridges](../../.gitbook/assets/image%20%2832%29.png)

### Strongly Connected Components

A directed graph is strongly connected if there is a **path between all pairs of vertices**. A strongly connected component \(SCC\) of a directed graph is a maximal strongly connected sub-graph. For eg., there are 3 SCCs in the following graph.

![Strongly Connected Components](../../.gitbook/assets/image%20%281%29.png)

We can find all strongly connected components in \(V+E\) time using [kosaraju's algorithm](graph-algorithms/kosarajus-algorithm.md).

### Transitive Closure of a Graph

Given a directed graph, find for all vertex pairs \(u,v\) if there is a path exists between them. The reach-ability matrix of \[v\]\[v\] is called transitive closure of a graph. This can be done using [Floyd Warshall Algorithm](graph-algorithms/floyd-warshall-algorithm-for-transitive-closure.md) in O\(V^3\) or using another algorithm in O\(v^2\) discussed [here](../../problem-solutions/graph-problems/graph-based-problems/transitive-closure-of-graph-using-dfs.md)





