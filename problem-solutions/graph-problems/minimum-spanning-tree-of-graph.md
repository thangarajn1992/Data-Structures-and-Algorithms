# Minimum Spanning Tree of Graph

### Sources

* [GeeksForGeeks](https://practice.geeksforgeeks.org/problems/minimum-spanning-tree/1#)

### Companies

* [Amazon](../../company-based-lists/amazon.md)
* [Microsoft](../../company-based-lists/microsoft.md)
* [Flipkart](../../company-based-lists/flipkart.md)
* [Samsung](../../company-based-lists/samsung.md)
* Cisco

### Problem Statement

Given a weighted, undirected and connected graph of **V** vertices and **E** edges. The task is to find the sum of weights of the edges of the Minimum Spanning Tree.

&#x20;

**Example 1:**

****![](<../../.gitbook/assets/image (58).png>)****

****![](<../../.gitbook/assets/image (59).png>)****

```
Output:
4

The Spanning Tree resulting in a weight
of 4 is shown above.
```

**Example 2:**

****![](<../../.gitbook/assets/image (57).png>)****

```
Output:
5
Explanation:
Only one Spanning Tree is possible
which has a weight of 5.
```

&#x20;

**Your task:**\
Since this is a functional problem you don't have to worry about input, you just have to complete the function  **spanningTree()** which takes number of vertices V** **and** **an adjacency matrix adj as input parameters and returns an integer denoting the sum of weights of the edges of the Minimum Spanning Tree. Here adj\[i] contains a list of lists containing two integers where the first integer a\[i]\[0] denotes that there is an edge between i and a\[i]\[0] and second integer a\[i]\[1] denotes that the distance between edge i and a\[i]\[0] is a\[i]\[1].

**Expected Time Complexity: **O(ElogV).\
**Expected Auxiliary Space: **O(V**^**2).\
&#x20;

**Constraints:**\
2 ≤ V ≤ 1000\
V-1 ≤ E ≤ (V\*(V-1))/2\
1 ≤ w ≤ 1000\
Graph is connected and doesn't contain self loops & multiple edges.

### Solution

```cpp
class Solution
{
	public:
	int V;
	//Function to find sum of weights of edges of the Minimum Spanning Tree.
    int spanningTree(int V, vector<vector<int>> adj[])
    {
        this->V = V;
        vector<vector<int>> graph(V, vector<int>(V,0));
        
        for(int v = 0; v < V; v++)
        {
            for(vector<int> myadj : adj[v])
                graph[v][myadj[0]] = myadj[1];
        }
        
        // Array to store constructed MST
        int parent[V];
     
        // Key values used to pick minimum weight edge in cut
        int key[V];
     
        // To represent set of vertices included in MST
        bool mstSet[V];
 
        // Initialize all keys as INFINITE
        for (int i = 0; i < V; i++)
            key[i] = INT_MAX, mstSet[i] = false;
 
        // Always include first vertex in MST.
        // Make key 0 so that this vertex is picked as first vertex.
        key[0] = 0;
        parent[0] = -1; // First node is always root of MST
 
        // The MST will have V vertices
        for (int count = 0; count < V - 1; count++)
        {
            // Pick the minimum key vertex from the
            // set of vertices not yet included in MST
            int u = minKey(key, mstSet);
 
            // Add the picked vertex to the MST Set
            mstSet[u] = true;
 
            // Update key value and parent index of
            // the adjacent vertices of the picked vertex.
            // Consider only those vertices which are not
            // yet included in MST
            for (int v = 0; v < V; v++)
                // graph[u][v] is non zero only for adjacent vertices of m
                // mstSet[v] is false for vertices not yet included in MST
                // Update the key only if graph[u][v] is smaller than key[v]
                if (graph[u][v] && mstSet[v] == false && graph[u][v] < key[v])
                    parent[v] = u, key[v] = graph[u][v];
        }
 
 
        int mstSum = 0;
        for (int i = 1; i < V; i++)
            mstSum += graph[i][parent[i]];
        
        return mstSum;
    }
    
    int minKey(int key[], bool mstSet[])
    {   
        // Initialize min value
        int min = INT_MAX, min_index;
 
        for (int v = 0; v < V; v++)
            if (mstSet[v] == false && key[v] < min)
                min = key[v], min_index = v;
 
        return min_index;
    }
    
};
```
