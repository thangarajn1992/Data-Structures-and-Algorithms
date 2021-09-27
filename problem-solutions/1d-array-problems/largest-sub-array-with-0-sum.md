# Largest sub-array with 0 sum

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/largest-subarray-with-0-sum/1#)

### Companies

* [Amazon](../../company-based-lists/amazon.md)
* [Microsoft](../../company-based-lists/microsoft.md)

### Problem Statement

Given an array having both positive and negative integers. The task is to compute the length of the largest sub-array with sum 0.

**Example 1:**

```text
Input:
N = 8
A[] = {15,-2,2,-8,1,7,10,23}
Output: 5
Explanation: The largest subarray with
sum 0 will be -2 2 -8 1 7.
```

**Expected Time Complexity:** O\(N\).  
**Expected Auxiliary Space:** O\(N\).

**Constraints:**  
1 &lt;= N &lt;= 10^5  
-1000 &lt;= A\[i\] &lt;= 1000, for each valid i

### Solution

**Algorithm:**  

1. Create a variable \(sum\), length \(maxLen\), and a hash map \(hm\) to store the sum-index pair as a key-value pair.
2. Move along the input array from the start to the end.
3. For every index, update the value of sum = sum + array\[i\].
4. Check every index, if the current sum is present in the hash map or not.
5. If present, update the value of maxLen to a maximum difference of two indices \(current index and index in the hash-map\) and max\_len.
6. Else, put the value \(sum\) in the hash map, with the index as a key-value pair.
7. Print the maximum length \(maxLen\).

```cpp
class Solution{
    public:
    int maxLen(vector<int>&arr, int n)
    {   
        // Map to store the previous sums
        unordered_map<int, int> presum;
 
        int sum = 0; // Initialize the sum of elements
        int maxLen = 0; // Initialize result
 
        // Traverse through the given array
        for (int index = 0; index < n; index++) {
            // Add current element to sum
            sum += arr[index];
 
            if (arr[index] == 0 && maxLen == 0)
                maxLen = 1;
            if (sum == 0)
                maxLen = index + 1;
 
            // Look for this sum in Hash table
            if (presum.find(sum) != presum.end()) {
                // If this sum is seen before, then update maxLen
                maxLen = max(maxLen, index - presum[sum]);
            }
            else {
                // Else insert this sum with index in hash table
                presum[sum] = index;
            }
        }
        return maxLen;    
    }
};
```

