# Breadth First Traversal

Breadth First Traversal(search) for a graph is similar to Breadth First Traversal of a tree. The only difference here is, unlike trees, graphs may contain cycles, so we may come to the same node again. To avoid processing a node more than once, we use a boolean visited array.

![](<../../../.gitbook/assets/image (7).png>)

The BFS traversal of this graph is `[2, 0, 3, 1]`

BFS traverses only the vertices reachable from a given source vertex. All the vertices may not be reachable from a given vertex ( disconnnected graph ). To print all the vertices, we can modify the BFS function to do traversal starting from all nodes one by one.

### BFS from a given Node in Connected Graph

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
    Graph(int V)  // Constructor
    {
        this->V = V;
        adj = new list<int>[V];
    }
 
    // function to add an edge to graph
    void addEdge(int v, int w)
    {
        adj[v].push_back(w); // Add w to v's list.
    }
 
    // prints BFS traversal from a given source s
    void BFS(int s)
    {
        // Mark all the vertices as not visited
        bool *visited = new bool[V];
        for(int i = 0; i < V; i++)
            visited[i] = false;
 
        // Create a queue for BFS
        list<int> queue;
 
        // Mark the current node as visited and enqueue it
        visited[s] = true;
        queue.push_back(s);
 
        // 'i' will be used to get all adjacent
        // vertices of a vertex
        list<int>::iterator i;
 
        while(!queue.empty())
        {
            // Dequeue a vertex from queue and print it
            s = queue.front();
            cout << s << " ";
            queue.pop_front();
 
            // Get all adjacent vertices of the dequeued
            // vertex s. If a adjacent has not been visited,
            // then mark it visited and enqueue it
            for (i = adj[s].begin(); i != adj[s].end(); ++i)
            {
                if (!visited[*i])
                {
                    visited[*i] = true;
                    queue.push_back(*i);
                }
            }
        }
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
 
    cout << "Following is Breadth First Traversal "
         << "(starting from vertex 2) \n";
    g.BFS(2);
 
    return 0;
}
```

### Modified BFS for Disconnected Graphs



## Applications of Breadth-First Search

### 1. Shortest Path and Minimum Spanning Tree for Unweighted Graph

In an unweighted graph, the shortest path is the path with least number of edges. With Breadth First, we always reach a vertex from a given source using the minimum number of edges. Also, in case of unweighted graphs, any spanning tree is Minimum Spanning Tree and we can either Depth or Breadth first traversal for finding a spanning tree.

### 2. Peer to Peer Networks

In Peer to Peer Networks like BitTorrent, Breadth First Search is used to find all neighbor nodes.

### 3. Crawlers in Search Engines:

Crawlers build index using Breadth First. The idea is to start from source page and follow all links from source and keep doing same. Depth first traversal can also be used for crawlers, but the advantages with BF traversal is, depth or levels of the built tree can be limited.

### 4. Social Networking Websites:

In solcial networks, we can find people within a given distance 'k' from a person using Breadth First Search till 'k' levels.

### 5. GPS Navigation Systems:

BFS is used to find all neighboring locations.

### 6. Broadcasting in Network:

In networks, a broadcasted packet follows BFS to reach all nodes.

### 7. Garbage Collection

BFS is used in copying garbage collection using [Cheney's algorithm](../../../algorithms/cheneys-algorithm.md). BFS is preferred over DFS because of better locality of references.

### 8. Cycle detection in undirected graph

In undirected graph, we can use BFS to detect cycle. We can also use BFS to detect cycle in directed graph.

### 9. Ford-Fulkerson Algorithm

In [Ford-Fulkerson Algorithm](../graph-algorithms/ford-fulkerson-algorithm-for-maximum-flow-problem.md), we can use BF traversal or DF traversal to find the maximum flow. BF traversal reduces worst case time complexity to O(VE^2).

### 10. To test if a graph is Bipartite

To test if a graph is Bipartite, we can either use BF or DF traversal

### 11. Path Finding

We can either use BF or DF traversal to find if there is a path between two vertices.

### 12. Finding all nodes within one connected component

We can use BF or DF traversal to find all nodes reachable from a given node

