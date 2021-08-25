# Search Pattern \(KMP-Algorithm\)

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/search-pattern0205/1#)

### Companies

* [Microsoft](../../company-based-lists/microsoft.md)

### Problem Statement

Given two strings, one is a text string, **txt** and other is a pattern string, **pat**. The task is to print the indexes of all the occurences of pattern string in the text string. For printing, Starting Index of a string should be taken as 1.

  
 **Example 1:**

```text
Input:
txt = "batmanandrobinarebat", pat = "bat"
Output: 1 18
Explanation: The string "bat" occurs twice
in txt, one starts are index 1 and the other
at index 18. 
```

**Example 2:**

```text
Input: 
txt = "abesdu", pat = "edu"
Output: -1
Explanation: There's not substring "edu"
present in txt.
```

**Expected Time Complexity:** O\(\|txt\|\).  
**Expected Auxiliary Space:** O\(\|txt\|\).

**Constraints:**  
 1 ≤ \|txt\| ≤ 10^5  
 1 ≤ \|pat\| &lt; \|S\|

### Solution

#### [KMP pattern Search Algorithm](../../data-structures/strings/string-algorithms/kmp-matching-algorithm-knuth-morris-pratt.md)

```cpp
class Solution
{
public:
    vector<int> search(string pattern, string text)
    {
        vector<int> startIndices;
        int patternLen = pattern.size();
            
        // calculate lps as per KMP Algorithm
        // lps is either longest proper prefix which is also suffix
        // or lps is longest proper suffix which is also prefix
        vector<int> lps(patternLen, 0);
        int patternIndex = 1;
        int lpsLen = 0;
        
        while(patternIndex < patternLen)
        {
            if(pattern[patternIndex] == pattern[lpsLen])
            {
                lpsLen++;
                lps[patternIndex] = lpsLen;
                patternIndex++;
            }
            else
            {
                if(lpsLen != 0)
                    lpsLen = lps[lpsLen - 1];
                else
                {
                    lps[patternIndex] = 0;
                    patternIndex++;
                }
            }
        }    
        // Using calculated lps, do optimised pattern search
        patternIndex = 0;
        int textIndex = 0;
        int textLen = text.size();
        while(textIndex < textLen)
        {
            if(text[textIndex] == pattern[patternIndex])
            {
                textIndex++;
                patternIndex++;
            }
            
            if(patternIndex == patternLen)
            {
                // found the match
                startIndices.push_back(textIndex - patternIndex + 1);
                patternIndex = lps[patternIndex - 1];
            }
            else if(textIndex < textLen && text[textIndex] != pattern[patternIndex])
            {
                if(patternIndex != 0)
                    patternIndex = lps[patternIndex - 1];
                else
                    textIndex++;
            }    
        }
        return startIndices;
    }
};
```



