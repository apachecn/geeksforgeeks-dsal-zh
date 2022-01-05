# Hoare vs Lomuto 快速排序中的分区方案

> 原文:[https://www . geesforgeks . org/hoares-vs-lomuto-partition-scheme-quick sort/](https://www.geeksforgeeks.org/hoares-vs-lomuto-partition-scheme-quicksort/)

我们已经讨论了使用 Lomuto 分区方案实现[快速排序。与 Hoare 方案相比，Lomuto 的分区方案易于实现。这在性能上不如霍尔的 QuickSort。](https://www.geeksforgeeks.org/quick-sort/)

**洛木托的分割方案:**

```
partition(arr[], lo, hi) 
    pivot = arr[hi]
    i = lo     // place for swapping
    for j := lo to hi – 1 do
        if arr[j] <= pivot then
            swap arr[i] with arr[j]
            i = i + 1
    swap arr[i] with arr[hi]
    return i
```

该分区方案详见[快速排序](https://www.geeksforgeeks.org/quick-sort/)。
以下是该方法的实施情况:-

## C++

```
/* C++ implementation QuickSort using Lomuto's partition
   Scheme.*/
#include<bits/stdc++.h>
using namespace std;

/* This function takes last element as pivot, places
   the pivot element at its correct position in sorted
    array, and places all smaller (smaller than pivot)
   to left of pivot and all greater elements to right
   of pivot */
int partition(int arr[], int low, int high)
{
    int pivot = arr[high];    // pivot
    int i = (low - 1);  // Index of smaller element

    for (int j = low; j <= high- 1; j++)
    {
        // If current element is smaller than or
        // equal to pivot
        if (arr[j] <= pivot)
        {
            i++;    // increment index of smaller element
            swap(arr[i], arr[j]);
        }
    }
    swap(arr[i + 1], arr[high]);
    return (i + 1);
}

/* The main function that implements QuickSort
 arr[] --> Array to be sorted,
  low  --> Starting index,
  high  --> Ending index */
void quickSort(int arr[], int low, int high)
{
    if (low < high)
    {
        /* pi is partitioning index, arr[p] is now
           at right place */
        int pi = partition(arr, low, high);

        // Separately sort elements before
        // partition and after partition
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}

/* Function to print an array */
void printArray(int arr[], int size)
{
    int i;
    for (i=0; i < size; i++)
        printf("%d ", arr[i]);
    printf("\n");
}

// Driver program to test above functions
int main()
{
    int arr[] = {10, 7, 8, 9, 1, 5};
    int n = sizeof(arr)/sizeof(arr[0]);
    quickSort(arr, 0, n-1);
    printf("Sorted array: \n");
    printArray(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation QuickSort
// using Lomuto's partition Scheme
import java.io.*;

class GFG
{
static void Swap(int[] array,
                 int position1,
                 int position2)
{
    // Swaps elements in an array

    // Copy the first position's element
    int temp = array[position1];

    // Assign to the second element
    array[position1] = array[position2];

    // Assign to the first element
    array[position2] = temp;
}

/* This function takes last element as
pivot, places the pivot element at its
correct position in sorted array, and
places all smaller (smaller than pivot)
to left of pivot and all greater elements
to right of pivot */
static int partition(int []arr, int low,
                                int high)
{
    int pivot = arr[high];

    // Index of smaller element
    int i = (low - 1);

    for (int j = low; j <= high- 1; j++)
    {
        // If current element is smaller
        // than or equal to pivot
        if (arr[j] <= pivot)
        {
            i++; // increment index of
                 // smaller element
            Swap(arr, i, j);
        }
    }
    Swap(arr, i + 1, high);
    return (i + 1);
}

/* The main function that
   implements QuickSort
arr[] --> Array to be sorted,
low --> Starting index,
high --> Ending index */
static void quickSort(int []arr, int low,
                                 int high)
{
    if (low < high)
    {
        /* pi is partitioning index,
        arr[p] is now at right place */
        int pi = partition(arr, low, high);

        // Separately sort elements before
        // partition and after partition
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}

/* Function to print an array */
static void printArray(int []arr, int size)
{
    int i;
    for (i = 0; i < size; i++)
    System.out.print(" " + arr[i]);
    System.out.println();
}

// Driver Code
static public void main (String[] args)
{
    int []arr = {10, 7, 8, 9, 1, 5};
    int n = arr.length;
    quickSort(arr, 0, n-1);
    System.out.println("Sorted array: ");
    printArray(arr, n);
}
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
''' Python3 implementation QuickSort using Lomuto's partition
Scheme.'''

''' This function takes last element as pivot, places
the pivot element at its correct position in sorted
    array, and places all smaller (smaller than pivot)
to left of pivot and all greater elements to right
of pivot '''
def partition(arr, low, high):

    # pivot
    pivot = arr[high]

    # Index of smaller element
    i = (low - 1)
    for j in range(low, high):

        # If current element is smaller than or
        # equal to pivot
        if (arr[j] <= pivot):

            # increment index of smaller element
            i += 1
            arr[i], arr[j] = arr[j], arr[i]
    arr[i + 1], arr[high] = arr[high], arr[i + 1]
    return (i + 1)

''' The main function that implements QuickSort
arr --> Array to be sorted,
low --> Starting index,
high --> Ending index '''
def quickSort(arr, low, high):
    if (low < high):

        ''' pi is partitioning index, arr[p] is now    
        at right place '''
        pi = partition(arr, low, high)

        # Separately sort elements before
        # partition and after partition
        quickSort(arr, low, pi - 1)
        quickSort(arr, pi + 1, high)

''' Function to pran array '''
def printArray(arr, size):

    for i in range(size):
        print(arr[i], end = " ")
    print()

# Driver code

arr = [10, 7, 8, 9, 1, 5]
n = len(arr)
quickSort(arr, 0, n - 1)
print("Sorted array:")
printArray(arr, n)

# This code is contributed by SHUBHAMSINGH10
```

## C#

```
// C# implementation QuickSort
// using Lomuto's partition Scheme
using System;

class GFG
{
static void Swap(int[] array,
                 int position1,
                 int position2)
{
    // Swaps elements in an array

    // Copy the first position's element
    int temp = array[position1];

    // Assign to the second element
    array[position1] = array[position2];

    // Assign to the first element
    array[position2] = temp;
}

/* This function takes last element as
pivot, places the pivot element at its
correct position in sorted array, and
places all smaller (smaller than pivot)
to left of pivot and all greater elements
to right of pivot */
static int partition(int []arr, int low,
                                int high)
{
    int pivot = arr[high];

    // Index of smaller element
    int i = (low - 1);

    for (int j = low; j <= high- 1; j++)
    {
        // If current element is smaller
        // than or equal to pivot
        if (arr[j] <= pivot)
        {
            i++; // increment index of
                 // smaller element
            Swap(arr, i, j);
        }
    }
    Swap(arr, i + 1, high);
    return (i + 1);
}

/* The main function that
   implements QuickSort
arr[] --> Array to be sorted,
low --> Starting index,
high --> Ending index */
static void quickSort(int []arr, int low,
                                 int high)
{
    if (low < high)
    {
        /* pi is partitioning index,
        arr[p] is now at right place */
        int pi = partition(arr, low, high);

        // Separately sort elements before
        // partition and after partition
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}

/* Function to print an array */
static void printArray(int []arr, int size)
{
    int i;
    for (i = 0; i < size; i++)
    Console.Write(" " + arr[i]);
    Console.WriteLine();
}

// Driver Code
static public void Main()
{
    int []arr = {10, 7, 8, 9, 1, 5};
    int n = arr.Length;
    quickSort(arr, 0, n-1);
    Console.WriteLine("Sorted array: ");
    printArray(arr, n);
}
}

// This code is contributed by vt_m.
```

## java 描述语言

```
<script>

// JavaScript implementation QuickSort
// using Lomuto's partition Scheme

function Swap(array, position1, position2)
{
    // Swaps elements in an array

    // Copy the first position's element
    let temp = array[position1];

    // Assign to the second element
    array[position1] = array[position2];

    // Assign to the first element
    array[position2] = temp;
}

/* This function takes last element as
pivot, places the pivot element at its
correct position in sorted array, and
places all smaller (smaller than pivot)
to left of pivot and all greater elements
to right of pivot */
function partition(arr, low, high)
{
    let pivot = arr[high];

    // Index of smaller element
    let i = (low - 1);

    for (let j = low; j <= high- 1; j++)
    {
        // If current element is smaller
        // than or equal to pivot
        if (arr[j] <= pivot)
        {
            i++; // increment index of
                 // smaller element
            Swap(arr, i, j);
        }
    }
    Swap(arr, i + 1, high);
    return (i + 1);
}

/* The main function that
   implements QuickSort
arr[] --> Array to be sorted,
low --> Starting index,
high --> Ending index */
function quickSort(arr, low, high)
{
    if (low < high)
    {
        /* pi is partitioning index,
        arr[p] is now at right place */
        let pi = partition(arr, low, high);

        // Separately sort elements before
        // partition and after partition
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}

/* Function to print an array */
function printArray(arr, size)
{
    let i;
    for (i = 0; i < size; i++)
    document.write(" " + arr[i]);
    document.write("<br/>");
}

// Driver Code
    let arr = [10, 7, 8, 9, 1, 5];
    let n = arr.length;
    quickSort(arr, 0, n-1);
    document.write("Sorted array: ");
    printArray(arr, n);

 // This code is contributed by chinmoy1997pal.
</script>
```

**Output**

```
Sorted array: 
1 5 7 8 9 10 
```