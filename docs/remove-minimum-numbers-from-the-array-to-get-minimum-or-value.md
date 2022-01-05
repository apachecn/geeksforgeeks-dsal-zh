# 从数组中移除最小数字以获得最小或值

> 原文:[https://www . geesforgeks . org/remove-从数组中移除最小数字以获取最小值或最大值/](https://www.geeksforgeeks.org/remove-minimum-numbers-from-the-array-to-get-minimum-or-value/)

给定一个由正整数 **N** 组成的数组 **arr[]** ，任务是找到要从数组中删除的最小元素数，以便最小化数组元素的按位或。不允许移除所有元素，即数组中必须至少保留一个元素。
**例:**

> **输入:** arr[] = {1，2，3}
> **输出:** 2
> 所有可能的子集，其中 OR 值为:
> a) {1，2，3} = 3
> b) {1，2} = 3
> c) {2，3} = 3
> d) {1，3 } = 3
> e){ 1 } = 1
> f){ 2 } = 2
> g){ 3 } = 3
> 所以，我们需要删除 2 个元素。
> **输入:** arr[] = {3，3，3}
> **输出:** 0

**天真方法:**生成所有可能的子序列，并测试哪一个给出最小的“或”值。假设最大子序列的长度和最小可能的 OR 为 **L** ，则答案为**N–L**。这需要指数级的时间。
**更好的方法:**最小值总是等于数组中存在的最小数。如果这个数与除自身之外的任何其他数按位“或”，则“或”的值将改变，并且不再保持最小值。因此，我们需要移除所有不等于这个最小元素的元素。

*   找出数组中最小的数字。
*   求数组中这个元素的频率，说 **cnt** 。
*   最终答案将是**N–CNT**。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum
// deletions to get minimum OR
int findMinDel(int* arr, int n)
{

    // To store the minimum element
    int min_num = INT_MAX;

    // Find the minimum element
    // from the array
    for (int i = 0; i < n; i++)
        min_num = min(arr[i], min_num);

    // To store the frequency of
    // the minimum element
    int cnt = 0;

    // Find the frequency of the
    // minimum element
    for (int i = 0; i < n; i++)
        if (arr[i] == min_num)
            cnt++;

    // Return the final answer
    return n - cnt;
}

// Driver code
int main()
{
    int arr[] = { 3, 3, 2 };
    int n = sizeof(arr) / sizeof(int);

    cout << findMinDel(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the minimum
// deletions to get minimum OR
static int findMinDel(int []arr, int n)
{

    // To store the minimum element
    int min_num = Integer.MAX_VALUE;

    // Find the minimum element
    // from the array
    for (int i = 0; i < n; i++)
        min_num = Math.min(arr[i], min_num);

    // To store the frequency of
    // the minimum element
    int cnt = 0;

    // Find the frequency of the
    // minimum element
    for (int i = 0; i < n; i++)
        if (arr[i] == min_num)
            cnt++;

    // Return the final answer
    return n - cnt;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 3, 3, 2 };
    int n = arr.length;

    System.out.print(findMinDel(arr, n));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import sys

# Function to return the minimum
# deletions to get minimum OR
def findMinDel(arr, n) :

    # To store the minimum element
    min_num = sys.maxsize;

    # Find the minimum element
    # from the array
    for i in range(n) :
        min_num = min(arr[i], min_num);

    # To store the frequency of
    # the minimum element
    cnt = 0;

    # Find the frequency of the
    # minimum element
    for i in range(n) :
        if (arr[i] == min_num) :
            cnt += 1;

    # Return the final answer
    return n - cnt;

# Driver code
if __name__ == "__main__" :

    arr = [ 3, 3, 2 ];
    n = len(arr);

    print(findMinDel(arr, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the minimum
// deletions to get minimum OR
static int findMinDel(int []arr, int n)
{

    // To store the minimum element
    int min_num = int.MaxValue;

    // Find the minimum element
    // from the array
    for (int i = 0; i < n; i++)
        min_num = Math.Min(arr[i],
                           min_num);

    // To store the frequency of
    // the minimum element
    int cnt = 0;

    // Find the frequency of the
    // minimum element
    for (int i = 0; i < n; i++)
        if (arr[i] == min_num)
            cnt++;

    // Return the readonly answer
    return n - cnt;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 3, 3, 2 };
    int n = arr.Length;

    Console.Write(findMinDel(arr, n));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the minimum
// deletions to get minimum OR
function findMinDel(arr, n)
{

    // To store the minimum element
    var min_num = 1000000000;

    // Find the minimum element
    // from the array
    for (var i = 0; i < n; i++)
        min_num = Math.min(arr[i], min_num);

    // To store the frequency of
    // the minimum element
    var cnt = 0;

    // Find the frequency of the
    // minimum element
    for (var i = 0; i < n; i++)
        if (arr[i] == min_num)
            cnt++;

    // Return the final answer
    return n - cnt;
}

// Driver code
var arr = [3, 3, 2];
var n = arr.length;
document.write( findMinDel(arr, n));

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(N)