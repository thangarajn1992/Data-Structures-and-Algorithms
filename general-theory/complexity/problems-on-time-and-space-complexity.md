# Problems On Time and Space Complexity

#### Problem 1:

```cpp
int a = 0, b = 0;    
for (i = 0; i < N; i++) {
    a = a + rand();  
}
for (j = 0; j < M; j++) {
    b = b + rand();
}

// Time Complexity : O(N+M)
// Space Complexity : O(1)
```

#### Problem 2

```cpp
int a = 0, b = 0;    
for (i = 0; i < N; i++) {
    for (j = 0; j < N; j++) {
        a = a + j;
    }
}
for (k = 0; k < N; k++) {
    b = b + k;
} 

// Time Complexity : O(N * N)
// Space Complexity : O(1)
```

#### Problem 3

```cpp
int a = 0;
for (i = 0; i < N; i++) {
    for (j = N; j > i; j--) {
        a = a + i + j;
    }
}

// Time Complexity : O(N * N)
// Space Complexity : O(1)
```

#### Problem 4

What does it mean when we say that an algorithm X is asymptotically more efficient than Y?

Answer : X will always be a better choice for large inputs

#### Problem 5

```cpp
int a = 0, i = N;
while (i > 0) {
    a += i;
    i /= 2;
}

// Time Complexity : O(log(N))
// Space Complexity : O(1)
```

#### Problem 6 \(Tricky\)

```cpp
int count = 0;
for (int i = N; i > 0; i /= 2) {
    for (int j = 0; j < i; j++) {
        count += 1;
    }
}

// Time Complexity : O(N)
// Space Complexity : O(1)
```

#### Problem 7

```cpp
int i, j, k = 0;
for (i  = n/2; i <= n; i++) {
    for (j = 2; j <= n; j = j * 2) {
        k = k + n/2;
    }
}

// Time Complexity : O(N * log(N))
// Space Complexity : O(1)
```



