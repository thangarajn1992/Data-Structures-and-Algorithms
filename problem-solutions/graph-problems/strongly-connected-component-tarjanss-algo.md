# Strongly connected component \(Tarjans's Algo\)

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/strongly-connected-component-tarjanss-algo-1587115621/1#)

### Companies

* [Amazon](../../company-based-lists/amazon.md)

### Problem Statement

Given a Directed Graph with V vertices and E edges, Find the members of strongly connected components in the graph.

**Note:** A single strongly connected component must be represented in the form of a list if integers sorted in the ascending order. The resulting list should consist of a list of all SCCs which must be sorted in a way such that a lexicographic-ally smaller list of integers appears first.

  
 **Example 1:**

![](../../.gitbook/assets/image%20%2827%29.png)

```text
Output:
0 1 2,3,4,

Explanation:
We can clearly see that there are 3 Strongly
Connected Components in the Graph as mentioned
in the Output.
```

**Example 2:**

![](../../.gitbook/assets/image%20%2831%29.png)

```text
Output:
0 1 2,

Explanation:
All of the nodes are connected to each other.
So, there's only one SCC as shown.
```

**Expected Time Complexity:** O\(V + E\).  
**Expected Auxiliary Space:** O\(V\).

**Constraints:**  
 1 ≤ V  ≤ 10**^**5  
 1 ≤ E  ≤ 10^5  
 0 ≤ u, v ≤ N-1

### Solution

For more details on [Tarjan's Algorithm for Strongly Connected Components](../../data-structures/graphs/graph-algorithms/tarjans-algorithm-for-strongly-connected-components.md).

```cpp
class Solution
{
	public:
	vector<vector<int>> scc;
	vector<int> discoveryTime;
	vector<int> lowestAncestor;
	vector<bool> stackMember;
	stack<int> st;
	int timer = 0;

    vector<vector<int>> tarjans(int V, vector<int> adj[])
    {
        discoveryTime.resize(V, -1);
        lowestAncestor.resize(V, -1);
        stackMember.resize(V, false);

        for (int v = 0; v < V; v++)
            if (discoveryTime[v] == -1)
                SCCUtil(v, adj);
                
       sort(scc.begin(), scc.end());
       return scc;
    }
    
    void SCCUtil(int u, vector<int> adj[])
    {
        timer++;
        discoveryTime[u] = lowestAncestor[u] = timer;
        st.push(u);
        stackMember[u] = true;
 
        for (int v : adj[u])
        {
            if (discoveryTime[v] == -1)
            {
                SCCUtil(v, adj);
                if(lowestAncestor[v] < lowestAncestor[u])
                    lowestAncestor[u] = lowestAncestor[v];
            }
            else if (stackMember[v] == true)
            {
                if(discoveryTime[v] < lowestAncestor[u])
                    lowestAncestor[u] = discoveryTime[v];
            }
        }
 
        // If Head Node, pop the stack and populate its SCC
        if (lowestAncestor[u] == discoveryTime[u])
        {
            vector<int> curScc;
            while (st.top() != u)
            {
                curScc.push_back(st.top());
                stackMember[st.top()] = false;
                st.pop();
            }
            curScc.push_back(st.top());
            stackMember[st.top()] = false;
            st.pop();
            sort(curScc.begin(), curScc.end());
            scc.push_back(curScc);
        }
    }
};
```

