# 迭代合并排序

> 原文:[https://www.geeksforgeeks.org/iterative-merge-sort/](https://www.geeksforgeeks.org/iterative-merge-sort/)

以下是[合并排序](http://geeksquiz.com/merge-sort/)的典型递归实现

## C++

```
// Recursive C++ program for merge sort
#include<bits/stdc++.h>
using namespace std;

// Function to merge the two haves
// arr[l..m] and arr[m+1..r] of array arr[]
void merge(int arr[], int l, int m, int r);

// l is for left index and r is
// right index of the sub-array
// of arr to be sorted
void mergeSort(int arr[], int l, int r)
{
    if (l < r)
    {

        // Same as (l+r)/2 but avoids
        // overflow for large l & h
        int m = l + (r - l) / 2;
        mergeSort(arr, l, m);
        mergeSort(arr, m + 1, r);
        merge(arr, l, m, r);
    }
}

// Function to merge the two haves arr[l..m]
// and arr[m+1..r] of array arr[]
void merge(int arr[], int l, int m, int r)
{
    int k;
    int n1 = m - l + 1;
    int n2 =  r - m;

    // Create temp arrays
    int L[n1], R[n2];

    // Copy data to temp arrays L[] and R[]
    for(int i = 0; i < n1; i++)
        L[i] = arr[l + i];
    for(int j = 0; j < n2; j++)
        R[j] = arr[m + 1+ j];

    // Merge the temp arrays
    // back into arr[l..r]
    int i = 0;
    int j = 0;
    k = l;

    while (i < n1 && j < n2)
    {
        if (L[i] <= R[j])
        {
            arr[k] = L[i];
            i++;
        }
        else
        {
            arr[k] = R[j];
            j++;
        }
        k++;
    }

    // Copy the remaining elements
    // of L[], if there are any
    while (i < n1)
    {
        arr[k] = L[i];
        i++;
        k++;
    }

    // Copy the remaining elements
    // of R[], if there are any
    while (j < n2)
    {
        arr[k] = R[j];
        j++;
        k++;
    }
}

// Function to print an array
void printArray(int A[], int size)
{
    for(int i = 0; i < size; i++)
        printf("%d ", A[i]);

    cout << "\n";
}

// Driver code
int main()
{
    int arr[] = { 12, 11, 13, 5, 6, 7 };
    int arr_size = sizeof(arr) / sizeof(arr[0]);

    cout << "Given array is \n";
    printArray(arr, arr_size);

    mergeSort(arr, 0, arr_size - 1);

    cout << "\nSorted array is \n";
    printArray(arr, arr_size);
    return 0;
}

// This code is contributed by Mayank Tyagi
```

## C

```
/* Recursive C program for merge sort */
#include<stdlib.h>
#include<stdio.h>

/* Function to merge the two haves
 arr[l..m] and arr[m+1..r] of array arr[] */
void merge(int arr[], int l, int m, int r);

/* l is for left index and r is
 right index of the sub-array
  of arr to be sorted */
void mergeSort(int arr[], int l, int r)
{
   if (l < r)
   {
      // Same as (l+r)/2 but avoids
      // overflow for large l & h
      int m = l+(r-l)/2;
      mergeSort(arr, l, m);
      mergeSort(arr, m+1, r);
      merge(arr, l, m, r);
   }
}

/* Function to merge the two haves arr[l..m]
 and arr[m+1..r] of array arr[] */
void merge(int arr[], int l, int m, int r)
{
    int i, j, k;
    int n1 = m - l + 1;
    int n2 =  r - m;

    /* create temp arrays */
    int L[n1], R[n2];

    /* Copy data to temp arrays L[] and R[] */
    for (i = 0; i < n1; i++)
        L[i] = arr[l + i];
    for (j = 0; j < n2; j++)
        R[j] = arr[m + 1+ j];

    /* Merge the temp arrays back into arr[l..r]*/
    i = 0;
    j = 0;
    k = l;
    while (i < n1 && j < n2)
    {
        if (L[i] <= R[j])
        {
            arr[k] = L[i];
            i++;
        }
        else
        {
            arr[k] = R[j];
            j++;
        }
        k++;
    }

    /* Copy the remaining elements
    of L[], if there are any */
    while (i < n1)
    {
        arr[k] = L[i];
        i++;
        k++;
    }

    /* Copy the remaining elements
    of R[], if there are any */
    while (j < n2)
    {
        arr[k] = R[j];
        j++;
        k++;
    }
}

/* Function to print an array */
void printArray(int A[], int size)
{
    int i;
    for (i=0; i < size; i++)
        printf("%d ", A[i]);
    printf("\n");
}

/* Driver program to test above functions */
int main()
{
    int arr[] = {12, 11, 13, 5, 6, 7};
    int arr_size = sizeof(arr)/sizeof(arr[0]);

    printf("Given array is \n");
    printArray(arr, arr_size);

    mergeSort(arr, 0, arr_size - 1);

    printf("\nSorted array is \n");
    printArray(arr, arr_size);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Recursive Java Program for merge sort

import java.util.Arrays;
public class GFG
{
    public static void mergeSort(int[] array)
    {
        if(array == null)
        {
            return;
        }

        if(array.length > 1)
        {
            int mid = array.length / 2;

            // Split left part
            int[] left = new int[mid];
            for(int i = 0; i < mid; i++)
            {
                left[i] = array[i];
            }

            // Split right part
            int[] right = new int[array.length - mid];
            for(int i = mid; i < array.length; i++)
            {
                right[i - mid] = array[i];
            }
            mergeSort(left);
            mergeSort(right);

            int i = 0;
            int j = 0;
            int k = 0;

            // Merge left and right arrays
            while(i < left.length && j < right.length)
            {
                if(left[i] < right[j])
                {
                    array[k] = left[i];
                    i++;
                }
                else
                {
                    array[k] = right[j];
                    j++;
                }
                k++;
            }
            // Collect remaining elements
            while(i < left.length)
            {
                array[k] = left[i];
                i++;
                k++;
            }
            while(j < right.length)
            {
                array[k] = right[j];
                j++;
                k++;
            }
        }
    }

    // Driver program to test above functions.
    public static void main(String[] args)
    {
        int arr[] = {12, 11, 13, 5, 6, 7};
        int i=0;
        System.out.println("Given array is");

        for(i=0; i<arr.length; i++)
            System.out.print(arr[i]+" ");

        mergeSort(arr);

        System.out.println("\n");
        System.out.println("Sorted array is");

        for(i=0; i<arr.length; i++)
            System.out.print(arr[i]+" ");
    }
}

// Code Contributed by Mohit Gupta_OMG
```

## 蟒蛇 3

```
# Recursive Python Program for merge sort

def merge(left, right):
    if not len(left) or not len(right):
        return left or right

    result = []
    i, j = 0, 0
    while (len(result) < len(left) + len(right)):
        if left[i] < right[j]:
            result.append(left[i])
            i+= 1
        else:
            result.append(right[j])
            j+= 1
        if i == len(left) or j == len(right):
            result.extend(left[i:] or right[j:])
            break

    return result

def mergesort(list):
    if len(list) < 2:
        return list

    middle = int(len(list)/2)
    left = mergesort(list[:middle])
    right = mergesort(list[middle:])

    return merge(left, right)

seq = [12, 11, 13, 5, 6, 7]
print("Given array is")
print(seq);
print("\n")
print("Sorted array is")
print(mergesort(seq))

# Code Contributed by Mohit Gupta_OMG
```

## C#

```
/* Iterative C# program for merge
sort */
using System;

class GFG {

    /* l is for left index and r
    is right index of the sub-array
    of arr to be sorted */
    static void mergeSort(int[] arr,
                           int l, int r)
    {
        if (l < r)
        {

            // Same as (l+r)/2 but avoids
            // overflow for large l & h
            int m = l + (r - l) / 2;
            mergeSort(arr, l, m);
            mergeSort(arr, m+1, r);
            merge(arr, l, m, r);
       }
    }

    /* Function to merge the two haves
    arr[l..m] and arr[m+1..r] of array
    arr[] */
    static void merge(int[] arr, int l,
                           int m, int r)
    {
        int i, j, k;
        int n1 = m - l + 1;
        int n2 = r - m;

        /* create temp arrays */
        int []L = new int[n1];
        int []R = new int[n2];

        /* Copy data to temp arrays
        L[] and R[] */
        for (i = 0; i < n1; i++)
            L[i] = arr[l + i];
        for (j = 0; j < n2; j++)
            R[j] = arr[m + 1+ j];

        /* Merge the temp arrays back
        into arr[l..r]*/
        i = 0;
        j = 0;
        k = l;
        while (i < n1 && j < n2)
        {
            if (L[i] <= R[j])
            {
                arr[k] = L[i];
                i++;
            }
            else
            {
                arr[k] = R[j];
                j++;
            }
            k++;
        }

        /* Copy the remaining elements of
        L[], if there are any */
        while (i < n1)
        {
            arr[k] = L[i];
            i++;
            k++;
        }

        /* Copy the remaining elements of
        R[], if there are any */
        while (j < n2)
        {
            arr[k] = R[j];
            j++;
            k++;
        }
    }

    /* Function to print an array */
    static void printArray(int []A, int size)
    {
        int i;
        for (i=0; i < size; i++)
            Console.Write(A[i]+" ");
        Console.Write("\n");
    }

    /* Driver program to test above functions */
    public static void Main()
    {
        int []arr = {12, 11, 13, 5, 6, 7};
        int arr_size = arr.Length;

        Console.Write("Given array is \n");
        printArray(arr, arr_size);

        mergeSort(arr, 0, arr_size - 1);

        Console.Write("\nSorted array is \n");
        printArray(arr, arr_size);
    }
}

// This code is contributed by Smitha
```

## java 描述语言

```
<script>

// Recursive javascript Program for merge sort

    function mergeSort(array) {
        if (array == null) {
            return;
        }

        if (array.length > 1) {
            var mid = parseInt(array.length / 2);

            // Split left part
            var left = Array(mid).fill(0);
            for (i = 0; i < mid; i++) {
                left[i] = array[i];
            }

            // Split right part
            var right = Array(array.length - mid).fill(0);
            for (i = mid; i < array.length; i++) {
                right[i - mid] = array[i];
            }
            mergeSort(left);
            mergeSort(right);

            var i = 0;
            var j = 0;
            var k = 0;

            // Merge left and right arrays
            while (i < left.length && j < right.length) {
                if (left[i] < right[j]) {
                    array[k] = left[i];
                    i++;
                } else {
                    array[k] = right[j];
                    j++;
                }
                k++;
            }
            // Collect remaining elements
            while (i < left.length) {
                array[k] = left[i];
                i++;
                k++;
            }
            while (j < right.length) {
                array[k] = right[j];
                j++;
                k++;
            }
        }
    }

    // Driver program to test above functions.

        var arr = [ 12, 11, 13, 5, 6, 7 ];
        var i = 0;
        document.write("Given array is<br/>");

        for (i = 0; i < arr.length; i++)
            document.write(arr[i] + " ");

        mergeSort(arr);

        document.write("<br/><br/>");
        document.write("Sorted array is<br/>");

        for (i = 0; i < arr.length; i++)
            document.write(arr[i] + " ");

// This code is contributed by umadevi9616

</script>
```

**输出:**

```
Given array is
12 11 13 5 6 7

Sorted array is
5 6 7 11 12 13
```

**迭代合并排序:**
上述函数是递归的，所以使用[函数调用栈](http://en.wikipedia.org/wiki/Call_stack)来存储 l 和 h 的中间值，函数调用栈将其他记账信息和参数一起存储。此外，函数调用涉及到一些开销，比如存储调用方函数的激活记录，然后恢复执行。与[迭代快速排序](https://www.geeksforgeeks.org/iterative-quick-sort/)不同，迭代合并排序不需要显式的辅助栈。

注意:在迭代合并排序中，我们采用自下而上的方法，即从 2 个元素大小的数组开始(我们知道 1 个元素大小的数组已经排序)。同样关键的一点是，由于我们不知道如何像自上而下的方法那样精确地划分数组，其中 2 元素大小的数组可能具有大小序列 2，1，2，2，1…我们在自下而上的方法中假设数组被 2 的幂(n/2，n/4…)精确地划分。等等),例如:n=2，4，8，16。
所以对于其他的输入大小，比如 5，7，11，我们将会有剩余的子列表，当我们继续合并和向上的时候，这些子列表在每一级都没有进入 2 的幂宽度，这个大小不是 2 的精确幂的未合并的子列表将会保持隔离，直到最后的合并。
要在最终合并时合并这个未合并的列表，我们需要强制 mid 位于未合并列表的开头，以便它成为合并的候选列表。

在使用余数(n %宽度)找到最终合并调用之前，将被隔离的未合并子列表元素计数。最终的合并(当我们有不均匀的列表时)可以通过(宽度> n/2)来识别。

因为当 width == n/2 时，width 以 2 的幂增长，那么这意味着输入的大小已经是 2 的幂，否则如果 width < n/2 then we haven’t reached final merge yet, so when width > n/2，我们一定有未合并的不平衡列表，因此我们只在这种情况下重置 mid。

上述函数可以很容易地转换为迭代版本。下面是迭代合并排序。

## C++

```
/* Iterative C program for merge sort */
#include <bits/stdc++.h>
using namespace std;

/* Function to merge the two haves arr[l..m] and arr[m+1..r] of array arr[] */
void merge(int arr[], int l, int m, int r);

// Utility function to find minimum of two integers
int min(int x, int y) { return (x<y)? x :y; }

/* Iterative mergesort function to sort arr[0...n-1] */
void mergeSort(int arr[], int n)
{
   int curr_size;  // For current size of subarrays to be merged
                   // curr_size varies from 1 to n/2
   int left_start; // For picking starting index of left subarray
                   // to be merged

   // Merge subarrays in bottom up manner.  First merge subarrays of
   // size 1 to create sorted subarrays of size 2, then merge subarrays
   // of size 2 to create sorted subarrays of size 4, and so on.
   for (curr_size=1; curr_size<=n-1; curr_size = 2*curr_size)
   {
       // Pick starting point of different subarrays of current size
       for (left_start=0; left_start<n-1; left_start += 2*curr_size)
       {
           // Find ending point of left subarray. mid+1 is starting
           // point of right
           int mid = min(left_start + curr_size - 1, n-1);

           int right_end = min(left_start + 2*curr_size - 1, n-1);

           // Merge Subarrays arr[left_start...mid] & arr[mid+1...right_end]
           merge(arr, left_start, mid, right_end);
       }
   }
}

/* Function to merge the two haves arr[l..m] and arr[m+1..r] of array arr[] */
void merge(int arr[], int l, int m, int r)
{
    int i, j, k;
    int n1 = m - l + 1;
    int n2 =  r - m;

    /* create temp arrays */
    int L[n1], R[n2];

    /* Copy data to temp arrays L[] and R[] */
    for (i = 0; i < n1; i++)
        L[i] = arr[l + i];
    for (j = 0; j < n2; j++)
        R[j] = arr[m + 1+ j];

    /* Merge the temp arrays back into arr[l..r]*/
    i = 0;
    j = 0;
    k = l;
    while (i < n1 && j < n2)
    {
        if (L[i] <= R[j])
        {
            arr[k] = L[i];
            i++;
        }
        else
        {
            arr[k] = R[j];
            j++;
        }
        k++;
    }

    /* Copy the remaining elements of L[], if there are any */
    while (i < n1)
    {
        arr[k] = L[i];
        i++;
        k++;
    }

    /* Copy the remaining elements of R[], if there are any */
    while (j < n2)
    {
        arr[k] = R[j];
        j++;
        k++;
    }
}

/* Function to print an array */
void printArray(int A[], int size)
{
    int i;
    for (i=0; i < size; i++)
        cout <<" "<< A[i];
    cout <<"\n";
}

/* Driver program to test above functions */
int main()
{
    int arr[] = {12, 11, 13, 5, 6, 7};
    int n = sizeof(arr)/sizeof(arr[0]);

    cout <<"Given array is \n ";
    printArray(arr, n);

    mergeSort(arr, n);

    cout <<"\nSorted array is \n ";
    printArray(arr, n);
    return 0;
}
// This code is contributed shivanisinghss2110
```

## C

```
/* Iterative C program for merge sort */
#include<stdlib.h>
#include<stdio.h>

/* Function to merge the two haves arr[l..m] and arr[m+1..r] of array arr[] */
void merge(int arr[], int l, int m, int r);

// Utility function to find minimum of two integers
int min(int x, int y) { return (x<y)? x :y; }

/* Iterative mergesort function to sort arr[0...n-1] */
void mergeSort(int arr[], int n)
{
   int curr_size;  // For current size of subarrays to be merged
                   // curr_size varies from 1 to n/2
   int left_start; // For picking starting index of left subarray
                   // to be merged

   // Merge subarrays in bottom up manner.  First merge subarrays of
   // size 1 to create sorted subarrays of size 2, then merge subarrays
   // of size 2 to create sorted subarrays of size 4, and so on.
   for (curr_size=1; curr_size<=n-1; curr_size = 2*curr_size)
   {
       // Pick starting point of different subarrays of current size
       for (left_start=0; left_start<n-1; left_start += 2*curr_size)
       {
           // Find ending point of left subarray. mid+1 is starting
           // point of right
           int mid = min(left_start + curr_size - 1, n-1);

           int right_end = min(left_start + 2*curr_size - 1, n-1);

           // Merge Subarrays arr[left_start...mid] & arr[mid+1...right_end]
           merge(arr, left_start, mid, right_end);
       }
   }
}

/* Function to merge the two haves arr[l..m] and arr[m+1..r] of array arr[] */
void merge(int arr[], int l, int m, int r)
{
    int i, j, k;
    int n1 = m - l + 1;
    int n2 =  r - m;

    /* create temp arrays */
    int L[n1], R[n2];

    /* Copy data to temp arrays L[] and R[] */
    for (i = 0; i < n1; i++)
        L[i] = arr[l + i];
    for (j = 0; j < n2; j++)
        R[j] = arr[m + 1+ j];

    /* Merge the temp arrays back into arr[l..r]*/
    i = 0;
    j = 0;
    k = l;
    while (i < n1 && j < n2)
    {
        if (L[i] <= R[j])
        {
            arr[k] = L[i];
            i++;
        }
        else
        {
            arr[k] = R[j];
            j++;
        }
        k++;
    }

    /* Copy the remaining elements of L[], if there are any */
    while (i < n1)
    {
        arr[k] = L[i];
        i++;
        k++;
    }

    /* Copy the remaining elements of R[], if there are any */
    while (j < n2)
    {
        arr[k] = R[j];
        j++;
        k++;
    }
}

/* Function to print an array */
void printArray(int A[], int size)
{
    int i;
    for (i=0; i < size; i++)
        printf("%d ", A[i]);
    printf("\n");
}

/* Driver program to test above functions */
int main()
{
    int arr[] = {12, 11, 13, 5, 6, 7};
    int n = sizeof(arr)/sizeof(arr[0]);

    printf("Given array is \n");
    printArray(arr, n);

    mergeSort(arr, n);

    printf("\nSorted array is \n");
    printArray(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Iterative Java program for merge sort */
import java.lang.Math.*;

class GFG {

    /* Iterative mergesort function to sor
    t arr[0...n-1] */
    static void mergeSort(int arr[], int n)
    {

        // For current size of subarrays to
        // be merged curr_size varies from
        // 1 to n/2
        int curr_size;

        // For picking starting index of
        // left subarray to be merged
        int left_start;

        // Merge subarrays in bottom up
        // manner. First merge subarrays
        // of size 1 to create sorted
        // subarrays of size 2, then merge
        // subarrays of size 2 to create
        // sorted subarrays of size 4, and
        // so on.
        for (curr_size = 1; curr_size <= n-1;
                      curr_size = 2*curr_size)
        {

            // Pick starting point of different
            // subarrays of current size
            for (left_start = 0; left_start < n-1;
                        left_start += 2*curr_size)
            {
                // Find ending point of left
                // subarray. mid+1 is starting
                // point of right
                int mid = Math.min(left_start + curr_size - 1, n-1);

                int right_end = Math.min(left_start
                             + 2*curr_size - 1, n-1);

                // Merge Subarrays arr[left_start...mid]
                // & arr[mid+1...right_end]
                merge(arr, left_start, mid, right_end);
            }
        }
    }

    /* Function to merge the two haves arr[l..m] and
    arr[m+1..r] of array arr[] */
    static void merge(int arr[], int l, int m, int r)
    {
        int i, j, k;
        int n1 = m - l + 1;
        int n2 = r - m;

        /* create temp arrays */
        int L[] = new int[n1];
        int R[] = new int[n2];

        /* Copy data to temp arrays L[]
        and R[] */
        for (i = 0; i < n1; i++)
            L[i] = arr[l + i];
        for (j = 0; j < n2; j++)
            R[j] = arr[m + 1+ j];

        /* Merge the temp arrays back into
        arr[l..r]*/
        i = 0;
        j = 0;
        k = l;
        while (i < n1 && j < n2)
        {
            if (L[i] <= R[j])
            {
                arr[k] = L[i];
                i++;
            }
            else
            {
                arr[k] = R[j];
                j++;
            }
            k++;
        }

        /* Copy the remaining elements of
        L[], if there are any */
        while (i < n1)
        {
            arr[k] = L[i];
            i++;
            k++;
        }

        /* Copy the remaining elements of
        R[], if there are any */
        while (j < n2)
        {
            arr[k] = R[j];
            j++;
            k++;
        }
    }

    /* Function to print an array */
    static void printArray(int A[], int size)
    {
        int i;
        for (i=0; i < size; i++)
            System.out.printf("%d ", A[i]);
        System.out.printf("\n");
    }

    /* Driver program to test above functions */
    public static void main(String[] args)
    {
        int arr[] = {12, 11, 13, 5, 6, 7};
        int n = arr.length;

        System.out.printf("Given array is \n");
        printArray(arr, n);

        mergeSort(arr, n);

        System.out.printf("\nSorted array is \n");
        printArray(arr, n);
    }
}

// This code is contributed by Smitha
```

## 蟒蛇 3

```
# Iterative Merge sort (Bottom Up)

# Iterative mergesort function to
# sort arr[0...n-1]

# perform bottom up merge
def mergeSort(a):
    # start with least partition size of 2^0 = 1
    width = 1   
    n = len(a)                                         
    # subarray size grows by powers of 2
    # since growth of loop condition is exponential,
    # time consumed is logarithmic (log2n)
    while (width < n):
        # always start from leftmost
        l=0;
        while (l < n):
            r = min(l+(width*2-1), n-1)
            m = (l+r)//2
            # final merge should consider
            # unmerged sublist if input arr
            # size is not power of 2
            if (width>n//2):       
                m = r-(n%width)  
            merge(a, l, m, r)
            l += width*2
        # Increasing sub array size by powers of 2
        width *= 2
    return a

# Merge Function
def merge(a, l, m, r):
    n1 = m - l + 1
    n2 = r - m
    L = [0] * n1
    R = [0] * n2
    for i in range(0, n1):
        L[i] = a[l + i]
    for i in range(0, n2):
        R[i] = a[m + i + 1]

    i, j, k = 0, 0, l
    while i < n1 and j < n2:
        if L[i] > R[j]:
            a[k] = R[j]
            j += 1
        else:
            a[k] = L[i]
            i += 1
        k += 1

    while i < n1:
        a[k] = L[i]
        i += 1
        k += 1

    while j < n2:
        a[k] = R[j]
        j += 1
        k += 1

# Driver code
a = [12, 11, 13, 5, 6, 7]
print("Given array is ")
print(a)

mergeSort(a)

print("Sorted array is ")
print(a)

# Contributed by Madhur Chhangani [RCOEM]
# corrected and improved by @mahee96
```

## C#

```
/* Iterative C# program for merge sort */
using System;
public class GFG {

    /* Iterative mergesort function to sor
    t arr[0...n-1] */
    static void mergeSort(int []arr, int n)
    {

        // For current size of subarrays to
        // be merged curr_size varies from
        // 1 to n/2
        int curr_size;

        // For picking starting index of
        // left subarray to be merged
        int left_start;

        // Merge subarrays in bottom up
        // manner. First merge subarrays
        // of size 1 to create sorted
        // subarrays of size 2, then merge
        // subarrays of size 2 to create
        // sorted subarrays of size 4, and
        // so on.
        for (curr_size = 1; curr_size <= n-1;
                      curr_size = 2*curr_size)
        {

            // Pick starting point of different
            // subarrays of current size
            for (left_start = 0; left_start < n-1;
                        left_start += 2*curr_size)
            {
                // Find ending point of left
                // subarray. mid+1 is starting
                // point of right
                int mid = left_start + curr_size - 1;

                int right_end = Math.Min(left_start
                             + 2*curr_size - 1, n-1);

                // Merge Subarrays arr[left_start...mid]
                // & arr[mid+1...right_end]
                merge(arr, left_start, mid, right_end);
            }
        }
    }

    /* Function to merge the two haves arr[l..m] and
    arr[m+1..r] of array arr[] */
    static void merge(int []arr, int l, int m, int r)
    {
        int i, j, k;
        int n1 = m - l + 1;
        int n2 = r - m;

        /* create temp arrays */
        int []L = new int[n1];
        int []R = new int[n2];

        /* Copy data to temp arrays L[]
        and R[] */
        for (i = 0; i < n1; i++)
            L[i] = arr[l + i];
        for (j = 0; j < n2; j++)
            R[j] = arr[m + 1+ j];

        /* Merge the temp arrays back into
        arr[l..r]*/
        i = 0;
        j = 0;
        k = l;
        while (i < n1 && j < n2)
        {
            if (L[i] <= R[j])
            {
                arr[k] = L[i];
                i++;
            }
            else
            {
                arr[k] = R[j];
                j++;
            }
            k++;
        }

        /* Copy the remaining elements of
        L[], if there are any */
        while (i < n1)
        {
            arr[k] = L[i];
            i++;
            k++;
        }

        /* Copy the remaining elements of
        R[], if there are any */
        while (j < n2)
        {
            arr[k] = R[j];
            j++;
            k++;
        }
    }

    /* Function to print an array */
    static void printArray(int []A, int size)
    {
        int i;
        for (i=0; i < size; i++)
            Console.Write(A[i]+" ");
        Console.WriteLine("");
    }

    /* Driver program to test above functions */
    public static void Main()
    {
        int []arr = {12, 11, 13, 5, 6, 7};
        int n = arr.Length;

        Console.Write("Given array is \n");
        printArray(arr, n);

        mergeSort(arr, n);

        Console.Write("\nSorted array is \n");
        printArray(arr, n);
    }
}
// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
/* Iterative javascript program for merge sort */

    /*
     * Iterative mergesort function to sor t arr[0...n-1]
     */
    function mergeSort(arr , n) {

        // For current size of subarrays to
        // be merged curr_size varies from
        // 1 to n/2
        var curr_size;

        // For picking starting index of
        // left subarray to be merged
        var left_start;

        // Merge subarrays in bottom up
        // manner. First merge subarrays
        // of size 1 to create sorted
        // subarrays of size 2, then merge
        // subarrays of size 2 to create
        // sorted subarrays of size 4, and
        // so on.
        for (curr_size = 1; curr_size <= n - 1; curr_size = 2 * curr_size) {

            // Pick starting point of different
            // subarrays of current size
            for (left_start = 0; left_start < n - 1; left_start += 2 * curr_size) {
                // Find ending point of left
                // subarray. mid+1 is starting
                // point of right
                var mid = Math.min(left_start + curr_size - 1, n - 1);

                var right_end = Math.min(left_start + 2 * curr_size - 1, n - 1);

                // Merge Subarrays arr[left_start...mid]
                // & arr[mid+1...right_end]
                merge(arr, left_start, mid, right_end);
            }
        }
    }

    /*
     * Function to merge the two haves arr[l..m] and arr[m+1..r] of array arr
     */
    function merge(arr , l , m , r) {
        var i, j, k;
        var n1 = m - l + 1;
        var n2 = r - m;

        /* create temp arrays */
        var L = Array(n1).fill(0);
        var R = Array(n2).fill(0);

        /*
         * Copy data to temp arrays L and R
         */
        for (i = 0; i < n1; i++)
            L[i] = arr[l + i];
        for (j = 0; j < n2; j++)
            R[j] = arr[m + 1 + j];

        /*
         * Merge the temp arrays back into arr[l..r]
         */
        i = 0;
        j = 0;
        k = l;
        while (i < n1 && j < n2) {
            if (L[i] <= R[j]) {
                arr[k] = L[i];
                i++;
            } else {
                arr[k] = R[j];
                j++;
            }
            k++;
        }

        /*
         * Copy the remaining elements of L, if there are any
         */
        while (i < n1) {
            arr[k] = L[i];
            i++;
            k++;
        }

        /*
         * Copy the remaining elements of R, if there are any
         */
        while (j < n2) {
            arr[k] = R[j];
            j++;
            k++;
        }
    }

    /* Function to print an array */
    function printArray(A , size) {
        var i;
        for (i = 0; i < size; i++)
            document.write( A[i]+" ");
        document.write("<br/>");
    }

    /* Driver program to test above functions */

        var arr = [ 12, 11, 13, 5, 6, 7 ];
        var n = arr.length;

        document.write("Given array is <br/>");
        printArray(arr, n);

        mergeSort(arr, n);

        document.write("<br/>Sorted array is <br/>");
        printArray(arr, n);

// This code contributed by umadevi9616
</script>
```

**输出:**

```
Given array is
12 11 13 5 6 7

Sorted array is
5 6 7 11 12 13
```

上述迭代函数的时间复杂度与递归相同，即θ(nLogn)。

**参考文献:**
http://csg.sph.umich.edu/abecasis/class/2006/615.09.pdf
本文由 **Shivam Agrawal** 供稿。如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息