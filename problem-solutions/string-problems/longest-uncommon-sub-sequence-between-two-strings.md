# Longest Uncommon Sub-sequence between two strings

### Sources

* [Leetcode 521](https://leetcode.com/problems/longest-uncommon-subsequence-i/)

### Companies

### Problem Statement

Given two strings `a` and `b`, return _the length of the **longest uncommon subsequence** between_ `a` _and_ `b`. If the longest uncommon subsequence does not exist, return `-1`.

An **uncommon subsequence** between two strings is a string that is a **subsequence of one but not the other**.

A **subsequence** of a string `s` is a string that can be obtained after deleting any number of characters from `s`.

* For example, `"abc"` is a subsequence of `"aebdc"` because you can delete the underlined characters in `"aebdc"` to get `"abc"`. Other subsequences of `"aebdc"` include `"aebdc"`, `"aeb"`, and `""` (empty string).

**Example 1:**

```
Input: a = "aba", b = "cdc"
Output: 3
Explanation: 
One longest uncommon subsequence is "aba" because "aba" is a subsequence of "aba"
but not "cdc".
Note that "cdc" is also a longest uncommon subsequence.
```

**Example 2:**

```
Input: a = "aaa", b = "bbb"
Output: 3
Explanation: 
The longest uncommon subsequences are "aaa" and "bbb".
```

**Example 3:**

```
Input: a = "aaa", b = "aaa"
Output: -1
Explanation: 
Every subsequence of string a is also a subsequence of string b. 
Similarly, every subsequence of string b is also a subsequence of string a.
```

**Constraints:**

* `1 <= a.length, b.length <= 100`
* `a` and `b` consist of lower-case English letters.

### Solution

Simple analysis of this problem can lead to an easy solution.

These three cases are possible with string `a` and` b`:-

* `a == b.` If both the strings are identical, it is obvious that no sub-sequence will be uncommon. Hence, return -1.
* `length(a) == length(b)` and `a≠b`. Example: `abc` and `abd`. In this case we can consider any string i.e. `abc` or `abd` as a required sub-sequence, as out of these two strings one string will never be a sub-sequence of other string. Hence, return `length(a)` or` length(b)`
* `length(a) ≠ length(b)`. Example `abcd` and `abc`. In this case we can consider bigger string as a required sub-sequence because bigger string can't be a sub-sequence of smaller string. Hence, return `max(length(a),length(b))`

```cpp
class Solution {
public:
    int findLUSlength(string a, string b) {
        if(a == b)
            return -1;
        else
            return max(a.size(), b.size());
    }
};
```
