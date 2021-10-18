# Merge Sort

Merge sort is one of the most efficient sorting algorithms. It works on the principle of Divide and Conquer. Merge sort repeatedly breaks down a list into several sub-lists until each sub-list consists of a single element and merging those sub-lists in a manner that results into a sorted list.

#### Top-Down Merge Sort

The top-down merge sort approach is the methodology which uses recursion mechanism. It starts at the Top and proceeds downwards, with each recursive turn asking the same question such as “What is required to be done to sort the array?” and having the answer as, “split the array into two, make a recursive call, and merge the results.”, until one gets to the bottom of the array-tree.

Example: Let us consider an example to understand the approach better.

1. Divide the unsorted list into n sub-lists, each comprising 1 element (a list of 1 element is supposed sorted).

![Working of Merge Sort](https://s3-us-west-2.amazonaws.com/tutorials-image/merge+sort+working.png)

Top-down Implementation

1. Repeatedly merge sub-lists to produce newly sorted sub-lists until there is only 1 sub-list remaining. This will be the sorted list.

#### Merging of two lists done as follows:

The first element of both lists is compared. If sorting in ascending order, the smaller element among two becomes a new element of the sorted list. This procedure is repeated until both the smaller sub-lists are empty and the newly combined sub-list covers all the elements of both the sub-lists.

![Merging Two Lists](https://s3-us-west-2.amazonaws.com/tutorials-image/merging+of+two+lists.png)

#### Bottom-up Merge Sort Algorithm:

The Bottom-Up merge sort approach uses iterative methodology. It starts with the “single-element” array, and combines two adjacent elements and also sorting the two at the same time. The combined-sorted arrays are again combined and sorted with each other until one single unit of sorted array is achieved.

Example: Let us understand the concept with the following example.

Iteration (1)\


![Bottom-up Iteration 1](https://s3-us-west-2.amazonaws.com/tutorials-image/Bottom-Up+Merge+Sort.png)



Iteration (2)\


![Bottom-up Iteration 2](https://s3-us-west-2.amazonaws.com/tutorials-image/bottom+up+Iteration+2.png)

Iteration (3)\


![Bottom-up implementation](https://s3-us-west-2.amazonaws.com/tutorials-image/bottom+up+implementation.png)

Thus the entire array has been sorted and merged.

### Top Down Approach Implementation

```cpp
// example of merge sort in C/C++
// merge function take two intervals
// one from start to mid
// second from mid+1, to end
// and merge them in sorted order

void merge(int *Arr, int start, int mid, int end) {
	// create a temp array
	int temp[end - start + 1];

	// crawlers for both intervals and for temp
	int i = start, j = mid+1, k = 0;

	// traverse both arrays and in each iteration add smaller of both elements in temp 
	while(i <= mid && j <= end) {
		if(Arr[i] <= Arr[j]) {
			temp[k++] = Arr[i++];
		}
		else {
			temp[k++] = Arr[j++];
		}
	}

	// add elements left in the first interval 
	while(i <= mid) {
		temp[k++] = Arr[i++];
	}

	// add elements left in the second interval 
	while(j <= end) {
		temp[k++] = Arr[j++];
	}

	// copy temp to original interval
	for(i = start; i <= end; i++) {
		Arr[i] = temp[i - start]
	}
}

// Arr is an array of integer type
// start and end are the starting and ending index of current interval of Arr

void mergeSort(int *Arr, int start, int end) {

	if(start < end) {
		int mid = (start + end) / 2;
		mergeSort(Arr, start, mid);
		mergeSort(Arr, mid+1, end);
		merge(Arr, start, mid, end);
	}
}
```
