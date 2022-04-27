# Find starting point to complete circular tour of set of petrol bunks

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/circular-tour-1587115620/1#)

### Companies

* [Google](../../company-based-lists/google.md)
* [Amazon](../../company-based-lists/amazon.md)
* [Microsoft](../../company-based-lists/microsoft.md)

### Problem Statement

Suppose there is a circle. There are **N** petrol pumps on that circle. You will be given two sets of data.\
&#x20;**1.** The amount of petrol that every petrol pump has.\
&#x20;**2.** Distance from that petrol pump to the next petrol pump.\
&#x20;Find a starting point where the truck can start to get through the complete circle without exhausting its petrol in between.Assume for 1 litre petrol, the truck can go 1 unit of distance. Your task is to complete the function **tour**() which takes the required data as inputs and returns an integer denoting a point from where a truck will be able to complete the circle (The truck will stop at each petrol pump and it has infinite capacity). If there exists multiple such starting points, then the function must return the first one out of those. (return -1 otherwise)

**Example 1:**

```
Input:
N = 4
Petrol = 4 6 7 4
Distance = 6 5 3 5
Output: 1
Explanation: There are 4 petrol pumps with
amount of petrol and distance to next
petrol pump value pairs as {4, 6}, {6, 5},
{7, 3} and {4, 5}. The first point from
where truck can make a circular tour is
2nd petrol pump. Output in this case is 1
(index of 2nd petrol pump).Your Task:
 
```

**Expected Time Complexity:** O(N)\
**Expected Auxiliary Space** : O(1)

**Constraints:**\
&#x20;2 ≤ N ≤ 10000\
&#x20;1 ≤ petrol, distance ≤ 1000

### Solution

```cpp
class Solution{
  public:
    //Function to find starting point where the truck can start to get through
    //the complete circle without exhausting its petrol in between.
    int tour(petrolPump p[],int n)
    {
       int start = 0, end = 1;
       int cur_petrol = p[start].petrol - p[start].distance;
       
       while(end != start || cur_petrol < 0)
       {
           // If current petrol in truck becomes less than 0, 
           // then remove the starting pump from tour
           while(cur_petrol < 0 && start != end)
           {
               cur_petrol -= p[start].petrol - p[start].distance;
               start = (start + 1) % n;
               
               //if 0 is considered as start again, then no solution possible
               if(start == 0)
                    return -1;
           }         
           // Add a petrol bunk to current tour
           cur_petrol += p[end].petrol - p[end].distance;
           end = (end + 1) % n;
        }
        return start;
    }
};
```
