# 大于和不小于

的查询

> 原文:[https://www.geeksforgeeks.org/queries-greater-not-less/](https://www.geeksforgeeks.org/queries-greater-not-less/)

给定一组 **N 个**整数。将有 **Q** 查询，每个查询包括两个整数形式的 **q** 和 **x** ，0 < = q < = 1。查询有两种类型:

*   在第一个查询(q = 0)中，任务是查找不小于 x(或大于或等于 x)的整数的计数。

*   在第二个查询(q = 1)中，任务是查找大于 x 的整数的计数。

示例:

```
Input : arr[] = { 1, 2, 3, 4 } and Q = 3
        Query 1: 0 5
        Query 2: 1 3
        Query 3: 0 3
Output :0
        1
        2
Explanation:
x = 5, q = 0 : There are no elements greater than or equal to it.
x = 3, q = 1 : There is one element greater than 3 which is 4.
x = 3, q = 0 : There are two elements greater than or equal to 3.
```

**方法 1:** 一种**朴素方法**可以针对每个查询，遍历整个数组并计算小于或大于 x 的整数，具体取决于 Q。这种方法的时间复杂度为 **O(Q*N)** 。
**方法 2:** 一种**高效的**方法可以对数组进行排序，并对每个查询使用二分搜索法。这需要 **O(NlogN + QlogN)** 。
以下是本办法的实施情况:

## C++

```
// C++ to find number of integer less or greater given
// integer queries
#include<bits/stdc++.h>
using namespace std;

// Return the index of integer which are not less than x
// (or greater than or equal to x)
int lower_bound(int arr[], int start, int end, int x)
{
    while (start < end)
    {
        int mid = (start + end)>>1;
        if (arr[mid] >= x)
            end = mid;
        else
            start = mid + 1;
    }

    return start;
}

// Return the index of integer which are greater than x.
int upper_bound(int arr[], int start, int end, int x)
{
    while (start < end)
    {
        int mid = (start + end)>>1;
        if (arr[mid] <= x)
            start = mid + 1;
        else
            end = mid;
    }

    return start;
}

void query(int arr[], int n, int type, int x)
{
    // Counting number of integer which are greater than x.
    if (type)
        cout << n - upper_bound(arr, 0, n, x) << endl;

    // Counting number of integer which are not less than x
    // (Or greater than or equal to x)
    else
        cout << n - lower_bound(arr, 0, n, x) << endl;
}

// Driven Program
int main()
{
    int arr[] = { 1, 2, 3, 4 };
    int n = sizeof(arr)/sizeof(arr[0]);

    sort(arr, arr + n);

    query(arr, n, 0, 5);
    query(arr, n, 1, 3);
    query(arr, n, 0, 3);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java to find number of integer
// less or greater given
// integer queries
import java.util.Arrays;
class GFG
{
// Return the index of integer
// which are not less than x
// (or greater than or equal
// to x)
static int lower_bound(int arr[], int start,
                            int end, int x)
{
    while (start < end)
    {
        int mid = (start + end)>>1;
        if (arr[mid] >= x)
            end = mid;
        else
            start = mid + 1;
    }

    return start;
}

// Return the index of integer
// which are greater than x.
static int upper_bound(int arr[], int start, int end, int x)
{
    while (start < end)
    {
        int mid = (start + end)>>1;
        if (arr[mid] <= x)
            start = mid + 1;
        else
            end = mid;
    }

    return start;
}

static void query(int arr[], int n, int type, int x)
{
    // Counting number of integer
    // which are greater than x.
    if (type==1)
        System.out.println(n - upper_bound(arr, 0, n, x));

    // Counting number of integer which
    // are not less than x (Or greater
    // than or equal to x)
    else
        System.out.println(n - lower_bound(arr, 0, n, x));
}

// Driver code
public static void main (String[] args)
{
    int arr[] = { 1, 2, 3, 4 };
    int n = arr.length;

    Arrays.sort(arr);

    query(arr, n, 0, 5);
    query(arr, n, 1, 3);
    query(arr, n, 0, 3);
}
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to find number of integer
# less or greater given integer queries

# Return the index of integer 
# which are not less than x
# (or greater than or equal to x)
def lower_bound(arr, start, end, x):

    while (start < end):

        mid = (start + end) >> 1
        if (arr[mid] >= x):
            end = mid
        else:
            start = mid + 1

    return start

# Return the index of integer
# which are greater than x.
def upper_bound(arr, start, end, x):

    while (start < end):

        mid = (start + end) >> 1
        if (arr[mid] <= x):
            start = mid + 1
        else:
            end = mid

    return start

def query(arr, n, type, x):

    # Counting number of integer
    # which are greater than x.
    if (type == 1):
        print(n - upper_bound(arr, 0, n, x))

    # Counting number of integer
    # which are not less than x
    # (Or greater than or equal to x)
    else:
        print(n - lower_bound(arr, 0, n, x))

# Driver code
arr = [ 1, 2, 3, 4 ]
n =len(arr)

arr.sort()

query(arr, n, 0, 5)
query(arr, n, 1, 3)
query(arr, n, 0, 3)

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# to find number of integer less
// or greater given integer queries
using System;

class GFG {

// Return the index of integer which are
// not less than x (or greater than or
// equal to x)
static int lower_bound(int []arr, int start,
                             int end, int x)
{
    while (start < end)
    {
        int mid = (start + end)>>1;
        if (arr[mid] >= x)
            end = mid;
        else
            start = mid + 1;
    }

    return start;
}

// Return the index of integer
// which are greater than x.
static int upper_bound(int []arr, int start,
                             int end, int x)
{
    while (start < end)
    {
        int mid = (start + end)>>1;
        if (arr[mid] <= x)
            start = mid + 1;
        else
            end = mid;
    }

    return start;
}

static void query(int []arr, int n, int type, int x)
{
    // Counting number of integer
    // which are greater than x.
    if (type==1)
        Console.WriteLine(n - upper_bound(arr, 0, n, x));

    // Counting number of integer which
    // are not less than x (Or greater
    // than or equal to x)
    else
        Console.WriteLine(n - lower_bound(arr, 0, n, x));
}

// Driver code
public static void Main ()
{
    int []arr = {1, 2, 3, 4};
    int n = arr.Length;

    Array.Sort(arr);

    query(arr, n, 0, 5);
    query(arr, n, 1, 3);
    query(arr, n, 0, 3);
}
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP to find number of integer
// less or greater given
// integer queries

// Return the index of integer
// which are not less than x
// (or greater than or equal to x)
function lower_bound($arr, $start, $end, $x)
{
    while ($start < $end)
    {
    $mid = ($start + $end) >> 1;
        if ($arr[$mid] >= $x)
            $end = $mid;
        else
            $start = $mid + 1;
    }

    return $start;
}

// Return the index of integer
// which are greater than x.
function upper_bound($arr, $start, $end, $x)
{
    while ($start < $end)
    {
        $mid = ($start + $end) >> 1;
        if ($arr[$mid] <= $x)
            $start = $mid + 1;
        else
            $end = $mid;
    }

    return $start;
}

function query($arr, $n, $type, $x)
{

    // Counting number of integer
    // which are greater than x.
    if ($type)
        echo $n - upper_bound($arr, 0, $n, $x) ,"\n";

    // Counting number of integer
    // which are not less than x
    // (Or greater than or equal to x)
    else
        echo $n - lower_bound($arr, 0, $n, $x) ,"\n";
}

    // Driver Code
    $arr = array(1, 2, 3, 4);
    $n = count($arr);

    sort($arr);

    query($arr, $n, 0, 5);
    query($arr, $n, 1, 3);
    query($arr, $n, 0, 3);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// JavaScript program to find number of integer
// less or greater given
// integer queries

// Return the index of integer
// which are not less than x
// (or greater than or equal
// to x)
function lower_bound(arr, start,
                            end, x)
{
    while (start < end)
    {
        let mid = (start + end)>>1;
        if (arr[mid] >= x)
            end = mid;
        else
            start = mid + 1;
    }

    return start;
}

// Return the index of integer
// which are greater than x.
function upper_bound(arr, start, end, x)
{
    while (start < end)
    {
        let mid = (start + end)>>1;
        if (arr[mid] <= x)
            start = mid + 1;
        else
            end = mid;
    }

    return start;
}

function query(arr, n, type, x)
{
    // Counting number of integer
    // which are greater than x.
    if (type==1)
        document.write(n - upper_bound(arr, 0, n, x) + "<br/>");

    // Counting number of integer which
    // are not less than x (Or greater
    // than or equal to x)
    else
        document.write(n - lower_bound(arr, 0, n, x) + "<br/>");
}

// Driver code
    let arr = [ 1, 2, 3, 4 ];
    let n = arr.length;

    arr.sort();

    query(arr, n, 0, 5);
    query(arr, n, 1, 3);
    query(arr, n, 0, 3);

</script>
```

**输出:**

```
0
1
2
```

**时间复杂度:** O( (N + Q) * logN。

本文由 [**Anuj Chauhan**](https://www.facebook.com/anuj0503) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。