# 2D-Arrays

Two-Dimensional \(2D\) arrays are simply a matrix. We have an array of array of same types. Eg: array of array of integers.

#### Declaring 2D Array

`Datatype variable-name[row-size][col-size]   Eg: m[5][100]`

**Memory Orientation of 2D Array**

 ****m\[0\] is one 1D array with 100 elements. 5 such array of 100 elements in 2D array. In memory, `m[0][0]...m[0][99]` and then we will have `m[1][0]...m[1][99]` and so on. Once we declare this array, we will have contiguous memory allocated for this array to hold 500 integers.

**Pointer to 2D Array**

`int *p = m`     =&gt; Gives pointer to base address of first element \(works in 1D array\). So this will throw compilation error. So we need to do as

`int *p[100] = m`   =&gt; Gives pointer to first 1D array of size 100.

`*(m+1)` will add the size of one array of 100 elements, So after this the pointer will be at 2nd 1D array `&m[1][0]`

`*(m+1)+2`  equivalent to `&m[1][0] + 2 => &m[1][2]`

`*(*(m+1)) equivalent to value at m[1][0]`

`*(*m + 1) equivalent to value at m[0][1]`

`m[i][j] = *(m[i] + j) = *(*(m+i)+j)`

   



