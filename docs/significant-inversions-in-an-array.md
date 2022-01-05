# 阵列中的显著反转

> 原文:[https://www . geeksforgeeks . org/material-inversion-in-a-array/](https://www.geeksforgeeks.org/significant-inversions-in-an-array/)

给定一个数组 **arr[]** ，任务是找到该数组的总有效反转计数。如果 **arr[i] > 2 * arr[j]** 和 **i < j** ，则两个元素 **arr[i]** 和 **arr[j]** 形成显著的反转。
**举例:**

> **输入:** arr[] = { 1，20，6，4，5 }
> **输出:** 3
> 有效反转对为(20，6)、(20，5)和(20，4)。
> **输入:** arr[] = { 1，20 }
> **输出:** 0

**先决条件:** [计数反转](https://www.geeksforgeeks.org/counting-inversions/)
**进场:**

*   寻找反演的基本思想将基于上述前提，使用修改后的[合并排序](https://www.geeksforgeeks.org/merge-sort/)的[分治](https://www.geeksforgeeks.org/divide-and-conquer/)方法。
*   左半部分和右半部分的显著反转数可以计数。用索引(I，j)包括有效反转的计数，使得 I 在左半部分，j 在右半部分，然后将三者相加，得到总有效反转计数。
*   可以修改上述链接中使用的方法，以便在合并步骤中执行左右两次传递。在第一遍中，计算合并数组中有效反转计数的数量。对于左数组中的任何索引 I，如果 arr[i] > 2 * arr[j]，则左数组中第 I 个索引左侧的所有元素也将有助于显著的反转计数。递增 j，否则递增 I。
*   第二步是构造合并的数组。这里需要两次通过，因为在正常的反转计数中，两次通过会在相同的点移动 I 和 j，因此可以合并，但在这种情况下不是这样。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

int _mergeSort(int arr[], int temp[], int left, int right);
int merge(int arr[], int temp[], int left, int mid, int right);

// Function that sorts the input array
// and returns the number of inversions
// in the array
int mergeSort(int arr[], int array_size)
{
    int temp[array_size];
    return _mergeSort(arr, temp, 0, array_size - 1);
}

// Recursive function that sorts the input
// array and returns the number of
// inversions in the array
int _mergeSort(int arr[], int temp[], int left, int right)
{
    int mid, inv_count = 0;
    if (right > left) {

        // Divide the array into two parts and
        // call _mergeSortAndCountInv()
        // for each of the parts
        mid = (right + left) / 2;

        // Inversion count will be sum of the
        // inversions in the left-part, the right-part
        // and the number of inversions in merging
        inv_count = _mergeSort(arr, temp, left, mid);
        inv_count += _mergeSort(arr, temp, mid + 1, right);

        // Merge the two parts
        inv_count += merge(arr, temp, left, mid + 1, right);
    }
    return inv_count;
}

// Function that merges the two sorted arrays
// and returns the inversion count in the arrays
int merge(int arr[], int temp[], int left,
          int mid, int right)
{
    int i, j, k;
    int inv_count = 0;

    // i is the index for the left subarray
    i = left;

    // j is the index for the right subarray
    j = mid;

    // k is the index for the resultant
    // merged subarray
    k = left;

    // First pass to count number
    // of significant inversions
    while ((i <= mid - 1) && (j <= right)) {
        if (arr[i] > 2 * arr[j]) {
            inv_count += (mid - i);
            j++;
        }
        else {
            i++;
        }
    }

    // i is the index for the left subarray
    i = left;

    // j is the index for the right subarray
    j = mid;

    // k is the index for the resultant
    // merged subarray
    k = left;

    // Second pass to merge the two sorted arrays
    while ((i <= mid - 1) && (j <= right)) {
        if (arr[i] <= arr[j]) {
            temp[k++] = arr[i++];
        }
        else {
            temp[k++] = arr[j++];
        }
    }

    // Copy the remaining elements of the left
    // subarray (if there are any) to temp
    while (i <= mid - 1)
        temp[k++] = arr[i++];

    // Copy the remaining elements of the right
    // subarray (if there are any) to temp
    while (j <= right)
        temp[k++] = arr[j++];

    // Copy back the merged elements to
    // the original array
    for (i = left; i <= right; i++)
        arr[i] = temp[i];

    return inv_count;
}

// Driver code
int main()
{
    int arr[] = { 1, 20, 6, 4, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << mergeSort(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{

    // Function that sorts the input array
    // and returns the number of inversions
    // in the array
    static int mergeSort(int arr[], int array_size)
    {
        int temp[] = new int[array_size];
        return _mergeSort(arr, temp, 0, array_size - 1);
    }

    // Recursive function that sorts the input
    // array and returns the number of
    // inversions in the array
    static int _mergeSort(int arr[], int temp[],
                          int left, int right)
    {
        int mid, inv_count = 0;
        if (right > left)
        {

            // Divide the array into two parts and
            // call _mergeSortAndCountInv()
            // for each of the parts
            mid = (right + left) / 2;

            // Inversion count will be sum of the
            // inversions in the left-part, the right-part
            // and the number of inversions in merging
            inv_count = _mergeSort(arr, temp, left, mid);
            inv_count += _mergeSort(arr, temp, mid + 1, right);

            // Merge the two parts
            inv_count += merge(arr, temp, left,
                               mid + 1, right);
        }
        return inv_count;
    }

    // Function that merges the two sorted arrays
    // and returns the inversion count in the arrays
    static int merge(int arr[], int temp[], int left,
                                int mid, int right)
    {
        int i, j, k;
        int inv_count = 0;

        // i is the index for the left subarray
        i = left;

        // j is the index for the right subarray
        j = mid;

        // k is the index for the resultant
        // merged subarray
        k = left;

        // First pass to count number
        // of significant inversions
        while ((i <= mid - 1) && (j <= right))
        {
            if (arr[i] > 2 * arr[j])
            {
                inv_count += (mid - i);
                j++;
            }
            else
            {
                i++;
            }
        }

        // i is the index for the left subarray
        i = left;

        // j is the index for the right subarray
        j = mid;

        // k is the index for the resultant
        // merged subarray
        k = left;

        // Second pass to merge the two sorted arrays
        while ((i <= mid - 1) && (j <= right))
        {
            if (arr[i] <= arr[j])
            {
                temp[k++] = arr[i++];
            }
            else
            {
                temp[k++] = arr[j++];
            }
        }

        // Copy the remaining elements of the left
        // subarray (if there are any) to temp
        while (i <= mid - 1)
            temp[k++] = arr[i++];

        // Copy the remaining elements of the right
        // subarray (if there are any) to temp
        while (j <= right)
            temp[k++] = arr[j++];

        // Copy back the merged elements to
        // the original array
        for (i = left; i <= right; i++)
            arr[i] = temp[i];

        return inv_count;
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = { 1, 20, 6, 4, 5 };
        int n = arr.length;

        System.out.println(mergeSort(arr, n));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that sorts the input array
# and returns the number of inversions
# in the array
def mergeSort(arr, array_size):
    temp = [0 for i in range(array_size)]
    return _mergeSort(arr, temp, 0,
                      array_size - 1)

# Recursive function that sorts the input
# array and returns the number of
# inversions in the array
def _mergeSort(arr, temp, left, right):
    mid, inv_count = 0, 0
    if (right > left):

        # Divide the array into two parts and
        # call _mergeSortAndCountInv()
        # for each of the parts
        mid = (right + left) // 2

        # Inversion count will be sum of the
        # inversions in the left-part, the right-part
        # and the number of inversions in merging
        inv_count = _mergeSort(arr, temp, left, mid)
        inv_count += _mergeSort(arr, temp,
                                mid + 1, right)

        # Merge the two parts
        inv_count += merge(arr, temp, left,
                           mid + 1, right)
    return inv_count

# Function that merges the two sorted arrays
# and returns the inversion count in the arrays
def merge(arr, temp, left,mid, right):
    inv_count = 0

    # i is the index for the left subarray
    i = left

    # j is the index for the right subarray
    j = mid

    # k is the index for the resultant
    # merged subarray
    k = left

    # First pass to count number
    # of significant inversions
    while ((i <= mid - 1) and (j <= right)):
        if (arr[i] > 2 * arr[j]):
            inv_count += (mid - i)
            j += 1
        else:
            i += 1

    # i is the index for the left subarray
    i = left

    # j is the index for the right subarray
    j = mid

    # k is the index for the resultant
    # merged subarray
    k = left

    # Second pass to merge the two sorted arrays
    while ((i <= mid - 1) and (j <= right)):
        if (arr[i] <= arr[j]):
            temp[k] = arr[i]
            i, k = i + 1, k + 1
        else:
            temp[k] = arr[j]
            k, j = k + 1, j + 1

    # Copy the remaining elements of the left
    # subarray (if there are any) to temp
    while (i <= mid - 1):
        temp[k] = arr[i]
        i, k = i + 1, k + 1

    # Copy the remaining elements of the right
    # subarray (if there are any) to temp
    while (j <= right):
        temp[k] = arr[j]
        j, k = j + 1, k + 1

    # Copy back the merged elements to
    # the original array
    for i in range(left, right + 1):
        arr[i] = temp[i]

    return inv_count

# Driver code
arr = [1, 20, 6, 4, 5]
n = len(arr)

print(mergeSort(arr, n))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    // Function that sorts the input array
    // and returns the number of inversions
    // in the array
    static int mergeSort(int []arr,
                         int array_size)
    {
        int []temp = new int[array_size];
        return _mergeSort(arr, temp, 0,
                          array_size - 1);
    }

    // Recursive function that sorts the input
    // array and returns the number of
    // inversions in the array
    static int _mergeSort(int []arr, int []temp,
                          int left, int right)
    {
        int mid, inv_count = 0;
        if (right > left)
        {

            // Divide the array into two parts and
            // call _mergeSortAndCountInv()
            // for each of the parts
            mid = (right + left) / 2;

            // Inversion count will be sum of the
            // inversions in the left-part, the right-part
            // and the number of inversions in merging
            inv_count = _mergeSort(arr, temp, left, mid);
            inv_count += _mergeSort(arr, temp,
                                    mid + 1, right);

            // Merge the two parts
            inv_count += merge(arr, temp, left,
                               mid + 1, right);
        }
        return inv_count;
    }

    // Function that merges the two sorted arrays
    // and returns the inversion count in the arrays
    static int merge(int []arr, int []temp, int left,
                                int mid, int right)
    {
        int i, j, k;
        int inv_count = 0;

        // i is the index for the left subarray
        i = left;

        // j is the index for the right subarray
        j = mid;

        // k is the index for the resultant
        // merged subarray
        k = left;

        // First pass to count number
        // of significant inversions
        while ((i <= mid - 1) && (j <= right))
        {
            if (arr[i] > 2 * arr[j])
            {
                inv_count += (mid - i);
                j++;
            }
            else
            {
                i++;
            }
        }

        // i is the index for the left subarray
        i = left;

        // j is the index for the right subarray
        j = mid;

        // k is the index for the resultant
        // merged subarray
        k = left;

        // Second pass to merge the two sorted arrays
        while ((i <= mid - 1) && (j <= right))
        {
            if (arr[i] <= arr[j])
            {
                temp[k++] = arr[i++];
            }
            else
            {
                temp[k++] = arr[j++];
            }
        }

        // Copy the remaining elements of the left
        // subarray (if there are any) to temp
        while (i <= mid - 1)
            temp[k++] = arr[i++];

        // Copy the remaining elements of the right
        // subarray (if there are any) to temp
        while (j <= right)
            temp[k++] = arr[j++];

        // Copy back the merged elements to
        // the original array
        for (i = left; i <= right; i++)
            arr[i] = temp[i];

        return inv_count;
    }

    // Driver code
    public static void Main ()
    {
        int []arr = { 1, 20, 6, 4, 5 };
        int n = arr.Length;

        Console.WriteLine(mergeSort(arr, n));
    }
}

// This code is contributed by anuj_67..
```

## java 描述语言

```
<script>
    // Javascript implementation of the above approach

    // Function that sorts the input array
    // and returns the number of inversions
    // in the array
    function mergeSort(arr, array_size)
    {
        let temp = new Array(array_size);
        return _mergeSort(arr, temp, 0, array_size - 1);
    }

    // Recursive function that sorts the input
    // array and returns the number of
    // inversions in the array
    function _mergeSort(arr, temp, left, right)
    {
        let mid, inv_count = 0;
        if (right > left)
        {

            // Divide the array into two parts and
            // call _mergeSortAndCountInv()
            // for each of the parts
            mid = parseInt((right + left) / 2, 10);

            // Inversion count will be sum of the
            // inversions in the left-part, the right-part
            // and the number of inversions in merging
            inv_count = _mergeSort(arr, temp, left, mid);
            inv_count += _mergeSort(arr, temp,
                                    mid + 1, right);

            // Merge the two parts
            inv_count += merge(arr, temp, left,
                               mid + 1, right);
        }
        return inv_count;
    }

    // Function that merges the two sorted arrays
    // and returns the inversion count in the arrays
    function merge(arr, temp, left, mid, right)
    {
        let i, j, k;
        let inv_count = 0;

        // i is the index for the left subarray
        i = left;

        // j is the index for the right subarray
        j = mid;

        // k is the index for the resultant
        // merged subarray
        k = left;

        // First pass to count number
        // of significant inversions
        while ((i <= mid - 1) && (j <= right))
        {
            if (arr[i] > 2 * arr[j])
            {
                inv_count += (mid - i);
                j++;
            }
            else
            {
                i++;
            }
        }

        // i is the index for the left subarray
        i = left;

        // j is the index for the right subarray
        j = mid;

        // k is the index for the resultant
        // merged subarray
        k = left;

        // Second pass to merge the two sorted arrays
        while ((i <= mid - 1) && (j <= right))
        {
            if (arr[i] <= arr[j])
            {
                temp[k++] = arr[i++];
            }
            else
            {
                temp[k++] = arr[j++];
            }
        }

        // Copy the remaining elements of the left
        // subarray (if there are any) to temp
        while (i <= mid - 1)
            temp[k++] = arr[i++];

        // Copy the remaining elements of the right
        // subarray (if there are any) to temp
        while (j <= right)
            temp[k++] = arr[j++];

        // Copy back the merged elements to
        // the original array
        for (i = left; i <= right; i++)
            arr[i] = temp[i];

        return inv_count;
    }

    let arr = [ 1, 20, 6, 4, 5 ];
    let n = arr.length;

    document.write(mergeSort(arr, n));

    // This code is contributed by mukesh07.
</script>
```

**Output:** 

```
3
```