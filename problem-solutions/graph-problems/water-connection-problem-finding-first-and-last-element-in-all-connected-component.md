# Water Connection Problem - Finding First and Last element in all Connected Component

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/water-connection-problem5822/1#)

### Companies

### Problem Statement

Every house in the colony has at most one pipe going into it and at most one pipe going out of it. Tanks and taps are to be installed in a manner such that every house with one outgoing pipe but no incoming pipe gets a tank installed on its roof and every house with only an incoming pipe and no outgoing pipe gets a tap.

Given two integers **n** and **p** denoting the number of houses and the number of pipes. The connections of pipe among the houses contain three input values: **ai**, **bi**, **di** denoting the pipe of diameter **di** from house **ai** to house **bi.** Find the efficient way for the construction of the network of pipes.

The output will contain the number of pairs of tanks and taps **t** installed in first line and the next **t** lines contain three integers: house number of tank, house number of tap and the minimum diameter of pipe between them.

\
&#x20;**Example 1:**

```
Input:
n = 9, p = 6
a[] = {7,5,4,2,9,3}
b[] = {4,9,6,8,7,1}
d[] = {98,72,10,22,17,66} 
Output: 
3
2 8 22
3 1 66
5 6 10
Explanation:
Connected components are 
3->1, 5->9->7->4->6 and 2->8.
Therefore, our answer is 3 
followed by 2 8 22, 3 1 66, 5 6 10.
```

**Your Task:**\
&#x20;You don't need to read input or print anything. Your task is to complete the function **solve()** which takes an integer n(the number of houses), p(the number of pipes),the array a\[] , b\[] and d\[] (where **d\[i]** denoting the diameter of the ith pipe from the house **a\[i]** to house **b\[i]**) as input parameter and returns the array of pairs of tanks and taps installed i.e ith element of the array contains three integers: house number of tank, house number of tap and the minimum diameter of pipe between them. &#x20;

**Expected Time Complexity:** O(n+p)\
&#x20;**Expected Auxiliary Space:** O(n+p)

**Constraints:**\
&#x20;1<=n<=20\
&#x20;1<=p<=50\
&#x20;1<=a\[i],b\[i]<=20\
&#x20;1<=d\[i]<=100

### Solution

```cpp
class Solution
{
    public:
    vector<vector<int>> solve(int n,int p,vector<int> a,vector<int> b,vector<int> d)
    {
        vector<vector<int>> result;
        vector<vector<pair<int,int>>> adj(n+1);
        vector<int> inDegree(n+1);
        for(int pipeNum = 0; pipeNum < p; pipeNum++)
        {
            inDegree[b[pipeNum]]++;
            adj[a[pipeNum]].push_back({b[pipeNum], d[pipeNum]});
        }
        for(int houseNum = 1; houseNum <= n; houseNum++)
        {
            if(inDegree[houseNum] == 0 && adj[houseNum].size() > 0)
            {
                int minDiameter = INT_MAX;
                int currHouse = houseNum;
                while(adj[currHouse].size() > 0)
                {
                    minDiameter = min(minDiameter, adj[currHouse][0].second);
                    currHouse = adj[currHouse][0].first;
                }
                result.push_back({houseNum, currHouse, minDiameter});
            }
        }
        return result;
    }
};
```
