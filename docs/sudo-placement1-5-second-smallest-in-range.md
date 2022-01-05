# Sudo 放置[1.5] |范围内第二小

> 原文:[https://www . geesforgeks . org/sudo-placement 1-5-范围内第二小/](https://www.geeksforgeeks.org/sudo-placement1-5-second-smallest-in-range/)

给定一个由 N 个整数和 Q 个查询组成的数组。每个查询都由 L 和 r 组成。任务是打印 L-R 范围内的第二小元素。如果不存在第二小元素，则打印-1。

**示例:**

> **输入:**
> a[] = {1，2，2，4}
> 查询= 2
> L = 1，R = 2
> L = 0，R = 1
> **输出:**
> -1
> 2

**方法:**使用以下算法处理每个查询并打印第二小查询。

*   将第一个和第二个最小值都初始化为 INT_MAX
*   遍历所有元素。
    1.  如果当前元素小于第一个元素，则更新第一个和第二个元素。
    2.  否则，如果当前元素小于第二个元素，则更新第二个元素

如果在遍历所有元素后，第二个元素仍然是 INT_MAX，那么 print -1 将打印第二个最小的元素。

下面是上述方法的实现:

## C++

```
// C++ program for
// SP - Second Smallest in Range
#include <bits/stdc++.h>
using namespace std;

// Function to find the second smallest element
// in range L-R of an array
int secondSmallest(int a[], int n, int l, int r)
{

    int first = INT_MAX;
    int second = INT_MAX;
    for (int i = l; i <= r; i++) {
        if (a[i] < first) {
            second = first;
            first = a[i];
        }
        else if (a[i] < second and a[i] != first) {
            second = a[i];
        }
    }

    if (second == INT_MAX)
        return -1;
    else
        return second;
}

// function to perform queries
void performQueries(int a[], int n)
{
    // 1-st query
    int l = 1;
    int r = 2;
    cout << secondSmallest(a, n, l, r) << endl;

    // 2nd query
    l = 0;
    r = 1;
    cout << secondSmallest(a, n, l, r);
}

// Driver Code
int main()
{
    int a[] = { 1, 2, 2, 4 };
    int n = sizeof(a) / sizeof(a[0]);
    performQueries(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
// SP - Second Smallest in Range
class GFG
{
// Function to find the
// second smallest element
// in range L-R of an array
static int secondSmallest(int a[], int n,
                          int l, int r)
{
int first = Integer.MAX_VALUE;
int second = Integer.MAX_VALUE;
for (int i = l; i <= r; i++)
{
    if (a[i] < first)
    {
        second = first;
        first = a[i];
    }
    else if (a[i] < second &&
             a[i] != first)
    {
        second = a[i];
    }
}

if (second == Integer.MAX_VALUE)
    return -1;
else
    return second;
}

// function to perform queries
static void performQueries(int a[], int n)
{
    // 1-st query
    int l = 1;
    int r = 2;
    System.out.println(secondSmallest(a, n, l, r));

    // 2nd query
    l = 0;
    r = 1;
    System.out.println(secondSmallest(a, n, l, r));
}

// Driver Code
public static void main(String[] args)
{
    int a[] = { 1, 2, 2, 4 };
    int n = a.length;
    performQueries(a, n);
}
}

// This code is contributed
// by ChitraNayal
```

## 计算机编程语言

```
# Python program for
# SP - Second Smallest in Range

# Function to find the
# second smallest element
# in range L-R of an array
import sys
def secondSmallest(a, n, l, r):

    first = sys.maxsize
    second = sys.maxsize
    for i in range(l, r + 1):

        if (a[i] < first):

            second = first
            first = a[i]

        elif (a[i] < second and
              a[i] != first):

            second = a[i]

    if (second == sys.maxsize):
        return -1
    else:
        return second

# function to perform queries
def performQueries(a, n):

    # 1-st query
    l = 1
    r = 2
    print(secondSmallest(a, n, l, r))

    # 2nd query
    l = 0
    r = 1
    print(secondSmallest(a, n, l, r))

# Driver Code
a = [1, 2, 2, 4 ]
n = len(a)
performQueries(a, n);

# This code is contributed
# by Shivi_Aggarwal

```

## C#

```
// C# program for
// SP - Second Smallest in Range
using System;

class GFG
{
// Function to find the
// second smallest element
// in range L-R of an array
static int secondSmallest(int[] a, int n,
                        int l, int r)
{

int first = int.MaxValue;
int second = int.MaxValue;
for (int i = l; i <= r; i++)
{
    if (a[i] < first)
    {
        second = first;
        first = a[i];
    }
    else if (a[i] < second &&
            a[i] != first)
    {
        second = a[i];
    }
}

if (second == int.MaxValue)
    return -1;
else
    return second;
}

// function to perform queries
static void performQueries(int[] a, int n)
{
    // 1-st query
    int l = 1;
    int r = 2;
    Console.WriteLine(secondSmallest(a, n, l, r));

    // 2nd query
    l = 0;
    r = 1;
    Console.WriteLine(secondSmallest(a, n, l, r));
}

// Driver Code
public static void Main()
{
    int[] a = { 1, 2, 2, 4 };
    int n = a.Length;
    performQueries(a, n);
}
}

// This code is contributed
// by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for
// SP - Second Smallest in Range

// Function to find the
// second smallest element
// in range L-R of an array
function secondSmallest(&$a, $n, $l, $r)
{
    $first = PHP_INT_MAX;
    $second = PHP_INT_MAX;
    for ($i = $l; $i <= $r; $i++)
    {
        if ($a[$i] < $first)
        {
            $second = $first;
            $first = $a[$i];
        }
        else if ($a[$i] < $second and
                 $a[$i] != $first)
        {
            $second = $a[$i];
        }
    }

    if ($second == PHP_INT_MAX)
        return -1;
    else
        return $second;
}

// function to perform queries
function performQueries(&$a, $n)
{
    // 1-st query
    $l = 1;
    $r = 2;
    echo secondSmallest($a, $n,
                        $l, $r)."\n";

    // 2nd query
    $l = 0;
    $r = 1;
    echo secondSmallest($a, $n,
                        $l, $r)."\n";
}

// Driver Code
$a = array(1, 2, 2, 4);
$n = sizeof($a);
performQueries($a, $n);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>
// Javascript program for
// SP - Second Smallest in Range

// Function to find the
// second smallest element
// in range L-R of an array   
function secondSmallest(a,n,l,r)
{
let first = Number.MAX_VALUE;
let second = Number.MAX_VALUE;
for (let i = l; i <= r; i++)
{
    if (a[i] < first)
    {
        second = first;
        first = a[i];
    }
    else if (a[i] < second &&
             a[i] != first)
    {
        second = a[i];
    }
}

if (second == Number.MAX_VALUE)
    return -1;
else
    return second;
}

// function to perform queries
function performQueries(a,n)
{
    // 1-st query
    let l = 1;
    let r = 2;
    document.write(secondSmallest(a, n, l, r)+"<br>");

    // 2nd query
    l = 0;
    r = 1;
    document.write(secondSmallest(a, n, l, r)+"<br>");
}

// Driver Code
let a=[1, 2, 2, 4];
let n = a.length;
performQueries(a, n);

// This code is contributed by rag2127
</script>
```

**输出:**

```
-1
2
```

**时间复杂度:** O(M)，其中 M = R-L 是[L，R]
**范围内的元素个数注:**由于问题的约束非常少，所以蛮力解会通过。使用[段树](https://www.geeksforgeeks.org/segment-tree-set-1-range-minimum-query/)可以进一步优化解决方案。