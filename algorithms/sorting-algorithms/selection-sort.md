# Selection Sort

Selection sort is a simple comparison-based sorting algorithm. It is in-place and needs no extra memory.

The idea behind this algorithm is pretty simple. We divide the array into two parts: sorted and unsorted. The left part is sorted sub-array and the right part is unsorted sub-array. Initially, sorted subarray is empty and unsorted array is the complete given array.

#### Algorithm

We perform the steps given below until the unsorted sub-array becomes empty:

1. Pick the minimum element from the unsorted sub-array.
2. Swap it with the leftmost element of the unsorted sub-array.
3. Now the leftmost element of unsorted sub-array becomes a part (rightmost) of sorted sub-array and will not be a part of unsorted sub-array.

#### Example

### A selection sort works as follows:&#x20;

&#x20;<img src="https://tutorials-image.s3-us-west-2.amazonaws.com/unsorted+array.png" alt="" data-size="line">  Part of unsorted array

&#x20;<img src="https://tutorials-image.s3-us-west-2.amazonaws.com/sorted+array.png" alt="" data-size="line">  Part of sorted array

&#x20;<img src="https://tutorials-image.s3-us-west-2.amazonaws.com/Leftmost+element+in+unsorted+array.png" alt="" data-size="line">  Leftmost element in unsorted array

&#x20;<img src="https://tutorials-image.s3-us-west-2.amazonaws.com/Minimum+element+in+unsorted+array.png" alt="" data-size="line">  Minimum element in unsorted array

![](https://tutorials-image.s3-us-west-2.amazonaws.com/Selection+Sort.png)

This is our initial array A = \[5, 2, 6, 7, 2, 1, 0, 3]

![](https://s3-us-west-2.amazonaws.com/tutorials-image/selection+sort+algorithm.png)

We will swap A\[0] and A\[6] then, make A\[0] part of sorted sub-array.

![](https://s3-us-west-2.amazonaws.com/tutorials-image/selection+sort4.png)

We will swap A\[1] and A\[5] then, make A\[1] part of sorted sub-array.

![](https://s3-us-west-2.amazonaws.com/tutorials-image/selection+sort2.png)

We will swap A\[2] and A\[4] then, make A\[2] part of sorted sub-array.

![](https://s3-us-west-2.amazonaws.com/tutorials-image/selection+sort3.png)

We will swap A\[3] and A\[5] then, make A\[3] part of sorted sub-array.

![](https://s3-us-west-2.amazonaws.com/tutorials-image/selection+sort6.png)

We will swap A\[4] and A\[7] then, make A\[4] part of sorted sub-array.

![](https://s3-us-west-2.amazonaws.com/tutorials-image/selection+sort5.png)

We will swap A\[5] and A\[6] then, make A\[5] part of sorted sub-array.

![](https://s3-us-west-2.amazonaws.com/tutorials-image/selection+sort1.png)

We will swap A\[6] and A\[7] then, make A\[6] part of sorted sub-array.

![](https://s3-us-west-2.amazonaws.com/tutorials-image/final+sorted+arrary+selection+sort.png)

This is the final sorted array.

### Implementation

```cpp
#include <iostream>  
#include <vector>  
  
using namespace std;  

// Time Complexity for Min Index: O(n)
// Space Complexity for Min Index: O(1)
int findMinIndex(vector<int> &A, int start) {  
    int min_index = start;  
  
    ++start;  
    while(start < (int)A.size()) {  
        if(A[start] < A[min_index])  
            min_index = start;  
        ++start;  
    }  
    return min_index;  
}  

// Time Complexity for Selection Sort: O(n^2)
// Space Complexity for Selection Sort: O(1)
void selectionSort(vector<int> &A) {  
    for(int i = 0; i < (int)A.size(); ++i) {  
        int min_index = findMinIndex(A, i);  
  
        if(i != min_index)  
            swap(A[i], A[min_index]);  
    }  
}  
  
int main() {  
    vector<int> A = {5, 2, 6, 7, 2, 1, 0, 3};  
  
    selectionSort(A);  
  
    for(int num : A)  
        cout << num << ' ';  
  
    return 0;  
} 
```

#### Complexity Analysis

Time Complexity : O(n^2)

Space Complexity: O(1)
