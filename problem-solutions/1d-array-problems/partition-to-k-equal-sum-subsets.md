# Partition to K Equal Sum Subsets

### Sources

* [Leetcode 698](https://leetcode.com/problems/partition-to-k-equal-sum-subsets/)

### Companies

### Problem Statement

Given an integer array `nums` and an integer `k`, return `true` if it is possible to divide this array into `k` non-empty subsets whose sums are all equal.

**Example 1:**

```text
Input: nums = [4,3,2,3,5,2,1], k = 4
Output: true
Explanation: 
It's possible to divide it into 4 subsets (5), (1, 4), (2,3), (2,3) with equal sums.
```

**Example 2:**

```text
Input: nums = [1,2,3,4], k = 3
Output: false
```

**Constraints:**

* `1 <= k <= nums.length <= 16`
* `1 <= nums[i] <= 10^4`
* The frequency of each element is in the range `[1, 4]`.

### Solution

#### Dynamic Programming + Memoization + Recursion

```cpp
class Solution {
public:
    int size, k, target;
    int dp[(1 << 16) + 1];
 
    bool canPartitionKSubsets(vector<int>& nums, int k) {
        int sum = 0;
        for(int &num : nums)
            sum += num;
        if(sum % k != 0)
            return false;
        
        this->target = sum/k;
        this->size = nums.size();
        this->k = k;
        
        sort(nums.begin(),nums.end());
        memset(dp, -1, sizeof(dp));
        return recursion(0, 0, 0, nums);
    }
    
    int recursion(int thisPartitionSum, int partitionNum, int mask, vector<int>&nums){
        if(partitionNum == k-1){
            return 1;
        }
        if(dp[mask] != -1)
            return dp[mask];
        
        int ans = 0;
        for(int index = 0; index < size; index++){
             // Number already selected
            if(mask & (1 << index))
                continue;
            
            // Selecting this number takes this partition to exceed target
            if(thisPartitionSum + nums[index] > target) 
                break;
            
            // This number Completes this partition, create new partition
            if(thisPartitionSum + nums[index] == target){
               mask ^= (1 << index);
               ans = max(ans, recursion(0, partitionNum+1, mask, nums)); 
               mask ^= (1 << index);
            }
            else{
               mask ^= (1 << index); 
               ans = max(ans, recursion(thisPartitionSum + nums[index], partitionNum, mask, nums)); 
               mask ^= (1 << index); 
            }
            if(ans == 1)
                break;
        }
        return dp[mask] = ans;
    }
};
```

