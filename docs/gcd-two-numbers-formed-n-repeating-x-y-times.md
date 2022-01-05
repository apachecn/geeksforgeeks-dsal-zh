# n 次重复 x 和 y 次形成的两个数的 GCD

> 原文:[https://www . geesforgeks . org/gcd-two-numbers-formed-n-repeating-x-y-times/](https://www.geeksforgeeks.org/gcd-two-numbers-formed-n-repeating-x-y-times/)

给定三个正整数 **n** 、 **x** 、 **y** 。任务是打印 n 次重复 x 次形成的数和 n 次重复 y 次形成的数的最大公约数。
0 < = n，x，y < = 1000000000。
**示例:**

```
Input : n = 123, x = 2, y = 3.
Output : 123
Number formed are 123123 and 123123123.
Greatest Common Divisor of 123123 and
123123123 is 123.

Input : n = 4, x = 4, y = 6.
Output : 44
```

这个想法是基于[欧几里德算法计算两个数](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/)的 GCD。
设 f(n，x)是一个给出 n 次重复的数的函数。所以，我们需要求 GCD(f(n，x)，f(n，y))。
设 n = 123，x = 3，y = 2。
所以，第一个数字 A 是 f(123，3) = 123123123，第二个数字 B 是 f(123，2) = 123123。我们知道，GCD(A，B)= GCD(A–B，B)，利用这个性质，我们可以从第一个 A 中减去 B 的任意倍数，比如说 B’，只要 B’小于 A 即可。
所以，A = 123123123，B’可以是 123123000。减去 A 将变成 123，B 保持不变。
因此，A = A–B’= f(n，x–y)。
那么，GCD(f(n，x)，f(n，y)) = GCD(f(n，x–y)，f(n，y))
我们可以得出如下结论:

```
GCD(f(n, x), f(n, y)) = f(n, GCD(x, y)). 
```

下面是基于这种方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to print Greatest Common Divisor
// of number formed by N repeating x times and
// y times.
#include<bits/stdc++.h>
using namespace std;

// Return the Greatest common Divisor of two numbers.
int gcd(int a, int b)
{
    if (a == 0)
        return b;
    return gcd(b%a, a);
}

// Prints Greatest Common Divisor of number formed
// by n repeating x times and y times.
void findgcd(int n, int x, int y)
{
    // Finding GCD of x and y.
    int g = gcd(x,y);

    // Print n, g times.
    for (int i = 0; i < g; i++)
        cout << n;
}

// Driven Program
int main()
{
    int n = 123, x = 5, y = 2;
    findgcd(n, x, y);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print Greatest Common Divisor
// of number formed by N repeating x times and
// y times
class GFG {

    // Return the Greatest common Divisor
    // of two numbers.
    static int gcd(int a, int b) {

        if (a == 0)
            return b;

        return gcd(b % a, a);
    }

    // Prints Greatest Common Divisor of
    // number formed by n repeating x
    // times and y times.
    static void findgcd(int n, int x, int y) {

        // Finding GCD of x and y.
        int g = gcd(x, y);

        // Print n, g times.
        for (int i = 0; i < g; i++)
            System.out.print(n);
    }

    // Driver code
    public static void main(String[] args) {

        int n = 123, x = 5, y = 2;
        findgcd(n, x, y);
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python program to print Greatest
# Common Divisor of number formed
# by N repeating x times and y times

# Return the Greatest common Divisor
# of two numbers.
def gcd(a, b):

    if (a == 0):
        return b

    return gcd(b % a, a)

# Prints Greatest Common Divisor of
# number formed by n repeating x times
# and y times.
def findgcd(n, x, y):

    # Finding GCD of x and y.
    g = gcd(x, y)

    # Print n, g times.
    for i in range(g):
        print(n)

# Driver code
n = 123
x = 5
y = 2

findgcd(n, x, y)

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# program to print Greatest Common
// Divisor of number formed by N
// repeating x times and y times
using System;

class GFG {

    // Return the Greatest common
    // Divisor of two numbers.
    static int gcd(int a, int b)
    {

        if (a == 0)
            return b;

        return gcd(b % a, a);
    }

    // Prints Greatest Common
    // Divisor of number formed
    // by n repeating x times
    // and y times.
    static void findgcd(int n,
                      int x, int y)
    {

        // Finding GCD of x and y.
        int g = gcd(x, y);

        // Print n, g times.
        for (int i = 0; i < g; i++)
            Console.Write(n);
    }

    // Driver code
    public static void Main() {

        int n = 123, x = 5, y = 2;

        findgcd(n, x, y);
    }
}

// This code is contributed by
// nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print
// Greatest Common Divisor
// of number formed by N
// repeating x times and y times.

// Return the Greatest common
// Divisor of two numbers.
function gcd($a, $b)
{
    if ($a == 0)
        return $b;
    return gcd($b % $a, $a);
}

// Prints Greatest Common Divisor
// of number formed by n repeating
// x times and y times.
function findgcd($n, $x, $y)
{
    // Finding GCD of x and y.
    $g = gcd($x, $y);

    // Print n, g times.
    for ($i = 0; $i < $g; $i++)
        echo($n);
}

// Driver Code
$n = 123; $x = 5; $y = 2;
findgcd($n, $x, $y);

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// Javascript program to print Greatest Common Divisor
// of number formed by N repeating x times and
// y times.

// Return the Greatest common Divisor of two numbers.
function gcd(a, b)
{
    if (a == 0)
        return b;
    return gcd(b%a, a);
}

// Prints Greatest Common Divisor of number formed
// by n repeating x times and y times.
function findgcd(n, x, y)
{
    // Finding GCD of x and y.
    let g = gcd(x,y);

    // Print n, g times.
    for (let i = 0; i < g; i++)
        document.write(n);
}

// Driven Program

    let n = 123, x = 5, y = 2;
    findgcd(n, x, y);

// This is code is contributed by Mayank Tyagi

</script>
```

**输出:**

```
123
```

本文由 [**Anuj Chauhan**](https://www.facebook.com/anuj0503) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。