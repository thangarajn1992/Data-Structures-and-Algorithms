# Find a Mother Vertex in a Graph

**What is a Mother Vertex?**

A Mother vertex in a graph G, is a vertex v such that all other vertices in G can be reached by a path from v. There can also be more than one mother vertex in a graph. Our task here is to find one of them.

![](<../../.gitbook/assets/image (21).png>)

### Mother vertex in different types of graphs

* **Case 1:- Undirected Connected Graph :** In this case, all the vertices are mother vertices as we can reach to all the other nodes in the graph.
* **Case 2:- Undirected/Directed Disconnected Graph** : In this case, there is no mother vertices as we cannot reach to all the other nodes in the graph.
* **Case 3:- Directed Connected Graph** : In this case, we have to find a vertex v in the graph such that we can reach to all the other nodes in the graph through a directed path.

### Algorithm

In a graph of strongly connected components, mother vertices are always vertices of source component in component graph. If there exist mother vertex, then one of the mother vertices is the last finished vertex in DFS. A vertex is said to be finished in DFS if a recursive call for its DFS is over i.e all descendants of the vertex have been visited. **A mother vertex has the maximum finish time in DFS traversal.**

1. Do DF traversal of graph. While doing traversal keep track of last finished vertex 'v'. It takes O(V+E)
2. If there exist mother vertex, then v must be one of them. Check if v is a mother vertex by doinng DFS/BFS from v. This step takes O(V+E) time

### Implementation

```cpp
class Graph
{
    int V;    // No. of vertices
    list<int> *adj;    // adjacency lists
 
    // A recursive function to print DFS starting from v
    void DFSUtil(int v, vector<bool> &visited)
    {
        // Mark the current node as visited and print it
        visited[v] = true;
 
        // Recur for all the vertices adjacent to this vertex
        list<int>::iterator i;
        for (i = adj[v].begin(); i != adj[v].end(); ++i)
            if (!visited[*i])
                DFSUtil(*i, visited);
    }
public:
    Graph(int V)
    {
        this->V = V;
        adj = new list<int>[V];
    }
    void addEdge(int v, int w)
    {
        adj[v].push_back(w); // Add w to v’s list.
    }
    // Returns a mother vertex if exists. Otherwise returns -1
    int findMother()
    {    
        // visited[] is used for DFS. Initially all are
        // initialized as not visited
        vector <bool> visited(V, false);
 
        // To store last finished vertex (or mother vertex)
        int v = 0;
 
        // Do a DFS traversal and find the last finished vertex
        for (int i = 0; i < V; i++)
        {
            if (visited[i] == false)
            {
                DFSUtil(i, visited);
                v = i;
            }
        }
 
        // If there exist mother vertex (or vetices) in given
        // graph, then v must be one (or one of them)
 
        // Now check if v is actually a mother vertex (or graph
        // has a mother vertex).  We basically check if every vertex
        // is reachable from v or not.
 
        // Reset all values in visited[] as false and do
        // DFS beginning from v to check if all vertices are
        // reachable from it or not.
        fill(visited.begin(), visited.end(), false);
        DFSUtil(v, visited);
        for (int i = 0; i < V; i++)
            if (visited[i] == false)
                return -1;
 
        return v;
    }
};
```
