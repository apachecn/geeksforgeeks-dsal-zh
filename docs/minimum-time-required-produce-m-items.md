# 生产 m 个产品所需的最短时间

> 原文:[https://www . geesforgeks . org/最短所需时间-生产-m-items/](https://www.geeksforgeeks.org/minimum-time-required-produce-m-items/)

考虑 **n** 台机器，它们生产相同类型的物品，但速度不同，即机器 1 需要 <sub>1</sub> 秒来生产物品，机器 2 需要 <sub>2</sub> 秒来生产物品。给定一个数组，该数组包含第一台<sup>机器生产一个产品所需的时间。考虑到所有机器同时工作，任务是找到生产 **m** 项所需的最短时间。</sup>

**示例:**

```
Input : arr[] = {1, 2, 3}, m = 11
Output : 6
In 6 sec, machine 1 produces 6 items, machine 2 produces 3 items,
and machine 3 produces 2 items. So to produce 11 items minimum
6 sec are required.

Input : arr[] = {5, 6}, m = 11
Output : 30
```

**方法一:(蛮力)**
初始化时间= 0，递增 1。计算每次生产的产品数量，直到生产的产品数量不等于 m。

下面是上述想法的实现:

## C++

```
// C++ program to find minimum time
// required to produce m items.
#include<bits/stdc++.h>
using namespace std;

// Return the minimum time required to
// produce m items with given machines.
int minTime(int arr[], int n, int m)
{
    // Initialize time, items equal to 0.
    int t = 0;

    while (1)
    {
        int items = 0;

        // Calculating items at each second
        for (int i = 0; i < n; i++)
            items += (t / arr[i]);

        // If items equal to m return time.
        if (items >= m)
            return t;

        t++; // Increment time
    }
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3 };
    int n = sizeof(arr)/sizeof(arr[0]);
    int m = 11;

    cout << minTime(arr, n, m) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum time
// required to produce m items.
import java.io.*;

public class GFG{

// Return the minimum time required to
// produce m items with given machines.
static int minTime(int []arr, int n,
                   int m)
{

    // Initialize time, items equal to 0.
    int t = 0;

    while (true)
    {
        int items = 0;

        // Calculating items at each second
        for (int i = 0; i < n; i++)
            items += (t / arr[i]);

        // If items equal to m return time.
        if (items >= m)
            return t;

        t++; // Increment time
    }
}

    // Driver Code
    static public void main (String[] args)
    {
            int []arr = { 1, 2, 3 };
            int n = arr.length;
            int m = 11;

    System.out.println(minTime(arr, n, m));
    }
}

// This code is contributed by vt_m.
```

## 计算机编程语言

```
# Python3 program to find minimum time
# required to produce m items.
import math as mt

# Return the minimum time required to
# produce m items with given machines.
def minTime(arr, n, m):

    # Initialize time, items equal to 0.
    t = 0

    while (1):

        items = 0

        # Calculating items at each second
        for i in range(n):
            items += (t // arr[i])

        # If items equal to m return time.
        if (items >= m):
            return t

        t += 1 # Increment time

# Driver Code
arr = [1, 2, 3]
n = len(arr)
m = 11

print(minTime(arr, n, m) )

# This code is contributed by
# Mohit kumar 29
```

## C#

```
// C# program to find minimum time
// required to produce m items.
using System;

public class GFG{

// Return the minimum time
// required to produce m
// items with given machines.
static int minTime(int []arr, int n,
                   int m)
{

    // Initialize time, items equal to 0.
    int t = 0;

    while (true)
    {
        int items = 0;

        // Calculating items at each second
        for (int i = 0; i < n; i++)
            items += (t / arr[i]);

        // If items equal to m return time.
        if (items >= m)
            return t;

        t++; // Increment time
    }
}

// Driven Code
static public void Main (String []args)
{
    int []arr = {1, 2, 3};
    int n = arr.Length;
    int m = 11;

    // Calling function
    Console.WriteLine(minTime(arr, n, m));

}
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum time
// required to produce m items.

// Return the minimum time required to
// produce m items with given machines.
function minTime($arr, $n, $m)
{

    // Initialize time, items
    // equal to 0.
    $t = 0;

    while (1)
    {
        $items = 0;

        // Calculating items at each second
        for ( $i = 0; $i < $n; $i++)
            $items += ($t / $arr[$i]);

        // If items equal to m return time.
        if ($items >= $m)
            return $t;

        $t++; // Increment time
    }
}

    // Driver Code
    $arr = array(1, 2, 3);
    $n =count($arr);
    $m = 11;
    echo minTime($arr, $n, $m);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// JavaScript program to find minimum time
// required to produce m items.

// Return the minimum time required to
// produce m items with given machines.
function minTime(arr, n, m)
{

    // Initialize time, items equal to 0.
    let t = 0;

    while (true)
    {
        let items = 0;

        // Calculating items at each second
        for (let i = 0; i < n; i++)
            items += (t / arr[i]);

        // If items equal to m return time.
        if (items >= m)
            return t;

        t++; // Increment time
    }
}

// Driver Code
    let arr = [ 1, 2, 3 ];
    let n = arr.length;
    let m = 11;

    document.write(minTime(arr, n, m));

</script>
```

**输出:**

```
6
```

**方法二(高效):**
思路是用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)。生产 m 个物品所需的最大可能时间将是阵列中的最大时间，a <sub>max</sub> ，乘以 m 即 **a <sub>max</sub> * m** 。因此，使用 1 到 a <sub>最大值</sub> * m 之间的二分搜索法，并找出产生 m 个项目的最小时间。

