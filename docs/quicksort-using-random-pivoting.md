# 使用随机旋转快速排序

> 原文:[https://www . geeksforgeeks . org/quick sort-use-random-pivoting/](https://www.geeksforgeeks.org/quicksort-using-random-pivoting/)

在本文中，我们将讨论如何使用随机旋转来实现[快速排序](https://www.geeksforgeeks.org/quick-sort/)。在快速排序中，我们首先对数组进行适当的划分，这样枢轴元素左侧的所有元素都较小，而枢轴右侧的所有元素都大于枢轴。然后我们递归地对左右子阵列调用相同的过程。
与[合并排序](https://www.geeksforgeeks.org/merge-sort/)不同，我们不需要合并两个排序后的数组。因此，快速排序比合并排序需要更少的辅助空间，这就是为什么它通常更倾向于合并排序。使用随机生成的枢轴，我们可以进一步提高快速排序的时间复杂度。

我们已经讨论了两种常用的数组分区方法- [霍尔 vs 洛姆托分区方案](https://www.geeksforgeeks.org/hoares-vs-lomuto-partition-scheme-quicksort/)
建议读者已经阅读了那篇文章，或者知道如何使用这两种分区方案中的任何一种来实现快速排序。

**<u>使用 Lomuto 分区进行随机旋转的算法</u>**

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

partition_r(arr[], lo, hi)
    r = Random Number from lo to hi
    Swap arr[r] and arr[hi]
    return partition(arr, lo, hi)

quicksort(arr[], lo, hi)
    if lo < hi
        p = partition_r(arr, lo, hi)
        quicksort(arr, lo , p-1)
        quicksort(arr, p+1, hi)
```

**<u>使用 Lomuto 分区实现:</u>**

## C++

```
// C++ implementation QuickSort
// using Lomuto's partition Scheme.
#include <cstdlib>
#include <time.h>
#include <iostream>
using namespace std;

// This function takes last element
// as pivot, places
// the pivot element at its correct
// position in sorted array, and
// places all smaller (smaller than pivot)
// to left of pivot and all greater
// elements to right of pivot
int partition(int arr[], int low, int high)
{
    // pivot
    int pivot = arr[high];

    // Index of smaller element
    int i = (low - 1);

    for (int j = low; j <= high - 1; j++)
    {
        // If current element is smaller
        // than or equal to pivot
        if (arr[j] <= pivot) {

            // increment index of
            // smaller element
            i++;
            swap(arr[i], arr[j]);
        }
    }
    swap(arr[i + 1], arr[high]);
    return (i + 1);
}

// Generates Random Pivot, swaps pivot with
// end element and calls the partition function
int partition_r(int arr[], int low, int high)
{
    // Generate a random number in between
    // low .. high
    srand(time(NULL));
    int random = low + rand() % (high - low);

    // Swap A[random] with A[high]
    swap(arr[random], arr[high]);

    return partition(arr, low, high);
}

/* The main function that implements
QuickSort
arr[] --> Array to be sorted,
low --> Starting index,
high --> Ending index */
void quickSort(int arr[], int low, int high)
{
    if (low < high) {

        /* pi is partitioning index,
        arr[p] is now
        at right place */
        int pi = partition_r(arr, low, high);

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
    for (i = 0; i < size; i++)
        cout<<arr[i]<<" ";
}

// Driver Code
int main()
{
    int arr[] = { 10, 7, 8, 9, 1, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);

    quickSort(arr, 0, n - 1);
    printf("Sorted array: \n");
    printArray(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to illustrate
// Randomised Quick Sort
import java.util.*;

class RandomizedQsort
{    
    // This Function helps in calculating
    // random numbers between low(inclusive)
    // and high(inclusive)
    static void random(int arr[],int low,int high)
    {

        Random rand= new Random();
        int pivot = rand.nextInt(high-low)+low;

        int temp1=arr[pivot]; 
        arr[pivot]=arr[high];
        arr[high]=temp1;
    }

    /* This function takes last element as pivot,
    places the pivot element at its correct
    position in sorted array, and places all
    smaller (smaller than pivot) to left of
    pivot and all greater elements to right
    of pivot */
    static int partition(int arr[], int low, int high)
    {
        // pivot is chosen randomly
        random(arr,low,high);
        int pivot = arr[high];

        int i = (low-1); // index of smaller element
        for (int j = low; j < high; j++)
        {
            // If current element is smaller than or
            // equal to pivot
            if (arr[j] < pivot)
            {
                i++;

                // swap arr[i] and arr[j]
                int temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }
        }

        // swap arr[i+1] and arr[high] (or pivot)
        int temp = arr[i+1];
        arr[i+1] = arr[high];
        arr[high] = temp;

        return i+1;
    }

    /* The main function that implements QuickSort()
    arr[] --> Array to be sorted,
    low --> Starting index,
    high --> Ending index */
    static void sort(int arr[], int low, int high)
    {
        if (low < high)
        {
            /* pi is partitioning index, arr[pi] is
            now at right place */
            int pi = partition(arr, low, high);

            // Recursively sort elements before
            // partition and after partition
            sort(arr, low, pi-1);
            sort(arr, pi+1, high);
        }
    }

    /* A utility function to print array of size n */
    static void printArray(int arr[])
    {
        int n = arr.length;
        for (int i = 0; i < n; ++i)
            System.out.print(arr[i]+" ");
        System.out.println();
    }

    // Driver Code
    public static void main(String args[])
    {
        int arr[] = {10, 7, 8, 9, 1, 5};
        int n = arr.length;

        sort(arr, 0, n-1);

        System.out.println("Sorted array");
        printArray(arr);
    }
}

// This code is contributed by Ritika Gupta.
```

## 蟒蛇 3

```
# Python implementation QuickSort using
# Lomuto's partition Scheme.
import random

'''
The function which implements QuickSort.
arr :- array to be sorted.
start :- starting index of the array.
stop :- ending index of the array.
'''
def quicksort(arr, start , stop):
    if(start < stop):

        # pivotindex is the index where
        # the pivot lies in the array
        pivotindex = partitionrand(arr,\
                             start, stop)

        # At this stage the array is
        # partially sorted around the pivot.
        # Separately sorting the
        # left half of the array and the
        # right half of the array.
        quicksort(arr , start , pivotindex-1)
        quicksort(arr, pivotindex + 1, stop)

# This function generates random pivot,
# swaps the first element with the pivot
# and calls the partition function.
def partitionrand(arr , start, stop):

    # Generating a random number between the
    # starting index of the array and the
    # ending index of the array.
    randpivot = random.randrange(start, stop)

    # Swapping the starting element of
    # the array and the pivot
    arr[start], arr[randpivot] = \
        arr[randpivot], arr[start]
    return partition(arr, start, stop)

'''
This function takes the first element as pivot,
places the pivot element at the correct position
in the sorted array. All the elements are re-arranged
according to the pivot, the elements smaller than the
pivot is places on the left and the elements
greater than the pivot is placed to the right of pivot.
'''
def partition(arr,start,stop):
    pivot = start # pivot

    # a variable to memorize where the
    i = start + 1

    # partition in the array starts from.
    for j in range(start + 1, stop + 1):

        # if the current element is smaller
        # or equal to pivot, shift it to the
        # left side of the partition.
        if arr[j] <= arr[pivot]:
            arr[i] , arr[j] = arr[j] , arr[i]
            i = i + 1
    arr[pivot] , arr[i - 1] =\
            arr[i - 1] , arr[pivot]
    pivot = i - 1
    return (pivot)

# Driver Code
if __name__ == "__main__":
    array = [10, 7, 8, 9, 1, 5]
    quicksort(array, 0, len(array) - 1)
    print(array)

# This code is contributed by soumyasaurav
```

## C#

```
// C# program to illustrate
// Randomised Quick sort
using System;
class RandomizedQsort
{    

  /* This function takes last element as pivot,
    places the pivot element at its correct
    position in sorted array, and places all
    smaller (smaller than pivot) to left of
    pivot and all greater elements to right
    of pivot */
  static int partition(int[] arr, int low, int high)
  {

    // pivot is chosen randomly
    random(arr, low, high);
    int pivot = arr[high];

    int i = (low-1); // index of smaller element
    for (int j = low; j < high; j++)
    {

      // If current element is smaller than or
      // equal to pivot
      if (arr[j] < pivot)
      {
        i++;

        // swap arr[i] and arr[j]
        int tempp = arr[i];
        arr[i] = arr[j];
        arr[j] = tempp;
      }
    }

    // swap arr[i+1] and arr[high] (or pivot)
    int tempp2 = arr[i + 1];
    arr[i + 1] = arr[high];
    arr[high] = tempp2;

    return i + 1;
  }

  // This Function helps in calculating
  // random numbers between low(inclusive)
  // and high(inclusive)
  static int random(int[] arr, int low, int high)
  {

    Random rand = new Random();
    int pivot = rand.Next() % (high - low) + low;

    int tempp1 = arr[pivot]; 
    arr[pivot] = arr[high];
    arr[high] = tempp1;

    return partition(arr, low, high);
  }

  /* The main function that implements Quicksort()
    arr[] --> Array to be sorted,
    low --> Starting index,
    high --> Ending index */
  static void sort(int[] arr, int low, int high)
  {
    if (low < high)
    {
      /* pi is partitioning index, arr[pi] is
            now at right place */
      int pi = partition(arr, low, high);

      // Recursively sort elements before
      // partition and after partition
      sort(arr, low, pi - 1);
      sort(arr, pi + 1, high);
    }
  }

  /* A utility function to print array of size n */
  static void printArray(int[] arr)
  {
    int n = arr.Length;
    for (int i = 0; i < n; ++i)
      Console.Write(arr[i] + " ");
    Console.WriteLine();
  }

  // Driver Code
  static public void Main ()
  {
    int[] arr = {10, 7, 8, 9, 1, 5};
    int n = arr.Length;

    sort(arr, 0, n-1);

    Console.WriteLine("sorted array");
    printArray(arr);
  }
}

//  This code is contributed by shubhamsingh10
```

**Output**

```
Sorted array: 
1 5 7 8 9 10 
```

**<u>使用霍尔分割进行随机旋转的算法</u>**

```
partition(arr[], lo, hi)
   pivot = arr[lo]
   i = lo - 1  // Initialize left index
   j = hi + 1  // Initialize right index

    while(True)
           // Find a value in left side greater than pivot
           do
              i = i + 1
           while arr[i] < pivot
        // Find a value in right side smaller than pivot
           do
              j = j - 1
           while arr[j] > pivot

           if i >= j then  
              return j
        else
               swap arr[i] with arr[j]
       end    while

partition_r(arr[], lo, hi)
    r = Random number from lo to hi
    Swap arr[r] and arr[lo]
    return partition(arr, lo, hi)

quicksort(arr[], lo, hi)
    if lo < hi
        p = partition_r(arr, lo, hi)
        quicksort(arr, lo, p)
        quicksort(arr, p+1, hi)
```

**<u>使用霍尔分区实现:</u>**

## C++

```
// C++ implementation of QuickSort
// using Hoare's partition scheme

#include <cstdlib>
#include <iostream>
using namespace std;

// This function takes last element as
// pivot, places the pivot element at
// its correct position in sorted
// array, and places all smaller
// (smaller than pivot) to left of pivot
// and all greater elements to right
int partition(int arr[], int low, int high)
{
    int pivot = arr[low];
    int i = low - 1, j = high + 1;

    while (true) {

        // Find leftmost element greater than
        // or equal to pivot
        do {
            i++;
        } while (arr[i] < pivot);

        // Find rightmost element smaller than
        // or equal to pivot
        do {
            j--;
        } while (arr[j] > pivot);

        // If two pointers met
        if (i >= j)
            return j;

        swap(arr[i], arr[j]);
    }
}

// Generates Random Pivot, swaps pivot with
// end element and calls the partition function
// In Hoare partition the low element is selected
// as first pivot
int partition_r(int arr[], int low, int high)
{
    // Generate a random number in between
    // low .. high
    srand(time(NULL));
    int random = low + rand() % (high - low);

    // Swap A[random] with A[high]
    swap(arr[random], arr[low]);

    return partition(arr, low, high);
}

// The main function that implements QuickSort
// arr[] --> Array to be sorted,
// low  --> Starting index,
// high  --> Ending index
void quickSort(int arr[], int low, int high)
{
    if (low < high) {
        // pi is partitioning index,
        // arr[p] is now at right place
        int pi = partition_r(arr, low, high);

        // Separately sort elements before
        // partition and after partition
        quickSort(arr, low, pi);
        quickSort(arr, pi + 1, high);
    }
}

// Function to print an array
void printArray(int arr[], int n)
{
    for (int i = 0; i < n; i++)
        printf("%d ", arr[i]);
    printf("\n");
}

// Driver Code
int main()
{
    int arr[] = { 10, 7, 8, 9, 1, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);
    quickSort(arr, 0, n - 1);
    printf("Sorted array: \n");
    printArray(arr, n);
    return 0;
}
```

## 蟒蛇 3

```
# Python implementation QuickSort using
# Hoare's partition Scheme.

import random

'''
The function which implements randomised
QuickSort, using Haore's partition scheme.
arr :- array to be sorted.
start :- starting index of the array.
stop :- ending index of the array.
'''
def quicksort(arr, start, stop):
    if(start < stop):

        # pivotindex is the index where
        # the pivot lies in the array
        pivotindex = partitionrand(arr,\
                              start, stop)

        # At this stage the array is
        # partially sorted around the pivot.
        # separately sorting the left half of
        # the array and the right
        # half of the array.
        quicksort(arr , start , pivotindex)
        quicksort(arr, pivotindex + 1, stop)

# This function generates random pivot,
# swaps the first element with the pivot
# and calls the partition function.
def partitionrand(arr , start, stop):

    # Generating a random number between
    # the starting index of the array and
    # the ending index of the array.
    randpivot = random.randrange(start, stop)

    # Swapping the starting element of
    # the array and the pivot
    arr[start], arr[randpivot] =\
        arr[randpivot], arr[start]
    return partition(arr, start, stop)

'''
This function takes the first element
as pivot, places the pivot element at
the correct position in the sorted array.
All the elements are re-arranged according
to the pivot, the elements smaller than
the pivot is places on the left and
the elements greater than the pivot is
placed to the right of pivot.
'''
def partition(arr,start,stop):
    pivot = start # pivot
    i = start - 1
    j = stop + 1
    while True:
        while True:
            i = i + 1
            if arr[i] >= arr[pivot]:
                break
        while True:
            j = j - 1
            if arr[j] <= arr[pivot]:
                break
        if i >= j:
            return j
        arr[i] , arr[j] = arr[j] , arr[i]

# Driver Code
if __name__ == "__main__":
    array = [10, 7, 8, 9, 1, 5]
    quicksort(array, 0, len(array) - 1)
    print(array)

# This code is contributed by soumyasaurav
```

**Output**

```
Sorted array: 
1 5 7 8 9 10 
```

[随机快速排序分析](https://www.geeksforgeeks.org/randomized-algorithms-set-1-introduction-and-analysis/)

**注释**

*   使用随机旋转，我们将预期或平均时间复杂度提高到 0(N ^ log N)。最坏情况下的复杂性仍然是 O ( N^2)。