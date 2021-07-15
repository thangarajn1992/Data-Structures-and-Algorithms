# Insertion Sort

Insertion sort is the sorting mechanism where the sorted array is built having one item at a time. The array elements are compared with each other sequentially and then arranged simultaneously in some particular order. The analogy can be understood from the style we arrange a deck of cards. This sort works on the principle of inserting an element at a particular position, hence the name Insertion Sort.

#### Algorithm

1. The first step involves the comparison of the element in question with its adjacent element.
2. And if at every comparison reveals that the element in question can be inserted at a particular position, then space is created for it by shifting the other elements one position to the right and inserting the element at the suitable position.
3. The above procedure is repeated until all the element in the array is at their apt position.

Consider the following array: 25, 17, 31, 13, 2

**First Iteration**: Compare 17 with 25. The comparison shows 17&lt; 25. Hence swap 17 and 25.

The array now looks like:

**17, 25, 31, 13, 2**

First Iteration![](https://s3-us-west-2.amazonaws.com/tutorials-image/first+iteration.png)

**Second Iteration**:  Now hold on to the third element \(31\) and compare with the ones preceding it.

Since 31&gt; 25, no swapping takes place.

Also, 31&gt; 17, no swapping takes place and 31 remains at its position.

The array after the Second iteration looks like:

**17, 25, 31, 13, 2**

  
Second Iteration![](https://s3-us-west-2.amazonaws.com/tutorials-image/second+iteration.png)

**Third Iteration**: Start the following Iteration with the fourth element \(13\), and compare it with its preceding elements.

Since 13&lt; 31, we swap the two.

Array now becomes: 17, 25, 13, 31, 2.

But there still exist elements that we haven’t yet compared with 13. Now the comparison takes place between 25 and 13. Since, 13 &lt; 25, we swap the two.

The array becomes **17, 13, 25, 31, 2**.

The last comparison for the iteration is now between 17 and 13. Since 13 &lt; 17, we swap the two.

The array now becomes **13, 17, 25, 31, 2**.

Third Iteration![](https://s3-us-west-2.amazonaws.com/tutorials-image/third+iteration.png)

![insertion sort working](https://s3-us-west-2.amazonaws.com/tutorials-image/working+of+insertion+sort.png)

**Fourth Iteration**: The last iteration calls for the comparison of the last element \(2\), with all the preceding elements and make the appropriate swapping between elements.

Since, 2&lt; 31. Swap 2 and 31.

Array now becomes: 13, 17, 25, 2, 31.

Compare 2 with 25, 17, 13.

Since, 2&lt; 25. Swap 25 and 2.

**13, 17, 2, 25, 31**.

Compare 2 with 17 and 13.

Since, 2&lt;17. Swap 2 and 17.

Array now becomes:

**13, 2, 17, 25, 31**.

The last comparison for the Iteration is to compare 2 with 13.

Since 2&lt; 13. Swap 2 and 13.

The array now becomes:

**2, 13, 17, 25, 31**.

This is the final array after all the corresponding iterations and swapping of elements.

Fourth Iteration![](https://s3-us-west-2.amazonaws.com/tutorials-image/insertion-sort.png)

### Implementation

```cpp
#include <stdlib.h>
#include <iostream>

using namespace std;

void insertionSort(int arr[], int length) 
{
    for (int i = 1; i < length; i++) 
    {
        key = arr[i];
        int j = i - 1;
        
        while(j >= 0 && arr[j] >key) 
        {
            arr[j+1] = arr[j];
            j--;
        }
        arr[j +1] = key; 
    }
    
    cout << "Sorted Array: ";
    // print the sorted array
    printArray(arr, length);
}

// function to print the given array 
void printArray(int array[], int size)
{ 
    for (int j = 0; j < size; j++)
        cout <<" "<< array[j];
    cout << endl;
}

// main function
int main() 
{
    int array[6] = {5, 1, 6, 2, 4, 3};
    // calling insertion sort function to sort the array
    insertionSort(array, 6);
    return 0;
}


```

#### Time Complexity Analysis: <a id="time-complexity"></a>

Even though insertion sort is efficient, still, if we provide an already sorted array to the insertion sort algorithm, it will still execute the outer for loop, thereby requiring n steps to sort an already sorted array of n elements, which makes its best case time complexity a linear function of n.

Wherein for an unsorted array, it takes for an element to compare with all the other elements which mean every n element compared with all other n elements. Thus, making it for `n x n, i.e., n^2` comparisons. One can also take a look at other sorting algorithms such as _Merge sort, Quick Sort, Selection Sort_, etc. and understand their complexities.

**Worst Case Time Complexity \[ Big-O \]: O\(n^2\)**

**Best Case Time Complexity \[Big-omega\]: O\(n\)**

**Average Time Complexity \[Big-theta\]: O\(n^2\)**

