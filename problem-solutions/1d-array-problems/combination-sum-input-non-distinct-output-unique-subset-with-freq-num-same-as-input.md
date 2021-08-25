# Combination Sum - Input non-distinct Output Unique subset with freq num same as input

### Sources

* [Leetcode 40](https://leetcode.com/problems/combination-sum-ii/)

### Companies

### Problem Statement

Given a collection of candidate numbers \(`candidates`\) and a target number \(`target`\), find all unique combinations in `candidates` where the candidate numbers sum to `target`.

Each number in `candidates` may only be used **once** in the combination.

**Note:** The solution set must not contain duplicate combinations.

**Example 1:**

```text
Input: candidates = [10,1,2,7,6,1,5], target = 8
Output: 
[
[1,1,6],
[1,2,5],
[1,7],
[2,6]
]
```

**Example 2:**

```text
Input: candidates = [2,5,2,1,2], target = 5
Output: 
[
[1,2,2],
[5]
]
```

**Constraints:**

* `1 <= candidates.length <= 100`
* `1 <= candidates[i] <= 50`
* `1 <= target <= 30`

### Solution

```cpp
class Solution {
private:
    vector<vector<int>> combos;
    vector<int> currCombo;
public:
    vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
        sort(candidates.begin(), candidates.end());
        helper(candidates, target, 0, 0);
        return combos;
    }
    
    void helper(vector<int>& candidates, int target, int sum, int index)
    {   
        if(sum == target)
        {
            combos.push_back(currCombo);
            return;
        }
        
        for(int nextIndex = index; nextIndex < candidates.size() ; nextIndex++)
        {
            if(nextIndex > index && candidates[nextIndex] == candidates[nextIndex-1])
                continue;
            
            if(sum + candidates[nextIndex] > target)
                break;
            currCombo.push_back(candidates[nextIndex]);
            helper(candidates, target, sum + candidates[nextIndex], nextIndex+1);            
            currCombo.pop_back();
        }
    }
};
```

