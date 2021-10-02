# Basic Array Operations

Now that we have a fairly good understanding of what an Array actually is, and how it is stored inside the computer's physical memory, the next important thing to look at is all the operations that Arrays support. An Array is a data structure, which means that it stores data in a specific format and supports certain operations on the data it stores. Consider the DVD inventory management software from the introduction section. Let's look at some operations you might want to perform using this software:

* **Insert** a new DVD into the collection at a specific location.
* **Delete** a DVD from the existing collection if it doesn't make sense to keep it in the inventory anymore.
* **Search** for a particular DVD in the collection. This is one of the most commonly executed operation on our collection, because our inventory management software would be used hundreds of times a day to look for a particular DVD asked for by the user.

In this section, we'll be looking at the three basic operations that are supported by almost every data structure; **insertion**, **deletion**, and **search**.

### Array Insertions

> In the previous chapter, we looked at how to write elements to an Array. There is a lot more to inserting elements though, as we're about to see!

Inserting a new element into an Array can take many forms:

1. Inserting a new element at the end of the Array.
2. Inserting a new element at the beginning of the Array.
3. Inserting a new element at any given index inside the Array.

#### Inserting at the End of an Array <a id="inserting-at-the-end-of-an-array"></a>

At any point in time, we know the index of the last element of the Array, as we've kept track of it in our `length` variable. All we need to do for inserting an element at the end is to assign the new element to one index past the current last element.

