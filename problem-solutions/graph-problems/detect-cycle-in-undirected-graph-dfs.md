# Detect Cycle in Undirected Graph DFS

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/detect-cycle-in-an-undirected-graph/1#)

### Companies

* [Amazon](../../company-based-lists/amazon.md)
* [Microsoft](../../company-based-lists/microsoft.md)
* [Flipkart](../../company-based-lists/flipkart.md)
* [Samsung](../../company-based-lists/samsung.md)
* [Adobe](../../company-based-lists/adobe.md)

### Problem Statement

Given an undirected graph with V vertices and E edges, check whether it contains any cycle or not. ****![](C:\Users\Mukul%20kumar\Desktop\GFG_PIC.JPG)

**Example 1:**

```text
Input:   

Output: 1
Explanation: 1->2->3->4->1 is a cycle.
```

**Example 2:**

```text
Input: 

Output: 0
Explanation: No cycle in the graph.
```

**Your Task:**  
 You don't need to read or print anything. Your task is to complete the function **isCycle\(\)** which takes V denoting the number of vertices and adjacency list as input parameters and returns a boolean value denoting if the undirected graph contains any cycle or not, return 1 if a cycle is present else return 0.

**NOTE:** The adjacency list denotes the edges of the graph where edges\[i\]\[0\] and edges\[i\]\[1\] represent an edge.

**Expected Time Complexity:** O\(V + E\)  
**Expected Space Complexity:** O\(V\)

**Constraints:**  
 1 ≤ V, E ≤ 10^5

### Solution

```cpp
class Solution {
  public:
    // Function to detect cycle in an undirected graph.
    bool isCycle(int V, vector<int> adj[]) {
        vector<bool> visited(V, false);
        for(int v = 0; v < V; v++)
        {
            if(visited[v] == false) // to take care of disconnected graph
            {
                if(isCycleDFS(-1, v, visited, adj) == true)
                    return true;
            }
        }
        return false;
    }
    bool isCycleDFS(int parent, int vertex, vector<bool> & visited, vector<int> adj[])
    {
        visited[vertex] = true;
        for(int neighbor : adj[vertex])
        {
            if(neighbor != parent && (visited[neighbor] == true || 
               isCycleDFS(vertex, neighbor, visited, adj) == true))
                return true;
        }
        return false;
    }
};

```

