# 当给定原始元素的平均值时，从数组中找出删除的值

> 原文:[https://www . geeksforgeeks . org/当给定原始元素的平均值时，从数组中查找删除的值/](https://www.geeksforgeeks.org/find-the-deleted-value-from-the-array-when-average-of-original-elements-is-given/)

给定一组长度 **N + K** 。也给出了数组中所有元素的平均值 **avg** 。如果一个恰好出现在 **K** 时间的元素从数组中被移除(所有出现的)并且结果数组被给出，任务是找到元素 **X** 。**注意**如果 **X** 不是整数，则打印 **-1** 。
**示例:**

> **输入:** arr[] = {2，7，3}，K = 3，avg = 4
> **输出:** 4
> 原始数组为{2，7，3，4，4，4}
> ，其中删除了 3 次出现的 4。
> (2 + 7 + 3 + 4 + 4 + 4) / 6 = 4
> 
> **输入:** arr[] = {5，2，3}，K = 4，avg = 7；
> **输出:** -1
> 所需元素为 9.75，不是整数。

**进场:**

*   求数组元素的和，存储在变量 **sum** 中。
*   既然 **X** 出现了 **K** 次那么原阵之和将是 **sumOrg = sum + (X * K)** 。
*   平均值为**平均值**，即**平均值= sumOrg / (N + K)** 。
*   现在， **X** 可以很容易地计算为 **X =((平均值*(N+K))–总和)/ K**

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the missing element
int findMissing(int arr[], int n, int k, int avg)
{

    // Find the sum of the array elements
    int sum = 0;
    for (int i = 0; i < n; i++) {
        sum += arr[i];
    }

    // The numerator and the denominator
    // of the equation
    int num = (avg * (n + k)) - sum;
    int den = k;

    // If not divisible then X is
    // not an integer
    // it is a floating point number
    if (num % den != 0)
        return -1;

    // Return X
    return (num / den);
}

// Driver code
int main()
{
    int k = 3, avg = 4;
    int arr[] = { 2, 7, 3 };
    int n = sizeof(arr) / sizeof(int);

    cout << findMissing(arr, n, k, avg);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to return the missing element
    static int findMissing(int arr[], int n,
                           int k, int avg)
    {

        // Find the sum of the array elements
        int sum = 0;
        for (int i = 0; i < n; i++)
        {
            sum += arr[i];
        }

        // The numerator and the denominator
        // of the equation
        int num = (avg * (n + k)) - sum;
        int den = k;

        // If not divisible then X is
        // not an integer
        // it is a floating point number
        if (num % den != 0)
            return -1;

        // Return X
        return (int)(num / den);
    }

    // Driver code
    public static void main (String[] args)
    {
        int k = 3, avg = 4;
        int arr[] = { 2, 7, 3 };
        int n = arr.length;

        System.out.println(findMissing(arr, n, k, avg));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the missing element
def findMissing(arr, n, k, avg):

    # Find the sum of the array elements
    sum = 0;
    for i in range(n):
        sum += arr[i];

    # The numerator and the denominator
    # of the equation
    num = (avg * (n + k)) - sum;
    den = k;

    # If not divisible then X is
    # not an integer
    # it is a floating ponumber
    if (num % den != 0):
        return -1;

    # Return X
    return (int)(num / den);

# Driver code
k = 3; avg = 4;
arr = [2, 7, 3] ;
n = len(arr);

print(findMissing(arr, n, k, avg));

# This code is contributed by 29AjayKumar
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

    // Function to return the missing element
    static int findMissing(int []arr, int n,
                           int k, int avg)
    {

        // Find the sum of the array elements
        int sum = 0;
        for (int i = 0; i < n; i++)
        {
            sum += arr[i];
        }

        // The numerator and the denominator
        // of the equation
        int num = (avg * (n + k)) - sum;
        int den = k;

        // If not divisible then X is
        // not an integer
        // it is a floating point number
        if (num % den != 0)
            return -1;

        // Return X
        return (int)(num / den);
    }

    // Driver code
    public static void Main (String[] args)
    {
        int k = 3, avg = 4;
        int []arr = { 2, 7, 3 };
        int n = arr.Length;

        Console.WriteLine(findMissing(arr, n, k, avg));
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript implementation of the
// above approach

// Function to return the missing element
function findMissing(arr, n, k, avg)
{

    // Find the sum of the array elements
    var sum = 0;
    for (var i = 0; i < n; i++) {
        sum += arr[i];
    }

    // The numerator and the denominator
    // of the equation
    var num = (avg * (n + k)) - sum;
    var den = k;

    // If not divisible then X is
    // not an integer
    // it is a floating point number
    if (num % den != 0)
        return -1;

    // Return X
    return (Math.floor(num / den));
}

// Driver code
var k = 3;
var avg = 4;
var arr = [ 2, 7, 3 ];
var n = arr.length;
document.write(findMissing(arr, n, k, avg));

// This code is contributed by ShubhamSingh10
</script>
```

**Output:** 

```
4
```

**时间复杂度:**O(1)
T3】辅助空间: O(1)