# Utopian Tree

### Source

* [Hacker Rank](https://www.hackerrank.com/challenges/utopian-tree/problem)

### Problem Statement

The Utopian Tree goes through _2_ cycles of growth every year. Each spring, it _doubles_ in height. Each summer, its height increases by _1_ meter.

A Utopian Tree sapling with a height of _1_ meter is planted at the onset of spring. How tall will the tree be after n growth cycles?

For example, if the number of growth cycles is n = 5, the calculations are as follows:

```text
Period  Height
0          1
1          2
2          3
3          6
4          7
5          14
```

**Function Description**

utopianTree has the following parameter\(s\):

* _int n_: the number of growth cycles to simulate

**Returns**

* _int:_ the height of the tree after the given number of cycles

**Constraints**

0 &lt;= n &lt;= 60

**Sample Inputs**

```text
0
1
4
```

**Sample Outputs**

```text
1
2
7
```

### Solution

```cpp
int utopianTree(int n) {
    int height = 0;
    int period = 0;
    while(period <= n)
    {
        period++;
        if(period % 2 == 0)
            height *= 2;
        else {
            height += 1;
        }
    }
    return height;
}
```

