# Space Complexity

Space Complexity is a measure of how efficient your code is in terms of memory used.

Additional space/memory is measured in terms of the largest memory use by the program when it runs. i.e if you allocated O\(N\) memory, and later freed it, it doesn't become O\(1\), it is still O\(N\).

Example of O\(N\) space complexity

```cpp
vector<int> V;
for(int i = 0; i < N; i++)
    V.push_back(i);
```



