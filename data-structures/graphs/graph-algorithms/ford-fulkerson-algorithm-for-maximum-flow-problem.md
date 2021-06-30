# Ford-Fulkerson Algorithm for Maximum Flow Problem

### Maximum Flow Problem

Maximum Flow problems involve finding a feasible flow through a single-source, single-sink flow network that is maximum.

![](../../../.gitbook/assets/image%20%2818%29.png)

Each edge is labeled with capcity, the maximum amount of stuff that it can carry. The goal is to figure out how much stuff can be pushed from the vertex s\(source\) to the vertex t\(sink\).

1. Flow on an edge doesn't exceed the given capacity of the edge
2. Incoming flow is equal to outgoing flow for every vertex except s and t.

![](../../../.gitbook/assets/image%20%2810%29.png)

Greedy Algorithm won't provide us the best possible solution, hence we need to use residual graphs approach

### Residual Graph

Residual Graph of a flow network is a graph which indicates additional possible flow. If there is a path from source to sink in residual graph, then it is possible to add flow. Every edge of a residual graph has a value called **Residual Capacity,** which is equal to original capcacity of the edge minus current flow. It is basically the current capacity of the edge.

### Implementation

1. Initialize the residual graph as original graph as there is no initial flow and initial residual capacity is equal to original capacity.
2. To find an augmenting path, we can either BFS or DFS of the residual graph. BFS is used here. Using BFS
   1. We can find out if there is a path from source to sink.
   2. BFS also builds parent\[\] array. Using parent\[\] array, we traverse through the found path and find possible flow through this path by finding minimum residual capacity along the path.
   3. We later add found path flow to overall flow.
3. Important thing is, we need to update residual capcacities in the residual graph. We substract path flow from all edges along the path and we add path flow along the reverse edges because may be later need to send flow in reverse direction.

**Time Complexity:** O\(max\_flow \* E\). We run a loop while there is an augmenting path. In worst case, we may add 1 unit flow in every iteration.

**Applications:**

* Maximizing the transportation with given traffic limits
* Maximizinng packet flow in computer networks.

### Implementation

This implementation of Ford Fulkerson Algorithm is called Edmonds-Karp Algorithm. The idea is to use BFS in Ford Fulkerson implementation as BFS always picks a path with minimum number of edges. When BFS is used, the worst case time complexity can be reduced to O\(VE^2\).

```cpp
// Number of vertices in given graph
#define V 6
 
/* Returns true if there is a path from source 's' to sink
  't' in residual graph. Also fills parent[] to store the
  path */
bool bfs(int rGraph[V][V], int s, int t, int parent[])
{
    // Create a visited array and mark all vertices as not
    // visited
    bool visited[V];
    memset(visited, 0, sizeof(visited));
 
    // Create a queue, enqueue source vertex and mark source
    // vertex as visited
    queue<int> q;
    q.push(s);
    visited[s] = true;
    parent[s] = -1;
 
    // Standard BFS Loop
    while (!q.empty()) {
        int u = q.front();
        q.pop();
 
        for (int v = 0; v < V; v++) {
            if (visited[v] == false && rGraph[u][v] > 0) {
                // If we find a connection to the sink node,
                // then there is no point in BFS anymore We
                // just have to set its parent and can return
                // true
                if (v == t) {
                    parent[v] = u;
                    return true;
                }
                q.push(v);
                parent[v] = u;
                visited[v] = true;
            }
        }
    }
 
    // We didn't reach sink in BFS starting from source, so
    // return false
    return false;
}
 
// Returns the maximum flow from s to t in the given graph
int fordFulkerson(int graph[V][V], int s, int t)
{
    int u, v;
 
    // Create a residual graph and fill the residual graph
    // with given capacities in the original graph as
    // residual capacities in residual graph
    int rGraph[V]
              [V]; // Residual graph where rGraph[i][j]
                   // indicates residual capacity of edge
                   // from i to j (if there is an edge. If
                   // rGraph[i][j] is 0, then there is not)
    for (u = 0; u < V; u++)
        for (v = 0; v < V; v++)
            rGraph[u][v] = graph[u][v];
 
    int parent[V]; // This array is filled by BFS and to
                   // store path
 
    int max_flow = 0; // There is no flow initially
 
    // Augment the flow while there is path from source to
    // sink
    while (bfs(rGraph, s, t, parent)) {
        // Find minimum residual capacity of the edges along
        // the path filled by BFS. Or we can say find the
        // maximum flow through the path found.
        int path_flow = INT_MAX;
        for (v = t; v != s; v = parent[v]) {
            u = parent[v];
            path_flow = min(path_flow, rGraph[u][v]);
        }
 
        // update residual capacities of the edges and
        // reverse edges along the path
        for (v = t; v != s; v = parent[v]) {
            u = parent[v];
            rGraph[u][v] -= path_flow;
            rGraph[v][u] += path_flow;
        }
 
        // Add path flow to overall flow
        max_flow += path_flow;
    }
 
    // Return the overall flow
    return max_flow;
}
```

\*\*\*\*



