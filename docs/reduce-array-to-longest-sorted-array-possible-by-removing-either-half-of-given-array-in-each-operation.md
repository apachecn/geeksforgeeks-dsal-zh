# 通过在每次操作中移除给定数组的一半，将数组缩减为可能的最长排序数组

> 原文:[https://www . geeksforgeeks . org/通过在每个操作中移除给定数组的一半来减少数组到最长排序数组的可能性/](https://www.geeksforgeeks.org/reduce-array-to-longest-sorted-array-possible-by-removing-either-half-of-given-array-in-each-operation/)

给定一个大小为 **N** ( *始终为 2* 的幂)的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】】**，任务是找到最长的[排序数组](https://www.geeksforgeeks.org/search-insert-and-delete-in-a-sorted-array/)的长度，通过在每次操作时移除数组的任意一半，给定数组可以被缩减到该长度。

**示例:**

> **输入:** arr[] = { 11，12，1，2，13，14，3，4 }
> **输出:** 2
> **解释:**
> arr[]前半部分的移除将 arr[]修改为{13，14，3，4 }。
> 删除 arr[]的前半部分将 arr[]修改为{3，4}。
> 因此，可能的最长排序数组的长度是 2，这是最大可能。
> 
> **输入:** arr[] = { 1，2，2，4 }
> **输出:** 4

**方法:**按照以下步骤解决问题:

*   初始化一个变量，比如 **MaxLength** ，来存储排序数组的最大长度，这个最大长度可以通过执行给定的操作获得。
*   递归地将数组分成相等的两半，对于每一半，[检查数组的分区是否排序](https://www.geeksforgeeks.org/program-check-array-sorted-not-iterative-recursive/)。如果发现是真的，那么更新**最大长度**到分区的长度。
*   最后，打印**最大长度**的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if the subarray
// arr[i..j] is a sorted subarray or not
int isSortedparitions(int arr[],
                      int i, int j)
{
    // Traverse all elements of
    // the subarray arr[i...j]
    for (int k = i + 1; k <= j; k++) {

        // If the previous element of the
        // subarray exceeds current element
        if (arr[k] < arr[k - 1]) {

            // Return 0
            return 0;
        }
    }

    // Return 1
    return 1;
}

// Recursively partition the array
// into two equal halves
int partitionsArr(int arr[],
                  int i, int j)
{
    // If atmost one element is left
    // in the subarray arr[i..j]
    if (i >= j)
        return 1;

    // Checks if subarray arr[i..j] is
    // a sorted subarray or not
    bool flag = isSortedparitions(
        arr, i, j);

    // If the subarray arr[i...j]
    // is a sorted subarray
    if (flag) {
        return (j - i + 1);
    }

    // Stores middle element
    // of the subarray arr[i..j]
    int mid = (i + j) / 2;

    // Recursively partition the current
    // subarray arr[i..j] into equal halves
    int X = partitionsArr(arr, i, mid);
    int Y = partitionsArr(arr, mid + 1, j);

    return max(X, Y);
}

// Driver Code
int main()
{

    int arr[] = { 11, 12, 1, 2,
                  13, 14, 3, 4 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << partitionsArr(
        arr, 0, N - 1);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to check if the subarray
// arr[i..j] is a sorted subarray or not
static int isSortedparitions(int arr[],
                             int i, int j)
{

    // Traverse all elements of
    // the subarray arr[i...j]
    for(int k = i + 1; k <= j; k++)
    {

        // If the previous element of the
        // subarray exceeds current element
        if (arr[k] < arr[k - 1])
        {

            // Return 0
            return 0;
        }
    }

    // Return 1
    return 1;
}

// Recursively partition the array
// into two equal halves
static int partitionsArr(int arr[], int i,
                         int j)
{

    // If atmost one element is left
    // in the subarray arr[i..j]
    if (i >= j)
        return 1;

    // Checks if subarray arr[i..j] is
    // a sorted subarray or not
    int flag = (int)isSortedparitions(arr, i, j);

    // If the subarray arr[i...j]
    // is a sorted subarray
    if (flag != 0)
    {
        return (j - i + 1);
    }

    // Stores middle element
    // of the subarray arr[i..j]
    int mid = (i + j) / 2;

    // Recursively partition the current
    // subarray arr[i..j] into equal halves
    int X = partitionsArr(arr, i, mid);
    int Y = partitionsArr(arr, mid + 1, j);

    return Math.max(X, Y);
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 11, 12, 1, 2,
                  13, 14, 3, 4 };

    int N = arr.length;

    System.out.print(partitionsArr(
        arr, 0, N - 1));
}
}

// This code is contributed by susmitakundugoaldanga
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to check if the subarray
# arr[i..j] is a sorted subarray or not
def isSortedparitions(arr, i, j):

    # Traverse all elements of
    # the subarray arr[i...j]
    for k in range(i + 1, j + 1):

        # If the previous element of the
        # subarray exceeds current element
        if (arr[k] < arr[k - 1]):

            # Return 0
            return 0

    # Return 1
    return 1

# Recursively partition the array
# into two equal halves
def partitionsArr(arr, i, j):

    # If atmost one element is left
    # in the subarray arr[i..j]
    if (i >= j):
        return 1

    # Checks if subarray arr[i..j] is
    # a sorted subarray or not
    flag = int(isSortedparitions(arr, i, j))

    # If the subarray arr[i...j]
    # is a sorted subarray
    if (flag != 0):
        return (j - i + 1)

    # Stores middle element
    # of the subarray arr[i..j]
    mid = (i + j) // 2

    # Recursively partition the current
    # subarray arr[i..j] into equal halves
    X = partitionsArr(arr, i, mid);
    Y = partitionsArr(arr, mid + 1, j)

    return max(X, Y)

# Driver Code
if __name__ == '__main__':

    arr = [ 11, 12, 1, 2, 13, 14, 3, 4 ]
    N = len(arr)

    print(partitionsArr(arr, 0, N - 1))

# This code is contributed by Princi Singh
```

## C#

```
// C# program to implement
// the above approach 
using System;

class GFG{

// Function to check if the subarray
// arr[i..j] is a sorted subarray or not
static int isSortedparitions(int[] arr,
                             int i, int j)
{

    // Traverse all elements of
    // the subarray arr[i...j]
    for(int k = i + 1; k <= j; k++)
    {

        // If the previous element of the
        // subarray exceeds current element
        if (arr[k] < arr[k - 1])
        {

            // Return 0
            return 0;
        }
    }

    // Return 1
    return 1;
}

// Recursively partition the array
// into two equal halves
static int partitionsArr(int[] arr, int i,
                         int j)
{

    // If atmost one element is left
    // in the subarray arr[i..j]
    if (i >= j)
        return 1;

    // Checks if subarray arr[i..j] is
    // a sorted subarray or not
    int flag = (int)isSortedparitions(arr, i, j);

    // If the subarray arr[i...j]
    // is a sorted subarray
    if (flag != 0)
    {
        return (j - i + 1);
    }

    // Stores middle element
    // of the subarray arr[i..j]
    int mid = (i + j) / 2;

    // Recursively partition the current
    // subarray arr[i..j] into equal halves
    int X = partitionsArr(arr, i, mid);
    int Y = partitionsArr(arr, mid + 1, j);

    return Math.Max(X, Y);
}

// Driver Code
public static void Main()
{
    int[] arr = { 11, 12, 1, 2,
                  13, 14, 3, 4 };

    int N = arr.Length;

    Console.Write(partitionsArr(
        arr, 0, N - 1));
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to check if the subarray
// arr[i..j] is a sorted subarray or not
function isSortedparitions(arr, i, j)
{
    // Traverse all elements of
    // the subarray arr[i...j]
    for (var k = i + 1; k <= j; k++) {

        // If the previous element of the
        // subarray exceeds current element
        if (arr[k] < arr[k - 1]) {

            // Return 0
            return 0;
        }
    }

    // Return 1
    return 1;
}

// Recursively partition the array
// into two equal halves
function partitionsArr(arr, i, j)
{
    // If atmost one element is left
    // in the subarray arr[i..j]
    if (i >= j)
        return 1;

    // Checks if subarray arr[i..j] is
    // a sorted subarray or not
    var flag = isSortedparitions(
        arr, i, j);

    // If the subarray arr[i...j]
    // is a sorted subarray
    if (flag) {
        return (j - i + 1);
    }

    // Stores middle element
    // of the subarray arr[i..j]
    var mid = parseInt((i + j) / 2);

    // Recursively partition the current
    // subarray arr[i..j] into equal halves
    var X = partitionsArr(arr, i, mid);
    var Y = partitionsArr(arr, mid + 1, j);

    return Math.max(X, Y);
}

// Driver Code
var arr = [11, 12, 1, 2,
              13, 14, 3, 4 ];
var N = arr.length;
document.write( partitionsArr(
    arr, 0, N - 1));

</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N * log(N))*
***辅助空间:** O(1)*