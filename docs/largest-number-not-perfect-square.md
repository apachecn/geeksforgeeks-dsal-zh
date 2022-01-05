# 不是完美正方形的最大数字

> 原文:[https://www . geesforgeks . org/最大数字-非完美平方/](https://www.geeksforgeeks.org/largest-number-not-perfect-square/)

给定 n 个整数，求最大的数不是一个完美的平方。如果没有完美平方的数字，打印-1。
**例:**

```
Input : arr[] = {16, 20, 25, 2, 3, 10| 
Output : 20 
Explanation: 20 is the largest number 
that is not a perfect square 

Input : arr[] = {36, 64, 10, 16, 29, 25| 
Output : 29 
```

一个**正常的解决方法**是对元素进行排序，对 n 个数字进行排序，然后使用 sqrt()函数从后面开始检查一个非完美的平方数。从最后开始的第一个不是完美平方数的数就是我们的答案。排序的复杂度是 **O(n log n)** ，sqrt()函数的复杂度是 log n，所以最坏的情况下复杂度是 **O(n log n log n)。**
**高效解**是使用 O(n)中的遍历对所有元素进行迭代，每次与最大元素进行比较，存储所有非完美平方的最大值。以最大值存储的数字将是我们的答案。
以下是上述方法的说明:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// CPP program to find the largest non perfect
// square number among n numbers
#include <bits/stdc++.h>
using namespace std;
bool check(int n)
{
    // takes the sqrt of the number
    int d = sqrt(n);

    // checks if it is a perfect square number
    if (d * d == n)
        return true;

    return false;
}

// function to find the largest non perfect square number
int largestNonPerfectSquareNumber(int a[], int n)
{
    // stores the maximum of all non perfect square numbers
    int maxi = -1;

    // traverse for all elements in the array
    for (int i = 0; i < n; i++) {

        // store the maximum if not a perfect square
        if (!check(a[i]))
            maxi = max(a[i], maxi);
    }
    return maxi;
}

// driver code to check the above functions
int main()
{
    int a[] = { 16, 20, 25, 2, 3, 10 };

    int n = sizeof(a) / sizeof(a[0]);
    // function call
    cout << largestNonPerfectSquareNumber(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the
// largest non perfect
// square number among n numbers

import java.io.*;

class GfG{

static Boolean check(int n)
{
    // takes the sqrt of the number
    int d = (int)Math.sqrt(n);

    // checks if it is a perfect square number
    if (d * d == n)
        return true;

    return false;
}

// function to find the largest
// non perfect square number
static int largestNonPerfectSquareNumber(int a[], int n)
{
    // stores the maximum of all
    // non perfect square numbers
    int maxi = -1;

    // traverse for all elements in the array
    for (int i = 0; i < n; i++) {

        // store the maximum if
        // not a perfect square
        if (!check(a[i]))
            maxi = Math.max(a[i], maxi);
    }
    return maxi;
}

    public static void main (String[] args) {

        int a[] = { 16, 20, 25, 2, 3, 10 };
        int n = a.length;

        // function call
        System.out.println(largestNonPerfectSquareNumber(a, n));
    }
}

// This code is contributed by Gitanjali.
```

## 蟒蛇 3

```
# python program to find
# the largest non perfect
# square number among n numbers

import math
def check( n):

    # takes the sqrt of the number
    d = int(math.sqrt(n))

    # checks if it is a
    # perfect square number
    if (d * d == n):
        return True

    return False

# function to find the largest
# non perfect square number
def largestNonPerfectSquareNumber(a, n):

    # stores the maximum of all
    # non perfect square numbers
    maxi = -1

    # traverse for all elements
    # in the array
    for i in range(0,n):

        # store the maximum if
        # not a perfect square
        if (check(a[i])==False):
            maxi = max(a[i], maxi)

    return maxi

# driver code
a = [ 16, 20, 25, 2, 3, 10 ]
n= len(a)

# function call
print (largestNonPerfectSquareNumber(a, n))

# This code is contributed by Gitanjali.
```

## C#

```
// C# program to find the largest non perfect
// square number among n numbers
using System;

class GfG {

    static bool check(int n)
    {

        // takes the sqrt of the number
        int d = (int)Math.Sqrt(n);

        // checks if it is a perfect
        // square number
        if (d * d == n)
            return true;

        return false;
    }

    // function to find the largest
    // non perfect square number
    static int largestNonPerfectSquareNumber(
                               int []a, int n)
    {

        // stores the maximum of all
        // non perfect square numbers
        int maxi = -1;

        // traverse for all elements in
        // the array
        for (int i = 0; i < n; i++) {

            // store the maximum if
            // not a perfect square
            if (!check(a[i]))
                maxi = Math.Max(a[i], maxi);
        }

        return maxi;
    }

    // driver code to check the above functions
    public static void Main ()
    {

        int []a = { 16, 20, 25, 2, 3, 10 };
        int n = a.Length;

        // function call
        Console.WriteLine(
           largestNonPerfectSquareNumber(a, n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// the largest non perfect
// square number among n
// numbers

function check($n)
{

    // takes the sqrt
    // of the number
    $d = sqrt($n);

    // checks if it is a
    // perfect square number
    if ($d * $d == $n)
        return true;

    return false;
}

// function to find the largest
// non perfect square number
function largestNonPerfectSquareNumber($a, $n)
{

    // stores the maximum of
    // all non perfect square
    // numbers
    $maxi = -1;

    // traverse for all
    // elements in the array
    for ($i = 0; $i < $n; $i++)
    {

        // store the maximum if
        // not a perfect square
        if (!check($a[$i]))
            $maxi = max($a[$i], $maxi);
    }
    return $maxi;
}

    // Driver Code
    $a = array(16, 20, 25, 2, 3, 10);
    $n = count($a);

    // function call
    echo largestNonPerfectSquareNumber($a, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// JavaScript program to find the
// largest non perfect
// square number among n numbers

function check(n)
{
    // takes the sqrt of the number
    let d = Math.sqrt(n);

    // checks if it is a perfect square number
    if (d * d == n)
        return true;

    return false;
}

// function to find the largest
// non perfect square number
function largestNonPerfectSquareNumber(a, n)
{
    // stores the maximum of all
    // non perfect square numbers
    let maxi = -1;

    // traverse for all elements in the array
    for (let i = 0; i < n; i++) {

        // store the maximum if
        // not a perfect square
        if (!check(a[i]))
            maxi = Math.max(a[i], maxi);
    }
    return maxi;
}

// Driver Code

        let a = [ 16, 20, 25, 2, 3, 10 ];
        let n = a.length;

        // function call
       document.write(largestNonPerfectSquareNumber(a, n));

</script>
```

**输出:**

```
20
```

时间复杂度可视为 O(n)，因为对于固定大小(32 位或 64 位)的整数，sqrt()函数可在 O(1)时间内实现【详情请参考[Wiki](https://en.wikipedia.org/wiki/Methods_of_computing_square_roots#Taylor_series)】

？list = plqm 7 alhxfysqdk 2 mdfbwedjd 2 svv JH 9p