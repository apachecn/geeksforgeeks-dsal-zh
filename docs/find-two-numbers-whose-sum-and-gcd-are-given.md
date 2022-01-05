# 找出两个和和 GCD 都给定的数字

> 原文:[https://www . geeksforgeeks . org/find-two-numbers-what-sum-and-gcd-被给定/](https://www.geeksforgeeks.org/find-two-numbers-whose-sum-and-gcd-are-given/)

给定两个数![a ](img/0ba2157801528a19d4dd5da5850ab39f.png "Rendered by QuickLaTeX.com")和![b ](img/0420d5d1d372a7e46d5d3b7e9aa62581.png "Rendered by QuickLaTeX.com")的**和**以及 **gcd** 。任务是找到数字 *a 和 b* 。如果数字不存在，则打印![-1 ](img/6687bcfd83e9eddc47b97c76d797bc11.png "Rendered by QuickLaTeX.com")。
**举例:**

> **输入:**和= 6，gcd = 2
> **输出:** a = 4，b = 2
> 4 + 2 = 6，gcd(4，2) = 2
> **输入:**和= 7，gcd = 2
> **输出:** -1
> 没有和为 7，GCD 为 2
> 的数字

**方法:**当给出 [GCD](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 时，已知两个数字都是它的倍数。

*   选择第一个数字作为 *gcd* ，然后另一个数字将是*sum–gcd*。
*   如果上一步选择的两个数字之和等于*之和*，则打印两个数字。
*   否则数字不存在，打印 *-1* 代替。

以下是上述方法的实现:

## C++

```
// C++ program to find two numbers
// whose sum and GCD is given
#include <bits/stdc++.h>
using namespace std;

// Function to find two numbers
// whose sum and gcd is given
void findTwoNumbers(int sum, int gcd)
{
    // sum != gcd checks that both the
    // numbers are positive or not
    if (__gcd(gcd, sum - gcd) == gcd && sum != gcd)
        cout << "a = " << min(gcd, sum - gcd)
             << ", b = " << sum - min(gcd, sum - gcd)
             << endl;
    else
        cout << -1 << endl;
}

// Driver code
int main()
{
    int sum = 8;
    int gcd = 2;

    findTwoNumbers(sum, gcd);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find two numbers
// whose sum and GCD is given
import java.util.*;
class Solution{

//function to find gcd of two numbers
static int __gcd(int a,int b)
{
    if (b==0) return a;
   return __gcd(b,a%b);
}

// Function to find two numbers
// whose sum and gcd is given
static void findTwoNumbers(int sum, int gcd)
{
    // sum != gcd checks that both the
    // numbers are positive or not
    if (__gcd(gcd, sum - gcd) == gcd && sum != gcd)
        System.out.println(  "a = " + Math.min(gcd, sum - gcd)
            + ", b = " + (int)(sum - Math.min(gcd, sum - gcd)) );
    else
        System.out.println( -1 );
}

// Driver code
public static void main(String args[])
{
    int sum = 8;
    int gcd = 2;

    findTwoNumbers(sum, gcd);

}

}
//contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python 3 program to find two numbers
# whose sum and GCD is given
from math import gcd as __gcd

# Function to find two numbers
# whose sum and gcd is given
def findTwoNumbers(sum, gcd):

    # sum != gcd checks that both the
    # numbers are positive or not
    if (__gcd(gcd, sum - gcd) == gcd and
                          sum != gcd):
        print("a =", min(gcd, sum - gcd),
              ", b =", sum - min(gcd, sum - gcd))
    else:
        print(-1)

# Driver code
if __name__ == '__main__':
    sum = 8
    gcd = 2

    findTwoNumbers(sum, gcd)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find two numbers
// whose sum and GCD is given
using System;
class GFG
{

// function to find gcd of two numbers
static int __gcd(int a, int b)
{
    if (b == 0)
        return a;
    return __gcd(b, a % b);
}

// Function to find two numbers
// whose sum and gcd is given
static void findTwoNumbers(int sum, int gcd)
{
    // sum != gcd checks that both the
    // numbers are positive or not
    if (__gcd(gcd, sum - gcd) == gcd && sum != gcd)
        Console.WriteLine("a = " + Math.Min(gcd, sum - gcd) +
            ", b = " + (int)(sum - Math.Min(gcd, sum - gcd)));
    else
        Console.WriteLine( -1 );
}

// Driver code
public static void Main()
{
    int sum = 8;
    int gcd = 2;

    findTwoNumbers(sum, gcd);
}
}

// This code is contributed by anuj_67..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find two numbers
// whose sum and GCD is given

// Function to find gcd of two numbers
function __gcd($a, $b)
{
    if ($b == 0)
        return $a;

    return __gcd($b, $a % $b);
}

// Function to find two numbers
// whose sum and gcd is given
function findTwoNumbers($sum, $gcd)
{
    // sum != gcd checks that both the
    // numbers are positive or not
    if (__gcd($gcd, $sum - $gcd) == $gcd &&
                            $sum != $gcd)
        echo "a = " , min($gcd, $sum - $gcd),
             " b = ", (int)($sum - min($gcd,
                            $sum - $gcd));
    else
        echo (-1);
}

// Driver code
$sum = 8;
$gcd = 2;

findTwoNumbers($sum, $gcd);

// This code is contributed by Sachin
?>
```

## java 描述语言

```
<script>

// Javascript program to find two numbers
// whose sum and GCD is given

//function to find gcd of two numbers
function __gcd(a, b)
{
    if (b==0) return a;
   return __gcd(b,a%b);
}

// Function to find two numbers
// whose sum and gcd is given
function findTwoNumbers(sum, gcd)
{
    // sum != gcd checks that both the
    // numbers are positive or not
    if (__gcd(gcd, sum - gcd) == gcd && sum != gcd)
        document.write(  "a = " + Math.min(gcd, sum - gcd)
            + ", b = " + (sum - Math.min(gcd, sum - gcd)) );
    else
        document.write( -1 );
}

// Driver code

    let sum = 8;
    let gcd = 2;

    findTwoNumbers(sum, gcd);

</script>
```

**Output:** 

```
a = 2, b = 6
```