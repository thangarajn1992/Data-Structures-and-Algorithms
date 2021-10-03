# In-Place Array Operations

### Introduction

> In programming interviews, the interviewer often expects you to minimize the time and space complexity of your implementation. In-place Array operations help to reduce space complexity, and so are a class of techniques that pretty much everybody encounters regularly in interviews.

So, what _are_ in-place array operations?

The best way of answering this question is to look at an example.

> Given an Array of integers, return an Array where every element at an even-indexed position is squared.

```text
Input: array = [9, -2, -9, 11, 56, -12, -3]
Output: [81, -2, 81, 11, 3136, -12, 9]
Explanation: The numbers at even indexes (0, 2, 4, 6) have been squared, 
whereas the numbers at odd indexes (1, 3, 5) have been left the same.
```

This problem is hopefully very straightforward. Have a quick think about how you would implement it as an algorithm though, possibly jotting down some code on a piece of paper.

Anyway, there are two ways we could approach it. The first is to create a new Array, of the same size as the original. Then, we should copy the odd-indexed elements and square the even-indexed elements, writing them into the new Array.

```java
public int[] squareEven(int[] array, int length) {

  // Check for edge cases.
  if (array == null) {
    return null;
  }

  // Create a resultant Array which would hold the result.
  int result[] = new int[length];

  // Iterate through the original Array.
  for(int i = 0; i < length; i++) {

    // Get the element from slot i of the input Array.
    int element = array[i];

    // If the index is an even number, then we need to square element.
    if (i % 2 == 0) {
      element *= element;
    }

    // Write element into the result Array.
    result[i] = element;
  }

  // Return the result Array.
  return result;
}
```

