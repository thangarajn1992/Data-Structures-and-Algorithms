# Maximum Meetings in One Room

### Sources

* [GeeksforGeeks](https://practice.geeksforgeeks.org/problems/n-meetings-in-one-room-1587115620/1#)

### Companies

* [Amazon](../../company-based-lists/amazon.md)
* [Microsoft](../../company-based-lists/microsoft.md)
* [Flipkart](../../company-based-lists/flipkart.md)

### Problem Statement

There is **one** meeting room in a firm. There are **N** meetings in the form of **(start\[i], end\[i])** where **start\[i]** is start time of meeting **i** and **end\[i]** is finish time of meeting **i.**\
&#x20;What is the **maximum** number of meetings that can be accommodated in the meeting room when only one meeting can be held in the meeting room at a particular time? **Note:** Start time of one chosen meeting can't be equal to the end time of the other chosen meeting. Complete the function **maxMeetings()** __ that takes two arrays **start\[]** and **end\[]** along with their size **N** as input parameters and returns the **maximum** number of meetings that can be held in the meeting room.

\
&#x20;**Example 1:**

```
Input:
N = 6
start[] = {1,3,0,5,8,5}
end[] =  {2,4,6,7,9,9}
Output: 
4
Explanation:
Maximum four meetings can be held with
given start and end timings.
The meetings are - (1, 2),(3, 4), (5,7) and (8,9)
```

**Example 2:**

```
Input:
N = 3
start[] = {10, 12, 20}
end[] = {20, 25, 30}
Output: 
1
Explanation:
Only one meetings can be held
with given start and end timings.
```

**Expected Time Complexity** : O(N\*LogN)\
**Expected Auxilliary Space** : O(N)

\
&#x20;**Constraints:**\
&#x20;1 ≤ N ≤ 10^5\
&#x20;0 ≤ **star**t**\[i]** < **end\[i]** ≤ 10^5

### Solution

### Greedy Algorithm by scheduling meeting with less finish time

```cpp
class Solution
{
    public:
    int maxMeetings(int start[], int end[], int n)
    {
        vector<pair<int,int>> duration;
        for(int i = 0; i < n ; i++)
            duration.push_back(make_pair(end[i], start[i]));
        
        sort(duration.begin(), duration.end()); // sorting based on end time
        
        int timeConsumed = duration[0].first;
        int totalMeetings = 1;
        for(int i = 1; i < n; i++)
        {
            if(duration[i].second > timeConsumed)
            {
                timeConsumed = duration[i].first; // schedule this meeting
                totalMeetings++;
            }
        }
        return totalMeetings;
    }
};
```
