# Kahn's Algorithm - Topological Sorting for Directed Acyclic Graph (DAG)

Topological sorting for a graph is not possible if the graph is not a [Directed Acyclic Graph(DAG)](../graph-terminology.md#directed-acyclic-graph-dag). Topological sorting for DAG is a linear ordering of vertices such that for every directed edge uv, vertex u comes before v in the ordering. There can be more than one topological sorting for a graph. The first vertex in topological sorting is always with in-degree as 0 ( a vertex with no in-coming edges). **A DAG has at least one vertex with in-degree 0 and one vertex with out-degree 0.** Kahn's Algorithm is also used for [detecting cycle in directed graph with BFS](../../../problem-solutions/graph-problems/detect-cycle-in-a-directed-graph-using-bfs.md)

### Approach

**Step 1:** Compute in-degree ( number of incoming edges) for each of the vertex present in the graph and initialize the count of visited nodes as 0.

**Step 2:** Pick all the vertices with in-degree as 0 and add them into the queue.

**Step 3:** Remove a vertex from the queue and then

1. Increment count of visited nodes by 1.
2. Decrease in-degree by 1 for all its neighboring nodes.
3. If in-degree of neighboring nodes is reduced to zero, then add it to queue.

**Step 4:** Repeat Step 3 until the queue is empty

**Step 5:** If count of visited nodes is not equal to the number of nodes in the graph then it has cycle, otherwise not.

#### How to find in-degree of each node?

We can calculate in-degree in 2 ways

1. Traverse the array of edges and simply increase the counter of the destination node by 1. Time Complexity: O(V+E).
2. Traverse the list for every node and then increment the in-degree of all the nodes connected to it by 1. Time Complexity: O(V+E).

### Implementation

```cpp
// Class to represent a graph
class Graph {
    int V; // No. of vertices
    list<int>* adj; // Pointer to an array containing adjacency lists
  
public:
    // Constructor
    Graph(int V)
    {
      this->V = V;
      adj = new list<int>[V];
    }
  
    // Function to add an edge to graph
    void addEdge(int u, int v)
    {
      adj[u].push_back(v);
    }
    
    // prints a Topological Sort of the complete graph
    void topologicalSort()
    {
          // Create a vector to store indgrees of all vertices.
          // Initialize all indegrees as 0.
          vector<int> in_degree(V, 0);
  
          // Traverse adjacency lists to fill indegrees of vertices.
          // This step takes O(V+E) time
 
          for (int u = 0; u < V; u++) {
              list<int>::iterator itr;
              for (itr = adj[u].begin(); itr != adj[u].end(); itr++)
                  in_degree[*itr]++;
          }
  
          // Create an queue and enqueue
          // all vertices with indegree 0
          queue<int> q;
          for (int i = 0; i < V; i++)
              if (in_degree[i] == 0)
                  q.push(i);
  
         // Initialize count of visited vertices
        int cnt = 0;
  
        // Create a vector to store result (Topological Order)
        vector<int> top_order;
  
        // One by one dequeue vertices from queue
        // and enqueue adjacents if its indegree becomes 0
        while (!q.empty()) {
            // Extract front of queue and add to topological order
            int u = q.front();
            q.pop();
            top_order.push_back(u);
  
            // Iterate through all its neighboring nodes
            // and decrease their in-degree by 1
            list<int>::iterator itr;
            for (itr = adj[u].begin(); itr != adj[u].end(); itr++)    
            // If in-degree becomes zero, add it to queue
                if (--in_degree[*itr] == 0)
                    q.push(*itr);
  
            cnt++;
        }
  
        // Check if there was a cycle
        // Only DAG can have topological order
        if (cnt != V) {
            cout << "There exists a cycle in the graph\n";
            return;
        }
  
        // Print topological order
        for (int i = 0; i < top_order.size(); i++)
            cout << top_order[i] << " ";
        cout << endl;
    }    
};
```
