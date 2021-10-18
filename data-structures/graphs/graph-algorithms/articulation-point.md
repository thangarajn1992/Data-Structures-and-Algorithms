# Tarjan's Algorithm for Articulation Point/Cut Vertices

A vertex in an un-directed connected graph is an articulation point (or cut vertex) **if removing it (and edges through it) disconnects the graph**. Articulation points represent vulnerabilities in a connected network – single points whose failure would split the network into 2 or more components. They are useful for designing reliable networks. 

For a disconnected un-directed graph, an articulation point is a vertex **removing which increases number of connected components**.

Following are some example graphs with articulation points encircled with red color. \
 

![ArticulationPoints](https://media.geeksforgeeks.org/wp-content/cdn-uploads/ArticulationPoints-300x189.png)

![ArticulationPoints1](https://media.geeksforgeeks.org/wp-content/cdn-uploads/ArticulationPoints1-129x300.png)

**How to find all articulation points in a given graph?** \
A simple approach is to one by one remove all vertices and see if removal of a vertex causes disconnected graph. Following are steps of simple approach for connected graph.\
1\) For every vertex v, do following \
…..a) Remove v from graph \
..…b) See if the graph remains connected (We can either use BFS or DFS) \
…..c) Add v back to the graph\
Time complexity of above method is` O(V*(V+E))` for a graph represented using adjacency list.

**A O(V+E) algorithm to find all Articulation Points (APs)** \
The idea is to use DFS (Depth First Search). In DFS, we follow vertices in tree form called DFS tree. In DFS tree, a vertex u is parent of another vertex v, if v is discovered by u (obviously v is an adjacent of u in graph). 

In DFS tree, a vertex u is articulation point if one of the following two conditions is true. \
**1)** **u is root of DFS tree and it has at least two children. **\
**2)** **u is not root of DFS tree and it has a child v such that no vertex in sub-tree rooted with v has a back edge to one of the ancestors (in DFS tree) of u.**

We do DFS traversal of given graph with additional code to find out Articulation Points (APs). In DFS traversal, we maintain a parent\[] array where** parent\[u] stores parent of vertex u**. Among the above mentioned two cases, the first case is simple to detect. For every vertex, count children. **If currently visited vertex u is root (parent\[u] is NIL) and has more than two children, print it. **

How to handle second case? The second case is trickier. We maintain an array disc\[] to store discovery time of vertices. **For every node u, we need to find out the earliest visited vertex (the vertex with minimum discovery time) that can be reached from sub-tree rooted with u**. So we maintain an additional array low\[] which is defined as follows.  

```
low[u] = min(disc[u], disc[w]) 
where w is an ancestor of u and there is a back edge from 
some descendant of u to w.
```

### Implementation

```cpp
// C++ program to find articulation points in an undirected graph
#include <bits/stdc++.h>
using namespace std;

// A recursive function that find articulation
// points using DFS traversal
// adj[] --> Adjacency List representation of the graph
// u --> The vertex to be visited next
// visited[] --> keeps tract of visited vertices
// disc[] --> Stores discovery times of visited vertices
// low[] -- >> earliest visited vertex (the vertex with minimum
// discovery time) that can be reached from subtree
// rooted with current vertex
// parent --> Stores the parent vertex in DFS tree
// isAP[] --> Stores articulation points
void APUtil(vector<int> adj[], int u, bool visited[],
			int disc[], int low[], int& time, int parent,
			bool isAP[])
{
	// Count of children in DFS Tree
	int children = 0;

	// Mark the current node as visited
	visited[u] = true;

	// Initialize discovery time and low value
	disc[u] = low[u] = ++time;

	// Go through all vertices aadjacent to this
	for (auto v : adj[u]) {
		// If v is not visited yet, then make it a child of u
		// in DFS tree and recur for it
		if (!visited[v]) {
			children++;
			APUtil(adj, v, visited, disc, low, time, u, isAP);

			// Check if the subtree rooted with v has
			// a connection to one of the ancestors of u
			low[u] = min(low[u], low[v]);

			// If u is not root and low value of one of
			// its child is more than discovery value of u.
			if (parent != -1 && low[v] >= disc[u])
				isAP[u] = true;
		}

		// Update low value of u for parent function calls.
		else if (v != parent) // undirected graph, so updated only for non-parent
			low[u] = min(low[u], disc[v]);
	}

	// If u is root of DFS tree and has two or more chilren.
	if (parent == -1 && children > 1)
		isAP[u] = true;
}

void AP(vector<int> adj[], int V)
{
	int disc[V] = { 0 };
	int low[V];
	bool visited[V] = { false };
	bool isAP[V] = { false };
	int time = 0, par = -1;

	// Loop to handle disconnected graph
	for (int u = 0; u < V; u++)
	{
		if (!visited[u])
		{
			APUtil(adj, u, visited, disc, low, time, par, isAP);
		}
	}
	
	// Printing the APs
	for (int u = 0; u < V; u++)
		if (isAP[u] == true)
			cout << u << " ";
}

// Utility function to add an edge
void addEdge(vector<int> adj[], int u, int v)
{
	adj[u].push_back(v);
	adj[v].push_back(u);
}

int main()
{
	// Create graphs given in above diagrams
	cout << "Articulation points in first graph \n";
	int V = 5;
	vector<int> adj1[V];
	addEdge(adj1, 1, 0);
	addEdge(adj1, 0, 2);
	addEdge(adj1, 2, 1);
	addEdge(adj1, 0, 3);
	addEdge(adj1, 3, 4);
	AP(adj1, V);

	cout << "\nArticulation points in second graph \n";
	V = 4;
	vector<int> adj2[V];
	addEdge(adj2, 0, 1);
	addEdge(adj2, 1, 2);
	addEdge(adj2, 2, 3);
	AP(adj2, V);

	cout << "\nArticulation points in third graph \n";
	V = 7;
	vector<int> adj3[V];
	addEdge(adj3, 0, 1);
	addEdge(adj3, 1, 2);
	addEdge(adj3, 2, 0);
	addEdge(adj3, 1, 3);
	addEdge(adj3, 1, 4);
	addEdge(adj3, 1, 6);
	addEdge(adj3, 3, 5);
	addEdge(adj3, 4, 5);
	AP(adj3, V);

	return 0;
}

```
