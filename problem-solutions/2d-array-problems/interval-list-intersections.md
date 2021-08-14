# Interval List Intersections

### Source

* [Leetcode 986](https://leetcode.com/problems/interval-list-intersections/)

### Problem Statement

You are given two lists of closed intervals, `firstList` and `secondList`, where `firstList[i] = [starti, endi]` and `secondList[j] = [startj, endj]`. Each list of intervals is pairwise **disjoint** and in **sorted order**.

Return _the intersection of these two interval lists_.

A **closed interval** `[a, b]` \(with `a < b`\) denotes the set of real numbers `x` with `a <= x <= b`.

The **intersection** of two closed intervals is a set of real numbers that are either empty or represented as a closed interval. For example, the intersection of `[1, 3]` and `[2, 4]` is `[2, 3]`.

**Example 1:** 

![](https://assets.leetcode.com/uploads/2019/01/30/interval1.png)

```text
Input: firstList = [[0,2],[5,10],[13,23],[24,25]], 
       secondList = [[1,5],[8,12],[15,24],[25,26]]
Output: [[1,2],[5,5],[8,10],[15,23],[24,24],[25,25]]
```

**Example 2:**

```text
Input: firstList = [[1,3],[5,9]], secondList = []
Output: []
```

**Example 3:**

```text
Input: firstList = [], secondList = [[4,8],[10,12]]
Output: []
```

**Example 4:**

```text
Input: firstList = [[1,7]], secondList = [[3,10]]
Output: [[3,7]]
```

**Constraints:**

* `0 <= firstList.length, secondList.length <= 1000`
* `firstList.length + secondList.length >= 1`
* `0 <= starti < endi <= 10^9`
* `endi < starti+1`
* `0 <= startj < endj <= 10^9`
* `endj < startj+1`

### Solution

```cpp
class Solution {
public:
    vector<vector<int>> intervalIntersection(vector<vector<int>>& firstList, 
                                             vector<vector<int>>& secondList) {
        int firstindex = 0, secondindex = 0;
        vector<vector<int>> intersection;

        while(firstindex < firstList.size() && secondindex < secondList.size())
        {
                int start = max(firstList[firstindex][0] , secondList[secondindex][0]);
                int end = min(firstList[firstindex][1], secondList[secondindex][1]);
                
                // If intersection is present, add to our list
                if(start <= end)
                    intersection.push_back({start, end});
                
                // Remove the interval with smallest endpoint
                if(firstList[firstindex][1] < secondList[secondindex][1])
                    firstindex++;
                else
                    secondindex++;
        }
        return intersection;
    }
};
```

```cpp
Testcases

Input:
[[0,2],[5,10],[13,23],[24,25]]
[[1,5],[8,12],[15,24],[25,26]]

[[1,3],[5,9]]
[]

[]
[[4,8],[10,12]]

[[1,7]]
[[3,10]]

[[8,15]]
[[2,6],[8,10],[12,20]]

[[3,5],[9,20]]
[[4,5],[7,10],[11,12],[14,15],[16,20]]

Output:
[[1,2],[5,5],[8,10],[15,23],[24,24],[25,25]]
[]
[]
[[3,7]]
[[8,10],[12,15]]
[[4,5],[9,10],[11,12],[14,15],[16,20]]
```

