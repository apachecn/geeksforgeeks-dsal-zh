# 求排序数组中大于 k 的元素个数

> 原文:[https://www . geeksforgeeks . org/find-在排序数组中查找大于 k 的元素数/](https://www.geeksforgeeks.org/find-the-number-of-elements-greater-than-k-in-a-sorted-array/)

给定一个整数排序数组 **arr[]** 和一个整数 **k** ，任务是找出数组中大于 **k** 的元素个数。**注意****k**可能存在也可能不存在于数组中。
**举例:**

> **输入:** arr[] = {2，3，5，6，6，9}，k = 6
> **输出:** 1
> **输入:** arr[] = {1，1，2，5，5，7}，k = 8
> **输出:** 0

**方法:**思路是执行[二分搜索法](https://www.geeksforgeeks.org/binary-search/)找到大于 k 的元素个数
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of elements
// from the array which are greater than k
int countGreater(int arr[], int n, int k)
{
    int l = 0;
    int r = n - 1;

    // Stores the index of the left most element
    // from the array which is greater than k
    int leftGreater = n;

    // Finds number of elements greater than k
    while (l <= r) {
        int m = l + (r - l) / 2;

        // If mid element is greater than
        // k update leftGreater and r
        if (arr[m] > k) {
            leftGreater = m;
            r = m - 1;
        }

        // If mid element is less than
        // or equal to k update l
        else
            l = m + 1;
    }

    // Return the count of elements greater than k
    return (n - leftGreater);
}

// Driver code
int main()
{
    int arr[] = { 3, 3, 4, 7, 7, 7, 11, 13, 13 };
    int n = sizeof(arr) / sizeof(arr[0]);

    int k = 7;

    cout << countGreater(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the count of elements
// from the array which are greater than k
static int countGreater(int arr[], int n, int k)
{
    int l = 0;
    int r = n - 1;

    // Stores the index of the left most element
    // from the array which is greater than k
    int leftGreater = n;

    // Finds number of elements greater than k
    while (l <= r) {
        int m = l + (r - l) / 2;

        // If mid element is greater than
        // k update leftGreater and r
        if (arr[m] > k) {
            leftGreater = m;
            r = m - 1;
        }

        // If mid element is less than
        // or equal to k update l
        else
            l = m + 1;
    }

    // Return the count of elements greater than k
    return (n - leftGreater);
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 3, 3, 4, 7, 7, 7, 11, 13, 13 };
    int n = arr.length;

    int k = 7;

    System.out.println(countGreater(arr, n, k));
}
}

// This code is contributed by Code_Mech
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to return the count of elements
# from the array which are greater than k
def countGreater(arr, n, k):
    l = 0
    r = n - 1

    # Stores the index of the left most element
    # from the array which is greater than k
    leftGreater = n

    # Finds number of elements greater than k
    while (l <= r):
        m = int(l + (r - l) / 2)

        # If mid element is greater than
        # k update leftGreater and r
        if (arr[m] > k):
            leftGreater = m
            r = m - 1

        # If mid element is less than
        # or equal to k update l
        else:
            l = m + 1

    # Return the count of elements
    # greater than k
    return (n - leftGreater)

# Driver code
if __name__ == '__main__':
    arr = [3, 3, 4, 7, 7, 7, 11, 13, 13]
    n = len(arr)
    k = 7

    print(countGreater(arr, n, k))
# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the count of elements
// from the array which are greater than k
static int countGreater(int[]arr, int n, int k)
{
    int l = 0;
    int r = n - 1;

    // Stores the index of the left most element
    // from the array which is greater than k
    int leftGreater = n;

    // Finds number of elements greater than k
    while (l <= r)
    {
        int m = l + (r - l) / 2;

        // If mid element is greater than
        // k update leftGreater and r
        if (arr[m] > k)
        {
            leftGreater = m;
            r = m - 1;
        }

        // If mid element is less than
        // or equal to k update l
        else
            l = m + 1;
    }

    // Return the count of elements greater than k
    return (n - leftGreater);
}

// Driver code
public static void Main()
{
    int[] arr = { 3, 3, 4, 7, 7, 7, 11, 13, 13 };
    int n = arr.Length;

    int k = 7;

    Console.WriteLine(countGreater(arr, n, k));
}
}

// This code is contributed by Code_Mech
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the count of elements
// from the array which are greater than k
function countGreater($arr, $n, $k)
{
    $l = 0;
    $r = $n - 1;

    // Stores the index of the left most element
    // from the array which is greater than k
    $leftGreater = $n;

    // Finds number of elements greater than k
    while ($l <= $r)
    {
        $m = $l + (int)(($r - $l) / 2);

        // If mid element is greater than
        // k update leftGreater and r
        if ($arr[$m] > $k)
        {
            $leftGreater = $m;
            $r = $m - 1;
        }

        // If mid element is less than
        // or equal to k update l
        else
            $l = $m + 1;
    }

    // Return the count of elements greater than k
    return ($n - $leftGreater);
}

// Driver code
$arr = array(3, 3, 4, 7, 7, 7, 11, 13, 13);
$n = sizeof($arr);
$k = 7;

echo countGreater($arr, $n, $k);

// This code is contributed
// by Akanksha Rai
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the count of elements
// from the array which are greater than k
function countGreater(arr, n, k)
{
    var l = 0;
    var r = n - 1;

    // Stores the index of the left most element
    // from the array which is greater than k
    var leftGreater = n;

    // Finds number of elements greater than k
    while (l <= r) {
        var m = l + parseInt((r - l) / 2);

        // If mid element is greater than
        // k update leftGreater and r
        if (arr[m] > k) {
            leftGreater = m;
            r = m - 1;
        }

        // If mid element is less than
        // or equal to k update l
        else
            l = m + 1;
    }

    // Return the count of elements greater than k
    return (n - leftGreater);
}

// Driver code
var arr = [3, 3, 4, 7, 7, 7, 11, 13, 13];
var n = arr.length;
var k = 7;
document.write( countGreater(arr, n, k));

</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(log(n))，其中 n 为数组中的元素个数。
**辅助空间:** O(1)