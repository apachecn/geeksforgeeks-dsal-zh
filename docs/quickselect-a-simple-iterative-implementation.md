# 快速选择(简单的迭代实现)

> 原文:[https://www . geeksforgeeks . org/quick sele-a-simple-iterative-implementation/](https://www.geeksforgeeks.org/quickselect-a-simple-iterative-implementation/)

[快速选择](https://www.geeksforgeeks.org/quickselect-algorithm/)是一种在无序列表中寻找第 k 个最小元素的选择算法。与[快速排序](https://www.geeksforgeeks.org/quick-sort/)排序算法有关。
示例:

```
Input: arr[] = {7, 10, 4, 3, 20, 15}
           k = 3
Output: 7

Input: arr[] = {7, 10, 4, 3, 20, 15}
           k = 4
Output: 10
```

快速选择算法基于[快速排序](https://www.geeksforgeeks.org/quick-sort/)。不同的是，它不是在两侧重复出现(找到枢轴后)，而是只在包含第 k 个最小元素的部分重复出现。逻辑很简单，如果分区元素的索引大于 k，那么我们对左边部分进行递归。如果索引与 k 相同，我们找到了第 k 个最小的元素，然后返回。如果指数小于 k，那么我们对右半部分重复。这将预期的复杂性从 O(n log n)降低到 O(n)，最坏的情况是 O(n^2).

```
function quickSelect(list, left, right, k)

   if left = right
      return list[left]

   Select a pivotIndex between left and right

   pivotIndex := partition(list, left, right, 
                                  pivotIndex)
   if k = pivotIndex
      return list[k]
   else if k < pivotIndex
      right := pivotIndex - 1
   else
      left := pivotIndex + 1
```

我们已经讨论了快速选择的递归实现。在这篇文章中，我们将讨论简单的迭代实现。

## C++

```
// CPP program for iterative implementation of QuickSelect
#include <bits/stdc++.h>
using namespace std;

// Standard Lomuto partition function
int partition(int arr[], int low, int high)
{
    int pivot = arr[high];
    int i = (low - 1);
    for (int j = low; j <= high - 1; j++) {
        if (arr[j] <= pivot) {
            i++;
            swap(arr[i], arr[j]);
        }
    }
    swap(arr[i + 1], arr[high]);
    return (i + 1);
}

// Implementation of QuickSelect
int kthSmallest(int a[], int left, int right, int k)
{

    while (left <= right) {

        // Partition a[left..right] around a pivot
        // and find the position of the pivot
        int pivotIndex = partition(a, left, right);

        // If pivot itself is the k-th smallest element
        if (pivotIndex == k - 1)
            return a[pivotIndex];

        // If there are more than k-1 elements on
        // left of pivot, then k-th smallest must be
        // on left side.
        else if (pivotIndex > k - 1)
            right = pivotIndex - 1;

        // Else k-th smallest is on right side.
        else
            left = pivotIndex + 1;
    }
    return -1;
}

// Driver program to test above methods
int main()
{
    int arr[] = { 10, 4, 5, 8, 11, 6, 26 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 5;
    cout << "K-th smallest element is "
         << kthSmallest(arr, 0, n - 1, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for iterative implementation
// of QuickSelect
class GFG
{

    // Standard Lomuto partition function
    static int partition(int arr[],
                         int low, int high)
    {
        int temp;
        int pivot = arr[high];
        int i = (low - 1);
        for (int j = low; j <= high - 1; j++)
        {
            if (arr[j] <= pivot)
            {
                i++;
                temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }
        }

            temp = arr[i + 1];
            arr[i + 1] = arr[high];
            arr[high] = temp;

        return (i + 1);
    }

    // Implementation of QuickSelect
    static int kthSmallest(int a[], int left,
                           int right, int k)
    {
        while (left <= right)
        {

            // Partition a[left..right] around a pivot
            // and find the position of the pivot
            int pivotIndex = partition(a, left, right);

            // If pivot itself is the k-th smallest element
            if (pivotIndex == k - 1)
                return a[pivotIndex];

            // If there are more than k-1 elements on
            // left of pivot, then k-th smallest must be
            // on left side.
            else if (pivotIndex > k - 1)
                right = pivotIndex - 1;

            // Else k-th smallest is on right side.
            else
                left = pivotIndex + 1;
        }
        return -1;
    }

    // Driver Code
    public static void main (String[] args)
    {
        int arr[] = { 10, 4, 5, 8, 11, 6, 26 };
        int n = arr.length;
        int k = 5;
        System.out.println("K-th smallest element is " +
                         kthSmallest(arr, 0, n - 1, k));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 program for iterative implementation
# of QuickSelect

# Standard Lomuto partition function
def partition(arr, low, high) :

    pivot = arr[high]
    i = (low - 1)
    for j in range(low, high) :
        if arr[j] <= pivot :
            i += 1
            arr[i], arr[j] = arr[j], arr[i]

    arr[i + 1], arr[high] = arr[high], arr[i + 1]
    return (i + 1)

# Implementation of QuickSelect
def kthSmallest(a, left, right, k) :

    while left <= right :

        # Partition a[left..right] around a pivot
        # and find the position of the pivot
        pivotIndex = partition(a, left, right)

        # If pivot itself is the k-th smallest element
        if pivotIndex == k - 1 :
            return a[pivotIndex]

        # If there are more than k-1 elements on
        # left of pivot, then k-th smallest must be
        # on left side.
        elif pivotIndex > k - 1 :
            right = pivotIndex - 1

        # Else k-th smallest is on right side.
        else :
            left = pivotIndex + 1

    return -1

# Driver Code
arr = [ 10, 4, 5, 8, 11, 6, 26 ]
n = len(arr)
k = 5
print("K-th smallest element is",
       kthSmallest(arr, 0, n - 1, k))

# This code is contributed by
# divyamohan123
```

## C#

```
// C# program for iterative implementation
// of QuickSelect
using System;

class GFG
{

    // Standard Lomuto partition function
    static int partition(int []arr,
                         int low, int high)
    {
        int temp;
        int pivot = arr[high];
        int i = (low - 1);
        for (int j = low; j <= high - 1; j++)
        {
            if (arr[j] <= pivot)
            {
                i++;
                temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }
        }

        temp = arr[i + 1];
        arr[i + 1] = arr[high];
        arr[high] = temp;

        return (i + 1);
    }

    // Implementation of QuickSelect
    static int kthSmallest(int []a, int left,
                           int right, int k)
    {
        while (left <= right)
        {

            // Partition a[left..right] around a pivot
            // and find the position of the pivot
            int pivotIndex = partition(a, left, right);

            // If pivot itself is the k-th smallest element
            if (pivotIndex == k - 1)
                return a[pivotIndex];

            // If there are more than k-1 elements on
            // left of pivot, then k-th smallest must be
            // on left side.
            else if (pivotIndex > k - 1)
                right = pivotIndex - 1;

            // Else k-th smallest is on right side.
            else
                left = pivotIndex + 1;
        }
        return -1;
    }

    // Driver Code
    public static void Main (String[] args)
    {
        int []arr = { 10, 4, 5, 8, 11, 6, 26 };
        int n = arr.Length;
        int k = 5;
        Console.WriteLine("K-th smallest element is " +
                        kthSmallest(arr, 0, n - 1, k));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
    // Javascript program for iterative implementation of QuickSelect

    // Standard Lomuto partition function
    function partition(arr, low, high)
    {
        let temp;
        let pivot = arr[high];
        let i = (low - 1);
        for (let j = low; j <= high - 1; j++)
        {
            if (arr[j] <= pivot)
            {
                i++;
                temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }
        }

        temp = arr[i + 1];
        arr[i + 1] = arr[high];
        arr[high] = temp;

        return (i + 1);
    }

    // Implementation of QuickSelect
    function kthSmallest(a, left, right, k)
    {
        while (left <= right)
        {

            // Partition a[left..right] around a pivot
            // and find the position of the pivot
            let pivotIndex = partition(a, left, right);

            // If pivot itself is the k-th smallest element
            if (pivotIndex == k - 1)
                return a[pivotIndex];

            // If there are more than k-1 elements on
            // left of pivot, then k-th smallest must be
            // on left side.
            else if (pivotIndex > k - 1)
                right = pivotIndex - 1;

            // Else k-th smallest is on right side.
            else
                left = pivotIndex + 1;
        }
        return -1;
    }

    let arr = [ 10, 4, 5, 8, 11, 6, 26 ];
    let n = arr.length;
    let k = 5;
    document.write("K-th smallest element is " + kthSmallest(arr, 0, n - 1, k));

    // This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
K-th smallest element is 10
```