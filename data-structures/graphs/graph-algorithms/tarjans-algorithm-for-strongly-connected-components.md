# Tarjan’s Algorithm for Strongly Connected Components

A directed graph is strongly connected if there is a path between all pairs of vertices. A strongly connected component \(**SCC**\) of a directed graph is a maximal strongly connected sub-graph. For example, there are 3 SCCs in the following graph.  
 

![SCC](https://media.geeksforgeeks.org/wp-content/cdn-uploads/kosaraju.jpg)

We have discussed [Kosaraju’s algorithm for strongly connected components](kosarajus-algorithm.md). The previously discussed algorithm requires two DFS traversals of a Graph. Tarjan’s algorithm requires only one DFS traversal.

Tarjan Algorithm is based on following facts:   
1. DFS search produces a DFS tree/forest   
2. Strongly Connected Components form sub-trees of the DFS tree.   
3. If we can find the head of such subtrees, we can print/store all the nodes in that sub-tree \(including head\) and that will be one SCC.   
4. There is no back edge from one SCC to another \(There can be cross edges, but cross edges will not be used while processing the graph\).

To find head of a SCC, we calculate disc and low array \(as done for [articulation point](https://www.geeksforgeeks.org/articulation-points-or-cut-vertices-in-a-graph/), [bridge](https://www.geeksforgeeks.org/bridge-in-a-graph/), [bi connected component](https://www.geeksforgeeks.org/biconnectivity-in-a-graph/)\). As discussed in the previous posts, low\[u\] indicates earliest visited vertex \(the vertex with minimum discovery time\) that can be reached from sub-tree rooted with u. A node u is head if disc\[u\] = low\[u\].

