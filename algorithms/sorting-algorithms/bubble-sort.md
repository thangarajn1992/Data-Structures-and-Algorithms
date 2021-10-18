# Bubble Sort

**Bubble sort**, also referred to as **comparison sort**, is a simple sorting algorithm that repeatedly goes through the list, compares adjacent elements and swaps them if they are in the wrong order. This is the most simplest algorithm and inefficient at the same time. Yet, it is very much necessary to learn about it as it represents the basic foundations of sorting.

**Algorithm**: 

We compare adjacent elements and see if their order is wrong (i.e `a[i] > a[j] for 1 <= i < j <= size of array`; if array is to be in ascending order, and vice-versa). If yes, then swap them.

**Explanation**:

* Let us say, we have an array of length `n`. To sort this array we do the above step (swapping) for `n - 1` passes.
* In simple terms, **first, the largest element goes at its extreme right place** then, second largest to the last by one place, and so on. In the ith pass, the ith largest element goes at its right place in the array by swapping.
* In mathematical terms, in `ith` pass, at least one element from `(n - i + 1)` elements from start will go at its right place. That element will be the ith `(for 1 <= i <= n - 1)` largest element of the array. Because in the `ith` pass of the array, in the `jth` iteration `(for 1 <= j <= n - i)`, we are checking `if a[j] > a[j + 1]`, and `a[j]` will always be greater than `a[j + 1]` when it is the largest element in range `[1, n - i + 1]`. Now we will swap it. This will continue until `ith` largest element is at the `(n - i + 1)`th position of the array.

#### Example:

Consider the following array: Arr=`14, 33, 27, 35, 10`. We need to sort this array using bubble sort algorithm.

![Initial array](https://tutorials-image.s3-us-west-2.amazonaws.com/unsorrted+array.png)

**First Pass**:

* We proceed with the first and second element i.e., Arr\[0] and Arr\[1]. Check if `14 > 33` which is false. So, **no swapping** happens and the array remains the same.

![](https://tutorials-image.s3-us-west-2.amazonaws.com/unsorrted+array.png)

* We proceed with the second and third element i.e., Arr\[1] and Arr\[2]. Check if `33 > 27` which is true. So, we swap Arr\[1] and Arr\[2].

![](https://tutorials-image.s3-us-west-2.amazonaws.com/bubble+sort.png)

\
Thus the array becomes:\


![](https://tutorials-image.s3-us-west-2.amazonaws.com/bubble+sort+1.png)

* We proceed with the third and fourth element i.e., Arr\[2] and Arr\[3]. Check if `33 > 35` which is false. So, no swapping happens and the array remains the same.

![](https://tutorials-image.s3-us-west-2.amazonaws.com/bubble+sort+1.png)

* We proceed with the fourth and fifth element i.e., Arr\[3] and Arr\[4]. Check if `35 > 10` which is true. So, we swap Arr\[3] and Arr\[4].

![](https://tutorials-image.s3-us-west-2.amazonaws.com/bubble+sort+3.png)

Thus, after swapping the array becomes:\


![](https://tutorials-image.s3-us-west-2.amazonaws.com/bubble+sort+4.png)

Thus, marks the end of the first pass, where the **Largest element reaches its final(last) position.**

**Second Pass**:

* We proceed with the first and second element i.e., Arr\[0] and Arr\[1]. Check if `14 > 27` which is false. So, no swapping happens and the array remains the same.

\


![](https://tutorials-image.s3-us-west-2.amazonaws.com/bubble+sort+4.png)

We now proceed with the second and third element i.e., Arr\[1] and Arr\[2]. Check if 27 > 33 which is false. So, no swapping happens and the **array remains the same.**

* We now proceed with the third and fourth element i.e., Arr\[2] and Arr\[3]. Check if `33 > 10` which is true. So, we swap Arr\[2] and Arr\[3].

![](https://tutorials-image.s3-us-west-2.amazonaws.com/bubble+sort+5.png)

Now, the array becomes\


![](https://tutorials-image.s3-us-west-2.amazonaws.com/bubble+sort+6.png)

Thus marks the end of second pass where the **second largest element in the array has occupied its correct position.**

**Third Pass:**\
After the third pass, the **third largest element will be at the third last position** in the array.

![enter image description here](https://i.pinimg.com/564x/9f/e7/0c/9fe70c83b7617d894550fac611f7f85a.jpg)

**i-th Pass:**\
After the ith pass, the **ith largest element will be at the ith last position** in the array.

\
**n-th Pass:**\
After the nth pass, **the nth largest element(smallest element) will be at nth last position(1st position)** in the array, where ‘n’ is the size of the array.

**After doing all the passes, we can easily see the array will be sorted.**\
Thus, the sorted array will look like this:

![](https://tutorials-image.s3-us-west-2.amazonaws.com/final+sorted+array+using+bubble+sort.png)

### Implementation Bubble Sort

```cpp
#include <iostream>
#include <vector>
 
using namespace std;
 
void BubbleSort (vector<int> &arr, int n)
{
   for (int i = 0; i < n - 1; ++i)
   { 
      bool swapped = false;
      for (int j = 0; j < n - i - 1; ++j)
      {
         //check if adjacent element is not in order
         if (arr[j] > arr[j+1]) 
         {
            swap(arr[j], arr[j + 1]);
            swapped = true;
         }
      }
      // Value at n-i-1 will be maximum of all the values below this index.
      if(!swapped) // Array is sorted already 
         break;
   }
} 

int main()
{
   vector<int> arr = {5, 6, 2, 6, 9, 0, -1};
   int n = 7;
 
   BubbleSort(arr, n);
 
   // Display the sorted data.
   cout << "\nSorted Data: ";
   for (i = 0; i < n; i++)
        cout << arr[i] << “ “;
 
   return 0;
}
```

### Complexity Analysis

**Time Complexity of Bubble sort**

* **Best case scenario:** The best case scenario occurs when the array is already sorted. In this case, no swapping will happen in the first iteration (The `swapped` variable will be false). So, when this happens, we break from the loop after the very first iteration. Hence, time complexity in the best case scenario is `O(n)` because it has to traverse through all the elements once.
*   **Worst case and Average case scenario:** In Bubble Sort, `n-1` comparisons are done in the 1st pass, `n-2` in 2nd pass, `n-3` in 3rd pass and so on. So, the total number of comparisons will be:

    ```
    Sum = (n-1) + (n-2) + (n-3) + ..... + 3 + 2 + 1 
    Sum = n(n-1)/2
    ```

     Hence, the time complexity is of the order **n^2** or **O(n^2)**.

**Space Complexity of Bubble sort**

The space complexity for the algorithm is **O(1)**, because only a single additional memory space is required i.e. for temporary variable used for swapping.