下面是上述想法的实现:

## C++

```
// Efficient C++ program to find minimum time
// required to produce m items.
#include<bits/stdc++.h>
using namespace std;

// Return the number of items can be
// produced in temp sec.
int findItems(int arr[], int n, int temp)
{
    int ans = 0;
    for (int i = 0; i < n; i++)
        ans += (temp/arr[i]);
    return ans;
}

// Binary search to find minimum time required
// to produce M items.
int bs(int arr[], int n, int m, int high)
{
    int low = 1;

    // Doing binary search to find minimum
    // time.
    while (low < high)
    {
        // Finding the middle value.
        int mid = (low+high)>>1;

        // Calculate number of items to
        // be produce in mid sec.
        int itm = findItems(arr, n, mid);

        // If items produce is less than
        // required, set low = mid + 1.
        if (itm < m)
            low = mid+1;

        //  Else set high = mid.
        else
            high = mid;
    }

    return high;
}

// Return the minimum time required to
// produce m items with given machine.
int minTime(int arr[], int n, int m)
{
    int maxval = INT_MIN;

    // Finding the maximum time in the array.
    for (int i = 0; i < n; i++)
        maxval = max(maxval, arr[i]);

    return bs(arr, n, m, maxval*m);
}

// Driven Program
int main()
{
    int arr[] = { 1, 2, 3 };
    int n = sizeof(arr)/sizeof(arr[0]);
    int m = 11;

    cout << minTime(arr, n, m) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Efficient Java program to find
// minimum time required to
// produce m items.
import java.io.*;

public class GFG{

// Return the number of items can
// be produced in temp sec.
static int findItems(int []arr, int n,
                     int temp)
{
    int ans = 0;
    for (int i = 0; i < n; i++)
        ans += (temp / arr[i]);
    return ans;
}

// Binary search to find minimum time
// required to produce M items.
static int bs(int []arr, int n,
              int m, int high)

{
    int low = 1;

    // Doing binary search to
    // find minimum time.
    while (low < high)
    {
        // Finding the middle value.
        int mid = (low + high) >> 1;

        // Calculate number of items to
        // be produce in mid sec.
        int itm = findItems(arr, n, mid);

        // If items produce is less than
        // required, set low = mid + 1.
        if (itm < m)
            low = mid + 1;

        // Else set high = mid.
        else
            high = mid;
    }

    return high;
}

// Return the minimum time required to
// produce m items with given machine.
static int minTime(int []arr, int n,
                   int m)
{
    int maxval = Integer.MIN_VALUE;

    // Finding the maximum time in the array.
    for (int i = 0; i < n; i++)
        maxval = Math.max(maxval, arr[i]);

    return bs(arr, n, m, maxval * m);
}

// Driven Program
static public void main (String[] args)
{
    int []arr = {1, 2, 3};
        int n = arr.length;
    int m = 11;

    System.out.println(minTime(arr, n, m));
}
}

// This code is contributed by vt_m.
```

## 计算机编程语言

```
# Efficient Python3 program to find
# minimum time required to produce m items.
import sys

def findItems(arr, n, temp):
    ans = 0
    for i in range(n):
        ans += temp // arr[i]
    return ans

# Binary search to find minimum time
# required to produce M items.
def bs(arr, n, m, high):
    low = 1

    # Doing binary search to find minimum
    # time.
    while low < high:

        # Finding the middle value.
        mid = (low + high) >> 1

        # Calculate number of items to
        # be produce in mid sec.
        itm = findItems(arr, n, mid)

        # If items produce is less than
        # required, set low = mid + 1.
        if itm < m:
            low = mid + 1

        # Else set high = mid.
        else:
            high = mid
    return high

# Return the minimum time required to
# produce m items with given machine.
def minTime(arr, n, m):
    maxval = -sys.maxsize

    # Finding the maximum time in the array.
    for i in range(n):
        maxval = max(maxval, arr[i])

    return bs(arr, n, m, maxval * m)

# Driver Code
if __name__ == "__main__":
    arr = [1, 2, 3]
    n = len(arr)
    m = 11
    print(minTime(arr, n, m))

# This code is contributed by
# sanjeev2552
```

