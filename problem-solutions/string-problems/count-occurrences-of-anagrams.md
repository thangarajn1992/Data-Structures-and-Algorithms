# Count Occurrences of Anagrams

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/count-occurences-of-anagrams5839/1#)

### Companies

* [Amazon](../../company-based-lists/amazon.md)
* [Microsoft](../../company-based-lists/microsoft.md)

### Problem Statement

Given a word **pat** and a text **txt**. Return the count of the occurrences of anagrams of the word in the text.

**Example 1:**

```text
Input:
txt = forxxorfxdofr
pat = for
Output: 3
Explanation: for, orf and ofr appears
in the txt, hence answer is 3.
```

**Example 2:**

```text
Input:
txt = aabaabaa
pat = aaba
Output: 4
Explanation: aaba is present 4 times
in txt.
```

**Expected Time Complexity:** O\(N\)  
**Expected Auxiliary Space:** O\(26\) or O\(256\)

**Constraints:**  
 1 &lt;= \|pat\| &lt;= \|txt\| &lt;= 10^5  
 Both string contains lowercase english letters.

### Solution

```cpp
class Solution{
public:
	int search(string pat, string txt) {
	    int patLen = pat.size();
	    int txtLen = txt.size();
	    vector<int> freq(26,0);
	    vector<int> curFreq(26,0);

	    for(int i = 0; i < patLen; i++)
	    {
	        freq[pat[i] - 'a']++;
	        curFreq[txt[i] - 'a']++;
	    }

	    int occurences = 0;
        
        if(freq == curFreq)
            occurences++;
            
	    for(int index = patLen; index < txtLen; index++)
	    {
	        curFreq[txt[index] - 'a']++;
	        curFreq[txt[index - patLen] - 'a']--;
	        if(curFreq == freq)
	            occurences++;
	    }
	    
	    return occurences;
	}
};
```

