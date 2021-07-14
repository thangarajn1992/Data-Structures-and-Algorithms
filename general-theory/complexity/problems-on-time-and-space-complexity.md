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

#### Problem 8

In a competition, four different functions are observed. All the functions use a single for loop and within the for loop, same set of statements are executed.

Consider the following for loops:

```text
  A) for(i = 0; i < n; i++)
 
  B) for(i = 0; i < n; i += 2)
 
  C) for(i = 1; i < n; i *= 2)
 
  D) for(i = n; i > -1; i /= 2)
```

If n is the size of input\(positive\), which function is the most efficient? In other words, which loop completes the fastest.

Answer: C

#### Problem 9

Which of the given options provides the increasing order of complexity of functions f1, f2, f3 and f4:

```text
f1(n) = 2^n
f2(n) = n^(3/2)
f3(n) = nLogn
f4(n) = n^(Logn)

f3, f2, f4, f1
f3, f2, f1, f4
f2, f3, f1, f4
f2, f3, f4, f1


// Correct order : f3, f2, f4, f1
```

#### Problem 10

```cpp
/* 
 * V is sorted 
 * V.size() = N
 * The function is initially called as searchNumOccurrence(V, k, 0, N-1)
 */
int searchNumOccurrence(vector<int> &V, int k, int start, int end) {
    if (start > end) return 0;
    int mid = (start + end) / 2;
    if (V[mid] < k) return searchNumOccurrence(V, k, mid + 1, end);
    if (V[mid] > k) return searchNumOccurrence(V, k, start, mid - 1);
    return searchNumOccurrence(V, k, start, mid - 1) + 1 + searchNumOccurrence(V, k, mid + 1, end);
}

// Worst Case Time Complexity: O(N)
```

#### Problem 11

What is the worst case time complexity of the following code:

```cpp
int findMinPath(vector<vector<int> > &V, int r, int c) {
  int R = V.size();
  int C = V[0].size();
  if (r >= R || c >= C) return 100000000; // Infinity
  if (r == R - 1 && c == C - 1) return 0;
  return V[r][c] + min(findMinPath(V, r + 1, c), findMinPath(V, r, c + 1));
}

// Worst Case Time Complexity : O(2^(R+C))
```

#### Problem 12

What is the worst case time complexity of the following code:

```cpp
int memo[101][101];
int findMinPath(vector<vector<int> >& V, int r, int c) {
  int R = V.size();
  int C = V[0].size();
  if (r >= R || c >= C) 
    return 100000000; // Infinity
  if (r == R - 1 && c == C - 1) 
    return 0;
  if (memo[r][c] != -1) 
    return memo[r][c];
  memo[r][c] =  V[r][c] + min(findMinPath(V, r + 1, c), findMinPath(V, r, c + 1));
  return memo[r][c];
}

// Worst Case Time Complexity : O(R*C)
```

#### Problem 13

In the following C++ function, let n &gt;= m. What is the time complexity of the above function assuming `n > m`?

```cpp
int gcd(int n, int m) {
    if (n % m ==0) 
        return m;
    if (n < m) 
        swap(n, m);
    while (m > 0) {
        n = n%m;
        swap(n, m);
    }
    return n;
}

// Time Complexity : ø(log(n))
```

#### Problem 14

What is the time complexity of the following code :

```cpp
int j = 0;
for(int i = 0; i < n; ++i) {
   while(j < n && arr[i] < arr[j]) {
      j++;
   }
}

// Amortized Time Complexity : O(N)
```

