# Circular Prime Number or not

### Sources

* [GeeksForGeeks](https://practice.geeksforgeeks.org/problems/circular-prime-number0230/1#)

### Companies

### Problem Statement

A prime number is a [**Circular Prime Number **](https://en.wikipedia.org/wiki/Circular\_prime)if all of its possible rotations are itself prime numbers. Now given a number N check if it is Circular Prime or Not.

**Example 1:**

```
Input: N = 197
Output: 1
Explanation: 197 is a Circular Prime because
all rotations of 197 are 197, 719, 971 all of 
the 3 are prime number's hence 197 is a 
circular prime.
```

**Example 2:**

```
Input: N = 101
Output: 0
Explanation: 101 and 11 is prime but 110 is
not a prime number.
```

**Your Task:**\
You don't need to read or print anything. Your task is to complete the function **isCircularPrime()** which takes N as input parameter and returns 1 if it is Circular Prime otherwise returns 0.\
&#x20;

**Expected Time Complexity: **O(Nlog(log(N))\
**Expected Space Complexity: **O(N)\
&#x20;

**Constraints:**\
1 <= N <= 10^5

### Solution

```cpp
class Solution
{
public:
    int isCircularPrime(int n) {
        // Count digits.
        int count = 0, temp = n;
        while (temp) {
            count++;
            temp /= 10;
        }
 
        int num = n;
        int multiple = pow(10, count - 1);
        while (isPrime(num)) {
            // Following three lines generate the next
            // circular permutation of a number. We move
            // last digit to first position.
            int rem = num % 10;
            int div = num / 10;
            num = multiple * rem + div;
 
            // If all the permutations are checked and
            // we obtain original number exit from loop.
            if (num == n)
                return true;
        }
 
        return false;	
	}
	
    // Function to check if a number is prime or not.
    bool isPrime(int n)
    {
        // Corner cases
        if (n <= 1)
            return false;
        if (n <= 3)
            return true;
 
        // This is checked so that we can skip
        // middle five numbers in below loop
        if (n % 2 == 0 || n % 3 == 0)
            return false;
 
        for (int i = 5; i * i <= n; i = i + 6)
            if (n % i == 0 || n % (i + 2) == 0)
                return false;
 
        return true;
    }
};
```
