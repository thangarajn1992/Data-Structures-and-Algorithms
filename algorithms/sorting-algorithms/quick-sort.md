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

