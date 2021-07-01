# Graph using Vectors

Vectors can be used to implement graphs and they are very helpful. Vector, a sequence container, we use it to store adjacency lists of all vertices. We use vertex number as the index in this vector.

### Implementation for DFS using Vectors

```cpp
// A utility function to add an edge in an
// undirected graph.
void addEdge(vector<int> adj[], int u, int v)
{
    adj[u].push_back(v);
    adj[v].push_back(u);
}

// A utility function to do DFS of graph
// recursively from a given vertex u.
void DFSUtil(int u, vector<int> adj[], vector<bool> &visited)
{
    visited[u] = true;
    cout << u << " ";
    for (int i = 0; i < adj[u].size(); i++)
        if (visited[adj[u][i]] == false)
            DFSUtil(adj[u][i], adj, visited);
}

// This function does DFSUtil() for all 
// unvisited vertices.
void DFS(vector<int> adj[], int V)
{
    vector<bool> visited(V, false);
    for (int u = 0; u < V; u++)
        if (visited[u] == false)
            DFSUtil(u, adj, visited);
}
```



