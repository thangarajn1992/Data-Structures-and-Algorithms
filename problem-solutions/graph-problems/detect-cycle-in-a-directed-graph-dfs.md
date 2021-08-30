# Detect cycle in a directed graph DFS

### Source

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/detect-cycle-in-a-directed-graph/1#)

### Companies

* [Amazon](../../company-based-lists/amazon.md)
* [Microsoft](../../company-based-lists/microsoft.md)
* [Flipkart](../../company-based-lists/flipkart.md)
* [Adobe](../../company-based-lists/adobe.md)
* [Samsung](../../company-based-lists/samsung.md)

### Problem Statement

Given a Directed Graph with **V** vertices \(Numbered from **0** to **V-1**\) and **E** edges, check whether it contains any cycle or not.  
 **Example 1:**

![Example 1](../../.gitbook/assets/image%20%2828%29.png)



```text
Output: 1
Explanation: 3 -> 3 is a cycle
```

  
 **Example 2:**

![](../../.gitbook/assets/image%20%2831%29.png)



```text
Output: 0
Explanation: no cycle in the graph
```

**Expected Time Complexity:** O\(V + E\)  
**Expected Auxiliary Space:** O\(V\)  
**Constraints:**  
 1 ≤ V, E ≤ 10**^**5

### **Solution**

#### DFS Approach

```cpp
class Solution {
public:
	//Function to detect cycle in a directed graph.
	vector<vector<int>> adj;
	bool isCyclic(int V, vector<int> adj[]) 
	{
        for(int v = 0; v < V; v++)
            this->adj.push_back(adj[v]);
        
        vector<bool> visited(V,false);
        vector<bool> curDFSVisited(V, false);
        
        for(int v = 0; v < V; v++)
            if(!visited[v] && detectLoopByDFS(v, visited, curDFSVisited))
                return true;
                
	   	return false;
	}
	bool detectLoopByDFS(int vertex, vector<bool>&visited, vector<bool>&curDFSVisited)
	{
	    visited[vertex] = true;
	    curDFSVisited[vertex] = true;
        for(int &neighbor : adj[vertex])
        {
            if(curDFSVisited[neighbor] || 
               !visited[neighbor] && detectLoopByDFS(neighbor, visited, curDFSVisited))
                 return true;
        }
        curDFSVisited[vertex] = false;
        return false;
	}
};
```



