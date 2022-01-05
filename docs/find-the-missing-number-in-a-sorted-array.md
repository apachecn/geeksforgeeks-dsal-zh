# 在排序的数组中找到缺失的数字

> 原文:[https://www . geesforgeks . org/find-在排序数组中查找缺失的数字/](https://www.geeksforgeeks.org/find-the-missing-number-in-a-sorted-array/)

给定一个 n-1 个整数的列表，这些整数在 1 到 n 的范围内。列表中没有重复项。列表中缺少一个整数。写一个高效的代码来找到丢失的整数。
**例:**

```
Input : arr[] = [1, 2, 3, 4, 6, 7, 8]
Output : 5

Input : arr[] = [1, 2, 3, 4, 5, 6, 8, 9]
Output : 7
```

一个**简单的解决方案**是应用所讨论的方法[在一个未排序的数组](https://www.geeksforgeeks.org/find-the-missing-number/)中寻找丢失的元素。这个解的时间复杂度是 O(n)。
一个**高效的解决方案**是基于我们在二分搜索法看到的分治算法，这个解决方案背后的概念是，出现在缺失元素之前的元素会有 ar[I]–I = 1，出现在缺失元素之后的元素会有 ar[I]–I = 2。
该解决方案的时间复杂度为 O(对数 n)

## C++

```
// A binary search based program to find the
// only missing number in a sorted array of
// distinct elements within limited range.
#include <iostream>
using namespace std;

int search(int ar[], int size)
{
    int a = 0, b = size - 1;
    int mid;
    while ((b - a) > 1) {
        mid = (a + b) / 2;
        if ((ar[a] - a) != (ar[mid] - mid))
            b = mid;
        else if ((ar[b] - b) != (ar[mid] - mid))
            a = mid;
    }
    return (ar[a] + 1);
}

int main()
{
    int ar[] = { 1, 2, 3, 4, 5, 6, 8 };
    int size = sizeof(ar) / sizeof(ar[0]);
    cout << "Missing number:" << search(ar, size);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A binary search based program
// to find the only missing number
// in a sorted array of distinct
// elements within limited range.
import java.io.*;

class GFG
{
static int search(int ar[],
                  int size)
{
    int a = 0, b = size - 1;
    int mid = 0;
    while ((b - a) > 1)
    {
        mid = (a + b) / 2;
        if ((ar[a] - a) != (ar[mid] - mid))
            b = mid;
        else if ((ar[b] - b) != (ar[mid] - mid))
            a = mid;
    }
    return (ar[a] + 1);
}

// Driver Code
public static void main (String[] args)
{
    int ar[] = { 1, 2, 3, 4, 5, 6, 8 };
    int size = ar.length;
    System.out.println("Missing number: " +
                        search(ar, size));
}
}

// This code is contributed
// by inder_verma.
```

## 蟒蛇 3

```
# A binary search based program to find
# the only missing number in a sorted
# in a sorted array of distinct elements
# within limited range
def search(ar, size):
    a = 0
    b = size - 1
    mid = 0
    while b > a + 1:
        mid = (a + b) // 2
        if (ar[a] - a) != (ar[mid] - mid):
            b = mid
        elif (ar[b] - b) != (ar[mid] - mid):
            a = mid
    return ar[a] + 1

# Driver Code
a = [1, 2, 3, 4, 5, 6, 8]
n = len(a)

print("Missing number:", search(a, n))

# This code is contributed
# by Mohit Kumar
```

## C#

```
// A binary search based program
// to find the only missing number
// in a sorted array of distinct
// elements within limited range.
using System;

class GFG
{
static int search(int []ar,
                  int size)
{
    int a = 0, b = size - 1;
    int mid = 0;
    while ((b - a) > 1)
    {
        mid = (a + b) / 2;
        if ((ar[a] - a) != (ar[mid] - mid))
            b = mid;
        else if ((ar[b] - b) != (ar[mid] - mid))
            a = mid;
    }
    return (ar[a] + 1);
}

// Driver Code
static public void Main (String []args)
{
    int []ar = { 1, 2, 3, 4, 5, 6, 8 };
    int size = ar.Length;
    Console.WriteLine("Missing number: " +
                        search(ar, size));
}
}

// This code is contributed
// by Arnab Kundu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A binary search based program to find the
// only missing number in a sorted array of
// distinct elements within limited range.

function search($ar, $size)
{
    $a = 0;
    $b = $size - 1;
    $mid;
    while (($b - $a) > 1)
    {
        $mid = (int)(($a + $b) / 2);
        if (($ar[$a] - $a) != ($ar[$mid] -
                                   $mid))
            $b = $mid;
        else if (($ar[$b] - $b) != ($ar[$mid] -
                                        $mid))
            $a = $mid;
    }
    return ($ar[$a] + 1);
}

// Driver Code
$ar = array(1, 2, 3, 4, 5, 6, 8 );
$size = sizeof($ar);
echo "Missing number: ",
     search($ar, $size);

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>
// A binary search based program
// to find the only missing number
// in a sorted array of distinct
// elements within limited range.

function search(ar, size)
{
    let a = 0, b = size - 1;
    let mid = 0;
    while ((b - a) > 1)
    {
        mid = (a + b) / 2;
        if ((ar[a] - a) != (ar[mid] - mid))
            b = mid;
        else if ((ar[b] - b) != (ar[mid] - mid))
            a = mid;
    }
    return (ar[a] + 3);
}

// Driver Code

let ar = [1, 2, 3, 4, 5, 6, 8];
let size = ar.length;
document.write("Missing number: " +search(ar, size));

// This code is contributed by mohit kumar 29.
</script>
```

**输出:**

```
Missing number: 7
```