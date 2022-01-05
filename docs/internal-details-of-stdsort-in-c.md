# c++中 std::sort()的内部细节

> 原文:[https://www . geesforgeks . org/internal-details-of-stdsort-in-c/](https://www.geeksforgeeks.org/internal-details-of-stdsort-in-c/)

[**排序**](https://www.geeksforgeeks.org/sort-algorithms-the-c-standard-template-library-stl/)**是应用于数据的最基本功能之一。这意味着以特定的方式排列数据，可以是增加的，也可以是减少的。C++ STL 中有一个名为 sort()的内置函数。**

**[**std::sort()**](https://www.geeksforgeeks.org/sort-c-stl/) 是 C++标准库中的一个泛型函数，用于做比较排序。**

### **语法:**

```
sort(startaddress, endaddress, comparator)

where:
startaddress: the address of the first element of the array
endaddress: the address of the last element of the array
comparator: the comparison to be done with the array. 
            This argument is optional. 
```

### **示例:**

## **C++**

```
// C++ program to demonstrate
// behaviour of sort() in STL.

#include <bits/stdc++.h>
using namespace std;

int main()
{
    int arr[] = {1, 5, 8, 9, 6, 7, 3, 4, 2, 0};
    int n = sizeof(arr)/sizeof(arr[0]);

    sort(arr, arr+n);

    cout << "\nArray after sorting using "
         "default sort is : \n";

    for (int i = 0; i < n; ++i)
        cout << arr[i] << " ";

    return 0;
}
```

****Output:** 

```
Array after sorting using default sort is : 
0 1 2 3 4 5 6 7 8 9
```** 

### **时间复杂性**

*   **最佳情况–无(无对数)**
*   **平均病例数**
*   **更糟的情况**

**其中，N =要排序的元素数量。**

### **排序使用的算法()**

**sort()使用的算法是[**内含排序**](https://www.geeksforgeeks.org/know-your-sorting-algorithm-set-2-introsort-cs-sorting-weapon/)**。Introsort 是一种混合排序算法，使用三种排序算法来最小化运行时间，[快速排序](https://www.geeksforgeeks.org/quick-sort/)、[堆排序](https://www.geeksforgeeks.org/heap-sort/)和[插入排序](https://www.geeksforgeeks.org/insertion-sort/)。简单来说，就是周围最好的排序算法。它是一种混合排序算法，这意味着它使用多个排序算法作为例程。****

## ****C++****

```
**/* A Program to sort the array using Introsort.
  The most popular C++ STL Algorithm- sort()
  uses Introsort. */

#include<bits/stdc++.h>
using namespace std;

// A utility function to swap the values pointed by
// the two pointers
void swapValue(int *a, int *b)
{
    int *temp = a;
    a = b;
    b = temp;
    return;
}

/* Function to sort an array using insertion sort*/
void InsertionSort(int arr[], int *begin, int *end)
{
    // Get the left and the right index of the subarray
    // to be sorted
    int left = begin - arr;
    int right = end - arr;

    for (int i = left+1; i <= right; i++)
    {
        int key = arr[i];
        int j = i-1;

       /* Move elements of arr[0..i-1], that are
          greater than key, to one position ahead
          of their current position */
        while (j >= left && arr[j] > key)
        {
            arr[j+1] = arr[j];
            j = j-1;
        }
        arr[j+1] = key;
   }

   return;
}

// A function to partition the array and return
// the partition point
int* Partition(int arr[], int low, int high)
{
    int pivot = arr[high];    // pivot
    int i = (low - 1);  // Index of smaller element

    for (int j = low; j <= high- 1; j++)
    {
        // If current element is smaller than or
        // equal to pivot
        if (arr[j] <= pivot)
        {
            // increment index of smaller element
            i++;

            swap(arr[i], arr[j]);
        }
    }
    swap(arr[i + 1], arr[high]);
    return (arr + i + 1);
}

// A function that find the middle of the
// values pointed by the pointers a, b, c
// and return that pointer
int *MedianOfThree(int * a, int * b, int * c)
{
    if (*a < *b && *b < *c)
        return (b);

    if (*a < *c && *c <= *b)
        return (c);

    if (*b <= *a && *a < *c)
        return (a);

    if (*b < *c && *c <= *a)
        return (c);

    if (*c <= *a && *a < *b)
        return (a);

    if (*c <= *b && *b <= *c)
        return (b);
}

// A Utility function to perform intro sort
void IntrosortUtil(int arr[], int * begin,
                  int * end, int depthLimit)
{
    // Count the number of elements
    int size = end - begin;

      // If partition size is low then do insertion sort
    if (size < 16)
    {
        InsertionSort(arr, begin, end);
        return;
    }

    // If the depth is zero use heapsort
    if (depthLimit == 0)
    {
        make_heap(begin, end+1);
        sort_heap(begin, end+1);
        return;
    }

    // Else use a median-of-three concept to
    // find a good pivot
    int * pivot = MedianOfThree(begin, begin+size/2, end);

    // Swap the values pointed by the two pointers
    swapValue(pivot, end);

   // Perform Quick Sort
    int * partitionPoint = Partition(arr, begin-arr, end-arr);
    IntrosortUtil(arr, begin, partitionPoint-1, depthLimit - 1);
    IntrosortUtil(arr, partitionPoint + 1, end, depthLimit - 1);

    return;
}

/* Implementation of introsort*/
void Introsort(int arr[], int *begin, int *end)
{
    int depthLimit = 2 * log(end-begin);

    // Perform a recursive Introsort
    IntrosortUtil(arr, begin, end, depthLimit);

      return;
}

// A utility function ot print an array of size n
void printArray(int arr[], int n)
{
   for (int i=0; i < n; i++)
       printf("%d ", arr[i]);
   printf("\n");
}

// Driver program to test Introsort
int main()
{
    int arr[] = {3, 1, 23, -9, 233, 23, -313, 32, -9};
    int n = sizeof(arr) / sizeof(arr[0]);

    // Pass the array, the pointer to the first element and
    // the pointer to the last element
    Introsort(arr, arr, arr+n-1);
    printArray(arr, n);

    return(0);
}**
```

******Output:** 

```
-313 -9 -9 1 3 23 23 32 233
```**** 

****标准 C 库提供了 **qsort()** 可以用来对数组进行排序。顾名思义，该函数使用快速排序算法对给定的数组进行排序****

****用 sort()代替 qsort() 更好**，因为:******

1.  ****sort()不使用像 qsort()这样的不安全的 void 指针。****
2.  ****与 sort()相比，qsort()对比较函数进行了大量的函数调用。****
3.  ****使用 sort()的 C++代码比使用 qsort()的代码相对更快。****

******详文:** [排序()与 qsort()](https://www.geeksforgeeks.org/c-qsort-vs-c-sort/)
的比较****