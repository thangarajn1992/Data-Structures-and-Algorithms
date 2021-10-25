# Managing dependent modules with given duration and parallelism possible

### Sources

* [GeeksForGeeks](https://practice.geeksforgeeks.org/problems/6b216f3d1f1ce9a14258b982d44f5e5199e7759a/1#)

### Companies

### Problem Statement

An IT company is working on a large project. The project is broken into **N** modules and distributed to different teams. Each team can work parallel. The amount of time (in months) required to complete each module is given in an array **duration\[ ]** _i.e._ time needed to complete** ith **module is **duration\[i]** months. \
You are also given **M** **dependencies** such that for each i (1 ≤ i ≤ M)  **dependencies\[i]\[1]th **module can be started after **dependencies\[i]\[0]th **module is completed.\
As the project manager, compute the minimum time required to complete the project.\
**Note**: It is guaranteed that a module is not dependent on itself.

**Example 1:**

****

```
Input
N = 6, M = 6
duration[] = {1, 2, 3, 1, 3, 2}
dependencies[][]:
[[5, 2]
 [5, 0]
 [4, 0] 
 [4, 1]
 [2, 3]
 [3, 1]]
Output: 
8


The Graph of dependency forms this and 
the project will be completed when Module 
1 is completed which takes 8 months.
```

****![](<../../.gitbook/assets/image (56).png>)****

**Example 2:**

```
Input:
N = 3, M = 3
duration[] = {5, 5, 5}
dependencies[][]:
[[0, 1]
 [1, 2]
 [2, 0]]
Output: 
-1
Explanation: 
There is a cycle in the dependency graph 
hence the project cannot be completed.
```

**Your Task:**\
Complete the function **minTime()** which takes **N**, **M**, **duration** **array**, and **dependencies** **array** as input parameter and return the minimum time required. return -1 if the project can not be completed.&#x20;

**Expected Time Complexity:** O(N+M)\
**Expected Auxiliary Space:** O(N)

**Constraints:**\
1 ≤ N ≤ 10^5\
0 ≤ M ≤ 2\*10^5\
1 ≤ duration\[i] ≤ 10**^**5\
0 ≤ dependencies\[i]\[j] < N

### Solution

```cpp
class Solution{
    public:
    int minTime(vector<pair<int, int>> &dependency, int duration[], int n, int m) {
        vector<int> outDegree(n, 0);
        vector<vector<int>> dependedBy(n);
        
        for(pair<int,int> dependence : dependency)
        {
            dependedBy[dependence.first].push_back(dependence.second);
            outDegree[dependence.second]++;
        }
        
        // walk through all nodes and process nodes with indegree of 0
        int modulesProcessed = 0;
        vector<int> timeTaken(n,0);
        
        queue<int> q;
        
        for(int i = 0; i < n; i++)
        {
            if(outDegree[i] == 0)
            {
                q.push(i);
                timeTaken[i] = duration[i];
                modulesProcessed++;
            }
        }
        while(q.empty() == false)
        {
            for(int index = q.size() - 1; index >= 0; index--)
            {
                int i = q.front(); q.pop();
                // reduce outdegree for all its depenedents
                for(int depend : dependedBy[i])
                {
                    outDegree[depend]--;
                    timeTaken[depend] = max(timeTaken[depend], duration[depend] + timeTaken[i]);
                    
                    if(outDegree[depend] == 0)
                    {
                        // this module can be processed
                        modulesProcessed++;
                        q.push(depend);
                    }
                }
            }
        }
        if(modulesProcessed == n)
            return *max_element(timeTaken.begin(), timeTaken.end());
        return -1;
    }
};
```
