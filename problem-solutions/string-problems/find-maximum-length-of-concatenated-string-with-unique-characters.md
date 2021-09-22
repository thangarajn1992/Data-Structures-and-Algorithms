# Find maximum length of concatenated string with unique characters

### Sources

* [Leetcode 1239](https://leetcode.com/problems/maximum-length-of-a-concatenated-string-with-unique-characters/)

### Companies

### Problem Statement

Given an array of strings `arr`. String `s` is a concatenation of a sub-sequence of `arr` which have **unique characters**.

Return _the maximum possible length_ of `s`.

**Example 1:**

```text
Input: arr = ["un","iq","ue"]
Output: 4
Explanation: All possible concatenations are "","un","iq","ue","uniq" and "ique".
Maximum length is 4.
```

**Example 2:**

```text
Input: arr = ["cha","r","act","ers"]
Output: 6
Explanation: Possible solutions are "chaers" and "acters".
```

**Example 3:**

```text
Input: arr = ["abcdefghijklmnopqrstuvwxyz"]
Output: 26
```

**Constraints:**

* `1 <= arr.length <= 16`
* `1 <= arr[i].length <= 26`
* `arr[i]` contains only lower case English letters.

### Solution

#### Backtracking approach

```cpp
class Solution {
public:
    int maxLength(vector<string>& arr) {
       return solve(arr,0);
    }
    
    int solve(vector<string> &str, int index, bitset<26> bits = 0, string s="")
    {
        if(index == str.size()) 
            return s.size();  //base case
        
        bitset<26> b{bits};
        for(auto &c: str[index])
        {
            if(b[c - 'a'] == 1)   // character is already in the string
                return solve(str, index+1, bits, s);  //can't include this string
            
            b[c - 'a'] = 1;  //updating our mask
        }
        // if the string can be included
        // then we have to check both choices and return the max value we get
        return max(solve(str, index+1, b, s+str[index]), solve(str, index+1, bits, s)); 
    }
};
```

