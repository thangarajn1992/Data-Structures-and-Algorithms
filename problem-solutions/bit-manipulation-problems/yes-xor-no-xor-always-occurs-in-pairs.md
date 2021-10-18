# Yes XOR No -- XOR Always occurs in pairs

### Source

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/yes-xor-no2901/1#)

### Problem Statement

You are given two arrays **A\[]** and **B\[]**, each of size **N** . Let's consider an integer **X** is the count of all different pairs of **Ai** and **Bj**, such that **Ai XOR Bj** is present in any of the two arrays. Return "**Yes" **(case-sensitive)** **if **X** is even, else return **"No"**.

**Example 1:**

```
Input:
N =  3
A[] = {1, 5, 7}
B[] = {2, 4, 8}
Output:
Yes
Explanation:
XOR(1,2)=3
XOR(1,4) = 5 is present in A[]
XOR(1,8) = 9
XOR(5,2) = 7 is present in A[]
XOR(5,4) = 1 is present in A[]
XOR(5,8) = 13
XOR(7,2) = 5 is present in A[]
XOR(7,4) = 3
XOR(7,8)=15
Out of all these XOR operations, 
5,7,1,5 are present, so count of X = 4 
which is even. Hence the output is "Yes".
```

**Example 2:**

```
Input:
N =  2
A[] = {1, 5}
B[] = {2, 4}
Output:
Yes
Explanation:
XOR(1,2) = 3
XOR(1,4) = 5 is present in A[]
XOR(5,2)=7
XOR(5,4)=1 is present in A[]
Out of all these XOR operations,
1,5 are present,
So count of X = 2 which is even.
Hence the output is "Yes".
```

**Expected Time Complexity:** O(1)\
**Expected Auxiliary Space:** O(1)

**Constraints:**\
 1 <= N <= 10^5\
 1 <= A\[i],B\[i] <= 10^9

### Solution

```cpp
class Solution {
  public:
    string yesXorNo(int N, long long A[], long long B[]) {
        /*
        The Primary Thing to observe in this problem is that,
        a xor b = c  then 
        a xor c = b  Also, 
        b xor c = a

        So If whenever we xor any element from Array A and Array B.
        If its result C is present in the array.....
            Then surely, we would encounter xoring of A with C or B with C
            and surely its result ( B or C respectively) will also be present in the array.
            
        That would make its count even. Basically, Xors occurs in Pairs, always.

        If the result of xoring is not present in the array.
        Then we dont need to worry, as then we are not counting that pair.
        So, Answer will always be a Yes, irrespective of the input.
        */
        return "Yes";
    }
};
```
