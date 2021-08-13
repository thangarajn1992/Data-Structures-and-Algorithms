# Number of palindromic strings

### Source

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/number-of-palindromic-strings2706/1#)

### Problem Statement

Given two integers **N** and **K**, the task is to find the count of palindromic strings of length lesser than or equal to **N**, with first K characters of lowercase English language, such that each character in a string doesn’t appear more than twice.

**Note:** Anwer can be very large, so, output answer modulo 109+7

**Example 1:**

```text
Input: N = 3, K = 2
Output: 6
Explanation: The possible strings are:
"a", "b", "aa", "bb", "aba", "bab".
```

**Example 2:**

```text
Input: N = 4, K = 3
Output: 18
Explanation: The possible strings are: 
"a", "b", "c", "aa", "bb", "cc", "aba",
"aca", "bab", "bcb", "cac", "cbc", 
"abba", "acca", "baab", "bccb", "caac", 
"cbbc". 
```

**Expected Time Complexity:** O\(K^2\)  
**Expected Auxiliary Space:** O\(K^2\)

**Constraints:**  
 1 ≤ K ≤ 26  
 1 ≤ N ≤ 52  
 N ≤ 2\*K

### Solution

```cpp
class Solution{
public:	
	
	int palindromicStrings(int N, int K)
	{
        long long mod = 1000000007;
        vector<vector<long long>> dp(K+1, vector<long long>(N+1, 0));
        for(int i = 1; i <= K ; i++)
            dp[i][1] = i, dp[i][2] = i;

        for(int i = 1 ; i <= K ; i++)
            for(int j = 3; j <= N ; j++)
                dp[i][j] = ((dp[i-1][j-2]) * i) % mod;

        long long sum = 0;
        for(int i = 1 ; i <= N ; i++)
            sum = (sum + dp[K][i]) % mod;

        return sum;
	}
};
```



