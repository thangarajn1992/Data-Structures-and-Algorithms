# Longest Palindromic Substring

### Source

* [Leetcode 5](https://leetcode.com/problems/longest-palindromic-substring/)
* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/longest-palindrome-in-a-string1956/1#)

### Companies

* [Amazon](../../company-based-lists/amazon.md)
* [Microsoft](../../company-based-lists/microsoft.md)
* [Samsung](../../company-based-lists/samsung.md)
* [Walmart](../../company-based-lists/walmart.md)

### Problem Statement

Given a string `s`, return _the longest palindromic substring_ in `s`.

**Example 1:**

```text
Input: s = "babad"
Output: "bab"
Note: "aba" is also a valid answer.
```

**Example 2:**

```text
Input: s = "cbbd"
Output: "bb"
```

**Example 3:**

```text
Input: s = "a"
Output: "a"
```

**Example 4:**

```text
Input: s = "ac"
Output: "a"
```

**Constraints:**

* `1 <= s.length <= 1000`
* `s` consist of only digits and English letters.

### Solution

```cpp
class Solution {
public:
    int maxPalindromeStart = -1, maxPalindromeLen = 0;
    string longestPalindrome(string s){
        for(int i = 0; i < s.size(); i++)
        {
            expandAroundCenter(s, i, i);
            if(i < s.size() - 1 && s[i] == s[i+1])
                expandAroundCenter(s, i, i+1);
        }
        return s.substr(maxPalindromeStart, maxPalindromeLen);    
    }
    
    void expandAroundCenter(const string &s, int left, int right)
    {
        while(left >= 0 && right < s.size() && s[left] == s[right])
            left--, right++;
            
        if(maxPalindromeLen < right - left - 1)
        {
            maxPalindromeLen = right - left -1;
            maxPalindromeStart = left+1;
        }
    }
};
```

