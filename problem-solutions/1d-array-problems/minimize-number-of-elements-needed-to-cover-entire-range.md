# Minimize number of elements needed to cover entire range

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/410d51d667ab93f2219b15126f001f32e8bb029e/1#)

### Companies

* [Microsoft](../../company-based-lists/microsoft.md)

### Problem Statement

A gallery with plants is divided into **n** parts, numbered : 0,1,2,3...n-1. There are provisions for attaching water sprinklers at every partition. A sprinkler with range **x** at partition **i** can water all partitions from **i-x** to **i+x**.  
 Given an array **gallery\[ \]** consisting of **n** integers, where **gallery\[i\]** is the range of sprinkler at partition **i** \(power==-1 indicates no sprinkler attached\), return the minimum number of sprinklers that need to be turned on to water the complete gallery.  
 If there is no possible way to water the full length using the given sprinklers, print -1.

**Example 1:**

```text
Input:
n = 6
gallery[ ] = {-1, 2, 2, -1, 0, 0}
Output:
2
Explanation: Sprinklers at index 2 and 5
can water thefull gallery, span of
sprinkler at index 2 = [0,4] and span
â€‹of sprinkler at index 5 = [5,5].
```

**Example 2:**

```text
Input:
n = 9
gallery[ ] = {2, 3, 4, -1, 2, 0, 0, -1, 0}
Output:
-1
Explanation: No sprinkler can throw water
at index 7. Hence all plants cannot be
watered.
```

**Example 3:**

```text
Input:
n = 9
gallery[ ] = {2, 3, 4, -1, 0, 0, 0, 0, 0}
Output:
3
Explanation: Sprinkler at indexes 2, 7 and
8 together can water all plants.
```

**Your task:**  
 Your task is to complete the function **min\_sprinklers\(\)** which takes the array **gallery\[ \]** and the integer **n** as input parameters and returns the value to be printed.

**Expected Time Complexity:** O\(NlogN\)  
 **Expected Auxiliary Space:** O\(N\)

**Constraints:**  
 1 ≤ n ≤ 10^5  
 gallery\[i\] ≤ 50

### Solution

```cpp
class Solution{
    public:
    int min_sprinklers(int gallery[], int n)
    {
        vector<pair<int,int>> usableSprinklers;
        
        for(int sprinklerNum = 0; sprinklerNum < n; sprinklerNum++)
            if(gallery[sprinklerNum] != -1)
                usableSprinklers.push_back(make_pair(sprinklerNum - gallery[sprinklerNum], 
                                                      sprinklerNum + gallery[sprinklerNum]));
        
        sort(usableSprinklers.begin(), usableSprinklers.end());
        
        int maxRight = 0; // Stores rightmost range we can reach so far
        
        int neededSprinklers = 0; // No. of sprinklers to be turned on
        
        int sprinklerNum = 0;
        
        // Iterate till we cover all range
        while(maxRight < n)
        {
            // If we run out of sprinlers or
            // if we can't reach this sprinler, return -1
            if(sprinklerNum == usableSprinklers.size() || 
               usableSprinklers[sprinklerNum].first > maxRight)
                return -1;
                
            int currMax = INT_MIN;

            // Iterate to all reachable sprinklers
            while(sprinklerNum < usableSprinklers.size() &&
                  usableSprinklers[sprinklerNum].first <= maxRight)
            {
                currMax = max(currMax, usableSprinklers[sprinklerNum].second);
                sprinklerNum++;
            }
            neededSprinklers++;
            maxRight = currMax + 1;
        }
        return neededSprinklers;
    }
};
```

