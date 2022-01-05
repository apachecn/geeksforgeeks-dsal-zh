# 计算斯特林数，斯特林数代表围绕 n 个不同的圆排列 r 个物体的方法数量

> 原文:[https://www . geeksforgeeks . org/calculate-stirling-numbers-代表排列 r 对象的方式数-围绕 n 个不同的圆/](https://www.geeksforgeeks.org/calculate-stirling-numbers-which-represents-the-number-of-ways-to-arrange-r-objects-around-n-different-circles/)

S(r，n)，表示我们可以将 r 个对象排列在长度为 n 的不可区分的圆周围的方式的数量，并且每个圆 n 周围必须至少有一个对象。

**示例:**

```
Input: r = 9, n = 2
Output: 109584

Input: r = 6, n = 3
Output: 225
```

特殊情况是:

*   S(r，0) = 0，微不足道。
*   S(r，1)代表[循环排列](http://mathworld.wolfram.com/CircularPermutation.html)，等于(r–1)！
*   S(r，n)其中 r = n，等于 1。
*   S(r，r -1) = rC2

斯特林数的一个重要恒等式，S(r，n)= S(r–1，n–1)+(r–1)* S(r–1，n)
**方法:**为简单起见，用 1，2，…，r 表示 r 个不同的对象。考虑对象“1”。在物体的任何排列中

1.  “1”是圆或中唯一的对象
2.  “1”是和别人混在一个圈子里的。

在案例 1 中，有 s(r–1，n–1)种方式来形成这种安排。在情况 2 中，首先，r — 1 对象 2，3，…，r 以 s(r — 1，n)的方式被放入 n 个圆中；那么“1”可以被放置在相应的 r-1 不同对象的“紧邻右侧”的 r-1 不同空间之一中。根据乘法原理，在情况 2 中有(r — 1)s(r — 1，n)种方式形成这种排列。现在恒等式来自 s(r，n)的定义和加法原理。
使用初始值 S(0，0) = 1，s(r，0) = 0 对于 r > 1 和 s(r，1) = (r — 1)！对于 r > 1，应用我们证明的恒等式，通过递归的方式计算，我们可以很容易地得到斯特林数。
在代码中，我们有三个函数用来生成 Stirling 数，它们是 nCr(n，r)，这是一个计算我们所谓的(n–choose–r)的函数，即我们可以从 n 个对象中取 r 个对象而不考虑排序重要性的方法的数量。阶乘(int n)用于计算一个数 n 的阶乘，这并不奇怪。函数 Stirling number(r，n)使用上面讨论的四种基本情况递归工作，然后使用我们证明的恒等式递归。

下面是上述方法的实现:

## C++

```
// C++ program to implement above approach
#include <iostream>
using namespace std;

// Calculating factorial of an integer n.
long long factorial(int n)
{
    // Our base cases of factorial 0! = 1! = 1
    if (n == 0)
        return 1;

    // n can't be less than 0.
    if (n < 0)
        return -1;
    long long res = 1;
    for (int i = 2; i < n + 1; ++i)
        res *= i;
    return res;
}

// Function to compute the number of combination
// of r objects out of n objects.
int nCr(int n, int r)
{
    // r cant be more than n so we'd like the
    // program to crash if the user entered
    // wrong input.
    if (r > n)
        return -1;

    if (n == r)
        return 1;

    if (r == 0)
        return 1;

    // nCr(n, r) = nCr(n - 1, r - 1) + nCr(n - 1, r)
    return nCr(n - 1, r - 1) + nCr(n - 1, r);
}

// Function to calculate the Stirling numbers.
// The base cases which were discussed above are handled
// to stop the recursive calls.
long long stirlingNumber(int r, int n)
{

    // n can't be more than
    // r, s(r, 0) = 0.
    if (n > r)
        return -1;

    if (n == 0)
        return 0;

    if (r == n)
        return 1;

    if (n == 1)
        return factorial(r - 1);

    if (r - n == 1)
        return nCr(r, 2);
    else
        return stirlingNumber(r - 1, n - 1)
               + (r - 1) * stirlingNumber(r - 1, n);
}

// Driver program
int main()
{
    // Calculating the stirling number s(9, 2)
    int r = 9, n = 2;

    long long val = stirlingNumber(r, n);
    if (val == -1)
        cout << " No stirling number";
    else
        cout << "The Stirling Number s(" << r
             << ", " << n << ") is : "  << val;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// above approach
import java.io.*;

class GFG
{

// Calculating factorial of
// an integer n.
static long factorial(int n)
{
    // Our base cases of factorial
    // 0! = 1! = 1
    if (n == 0)
        return 1;

    // n can't be less than 0.
    if (n < 0)
        return -1;
    long res = 1;
    for (int i = 2; i < n + 1; ++i)
        res *= i;
    return res;
}

// Function to compute the number
// of combination of r objects
// out of n objects.
static int nCr(int n, int r)
{
    // r cant be more than n so
    // we'd like the program to
    // crash if the user entered
    // wrong input.
    if (r > n)
        return -1;

    if (n == r)
        return 1;

    if (r == 0)
        return 1;

    return nCr(n - 1, r - 1) +
           nCr(n - 1, r);
}

// Function to calculate the Stirling
// numbers. The base cases which were
// discussed above are handled to stop
// the recursive calls.
static long stirlingNumber(int r, int n)
{

    // n can't be more than
    // r, s(r, 0) = 0.
    if (n > r)
        return -1;

    if (n == 0)
        return 0;

    if (r == n)
        return 1;

    if (n == 1)
        return factorial(r - 1);

    if (r - n == 1)
        return nCr(r, 2);
    else
        return stirlingNumber(r - 1, n - 1) +
                                    (r - 1) *
               stirlingNumber(r - 1, n);
}

// Driver Code
public static void main (String[] args)
{
    // Calculating the stirling number s(9, 2)
    int r = 9, n = 2;

    long val = stirlingNumber(r, n);
    if (val == -1)
        System.out.println(" No stirling number");
    else
        System.out.println( "The Stirling Number s(" +
                      r + ", " + n + ") is : " + val);
}
}

// This Code is Contributed by anuj_67
```

## 蟒蛇 3

```
# Python 3 program to implement above approach

# Function to compute the number of combination
# of r objects out of n objects.
# nCr(n, n) = 1, nCr(n, 0) = 1, and these are
# the base cases.

def nCr(n, r):
    if(n == r):
        return 1
    if(r == 0):
        return 1
    # nCr(n, r) = nCr(n - 1, r - 1) + nCr(n - 1, r)
    return nCr(n - 1, r - 1) + nCr(n - 1, r)

# This function is used to calculate the
# factorial of a number n.
def factorial(n):
    res = 1

    # 1 ! = 0 ! = 1
    if(n <= 1):
        return res
    for i in range(1, n + 1):
        res *= i
    return res

# Main function to calculate the Stirling numbers.
# the base cases which were discussed above are
# handled to stop the recursive call, n can't be
# more than r, s(r, 0) = 0.
# s(r, r) = 1\. s(r, 1) = (r - 1)!.
# s(r, r - 1) = nCr(r, 2)
# else as we proved, s(r, n) = s(r - 1, n - 1)
# + (r - 1) * s(r - 1, n)

def stirlingNumber(r, n):
    if(r == n):
        return 1
    if(n == 0):
        return 0
    if(n == r -1):
        return nCr(r, 2)
    if(r - n == 1):
        return factorial(r - 1)
    return (stirlingNumber(r - 1, n - 1)
        + (r - 1) * stirlingNumber(r - 1, n))

r, n = 9, 2

print(stirlingNumber(r, n))
```

## C#

```
// C# program to implement
// above approach
using System;

class GFG
{

// Calculating factorial of
// an integer n.
static long factorial(int n)
{
    // Our base cases of factorial
    // 0! = 1! = 1
    if (n == 0)
        return 1;

    // n can't be less than 0.
    if (n < 0)
        return -1;
    long res = 1;
    for (int i = 2; i < n + 1; ++i)
        res *= i;
    return res;
}

// Function to compute the number
// of combination of r objects
// out of n objects.
static int nCr(int n, int r)
{
    // r cant be more than n so
    // we'd like the program to
    // crash if the user entered
    // wrong input.
    if (r > n)
        return -1;

    if (n == r)
        return 1;

    if (r == 0)
        return 1;

    return nCr(n - 1, r - 1) +
        nCr(n - 1, r);
}

// Function to calculate the Stirling
// numbers. The base cases which were
// discussed above are handled to stop
// the recursive calls.
static long stirlingNumber(int r, int n)
{

    // n can't be more than
    // r, s(r, 0) = 0.
    if (n > r)
        return -1;

    if (n == 0)
        return 0;

    if (r == n)
        return 1;

    if (n == 1)
        return factorial(r - 1);

    if (r - n == 1)
        return nCr(r, 2);
    else
        return stirlingNumber(r - 1, n - 1) +
                                    (r - 1) *
            stirlingNumber(r - 1, n);
}

// Driver Code
public static void Main ()
{
    // Calculating the stirling
    // number s(9, 2)
    int r = 9, n = 2;

    long val = stirlingNumber(r, n);
    if (val == -1)
        Console.WriteLine(" No stirling number");
    else
        Console.WriteLine( "The Stirling Number s(" +
                     r + ", " + n + ") is : " + val);
}
}

// This code is contributed by inder_verma..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to implement above approach

// Calculating factorial of an integer n.
function factorial($n)
{
    // Our base cases of factorial 0! = 1! = 1
    if ($n == 0)
        return 1;

    // n can't be less than 0.
    if ($n < 0)
        return -1;

    $res = 1;
    for ($i = 2; $i < $n + 1; ++$i)
        $res *= $i;
    return $res;
}

// Function to compute the number of combination
// of r objects out of n objects.
function nCr($n, $r)
{
    // r cant be more than n so we'd like the
    // program to crash if the user entered
    // wrong input.
    if ($r > $n)
        return -1;

    if ($n == $r)
        return 1;

    if ($r == 0)
        return 1;

    // nCr($n, $r) = nCr($n - 1, $r - 1) + nCr($n - 1, $r)
    return nCr($n - 1, $r - 1) + nCr($n - 1, $r);
}

// Function to calculate the Stirling numbers.
// The base cases which were discussed above are handled
// to stop the recursive calls.
function stirlingNumber($r, $n)
{

    // n can't be more than
    // r, s(r, 0) = 0.
    if ($n > $r)
        return -1;

    if ($n == 0)
        return 0;

    if ($r == $n)
        return 1;

    if ($n == 1)
        return factorial($r - 1);

    if ($r - $n == 1)
        return nCr($r, 2);
    else
        return stirlingNumber($r - 1, $n - 1)
               + ($r - 1) * stirlingNumber($r - 1, $n);
}

     // Calculating the stirling number s(9, 2)
    $r = 9;
    $n = 2;

    $val = stirlingNumber($r, $n);
    if ($val == -1)
        echo " No stirling number";
    else
        echo  "The Stirling Number s(", $r
             ,", " , $n , ") is : " , $val;

// This code is contributed by ANKITRAI1
?>
```

## java 描述语言

```
<script>
// js program to implement above approach

// Calculating factorial of an integer n.
function factorial( n)
{
    // Our base cases of factorial 0! = 1! = 1
    if (n == 0)
        return 1;

    // n can't be less than 0.
    if (n < 0)
        return -1;
    let res = 1;
    for (let i = 2; i < n + 1; ++i)
        res *= i;
    return res;
}

// Function to compute the number of combination
// of r objects out of n objects.
function nCr(n, r)
{
    // r cant be more than n so we'd like the
    // program to crash if the user entered
    // wrong input.
    if (r > n)
        return -1;

    if (n == r)
        return 1;

    if (r == 0)
        return 1;

    // nCr(n, r) = nCr(n - 1, r - 1) + nCr(n - 1, r)
    return nCr(n - 1, r - 1) + nCr(n - 1, r);
}

// Function to calculate the Stirling numbers.
// The base cases which were discussed above are handled
// to stop the recursive calls.
function stirlingNumber( r, n)
{

    // n can't be more than
    // r, s(r, 0) = 0.
    if (n > r)
        return -1;

    if (n == 0)
        return 0;

    if (r == n)
        return 1;

    if (n == 1)
        return factorial(r - 1);

    if (r - n == 1)
        return nCr(r, 2);
    else
        return stirlingNumber(r - 1, n - 1)
               + (r - 1) * stirlingNumber(r - 1, n);
}

// Driver program
// Calculating the stirling number s(9, 2)
    let r = 9, n = 2;

    let val = stirlingNumber(r, n);
    if (val == -1)
        document.write( " No stirling number");
    else
        document.write( "The Stirling Number s(", r
             , ", " , n , ") is : "  , val);

</script>
```

**Output:** 

```
The Stirling Number s(9, 2) is : 109584
```

**注:**以上解决方案可通过[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)进行优化。请参考，例如[贝尔数(分割集合的方法数)](https://www.geeksforgeeks.org/bell-numbers-number-of-ways-to-partition-a-set/)。
请参考第一类斯特林数，了解更多斯特林数。