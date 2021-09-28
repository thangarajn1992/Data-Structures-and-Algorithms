# Break a Palindrome

### Sources

* [Leetcode 1328](https://leetcode.com/problems/break-a-palindrome/)

### Companies

### Problem Statement

Given a palindromic string of lowercase English letters `palindrome`, replace **exactly one** character with any lowercase English letter so that the resulting string is **not** a palindrome and that it is the **lexicographically smallest** one possible.

Return _the resulting string. If there is no way to replace a character to make it not a palindrome, return an **empty string**._

A string `a` is lexicographically smaller than a string `b` \(of the same length\) if in the first position where `a` and `b` differ, `a` has a character strictly smaller than the corresponding character in `b`. For example, `"abcc"` is lexicographically smaller than `"abcd"` because the first position they differ is at the fourth character, and `'c'` is smaller than `'d'`.

**Example 1:**

```text
Input: palindrome = "abccba"
Output: "aaccba"
Explanation: 
There are many ways to make "abccba" not a palindrome, such as "zbccba", "aaccba", and "abacba".
Of all the ways, "aaccba" is the lexicographically smallest.
```

**Example 2:**

```text
Input: palindrome = "a"
Output: ""
Explanation: 
There is no way to replace a single character to make "a" not a palindrome, 
so return an empty string.
```

**Example 3:**

```text
Input: palindrome = "aa"
Output: "ab"
```

**Example 4:**

```text
Input: palindrome = "aba"
Output: "abb"
```

**Constraints:**

* `1 <= palindrome.length <= 1000`
* `palindrome` consists of only lowercase English letters.

### Solution

```cpp
class Solution {
public:
    string breakPalindrome(string palindrome) {
        int size = palindrome.size();
        if(size == 1)
            return "";
        int halfSize = size/2;
        // Replace the first charcter != 'a' as 'a' to break palindrome
        // and also we will get lexicographically smallest string.
        for(int index = 0; index < halfSize; index++)
        {
            if(palindrome[index] != 'a')
            {
                palindrome[index] = 'a';
                return palindrome;
            }
        }
        // If all characters are 'a', then replace the last character to b
        palindrome[size-1] = 'b';
        return palindrome;
    }
};
```

