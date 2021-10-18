# Number of Non-Reachable Numbers using two co-prime numbers

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/2caf0501a39567d653197364a2b5c8a9f5943b7e/1#)

### Companies

### Problem Statement

In the game of Restricted Pacman, an infinite linear path is given. Pacman has to start at position 0 and eat as many candies as possible. In one move he can only jump a distance of either **M** or **N**.  If **M** and **N** are co-prime numbers, find how many candies will be left on the board after the game is over.\
 **Note:** The result is always finite as after a point **X** every index in the infinite path can be visited. 

**Example 1:**

```
Input: M = 2, N = 5
Output: 2
Explanation: From index 0, the indices that 
can be visited are
0 + 2 = 2
0 + 2 + 2 = 4
0 + 5 = 5
0 + 2 + 2 + 2 = 6
0 + 2 + 5 = 7
0 + 2 + 2 + 2 + 2 = 8
0 + 2 + 2 + 5 = 9
0 + 5 + 5 = 10
and so on.
1 and 3 are the only indices that cannot be 
visited. Therefore the candies at these two 
positions will be left on the board. 
```

\
 **Example 2:**

```
Input: M = 2, N = 7
Output: 3 
```

**Example 3:**

```
Input: M = 25, N = 7
Output: 72
```

**Your Task:**  \
 You don't need to read input or print anything. Complete the function **candies()** which take M and N as input parameters and return the answer.

**Expected Time Complexity:** O(N)\
**Expected Auxiliary Space:** O(N)

**Constraints:**\
 1 < M, N ≤ 500

### Solution

#### Frobenius Number

[https://mathworld.wolfram.com/CoinProblem.html](https://mathworld.wolfram.com/CoinProblem.html)

The largest such ![N](https://mathworld.wolfram.com/images/equations/CoinProblem/Inline14.gif) for a given problem is called the [Frobenius number](https://mathworld.wolfram.com/FrobeniusNumber.html) ![g(a\_1,a\_2,...)](https://mathworld.wolfram.com/images/equations/CoinProblem/Inline15.gif).

 The result

| ![g(a\_1,a\_2)](https://mathworld.wolfram.com/images/equations/CoinProblem/Inline16.gif) | ![=](https://mathworld.wolfram.com/images/equations/CoinProblem/Inline17.gif) | ![(a\_1-1)(a\_2-1)-1](https://mathworld.wolfram.com/images/equations/CoinProblem/Inline18.gif)   |  (2) |
| ---------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------ | ---- |
| ![](https://mathworld.wolfram.com/images/equations/CoinProblem/Inline19.gif)             | ![=](https://mathworld.wolfram.com/images/equations/CoinProblem/Inline20.gif) | ![a\_1a\_2-(a\_1+a\_2)](https://mathworld.wolfram.com/images/equations/CoinProblem/Inline21.gif) |  (3) |

 The total number of such non-representable amounts is given by

| ![ 1/2(N+1)=1/2(a\_1-1)(a\_2-1). ](https://mathworld.wolfram.com/images/equations/CoinProblem/NumberedEquation2.gif) |  (4) |
| -------------------------------------------------------------------------------------------------------------------- | ---- |

```cpp
class Solution{
    public:
    
    /* As per Frobenius number, the maximum number that cannot be formed using 2 co-prime numbers is
       X = (M * N) - M - N 
       i.e
       X = (M - 1) * (N - 1) - 1;
       The total number of non-reachable numbers are (X+1)/2 :-D !!!!!
    */
    int candies(int m , int n)
    {
        int frobeniusNumber = (m * n) - m - n;
        return (frobeniusNumber+1)/2;
    }
    
```

#### My initial working solution

```cpp
class Solution{
    public:
    int candies(int m, int n) 
    { 
    	int total = m * n;
    	vector<bool> candiesEaten(total+1,false);
    	vector<int> mcandies, ncandies;
    	for(int index = 1; index <= n; index++)
    	{
            mcandies.push_back(m*index);
            candiesEaten[m*index] = true;
    	}
    	for(int index = 1; index <= m; index++)
    	{
    	    ncandies.push_back(n*index);
    	    candiesEaten[n*index] = true;
        }
    	
    	for(int mindex = 0; mindex < mcandies.size(); mindex++)
    	{
    	    for(int nindex = 0; nindex < ncandies.size(); nindex++)
    	    {
    	        int value = mcandies[mindex] + ncandies[nindex];
    	        if(value <= total)
    	            candiesEaten[value] = true;
    	    }
    	}
    	int candiesLeft = 0;
    	for(int index = 1; index <= total; index++)
    	    if(candiesEaten[index] == false)
    	        candiesLeft++;
    	        
    	return candiesLeft;
    } 
};
```
