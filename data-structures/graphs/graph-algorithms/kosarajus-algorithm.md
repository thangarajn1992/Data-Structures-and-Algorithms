# Kosaraju's algorithm for strongly connected components

## Kosaraju-Sharir's Algorithm (or Kosaraju's Algorithm)

It is linear time algorithm to find the strongly connected components of a directed graph. It makes use of the fact that the **transpose graph ( the same graph with the direction of the every edge reversed) has exactly the same strongly connected components as the original graph.**

### Strongly Connected Components

A directed graph is strongly connected if there is a **path between all pairs of vertices**. A strongly connected component (SCC) of a directed graph is a maximal strongly connected sub-graph. For eg., there are 3 SCCs in the following graph.

![](<../../../.gitbook/assets/image (1).png>)

We can find all strongly connected components in (V+E) time using kosaraju's algorithm.

### Algorithm

The primitive graph operations that the algorithm uses are

1. Enumerate the vertices of the graph
2. Store data per vertex (if not in the graph data structure itself, then in some table that can use vertices as indices)
3. Enumerate the out-neighbors of a vertex ( traverse edges in forward direction)
4. Enumerate the in-neighbors of a vertex ( traverse edges in the backward direction)

However, the last can be done without, at the price of constructing a representation of the transpose graph during the forward traversal phase. The only additional data structure needed by the algorithm is an ordered list L of graph vertices, that will grow to contain each vertex once.

If strong components are to be represented by appointing a separate root vertex for each component, and assigning to each vertex the root vertex of its component, then Kosaraju's algorithm can be stated as follows.

1. For each vertex u of the graph, mark u as unvisited. Let L be empty.
2. For each vertex u of the graph, do Visit(u), where Visit(u) is recursive subroutine:
   1. If u is unvisited, then
      1. Mark u as visited
      2. For each out-neighbor v of u, do Visit(v).
      3. Prepend U to L
   2. Otherwise do nothing
3. For each element u of L in order, do Assign (u,root) where Assign(u,root) is the recursive subroutine:
   1. If u has not been assigned to a component then:
      1. Assign u as belonging to the component whose root is root.
      2. For each in-neighbor v of u, do Assign(v,root).
   2. Otherwise do nothing

Vertices are prepended to the list L in post-order relative to the search tree being explored. They key point of algorithm is that, **if there is a forward path from u to v, then u will appear before v on the final list L ( unless u and v both belong to the same strong component, in which case their relative order in L is arbitrary).**&#x20;

This algorithm in short can be understood as identifying the **strong component of a vertex u as the set of vertices which are reachable from u both by backwards and forwards traversal.**

## C++ Implementation of Kosaraju's Algorithm

```cpp
// C++ Implementation of Kosaraju's algorithm to print all SCCs
#include <iostream>
#include <list>
#include <stack>
using namespace std;
  
class Graph
{
    int V;    // No. of vertices
    list<int> *adj;    // An array of adjacency lists
  
    // Fills Stack with vertices (in increasing order of finishing
    // times). The top element of stack has the maximum finishing 
    // time
    void fillOrder(int v, bool visited[], stack<int> &Stack);
  
    // A recursive function to print DFS starting from v
    void DFSUtil(int v, bool visited[]);
public:
    Graph(int V);
    void addEdge(int v, int w);
  
    // The main function that finds and prints strongly connected
    // components
    void printSCCs();
  
    // Function that returns reverse (or transpose) of this graph
    Graph getTranspose();
};
  
Graph::Graph(int V)
{
    this->V = V;
    adj = new list<int>[V];
}
  
// A recursive function to print DFS starting from v
void Graph::DFSUtil(int v, bool visited[])
{
    // Mark the current node as visited and print it
    visited[v] = true;
    cout << v << " ";
  
    // Recur for all the vertices adjacent to this vertex
    list<int>::iterator i;
    for (i = adj[v].begin(); i != adj[v].end(); ++i)
        if (!visited[*i])
            DFSUtil(*i, visited);
}
  
Graph Graph::getTranspose()
{
    Graph g(V);
    for (int v = 0; v < V; v++)
    {
        // Recur for all the vertices adjacent to this vertex
        list<int>::iterator i;
        for(i = adj[v].begin(); i != adj[v].end(); ++i)
        {
            g.adj[*i].push_back(v);
        }
    }
    return g;
}
  
void Graph::addEdge(int v, int w)
{
    adj[v].push_back(w); // Add w to v’s list.
}
  
void Graph::fillOrder(int v, bool visited[], stack<int> &Stack)
{
    // Mark the current node as visited and print it
    visited[v] = true;
  
    // Recur for all the vertices adjacent to this vertex
    list<int>::iterator i;
    for(i = adj[v].begin(); i != adj[v].end(); ++i)
        if(!visited[*i])
            fillOrder(*i, visited, Stack);
  
    // All vertices reachable from v are processed by now, push v 
    Stack.push(v);
}
  
// The main function that finds and prints all strongly connected 
// components
void Graph::printSCCs()
{
    stack<int> Stack;
  
    // Mark all the vertices as not visited (For first DFS)
    bool *visited = new bool[V];
    for(int i = 0; i < V; i++)
        visited[i] = false;
  
    // Fill vertices in stack according to their finishing times
    for(int i = 0; i < V; i++)
        if(visited[i] == false)
            fillOrder(i, visited, Stack);
  
    // Create a reversed graph
    Graph gr = getTranspose();
  
    // Mark all the vertices as not visited (For second DFS)
    for(int i = 0; i < V; i++)
        visited[i] = false;
  
    // Now process all vertices in order defined by Stack
    while (Stack.empty() == false)
    {
        // Pop a vertex from stack
        int v = Stack.top();
        Stack.pop();
  
        // Print Strongly connected component of the popped vertex
        if (visited[v] == false)
        {
            gr.DFSUtil(v, visited);
            cout << endl;
        }
    }
}
  
// Driver program to test above functions
int main()
{
    // Create a graph given in the above diagram
    Graph g(5);
    g.addEdge(1, 0);
    g.addEdge(0, 2);
    g.addEdge(2, 1);
    g.addEdge(0, 3);
    g.addEdge(3, 4);
  
    cout << "Following are strongly connected components in "
            "given graph \n";
    g.printSCCs();
  
    return 0;
}
```



