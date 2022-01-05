# 将数组划分为两个奇数长度组，中间值

之间的绝对差值最小

> 原文:[https://www . geeksforgeeks . org/将数组划分为两个奇数长度组，中间值之间的绝对差值最小化/](https://www.geeksforgeeks.org/partition-the-array-into-two-odd-length-groups-with-minimized-absolute-difference-between-their-median/)

给定偶数长度正整数的数组 **arr[]** ，任务是将这些 **arr[]** 的元素分成两组，每组奇数长度，使得两组中间值之间的绝对差值最小。
**例:**

> **输入:** arr[] = { 1，2，3，4，5，6 }
> **输出:** 1
> **说明:**
> 第 1 组可以是带中位数 4 的【2，4，6】
> 第 2 组可以是带中位数 3 的【1，3，5】。
> 两个中间值的绝对差值为 4–3 = 1，这是任何一种分组都无法进一步缩小的。
> **输入:** arr[] = { 15，25，35，50 }
> **输出:** 10
> **说明:**
> 第 1 组可以是中位数为 25 的【15，25，50】
> 第 2 组可以是中位数为 35 的【35】。
> 两个中间值的绝对差值是 35–25 = 10，这是任何一种分组都无法进一步缩小的。

**进场:**

*   如果给定数组 **arr[]** 被排序， **arr[]** 的中间元素将给出最小的差异。
*   所以把**arr【】**分开，这样这两个元素就是两个奇数长度的新数组的中间值。
*   因此，将第一组 arr[]的 **n/2 <sup>第</sup>T3】元素和第二组 arr[]的**(n/2–1)<sup>第</sup>T7】元素分别作为中位数。****
*   那么**ABS(arr[n/2]–arr[(n/2)-1])**就是两个新数组的最小差。

以下是上述方法的实现:

## C++

```
// C++ program to minimise the
// median between partition array

#include "bits/stdc++.h"
using namespace std;

// Function to find minimise the
// median between partition array
int minimiseMedian(int arr[], int n)
{
    // Sort the given array arr[]
    sort(arr, arr + n);

    // Return the difference of two
    // middle element of the arr[]
    return abs(arr[n / 2] - arr[(n / 2) - 1]);
}

// Driver Code
int main()
{
    int arr[] = { 15, 25, 35, 50 };

    // Size of arr[]
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function that returns the minimum
    // the absolute difference between
    // median of partition array
    cout << minimiseMedian(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to minimise the
// median between partition array
import java.util.*;

class GFG
{

    // Function to find minimise the
    // median between partition array
    static int minimiseMedian(int arr[], int n)
    {
        // Sort the given array arr[]
        Arrays.sort(arr);

        // Return the difference of two
        // middle element of the arr[]
        return Math.abs(arr[n / 2] - arr[(n / 2) - 1]);
    }

    // Driver Code
    public static void main (String[] args)
    {
        int arr[] = { 15, 25, 35, 50 };

        // Size of arr[]
        int n = arr.length;

        // Function that returns the minimum
        // the absolute difference between
        // median of partition array
        System.out.println(minimiseMedian(arr, n));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 program to minimise the
# median between partition array

# Function to find minimise the
# median between partition array
def minimiseMedian(arr, n) :

    # Sort the given array arr[]
    arr.sort();

    # Return the difference of two
    # middle element of the arr[]
    ans = abs(arr[n // 2] - arr[(n // 2) - 1]);

    return ans;

# Driver Code
if __name__ == "__main__" :

    arr = [ 15, 25, 35, 50 ];

    # Size of arr[]
    n = len(arr);

    # Function that returns the minimum
    # the absolute difference between
    # median of partition array
    print(minimiseMedian(arr, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to minimise the
// median between partition array
using System;

class GFG
{

    // Function to find minimise the
    // median between partition array
    static int minimiseMedian(int []arr, int n)
    {
        // Sort the given array []arr
        Array.Sort(arr);

        // Return the difference of two
        // middle element of the []arr
        return Math.Abs(arr[n / 2] - arr[(n / 2) - 1]);
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int []arr = { 15, 25, 35, 50 };

        // Size of []arr
        int n = arr.Length;

        // Function that returns the minimum
        // the absolute difference between
        // median of partition array
        Console.WriteLine(minimiseMedian(arr, n));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to minimise the
// median between partition array

// Function to find minimise the
// median between partition array
function minimiseMedian(arr, n) {
    // Sort the given array arr[]
    arr.sort((a, b) => a - b);

    // Return the difference of two
    // middle element of the arr[]
    return Math.abs(arr[n / 2] - arr[(n / 2) - 1]);
}

// Driver Code
let arr = [15, 25, 35, 50];

// Size of arr[]
let n = arr.length;

// Function that returns the minimum
// the absolute difference between
// median of partition array
document.write(minimiseMedian(arr, n));

// This code is contributed by gfgking

</script>
```

**Output:** 

```
10
```

**时间复杂度:** O(N*log N)