## C#

```
// Efficient C# program to find
// minimum time required to
// produce m items.
using System;

public class GFG{

// Return the number of items can
// be produced in temp sec.
static int findItems(int []arr, int n,
                     int temp)
{
    int ans = 0;
    for (int i = 0; i < n; i++)
        ans += (temp / arr[i]);
    return ans;
}

// Binary search to find minimum time
// required to produce M items..
static int bs(int []arr, int n,
              int m, int high)
{
    int low = 1;

    // Doing binary search to
    // find minimum time.
    while (low < high)
    {
        // Finding the middle value.
        int mid = (low + high) >> 1;

        // Calculate number of items to
        // be produce in mid sec.
        int itm = findItems(arr, n, mid);

        // If items produce is less than
        // required, set low = mid + 1.
        if (itm < m)
            low = mid + 1;

        // Else set high = mid.
        else
            high = mid;
    }

    return high;
}

// Return the minimum time required to
// produce m items with given machine.
static int minTime(int []arr, int n,
                   int m)
{
    int maxval = int.MinValue;

    // Finding the maximum time in the array.
    for (int i = 0; i < n; i++)
        maxval = Math.Max(maxval, arr[i]);

    return bs(arr, n, m, maxval * m);
}

// Driver Code
static public void Main ()
{
    int []arr = {1, 2, 3};
    int n = arr.Length;
    int m = 11;

    Console.WriteLine(minTime(arr, n, m));
}
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Efficient PHP program to find minimum
// time required to produce m items.

// Return the number of items can be
// produced in temp sec.
function findItems( $arr, $n, $temp)
{
    $ans = 0;
    for($i = 0; $i < $n; $i++)
        $ans += ($temp / $arr[$i]);
    return $ans;
}

// Binary search to find minimum
// time required to produce M items.
function bs($arr, $n, $m, $high)
{
    $low = 1;

    // Doing binary search to
    // find minimum time.
    while ($low < $high)
    {

        // Finding the middle value.
        $mid = ($low + $high) >> 1;

        // Calculate number of items to
        // be produce in mid sec.
        $itm = findItems($arr, $n, $mid);

        // If items produce is less than
        // required, set low = mid + 1.
        if ($itm < $m)
            $low = $mid + 1;

        // Else set high = mid.
        else
            $high = $mid;
    }

    return $high;
}

// Return the minimum time required to
// produce m items with given machine.
function minTime($arr, $n, $m)
{
    $maxval = PHP_INT_MIN;

    // Finding the maximum
    // time in the array.
    for($i = 0; $i < $n; $i++)
        $maxval = max($maxval, $arr[$i]);

    return bs($arr, $n, $m, $maxval*$m);
}

    // Driver Code
    $arr = array(1, 2, 3);
    $n = count($arr);
    $m = 11;

    echo minTime($arr, $n, $m);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
// Efficient Javascript program to find
// minimum time required to
// produce m items.

// Return the number of items can
// be produced in temp sec.
function findItems(arr,n,temp)
{
    let ans = 0;
    for (let i = 0; i < n; i++)
        ans += Math.floor(temp / arr[i]);
    return ans;
}

// Binary search to find minimum time
// required to produce M items.
function bs(arr,n,m,high)
{
    let low = 1;

    // Doing binary search to
    // find minimum time.
    while (low < high)
    {
        // Finding the middle value.
        let mid = (low + high) >> 1;

        // Calculate number of items to
        // be produce in mid sec.
        let itm = findItems(arr, n, mid);

        // If items produce is less than
        // required, set low = mid + 1.
        if (itm < m)
            low = mid + 1;

        // Else set high = mid.
        else
            high = mid;
    }

    return high;
}

// Return the minimum time required to
// produce m items with given machine.
function minTime(arr,n,m)
{
    let maxval = Number.MIN_VALUE;

    // Finding the maximum time in the array.
    for (let i = 0; i < n; i++)
        maxval = Math.max(maxval, arr[i]);

    return bs(arr, n, m, maxval * m);
}

// Driven Program
let arr=[1, 2, 3];
let n = arr.length;
let m = 11;
document.write(minTime(arr, n, m));

// This code is contributed by patel2127
</script>
```

**输出:**

```
6
```

本文由 [**Anuj Chauhan**](https://www.facebook.com/anuj0503) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。