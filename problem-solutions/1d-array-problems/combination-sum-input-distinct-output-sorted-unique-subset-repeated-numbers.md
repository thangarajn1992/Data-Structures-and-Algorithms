# Combination Sum - Input distinct Output Sorted Unique Subset Repeated Numbers

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/combination-sum-1587115620/1#)

### Companies

* [Amazon](../../company-based-lists/amazon.md)
* [Adobe](../../company-based-lists/adobe.md)
* [Microsoft](../../company-based-lists/microsoft.md)

### Problem Statement

Given an array of integers and a sum B, find all unique combinations in the array where the sum is equal to B. The same number may be chosen from the array any number of times to make B.

**Note:**  
         **1.** All numbers will be positive integers.  
         **2.** Elements in a combination \(a1, a2, …, ak\) must be in non-descending order. \(ie, a1 ≤ a2 ≤ … ≤ ak\).  
         **3.** The combinations themselves must be sorted in ascending order.

  
 **Example 1:**

```text
Input:
N = 4
arr[] = {7,2,6,5}
B = 16
Output:
(2 2 2 2 2 2 2 2)
(2 2 2 2 2 6)
(2 2 2 5 5)
(2 2 5 7)
(2 2 6 6)
(2 7 7)
(5 5 6)
```

**Example 2:**

```text
Input:
N = 11
arr[] = {6,5,7,1,8,2,9,9,7,7,9}
B = 6
Output:
(1 1 1 1 1 1)
(1 1 1 1 2)
(1 1 2 2)
(1 5)
(2 2 2)
(6)
```

**Expected Time Complexity:** O\(X2 \* 2N\), where X is average of summation B/arri for every number in the array.  
 **Expected Auxiliary Space:** O\(X \* 2N\)

  
 **Constraints:**  
 1 &lt;= N &lt;= 30  
 1 &lt;= A\[i\] &lt;= 20  
 1 &lt;= B &lt;= 100

### Solution

#### Backtracking

```cpp
class Solution {
  public:
    vector<vector<int>> combos;
    vector<int> curr_combo;
    vector<vector<int> > combinationSum(vector<int> &candidates, int target) {
        sort(candidates.begin(), candidates.end());
        candidates.erase(unique(candidates.begin(), candidates.end()), candidates.end());
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

