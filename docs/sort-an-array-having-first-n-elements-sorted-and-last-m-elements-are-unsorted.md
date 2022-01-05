# 排序前 N 个元素已排序，后 M 个元素未排序的数组

> 原文:[https://www . geesforgeks . org/sort-a-array-first-n-elements-sorted-and-last-m-elements-unsorted/](https://www.geeksforgeeks.org/sort-an-array-having-first-n-elements-sorted-and-last-m-elements-are-unsorted/)

给定两个正整数 **N** 和 **M** ，以及一个由 **(N + M)** 整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，使得第一个 **N** 元素按 [**升序排序**](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/) ，最后一个 **M** 元素未排序，任务是[按升序排序给定数组](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)。

**示例:**

> **输入:** N = 3，M = 5，arr[] = {2，8，10，17，15，23，4，12}
> **输出:** 2 4 8 10 12 15 17 23
> 
> **输入:** N = 4，M = 3，arr[] = {4，7，9，11，10，5，17 }
> T3】输出: 4 5 7 9 10 11 17

**天真方法:**解决给定问题最简单的方法是使用[内置的 sort()函数](https://www.geeksforgeeks.org/sort-c-stl/)对给定数组进行[排序。](https://www.geeksforgeeks.org/sorting-algorithms/)

***时间复杂度:**O((N+M)log(N+M))*
***辅助空间:** O(1)*

**高效方式:**上述方式也可以利用[合并排序](https://www.geeksforgeeks.org/merge-sort/)的思路进行优化。其思想是对最后一个 **M** 数组元素执行合并排序操作，然后对数组的第一个 **N** 和最后一个 **M** 元素使用[合并两个排序数组](https://www.geeksforgeeks.org/merge-two-sorted-arrays/)的概念。按照以下步骤解决问题:

*   使用本文中讨论的方法，对最后一个 **M** 数组元素执行合并排序操作。
*   经过上述步骤后，子阵列 **arr[1，N]** 和 **arr[N + 1，M]** 按升序排序。
*   使用本文中讨论的方法，合并两个排序的子阵列 **arr[1，N]** 和 **arr[N + 1，M]【T3]。**
*   完成上述步骤后，[打印数组](https://www.geeksforgeeks.org/c-program-to-print-an-array-using-recursion/) **arr[]** 作为结果数组。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <iostream>
using namespace std;

// Function for merging the two sorted
// arrays
void merge(int a[], int l, int m, int r)
{
    int s1 = m - l + 1;
    int s2 = r - m;

    // Create two temp arrays
    int left[s1];
    int right[s2];

    // Copy elements to left array
    for (int i = 0; i < s1; i++)
        left[i] = a[l + i];

    // Copy elements to right array
    for (int j = 0; j < s2; j++)
        right[j] = a[j + m + 1];

    int i = 0, j = 0, k = l;

    // Merge the array back into the
    // array over the range [l, r]
    while (i < s1 && j < s2) {

        // If the current left element
        // is smaller than the current
        // right element
        if (left[i] <= right[j]) {
            a[k] = left[i];
            i++;
        }

        // Otherwise
        else {
            a[k] = right[j];
            j++;
        }
        k++;
    }

    // Copy the remaining elements of
    // the array left[]
    while (i < s1) {
        a[k] = left[i];
        i++;
        k++;
    }

    // Copy the remaining elements of
    // the array right[]
    while (j < s2) {
        a[k] = right[j];
        j++;
        k++;
    }
}

// Function to sort the array over the
// range [l, r]
void mergesort(int arr[], int l, int r)
{
    if (l < r) {

        // Find the middle index
        int mid = l + (r - l) / 2;

        // Recursively call for the
        // two halves
        mergesort(arr, l, mid);
        mergesort(arr, mid + 1, r);

        // Perform the merge operation
        merge(arr, l, mid, r);
    }
}

// Function to sort an array for the
// last m elements are unsorted
void sortlastMElements(int arr[], int N,
                       int M)
{
    int s = M + N - 1;

    // Sort the last m elements
    mergesort(arr, N, s);

    // Merge the two sorted subarrays
    merge(arr, 0, N - 1, N + M - 1);

    // Print the sorted array
    for (int i = 0; i < N + M; i++)
        cout << arr[i] << " ";
}

// Driver Code
int main()
{
    int N = 3;
    int M = 5;
    int arr[] = { 2, 8, 10, 17, 15,
                  23, 4, 12 };
    sortlastMElements(arr, N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function for merging the two sorted
// arrays
static void merge(int a[], int l, int m, int r)
{
    int s1 = m - l + 1;
    int s2 = r - m;

    // Create two temp arrays
    int left[] = new int[s1];
    int right[] = new int[s2];

    // Copy elements to left array
    for (int i = 0; i < s1; i++)
        left[i] = a[l + i];

    // Copy elements to right array
    for (int j = 0; j < s2; j++)
        right[j] = a[j + m + 1];

    int i = 0, j = 0, k = l;

    // Merge the array back into the
    // array over the range [l, r]
    while (i < s1 && j < s2) {

        // If the current left element
        // is smaller than the current
        // right element
        if (left[i] <= right[j]) {
            a[k] = left[i];
            i++;
        }

        // Otherwise
        else {
            a[k] = right[j];
            j++;
        }
        k++;
    }

    // Copy the remaining elements of
    // the array left[]
    while (i < s1) {
        a[k] = left[i];
        i++;
        k++;
    }

    // Copy the remaining elements of
    // the array right[]
    while (j < s2) {
        a[k] = right[j];
        j++;
        k++;
    }
}

// Function to sort the array over the
// range [l, r]
static void mergesort(int arr[], int l, int r)
{
    if (l < r) {

        // Find the middle index
        int mid = l + (r - l) / 2;

        // Recursively call for the
        // two halves
        mergesort(arr, l, mid);
        mergesort(arr, mid + 1, r);

        // Perform the merge operation
        merge(arr, l, mid, r);
    }
}

// Function to sort an array for the
// last m elements are unsorted
static void sortlastMElements(int arr[], int N,
                       int M)
{
    int s = M + N - 1;

    // Sort the last m elements
    mergesort(arr, N, s);

    // Merge the two sorted subarrays
    merge(arr, 0, N - 1, N + M - 1);

    // Print the sorted array
    for (int i = 0; i < N + M; i++)
         System.out.print( arr[i] + " ");
}

// Driver Code
public static void main(String[] args)
{
    int N = 3;
    int M = 5;
    int arr[] = { 2, 8, 10, 17, 15,
                  23, 4, 12 };
    sortlastMElements(arr, N, M);
}
}

// This code is contributed by code_hunt.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function for merging the two sorted
# arrays
def merge(a, l, m, r):

    s1 = m - l + 1
    s2 = r - m

    # Create two temp arrays
    left = [0 for i in range(s1)]
    right = [0 for i in range(s2)]

    # Copy elements to left array
    for i in range(s1):
        left[i] = a[l + i]

    # Copy elements to right array
    for j in range(s2):
        right[j] = a[j + m + 1]

    i = 0
    j = 0
    k = l

    # Merge the array back into the
    # array over the range [l, r]
    while (i < s1 and j < s2):

        # If the current left element
        # is smaller than the current
        # right element
        if (left[i] <= right[j]):
            a[k] = left[i]
            i += 1

        # Otherwise
        else:
            a[k] = right[j]
            j += 1

        k += 1

    # Copy the remaining elements of
    # the array left[]
    while (i < s1):
        a[k] = left[i]
        i += 1
        k += 1

    # Copy the remaining elements of
    # the array right[]
    while (j < s2):
        a[k] = right[j]
        j += 1
        k += 1

# Function to sort the array over the
# range [l, r]
def mergesort(arr, l,  r):

    if (l < r):

        # Find the middle index
        mid = l + (r - l) // 2

        # Recursively call for the
        # two halves
        mergesort(arr, l, mid)
        mergesort(arr, mid + 1, r)

        # Perform the merge operation
        merge(arr, l, mid, r)

# Function to sort an array for the
# last m elements are unsorted
def sortlastMElements(arr, N, M):

    s = M + N - 1

    # Sort the last m elements
    mergesort(arr, N, s)

    # Merge the two sorted subarrays
    merge(arr, 0, N - 1, N + M - 1)

    # Print the sorted array
    for i in range(N + M):
        print(arr[i], end = " ")

# Driver Code
if __name__ == '__main__':

    N = 3
    M = 5
    arr = [ 2, 8, 10, 17, 15, 23, 4, 12 ]

    sortlastMElements(arr, N, M)

# This code is contributed by ipg2016107
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

// Function for merging the two sorted
// arrays
static void merge(int[] a, int l, int m, int r)
{
    int s1 = m - l + 1;
    int s2 = r - m;
    int i = 0, j = 0;

    // Create two temp arrays
    int[] left = new int[s1];
    int[] right = new int[s2];

    // Copy elements to left array
    for (i = 0; i < s1; i++)
        left[i] = a[l + i];

    // Copy elements to right array
    for (j = 0; j < s2; j++)
        right[j] = a[j + m + 1];

    int k = l;

    // Merge the array back into the
    // array over the range [l, r]
    while (i < s1 && j < s2) {

        // If the current left element
        // is smaller than the current
        // right element
        if (left[i] <= right[j]) {
            a[k] = left[i];
            i++;
        }

        // Otherwise
        else {
            a[k] = right[j];
            j++;
        }
        k++;
    }

    // Copy the remaining elements of
    // the array left[]
    while (i < s1) {
        a[k] = left[i];
        i++;
        k++;
    }

    // Copy the remaining elements of
    // the array right[]
    while (j < s2) {
        a[k] = right[j];
        j++;
        k++;
    }
}

// Function to sort the array over the
// range [l, r]
static void mergesort(int[] arr, int l, int r)
{
    if (l < r) {

        // Find the middle index
        int mid = l + (r - l) / 2;

        // Recursively call for the
        // two halves
        mergesort(arr, l, mid);
        mergesort(arr, mid + 1, r);

        // Perform the merge operation
        merge(arr, l, mid, r);
    }
}

// Function to sort an array for the
// last m elements are unsorted
static void sortlastMElements(int[] arr, int N,
                       int M)
{
    int s = M + N - 1;

    // Sort the last m elements
    mergesort(arr, N, s);

    // Merge the two sorted subarrays
    merge(arr, 0, N - 1, N + M - 1);

    // Print the sorted array
    for (int i = 0; i < N + M; i++)
         Console.Write( arr[i] + " ");
}

// Driver code
static void Main()
{
    int N = 3;
    int M = 5;
    int[] arr = { 2, 8, 10, 17, 15,
                  23, 4, 12 };
    sortlastMElements(arr, N, M);

}
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function for merging the two sorted
// arrays
function merge(a, l, m, r) {
    let s1 = m - l + 1;
    let s2 = r - m;

    // Create two temp arrays
    let left = new Array(s1);
    let right = new Array(s2);

    // Copy elements to left array
    for (let i = 0; i < s1; i++)
        left[i] = a[l + i];

    // Copy elements to right array
    for (let j = 0; j < s2; j++)
        right[j] = a[j + m + 1];

    let i = 0, j = 0, k = l;

    // Merge the array back into the
    // array over the range [l, r]
    while (i < s1 && j < s2) {

        // If the current left element
        // is smaller than the current
        // right element
        if (left[i] <= right[j]) {
            a[k] = left[i];
            i++;
        }

        // Otherwise
        else {
            a[k] = right[j];
            j++;
        }
        k++;
    }

    // Copy the remaining elements of
    // the array left[]
    while (i < s1) {
        a[k] = left[i];
        i++;
        k++;
    }

    // Copy the remaining elements of
    // the array right[]
    while (j < s2) {
        a[k] = right[j];
        j++;
        k++;
    }
}

// Function to sort the array over the
// range [l, r]
function mergesort(arr, l, r) {
    if (l < r) {

        // Find the middle index
        let mid = Math.floor(l + (r - l) / 2);

        // Recursively call for the
        // two halves
        mergesort(arr, l, mid);
        mergesort(arr, mid + 1, r);

        // Perform the merge operation
        merge(arr, l, mid, r);
    }
}

// Function to sort an array for the
// last m elements are unsorted
function sortlastMElements(arr, N, M) {
    let s = M + N - 1;

    // Sort the last m elements
    mergesort(arr, N, s);

    // Merge the two sorted subarrays
    merge(arr, 0, N - 1, N + M - 1);

    // Print the sorted array
    for (let i = 0; i < N + M; i++)
        document.write(arr[i] + " ");
}

// Driver Code

let N = 3;
let M = 5;
let arr = [2, 8, 10, 17, 15,
    23, 4, 12];
sortlastMElements(arr, N, M);

</script>
```

**Output:** 

```
2 4 8 10 12 15 17 23
```

***时间复杂度:** O(M*log M)*
***辅助空间:** O(N + M)*