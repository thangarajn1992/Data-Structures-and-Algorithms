# Longest Uncommon Sub-sequence between array of strings

### Sources

* [Leetcode 522](https://leetcode.com/problems/longest-uncommon-subsequence-ii/)

### Companies

### Problem Statement

Given an array of strings `strs`, return _the length of the **longest uncommon subsequence** between them_. If the longest uncommon subsequence does not exist, return `-1`.

An **uncommon subsequence** between an array of strings is a string that is a **subsequence of one string but not the others**.

A **subsequence** of a string `s` is a string that can be obtained after deleting any number of characters from `s`.

* For example, `"abc"` is a subsequence of `"aebdc"` because you can delete the underlined characters in `"aebdc"` to get `"abc"`. Other subsequences of `"aebdc"` include `"aebdc"`, `"aeb"`, and `""` \(empty string\).

**Example 1:**

```text
Input: strs = ["aba","cdc","eae"]
Output: 3
```

**Example 2:**

```text
Input: strs = ["aaa","aaa","aa"]
Output: -1
```

**Constraints:**

* `1 <= strs.length <= 50`
* `1 <= strs[i].length <= 10`
* `strs[i]` consists of lowercase English letters.

### Solution

1. Sort the strings descending order of size
2. Check each string whether it is a sub-sequence of any other string.
3. If a string is not a sub-sequence of any other string, its size is uncommon sub-sequence.
4. If all strings are sub-sequence of other string,  return -1.

```cpp
class Solution {
public:
    int findLUSlength(vector<string>& strs) {
        // sort strings descending order of size
        sort(strs.begin(), strs.end(),[](string& a,string& b){
           return a.size() > b.size(); 
        });

        for(int str1Index = 0; str1Index < strs.size(); str1Index++){
            bool isSubseq = false;
            for(int str2Index = 0; str2Index < strs.size(); str2Index++){
                //Compare only with strings with size >= its size
                if(strs[str2Index].size() < strs[str1Index].size())
                    break;
               
                // Don't compare same strings at same index
                if(str1Index == str2Index) 
                    continue;
                
                // If subsequence, break the loop
                if(isSubsequence(strs[str1Index],strs[str2Index]))
                {
                    isSubseq = true;
                    break;
                }
            }
            if(!isSubseq)
                return strs[str1Index].size();
        }
        return -1;
    }
    
    // s2.size() >= s1.size()
    bool isSubsequence(string s1 ,string s2){
        int s1Index = 0;
        for(int s2Index = 0;  s2Index < s2.size(); s2Index++){
            if(s2[s2Index] == s1[s1Index])
                s1Index++;
            if(s1Index == s1.size())
                return true;
        }
        return s1Index == s1.size();
    }
};
```

