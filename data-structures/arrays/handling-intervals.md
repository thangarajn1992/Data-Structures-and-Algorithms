# Handling Intervals

Let's first have a look at some examples of intersections between two intervals:

1. Intersection between s1 and e2: `s2 s1____e2 e1`
2. Intersection between s2 and e1: `s1 s2____e1 e2`
3. Intersection between s1 and e1: `s2 s1____e1 e2`

Given that we can write one simple if statement to check if there is an intersection between two intervals `(start1, end1)` and `(start2, end2)`:

```cpp
if (start1 < end2 && end1 > start2) 
    return true;
    
// or we can check differently
int start = max(start1, start2);
int end = min(end1, end2);
if (start <= end) 
    return true
```

Usually during solving these types of problems we need to know If our intervals have some intersection or how many times we meet some interval intersection. I found two useful code example helpful to solve such problems:

```cpp
// Sorting intervals based on starting time and checking if we have encounter intersection.
sort(intervals.begin(), intervals.end());

//Sorting ensures that s1 < e2
for (int i = 1; i < intervals.size(); i++) {
    if (intervals[i - 1][1] > intervals[i][0]) // ensures that e1 > s2
        return false;  // We have intersection here.
}
```

```cpp
// Using map to track start/end times of our intervals.
map<int, int> inter;
for (auto& i : intervals) {
	inter[i[0]]++;
	inter[i[1]]--;
}

// Then by traversing map we can find how many intersections we had.
int res = 0, count = 0;
for (auto& [time, val] : inter) {
	count += val;
	res = max(res, count); // Max number of intervals intersects at any point of time.
}
```

