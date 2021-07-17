# Quick Sort

The algorithm was developed by a British computer scientist Tony Hoare in 1959. The name "Quick Sort" comes from the fact that, quick sort is capable of sorting a list of data elements significantly faster \(twice or thrice faster\) than any of the common sorting algorithms. It is one of the most efficient sorting algorithms and is based on the splitting of an array \(partition\) into smaller ones and swapping \(exchange\) based on the comparison with 'pivot' element selected. Due to this, quick sort is also called as "**Partition Exchange**" sort. Like Merge sort, Quick sort also falls into the category of divide and conquer approach of problem-solving methodology.

### Applications

Before diving into any algorithm, its very much necessary for us to understand what are the real world applications of it. Quick sort provides a fast and methodical approach to sort any lists of things. Following are some of the applications where quick sort is used.

* _**Commercial computing:**_ Used in various government and private organizations for the purpose of sorting various data like sorting of accounts/profiles by name or any given ID, sorting transactions by time or locations, sorting files by name or date of creation etc.
* _**Numerical computations:**_ Most of the efficiently developed algorithms use priority queues and in turn sorting to achieve accuracy in all the calculations.
* _**Information search:**_ Sorting algorithms aid in better search of information and what faster way exists than to achieve sorting using quick sort.

Basically, quick sort is used everywhere for faster results and in the cases where there are space constraints.

### Algorithm

Taking the analogical view in perspective, consider a situation where one had to sort the papers bearing the names of the students, by name from A-Z. One might use the approach as follows:

1. Select any splitting value, say L. The splitting value is also known as **Pivot**.
2. Divide the stack of papers into two. A-L and M-Z. It is not necessary that the piles should be equal.
3. Repeat the above two steps with the A-L pile, splitting it into its significant two halves. And M-Z pile, split into its halves. The process is repeated until the piles are small enough to be sorted easily.
4. Ultimately, the smaller piles can be placed one on top of the other to produce a fully sorted and ordered set of papers.
5. The approach used here is **reduction** at each split to get to the single-element array.
6. At every split, the pile was divided and then the same approach was used for the smaller piles by using the method of recursion.

Technically, quick sort follows the below steps:  
**Step 1** − Make any element as pivot  
**Step 2** − Partition the array on the basis of pivot  
**Step 3** − Apply quick sort on left partition recursively

![](../../.gitbook/assets/image%20%2824%29.png)

### Implemetation

```cpp
#include<iostream>
#include<cstdlib>
 
using namespace std;
 
// Swapping two values.
void swap(int *a, int *b)
{
		int temp; 
		temp = *a;
		*a = *b;
		*b = temp;
}
 
// Partitioning the array on the basis of values at high as pivot value.
int Partition(int a[], int low, int high)
{
		int pivot, index, i;
		index = low;
		pivot = high;
 
		// Getting index of the pivot.
		for(i = low; i < high; i++)
		{
				if(a[i] < a[pivot])
				{
						swap(&a[i], &a[index]);
						index++;
				}
		}
		// Swapping value at high and at the index obtained.
		swap(&a[pivot], &a[index]);
		return index;
	}
 
// Random selection of pivot.
int RandomPivotPartition(int a[], int low, int high)
{
		int pivot_index, n, temp;
		n = rand();
		// Randomizing the pivot value in the given subpart of array.
		pivot_index = low + n % (high - low + 1);
 
		// Swapping pivot value from high, so pivot value will be taken as a pivot 
		// while partitioning.
		swap(&a[high], &a[pivot_index]);
 
		return Partition(a, low, high);
}
 
int QuickSort(int a[], int low, int high)
{
		int pindex;
		if(low < high)
		{
				// Partitioning array using randomized pivot.
				pindex = RandomPivotPartition(a, low, high);
				// Recursively implementing QuickSort.
				QuickSort(a, low, pindex-1);
				QuickSort(a, pindex+1, high);
		}
		return 0;
}
 
int main()
{
	int n, i;
	cout<<"\nEnter the number of data elements to be sorted: ";
	cin>>n;
 
	int arr[n];
	for(i = 0; i < n; i++)
	{
		cout<<"Enter element "<<i+1<<": ";
		cin>>arr[i];
	}
 
	QuickSort(arr, 0, n-1);
 
	// Printing the sorted data.
	cout<<"\nSorted Data ";
	for (i = 0; i < n; i++)
        	cout<<"->"<<arr[i];
 
	return 0;
}
```

#### Complexity Analysis <a id="h827ske1ht0ea2fcemd1dxxl7u1ndu40q"></a>

**Time Complexity of Quick sort**

* **Best case scenario:** The best case scenario occurs when the partitions are as evenly balanced as possible, i.e their sizes on either side of the pivot element are either are equal or are have size difference of 1 of each other.

  * Case 1: The case when sizes of sub-list on either side of pivot becomes equal occurs when the subarray has an odd number of elements and the pivot is right in the middle after partitioning. Each partition will have `(n-1)/2` elements.
  * Case 2: The size difference of 1 between the two sub-lists on either side of pivot happens if the sub-array has an even number, `n`, of elements. One partition will have `n/2` elements with the other having `(n/2)-1`.

  In either of these cases, each partition will have at most `n/2` elements, and the tree representation of the sub-problem sizes will be as below:

![Best Case](https://s3.ap-south-1.amazonaws.com/myinterviewtrainer-domestic/public_assets/assets/000/000/285/original/quick-sort.png?1617203748)

The best-case complexity of the quick sort algorithm is O\(n log\(n\)\)

* **Worst case scenario:** This happens when we encounter the most unbalanced partitions possible, then the original call takes `n` time, the recursive call on `n-1` elements will take `(n-1)` time, the recursive call on `(n-2)` elements will take `(n-2)` time, and so on. The worst case time complexity of Quick Sort would be **O\(n2\)**.

![Quick Sort - Worst Case](https://i.pinimg.com/564x/49/3c/2e/493c2ea77dc9ea4ce978b485b8b46bae.jpg)

**Space Complexity of Quick sort**

The space complexity is calculated based on the space used in the recursion stack. The worst case space used will be `O(n)` . The average case space used will be of the order `O(log n)`. The worst case space complexity becomes `O(n)`, when the algorithm encounters its worst case where for getting a sorted list, we need to make `n` recursive calls.

