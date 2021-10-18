# Minimum Edits to transform one string to another ( Levenshtein Distance )

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/edit-distance3702/1#)
* EPI 17.2

### Companies

* [Google](../../company-based-lists/google.md)
* [Amazon](../../company-based-lists/amazon.md)
* [Microsoft](../../company-based-lists/microsoft.md)

### Problem Statement

Given two strings **s** and **t.** Find the minimum number of operations that need to be performed on str1 to convert it to str2. The possible operations are:

1. Insert a character at any position of the string.
2. Remove any character from the string.
3. Replace any character from the string with any other character.

**Example 1:**

```
Input: 
s = "geek", t = "gesek"
Output: 1
Explanation: One operation is required 
inserting 's' between two 'e's of str1.
```

**Example 2:**

```
Input : 
s = "gfg", t = "gfg"
Output: 
0
Explanation: Both strings are same.
```

**Your Task:**\
 You don't need to read or print anything. Your task is to complete the function **editDistance() **which takes strings s and t as input parameters and returns the minimum number of operation required to make both strings equal. 

\
 **Expected Time Complexity: **O(|s|\*|t|)\
 **Expected Space Complexity: **O(|s|\*|t|)

\
 **Constraints:**\
 1 ≤ Length of both strings ≤ 100\
 Both the strings are in lowercase.

### Solution

#### Dynamic Programming

```cpp
class Solution {
  public:
    int editDistance(string s, string t) 
    {
        // Create a table to store results of subproblems
        int dp[s.size() + 1][t.size() + 1];
 
        // Fill d[][] in bottom up manner
        for (int i = 0; i <= s.size(); i++) {
            for (int j = 0; j <= t.size(); j++) {
                // If first string is empty, only option is to
                // insert all characters of second string
                if (i == 0)
                    dp[i][j] = j; // Min. operations = j
 
                // If second string is empty, only option is to
                // remove all characters of second string
                else if (j == 0)
                    dp[i][j] = i; // Min. operations = i
 
                // If last characters are same, ignore last char
                // and recur for remaining string
                else if (s[i - 1] == t[j - 1])
                    dp[i][j] = dp[i - 1][j - 1];
 
                // If the last character is different, consider
                // all possibilities and find the minimum
                else
                dp[i][j]
                    = 1
                      + min(min(dp[i][j - 1], // Insert
                                 dp[i - 1][j]), // Remove
                            dp[i - 1][j - 1]); // Replace
            }
        }
 
        return dp[s.size()][t.size()];
    }
};
```

