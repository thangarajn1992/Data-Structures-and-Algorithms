# Graph using Set and Hash

Graph using vectors is discussed [here](graph-using-vectors.md).

A set is different from a vector in two ways: It sotres elements in sorted way, and duplicate elements are not allowed. Therefore, this approach cannot be used for graphs containing parallel edges. Since sets are internally implemented as binary search trees, **an edge between two vertices can be searched in O(logV) time, **where V is the number of vertices in the graph.

### Graph Implementation Using Ordered Set

**Advantages: **

Queries like whether there is annn edge between 2 vertex can be done in O(logV).

**Disadvantages:** 

* Adding** **an edge takes O(log V), as opposed to O(1) in vector implementation
* Graphs containing parallel edges cannot be implemented through this method.

```cpp
struct Graph {
    int V;
    set<int, greater<int> >* adjList;
};
 
// A utility function that creates a graph of V vertices
Graph* createGraph(int V)
{
    Graph* graph = new Graph;
    graph->V = V;
 
    // Create an array of sets representing
    // adjacency lists.  Size of the array will be V
    graph->adjList = new set<int, greater<int> >[V];
 
    return graph;
}
 
// Adds an edge to an undirected graph
void addEdge(Graph* graph, int src, int dest)
{
    // Add an edge from src to dest.  A new
    // element is inserted to the adjacent
    // list of src.
    graph->adjList[src].insert(dest);
 
    // Since graph is undirected, add an edge
    // from dest to src also
    graph->adjList[dest].insert(src);
}
 
// A utility function to print the adjacency
// list representation of graph
void printGraph(Graph* graph)
{
    for (int i = 0; i < graph->V; ++i) {
        set<int, greater<int> > lst = graph->adjList[i];
        cout << endl << "Adjacency list of vertex " << i << endl;
 
        for (auto itr = lst.begin(); itr != lst.end(); ++itr)
            cout << *itr << " ";
        cout << endl;
    }
}
 
// Searches for a given edge in the graph
void searchEdge(Graph* graph, int src, int dest)
{
    auto itr = graph->adjList[src].find(dest);
    if (itr == graph->adjList[src].end())
        cout << endl << "Edge from " << src
             << " to " << dest << " not found."
             << endl;
    else
        cout << endl << "Edge from " << src
             << " to " << dest << " found."
             << endl;
}
```

### Graph Implementation using Unordered sets

**Advantages**

* Queries like whether there is an edge from vertex u to vertex v can be done in O(1).
* Adding an edge takes O(1).

**Disadvantages**

* Graphs containing parallel edge(s) cannot be implemented through this method.
* Edges are stored in any order.

```cpp
struct Graph {
    int V;
    unordered_set<int>* adjList;
};
 
// A utility function that creates a graph of
// V vertices
Graph* createGraph(int V)
{
    Graph* graph = new Graph;
    graph->V = V;
 
    // Create an array of sets representing
    // adjacency lists. Size of the array will be V
    graph->adjList = new unordered_set<int>[V];
 
    return graph;
}
 
// Adds an edge to an undirected graph
void addEdge(Graph* graph, int src, int dest)
{
    // Add an edge from src to dest. A new
    // element is inserted to the adjacent
    // list of src.
    graph->adjList[src].insert(dest);
 
    // Since graph is undirected, add an edge
    // from dest to src also
    graph->adjList[dest].insert(src);
}
 
// A utility function to print the adjacency
// list representation of graph
void printGraph(Graph* graph)
{
    for (int i = 0; i < graph->V; ++i) {
        unordered_set<int> lst = graph->adjList[i];
        cout << endl << "Adjacency list of vertex "
             << i << endl;
 
        for (auto itr = lst.begin(); itr != lst.end(); ++itr)
            cout << *itr << " ";
        cout << endl;
    }
}
 
// Searches for a given edge in the graph
void searchEdge(Graph* graph, int src, int dest)
{
    auto itr = graph->adjList[src].find(dest);
    if (itr == graph->adjList[src].end())
        cout << endl << "Edge from " << src
             << " to " << dest << " not found."
             << endl;
    else
        cout << endl << "Edge from " << src
             << " to " << dest << " found."
             << endl;
}
```
