# Maximum difference of zeros and ones in binary string

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/maximum-difference-of-zeros-and-ones-in-binary-string4111/1#)

### Companies

### Problem Statement

Given a binary string **S** consisting of 0s and 1s. The task is to find the **maximum difference** of the number of **0s** and the number of **1s** \(number of 0s – number of 1s\) in the substrings of a string.

**Note:** In the case of all 1s, the answer will be -1.

**Example 1:**

```text
Input : S = "11000010001" 
Output : 6 
Explanatio: From index 2 to index 9, 
there are 7 0s and 1 1s, so number 
of 0s - number of 1s is 6. 
```

**Example 2:**

```text
Input: S = "111111"
Output: -1
Explanation: S contains 1s only 
```

**Your task:**  
 You do not need to read any input or print anything. The task is to complete the function **maxSubstring\(\)**, which takes a string as input and returns an integer.

**Expected Time Complexity:** O\(\|S\|\)  
 **Expected Auxiliary Space:** O\(\|S\|\)

**Constraints:**  
 1 ≤ \|S\| ≤ 10^5  
 S contains 0s and 1s only

### Solution

#### Kadane's Algorithm

```cpp
class Solution{
public:	
	int maxSubstring(string S)
	{
	    int maxDifference = -1, maxDiffSoFar = -1;
	    for(int i = 0; i < S.size(); i++)
	    {
	        int val = -1;
	        if(S[i] == '0')
	            val = 1;
	        maxDiffSoFar = max(maxDiffSoFar + val , val);
	        maxDifference = max(maxDifference, maxDiffSoFar);
	    }
	    return maxDifference;
	}
};
```