![](https://leetcode.com/explore/learn/card/fun-with-arrays/511/in-place-operations/Figures/Array_Explore/inplace-1.png)

The above approach, although correct, is an _inefficient_ way of solving the problem. This is because it usesO\(length\)O\(\text{length}\)O\(length\) extra space.

Instead, we could iterate over the original input Array itself, overwriting every even-indexed element with its own square. This way, we won't need that extra space. It is this technique of working directly in the input Array, and _not_ creating a new Array, that we call **in-place**. In-place Array operations are a big deal for programming interviews, where there is a big focus on minimising both time and space complexity of algorithms.

Here's the in-place implementation for our `squareEven(...)` function.

```java
public int[] squareEven(int[] array, int length) {

  // Check for edge cases.
  if (array == null) {
    return array;
  }

  // Iterate through the original array.
  for(int i = 0; i < length; i++) {

    // If the index is an even number, then we need to square the element
    // and replace the original value in the Array.
    if (i % 2 == 0) {
      array[i] *= array[i];
    }
    // Notice how we don't need to do *anything* for the odd indexes? :-)
  }

  // We just return the original array. Some problems on leetcode require you
  // to return it, and other's dont.
  return array;
}
```

An important difference for in-place vs not in-place is that in-place _modifies the input Array_. This means that other functions _can no longer access the original data_, because it has been overwritten.

### A Better Repeated Deletion Algorithm

Let's look at one more example. This time, the result Array is _smaller_ than the input Array! How's this going to work? Let's find out! Here's the problem description:

> Given a _sorted array_, remove the duplicates such that each element appears only once.

```text
Input: array = [1, 1, 2]
Output: [1, 2]
```

```text
Input: array = [0, 0, 1, 1, 1, 2, 2, 3, 3, 4]
Output: [0, 1, 2, 3, 4]
```

A Straight forward approach with in-place will be

```java
class Solution {
    public int removeDuplicates(int[] nums) {
        
        // The initial length is simply the capacity.
        int length = nums.length;
        
        // Assume the last element is always unique.
        // Then for each element, delete it iff it is
        // the same as the one after it. Use our deletion
        // algorithm for deleting from any index.
        for (int i = length - 2; i >= 0; i--) {
            if (nums[i] == nums[i + 1]) {
                // Delete the element at index i, using our standard
                // deletion algorithm we learned.
                for (int j = i + 1; j < length; j++) {
                    nums[j - 1] = nums[j];
                }
                // Reduce the length by 1.
                length--;
            }
        }
        // Return the new length.
        return length;
    }
}
```

This is actually an in-place algorithm, because it doesn't require any extra space—its space complexity is `O(1)`. However, the time complexity's not so flash, at `O(N2)`. This is because of the nested loop.

We want to get the algorithm down to an`O(N)` time complexity.

If we _don't_ try to do this in-place, then it's straightforward. We could simply iterate through the Array, adding all _unique_ elements to a new Array. Seeing as the the input Array is sorted, we can easily identify all unique elements, as they are the first element, and then any element that is _different_ to the one before it.

![](https://leetcode.com/explore/learn/card/fun-with-arrays/511/in-place-operations/Figures/Array_Explore/inplace-2.png)

One potential problem is that we actually don't know how long the result Array needs to be. Remember how that must be decided when the Array is created? The best solution for this problem is to do an initial pass, counting the number of unique elements. Then, we can create the result Array and do a second pass to add the elements into it. Here's the code for this approach.

```java
public int[] copyWithRemovedDuplicates(int[] nums) {
        
  // Check for edge cases.
  if (nums == null || nums.length == 0) {
      return nums;
  }

  // Count how many unique elements are in the Array.
  int uniqueNumbers = 0;
  for (int i = 0; i < nums.length; i++) {
      // An element should be counted as unique if it's the first
      // element in the Array, or is different to the one before it.
      if (i == 0 || nums[i] != nums[i - 1]) {
          uniqueNumbers++;
      }
  }

  // Create a result Array.
  int[] result = new int[uniqueNumbers];

  // Write the unique elements into the result Array.
  int positionInResult = 0;
  for (int i = 0; i < nums.length; i++) {
    // Same condition as in the previous loop. Except this time, we can write
    // each unique number into the result Array instead of just counting them.
      if (i == 0 || nums[i] != nums[i - 1]) {
          result[positionInResult] = nums[i];
          positionInResult++;
      }
  }
  return result;
}
```

Did you notice the fatal flaw with this approach though? It's the wrong return type! We could copy the result array back into the input array... and then return the length... but this is not what the question wants us to do. We want to instead do the deletions with a space complexity of `O(1)` and a time complexity of `O(N)`.

#### Algorithm with O\(1\) Space and O\(N\) Time complexity

Anyway, the algorithm with `O(N)` space is surprisingly similar to the one without. Interestingly, it's simpler though, because it doesn't need to firstly determine the size of the output.

![](https://leetcode.com/explore/learn/card/fun-with-arrays/511/in-place-operations/Figures/Array_Explore/inplace-3.png)

Implementing this requires the use of the **two-pointer technique**. This is where we iterate over the Array in two different places at the same time.

1. Read all the elements like we did before, to identify the duplicates. We call this our `readPointer`.
2. Keep track of the next position in the front to write the next unique element we've found. We call this our `writePointer`.

Here's the algorithm in Java code.

```java
public int removeDuplicates(int[] nums) {
        
  // Check for edge cases.
  if (nums == null) {
      return 0;
  }
  
  // Use the two pointer technique to remove the duplicates in-place.
  // The first element shouldn't be touched; it's already in its correct place.
  int writePointer = 1;
  // Go through each element in the Array.
  for (int readPointer = 1; readPointer < nums.length; readPointer++) {
      // If the current element we're reading is *different* to the previous
      // element...
      if (nums[readPointer] != nums[readPointer - 1]) {
          // Copy it into the next position at the front, tracked by writePointer.
          nums[writePointer] = nums[readPointer];
          // And we need to now increment writePointer, because the next element
          // should be written one space over.
          writePointer++;
      }
  }
  
  // This turns out to be the correct length value.
  return writePointer;
}
```

You're quite possibly surprised that this even works. How are we not overwriting any elements that we haven't yet looked at?! The key thing to notice is that the condition is such that it is _impossible_ for `writePointer` to ever get ahead of the `readPointer`. This means that we would never overwrite a value that we haven't yet read

This was just a very brief introduction to the very versatile and widely used **two-pointer technique**. It is one of the main techniques used for in-place Array algorithms.

#### When to Use In-Place Array Operations <a id="when-to-use-in-place-array-operations"></a>

It's important to know when to use in-place Array operations—they might not always be the way to go.

For example, if we'll need the original array values again later, then we shouldn't be overwriting them. In these cases, it's best to create a copy to work with, or to simply not use in-place techniques. It's important to be **very** careful when working with existing code that somebody else has written. If other code is depending on the original Array to work, then you might completely break the program if you modify that Array!

In-place operations are valuable when appropriate because they reduce the _space complexity_ of an algorithm. Instead of requiring `O(N)` space, we can reduce it down to `O(1)`.

