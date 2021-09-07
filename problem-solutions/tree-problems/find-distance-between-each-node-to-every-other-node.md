# Find Distance between each node to every other node

### Source

* [Leetcode 834](https://leetcode.com/problems/sum-of-distances-in-tree/)

### Companies

### Problem Statement

There is an undirected connected tree with `n` nodes labeled from `0` to `n - 1` and `n - 1` edges.

You are given the integer `n` and the array `edges` where `edges[i] = [ai, bi]` indicates that there is an edge between nodes `ai` and `bi` in the tree.

Return an array `answer` of length `n` where `answer[i]` is the sum of the distances between the `ith` node in the tree and all other nodes.

**Example 1:** 

![](https://assets.leetcode.com/uploads/2021/07/23/lc-sumdist1.jpg)

```text
Input: n = 6, edges = [[0,1],[0,2],[2,3],[2,4],[2,5]]
Output: [8,12,6,10,10,10]
Explanation: The tree is shown above.
We can see that dist(0,1) + dist(0,2) + dist(0,3) + dist(0,4) + dist(0,5)
equals 1 + 1 + 2 + 2 + 2 = 8.
Hence, answer[0] = 8, and so on.
```

**Example 2:** ![](https://assets.leetcode.com/uploads/2021/07/23/lc-sumdist2.jpg)

```text
Input: n = 1, edges = []
Output: [0]
```

**Example 3:** ![](https://assets.leetcode.com/uploads/2021/07/23/lc-sumdist3.jpg)

```text
Input: n = 2, edges = [[1,0]]
Output: [1,1]
```

**Constraints:**

* `1 <= n <= 3 * 10^4`
* `edges.length == n - 1`
* `edges[i].length == 2`
* `0 <= ai, bi < n`
* `ai != bi`
* The given input represents a valid tree.

### Solution

**Algorithm**

Root the tree. For each node, consider the subtreeSnodeS\_{\text{node}}Snode​ of that node plus all descendants. Let `count[node]` be the number of nodes inSnodeS\_{\text{node}}Snode​, and `stsum[node]` \("subtree sum"\) be the sum of the distances from `node` to the nodes inSnodeS\_{\text{node}}Snode​.

We can calculate `count` and `stsum` using a post-order traversal, where on exiting some `node`, the `count` and `stsum` of all descendants of this node is correct, and we now calculate `count[node] += count[child]` and `stsum[node] += stsum[child] + count[child]`.

This will give us the right answer for the `root`: `ans[root] = stsum[root]`.

Now, to use the insight explained previously: if we have a node `parent` and it's child `child`, then these are neighboring nodes, and so `ans[child] = ans[parent] - count[child] + (N - count[child])`. This is because there are `count[child]` nodes that are `1` easier to get to from `child` than `parent`, and `N-count[child]` nodes that are `1` harder to get to from `child` than `parent`. 

![Tree diagram illustrating recurrence for ans\[child\]](https://leetcode.com/problems/sum-of-distances-in-tree/Figures/834/sketch2.png)

Using a second, pre-order traversal, we can update our answer in linear time for all of our nodes.

```cpp
class Solution {
public:
    vector<int> SubTreeNodeCount;  // No.of nodes in sub-tree including this node
    vector<int> distanceToAllNodes; // Sum of distance from node to all nodes in the tree
    vector<vector<int>> graph;
    int totalNodes;
    vector<int> sumOfDistancesInTree(int n, vector<vector<int>>& edges) {
        this->totalNodes = n;
        distanceToAllNodes.resize(n, 0);
        SubTreeNodeCount.resize(n, 1);
        graph.resize(n);
        
        for (vector<int>& edge: edges) {
            graph[edge[0]].push_back(edge[1]);
            graph[edge[1]].push_back(edge[0]);
        }
        // After this DFS function, we will have sum of distance from a node to all nodes in its sub-tree
        calcSubTreeCount(0, -1);
        
        // Root's sub-tree distance sum = tree distance sum
        // Now we will need to find tree distance sum for other nodes using another DFS
        CalcTreeDistance(0, -1);
        
        return distanceToAllNodes;
    }
    
    void calcSubTreeCount(int node, int parent) {
        for (int child: graph[node])
            if (child != parent) {
                calcSubTreeCount(child, node);
                SubTreeNodeCount[node] += SubTreeNodeCount[child];
                distanceToAllNodes[node] += distanceToAllNodes[child] + SubTreeNodeCount[child];
            }
    }

    void CalcTreeDistance(int node, int parent) {
        for (int child: graph[node])
            if (child != parent) {
                /*
                There are SubTreeNodeCount[child] nodes that are 1 easier to get to from child than parent, 
                and (totalNodes -SubTreeNodeCount[child]) nodes that are 1 harder to get to from child than parent.
                */
                distanceToAllNodes[child] = (distanceToAllNodes[node] - SubTreeNodeCount[child]) + 
                                            (totalNodes - SubTreeNodeCount[child]);
                CalcTreeDistance(child, node);
            }
    }   
};
```

