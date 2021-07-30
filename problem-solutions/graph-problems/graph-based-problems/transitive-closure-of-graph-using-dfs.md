# Transitive Closure of Graph using DFS

Given a directed graph, find out if a vertex v is reachable from another vertex u for all vertex pairs \(u, v\) in the given graph. Here reachable mean that there is a path from vertex u to v. The reach-ability matrix is called transitive closure of a graph.

O\(V^3\) solution based on [Floyd Warshall Algorithm](../../../data-structures/graphs/graph-algorithms/floyd-warshall-algorithm-for-transitive-closure.md) is discussed already. Here we will discuss O\(V^2\).

### Algorithm

1. Create a `tc[V][V]` that would finally have tranisitve closure of given graph. Initialize all entries of `tc[][]` as 0.
2. Call DFS for every node of graph to mark reachable vertices in `tc[][]`. In recursive calls to DFS, we don't call DFS for an adjacent vertex if it is already as reachable in`tc[][]`

###  Implementation

The code uses adjacency list representation of input graph and builds a matrix `tc[V][V]` such that `tc[u][v]` would be true if v is reachable from u.

```cpp
class Graph
{
    int V; // No. of vertices
    bool **tc; // To store transitive closure
    list<int> *adj; // array of adjacency lists
    
    // A recursive DFS traversal function that finds
    // all reachable vertices for s.    
    void DFSUtil(int s, int v)
    {
        // Mark reachability from s to t as true.
        tc[s][v] = true;
   
        // Find all the vertices reachable through v
        list<int>::iterator i;
        for (i = adj[v].begin(); i != adj[v].end(); ++i)
            if (tc[s][*i] == false)
                DFSUtil(s, *i);
    }
public:
    Graph(int V) { // Constructor
        this->V = V;
        adj = new list<int>[V];
   
        tc = new bool* [V];
        for (int i = 0; i < V; i++)
        {
            tc[i] = new bool[V];
            memset(tc[i], false, V*sizeof(bool));
        }
    }
   
    // function to add an edge to graph
    void addEdge(int v, int w) 
    { 
        adj[v].push_back(w); 
    }
   
    // prints transitive closure matrix
    void transitiveClosure()
    {
        // Call the recursive helper function to print DFS
        // traversal starting from all vertices one by one
        for (int i = 0; i < V; i++)
            DFSUtil(i, i); // Every vertex is reachable from self.
   
        for (int i = 0; i < V; i++)
        {
            for (int j = 0; j < V; j++)
                cout << tc[i][j] << " ";
            cout << endl;
        }
    }
};
```

