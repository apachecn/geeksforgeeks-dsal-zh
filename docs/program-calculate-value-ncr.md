# 计算 nCr 值的程序

> 原文:[https://www.geeksforgeeks.org/program-calculate-value-ncr/](https://www.geeksforgeeks.org/program-calculate-value-ncr/)

以下是[二项式系数](http://en.wikipedia.org/wiki/Binomial_coefficient)的一般定义。

1.  A [二项式系数](http://en.wikipedia.org/wiki/Binomial_coefficient) C(n，k)可以定义为(1 + X)^n.)展开式中的 X^k 系数
2.  二项式系数 C(n，k)也给出了从 n 个对象中选择 k 个对象的方法，不考虑顺序；更正式地说，n 元素集的 k 元素子集(或 k 组合)的数量。

给定两个数字 n 和 r，求<sup>n</sup>C<sub>r</sub>T4**的值示例:**

```
Input :  n = 5, r = 2
Output : 10
The value of 5C2 is 10

Input : n = 3, r = 1
Output : 3
```

这个想法只是基于下面的公式。

> <sup>n</sup> C <sub>r</sub> = (n！)/ (r！* (n-r)！)

## C

```
#include <stdio.h>

int factorial(int n) {
    int factorial = 1;
    for (int i = 2; i <= n; i++)
        factorial = factorial * i;
    return factorial;
}

int nCr(int n, int r) {
    return factorial(n) / (factorial(r) * factorial(n - r));
}

int main() {
    int n = 5, r = 3;
      printf("%d", nCr(n, r));
    return 0;
}

// This code was contributed by Omkar Prabhune
```

## C++

```
// CPP program To calculate The Value Of nCr
#include <bits/stdc++.h>
using namespace std;

int fact(int n);

int nCr(int n, int r)
{
    return fact(n) / (fact(r) * fact(n - r));
}

// Returns factorial of n
int fact(int n)
{
    int res = 1;
    for (int i = 2; i <= n; i++)
        res = res * i;
    return res;
}

// Driver code
int main()
{
    int n = 5, r = 3;
    cout << nCr(n, r);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program To calculate
// The Value Of nCr
class GFG {

static int nCr(int n, int r)
{
    return fact(n) / (fact(r) *
                  fact(n - r));
}

// Returns factorial of n
static int fact(int n)
{
    int res = 1;
    for (int i = 2; i <= n; i++)
        res = res * i;
    return res;
}

// Driver code
public static void main(String[] args)
{
    int n = 5, r = 3;
    System.out.println(nCr(n, r));
}
}

// This code is Contributed by
// Smitha Dinesh Semwal.
```

## 蟒蛇 3

```
# Python 3 program To calculate
# The Value Of nCr

def nCr(n, r):

    return (fact(n) / (fact(r)
                * fact(n - r)))

# Returns factorial of n
def fact(n):

    res = 1

    for i in range(2, n+1):
        res = res * i

    return res

# Driver code
n = 5
r = 3
print(int(nCr(n, r)))

# This code is contributed
# by Smitha
```

## C#

```
// C# program To calculate
// The Value Of nCr
using System;

class GFG {

static int nCr(int n, int r)
{
   return fact(n) / (fact(r) *
                 fact(n - r));
}

// Returns factorial of n
static int fact(int n)
{
    int res = 1;
    for (int i = 2; i <= n; i++)
        res = res * i;
    return res;
}

   // Driver code
   public static void Main()
   {
      int n = 5, r = 3;
      Console.Write(nCr(n, r));
   }
}

// This code is Contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program To calculate
// the Value Of nCr

function nCr( $n, $r)
{
    return fact($n) / (fact($r) *
                  fact($n - $r));
}

// Returns factorial of n
function fact( $n)
{
    $res = 1;
    for ( $i = 2; $i <= $n; $i++)
        $res = $res * $i;
    return $res;
}

    // Driver code
    $n = 5;
    $r = 3;
    echo nCr($n, $r);

// This code is contributed by vt_m.
?>
```

## java 描述语言

```
<script>

// Javascript program To calculate The Value Of nCr

function nCr(n, r)
{
    return fact(n) / (fact(r) * fact(n - r));
}

// Returns factorial of n
function fact(n)
{
    var res = 1;
    for (var i = 2; i <= n; i++)
        res = res * i;
    return res;
}

// Driver code
var n = 5, r = 3;
document.write(nCr(n, r));

</script>
```

**Output:** 

```
10
```

**更高效的解决方案:**
[动态规划|集合 9(二项式系数)](https://www.geeksforgeeks.org/dynamic-programming-set-9-binomial-coefficient/)
[时空高效二项式系数](https://www.geeksforgeeks.org/space-and-time-efficient-binomial-coefficient/)
[**关于二项式系数的所有文章**](https://www.geeksforgeeks.org/tag/binomial-coefficient/)