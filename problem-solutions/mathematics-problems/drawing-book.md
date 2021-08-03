# Drawing Book

### Source

* [Hacker Rank](https://www.hackerrank.com/challenges/drawing-book/problem)

### Problem Statement

A teacher asks the class to open their books to a page number. A student can either start turning pages from the front of the book or from the back of the book. They always turn pages one at a time. When they open the book, page 1 is always on the right side:

![image](https://s3.amazonaws.com/hr-challenge-images/0/1481920803-d2b54f38f0-book.png)

When they flip page 1 , they see pages 2 and 3 . Each page except the last page will always be printed on both sides. The last page may only be printed on the front, given the length of the book. If the book is  n pages long, and a student wants to turn to page p , what is the minimum number of pages to turn? They can start at the beginning or the end of the book. Given  n and p , find and print the minimum number of pages that must be turned in order to arrive at page p 

**Example**

![Untitled Diagram\(4\).png](https://s3.amazonaws.com/hr-challenge-images/22564/1467398281-32b69f6fa9-UntitledDiagram4.png)

**Sample Input 0**

```text
Input:
5
4
Output:
```

### Solution

```cpp
int pageCount(int n, int p) {
    int total_pages = (n/2) + 1;
    int p_page = (p/2) + 1;
    if(total_pages - p_page <= p_page - 1)
        return total_pages - p_page;
    else {
        return p_page - 1;
    }
}
```

