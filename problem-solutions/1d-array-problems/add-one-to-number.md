# Add One to Number

[Leetcode 66](https://leetcode.com/problems/plus-one/)

[InterviewBit](https://www.interviewbit.com/problems/add-one-to-number/)

### Problem Statement

Given a non-negative number represented as an array of digits,

add 1 to the number \( increment the number represented by the digits \).

The digits are stored such that the most significant digit is at the head of the list.

**Example:**

If the vector has `[1, 2, 3]`

the returned vector should be `[1, 2, 4]`

as `123 + 1 = 124`.

> **NOTE:** Certain things are intentionally left unclear in this question which you should practice asking the interviewer.  
>  For example, for this problem, following are some good questions to ask :
>
> * **Q :** Can the input have 0’s before the most significant digit. Or in other words, is `0 1 2 3` a valid input?
> * **A :** For the purpose of this question, **YES**
> * **Q :** Can the output have 0’s before the most significant digit? Or in other words, is `0 1 2 4` a valid output?
> * **A :** For the purpose of this question, **NO**. Even if the input has zeroes before the most significant digit.

### Solution

```cpp
vector<int> Solution::plusOne(vector<int> &A) {
    int size = A.size();
    int i;
    
    // remove trailing zeroes
    for(i = 0; i < size && A[i] == 0; i++);
    A.erase(A.begin(), A.begin()+i);  
      
    size = A.size();
    int carry_in = 1;
    
    for(i = size - 1; i >= 0 && carry_in; i--)
    {
        A[i] += carry_in;
        carry_in = A[i]/10;
        A[i] %= 10;
    }
    if(carry_in)
        A.insert(A.begin(), 1);
    return A;
}
```

