# 打印给定数目的所有质因数的高效程序

> 原文:[https://www . geesforgeks . org/print-all-prime-factors-of-a-number/](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)

给定一个数字 n，写一个高效的函数打印 n 的所有[质因数](http://en.wikipedia.org/wiki/Prime_factor)，比如输入数字是 12，那么输出应该是“2 2 3”。如果输入的数字是 315，那么输出应该是“3 3 5 7”。

以下是寻找所有主要因素的步骤。
**1)** 当 n 可被 2 整除时，打印 2 并除以 2。
**2)** 第 1 步之后，n 一定是奇数。现在开始一个从 i = 3 到 n 的平方根的循环，当我除 n 时，打印 I，用 I 除 n，在我未能除 n 后，将 I 增加 2 并继续。
**3)** 如果 n 是素数且大于 2，那么通过以上两步 n 不会变成 1。所以如果大于 2 就打印 n。

## C++

```
// C++ program to print all prime factors
#include <bits/stdc++.h>
using namespace std;

// A function to print all prime
// factors of a given number n
void primeFactors(int n)
{
    // Print the number of 2s that divide n
    while (n % 2 == 0)
    {
        cout << 2 << " ";
        n = n/2;
    }

    // n must be odd at this point. So we can skip
    // one element (Note i = i +2)
    for (int i = 3; i <= sqrt(n); i = i + 2)
    {
        // While i divides n, print i and divide n
        while (n % i == 0)
        {
            cout << i << " ";
            n = n/i;
        }
    }

    // This condition is to handle the case when n
    // is a prime number greater than 2
    if (n > 2)
        cout << n << " ";
}

/* Driver code */
int main()
{
    int n = 315;
    primeFactors(n);
    return 0;
}

// This is code is contributed by rathbhupendra
```

## C

```
// Program to print all prime factors
# include <stdio.h>
# include <math.h>

// A function to print all prime factors of a given number n
void primeFactors(int n)
{
    // Print the number of 2s that divide n
    while (n%2 == 0)
    {
        printf("%d ", 2);
        n = n/2;
    }

    // n must be odd at this point.  So we can skip
    // one element (Note i = i +2)
    for (int i = 3; i <= sqrt(n); i = i+2)
    {
        // While i divides n, print i and divide n
        while (n%i == 0)
        {
            printf("%d ", i);
            n = n/i;
        }
    }

    // This condition is to handle the case when n
    // is a prime number greater than 2
    if (n > 2)
        printf ("%d ", n);
}

/* Driver program to test above function */
int main()
{
    int n = 315;
    primeFactors(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Program to print all prime factors
import java.io.*;
import java.lang.Math;

class GFG
{
    // A function to print all prime factors
    // of a given number n
    public static void primeFactors(int n)
    {
        // Print the number of 2s that divide n
        while (n%2==0)
        {
            System.out.print(2 + " ");
            n /= 2;
        }

        // n must be odd at this point.  So we can
        // skip one element (Note i = i +2)
        for (int i = 3; i <= Math.sqrt(n); i+= 2)
        {
            // While i divides n, print i and divide n
            while (n%i == 0)
            {
                System.out.print(i + " ");
                n /= i;
            }
        }

        // This condition is to handle the case when
        // n is a prime number greater than 2
        if (n > 2)
            System.out.print(n);
    }

    public static void main (String[] args)
    {
        int n = 315;
        primeFactors(n);
    }
}
```

## 计算机编程语言

```
# Python program to print prime factors

import math

# A function to print all prime factors of
# a given number n
def primeFactors(n):

    # Print the number of two's that divide n
    while n % 2 == 0:
        print 2,
        n = n / 2

    # n must be odd at this point
    # so a skip of 2 ( i = i + 2) can be used
    for i in range(3,int(math.sqrt(n))+1,2):

        # while i divides n , print i and divide n
        while n % i== 0:
            print i,
            n = n / i

    # Condition if n is a prime
    # number greater than 2
    if n > 2:
        print n

# Driver Program to test above function

n = 315
primeFactors(n)

# This code is contributed by Harshit Agrawal
```

