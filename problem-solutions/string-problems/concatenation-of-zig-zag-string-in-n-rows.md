# Concatenation of Zig-Zag String in n Rows

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/concatenation-of-zig-zag-string-in-n-rows0308/1#)

### Companies

* [Paypal](../../company-based-lists/paypal.md)

### Problem Statement

Given a string and number of rows ‘n’. Print the string formed by concatenating n rows when the input string is written in row-wise Zig-Zag fashion.

**Example 1:**

```
Input: 
str = "ABCDEFGH"
n = 2
Output: "ACEGBDFH"
Explanation: 
Let us write input string in 
Zig-Zag fashion in 2 rows.
A   C   E   G  
  B   D   F   H
Now concatenate the two rows and ignore 
spaces in every row. We get "ACEGBDFH"
```

**Example 2:**

```
Input: 
str = "GEEKSFORGEEKS"
n = 3
Output: GSGSEKFREKEOE
Explanation: 
Let us write input string in 
Zig-Zag fashion in 3 rows.
G       S       G       S
  E   K   F   R   E   K
    E       O       E
Now concatenate the two rows and ignore spaces
in every row. We get "GSGSEKFREKEOE"
```

**Your Task:**\
You need not read input or print anything. Your task is to complete the function **convert() **which takes 2 arguments(string str, integer n) and returns the resultant string.

**Expected Time Complexity: **O(|str|).\
**Expected Auxiliary Space: **O(|str|).

**Constraints:**\
1 ≤ N ≤ 10^5

### Solution

```cpp
class Solution{
    public:
    string convert(string s, int n) {
        if(n <= 1)
            return s;
        int size = s.size();
        string convertedString;
        
        for(int row = 0; row < n && row < size; row++)
        {
            bool up = true;
            int index = row;
            while(index < size)
            {
                convertedString += s[index];
                if(row == 0 || row == n - 1)
                    index += (n - 1)  * 2;
                else
                {
                    if(up == true)
                        index += (n - row - 1) * 2;
                    else
                        index += row * 2;
                    up ^= true;
                }
            }
        }
        return convertedString;
    }
};
```



