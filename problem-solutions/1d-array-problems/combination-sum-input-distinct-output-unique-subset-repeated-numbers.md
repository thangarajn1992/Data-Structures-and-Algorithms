# Combination Sum - Input distinct Output Unique Subset Repeated Numbers

### Sources

* [Leetcode 39](https://leetcode.com/problems/combination-sum/)

### Companies

### Problem Statement

Given an array of **distinct** integers `candidates` and a target integer `target`, return _a list of all **unique combinations** of_ `candidates` _where the chosen numbers sum to_ `target`_._ You may return the combinations in **any order**.

The **same** number may be chosen from `candidates` an **unlimited number of times**. Two combinations are unique if the frequency of at least one of the chosen numbers is different.

It is **guaranteed** that the number of unique combinations that sum up to `target` is less than `150` combinations for the given input.

**Example 1:**

```text
Input: candidates = [2,3,6,7], target = 7
Output: [[2,2,3],[7]]
Explanation:
2 and 3 are candidates, and 2 + 2 + 3 = 7. Note that 2 can be used multiple times.
7 is a candidate, and 7 = 7.
These are the only two combinations.
```

**Example 2:**

```text
Input: candidates = [2,3,5], target = 8
Output: [[2,2,2,2],[2,3,3],[3,5]]
```

**Example 3:**

```text
Input: candidates = [2], target = 1
Output: []
```

**Example 4:**

```text
Input: candidates = [1], target = 1
Output: [[1]]
```

**Example 5:**

```text
Input: candidates = [1], target = 2
Output: [[1,1]]
```

**Constraints:**

* `1 <= candidates.length <= 30`
* `1 <= candidates[i] <= 200`
* All elements of `candidates` are **distinct**.
* `1 <= target <= 500`

### Solution

#### Backtracking

```cpp
class Solution {
private:
    vector<vector<int>> combos;
    vector<int> curr_combo;
public:
    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
        helper(candidates, target, 0, 0);
        return combos;
    }
    
    void helper(vector<int>& candidates, int target, int sum, int idx){
        if(sum > target){
            return;
        }
        if(sum == target){
            combos.push_back(curr_combo);
            return;
        }
        for(int i = idx; i < candidates.size(); i++){
                curr_combo.push_back(candidates[i]);
                helper(candidates, target, sum+candidates[i], i);
                curr_combo.pop_back();
        }     
    }
};
```

