# 使用最小堆按降序进行堆排序

> 原文:[https://www . geesforgeks . org/heap-sort-for-降序-using-min-heap/](https://www.geeksforgeeks.org/heap-sort-for-decreasing-order-using-min-heap/)

给定一个元素数组，使用最小堆按降序对数组进行排序。
**例:**

```
Input : arr[] = {5, 3, 10, 1}
Output : arr[] = {10, 5, 3, 1}

Input : arr[] = {1, 50, 100, 25}
Output : arr[] = {100, 50, 25, 1}
```

先决条件:[堆排序](https://www.geeksforgeeks.org/heap-sort/)使用[最小堆](https://www.geeksforgeeks.org/binary-heap/)。
**算法:**
**1。**根据输入数据构建最小堆。
**2。**此时，最小的项目存储在堆的根。用堆的最后一项替换它，然后将堆的大小减少 1。最后，清理树根。
**3。**当堆的大小大于 1 时，重复上述步骤。
**注意:**堆排序使用最小堆按降序排序，其中最大堆按升序排序

## C++

```
// C++ program for implementation of Heap Sort
#include <bits/stdc++.h>
using namespace std;

// To heapify a subtree rooted with node i which is
// an index in arr[]. n is size of heap
void heapify(int arr[], int n, int i)
{
    int smallest = i; // Initialize smalles as root
    int l = 2 * i + 1; // left = 2*i + 1
    int r = 2 * i + 2; // right = 2*i + 2

    // If left child is smaller than root
    if (l < n && arr[l] < arr[smallest])
        smallest = l;

    // If right child is smaller than smallest so far
    if (r < n && arr[r] < arr[smallest])
        smallest = r;

    // If smallest is not root
    if (smallest != i) {
        swap(arr[i], arr[smallest]);

        // Recursively heapify the affected sub-tree
        heapify(arr, n, smallest);
    }
}

// main function to do heap sort
void heapSort(int arr[], int n)
{
    // Build heap (rearrange array)
    for (int i = n / 2 - 1; i >= 0; i--)
        heapify(arr, n, i);

    // One by one extract an element from heap
    for (int i = n - 1; i >= 0; i--) {
        // Move current root to end
        swap(arr[0], arr[i]);

        // call max heapify on the reduced heap
        heapify(arr, i, 0);
    }
}

/* A utility function to print array of size n */
void printArray(int arr[], int n)
{
    for (int i = 0; i < n; ++i)
        cout << arr[i] << " ";
    cout << "\n";
}

// Driver program
int main()
{
    int arr[] = { 4, 6, 3, 2, 9 };
    int n = sizeof(arr) / sizeof(arr[0]);

    heapSort(arr, n);

    cout << "Sorted array is \n";
    printArray(arr, n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for implementation of Heap Sort

import java.io.*;

class GFG {

    // To heapify a subtree rooted with node i which is
    // an index in arr[]. n is size of heap
    static void heapify(int arr[], int n, int i)
    {
        int smallest = i; // Initialize smalles as root
        int l = 2 * i + 1; // left = 2*i + 1
        int r = 2 * i + 2; // right = 2*i + 2

        // If left child is smaller than root
        if (l < n && arr[l] < arr[smallest])
            smallest = l;

        // If right child is smaller than smallest so far
        if (r < n && arr[r] < arr[smallest])
            smallest = r;

        // If smallest is not root
        if (smallest != i) {
            int temp = arr[i];
            arr[i] = arr[smallest];
            arr[smallest] = temp;

            // Recursively heapify the affected sub-tree
            heapify(arr, n, smallest);
        }
    }

    // main function to do heap sort
    static void heapSort(int arr[], int n)
    {
        // Build heap (rearrange array)
        for (int i = n / 2 - 1; i >= 0; i--)
            heapify(arr, n, i);

        // One by one extract an element from heap
        for (int i = n - 1; i >= 0; i--) {

            // Move current root to end
            int temp = arr[0];
            arr[0] = arr[i];
            arr[i] = temp;

            // call max heapify on the reduced heap
            heapify(arr, i, 0);
        }
    }

    /* A utility function to print array of size n */
    static void printArray(int arr[], int n)
    {
        for (int i = 0; i < n; ++i)
            System.out.print(arr[i] + " ");
        System.out.println();
    }

    // Driver program
    public static void main(String[] args)
    {
        int arr[] = { 4, 6, 3, 2, 9 };
        int n = arr.length;

        heapSort(arr, n);

        System.out.println("Sorted array is ");
        printArray(arr, n);
    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python3 program for implementation
# of Heap Sort

# To heapify a subtree rooted with
# node i which is an index in arr[].
# n is size of heap
def heapify(arr, n, i):
    smallest = i # Initialize smalles as root
    l = 2 * i + 1 # left = 2*i + 1
    r = 2 * i + 2 # right = 2*i + 2

    # If left child is smaller than root
    if l < n and arr[l] < arr[smallest]:
        smallest = l

    # If right child is smaller than
    # smallest so far
    if r < n and arr[r] < arr[smallest]:
        smallest = r

    # If smallest is not root
    if smallest != i:
        (arr[i],
         arr[smallest]) = (arr[smallest],
                           arr[i])

        # Recursively heapify the affected
        # sub-tree
        heapify(arr, n, smallest)

# main function to do heap sort
def heapSort(arr, n):

    # Build heap (rearrange array)
    for i in range(int(n / 2) - 1, -1, -1):
        heapify(arr, n, i)

    # One by one extract an element
    # from heap
    for i in range(n-1, -1, -1):

        # Move current root to end #
        arr[0], arr[i] = arr[i], arr[0]

        # call max heapify on the reduced heap
        heapify(arr, i, 0)

# A utility function to print
# array of size n
def printArray(arr, n):

    for i in range(n):
        print(arr[i], end = " ")
    print()

# Driver Code
if __name__ == '__main__':
    arr = [4, 6, 3, 2, 9]
    n = len(arr)

    heapSort(arr, n)

    print("Sorted array is ")
    printArray(arr, n)

# This code is contributed by PranchalK
```

## C#

```
// C# program for implementation of Heap Sort
using System;

class GFG {

    // To heapify a subtree rooted with
    // node i which is an index in arr[],
    // n is size of heap
    static void heapify(int[] arr, int n, int i)
    {
        int smallest = i; // Initialize smalles as root
        int l = 2 * i + 1; // left = 2*i + 1
        int r = 2 * i + 2; // right = 2*i + 2

        // If left child is smaller than root
        if (l < n && arr[l] < arr[smallest])
            smallest = l;

        // If right child is smaller than smallest so far
        if (r < n && arr[r] < arr[smallest])
            smallest = r;

        // If smallest is not root
        if (smallest != i) {
            int temp = arr[i];
            arr[i] = arr[smallest];
            arr[smallest] = temp;

            // Recursively heapify the affected sub-tree
            heapify(arr, n, smallest);
        }
    }

    // main function to do heap sort
    static void heapSort(int[] arr, int n)
    {
        // Build heap (rearrange array)
        for (int i = n / 2 - 1; i >= 0; i--)
            heapify(arr, n, i);

        // One by one extract an element from heap
        for (int i = n - 1; i >= 0; i--) {

            // Move current root to end
            int temp = arr[0];
            arr[0] = arr[i];
            arr[i] = temp;

            // call max heapify on the reduced heap
            heapify(arr, i, 0);
        }
    }

    /* A utility function to print array of size n */
    static void printArray(int[] arr, int n)
    {
        for (int i = 0; i < n; ++i)
            Console.Write(arr[i] + " ");
        Console.WriteLine();
    }

    // Driver program
    public static void Main()
    {
        int[] arr = { 4, 6, 3, 2, 9 };
        int n = arr.Length;

        heapSort(arr, n);

        Console.WriteLine("Sorted array is ");
        printArray(arr, n);
    }
}

// This code is contributed by vt_m.
```

## java 描述语言

```
<script>

// Javascript program for implementation of Heap Sort

// To heapify a subtree rooted with node i which is
// an index in arr[]. n is size of heap
function heapify(arr, n, i)
{
    var smallest = i; // Initialize smalles as root
    var l = 2 * i + 1; // left = 2*i + 1
    var r = 2 * i + 2; // right = 2*i + 2

    // If left child is smaller than root
    if (l < n && arr[l] < arr[smallest])
        smallest = l;

    // If right child is smaller than smallest so far
    if (r < n && arr[r] < arr[smallest])
        smallest = r;

    // If smallest is not root
    if (smallest != i) {
        [arr[i], arr[smallest]] = [arr[smallest], arr[i]]

        // Recursively heapify the affected sub-tree
        heapify(arr, n, smallest);
    }
}

// main function to do heap sort
function heapSort(arr, n)
{
    // Build heap (rearrange array)
    for (var i = parseInt(n / 2 - 1); i >= 0; i--)
        heapify(arr, n, i);

    // One by one extract an element from heap
    for (var i = n - 1; i >= 0; i--) {
        // Move current root to end
        [arr[0], arr[i]] = [arr[i], arr[0]]

        // call max heapify on the reduced heap
        heapify(arr, i, 0);
    }
}

/* A utility function to print array of size n */
function printArray(arr, n)
{
    for (var i = 0; i < n; ++i)
        document.write( arr[i] + " ");
    document.write("<br>");
}

// Driver program
var arr = [4, 6, 3, 2, 9];
var n = arr.length;
heapSort(arr, n);
document.write( "Sorted array is <br>");
printArray(arr, n);

</script>
```

**Output:** 

```
Sorted array is 
9 6 4 3 2
```

**时间复杂度:**需要 **O(logn)** 来**堆**和 **O(n)** 来**构建堆**。因此，使用**最小堆**或**最大堆**的**堆排序**的总时间复杂度为 **O(nlogn)**