# Number of Ways to Arrive at Destination

### Sources

* [Leetcode 1976](https://leetcode.com/problems/number-of-ways-to-arrive-at-destination/)

### Companies

### Problem Statement

You are in a city that consists of `n` intersections numbered from `0` to `n - 1` with **bi-directional** roads between some intersections. The inputs are generated such that you can reach any intersection from any other intersection and that there is at most one road between any two intersections.

You are given an integer `n` and a 2D integer array `roads` where `roads[i] = [ui, vi, timei]` means that there is a road between intersections `ui` and `vi` that takes `timei` minutes to travel. You want to know in how many ways you can travel from intersection `0` to intersection `n - 1` in the **shortest amount of time**.

Return _the **number of ways** you can arrive at your destination in the **shortest amount of time**_. Since the answer may be large, return it **modulo** `109 + 7`.

**Example 1:** ![](https://assets.leetcode.com/uploads/2021/07/17/graph2.png)

```text
Input: n = 7, roads = [[0,6,7],[0,1,2],[1,2,3],[1,3,3],[6,3,3],[3,5,1],[6,5,1],[2,5,1],[0,4,5],[4,6,2]]
Output: 4
Explanation: The shortest amount of time it takes to go from intersection 0 to intersection 6 is 7 minutes.
The four ways to get there in 7 minutes are:
- 0 ➝ 6
- 0 ➝ 4 ➝ 6
- 0 ➝ 1 ➝ 2 ➝ 5 ➝ 6
- 0 ➝ 1 ➝ 3 ➝ 5 ➝ 6
```

**Example 2:**

```text
Input: n = 2, roads = [[1,0,10]]
Output: 1
Explanation: There is only one way to go from intersection 0 to intersection 1, and it takes 10 minutes.
```

**Constraints:**

* `1 <= n <= 200`
* `n - 1 <= roads.length <= n * (n - 1) / 2`
* `roads[i].length == 3`
* `0 <= ui, vi <= n - 1`
* `1 <= timei <= 10^9`
* `ui != vi`
* There is at most one road connecting any two intersections.
* You can reach any intersection from any other intersection.

### Solution

#### Dijkstra's Shortest Path Approach

```cpp
class Solution {
public:
    int countPaths(int n, vector<vector<int>>& grid) {
        vector<vector<pair <int, long long>>> graph(n);
        for(vector<int>& x: grid) { 
            //creating adjacency list
            graph[x[0]].push_back({x[1], x[2]});
            graph[x[1]].push_back({x[0], x[2]});
        }
        long long INF = 1e15;
        long long MOD = 1e9 + 7;
        vector <long long> min_paths(n, 0);
        vector <long long> dist(n, INF);
        priority_queue <pair <long long, int>> q;
        dist[0] = 0;
        min_paths[0] = 1; // initilize it to 1 since to reach 0 we have 1 way
        q.push({0, 0});
        while(q.size()) {
            int node = q.top().second;
            long long nodeWt = -q.top().first;
            q.pop();
            
            // If we have already found lesser dist for this node, dont need to 
            // process this queue element
            if(dist[node] < nodeWt) 
                continue;
            
            for(pair<int,long long>&key: graph[node]) {
                int child = key.first;
                long long childWt = key.second;
                
                // this is extra part other than classical Dijkstra
                // we are adding parent's dp value to child's dp
                // when weights to reach this child is same
                if(nodeWt + childWt == dist[child]) { 
                    min_paths[child] = (min_paths[child] + min_paths[node]) % MOD;
                }
                if(nodeWt + childWt < dist[child]) {
                    // we are getting value of parent's min_paths
                    min_paths[child] = min_paths[node] % MOD; 
                    dist[child] = nodeWt + childWt;
                    q.push({-dist[child], child});
                }
            }
        }
        return min_paths[n-1];
    }
};
```

