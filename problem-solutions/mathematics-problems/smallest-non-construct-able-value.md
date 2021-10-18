# Smallest Non Constructable Value or Largest Constructable Value

### Sources

* Elements of Programming Interview
* [Leetcode 1798](smallest-non-construct-able-value.md)

### Problem Statement

Write a program that takes an array of positive integers and returns the smallest number which is not a sum of any subset of elements of the array

### Algorithm

Suppose a collection of numbers can produce every value up to and including `v`, but not `v+1`. Now consider the effect of adding a new element u to the collection.

If `u <= v+1`, we can still produce every value up to and including `v+u` and we cannot reproduce `v+u+1`.

If `u > v+1`, then even after adding u to the collection, we cannot produce `V+1`.

Also, sorting  array allows us to stop which we reach a value that is too large to help, since all subsequent values are at least as large as that value. Specifically, let `M[i-1]` be the maximum construct-able amount from the first `i `elements of the sorted array.

If the next array element `x > M[i-1] + 1`, then `M[i-1]` is still the maximum construct-able amount.

Otherwise, `M[i] = M[i-1] + x`

### Solution

For smallest non-constructible value and maximum constructible value

```cpp
/* maximum constructible value + 1 = smallest non-constructible value */
int SmallestNonConstructibleValue(vector<int> nums) {
    sort(nums.begin(), nums.end());
    int max_constructible_value = 0;
    for(int num : nums)
    {
        if( num > max_constructible_value + 1)
            break;
        max_constructible_value += num;
    }
    return max_constructible_value + 1;
}
```
