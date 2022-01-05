# 程序求一系列 a^1/1 的和！+ a^2/2！+ a^3/3！+ a^4/4！+…….+ a^n/n！

> 原文:[https://www . geesforgeks . org/program-find-sum-series-a11-a22-a33-a44-ann/](https://www.geeksforgeeks.org/program-find-sum-series-a11-a22-a33-a44-ann/)

给定两个值“a”和“n”，求 a^1/1 级数的和！+ a^2/2！+ a^3/3！+ a^4/4！+…….+ a^n/n！。
**例:**

```
Input : a = 2 and n = 5
Output : 6.26667
We get result by adding 
2^1/1! + 2^2/2! + 2^3/3! + 2^4/4! +
2^5/5! 
= 2/1 + 4/2 +  8/6 + 16/24 + 32/120
=  6.26667
```

一个简单的解决方案是逐个计算单个术语的值，并不断将它们添加到结果中。
我们只用一个循环就能找到解。这个想法是用以前的值乘以(a/i ),其中 I 是我们需要找到的项数。

```
for finding 1st term:-  a/1
for finding 2nd term:-  (1st term) * a/2
for finding 3rd term:-  (2nd term) * a/3
.
.
.
for finding nth term:-  ((n-1)th term) * a/n
```

插图:

```
Input: a = 2 and n = 5
By multiplying Each term by 2/i
  1st term :-              2/1 = 2
  2nd term :- (1st term) * 2/2 =(2)*1 = 2
  3rd term :- (2nd term) * 2/3 = 4/3
  4th term :- (3rd term) * 2/4 = 2/3
  5th term :- (4th term) * 2/5 = 4/15
=> 2 + 2 + 4/3 + 2/3 + 4/15
Output: sum = 6.26667
```

**复杂度:O(n)**

## 卡片打印处理机（Card Print Processor 的缩写）

```
/*CPP program to print the sum of series */
#include<bits/stdc++.h>
using namespace std;

/*function to calculate sum of given series*/
double sumOfSeries(double a,double num)
{
    double res = 0,prev=1;
    for (int i = 1; i <= num; i++)
    {
        /*multiply (a/i) to previous term*/
        prev *= (a/i);

        /*store result in res*/
        res = res + prev;
    }
    return(res);
}

/* Driver Function */
int main()
{
    double n = 5, a=2;
    cout << sumOfSeries(a,n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the
// sum of series
import java.io.*;

class GFG
{
    public static void main (String[] args)
    {
        double n = 5, a = 2;
        System.out.println(sumOfSeries(a, n));
    }

    // function to calculate sum of given series
    static double sumOfSeries(double a,double n)
    {
        double res = 0, prev = 1;
        for (int i = 1; i <= n; i++)
            {
                // multiply (a/i) to previous term
                prev *= (a / i);

                // store result in res
                res = res + prev;
            }
        return(res);
    }
}

// This code is Contributed by Azkia Anam.
```

## 蟒蛇 3

```
# Python program to print
# the sum of series.
# function to calculate
# sum of given series.

from __future__ import division

def sumOfSeries(a,num):
    res = 0
    prev=1
    for i in range(1, n+1):

        # multiply (a/i) to
        # previous term
        prev *= (a/i)

        # store result in res
        res = res + prev
    return res

# Driver code
n = 5
a = 2
print(round(sumOfSeries(a,n),4))

# This Code is Contributed
# by Azkia Anam.
```

## C#

```
// C# program to print the
// sum of series
using System;

class GFG
{
    public static void Main ()
    {
        double n = 5, a = 2;
        Console.WriteLine(sumOfSeries(a, n));
    }

    // Function to calculate sum of given series
    static float sumOfSeries(double a, double n)
    {
        double res = 0, prev = 1;
        for (int i = 1; i <= n; i++)
            {
                // multiply (a/i) to previous term
                prev *= (a / i);

                // store result in res
                res = res + prev;
            }
        return(float)(res);
    }
}

// This code is Contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print
// the sum of series

// Function to calculate
// sum of given series
function sumOfSeries($a, $num)
{
    $res = 0; $prev = 1;
    for ($i = 1; $i <= $num; $i++)
    {
        // multiply (a/i) to
        // previous term
        $prev *= ($a / $i);

        // store result in res
        $res = $res + $prev;
    }
    return ($res);
}

// Driver Code
$n = 5; $a = 2;
echo(sumOfSeries($a, $n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>
/* JavaScript program to print the sum of series */

/*function to calculate sum of given series*/
function sumOfSeries(a, num)
{
    let res = 0, prev = 1;
    for (let i = 1; i <= num; i++)
    {

        /*multiply (a/i) to previous term*/
        prev *= (a/i);

        /*store result in res*/
        res = res + prev;
    }
    return(res);
}

/* Driver Function */
    let n = 5, a=2;
    document.write(sumOfSeries(a,n));

// This code is contributed by Surbhi Tyagi.
</script>
```

**输出:**

```
6.26667
```

时间复杂度:0(n)

辅助空间:0(1)

本文由 **R_Raj** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。