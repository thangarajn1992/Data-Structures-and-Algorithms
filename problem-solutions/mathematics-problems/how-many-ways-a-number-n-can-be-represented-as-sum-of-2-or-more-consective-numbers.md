# How many ways a number N can be represented as sum of 2 or more consective numbers

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/count-of-sum-of-consecutives3741/1#)
* [Leetcode 829](https://leetcode.com/problems/consecutive-numbers-sum/)

### Companies

* [Walmart](../../company-based-lists/walmart.md)

### Problem Statement

Given a number **N**, the task is find the number of ways to represent this number as a sum of 2 or more consecutive natural numbers.

**Example 1:**

```text
Input:
N = 10
Output:
1
Explanation:
10 can be reprsented as sum of two or
more consecutive numbers in only one
way. 10 = 1+2+3+4.
```

**Example 2:**

```text
Input:
N = 15
Output:
3
Explanation:
15 can be reprsented as sum of two or
more consecutive numbers in 3 ways.
(15 = 1+2+3+4+5); (15 = 4+5+6); (15 = 7+8).
```

**Your Task:**  
 You don't need to read input or print anything. Your task is to complete the function **getCount\(\)** which takes an Integer n as input and returns the answer.

**Expected Time Complexity:** O\(sqrt\(N\)\)  
 **Expected Auxiliary Space:** O\(1\)

**Constraints:**  
 1 &lt;= N &lt;= 10^8

### Solution

```cpp
/*
Lets say consecutive numbers are: a,a+1,a+2...a+k-1
a + a+1 + a+2 + ...+ a+k-1 == n
ka + 1 + 2 + 3 +...+ k-1 == n
ka+ k*(k-1)/2 == n

a = (n- k*(k-1)/2) % k

so the values of a would be : (n-k*(k-1)/2)/k if k divides  n-k*(k-1)/2;
 
so, maximum value of k can be taken as:
n - (k *(k-1)/2() > 0
2n > k*k

*/
class Solution {
public:
    int consecutiveNumbersSum(int n) {
        int ans = 0, k;
        int maxK = sqrt(2*n);
        for(k = 1; k <= maxK; k++) {
            if((n - k*(k-1)/2) % k == 0) 
                ans++;
        }   
        return ans;
    }
};
```



