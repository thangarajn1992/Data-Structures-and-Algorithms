# Distribute N candies among K people

### Source

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/distribute-n-candies/1#)

### Problem Statement

Given **N** candies and **K** people. In the first turn, the first person gets 1 candy, the second gets 2 candies, and so on till K people. In the next turn, the first person gets K+1 candies, the second person gets K+2 candies and so on. If the number of candies is less than the required number of candies at every turn, then the person receives the remaining number of candies. Find the total number of candies every person has at the end.

**Example 1:**

```text
Input:
N = 7, K = 4
Output:
1 2 3 1
Explanation:
At the first turn, the fourth person
has to be given 4 candies, but there is
only 1 left, hence he takes only one. 
```

**Example 2:**

```text
Input:
N = 10, K = 3
Output :
5 2 3
Explanation:
At the second turn first one receives
4 and then we have no more candies left. 

```

**Expected Time Complexity:** O\(logN+K\)  
**Expected Auxiliary Space:** O\(K\)

  
 **Constraints:**  
 1 ≤ N ≤ 10^8  
 1 ≤ K ≤ 100

### Solution

#### Naive Approach

```cpp
class Solution {
  public:
    vector<long long> distributeCandies(int N, int K) {
        vector<long long> result(K,0);
        int value = 1; 
        long long index = 0;
        while(N > 0)
        {
            int val = min(N, value);
            result[index % K] += val;
            N -= value;
            value++;
            index++;
        }
        return result;
    }
};
```

#### Binary Search 

1. An **efficient approach** is to find the largest number\(say MAXI\) whose sum upto natural numbers is less than N using Binary search. 
2. Since the last number will always be a multiple of K, we get the last number of complete turns. Subtract the summation till then from N.
3. Distribute the remaining candies by traversing in the array. 

```cpp
class Solution {
  public:
    vector<long long> distributeCandies(int N, int K) {
        int left = 0, right = N/2;
        int no_of_rounds = 0;
        int valid_sum = 0;
        while(left <= right)
        {
            long long int mid = (left + right) >> 1;
            unsigned long long int sum = (mid * (mid+1))/2;

            if(sum <= (unsigned long long int)N)
            {
                left = mid + 1;
                no_of_rounds = mid/K;
            }
            else
            {
                right = mid - 1;
            }
        }
        int curr_value = no_of_rounds * K;
        N -= (curr_value * (curr_value+1))/2;
    
        int index = 0;
        vector<long long> result(K, 0);
        while(index < K)
        {
            curr_value++;
            // Sn = (n/2)[2*a + (n-1)d]
            long long value_till_complete_round = 
             ((no_of_rounds) * ((2 *(index+1) + (no_of_rounds - 1)*(K))))/2;
            int val = min(N, curr_value);
            result[index] += (long long)val + value_till_complete_round;
            if(N - curr_value > 0)
                N -= curr_value;
            else
                N = 0;
            index++;
        }
        return result;
    }    

};
```

