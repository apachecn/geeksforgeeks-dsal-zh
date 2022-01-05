# 数论|加法下有限循环群的生成元

> 原文:[https://www . geesforgeks . org/generators-有限-循环-群-加法/](https://www.geeksforgeeks.org/generators-finite-cyclic-group-addition/)

给定一个数 n，求模 n 下[循环可加群](https://en.wikipedia.org/wiki/Cyclic_group)的所有生成元，集合{0，1，… n-1}的生成元是元素 x，使得 x 小于 n，利用 x(和加法运算)，我们可以生成集合的所有元素。
**例:**

```
Input : 10
Output : 1 3 7 9
The set to be generated is {0, 1, .. 9}
By adding 1, single or more times, we 
can create all elements from 0 to 9.
Similarly using 3, we can generate all
elements.
30 % 10 = 0, 21 % 10 = 1, 12 % 10 = 2, ...
Same is true for 7 and 9.

Input  : 24
Output : 1 5 7 11 13 17 19 23
```

一个**简单的解决方案**是运行一个从 1 到 n-1 的循环，对于每个元素检查它是否是发电机。为了检查生成器，我们不断添加元素，并检查是否可以生成所有数字，直到余数开始重复。
一个**有效的解决方案**是基于这样一个事实:如果 x 相对于 n 是素数，即 gcd(n，x) =1，则 x 是生成器。
以下是上述方法的实施:

## C++

```
// A simple C++ program to find all generators
#include <bits/stdc++.h>
using namespace std;

// Function to return gcd of a and b
int gcd(int a, int b)
{
    if (a == 0)
        return b;
    return gcd(b%a, a);
}

// Print generators of n
int printGenerators(unsigned int n)
{
    // 1 is always a generator
    cout << "1 ";

    for (int i=2; i < n; i++)

        // A number x is generator of GCD is 1
        if (gcd(i, n) == 1)
            cout << i << " ";
}

// Driver program to test above function
int main()
{
    int n = 10;
    printGenerators(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A simple Java program to find all generators

class GFG {

// Function to return gcd of a and b
static int gcd(int a, int b)
{
    if (a == 0)
        return b;
    return gcd(b%a, a);
}

// Print generators of n
static void printGenerators(int n)
{
    // 1 is always a generator
    System.out.println("1 ");

    for (int i=2; i < n; i++)

        // A number x is generator of GCD is 1
        if (gcd(i, n) == 1)
            System.out.println(i +" ");
}

// Driver program to test above function
public static void main(String args[])
{
    int n = 10;
    printGenerators(n);
}
}
```

## 蟒蛇 3

```
# Python3 program to find all generators

# Function to return gcd of a and b
def gcd(a, b):
    if (a == 0):
        return b;
    return gcd(b % a, a);

# Print generators of n
def printGenerators(n):

    # 1 is always a generator
    print("1", end = " ");

    for i in range(2, n):

        # A number x is generator
        # of GCD is 1
        if (gcd(i, n) == 1):
            print(i, end = " ");

# Driver Code
n = 10;
printGenerators(n);

# This code is contributed by mits
```

## C#

```
// A simple C# program to find all generators
using System;

class GFG
{

// Function to return gcd of a and b
static int gcd(int a, int b)
{
    if (a == 0)
        return b;
    return gcd(b % a, a);
}

// Print generators of n
static void printGenerators(int n)
{
    // 1 is always a generator
    Console.Write("1 ");

    for (int i = 2; i < n; i++)

        // A number x is generator of GCD is 1
        if (gcd(i, n) == 1)
            Console.Write(i +" ");
}

// Driver code
public static void Main(String []args)
{
    int n = 10;
    printGenerators(n);
}
}

// This code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find all generators

// Function to return gcd of a and b

function gcd($a, $b)
{
    if ($a == 0)
        return $b;
    return gcd($b % $a, $a);
}

// Print generators of n
function printGenerators($n)
{

    // 1 is always a generator
    echo "1 ";

    for ($i = 2; $i < $n; $i++)

        // A number x is generator
        // of GCD is 1
        if (gcd($i, $n) == 1)
            echo $i, " ";
}

// Driver program to test
// above function
    $n = 10;
    printGenerators($n);

// This code is contributed by Ajit
?>
```

## java 描述语言

```
<script>

// A simple Javascript program to
// find all generators

// Function to return gcd of a and b
function gcd(a, b)
{
    if (a == 0)
        return b;

    return gcd(b % a, a);
}

// Print generators of n
function printGenerators(n)
{

    // 1 is always a generator
    document.write("1 ");

    for(var i = 2; i < n; i++)

        // A number x is generator of
        // GCD is 1
        if (gcd(i, n) == 1)
            document.write(i + " ");
}

// Driver Code
var n = 10;

printGenerators(n);

// This code is contributed by Kirti

</script>
```

**输出:**

```
1 3 7 9
```

**这是如何工作的？**
如果我们考虑 x 的 n 个连续倍数的所有余数，那么如果 x 和 n 的 GCD 不为 1，一些余数会重复。如果一些余数重复，那么 x 就不能是生成器。注意，在 n 个连续的倍数之后，余数还是会重复。
**有趣的观察:**
一个数 n 的发生器个数等于φ(n)，其中φ是[欧拉全能性函数](https://www.geeksforgeeks.org/eulers-totient-function/)。
本文由 **Ujjwal Goyal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。