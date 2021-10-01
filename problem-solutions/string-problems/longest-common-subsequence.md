# Longest Common Subsequence

### Sources

* [Leetcode 1143](https://leetcode.com/problems/longest-common-subsequence/)

### Companies

### Problem Statement

Given two strings `text1` and `text2`, return _the length of their longest **common subsequence**._ If there is no **common subsequence**, return `0`.

A **subsequence** of a string is a new string generated from the original string with some characters \(can be none\) deleted without changing the relative order of the remaining characters.

* For example, `"ace"` is a subsequence of `"abcde"`.

A **common subsequence** of two strings is a subsequence that is common to both strings.

**Example 1:**

```text
Input: text1 = "abcde", text2 = "ace" 
Output: 3  
Explanation: The longest common subsequence is "ace" and its length is 3.
```

**Example 2:**

```text
Input: text1 = "abc", text2 = "abc"
Output: 3
Explanation: The longest common subsequence is "abc" and its length is 3.
```

**Example 3:**

```text
Input: text1 = "abc", text2 = "def"
Output: 0
Explanation: There is no such common subsequence, so the result is 0.
```

**Constraints:**

* `1 <= text1.length, text2.length <= 1000`
* `text1` and `text2` consist of only lowercase English characters.

### Solution

```cpp
class Solution {
public:
    int longestCommonSubsequence(string text1, string text2) {
        vector<short> m(text2.size() + 1);
        for (auto i = 1; i <= text1.size(); ++i)
        {
            int previousValue = 0;
            for (auto j = 1; j <= text2.size(); ++j)
            {
                int currentValue = m[j]; // this stores value of m[j-1] to be used for next j
                if (text1[i - 1] == text2[j - 1]) 
                {
                    m[j] = previousValue + 1;
                }
                else 
                {
                    m[j] = max(m[j], m[j - 1]);
                }
                previousValue = currentValue;
            }
        }
        return m[text2.size()];        
    }
};
```

