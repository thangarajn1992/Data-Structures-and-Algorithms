# Adjacency Matrix Representation

Adjacency Matrix is a 2D array of size V x V, where V is the number of vertices in a graph. Let the 2D array be `adj[][]`, a slot `adj[i][j] = 1` indicates that there is an edge from vertex i to vertex j. Adjacency matrix for undirected graph is always symmetric. Adjacency matrix is also used to represent weighted graphs like `adj[i][j] = w`

![](../../../.gitbook/assets/image%20%283%29.png)

![Adjacency Matrix Representation of Graph](../../../.gitbook/assets/image%20%285%29.png)

### Advantages of Adjacency Matrix Representation

* Easier to Implement and follow
* Removing an edge takes O\(1\) time.
* Queries like whether there is an edge from vertex u to v are efficient and can be done in O\(1\).

### Disadvantages of Adjacency Matrix Representation

* Consumes more space O\(V^2\). Even if graph has less number of edges.
* Adding a vertex is O\(V^2\).

## Implementation of Adjacency Matrix Representation



