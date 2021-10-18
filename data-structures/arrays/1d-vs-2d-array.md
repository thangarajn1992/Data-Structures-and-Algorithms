# 1D vs 2D Array

##  1D Array

Array is a collection of same types. 

#### Why we need Array?

Consider you want to find total marks of 100 students in a class. We need to define 100 variables for each student and perform addition as below

```
int m1, m2, m3, m4, m5, m6.....m100;
sum = m1 + m2 + m3 + m4 .... + m100;
```

As you can see this is very tedious and not scalable. This is where array comes as a savior. With arrays, we have its size as 100 and store all student's mark and finding their sum in a single simple loop as below

```cpp
int m[100];
for(int i = 0; i < 100; i++)
    sum += m[i];
```

The array elements are stored contiguous memory. First element has array index of '0'. 

`m`points to the location of the first element of the array. But this is not a pointer variable, so we cannot do increment/decrement like `m++`.  `*m` will be value of the first element

`m+1` will point to the second element. i.e incrementing m will increase its location by the size of the type which array holds. \[ Here it is int, so it will be incremented by 4 bytes ]

#### Declaration of Array

`datatype variablename[array_size]; Eg: int m[100];`

 **Access/Modify element of Array**

To Access any element, we can use `Base + offset`, hence it is O(1) for accessing or modifying. Eg: To access 4th  element, we can use either `m[3] or *(m+3)`

## 2D Array

Two-Dimensional (2D) arrays are simply a matrix. We have an array of array of same types. Eg: array of array of integers.

#### Declaring 2D Array

`Datatype variable-name[row-size][col-size]   Eg: m[5][100]`

**Memory Orientation of 2D Array**

** **m\[0] is one 1D array with 100 elements. 5 such array of 100 elements in 2D array. In memory, `m[0][0]...m[0][99]` and then we will have `m[1][0]...m[1][99]` and so on. Once we declare this array, we will have contiguous memory allocated for this array to hold 500 integers.

**Pointer to 2D Array**

`int *p = m  `   => Gives pointer to base address of first element (works in 1D array). So this will throw compilation error. So we need to do as

`int *p[100] = m`   => Gives pointer to first 1D array of size 100.

`*(m+1)` will add the size of one array of 100 elements, So after this the pointer will be at 2nd 1D array `&m[1][0]`

`*(m+1)+2 ` equivalent to `&m[1][0] + 2 => &m[1][2]`

`*(*(m+1)) equivalent to value at m[1][0]`

`*(*m + 1) equivalent to value at m[0][1]`

`m[i][j] = *(m[i] + j) = *(*(m+i)+j)`
