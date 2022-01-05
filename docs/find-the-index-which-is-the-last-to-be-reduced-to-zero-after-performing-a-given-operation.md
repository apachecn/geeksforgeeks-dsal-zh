# 找到执行给定操作后最后一个归零的索引

> 原文:[https://www . geesforgeks . org/find-the-index-这是执行给定操作后最后一个被还原为零的索引/](https://www.geeksforgeeks.org/find-the-index-which-is-the-last-to-be-reduced-to-zero-after-performing-a-given-operation/)

给定一个大小为 **N** 的整数数组 **arr[]** 和一个整数 **K** ，任务是找到在执行给定操作后最后一个被归零的索引。操作描述如下:

*   从 **arr[0]** 到**arr[N–1]**开始，将每个元素更新为**arr[I]= arr[I]–K**。
*   如果 **arr[i] < K** 则设置 **arr[i] = 0** ，一旦是 **0** ，则不再对 **arr[i]** 进行操作。
*   重复以上步骤，直到所有元素都减少到 **0** 。

打印最后变为零的索引。
**例:**

> **输入:** arr[] = { 3，2，5，7，2，9 }，K = 4
> **输出:** 5
> 操作 1: arr[] = {0，0，1，3，0，5}
> 操作 2: arr[] = {0，0，0，0，0，1}
> 操作 3: arr[] = {0，0，0，0，0，0}
> 索引 5 是最后一个减少的。
> **输入:** arr[] = { 31，12，25，27，32，19 }，K = 5
> **输出:** 4

**方法:**在每一步中，特定索引处的元素被 **K** 减去。因此，一个特定的元素需要 **ceil(arr[i] / K)** 或**(arr[I]+K–1)/K**步才能降为零。因此所需的索引由最大值为**(arr[I]+K–1)/K**的数组索引给出。如果最大值出现不止一次，那么当从 **0** 到**N–1**执行操作时，返回最大索引。
以下是上述方法的实施:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns the index
// which will be the last to become
// zero after performing given operation
int findIndex(int a[], int n, int k)
{

    // Initialize the result
    int index = -1, max_ceil = INT_MIN;

    for (int i = 0; i < n; i++) {

        // Finding the ceil value
        // of each index
        a[i] = (a[i] + k - 1) / k;
    }

    for (int i = 0; i < n; i++) {

        // Finding the index with
        // maximum ceil value
        if (a[i] >= max_ceil) {
            max_ceil = a[i];
            index = i;
        }
    }

    return index;
}

// Driver code
int main()
{
    int arr[] = { 31, 12, 25, 27, 32, 19 };
    int K = 5;
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << findIndex(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java .io.*;

class GFG
{

    // Function that returns the index
    // which will be the last to become
    // zero after performing given operation
    static int findIndex(int[] a, int n, int k)
    {

        // Initialize the result
        int index = -1, max_ceil = Integer.MIN_VALUE;

        for (int i = 0; i < n; i++)
        {

            // Finding the ceil value
            // of each index
            a[i] = (a[i] + k - 1) / k;
        }

        for (int i = 0; i < n; i++)
        {

            // Finding the index with
            // maximum ceil value
            if (a[i] >= max_ceil)
            {
                max_ceil = a[i];
                index = i;
            }
        }

        return index;
    }

    // Driver code
    static public void main (String[] args)
    {
        int []arr = { 31, 12, 25, 27, 32, 19 };
        int K = 5;
        int N = arr.length ;

        System.out.print(findIndex(arr, N, K));
    }
}

// This code is contributed by anuj_67..
```

## 计算机编程语言

```
# Python implementation of the approach

# Function that returns the index
# which will be the last to become
# zero after performing given operation
def findIndex(a, n, k):

    # Initialize the result
    index = -1
    max_ceil = -10**9

    for i in range(n):

        # Finding the ceil value
        # of each index
        a[i] = (a[i] + k - 1) // k

    for i in range(n):

        # Finding the index with
        # maximum ceil value
        if (a[i] >= max_ceil):
            max_ceil = a[i]
            index = i

    return index

# Driver code

arr = [31, 12, 25, 27, 32, 19]
K = 5
N = len(arr)

print(findIndex(arr, N, K))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function that returns the index
    // which will be the last to become
    // zero after performing given operation
    static int findIndex(int[] a, int n, int k)
    {

        // Initialize the result
        int index = -1, max_ceil = int.MinValue;

        for (int i = 0; i < n; i++)
        {

            // Finding the ceil value
            // of each index
            a[i] = (a[i] + k - 1) / k;
        }

        for (int i = 0; i < n; i++)
        {

            // Finding the index with
            // maximum ceil value
            if (a[i] >= max_ceil)
            {
                max_ceil = a[i];
                index = i;
            }
        }

        return index;
    }

    // Driver code
    static public void Main ()
    {
        int []arr = { 31, 12, 25, 27, 32, 19 };
        int K = 5;
        int N = arr.Length ;

        Console.WriteLine(findIndex(arr, N, K));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// javascript implementation of the approach

// Function that returns the index
// which will be the last to become
// zero after performing given operation
function findIndex(a, n, k)
{

    // Initialize the result
    var index = -1, max_ceil = Number.MIN_VALUE;

    for (i = 0; i < n; i++)
    {

        // Finding the ceil value
        // of each index
        a[i] = (a[i] + k - 1) / k;
    }

    for (i = 0; i < n; i++)
    {

        // Finding the index with
        // maximum ceil value
        if (a[i] >= max_ceil)
        {
            max_ceil = a[i];
            index = i;
        }
    }

    return index;
}

// Driver code

var arr = [ 31, 12, 25, 27, 32, 19 ];
var K = 5;
var N = arr.length ;

document.write(findIndex(arr, N, K));

// This code is contributed by Amit Katiyar

</script>
```

**Output:** 

```
4
```