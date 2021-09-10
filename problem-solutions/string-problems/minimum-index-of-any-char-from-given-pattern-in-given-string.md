# Minimum index of any char from given pattern in given string

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/minimum-indexed-character-1587115620/1#)

### Companies

### Problem Statement

Given a string **str** and another string **patt**. Find the first position \(considering 0-based indexing\) of the character in **patt** that is present at the minimum index in **str**. Complete the function **minIndexChar\(\)** that returns the index of answer in str or returns -1 in case no character of patt is present in str.  
 **Example 1:**

```text
Input:
str = geeksforgeeks
patt = set
Output: 1
Explanation: e is the character which is
present in given patt "geeksforgeeks"
and is first found in str "set". First Position
of e in str is 1. 
```

**Example 2:**

```text
Input:
str = adcffaet
patt = onkl
Output: -1
Explanation: There are none of the
characters which is common in patt
and str.
```

 **Expected Time Complexity:** O\(N\).  
 **Expected Auxiliary Space:** O\(Number of distinct characters\).

  
 **Constraints:**  
 1 ≤ \|str\| , \|patt\| ≤ 10^5

### Solution

```cpp
class Solution
{
  public:
    int minIndexChar(string str, string patt)
    {
        set<char> myset;
        for(char c : patt)
            myset.insert(c);
        for(int i = 0; i < str.size(); i++)
            if(myset.find(str[i]) != myset.end())
                return i;
        return -1;
    }
};
```

