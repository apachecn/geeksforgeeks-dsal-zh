# 四分之一区间(iqn)

> 原文:[https://www.geeksforgeeks.org/interquartile-range-iqr/](https://www.geeksforgeeks.org/interquartile-range-iqr/)

一组有序数据值的**四分位数**是三个点，它们将数据精确地分成四个相等的部分，每个部分由四分之一数据组成。

1.  **Q1** 定义为数据集最小数和中位数之间的中间数。
2.  **Q2** 是数据的[中位数](https://www.geeksforgeeks.org/mean-median-unsorted-array/)。
3.  **Q3** 是数据集的中值和最高值之间的中间值。

```
The interquartile range IQR tells us the range 
where the bulk of the values lie. The interquartile 
range is calculated by subtracting the first quartile
from the third quartile. 
IQR = Q3 - Q1
```

**用途**T2**1。**与范围不同，IQR 告诉大多数数据位于何处，因此比范围更受青睐。
**2。** IQR 可以用来识别数据集中的[异常值](http://www.dictionary.com/browse/outlier)。
**3。**给出数据的中心趋势。
**举例:**

```
Input : 1, 19, 7, 6, 5, 9, 12, 27, 18, 2, 15
Output : 13
The data set after being sorted is 
1, 2, 5, 6, 7, 9, 12, 15, 18, 19, 27
As mentioned above Q2 is the median of the data. 
Hence Q2 = 9
Q1 is the median of lower half, taking Q2 as pivot.
So Q1 = 5
Q3 is the median of upper half talking Q2 as pivot. 
So Q3 = 18
Therefore IQR for given data=Q3-Q1=18-5=13 

Input : 1, 3, 4, 5, 5, 6, 7, 11
Output : 3
```

## C++

```
// CPP program to find IQR of a data set
#include <bits/stdc++.h>
using namespace std;

// Function to give index of the median
int median(int* a, int l, int r)
{
    int n = r - l + 1;
    n = (n + 1) / 2 - 1;
    return n + l;
}

// Function to calculate IQR
int IQR(int* a, int n)
{
    sort(a, a + n);

    // Index of median of entire data
    int mid_index = median(a, 0, n);

    // Median of first half
    int Q1 = a[median(a, 0, mid_index)];

    // Median of second half
    int Q3 = a[mid_index + median(a, mid_index + 1, n)];

    // IQR calculation
    return (Q3 - Q1);
}

// Driver Function
int main()
{
    int a[] = { 1, 19, 7, 6, 5, 9, 12, 27, 18, 2, 15 };
    int n = sizeof(a)/sizeof(a[0]);
    cout << IQR(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find
// IQR of a data set
import java.io.*;
import java .util.*;

class GFG
{

// Function to give
// index of the median
static int median(int a[],
                  int l, int r)
{
    int n = r - l + 1;
    n = (n + 1) / 2 - 1;
    return n + l;
}

// Function to
// calculate IQR
static int IQR(int [] a, int n)
{
    Arrays.sort(a);

    // Index of median
    // of entire data
    int mid_index = median(a, 0, n);

    // Median of first half
    int Q1 = a[median(a, 0,
                      mid_index)];

    // Median of second half
    int Q3 = a[mid_index + median(a,
               mid_index + 1, n)];

    // IQR calculation
    return (Q3 - Q1);
}

// Driver Code
public static void main (String[] args)
{
    int []a = {1, 19, 7, 6, 5, 9,
               12, 27, 18, 2, 15};
    int n = a.length;
    System.out.println(IQR(a, n));
}
}

// This code is contributed
// by anuj_67.
```

## 蟒蛇 3

```
# Python3 program to find IQR of
# a data set

# Function to give index of the median
def median(a, l, r):
    n = r - l + 1
    n = (n + 1) // 2 - 1
    return n + l

# Function to calculate IQR
def IQR(a, n):

    a.sort()

    # Index of median of entire data
    mid_index = median(a, 0, n)

    # Median of first half
    Q1 = a[median(a, 0, mid_index)]

    # Median of second half
    Q3 = a[mid_index + median(a, mid_index + 1, n)]

    # IQR calculation
    return (Q3 - Q1)

# Driver Function
if __name__=='__main__':
    a = [1, 19, 7, 6, 5, 9, 12, 27, 18, 2, 15]
    n = len(a)
    print(IQR(a, n))

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# program to find
// IQR of a data set
using System;

class GFG
{

// Function to give
// index of the median
static int median(int []a,
                int l, int r)
{
    int n = r - l + 1;
    n = (n + 1) / 2 - 1;
    return n + l;
}

// Function to
// calculate IQR
static int IQR(int [] a, int n)
{
    Array.Sort(a);

    // Index of median
    // of entire data
    int mid_index = median(a, 0, n);

    // Median of first half
    int Q1 = a[median(a, 0,
                    mid_index)];

    // Median of second half
    int Q3 = a[mid_index + median(a,
            mid_index + 1, n)];

    // IQR calculation
    return (Q3 - Q1);
}

// Driver Code
public static void Main ()
{
    int []a = {1, 19, 7, 6, 5, 9,
            12, 27, 18, 2, 15};
    int n = a.Length;
    Console.WriteLine(IQR(a, n));
}
}

// This code is contributed
// by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find IQR of a data set

// Function to give index of the median
function median($a, $l, $r)
{
    $n = $r - $l + 1;
    $n = (int)(($n + 1) / 2) - 1;
    return $n + $l;
}

// Function to calculate IQR
function IQR($a, $n)
{
    sort($a);

    // Index of median of entire data
    $mid_index = median($a, 0, $n);

    // Median of first half
    $Q1 = $a[median($a, 0, $mid_index)];

    // Median of second half
    $Q3 = $a[$mid_index + median($a, $mid_index + 1, $n)];

    // IQR calculation
    return ($Q3 - $Q1);
}

// Driver Function
$a = array( 1, 19, 7, 6, 5, 9,
            12, 27, 18, 2, 15 );
$n = count($a);
echo IQR($a, $n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// javascript program to find
// IQR of a data set

// Function to give
// index of the median
function median(a, l , r)
{
    var n = r - l + 1;
    n = parseInt((n + 1) / 2) - 1;
    return parseInt(n + l);
}

// Function to
// calculate IQR
function IQR(a , n)
{
    a.sort((a,b)=>a-b);

    // Index of median
    // of entire data
    var mid_index = median(a, 0, n);

    // Median of first half
    var Q1 = a[median(a, 0,
                      mid_index)];

    // Median of second half
    var Q3 = a[mid_index + median(a,
               mid_index + 1, n)];

    // IQR calculation
    return (Q3 - Q1);
}

// Driver Code
var a = [1, 19, 7, 6, 5, 9,
         12, 27, 18, 2, 15];
var n = a.length;
document.write(IQR(a, n));

// This code contributed by Princi Singh
</script>
```

**输出:**

```
13
```

**参考**
[https://en.wikipedia.org/wiki/Interquartile_range](https://en.wikipedia.org/wiki/Interquartile_range)
本文由**vinet Joshi**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。