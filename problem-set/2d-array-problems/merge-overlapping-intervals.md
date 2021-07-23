# Merge Overlapping Intervals

[InterviewBit](https://www.interviewbit.com/problems/merge-overlapping-intervals/)

[Leetcode 56](https://leetcode.com/problems/merge-intervals/)

### Problem Statement

Given a collection of intervals, merge all overlapping intervals.

**For example:**

Given `[1,3],[2,6],[8,10],[15,18]`,

return `[1,6],[8,10],[15,18]`.

Make sure the returned intervals are sorted.

### Solution

```cpp
/**
 * Definition for an interval.
 * struct Interval {
 *     int start;
 *     int end;
 *     Interval() : start(0), end(0) {}
 *     Interval(int s, int e) : start(s), end(e) {}
 * };
 */
 bool comp(Interval A, Interval B)
 {
     return A.start < B.start;
 }
vector<Interval> Solution::merge(vector<Interval> &A) {
    sort(A.begin(), A.end(), comp);
    vector<Interval> result;
    int size = A.size();
    if(size == 0)
        return result;
    result.push_back(A[0]);
    for(int i = 1; i < size; i++)
    {
        if(result.back().end < A[i].start) // no overlap
            result.push_back(A[i]);
        else if(result.back().end < A[i].end)
            result.back().end = A[i].end;
    }
    return result;
}
```

