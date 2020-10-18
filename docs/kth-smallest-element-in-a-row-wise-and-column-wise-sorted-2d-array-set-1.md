# 按行和按列排序的 2D 数组中的第`K`个最小元素 | 系列 1

> 原文： [https://www.geeksforgeeks.org/kth-smallest-element-in-a-row-wise-and-column-wise-sorted-2d-array-set-1/](https://www.geeksforgeeks.org/kth-smallest-element-in-a-row-wise-and-column-wise-sorted-2d-array-set-1/)

给定一个`n x n`矩阵，其中每一行和每一列均以非降序排列。 在给定的 2D 数组中找到第`k`个最小的元素。

**示例**：

```
Input:k = 3 and array =
        10, 20, 30, 40
        15, 25, 35, 45
        24, 29, 37, 48
        32, 33, 39, 50 
Output: 20
Explanation: The 3rd smallest element is 20 

Input:k = 7 and array =
        10, 20, 30, 40
        15, 25, 35, 45
        24, 29, 37, 48
        32, 33, 39, 50 
Output: 30

Explanation: The 7th smallest element is 30

```



**方法**：因此，想法是找到第`k`个最小元素。 每行和每一列进行排序。 因此，可以将其视为 [C 有序列表，并且这些列表必须合并为一个列表](https://www.geeksforgeeks.org/merge-k-sorted-linked-lists-set-2-using-min-heap/)，因此必须找出列表的第`k`个元素。 因此，方法类似，唯一的区别是找到第`k`个元素时，循环结束。

**算法**：

1.  这个想法是使用最小堆。 创建最小堆以存储元素。

2.  从头到尾遍历第一行，并从第一行开始构建最小的元素堆。 堆条目还存储行号和列号。

3.  现在运行循环`k`次以在每次迭代中从堆中提取最小元素。

4.  从最小堆获取最小元素（或根）。

5.  查找最小元素的行号和列号。

6.  用同一列中的下一个元素替换根，并最小化根。

7.  打印最后提取的元素，即第`k`个最小元素。

**实现**：

## C++ 

```cpp

// kth largest element in a 2d array sorted row-wise and column-wise 
#include<iostream> 
#include<climits> 
using namespace std; 

// A structure to store entry of heap.  The entry contains 
// value from 2D array, row and column numbers of the value 
struct HeapNode { 
    int val;  // value to be stored 
    int r;    // Row number of value in 2D array 
    int c;    // Column number of value in 2D array 
}; 

// A utility function to swap two HeapNode items. 
void swap(HeapNode *x, HeapNode *y) { 
    HeapNode z = *x; 
    *x = *y; 
    *y = z; 
} 

// A utility function to minheapify the node harr[i] of a heap 
// stored in harr[] 
void minHeapify(HeapNode harr[], int i, int heap_size) 
{ 
    int l = i*2 + 1; 
    int r = i*2 + 2; 
    int smallest = i; 
    if (l < heap_size && harr[l].val < harr[i].val) 
        smallest = l; 
    if (r < heap_size && harr[r].val < harr[smallest].val) 
        smallest = r; 
    if (smallest != i) 
    { 
        swap(&harr[i], &harr[smallest]); 
        minHeapify(harr, smallest, heap_size); 
    } 
} 

// A utility function to convert harr[] to a max heap 
void buildHeap(HeapNode harr[], int n) 
{ 
    int i = (n - 1)/2; 
    while (i >= 0) 
    { 
        minHeapify(harr, i, n); 
        i--; 
    } 
} 

// This function returns kth smallest element in a 2D array mat[][] 
int kthSmallest(int mat[4][4], int n, int k) 
{ 
    // k must be greater than 0 and smaller than n*n 
    if (k <= 0 || k > n*n) 
       return INT_MAX; 

    // Create a min heap of elements from first row of 2D array 
    HeapNode harr[n]; 
    for (int i = 0; i < n; i++) 
        harr[i] =  {mat[0][i], 0, i}; 
    buildHeap(harr, n); 

    HeapNode hr; 
    for (int i = 0; i < k; i++) 
    { 
       // Get current heap root 
       hr = harr[0]; 

       // Get next value from column of root's value. If the 
       // value stored at root was last value in its column, 
       // then assign INFINITE as next value 
       int nextval = (hr.r < (n-1))? mat[hr.r + 1][hr.c]: INT_MAX; 

       // Update heap root with next value 
       harr[0] =  {nextval, (hr.r) + 1, hr.c}; 

       // Heapify root 
       minHeapify(harr, 0, n); 
    } 

    // Return the value at last extracted root 
    return hr.val; 
} 

// driver program to test above function 
int main() 
{ 
  int mat[4][4] = { {10, 20, 30, 40}, 
                    {15, 25, 35, 45}, 
                    {25, 29, 37, 48}, 
                    {32, 33, 39, 50}, 
                  }; 
  cout << "7th smallest element is " << kthSmallest(mat, 4, 7); 
  return 0; 
} 

```

## Java

```java
// Java program for kth largest element in a 2d 
// array sorted row-wise and column-wise 
class GFG{
     
// A structure to store entry of heap.
// The entry contains value from 2D array,
// row and column numbers of the value 
static class HeapNode
{
     
    // Value to be stored 
    int val;
     
    // Row number of value in 2D array 
    int r;
     
    // Column number of value in 2D array 
    int c;
     
    HeapNode(int val, int r, int c)
    {
        this.val = val;
        this.c = c;
        this.r = r;
    }
}
 
// A utility function to swap two HeapNode items. 
static void swap(int i, int min, HeapNode[] arr)
{
    HeapNode temp = arr[i];
    arr[i] = arr[min];
    arr[min] = temp;
}
 
// A utility function to minheapify the node
// harr[i] of a heap stored in harr[] 
static void minHeapify(HeapNode harr[], 
                       int i, int heap_size)
{
    int l = 2 * i + 1;
    int r = 2 * i + 2;
    int min = i;
     
    if (l < heap_size && 
        harr[l].val < harr[i].val)
    {
        min = l;
    }
    if (r < heap_size && 
        harr[r].val < harr[i].val)
    {
        min = r;
    }
     
    if (min != i)
    {
        swap(i, min, harr);
        minHeapify(harr, min, heap_size);
    }
}
 
// A utility function to convert 
// harr[] to a max heap 
static void buildHeap(HeapNode harr[], int n)
{
    int i = (n - 1) / 2;
    while (i >= 0) 
    {
        minHeapify(harr, i, n);
        i--;
    }
}
 
// This function returns kth smallest
// element in a 2D array mat[][] 
public static int kthSmallest(int[][] mat,
                              int n, int k)
{
     
    // k must be greater than 0 and 
    // smaller than n*n 
    if (k <= 0 || k > n * n)
    {
        return Integer.MAX_VALUE;
    }
     
    // Create a min heap of elements 
    // from first row of 2D array 
    HeapNode harr[] = new HeapNode[n];
     
    for(int i = 0; i < n; i++)
    {
        harr[i] = new HeapNode(mat[0][i], 0, i);
    }
    buildHeap(harr, n);
     
    HeapNode hr = new HeapNode(0, 0, 0);
     
    for(int i = 1; i < k; i++)
    {
         
        // Get current heap root 
        hr = harr[0];
         
        // Get next value from column of root's
        // value. If the value stored at root was
        // last value in its column, then assign
        // INFINITE as next value 
        int nextVal = hr.r < n - 1 ? 
                      mat[hr.r + 1][hr.c] :
                      Integer.MAX_VALUE;
                       
        // Update heap root with next value 
        harr[0] = new HeapNode(nextVal, 
                               hr.r + 1, hr.c);
                                
        // Heapify root 
        minHeapify(harr, 0, n);
    }
     
    // Return the value at last extracted root 
    return hr.val;
}
 
// Driver code
public static void main(String args[])
{
    int mat[][] = { { 10, 20, 30, 40 },
                    { 15, 25, 35, 45 },
                    { 25, 29, 37, 48 },
                    { 32, 33, 39, 50 } };
                     
    int res = kthSmallest(mat, 4, 7);
     
    System.out.print("7th smallest element is "+ res);
}
}
 
// This code is contributed by nikhil kumar sharma
```

## Python3

```py
# Program for kth largest element in a 2d array 
# sorted row-wise and column-wise 
from sys import maxsize 
 
# A structure to store an entry of heap. 
# The entry contains a value from 2D array, 
# row and column numbers of the value 
class HeapNode: 
    def __init__(self, val, r, c): 
        self.val = val # value to be stored 
        self.r = r # Row number of value in 2D array 
        self.c = c # Column number of value in 2D array 
 
# A utility function to minheapify the node harr[i] 
# of a heap stored in harr[] 
def minHeapify(harr, i, heap_size): 
    l = i * 2 + 1
    r = i * 2 + 2
    smallest = i 
    if l < heap_size and harr[l].val < harr[i].val: 
        smallest = l 
    if r < heap_size and harr[r].val < harr[smallest].val: 
        smallest = r 
 
    if smallest != i: 
        harr[i], harr[smallest] = harr[smallest], harr[i] 
        minHeapify(harr, smallest, heap_size) 
 
# A utility function to convert harr[] to a max heap 
def buildHeap(harr, n): 
    i = (n - 1) // 2
    while i >= 0: 
        minHeapify(harr, i, n) 
        i -= 1
 
# This function returns kth smallest element 
# in a 2D array mat[][] 
def kthSmallest(mat, n, k): 
 
    # k must be greater than 0 and smaller than n*n 
    if k <= 0 or k > n * n: 
        return maxsize 
 
    # Create a min heap of elements from 
    # first row of 2D array 
    harr = [0] * n 
    for i in range(n): 
        harr[i] = HeapNode(mat[0][i], 0, i) 
    buildHeap(harr, n) 
 
    hr = HeapNode(0, 0, 0) 
    for i in range(k): 
 
        # Get current heap root 
        hr = harr[0] 
 
        # Get next value from column of root's value. 
        # If the value stored at root was last value 
        # in its column, then assign INFINITE as next value 
        nextval = mat[hr.r + 1][hr.c] if (hr.r < n - 1) else maxsize 
 
        # Update heap root with next value 
        harr[0] = HeapNode(nextval, hr.r + 1, hr.c) 
 
        # Heapify root 
        minHeapify(harr, 0, n) 
 
    # Return the value at last extracted root 
    return hr.val 
 
# Driver Code 
if __name__ == "__main__": 
    mat = [[10, 20, 30, 40], 
        [15, 25, 35, 45], 
        [25, 29, 37, 48], 
        [32, 33, 39, 50]] 
    print("7th smallest element is", 
            kthSmallest(mat, 4, 7)) 
 
# This code is contributed by 
# sanjeev2552 
```

## C#

```cs
// C# program for kth largest element in a 2d 
// array sorted row-wise and column-wise 
using System;
 
class GFG{
     
// A structure to store entry of heap.
// The entry contains value from 2D array,
// row and column numbers of the value 
class HeapNode
{
     
    // Value to be stored 
    public int val;
     
    // Row number of value in 2D array 
    public int r;
     
    // Column number of value in 2D array 
    public int c;
     
    public HeapNode(int val, int r, int c)
    {
        this.val = val;
        this.c = c;
        this.r = r;
    }
}
 
// A utility function to swap two
// HeapNode items. 
static void swap(int i, int min,
                 HeapNode[] arr)
{
    HeapNode temp = arr[i];
    arr[i] = arr[min];
    arr[min] = temp;
}
 
// A utility function to minheapify the node
// harr[i] of a heap stored in harr[] 
static void minHeapify(HeapNode []harr, 
                       int i, int heap_size)
{
    int l = 2 * i + 1;
    int r = 2 * i + 2;
    int min = i;
     
    if (l < heap_size && 
        harr[l].val < harr[i].val)
    {
        min = l;
    }
    if (r < heap_size && 
        harr[r].val < harr[i].val)
    {
        min = r;
    }
     
    if (min != i)
    {
        swap(i, min, harr);
        minHeapify(harr, min, heap_size);
    }
}
 
// A utility function to convert 
// harr[] to a max heap 
static void buildHeap(HeapNode []harr, int n)
{
    int i = (n - 1) / 2;
    while (i >= 0) 
    {
        minHeapify(harr, i, n);
        i--;
    }
}
 
// This function returns kth smallest
// element in a 2D array [,]mat 
public static int kthSmallest(int[,] mat,
                              int n, int k)
{
     
    // k must be greater than 0 and 
    // smaller than n*n 
    if (k <= 0 || k > n * n)
    {
        return int.MaxValue;
    }
     
    // Create a min heap of elements 
    // from first row of 2D array 
    HeapNode []harr = new HeapNode[n];
     
    for(int i = 0; i < n; i++)
    {
        harr[i] = new HeapNode(mat[0, i], 0, i);
    }
    buildHeap(harr, n);
     
    HeapNode hr = new HeapNode(0, 0, 0);
     
    for(int i = 1; i < k; i++)
    {
         
        // Get current heap root 
        hr = harr[0];
         
        // Get next value from column of root's
        // value. If the value stored at root was
        // last value in its column, then assign
        // INFINITE as next value 
        int nextVal = hr.r < n - 1 ? 
                      mat[hr.r + 1, hr.c] :
                      int.MaxValue;
                       
        // Update heap root with next value 
        harr[0] = new HeapNode(nextVal, 
                               hr.r + 1, hr.c);
                                
        // Heapify root 
        minHeapify(harr, 0, n);
    }
     
    // Return the value at last
    // extracted root 
    return hr.val;
}
 
// Driver code
public static void Main(String []args)
{
    int [,]mat = { { 10, 20, 30, 40 },
                   { 15, 25, 35, 45 },
                   { 25, 29, 37, 48 },
                   { 32, 33, 39, 50 } };
                     
    int res = kthSmallest(mat, 4, 7);
     
    Console.Write("7th smallest element is " + res);
}
}
 
// This code is contributed by Amit Katiyar
```

输出：

```
7th smallest element is 30
```

复杂度分析：

1.  时间复杂度：上述解决方案涉及以下步骤。
    +   建立耗时`O(n)`的最小堆
    +   建堆`k`次，这需要`O(k Logn)`时间。
2.  空间复杂度：`O(R)`，其中`R`是一行的长度，因为最小堆一次存储一行。

当`k`小于`n`时，可以优化上述代码以构建大小为k的堆。 在这种情况下，第`k`个最小的元素必须位于前`k`行和`k`列中。

我们很快将发布更有效的算法来查找第`k`个最小元素。