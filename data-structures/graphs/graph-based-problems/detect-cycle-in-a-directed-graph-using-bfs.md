# Detect Cycle in a Directed Graph using BFS

Given a directed graph, check whether the graph contains a cycle or not.

![](../../../.gitbook/assets/image%20%2816%29.png)

### Approach

Idea is simply to use [Kahn's Algorithm for topological sorting](../graph-algorithms/kahns-algorithm-topological-sorting-for-directed-acyclic-graph-dag.md).

**Step 1:** Compute in-degree \( number of incoming edges\) for each of the vertex present in the graph and initialise the count of visited nodes as 0.

**Step 2:** Pick all the vertices with in-degree as 0 and add them into the queue.

**Step 3:** Remove a vertex from the queue and then

1. Increment count of visited nodes by 1.
2. Decrease in-degree by 1 for all its neighboring nodes.
3. If in-degree of neighboring nodes is reduced to zero, then add it to queue.

**Step 4:** Repeat Step 3 until the queue is empty

**Step 5:** If count of visited nodes is not equal to the number of nodes in the graph then it has cycle, otherwise not.

#### How to find in-degree of each node?

We can calculate in-degree in 2 ways

1. Traverse the array of edges and simply increase the counter of the destination node by 1. Time Complexity: O\(V+E\).
2. Traverse the list for every node and then increment the in-degree of all the nodes connected to it by 1. Time Complexity: O\(V+E\).

### Implementation

```cpp
// Class to represent a graph
class Graph {
    int V; // No. of vertices'
    list<int> *adj; // Pointer to an array containing adjacency list
 
public:
    Graph(int V) // Constructor
    {
        this->V = V;
        adj = new list<int>[V];
    }
    // function to add an edge to graph
    void addEdge(int u, int v)
    {
        adj[u].push_back(v);
    }
 
    // Returns true if there is a cycle in the graph
    // else false.
    bool isCycle()
    {
        // Create a vector to store indegrees of all
        // vertices. Initialize all indegrees as 0.
        vector<int> in_degree(V, 0);
 
        // Traverse adjacency lists to fill indegrees of
        // vertices. This step takes O(V+E) time
        for (int u = 0; u < V; u++) {
            for (int v : adj[u])
                in_degree[v]++;
        }
 
        // Create an queue and enqueue all vertices with
        // indegree 0
        queue<int> q;
        for (int i = 0; i < V; i++)
            if (in_degree[i] == 0)
                q.push(i);
 
        // Initialize count of visited vertices
        int cnt = 0;
 
        // One by one dequeue vertices from queue and enqueue
        // adjacents if indegree of adjacent becomes 0
        while (!q.empty()) {
 
            // Extract front of queue (or perform dequeue)
            // and add it to topological order
            int u = q.front();
            q.pop();
 
            // Iterate through all its neighbouring nodes
            // of dequeued node u and decrease their in-degree
            // by 1
            list<int>::iterator itr;
            for (itr = adj[u].begin(); itr != adj[u].end(); itr++)
                // If in-degree becomes zero, add it to queue
                if (--in_degree[*itr] == 0)
                    q.push(*itr);
 
            cnt++;
        }
 
        // Check if there was a cycle
        if (cnt != V)
            return true;
        else
            return false;
    }
};
```

