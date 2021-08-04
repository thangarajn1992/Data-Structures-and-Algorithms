# m coloring a graph

Given an undirected graph and a number m, determine if the graph can be coloured with at most m colors such that no adjacent vertices of the graph are colored with same color. Here coloring of a graph means the assignment of colors to all vertices. There may be more than one possible solution.

## Backtracking Approach

1. Create a recursive function that takes the graph, current index, number of vertices, and output color array.
2. If the current index is equal to the number of vertices. Print the color configuration in output array
3. Assign a color\(1 to m\) to vertex.
4. For every assigned color, check if the configuration is safe, \(i.e. check if the adjacent vertices do not have the same color\) recursively call the function with next index and number of vertices.
5. If any recursive function returns true break the loop and return true.
6. If no recursive function returns true, then return false.

### Implementation

**Time Complexity : O\(m^V\)          Space Complexity: O\(V\)**

```cpp
// Number of vertices in the graph
#define V 4
 
void printSolution(int color[]);
 
/* A utility function to check if the current color assignment
   is safe for vertex v i.e. 
   checks whether the edge exists or not (i.e, graph[v][i] == 1)
   If exist then checks whether the color to
   be filled in the new vertex is already
   used by its adjacent
   vertices(i-->adj vertices) or
   not (i.e, color[i] == c) */
bool isSafe(int v, bool graph[V][V],
            int color[], int c)
{
    for(int i = 0; i < V; i++)
        if (graph[v][i] && c == color[i])
            return false;
             
    return true;
}
 
/* A recursive utility function to solve m coloring problem */
bool graphColoringUtil(bool graph[V][V], int m,
                       int color[], int v)
{ 
    /* base case: If all vertices are
       assigned a color then return true */
    if (v == V)
        return true;
 
    /* Consider this vertex v and try different colors */
    for(int c = 1; c <= m; c++)
    {
        /* Check if assignment of color
           c to v is fine*/
        if (isSafe(v, graph, color, c))
        {
            color[v] = c;
            /* recur to assign colors to rest of the vertices */
            if (graphColoringUtil(graph, m, color, v + 1) == true)
                return true;
 
            /* If assigning color c doesn't
               lead to a solution then remove it */
            color[v] = 0;
        }
    }
 
    /* If no color can be assigned to
       this vertex then return false */
    return false;
}
 
/* This function solves the m Coloring problem using Backtracking. 
   It mainly uses graphColoringUtil() to solve the problem. 
   It returns false if the m colors cannot be assigned, 
   otherwise return true and 
   prints assignments of colors to all vertices. 
   Please note that there may be more than one solutions,
   this function prints one of the
   feasible solutions.*/
bool graphColoring(bool graph[V][V], int m)
{    
    // Initialize all color values as 0.
    // This initialization is needed for
    // proper functioning of isSafe()
    int color[V];
    for(int i = 0; i < V; i++)
        color[i] = 0;
 
    // Call graphColoringUtil() for vertex 0
    if (graphColoringUtil(graph, m, color, 0) == false)
    {
        cout << "Solution does not exist";
        return false;
    }
 
    // Print the solution
    printSolution(color);
    return true;
}
```

## BFS Approach

The approach here is to color each node from 1 to n initially by color 1. And start travelling BFS from an unvisited starting node to cover all connected components in one go. On reaching each node during BFS traversal, do the following:

* Check all edges of the given node.
* For each vertex connected to our node via an edge:
  * check if the color of the nodes is the same. If same, increase the color of the other node \(not the current\) by one.
  * check if it visited or unvisited. If not visited, mark it as visited and push it in a queue.
* Check condition for maxColors till now. If it exceeds M, return false

After visiting all nodes, return true \(As no violating condition could be found while travelling\).

### Implementation

**Time Complexity : O\(V+E\)      Space Complexity: O\(V\)**

```cpp
class node
{ 
    // A node class which stores the color and the edges
    // connected to the node
public:
    int color = 1;
    set<int> edges;
};
 
int canPaint(vector<node>& nodes, int n, int m)
{
 
    // Create a visited array of n nodes, initialized to zero
    vector<int> visited(n + 1, 0);
 
    // maxColors used till now are 1 as all nodes are painted color 1
    int maxColors = 1;
 
    // Do a full BFS traversal from all unvisited starting points
    for (int sv = 1; sv <= n; sv++)
    {
 
        if (visited[sv])
            continue;
 
        // If the starting point is unvisited, mark it visited and push it in queue
        visited[sv] = 1;
        queue<int> q;
        q.push(sv);
 
        // BFS Travel starts here
        while (!q.empty())
        {
            int top = q.front();
            q.pop();
 
            // Checking all adjacent nodes to "top" edge in our queue
            for (auto it = nodes[top].edges.begin();
                 it != nodes[top].edges.end(); it++)
            {
 
                // IMPORTANT: If the color of the
                // adjacent node is same, increase it by 1
                if (nodes[top].color == nodes[*it].color)
                    nodes[*it].color += 1;
 
                // If number of colors used shoots m, return
                // 0
                maxColors
                    = max(maxColors, max(nodes[top].color,
                                         nodes[*it].color));
                if (maxColors > m)
                    return 0;
 
                // If the adjacent node is not visited,
                // mark it visited and push it in queue
                if (!visited[*it]) {
                    visited[*it] = 1;
                    q.push(*it);
                }
            }
        }
    }
    return 1;
}
```

