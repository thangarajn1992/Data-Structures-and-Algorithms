# Adjacency List Representation

An array if lists is used to represent the Graph. The size of the array is equal to the number of vertices. Let the array be an array\[\]. An entry array\[i\] represents the list of vertices adjacent to ith vertex. This representation can also be used to represent a weighted graph. The weights of the edges can be represented as lists of pairs.

![](../../../.gitbook/assets/image%20%288%29.png)

![Adjacency List Representation](../../../.gitbook/assets/image%20%2812%29.png)

### Advantages of Adjacency List Representation

* Saves space O\(\|V\| + \|E\|\). In worst case, consumes O\(V^2\) space
* Adding a vertex is easier

### Disadvantages of Adjacency List Representation

* Queries like whether there is an edge from vertex u to v are not efficient and can be done in O\(V\).

## Implementation of Adjacency List Representation

### Directed Graph using Adjacency List

```cpp
#include<iostream>
#include <list>
 
using namespace std;
 
// This class represents a directed graph using
// adjacency list representation
class Graph
{
    int V;    // No. of vertices
    list<int> *adj;  // Pointer to an array containing adjacency lists
public:
    Graph(int V);  // Constructor
    {
        this->V = V;
        adj = new list<int>[V];
    } 
    // function to add an edge to graph
    void addEdge(int v, int w);
    {
        adj[v].push_back(w); // Add w to v’s list.
    }    
};

// Driver program to test methods of graph class
int main()
{
    // Create a graph given in the above diagram
    Graph g(4);
    
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 2);
    g.addEdge(2, 0);
    g.addEdge(2, 3);
    g.addEdge(3, 3);
 
    return 0;
}
```

### Undirected Graph using C++ vector

```cpp
// A simple representation of graph using STL
#include<bits/stdc++.h>
using namespace std;
 
// A utility function to add an edge in an
// undirected graph.
void addEdge(vector<int> adj[], int u, int v)
{
    adj[u].push_back(v);
    adj[v].push_back(u); // For directed graph, we won't add this line
}
 
// A utility function to print the adjacency list
// representation of graph
void printGraph(vector<int> adj[], int V)
{
    for (int v = 0; v < V; ++v)
    {
        cout << "\n Adjacency list of vertex "
             << v << "\n head ";
        for (auto x : adj[v])
           cout << "-> " << x;
        printf("\n");
    }
}
 
// Driver code
int main()
{
    int V = 5;
    
    vector<int> adj[V];
    
    addEdge(adj, 0, 1);
    addEdge(adj, 0, 4);
    addEdge(adj, 1, 2);
    addEdge(adj, 1, 3);
    addEdge(adj, 1, 4);
    addEdge(adj, 2, 3);
    addEdge(adj, 3, 4);
    
    printGraph(adj, V);
    return 0;
}
```

