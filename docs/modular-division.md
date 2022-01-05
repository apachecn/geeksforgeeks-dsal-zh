# 模块化划分

> 原文:[https://www.geeksforgeeks.org/modular-division/](https://www.geeksforgeeks.org/modular-division/)

给定三个正数 a，b 和 m。在模 m 下计算 a/b。任务基本上是找到一个数 c，使得(b * c)% m = a % m
**例:**

```
Input  : a  = 8, b = 4, m = 5
Output : 2

Input  : a  = 8, b = 3, m = 5
Output : 1
Note that (1*3)%5 is same as 8%5

Input  : a  = 11, b = 4, m = 5
Output : 4
Note that (4*4)%5 is same as 11%5
```

以下文章是这方面的先决条件。
[模乘逆](https://www.geeksforgeeks.org/multiplicative-inverse-under-modulo-m/)
[扩展欧氏算法](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/)
**我们能一直做模除法吗？**
答案是“否”。首先，和普通算术一样，除以 0 是没有定义的。例如，不允许 4/0。在模算术中，不仅不允许 4/0，而且模 6 下的 4/12 也不允许。原因是，当模量为 6 时，12 与 0 全等。
**模块化划分是什么时候定义的？**
当除数的模逆存在时，定义模除。整数“x”的倒数是另一个整数“y”，使得(x*y) % m = 1，其中 m 是模数。
逆什么时候存在？如这里所讨论的，如果‘a’和‘m’是同素的，即它们的 GCD 是 1，则在模‘m’下存在一个数‘a’的倒数。
**如何找到模块化划分？**

```
The task is to compute a/b under modulo m.
1) First check if inverse of b under modulo m exists or not. 
    a) If inverse doesn't exists (GCD of b and m is not 1), 
          print "Division not defined"
    b) Else return  "(inverse * a) % m" 
```

## C

```
// C program to do modular division
#include <stdio.h>

// C function for extended Euclidean Algorithm
int gcdExtended(int a, int b, int *x, int *y);

// Function to find modulo inverse of b. It returns
// -1 when inverse doesn't
int modInverse(int b, int m)
{
    int x, y; // used in extended GCD algorithm
    int g = gcdExtended(b, m, &x, &y);

    // Return -1 if b and m are not co-prime
    if (g != 1)
        return -1;

    // m is added to handle negative x
    return (x%m + m) % m;
}

// Function to compute a/b under modulo m
void modDivide(int a, int b, int m)
{
    a = a % m;
    int inv = modInverse(b, m);
    if (inv == -1)
     printf ("Division not defined");
    else
    {
      int c = (inv * a) % m ;
       printf ("Result of division is %d", c) ;
    }
}

// C function for extended Euclidean Algorithm (used to
// find modular inverse.
int gcdExtended(int a, int b, int *x, int *y)
{
    // Base Case
    if (a == 0)
    {
        *x = 0, *y = 1;
        return b;
    }

    int x1, y1; // To store results of recursive call
    int gcd = gcdExtended(b%a, a, &x1, &y1);

    // Update x and y using results of recursive
    // call
    *x = y1 - (b/a) * x1;
    *y = x1;

    return gcd;
}

// Driver Program
int main()
{
    int  a  = 8, b = 3, m = 5;
    modDivide(a, b, m);
    return 0;
}
```

## 蟒蛇 3

```
# Python3 program to do modular division
import math

# Function to find modulo inverse of b. It returns
# -1 when inverse doesn't
# modInverse works for prime m
def modInverse(b,m):
    g = math.gcd(b, m)
    if (g != 1):
        # print("Inverse doesn't exist")
        return -1
    else:
        # If b and m are relatively prime,
        # then modulo inverse is b^(m-2) mode m
        return pow(b, m - 2, m)

# Function to compute a/b under modulo m
def modDivide(a,b,m):
    a = a % m
    inv = modInverse(b,m)
    if(inv == -1):
        print("Division not defined")
    else:
        print("Result of Division is ",(inv*a) % m)

# Driver Program
a = 8
b = 3
m = 5
modDivide(a, b, m)

# This code is Contributed by HarendraSingh22
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to do modular division

// Function to find modulo inverse of b.
// It returns -1 when inverse doesn't
function modInverse($b, $m)
{
    $x = 0;
    $y = 0; // used in extended GCD algorithm
    $g = gcdExtended($b, $m, $x, $y);

    // Return -1 if b and m are not co-prime
    if ($g != 1)
        return -1;

    // m is added to handle negative x
    return ($x % $m + $m) % $m;
}

// Function to compute a/b under modulo m
function modDivide($a, $b, $m)
{
    $a = $a % $m;
    $inv = modInverse($b, $m);
    if ($inv == -1)
        echo "Division not defined";
    else
        echo "Result of division is " .
                      ($inv * $a) % $m;
}

// function for extended Euclidean Algorithm
// (used to find modular inverse.
function gcdExtended($a, $b, &$x, &$y)
{
    // Base Case
    if ($a == 0)
    {
        $x = 0;
        $y = 1;
        return $b;
    }

    $x1 = 0;
    $y1 = 0; // To store results of recursive call
    $gcd = gcdExtended($b % $a, $a, $x1, $y1);

    // Update x and y using results of
    // recursive call
    $x = $y1 - (int)($b / $a) * $x1;
    $y = $x1;

    return $gcd;
}

// Driver Code
$a = 8;
$b = 3;
$m = 5;
modDivide($a, $b, $m);

// This code is contributed by mits
?>
```

## C++

```
// C++ program to do modular division
#include<iostream>
using namespace std;

// C++ function for extended Euclidean Algorithm
int gcdExtended(int a, int b, int *x, int *y);

// Function to find modulo inverse of b. It returns
// -1 when inverse doesn't
int modInverse(int b, int m)
{
    int x, y; // used in extended GCD algorithm
    int g = gcdExtended(b, m, &x, &y);

    // Return -1 if b and m are not co-prime
    if (g != 1)
        return -1;

    // m is added to handle negative x
    return (x%m + m) % m;
}

// Function to compute a/b under modulo m
void modDivide(int a, int b, int m)
{
    a = a % m;
    int inv = modInverse(b, m);
    if (inv == -1)
       cout << "Division not defined";
    else
       cout << "Result of division is " << (inv * a) % m;
}

// C function for extended Euclidean Algorithm (used to
// find modular inverse.
int gcdExtended(int a, int b, int *x, int *y)
{
    // Base Case
    if (a == 0)
    {
        *x = 0, *y = 1;
        return b;
    }

    int x1, y1; // To store results of recursive call
    int gcd = gcdExtended(b%a, a, &x1, &y1);

    // Update x and y using results of recursive
    // call
    *x = y1 - (b/a) * x1;
    *y = x1;

    return gcd;
}

// Driver Program
int main()
{
    int  a  = 8, b = 3, m = 5;
    modDivide(a, b, m);
    return 0;
}

//this code is contributed by khushboogoyal499
```

**输出:**

```
Result of division is 1
```

**模除不同于加减乘除。**
一个区别是分裂并不总是存在的(如上所述)。下面是另一个区别。

```
Below equations are valid
(a * b) % m = ((a % m) * (b % m)) % m
(a + b) % m = ((a % m) + (b % m)) % m

// m is added to handle negative numbers
(a - b + m) % m = ((a % m) - (b % m) + m) % m 

But, 
(a / b) % m may NOT be same as ((a % m)/(b % m)) % m

For example, a = 10, b = 5, m = 5\. 
   (a / b) % m is 2, but ((a % m) / (b % m)) % m 
                          is not defined.
```

**参考文献:**
[【http://www.doc.ic.ac.uk/~mrh/330tutor/ch03.html】](http://www.doc.ic.ac.uk/~mrh/330tutor/ch03.html)
本文由 **Dheeraj Gupta** 供稿。如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息