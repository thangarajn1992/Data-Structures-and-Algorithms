# Is Graph Bipartite

### Source

* [Leetcode 785](https://leetcode.com/problems/is-graph-bipartite/)
* [Leetcode 886](https://leetcode.com/problems/possible-bipartition/)



A Bipartite Graph is a graph whose vertices can be divided into two independent sets, U and V such that every edge \(u, v\) either connects a vertex from U to V or a vertex from V to U. In other words, for every edge \(u, v\), either u belongs to U and v to V, or u belongs to V and v to U. We can also say that there is no edge that connects vertices of same set.

![](../../.gitbook/assets/image%20%2815%29.png)

A bipartite graph is possible if the graph coloring is possible using two colors such that vertices in a set are colored with the same color.

### Approach

One approach would be to use [backtracking algorithm - m coloring problem](m-coloring-a-graph.md). Here we will use simple algorithm to find out whether a given graph is Bipartite or not using BFS.

1. Assign RED color to the source vertex \( Putting into set U\).
2. Color all the neighbors with BLUE color \(Putting into set V\).
3. Color all neighbor's neighbor with RED color \(Putting into set U\).
4. While assigning colors, if we find a neighbor which is colored with same color as current vertex, then the graph cannot be colored with 2 vertices \(or graph is not Bipartite\).

### Implementation

```cpp
bool isBipartite(int V, vector<int> adj[])
{
    // vector to store colour of vertex
    // assiging all to -1 i.e. uncoloured
    // colours are either 0 or 1
    // for understanding take 0 as red and 1 as blue
    vector<int> col(V, -1);
 
    // queue for BFS storing {vertex , colour}
    queue<pair<int, int>> q;
   
    // loop incase graph is not connected
    for (int i = 0; i < V; i++) {
       
        // if not coloured
        if (col[i] == -1) {
           
            // colouring with 0 i.e. red
            q.push({ i, 0 });
            col[i] = 0;
           
            while (!q.empty()) {
                pair<int, int> p = q.front();
                q.pop();
               
                // current vertex
                int u = p.first;
                // colour of current vertex
                int c = p.second;
                 
                // traversing neighbors
                for (int v : adj[u]) {
                    // if already coloured with parent vertex color
                    // then bipartite graph is not possible
                    if (col[v] == c)
                        return 0;
                   
                    //if uncoloured
                    if (col[v] == -1) {
                        //colouring with opposite color to that of parent
                        col[v] = (c) ? 0 : 1;
                        q.push({ v, col[v] });
                    }
                }
            }
        }
    }
    //if all vertexes are coloured such that no two connected vertex have same colours
    return 1;
}
```

