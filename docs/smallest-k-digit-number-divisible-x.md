# 可被 X 整除的最小 K 位数

> 原文:[https://www . geesforgeks . org/minist-k-digital-number-除尽-x/](https://www.geeksforgeeks.org/smallest-k-digit-number-divisible-x/)

给出了整数 X 和 K。任务是找到能被 x 整除的最小 K 位数。

**示例:**

```
Input : X = 83, K = 5
Output : 10043
10040 is the smallest 5 digit
number that is multiple of 83.

Input : X = 5, K = 2
Output : 10
```

一个**简单的解决方法**是从最小的 K 位数
(是 100……(K-1)次)开始尝试所有数字，返回第一个被 x 整除的数字。

一个有效的解决方案是:

```
Compute MIN : smallest K-digit number (1000...(K-1)times)
If, MIN % X is 0, ans = MIN
else, ans = (MIN + X) - ((MIN + X) % X))
This is because there will be a number in 
range [MIN...MIN+X] divisible by X.
```

## C++

```
// C++ code to find smallest K-digit number
// divisible by X
#include <bits/stdc++.h>
using namespace std;

// Function to compute the result
int answer(int X, int K)
{
    // Computing MIN
    int MIN = pow(10, K - 1);

    // MIN is the result
    if (MIN % X == 0)
        return MIN;

    // returning ans
    return ((MIN + X) - ((MIN + X) % X));
}

// Driver Code
int main()
{
    // Number whose divisible is to be found
    int X = 83;

    // Max K-digit divisible is to be found
    int K = 5;

    cout << answer(X, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find smallest K-digit
// number divisible by X

import java.io.*;
import java.lang.*;

class GFG {
    public static double answer(double X, double K)
    {
        double i = 10;
        // Computing MIN
        double MIN = Math.pow(i, K - 1);

        // returning ans
        if (MIN % X == 0)
            return (MIN);
        else
            return ((MIN + X) - ((MIN + X) % X));
    }

    public static void main(String[] args)
    {

        // Number whose divisible is to be found
        double X = 83;
        double K = 5;

        System.out.println((int)answer(X, K));
    }
}

// Code contributed by Mohit Gupta_OMG <(0_o)>
```

## 蟒蛇 3

```
# Python code to find smallest K-digit 
# number divisible by X

def answer(X, K):

    # Computing MAX
    MIN = pow(10, K-1)

    if(MIN % X == 0):
        return (MIN)

    else:
        return ((MIN + X) - ((MIN + X) % X))

X = 83;
K = 5;

print(answer(X, K));

# Code contributed by Mohit Gupta_OMG <(0_o)>
```

## C#

```
// C# code to find smallest K-digit
// number divisible by X
using System;

class GFG {

    // Function to compute the result
    public static double answer(double X, double K)
    {

        double i = 10;

        // Computing MIN
        double MIN = Math.Pow(i, K - 1);

        // returning ans
        if (MIN % X == 0)
            return MIN;
        else
            return ((MIN + X) - ((MIN + X) % X));
    }

    // Driver code
    public static void Main()
    {

        // Number whose divisible is to be found
        double X = 83;
        double K = 5;

        Console.WriteLine((int)answer(X, K));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to find smallest
// K-digit number divisible by X

// Function to compute
// the result
function answer($X, $K)
{
    // Computing MIN
    $MIN = pow(10, $K - 1);

    // MIN is the result
    if ($MIN % $X == 0)
        return $MIN;

    // returning ans
    return (($MIN + $X) -
           (($MIN + $X) % $X));
}

// Driver Code

// Number whose divisible
// is to be found
$X = 83;

// Max K-digit divisible
// is to be found
$K = 5;

echo answer($X, $K);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Javascript code to find smallest
// K-digit number divisible by X

// Function to compute
// the result
function answer(X, K)
{

    // Computing MIN
    let MIN = Math.pow(10, K - 1);

    // MIN is the result
    if (MIN % X == 0)
        return MIN;

    // returning ans
    return ((MIN + X) -
           ((MIN + X) % X));
}

// Driver Code

// Number whose divisible
// is to be found
let X = 83;

// Max K-digit divisible
// is to be found
let K = 5;

document.write(answer(X, K));

// This code is contributed by sravan kumar

</script>
```

**输出:**

```
10043
```

本文由 [**罗希特·塔普利亚尔**](https://www.hackerrank.com/rohit_thapliyal) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。