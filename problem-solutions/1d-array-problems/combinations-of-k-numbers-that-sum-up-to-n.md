# Combinations of k numbers that sum up to n

### Sources

* [Leetcode 216](https://leetcode.com/problems/combination-sum-iii/)

### Companies

### Problem Statement

Find all valid combinations of `k` numbers that sum up to `n` such that the following conditions are true:

* Only numbers `1` through `9` are used.
* Each number is used **at most once**.

Return _a list of all possible valid combinations_. The list must not contain the same combination twice, and the combinations may be returned in any order.

**Example 1:**

```text
Input: k = 3, n = 7
Output: [[1,2,4]]
Explanation:
1 + 2 + 4 = 7
There are no other valid combinations.
```

**Example 2:**

```text
Input: k = 3, n = 9
Output: [[1,2,6],[1,3,5],[2,3,4]]
Explanation:
1 + 2 + 6 = 9
1 + 3 + 5 = 9
2 + 3 + 4 = 9
There are no other valid combinations.
```

**Example 3:**

```text
Input: k = 4, n = 1
Output: []
Explanation: There are no valid combinations.
Using 4 different numbers in the range [1,9], the smallest sum we can get is 1+2+3+4 = 10 and since 10 > 1, there are no valid combination.
```

**Example 4:**

```text
Input: k = 3, n = 2
Output: []
Explanation: There are no valid combinations.
```

**Example 5:**

```text
Input: k = 9, n = 45
Output: [[1,2,3,4,5,6,7,8,9]]
Explanation:
1 + 2 + 3 + 4 + 5 + 6 + 7 + 8 + 9 = 45
There are no other valid combinations.
```

**Constraints:**

* `2 <= k <= 9`
* `1 <= n <= 60`

### Solution

```cpp
class Solution {
public:
    vector<vector<int>> combos;
    vector<int> currCombo;
    vector<vector<int>> combinationSum3(int k, int n) {
        helper(1, 0, n, k);
        return combos;
    }
    void helper(int index, int sum, int target, int comboSize)
    {
        if(index > 10 || sum > target || currCombo.size() > comboSize)
            return;
        
        if(currCombo.size() == comboSize)
        {
            if(sum == target)
                combos.push_back(currCombo);
            return;
        }
        helper(index+1, sum, target, comboSize);
        
        currCombo.push_back(index);
        helper(index+1, sum + index, target, comboSize);
        currCombo.pop_back();
    }
};
```

