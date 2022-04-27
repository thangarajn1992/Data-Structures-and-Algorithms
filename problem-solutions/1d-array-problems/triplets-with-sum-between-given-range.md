# Triplets with Sum between given range

[InterviewBit](https://www.interviewbit.com/problems/triplets-with-sum-between-given-range/)

### Problem Statement

Given an array of real numbers greater than zero in form of strings. Find if there exists a **triplet** (a,b,c) such that **1** < **a+b+c** < **2** . Return **1** for **true** or **0** for **false**.

**Example:**

Given `[0.6, 0.7, 0.8, 1.2, 0.4]` , You should return **`1` ** as `0.6+0.7+0.4=1.7`  `1<1.7<2`

**O(n)** solution is expected.

**Note**: You can assume the numbers in strings don’t overflow the primitive data type and there are no leading zeroes in numbers. Extra memory usage is allowed.

### Solution

```cpp
int Solution::solve(vector<string> &A) {
    vector<float> A_float;
    for(const string a : A)
        A_float.push_back(stof(a));
    if(A_float.size() < 3)
        return 0;
    float a = A_float[0], b = A_float[1], c = A_float[2];
    for(int i = 3; i < A_float.size(); i++)
    {
        if(a+b+c < 2.0 && a+b+c > 1.0)
            return 1;
        else
        {
            if(a+b+c > 2.0)
            {
                //replace max with next element
                if(a >= b && a >= c)
                    a = A_float[i];
                else if(b >= a && b >= c)
                    b = A_float[i];
                else if( c >=a && c >= b)
                    c = A_float[i];
            }
            else
            {
                // replace min with next element
                if(a <= b && a <= c)
                    a = A_float[i];
                else if(b <= a && b <= c)
                    b = A_float[i];
                else if( c <=a && c <= b)
                    c = A_float[i];
            }
        }
    }
    if(a+b+c > 1.0 && a+b+c < 2.0)
        return 1;

    return 0;
}
```
