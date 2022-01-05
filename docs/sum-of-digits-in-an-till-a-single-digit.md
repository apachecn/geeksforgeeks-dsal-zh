# a^n 的位数总和，直到一位数

> 原文:[https://www . geesforgeks . org/一位数总和/直到一位数/](https://www.geeksforgeeks.org/sum-of-digits-in-an-till-a-single-digit/)

给定两个数字 a 和 n，任务是找出 a^n(幂(a，n))的位数之和。在一位数求和中，我们一直做位数求和，直到剩下一位数。
**例:**

```
Input : a = 5, n = 4
Output : 4
5^4 = 625 = 6+2+5 = 13
Since 13 has two digits, we
sum again 1 + 3 = 4.

Input : a = 2, n = 8
Output : 4
2^8=256 = 2+5+6 = 13 = 1+3 = 4
```

一种天真的方法是首先找到 a^n，然后使用这里讨论的方法找到 a^n 的数字总和。
以上做法可能造成溢出。更好的解决方案是基于以下观察。

```
int res = 1;
for (int i=1; i<=n; i++)
{
     res = res*a;
     res = digSum(res);
}

Here digSum() finds single digit sum 
of res. Please refer this for details
of digSum().
```

以上伪代码图解:

> 例如，假设 a = 5，n = 4。
> 第一次迭代后，
> res = 5
> 第二次迭代后，
> res = 7(注:2 + 5 = 7)
> 第三次迭代后，
> res = 8(注:3 + 5 = 8)
> 第四次迭代后，
> res = 4(注:4 + 0 = 4)

我们可以写一个类似于快速模幂运算的函数来计算 digSum(a^n)，它以对数(n)步来计算。
以下是上述方法的实施:

## C++

```
// CPP program to find single digit
// sum of a^n.
#include <bits/stdc++.h>
using namespace std;

// This function finds single digit
// sum of n.
int digSum(int n)
{
    if (n == 0)
    return 0;
    return (n % 9 == 0) ? 9 : (n % 9);
}

// Returns single digit sum of a^n.
// We use modular exponentiation technique.
int powerDigitSum(int a, int n)
{
    int res = 1;
    while (n) {
        if (n % 2 == 1) {
            res = res * digSum(a);
            res = digSum(res);
        }
        a = digSum(digSum(a) * digSum(a));
        n /= 2;
    }

    return res;
}

// Driver code
int main()
{
    int a = 9, n = 4;
    cout << powerDigitSum(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find single digit
// sum of a^n.

import java.util.*;
import java.lang.*;
import java.io.*;

class GFG{

// This function finds single digit
// sum of n.
static int digSum(int n)
{
    if (n == 0)
    return 0;
    return (n % 9 == 0) ? 9 : (n % 9);
}

// Returns single digit sum of a^n.
// We use modular exponentiation technique.
static int powerDigitSum(int a, int n)
{
    int res = 1;
    while (n>0) {
        if (n % 2 == 1) {
            res = res * digSum(a);
            res = digSum(res);
        }
        a = digSum(digSum(a) * digSum(a));
        n /= 2;
    }

    return res;
}

// Driver code
public static void main(String args[])
{
    int a = 9, n = 4;
    System.out.print(powerDigitSum(a, n));
}
}
```

## 蟒蛇 3

```
# Python 3 Program to find single digit
# sum of a^n.

# This function finds single digit
# sum of n.
def digSum(n) :

    if n == 0 :
        return 0

    elif n % 9 == 0 :
        return 9

    else :
        return n % 9

# Returns single digit sum of a^n.
# We use modular exponentiation technique.
def powerDigitSum(a, n) :

    res = 1
    while(n) :

        if n %2 == 1 :
            res = res * digSum(a)
            res = digSum(res)

        a = digSum(digSum(a) * digSum(a))
        n //= 2

    return res

# Driver Code
if __name__ == "__main__" :

    a, n = 9, 4
    print(powerDigitSum(a, n))

# This code is contributed by ANKITRAI1
```

## C#

```
// C# program to find single
// digit sum of a^n.
class GFG
{

// This function finds single
// digit sum of n.
static int digSum(int n)
{
    if (n == 0)
    return 0;
    return (n % 9 == 0) ?
                      9 : (n % 9);
}

// Returns single digit sum of a^n.
// We use modular exponentiation
// technique.
static int powerDigitSum(int a, int n)
{
    int res = 1;
    while (n > 0)
    {
        if (n % 2 == 1)
        {
            res = res * digSum(a);
            res = digSum(res);
        }
        a = digSum(digSum(a) * digSum(a));
        n /= 2;
    }

    return res;
}

// Driver code
static void Main()
{
    int a = 9, n = 4;
    System.Console.WriteLine(powerDigitSum(a, n));
}
}

// This Code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find single 
// digit sum of a^n.

// This function finds single
// digit sum of n.
function digSum($n)
{
    if ($n == 0)
    return 0;
    return ($n % 9 == 0) ?
                 9 : ($n % 9);
}

// Returns single digit sum 
// of a^n. We use modular
// exponentiation technique.
function powerDigitSum($a, $n)
{
    $res = 1;
    while ($n)
    {
        if ($n % 2 == 1)
        {
            $res = $res * digSum($a);
            $res = digSum($res);
        }
        $a = digSum(digSum($a) *
             digSum($a));
        $n /= 2;
    }

    return $res;
}

// Driver code
$a = 9;
$n = 4;
echo powerDigitSum($a, $n);

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

// javascript program to find single digit
// sum of a^n.

// This function finds single digit
// sum of n.
function digSum( n)
{
    if (n == 0)
    return 0;
    return (n % 9 == 0) ? 9 : (n % 9);
}

// Returns single digit sum of a^n.
// We use modular exponentiation technique.
function powerDigitSum( a,  n)
{
    let res = 1;
    while (n) {
        if (n % 2 == 1) {
            res = res * digSum(a);
            res = digSum(res);
        }
        a = digSum(digSum(a) * digSum(a));
        n /= 2;
    }

    return res;
}

// Driver code

    let a = 9, n = 4;
    document.write( powerDigitSum(a, n));

// This code is contributed by todaysgaurav

</script>
```

**Output:** 

```
9
```