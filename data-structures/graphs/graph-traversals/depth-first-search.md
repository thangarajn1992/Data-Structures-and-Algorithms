# Depth First Traversal

Depth First Traversal for a graph is similar to DFS of a tree. The only catch here is, unlike trees, graphs may contain cycles, a node may be visited twice. To avoid processing a node more than once, use a boolean visited array.

The Algorithm starts at the root node \( selecting some arbitary node as root nonde in case of graph\) and explores as far as possible along each branch before backtracking. So the basic idea is to start from the root or any arbitary node and makr the node and move to the adjacent unmarked node and continue this loop until there is no unmarked adjacent nonde. Then backtrack and check for other unmarked nodes and traverse them.

1. Create a recursive function that takes the index of node and a visited array.
2. Mark the current node as visited and print the node.
3. Traverse all the adjacent and unmarked nodes and call the recursive function with index of adjacent node.

### Implementation \( Modified DFS to handle disconnected graphs also\)

All the vertices may not be reachable from a given vertex as in the case of disconnected graph. To do complete DF traversal of such graphs, run DFS for all unvisited nodes after a DFS.

1. Create a recursive function that takes the index of node and a visited array.
2. Mark the current node as visited and print the node.
3. Traverse all the adjacent and unmarked nodes and call the recursive function with index of adjacent node.
4. Run a loop from 0 to number of vertices and check if the node is unvisited in previous DFS then call the recursive function with the current node.

```cpp
class Graph {
    // A function used by DFS
    void DFSUtil(int v)
    {
        // Mark the current node as visited and print it
        visited[v] = true;
        cout << v << " ";
 
        // Recur for all the vertices adjacent to this vertex
        list<int>::iterator i;
        for (i = adj[v].begin(); i != adj[v].end(); ++i)
            if (!visited[*i])
                DFSUtil(*i);
    }
 
public:
    map<int, bool> visited;
    map<int, list<int>> adj;
    // function to add an edge to graph
    void addEdge(int v, int w)
    {
        adj[v].push_back(w); // Add w to v’s list.
    }
 
    // The function to do DFS traversal. It uses recursive DFSUtil()
    void Graph::DFS()
    {
        // Call the recursive helper function to print DFS
        // traversal starting from all vertices one by one
        for (auto i:adj)
            if (visited[i.first] == false)
                DFSUtil(i.first);
    }
};
```

## Application of Depth-First Search \(DFS\)

### 1. Detecting Cycle in a graph

A Graph has cycle if and only if we see a back edge during DFS. So we can run DFS for graph and check for back edges.

### 2. Path Finding

We can specialize the DFS algorithm to find a path between two given vertices u and v.

1. Call DFS\(G,u\) with u as the start vertex.
2. Use a stack S to keep track of the path between the start vertex and the current vertex.
3. As soon as destination vertex z is encountered, return the path as the contents of the stack.

### 3. Topological Sorting

Topological Sorting is mainly used for scheduling jobs from the given dependencies among jobs. In Computer science, applications of this type arise in instruction scheduling, ordering of formula cell evaluation when recomputing formula values in spreadsheets, logic synthesis, determining the order of compilation tasks to perform in makefiles, data serialization, and resolving symbol dependencies in linkers.

### 4. To test if a graph is bipartite

We can use either BF or DF when we first discover a new vertex, color it opposited its parents, and for each other edge, check it doesn't link two vertices of the same color.

### 5. Finding Strongly Connected Components of a graph

A directed graph is called strongly connected if there is a path from each vertex in the graph to every other vertex. Refer [link](../graph-algorithms/kosarajus-algorithm.md)

### 6. Solving Puzzles with only one solution

Solving puzzles like mazes with only solution. If there are multiple solution, DFS can be modified by only including nodes on the current path in the visited set.