![](https://leetcode.com/explore/learn/card/fun-with-arrays/525/inserting-items-into-an-array/Figures/Array_Explore/Array_Insertion_1.png)

This is pretty much the same as we've already seen. Here's the code to make a new Array that can hold up to `6` items, and then add items into the first `3` three indexes.

```java
// Declare an integer array of 6 elements
int intArray = new int[6];
int length = 0;

// Add 3 elements to the Array
for (int i = 0; i < 3; i++) {
    intArray[length] = i;
    length++;
}
```

Let's define a function, `printArray`, to help us visualize what's happening.

```java
for (int i = 0; i < intArray.length; i++) {
    System.out.println("Index " + i + " contains " + intArray[i]);
}
```

If we run our `printArray` function, we'll get the following output.

```text
Index 0 contains 0.
Index 1 contains 1.
Index 2 contains 2.
Index 3 contains 0.
Index 4 contains 0.
Index 5 contains 0.
```

Notice how indexes `3`, `4`, and `5` all contain `0`? This is because Java fills unused `int` Array slots with `0`s.

Let's now add a 4th element. We'll add the number 10.

```java
// Insert a new element at the end of the Array. Again,
// it's important to ensure that there is enough space
// in the array for inserting a new element.
intArray[length] = 10;
length++;
```

Notice how we also incremented the length? This is very important, next time when we add another element, we'll accidentally overwrite the one we just added!

Running `printArray` again, we'll get the following:

```text
Index 0 contains 0.
Index 1 contains 1.
Index 2 contains 2.
Index 3 contains 10.
Index 4 contains 0.
Index 5 contains 0.
```

#### Inserting at the Start of an Array <a id="inserting-at-the-start-of-an-array"></a>

To insert an element at the start of an Array, we'll need to shift all other elements in the Array to the right by one index to create space for the new element. This is a very costly operation, since each of the existing elements has to be shifted one step to the right. The need to shift everything implies that this is not a constant time operation. In fact, the time taken for insertion at the beginning of an Array will be proportional to the length of the Array. In terms of time complexity analysis, this is a linear time complexity:`O(N)` , where `N` is the length of the Array.

![](https://leetcode.com/explore/learn/card/fun-with-arrays/525/inserting-items-into-an-array/Figures/Array_Explore/Array_Insertion_2.png)

Here's what this looks like in code.

```java
// First, we will have to create space for a new element.
// We do that by shifting each element one index to the right.
// This will firstly move the element at index 3, then 2, then 1, then finally 0.
// We need to go backwards to avoid overwriting any elements.
for (int i = 3; i >= 0; i--) {
    intArray[i + 1] = intArray[i];
}

// Now that we have created space for the new element,
// we can insert it at the beginning.
intArray[0] = 20;
```

And here's the result of running `printArray`.

```text
Index 0 contains 20.
Index 1 contains 0.
Index 2 contains 1.
Index 3 contains 2.
Index 4 contains 10.
Index 5 contains 0.
```

#### Inserting Anywhere in the Array <a id="inserting-anywhere-in-the-array"></a>

Similarly, for inserting at any given index, we first need to shift all the elements from that index till one position to the right. Once the space is created for the new element, we proceed with the insertion. If you think about it, insertion at the beginning is basically a special case of inserting an element at a given index—in that case, the given index was `0`.

![](https://leetcode.com/explore/learn/card/fun-with-arrays/525/inserting-items-into-an-array/Figures/Array_Explore/Array_Insertion_3.png)

Again, this is also a costly operation since we could _potentially_ have to shift almost all the other elements to the right before actually inserting the new element. As your saw above, shifting lots of elements one place to the right adds to the time complexity of the insertion task.

Here's what it looks like in code.

```java
// Say we want to insert the element at index 2.
// First, we will have to create space for the new element.
for (int i = 4; i >= 2; i--)
{
    // Shift each element one position to the right.
    intArray[i + 1] = intArray[i];
}

// Now that we have created space for the new element,
// we can insert it at the required index.
intArray[2] = 30;
```

And here's the result of running `printArray`.

```text
Index 0 contains 20.
Index 1 contains 0.
Index 2 contains 30.
Index 3 contains 1.
Index 4 contains 2.
Index 5 contains 10.
```

Does that all sound good? The main thing to be careful of is remembering that `array.length` gives you the _total capacity_ of the Array. If you want to know the last _used_ slot, you'll need to keep track of this yourself using a `length` variable. Other than that, just be careful to read any elements you want to keep, before you overwrite them!

### Array Deletions

> Now that we know how insertion works, it's time to look at its complement—deletion!

Deletion in an Array works in a very similar manner to insertion, and has the same three different cases:

1. Deleting the last element of the Array.
2. Deleting the first element of the Array.
3. Deletion at any given index.

#### Deleting From the End of an Array <a id="deleting-from-the-end-of-an-array"></a>

Deletion at the end of an Array is similar to people standing in a line, also known as a `queue`. The person who most recently joined the queue \(at the end\) can leave at any time without disturbing the rest of the queue. Deleting from the end of an Array is the least time consuming of the three cases. Recall that insertion at the end of an Array was also the least time-consuming case for insertion.

![](https://leetcode.com/explore/learn/card/fun-with-arrays/526/deleting-items-from-an-array/Figures/Array_Explore/Array_Deletion_1.png)

So, how does this work in code? Before we look at this, let's quickly remind ourselves what the `length` of an Array means. Here is some code that creates an Array with room for 10 elements, and then adds elements into the first 6 indexes of it.

```java
// Declare an integer array of 10 elements.
int[] intArray = new int[10];

// The array currently contains 0 elements
int length = 0;

// Add elements at the first 6 indexes of the Array.
for(int i = 0; i < 6; i++) {
    intArray[length] = i;
    length++;
}
```

Notice the `length` variable. Essentially, this variable keeps track of the next index that is free for inserting a new element. This is always the same value as the overall length of the Array. Note that when we declare an Array of a certain size, we simply fix the maximum number of elements it could contain. Initially, the Array doesn't contain anything. Thus, when we add new elements, we also increment the `length` variable accordingly.

Anyway, here's the code for deleting the last element of an Array.

```cpp
// Deletion from the end is as simple as reducing the length
// of the array by 1.
length--;
```

Remember how insertion we were using this `printArray` function?

```java
for (int i = 0; i < length; i++) {
    System.out.println("Index " + i + " contains " + intArray[i]);
}
```

Run this, and you'll get the following before the deletion:

```text
Index 0 contains 0.
Index 1 contains 1.
Index 2 contains 2.
Index 3 contains 3.
Index 4 contains 4.
Index 5 contains 5.
```

And the following after:

```text
Index 0 contains 0.
Index 1 contains 1.
Index 2 contains 2.
Index 3 contains 3.
Index 4 contains 4.
```

Yup, that's it! Even though we call it a deletion, its not like we actually freed up the space for a new element, right? This is because **we don't actually need to free up any space**. Simply overwriting the value at a certain index deletes the element at that index. Seeing as the length variable in our examples tells us the next index where we can insert a new element, reducing it by one ensures the next new element is written over the deleted one. This also indicates that the Array now contains one less element, which is exactly what we want programmatically.

#### Deleting From the Start of an Array <a id="deleting-from-the-start-of-an-array"></a>

Next comes the costliest of all deletion operations for an Array—deleting the first element. If we want to delete the first element of the Array, that will create a vacant spot at the `0th` index. To fill that spot, we will shift the element at index `1` one step to the left. Going by the ripple effect, every element all the way to the last one will be shifted one place to the left. This shift of elements takesO\(N\)O\(N\)O\(N\) time, whereNNN is the number of elements in the Array.

![](https://leetcode.com/explore/learn/card/fun-with-arrays/526/deleting-items-from-an-array/Figures/Array_Explore/Array_Deletion_2.png)

Here is how deleting the first element looks in code.

```java
// Starting at index 1, we shift each element one position
// to the left.
for (int i = 1; i < length; i++) {
    // Shift each element one position to the left
    int_array[i - 1] = int_array[i];
}

// Note that it's important to reduce the length of the array by 1.
// Otherwise, we'll lose consistency of the size. This length
// variable is the only thing controlling where new elements might
// get added.
length--;
```

Starting from index `0`, we'll move every element one position to its left, effectively "deleting" the element at index `0`. We also need to reduce `length` by `1` so that the next new element is inserted in the correct position.

And here's the output we'll get, with our updated `printArray` function.

```text
Index 0 contains 1.
Index 1 contains 2.
Index 2 contains 3.
Index 3 contains 4.
```

#### Deleting From Anywhere in the Array <a id="deleting-from-anywhere-in-the-array"></a>

For deletion at any given index, the empty space created by the deleted item will need to be filled. Each of the elements to the _right_ of the index we're deleting at will get shifted to the _left_ by one. Deleting the first element of an Array is a special case of deletion at a given index, where the index is `0`. This shift of elements takes `O(K)` time where `K` is the number of elements to the right of the given index. Since _potentially_ `K = N`, we say that the time complexity of this operation is also `O(N)`

![](https://leetcode.com/explore/learn/card/fun-with-arrays/526/deleting-items-from-an-array/Figures/Array_Explore/Array_Deletion_3.png)

Here is the code to delete the element at index 1. To do this, we'll need to move over the elements after it in the Array.

```java
// Say we want to delete the element at index 1
for (int i = 2; i < length; i++) {
    // Shift each element one position to the left
    int_array[i - 1] = int_array[i];
}

// Again, the length needs to be consistent with the current
// state of the array.
length--;
```

Notice that this works exactly like deleting the first element, except that we don't touch the elements that are at _lower_ indexes than the element we're deleting.

Here is the output from the `printArray` function.

```text
Index 0 contains 1.
Index 1 contains 3.
Index 2 contains 4.
```

Did that all make sense?



