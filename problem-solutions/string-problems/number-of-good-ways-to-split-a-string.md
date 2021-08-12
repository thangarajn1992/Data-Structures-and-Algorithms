# Number of Good Ways to Split a String

### Source

* [Leetcode 1525](https://leetcode.com/problems/number-of-good-ways-to-split-a-string/)

### Problem Statement

You are given a string `s`, a split is called _good_ if you can split `s` into 2 non-empty strings `p` and `q` where its concatenation is equal to `s` and the number of distinct letters in `p` and `q` are the same.

Return the number of _good_ splits you can make in `s`.

**Example 1:**

```text
Input: s = "aacaba"
Output: 2
Explanation: 
There are 5 ways to split "aacaba" and 2 of them are good. 
("a", "acaba") Left string and right string contains 1 and 3 different letters respectively.
("aa", "caba") Left string and right string contains 1 and 3 different letters respectively.
("aac", "aba") Left string and right string contains 2 and 2 different letters respectively (good split).
("aaca", "ba") Left string and right string contains 2 and 2 different letters respectively (good split).
("aacab", "a") Left string and right string contains 3 and 1 different letters respectively.
```

**Example 2:**

```text
Input: s = "abcd"
Output: 1
Explanation: Split the string as follows ("ab", "cd").
```

**Example 3:**

```text
Input: s = "aaaaa"
Output: 4
Explanation: All possible splits are good.
```

**Example 4:**

```text
Input: s = "acbadbaada"
Output: 2
```

**Constraints:**

* `s` contains only lowercase English letters.
* `1 <= s.length <= 10^5`

### Solution

```cpp
class Solution {
public:
    int numSplits(string s) {
        vector<int> unique_count(26);
        int remaining_unique = 0;
        int left_unique = 0;
        int good_splits = 0;
        
        for(char &c : s)
        {
            if(unique_count[c - 'a'] == 0)
                remaining_unique++;
            unique_count[c - 'a']++;
        }
        

        vector<bool> left_seen(26, false);
        for(char &c : s)
        {
            unique_count[c - 'a']--;
            if(unique_count[c - 'a'] == 0)
                remaining_unique--;
            if(left_seen[c - 'a'] == false)
            {
                left_seen[c - 'a'] = true;
                left_unique++;
            }
            if(left_unique == remaining_unique)
                good_splits++;
        }
        return good_splits;
    }
};
```

