# 可被 X 整除的最大 K 位数

> 原文:[https://www . geesforgeks . org/maximum-k-digital-number-除尽-x/](https://www.geeksforgeeks.org/largest-k-digit-number-divisible-x/)

给出了整数 X 和 K。任务是找到能被 x 整除的最高 K 位数
**示例:**

```
Input : X = 30, K = 3
Output : 990
990 is the largest three digit 
number divisible by 30.

Input : X = 7, K = 2
Output : 98
```

一个**简单的解决方案**是从最大的 K 位数(也就是 999…K 次)开始尝试所有的数字，返回第一个能被 x 整除的数字。
一个**高效的解决方案**是使用下面的公式。

```
ans = MAX - (MAX % X)
where MAX is the largest K digit 
number which is  999...K-times
```

这个公式适用于简单的学校方法划分。我们去掉余数得到最大的可除数。

## C++

```
// CPP code to find highest K-digit number divisible by X
#include <bits/stdc++.h>
using namespace std;

// Function to compute the result
int answer(int X, int K)
{
    // Computing MAX
    int MAX = pow(10, K) - 1;

    // returning ans
    return (MAX - (MAX % X));
}

// Driver
int main()
{
    // Number whose divisible is to be found
    int X = 30;

    // Max K-digit divisible is to be found
    int K = 3;

    cout << answer(X, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find highest
// K-digit number divisible by X

import java.io.*;
import java.lang.*;

class GFG {
    public static double answer(double X, double K)
    {
        double i = 10;
        // Computing MAX
        double MAX = Math.pow(i, K) - 1;

        // returning ans
        return (MAX - (MAX % X));
    }

    public static void main(String[] args)
    {

        // Number whose divisible is to be found
        double X = 30;

        // Max K-digit divisible is to be found
        double K = 3;

        System.out.println((int)answer(X, K));
    }
}

// Code contributed by Mohit Gupta_OMG <(0_o)>
```

## 蟒蛇 3

```
# Python code to find highest
# K-digit number divisible by X

def answer(X, K):

    # Computing MAX
    MAX = pow(10, K) - 1

    # returning ans
    return (MAX - (MAX % X))

X = 30;
K = 3;

print(answer(X, K));

# Code contributed by Mohit Gupta_OMG <(0_o)>
```

## C#

```
// C# code to find highest
// K-digit number divisible by X

using System;

class GFG {

    public static double answer(double X, double K)
    {

        double i = 10;

        // Computing MAX
        double MAX = Math.Pow(i, K) - 1;

        // returning ans
        return (MAX - (MAX % X));
    }

    public static void Main()
    {

        // Number whose divisible is to be found
        double X = 30;

        // Max K-digit divisible is to be found
        double K = 3;

        Console.WriteLine((int)answer(X, K));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to find highest K-digit
// number divisible by X

// Function to compute the result
function answer($X, $K)
{

    // Computing MAX
    $MAX = pow(10, $K) - 1;

    // returning ans
    return ($MAX - ($MAX % $X));
}

// Driver
    // Number whose divisible
    // is to be found
    $X = 30;

    // Max K-digit divisible
    // is to be found
    $K = 3;

    echo answer($X, $K);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
// Javascript code to find highest K-digit
// number divisible by X

// Function to compute the result
function answer(X, K)
{

    // Computing MAX
    let MAX = Math.pow(10, K) - 1;

    // returning ans
    return (MAX - (MAX % X));
}

// Driver
    // Number whose divisible
    // is to be found
    let X = 30;

    // Max K-digit divisible
    // is to be found
    let K = 3;

    document.write(answer(X, K));

// This code is contributed by gfgking
</script>
```

**输出:**

```
990
```

本文由 **Rohit Thapliyal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。