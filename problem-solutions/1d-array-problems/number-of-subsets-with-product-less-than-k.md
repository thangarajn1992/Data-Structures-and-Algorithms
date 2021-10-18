# Number of subsets with product less than k

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/number-of-subsets-with-product-less-than-k/1#)

### Companies

* [Amazon](../../company-based-lists/amazon.md)

### Problem Statement

Given an array **arr\[]** of **N** elements. Find the number of non-empty subsets whose product of elements is less than or equal to a given integer **K**.

**Example 1:**

```
Input:
N = 4
arr[] = {2, 4, 5, 3}
K = 12
Output:
8
Explanation:
All possible subsets whose 
products are less than 12 are:
(2), (4), (5), (3), (2, 4), (2, 5), (2, 3), (4, 3)
```

**Example 2:**

```
Input:
N = 3
arr[] = {9, 8, 3}
K = 2 
Output:
0
Explanation:
There is no subsets with product less
than or equal to 2.

```

Complete the function **numOfSubsets()** which takes 2 integers N, and K, and an array arr of size N as input and returns the number of subsets with product less equal to K.

\
 **Expected Time Complexity:** O(N\*2N/2)\
 **Expected Auxiliary Space:** O(N)

\
 **Constraints:**\
 1 ≤ N ≤ 30\
 1 ≤ arr\[i] ≤ 10\
 1 ≤ K ≤ 10^6

### Solution

```cpp
class Solution {
public:
    int numOfSubsets(int arr[], int n, int k) {
        vector<int> vect1, vect2; // dividing vectors into two
        vector<long long int>subset1, subset2; // subsets for 2 halves of vector

        // ignore element greater than k and divide array into 2 halves
        for (int i = 0; i <= n/2; i++)
            if (arr[i] <= k)
                vect1.push_back(arr[i]);
        
        for(int i = (n/2)+1; i < n; i++)
            if(arr[i] <= k)
                vect2.push_back(arr[i]);

        // generate all subsets for 1st half (vect1)
        int vect1Size = vect1.size();
        long long int totalSubsets = pow(2,vect1Size);
        
        for (int i = 0; i < totalSubsets; i++) {
            long long value = 1;
            for (int j = 0; j < vect1Size; j++) {
                if (i & (1 << j))
                    value *= vect1[j];
            }
            if (value <= k)
                subset1.push_back(value);
        }

        // generate all subsets for 2nd half (vect2)
        int vect2Size = vect2.size();
        totalSubsets = pow( 2,vect2Size);
        for (int i = 0; i < totalSubsets; i++) {
            long long value = 1;
            for (int j = 0; j < vect2Size; j++) {
                if (i & (1 << j))
                    value *= vect2[j];
            }
            if (value <= k)
                subset2.push_back(value);
        }

        sort(subset2.begin(), subset2.end());

        long long count = 0;
        for (int i = 0; i < subset1.size(); i++)
        {
            vector<long long int>::iterator it = upper_bound(subset2.begin(), 
                                                             subset2.end(), 
                                                             (k / subset1[i]));
            count += (it - subset2.begin());                  
        }
        // for null subset decrement the value of count
        count--;

        return count;
    }
};
```

