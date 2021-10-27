# Strongly Connected Component (Kosaraju's Algorithm)

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/strongly-connected-components-kosarajus-algo/1#)

### Companies

* [Amazon](../../company-based-lists/amazon.md)
* [Microsoft](../../company-based-lists/microsoft.md)

### Problem Statement

Given a Directed Graph with **V** vertices **(**Numbered from **0 to V-1)** and **E** edges, Find the number of strongly connected components in the graph.

**Example 1:**

![](<../../.gitbook/assets/image (38).png>)

```
Output:
3
Explanation:

We can clearly see that there are 3 Strongly
Connected Components in the Graph
```

**Example 2:**

![](<../../.gitbook/assets/image (39).png>)

```
Output:
1
Explanation:
All of the nodes are connected to each other.
So, there's only one SCC.
```

**Expected Time Complexity:** O(V+E).\
**Expected Auxiliary Space:** O(V).\
&#x20;&#x20;

**Constraints:**\
&#x20;1 ≤ V ≤ 5000\
&#x20;0 ≤ E ≤ (V\*(V-1))\
&#x20;0 ≤ u, v ≤ N-1\
&#x20;Sum of E over all testcases will not exceed 25\*10^6

### **Solution**

For more details on [kosaraju's Algorithm](../../data-structures/graphs/graph-algorithms/kosarajus-algorithm.md)

```cpp
class Graph
{
    int V;  
    vector<vector<int>> adj;
    
    void fillOrder(int v, vector<bool> &visited, stack<int> &s)
    {
        visited[v] = true;
        for(int i = 0; i < adj[v].size(); i++)
            if(!visited[adj[v][i]])
                fillOrder(adj[v][i], visited, s);
        
        s.push(v);
    }
    
    void DFSUtil(int v, vector<bool> &visited)
    {
        visited[v] = true;
        // Print or do what u need with this element
        for(int i = 0; i < adj[v].size(); i++)
            if(!visited[adj[v][i]])
                DFSUtil(adj[v][i], visited);
        
    }
    public:
    Graph(int V)
    {
        this->V = V;
        this->adj.resize(V);
    }
    
    void addEdge(int v, int w)
    {
        adj[v].push_back(w);
    }
    
    Graph getTranspose()
    {
        Graph gf(V);
        for(int v = 0; v < V; v++)
            for(int i = 0; i < adj[v].size(); i++)
                gf.adj[adj[v][i]].push_back(v);
                      
        return gf;
    }
    
    int get_Scc_Count()
    {
        stack<int> s;
        int count = 0;
        
        vector<bool> visited(V,false);

        for(int i = 0; i < V; i++)
            if(!visited[i])
                fillOrder(i, visited, s);
                
        Graph gr = getTranspose();
        
        for(int i = 0; i < V; i++) 
            visited[i] = false;

        while(!s.empty())
        {
            int v = s.top(); s.pop();
            if(!visited[v])
            {
                gr.DFSUtil(v, visited);
                count++;
            }
        }
        return count;
    }
};

class Solution
{
public:
    int kosaraju(int V, vector<int> adj[])
    {
        Graph g(V);
        for(int v = 0; v < V; v++)
            for(int i = 0; i < adj[v].size(); i++)
                g.addEdge(v, adj[v][i]);
    
        return g.get_Scc_Count();
    }
};
```

