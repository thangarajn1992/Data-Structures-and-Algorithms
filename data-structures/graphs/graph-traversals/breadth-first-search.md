# Breadth First Traversal

Breadth First Traversal\(search\) for a graph is similar to Breadth First Traversal of a tree. The only difference here is, unlike trees, graphs may contain cycles, so we may come to the same node again. To avoid processing a node more than once, we use a boolean visited array.

![](../../../.gitbook/assets/image%20%287%29.png)

The BFS traversal of this graph is `[2, 0, 3, 1]`

BFS traverses only the vertices reachable from a given source vertex. All the vertices may not be reachable from a given vertex \( disconnnected graph \). To print all the vertices, we can modify the BFS function to do traversal starting from all nodes one by one.

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

