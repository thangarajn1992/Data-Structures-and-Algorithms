# Flip String to Monotone Increasing

### Source

* [Leetcode 926](https://leetcode.com/problems/flip-string-to-monotone-increasing/)

### Problem Statement

A binary string is monotone increasing if it consists of some number of `0`'s \(possibly none\), followed by some number of `1`'s \(also possibly none\).

You are given a binary string `s`. You can flip `s[i]` changing it from `0` to `1` or from `1` to `0`.

Return _the minimum number of flips to make_ `s` _monotone increasing_.

**Example 1:**

```text
Input: s = "00110"
Output: 1
Explanation: We flip the last digit to get 00111.
```

**Example 2:**

```text
Input: s = "010110"
Output: 2
Explanation: We flip to get 011111, or alternatively 000111.
```

**Example 3:**

```text
Input: s = "00011000"
Output: 2
Explanation: We flip to get 00000000.
```

**Constraints:**

* `1 <= s.length <= 10^5`
* `s[i]` is either `'0'` or `'1'`.

### Solution

```cpp
class Solution {
public:
    int minFlipsMonoIncr(string s) {
        int remaining_zeros = 0;
        for(auto ch : s)
            if(ch == '0')
                remaining_zeros++;
        
        int ones_so_far = 0;
        
        // Resultant string has 2 parts: 
        // First half with O to N zeroes + Second half with N to 0 ones
        // We need to figure out the index that splits them with min flips
        
        // If that index is -1 i.e resultant string is all 1s, then flips = total_zeros;
        int flips = remaining_zeros;
        for(auto ch : s)
        {
            if(ch == '0')
                remaining_zeros--;
            else
                ones_so_far++;
            
            // For each index, calculate
            //  flips  = converting previous 1s to 0s + following 0s to 1s
            flips = min(flips, ones_so_far + remaining_zeros);
        }
        return flips;    
    }
};
```

