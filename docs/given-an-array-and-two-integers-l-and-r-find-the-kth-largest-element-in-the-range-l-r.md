# 给定一个数组和两个整数 l 和 r，找到范围【l，r】

中第 k 个最大的元素

> 原文:[https://www . geeksforgeeks . org/给定一个数组和两个整数-l 和-r-查找范围内第 k 个最大元素-l-r/](https://www.geeksforgeeks.org/given-an-array-and-two-integers-l-and-r-find-the-kth-largest-element-in-the-range-l-r/)

给定一个由 **n** 个整数和一个整数 **k** 组成的未排序数组 **arr[]** ，任务是在给定的索引范围**【l】【r】**
**中找到最大的元素 **kth** 示例:**

> **输入:** arr[] = {5，3，2，4，1}，k = 4，l = 1，r = 5
> **输出:** 4
> 4 将是 arr[0…4]排序时的第 4 个元素。
> **输入:** arr[] = {1，4，2，3，5，7，6}，k = 3，l = 3，r = 6
> **输出:** 5

**方法:**一个简单的解决方案是对范围内的元素进行排序，得到 **kth** 最大的元素，对于每个查询，该解决方案的时间复杂度为 **nlog(n)** 。我们可以使用前缀数组和二分搜索法来解决 **log(n)** 中的每个查询。我们所要做的就是维护一个 2d 前缀数组，其中第**行和第**行包含的元素数量小于或等于第 **i** 行，且与给定数组的元素数量在同一范围内。前缀数组完成后，我们需要做的就是对前缀数组进行简单的二分搜索法运算。因此时间复杂度大大降低。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define MAX 1001
static int prefix[MAX][MAX];
int ar[MAX];

// Function to calculate the prefix
void cal_prefix(int n, int arr[])
{
    int i, j;

    // Creating one based indexing
    for (i = 0; i < n; i++)
        ar[i + 1] = arr[i];

    // Initializing and creating prefix array
    for (i = 1; i <= 1000; i++) {
        for (j = 0; j <= n; j++)
            prefix[i][j] = 0;

        for (j = 1; j <= n; j++) {

            // Creating a prefix array for every
            // possible value in a given range
            prefix[i][j] = prefix[i][j - 1]
                           + (int)(ar[j] <= i ? 1 : 0);
        }
    }
}

// Function to return the kth largest element
// in the index range [l, r]
int ksub(int l, int r, int n, int k)
{
    int lo, hi, mid;

    lo = 1;
    hi = 1000;

    // Binary searching through the 2d array
    // and only checking the range in which
    // the sub array is a part
    while (lo + 1 < hi) {
        mid = (lo + hi) / 2;
        if (prefix[mid][r] - prefix[mid][l - 1] >= k)
            hi = mid;
        else
            lo = mid + 1;
    }

    if (prefix[lo][r] - prefix[lo][l - 1] >= k)
        hi = lo;

    return hi;
}

// Driver code
int main()
{
    int arr[] = { 1, 4, 2, 3, 5, 7, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 4;

    // Creating the prefix array
    // for the given array
    cal_prefix(n, arr);

    // Queries
    int queries[][3] = { { 1, n, 1 },
                         { 2, n - 2, 2 },
                         { 3, n - 1, 3 } };
    int q = sizeof(queries) / sizeof(queries[0]);

    // Perform queries
    for (int i = 0; i < q; i++)
        cout << ksub(queries[i][0], queries[i][1],
                     n, queries[i][2])
             << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

static int MAX = 1001;
static int prefix[][] = new int[MAX][MAX];
static int ar[] = new int[MAX];

// Function to calculate the prefix
static void cal_prefix(int n, int arr[])
{
    int i, j;

    // Creating one based indexing
    for (i = 0; i < n; i++)
        ar[i + 1] = arr[i];

    // Initializing and creating prefix array
    for (i = 1; i <= 1000; i++)
    {
        for (j = 0; j <= n; j++)
            prefix[i][j] = 0;

        for (j = 1; j <= n; j++)
        {

            // Creating a prefix array for every
            // possible value in a given range
            prefix[i][j] = prefix[i][j - 1]
                        + (int)(ar[j] <= i ? 1 : 0);
        }
    }
}

// Function to return the kth largest element
// in the index range [l, r]
static int ksub(int l, int r, int n, int k)
{
    int lo, hi, mid;

    lo = 1;
    hi = 1000;

    // Binary searching through the 2d array
    // and only checking the range in which
    // the sub array is a part
    while (lo + 1 < hi)
    {
        mid = (lo + hi) / 2;
        if (prefix[mid][r] - prefix[mid][l - 1] >= k)
            hi = mid;
        else
            lo = mid + 1;
    }

    if (prefix[lo][r] - prefix[lo][l - 1] >= k)
        hi = lo;

    return hi;
}

// Driver code
public static void main(String args[])
{
    int arr[] = { 1, 4, 2, 3, 5, 7, 6 };
    int n = arr.length;
    int k = 4;

    // Creating the prefix array
    // for the given array
    cal_prefix(n, arr);

    // Queries
    int queries[][] = { { 1, n, 1 },
                        { 2, n - 2, 2 },
                        { 3, n - 1, 3 } };
    int q = queries.length;

    // Perform queries
    for (int i = 0; i < q; i++)
        System.out.println( ksub(queries[i][0], queries[i][1],
                    n, queries[i][2]));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of the approach

MAX = 1001
prefix = [[0 for i in range(MAX)]
             for j in range(MAX)]
ar = [0 for i in range(MAX)]

# Function to calculate the prefix
def cal_prefix(n, arr):

    # Creating one based indexing
    for i in range(n):
        ar[i + 1] = arr[i]

    # Initializing and creating prefix array
    for i in range(1, 1001, 1):
        for j in range(n + 1):
            prefix[i][j] = 0

        for j in range(1, n + 1):

            # Creating a prefix array for every
            # possible value in a given range
            if ar[j] <= i:
                k = 1
            else:
                k = 0
            prefix[i][j] = prefix[i][j - 1] + k

# Function to return the kth largest element
# in the index range [l, r]
def ksub(l, r, n, k):
    lo = 1
    hi = 1000

    # Binary searching through the 2d array
    # and only checking the range in which
    # the sub array is a part
    while (lo + 1 < hi):
        mid = int((lo + hi) / 2)
        if (prefix[mid][r] -
            prefix[mid][l - 1] >= k):
            hi = mid
        else:
            lo = mid + 1

    if (prefix[lo][r] -
        prefix[lo][l - 1] >= k):
        hi = lo

    return hi

# Driver code
if __name__ == '__main__':
    arr = [1, 4, 2, 3, 5, 7, 6]
    n = len(arr)
    k = 4

    # Creating the prefix array
    # for the given array
    cal_prefix(n, arr)

    # Queries
    queries = [[1, n, 1],
               [2, n - 2, 2],
               [3, n - 1, 3]]
    q = len(queries)

    # Perform queries
    for i in range(q):
        print(ksub(queries[i][0],
                   queries[i][1], n, queries[i][2]))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

static int MAX = 1001;
static int[,] prefix = new int[MAX,MAX];
static int[] ar = new int[MAX];

// Function to calculate the prefix
static void cal_prefix(int n, int[] arr)
{
    int i, j;

    // Creating one based indexing
    for (i = 0; i < n; i++)
        ar[i + 1] = arr[i];

    // Initializing and creating prefix array
    for (i = 1; i <= 1000; i++)
    {
        for (j = 0; j <= n; j++)
            prefix[i, j] = 0;

        for (j = 1; j <= n; j++)
        {

            // Creating a prefix array for every
            // possible value in a given range
            prefix[i, j] = prefix[i, j - 1]
                        + (int)(ar[j] <= i ? 1 : 0);
        }
    }
}

// Function to return the kth largest element
// in the index range [l, r]
static int ksub(int l, int r, int n, int k)
{
    int lo, hi, mid;

    lo = 1;
    hi = 1000;

    // Binary searching through the 2d array
    // and only checking the range in which
    // the sub array is a part
    while (lo + 1 < hi)
    {
        mid = (lo + hi) / 2;
        if (prefix[mid, r] - prefix[mid, l - 1] >= k)
            hi = mid;
        else
            lo = mid + 1;
    }

    if (prefix[lo, r] - prefix[lo, l - 1] >= k)
        hi = lo;

    return hi;
}

// Driver code
static void Main()
{
    int []arr = { 1, 4, 2, 3, 5, 7, 6 };
    int n = arr.Length;
    //int k = 4;

    // Creating the prefix array
    // for the given array
    cal_prefix(n, arr);

    // Queries
    int [,]queries = { { 1, n, 1 },
                        { 2, n - 2, 2 },
                        { 3, n - 1, 3 } };
    int q = queries.Length/queries.Rank-1;

    // Perform queries
    for (int i = 0; i < q; i++)
        Console.WriteLine( ksub(queries[i,0], queries[i,1],
                    n, queries[i, 2]));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach
$MAX = 101;
$prefix = array_fill(0, $MAX, array_fill(0, $MAX, 0));
$ar = array_fill(0, $MAX, 0);

// Function to calculate the prefix
function cal_prefix($n, $arr)
{
    global $prefix,$ar,$MAX;

    // Creating one based indexing
    for ($i = 0; $i < $n; $i++)
        $ar[$i + 1] = $arr[$i];

    // Initializing and creating prefix array
    for ($i = 1; $i <$MAX; $i++)
    {
        for ($j = 0; $j <= $n; $j++)
            $prefix[$i][$j] = 0;

        for ($j = 1; $j <= $n; $j++)
        {

            // Creating a prefix array for every
            // possible value in a given range
            $prefix[$i][$j] = $prefix[$i][$j - 1]
                        + (int)($ar[$j] <= $i ? 1 : 0);
        }
    }
}

// Function to return the kth largest element
// in the index range [l, r]
function ksub($l, $r, $n, $k)
{
    global $prefix, $ar, $MAX;
    $lo = 1;
    $hi = $MAX-1;

    // Binary searching through the 2d array
    // and only checking the range in which
    // the sub array is a part
    while ($lo + 1 < $hi)
    {
        $mid = (int)(($lo + $hi) / 2);
        if ($prefix[$mid][$r] - $prefix[$mid][$l - 1] >= $k)
            $hi = $mid;
        else
            $lo = $mid + 1;
    }

    if ($prefix[$lo][$r] - $prefix[$lo][$l - 1] >= $k)
        $hi = $lo;

    return $hi;
}

    // Driver code
    $arr = array( 1, 4, 2, 3, 5, 7, 6 );
    $n = count($arr);
    $k = 4;

    // Creating the prefix array
    // for the given array
    cal_prefix($n, $arr);

    // Queries
    $queries = array(array( 1, $n, 1 ),
                        array( 2, $n - 2, 2 ),
                        array( 3, $n - 1, 3 ));
    $q = count($queries);

    // Perform queries
    for ($i = 0; $i < $q; $i++)
        echo ksub($queries[$i][0], $queries[$i][1],$n, $queries[$i][2])."\n";

    // This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// Javascript implementation of the approach
let MAX = 101;
let prefix = new Array(MAX);

for (let i = 0; i < MAX; i++) {
    prefix[i] = new Array(MAX).fill(0)
}

let ar = new Array(MAX).fill(0);

// Function to calculate the prefix
function cal_prefix(n, arr) {

    // Creating one based indexing
    for (let i = 0; i < n; i++)
        ar[i + 1] = arr[i];

    // Initializing and creating prefix array
    for (let i = 1; i < MAX; i++) {
        for (let j = 0; j <= n; j++)
            prefix[i][j] = 0;

        for (let j = 1; j <= n; j++) {

            // Creating a prefix array for every
            // possible value in a given range
            prefix[i][j] = prefix[i][j - 1]
                + (ar[j] <= i ? 1 : 0);
        }
    }
}

// Function to return the kth largest element
// in the index range [l, r]
function ksub(l, r, n, k) {
    let lo = 1;
    let hi = MAX - 1;

    // Binary searching through the 2d array
    // and only checking the range in which
    // the sub array is a part
    while (lo + 1 < hi) {
        let mid = Math.floor((lo + hi) / 2);
        if (prefix[mid][r] - prefix[mid][l - 1] >= k)
            hi = mid;
        else
            lo = mid + 1;
    }

    if (prefix[lo][r] - prefix[lo][l - 1] >= k)
        hi = lo;

    return hi;
}

// Driver code
let arr = new Array(1, 4, 2, 3, 5, 7, 6);
let n = arr.length;
let k = 4;

// Creating the prefix array
// for the given array
cal_prefix(n, arr);

// Queries
let queries = new Array(new Array(1, n, 1),
    new Array(2, n - 2, 2),
    new Array(3, n - 1, 3));
let q = queries.length;

// Perform queries
for (let i = 0; i < q; i++)
    document.write(ksub(queries[i][0], queries[i][1], n, queries[i][2]) + "<br>");

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
1
3
5
```