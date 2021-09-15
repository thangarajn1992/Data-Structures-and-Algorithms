# Longest Turbulent Sub-array

### Sources

* [Leetcode 978](https://leetcode.com/problems/longest-turbulent-subarray/)

### Companies

### Problem Statement

Given an integer array `arr`, return _the length of a maximum size turbulent subarray of_ `arr`.

A subarray is **turbulent** if the comparison sign flips between each adjacent pair of elements in the subarray.

More formally, a subarray `[arr[i], arr[i + 1], ..., arr[j]]` of `arr` is said to be turbulent if and only if:

* For `i <= k < j`:
  * `arr[k] > arr[k + 1]` when `k` is odd, and
  * `arr[k] < arr[k + 1]` when `k` is even.
* Or, for `i <= k < j`:
  * `arr[k] > arr[k + 1]` when `k` is even, and
  * `arr[k] < arr[k + 1]` when `k` is odd.

**Example 1:**

```text
Input: arr = [9,4,2,10,7,8,8,1,9]
Output: 5
Explanation: arr[1] > arr[2] < arr[3] > arr[4] < arr[5]
```

**Example 2:**

```text
Input: arr = [4,8,12,16]
Output: 2
```

**Example 3:**

```text
Input: arr = [100]
Output: 1
```

**Constraints:**

* `1 <= arr.length <= 4 * 10^4`
* `0 <= arr[i] <= 10^9`

### Algorithm

We only care about the comparisons between adjacent elements. If the comparisons are represented by `-1, 0, 1` \(for `<, =, >`\), then we want the longest sequence of alternating `1, -1, 1, -1, ...` \(starting with either `1` or `-1`\).

These alternating comparisons form contiguous blocks. We know when the next block ends: when it is the last two elements being compared, or when the sequence isn't alternating.

For example, take an array like `A = [9,4,2,10,7,8,8,1,9]`. The comparisons are `[1,1,-1,1,-1,0,-1,1]`. The blocks are `[1], [1,-1,1,-1], [0], [-1,1]`.

Scan the array from left to right. If we are at the end of a block \(last elements OR it stopped alternating\), then we should record the length of that block as our candidate answer, and set the start of the new block as the next element.

### Solution

```cpp
class Solution {
public:
    int maxTurbulenceSize(vector<int>& arr) {
        int size = arr.size();
        int answer = 1;
        int anchor = 0;
        
        for(int index = 1; index < size; index++)
        {
            int c = compare(arr[index-1] , arr[index]);
            
            if(c == 0)
            {
                anchor = index;
            }
            else if(index == size-1 || c * compare(arr[index] , arr[index+1]) != -1)
            {
                answer = max(answer, index - anchor +1);
                anchor = index;
            }
        }
        return answer;
    }
    int compare(const int a, const int b)
    {
        if(a < b)
            return 1;
        else if(a > b)
            return -1;
        return 0;
    }
};
```