## C#

```
// C# Program to print all prime factors
using System;

namespace prime
{
public class GFG
{    

    // A function to print all prime
    // factors of a given number n
    public static void primeFactors(int n)
    {
        // Print the number of 2s that divide n
        while (n % 2 == 0)
        {
            Console.Write(2 + " ");
            n /= 2;
        }

        // n must be odd at this point. So we can
        // skip one element (Note i = i +2)
        for (int i = 3; i <= Math.Sqrt(n); i+= 2)
        {
            // While i divides n, print i and divide n
            while (n % i == 0)
            {
                Console.Write(i + " ");
                n /= i;
            }
        }

        // This condition is to handle the case whien
        // n is a prime number greater than 2
        if (n > 2)
            Console.Write(n);
    }

    // Driver Code
    public static void Main()
    {
        int n = 315;
        primeFactors(n);
    }

}
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Efficient program to print all
// prime factors of a given number

// function to print all prime
// factors of a given number n
function primeFactors($n)
{

    // Print the number of
    // 2s that divide n
    while($n % 2 == 0)
    {
        echo 2," ";
        $n = $n / 2;
    }

    // n must be odd at this
    // point. So we can skip
    // one element (Note i = i +2)
    for ($i = 3; $i <= sqrt($n);
                   $i = $i + 2)
    {

        // While i divides n,
        // print i and divide n
        while ($n % $i == 0)
        {
            echo $i," ";
            $n = $n / $i;
        }
    }

    // This condition is to
    // handle the case when n
    // is a prime number greater
    // than 2
    if ($n > 2)
        echo $n," ";
}

    // Driver Code
    $n = 315;
    primeFactors($n);

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>

// JavaScript program to print all prime factors

// A function to print all prime
// factors of a given number n
function primeFactors(n)
{

    // Print the number of 2s that divide n
    while (n % 2 == 0)
    {
        document.write(2 + " ");
        n = Math.floor(n / 2);
    }

    // n must be odd at this point.
    // So we can skip one element
    // (Note i = i +2)
    for(let i = 3;
            i <= Math.floor(Math.sqrt(n));
            i = i + 2)
    {

        // While i divides n, print i
        // and divide n
        while (n % i == 0)
        {
            document.write(i + " ");
            n = Math.floor(n / i);
        }
    }

    // This condition is to handle the
    // case when n is a prime number
    // greater than 2
    if (n > 2)
        document.write(n + " ");
}

// Driver code
let n = 315;

primeFactors(n);

// This code is contributed by Surbhi Tyagi.

</script>
```

输出:

```
3 3 5 7
```

**这是如何工作的？**
步骤 1 和 2 处理复合数，步骤 3 处理素数。为了证明完整的算法是有效的，我们需要证明步骤 1 和 2 实际上处理了复合数。很明显，步骤 1 处理偶数。在步骤 1 之后，所有剩余的质因数必须是奇数(两个质因数的差必须至少为 2)，这解释了为什么 I 增加 2。

现在主要部分是，循环运行到 n 的平方根，而不是 n。为了证明这种优化是有效的，让我们考虑复合数的以下性质。

*每个复合数至少有一个质因数小于或等于*本身的*平方根。*
这个性质可以用反例来证明。设 a 和 b 是 n 的两个因子，使得 a*b = n，如果两者都大于√n，那么 a.b > √n，* √n，这与表达式“a * b = n”相矛盾。

在上述算法的步骤 2 中，我们运行一个循环，并在循环
中执行以下操作:a)找到最小质因数 I(必须小于√n)，
b)通过重复用 I 除 n 来从 n 中移除所有出现的 I，即
c)对除 n 和 i = i + 2 重复步骤 a 和 b。重复步骤 a 和 b，直到 n 变成 1 或质数。

**相关文章:**
[使用筛子 O(log n)进行多查询的素分解](https://www.geeksforgeeks.org/prime-factorization-using-sieve-olog-n-multiple-queries/)
感谢 **Vishwas Garg** 提出上述算法。如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息