# Swap all odd and even bits

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/swap-all-odd-and-even-bits-1587115621/1#)

### Companies



### Problem Statement

Given an unsigned integer **N**. The task is to swap all odd bits with even bits. For example, if the given number is 23 (**0**0**0**1**0**1**1**1), it should be converted to 43(0**0**1**0**1**0**1**1**). Here, every even position bit is swapped with adjacent bit on the right side(even position bits are highlighted in the binary representation of 23), and every odd position bit is swapped with an adjacent on the left side.\
\
**Example 1**:

```
Input: N = 23
Output: 43
Explanation: 
Binary representation of the given number 
is 00010111 after swapping 
00101011 = 43 in decimal.
```

**Example 2**:

```
Input: N = 2
Output: 1
Explanation: 
Binary representation of the given number 
is 10 after swapping 01 = 1 in decimal.
```

\
**Your Task: **Your task is to complete the function **swapBits**() which takes an integer and **returns an **integer with all the odd and even bits swapped.

\
**Expected Time Complexity:** O(1).\
**Expected Auxiliary Space:** O(1).\
\
**Constraints:**\
1 ≤ N ≤ 10^9

### Solution

```cpp
class Solution
{
    public:
    //Function to swap odd and even bits.
    unsigned int swapBits(unsigned int n)
    {
        unsigned int evenBits = n & 0xAAAAAAAA;
        unsigned int oddBits = n & 0x55555555;
        
        evenBits >>= 1;
        oddBits <<= 1;
        
    	return (evenBits | oddBits);
    }
};
```
