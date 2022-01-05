# 求两个数移位表的最小差

> 原文:[https://www . geeksforgeeks . org/find-两个数移位表之间的差异/](https://www.geeksforgeeks.org/find-the-difference-between-shifted-tables-of-two-numbers/)

给定两个数字“a”和“b”。在给定移位“x”和“y”的情况下，找出移位无限表“a”和“b”中任何项之间的最小差异，其中 x，y >= 0。
让我们考虑 a = 6，b = 16。这些数字的无限表格是。
a 表:6、12、18、24、30、36、42、 **48。** …。
b 表:16，32， **48** ，64，80，96，112，128…..
让给定的班次为 x = 5 和 y = 2
a 的班次表:11、 **17** **、** 23、29、 **35** 、41、47……
b 的班次表: **18** 、 **34** 、50、66 所以输出应该是 1。
**强烈建议大家尽量减少浏览器，先自己试试这个。**
**算法:**

1.  计算数字“a”和“b”的最大公约数。让两个数字的 GCD 为‘g’。
2.  计算模“g”下移位“x”和“y”的绝对差值“diff”，即 diff = ABS(a–b)% g
3.  所需的移位差值最小为“diff”和“g–diff”。

下面是上述算法的实现。

## C++

```
// C++ program to find the minimum difference
// between any two terms of two tables
#include <bits/stdc++.h>
using namespace std;

// Utility function to find GCD of a and b
int gcd(int a, int b)
{
    while (b != 0)
    {
        int t = b;
        b = a % b;
        a = t;
    }
    return a;
}

// Returns minimum difference between
// any two terms of shifted tables of 'a'
// and 'b'. 'x' is shift in table of 'a'
// and 'y' is shift in table of 'b'.
int findMinDiff(int a, int b, int x, int y)
{
    // Calculate gcd of a nd b
    int g  = gcd(a,b);

    // Calculate difference between x and y
    int diff = abs(x-y) % g;

    return min(diff, g - diff);
}

// Driver Code
int main()
{
    int a = 20, b = 52, x = 5, y = 7;

    cout << findMinDiff(a, b, x, y) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the
// minimum difference between
// any two terms of two tables
import java.io.*;

class GFG
{

// Utility function to
// find GCD of a and b
static int gcd(int a, int b)
{
    while (b != 0)
    {
        int t = b;
        b = a % b;
        a = t;
    }
    return a;
}

// Returns minimum difference
// between any two terms of
// shifted tables of 'a' and
// 'b'. 'x' is shift in table
// of 'a' and 'y' is shift in
// table of 'b'.
static int findMinDiff(int a, int b,
                       int x, int y)
{
    // Calculate gcd
    // of a nd b
    int g = gcd(a,b);

    // Calculate difference
    // between x and y
    int diff = Math.abs(x - y) % g;

    return Math.min(diff, g - diff);
}

// Driver Code
public static void main (String[] args)
{
    int a = 20, b = 52, x = 5, y = 7;
    System.out.println( findMinDiff(a, b, x, y));
}
}

// This code is contributed by ajit
```

## 蟒蛇 3

```
# python3 program to find the minimum difference
# between any two terms of two tables
import math as mt

# Utility function to find GCD of a and b
def gcd(a,b):

    while (b != 0):
        t = b
        b = a % b
        a = t

    return a

# Returns minimum difference between
# any two terms of shifted tables of 'a'
# and 'b'. 'x' is shift in table of 'a'
# and 'y' is shift in table of 'b'.
def findMinDiff (a, b, x, y):
    # Calculate gcd of a nd b
    g  = gcd(a,b)

    # Calculate difference between x and y
    diff = abs(x-y) % g

    return min(diff, g - diff)

# Driver Code
a,b,x,y = 20,52,5,7

print(findMinDiff(a, b, x, y))
#This code is contributed by Mohit kumar 29
```

## C#

```
// C# program to find the minimum difference
// between any two terms of two tables
using System;
class GFG
{

// Utility function to find GCD of a and b
static int gcd(int a, int b)
{
    while (b != 0)
    {
        int t = b;
        b = a % b;
        a = t;
    }
    return a;
}

// Returns minimum difference between any
// two terms of shifted tables of 'a' and
// 'b'. 'x' is shift in table of 'a' and
// 'y' is shift in table of 'b'.
static int findMinDiff(int a, int b,
                       int x, int y)
{
    // Calculate gcd
    // of a nd b
    int g = gcd(a, b);

    // Calculate difference
    // between x and y
    int diff = Math.Abs(x - y) % g;

    return Math.Min(diff, g - diff);
}

// Driver Code
static void Main()
{
    int a = 20, b = 52, x = 5, y = 7;
    Console.WriteLine(findMinDiff(a, b, x, y));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the minimum
// difference between any two terms
// of two tables

// Utility function to
// find GCD of a and b
function gcd($a, $b)
{
    while ($b != 0)
    {
        $t = $b;
        $b = $a % $b;
        $a = $t;
    }
    return $a;
}

// Returns minimum difference
// between any two terms of
// shifted tables of 'a' and
// 'b'. 'x' is shift in table
// of 'a' and 'y' is shift in
// table of 'b'.
function findMinDiff($a, $b, $x, $y)
{
    // Calculate gcd of a nd b
    $g = gcd($a, $b);

    // Calculate difference
    // between x and y
    $diff = abs($x - $y) % $g;

    return min($diff, $g - $diff);
}

// Driver Code
$a = 20; $b = 52; $x = 5; $y = 7;

echo findMinDiff($a, $b, $x, $y), "\n";

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>

// Javascript program to find the
// minimum difference between
// any two terms of two tables

// Utility function to
// find GCD of a and b
function gcd(a, b)
{
    while (b != 0)
    {
        let t = b;
        b = a % b;
        a = t;
    }
    return a;
}

// Returns minimum difference
// between any two terms of
// shifted tables of 'a' and
// 'b'. 'x' is shift in table
// of 'a' and 'y' is shift in
// table of 'b'.
function findMinDiff(a, b,
                       x, y)
{
    // Calculate gcd
    // of a and b
    let g = gcd(a,b);

    // Calculate difference
    // between x and y
    let diff = Math.abs(x - y) % g;

    return Math.min(diff, g - diff);
}

// Driver Code

    let a = 20, b = 52, x = 5, y = 7;
    document.write( findMinDiff(a, b, x, y));

</script>
```

**输出:**

```
 2
```

**复杂度:** O(log n)，计算 GCD。
**这是怎么工作的？**
换挡后表变成(假设 y > x 和 diff = y-x)
a+x，2a+x，3a+x，..ab+x，…和 b+y，2b+y，3b+y，…，ab+y，…
一般来说，差为，ABS[(am+x)–(bn+y)]，其中 m > = 1，n > = 1
最小差的上限为“ABS(x–y)”。我们总是可以通过放入 m = b 和 n = a 来得到这个差值。
如何将绝对差值降低到“ABS(x–y)”以下？
让我们把“ABS【(am+x)–(bn+y)】”改写为 ABS【(x–y)–(bn–am)】
让‘a’和‘b’的 GCD 为‘g’。让我们考虑一下“g”的表格。该表包含所有术语，如 a、2a、3a、… b、2b、3b、…以及术语(bn–am)和(am–bn)。

本文由 **Vaibhav Agarwal** 供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息