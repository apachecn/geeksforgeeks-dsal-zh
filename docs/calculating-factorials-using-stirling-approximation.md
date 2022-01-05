# 使用斯特林近似计算阶乘

> 原文:[https://www . geeksforgeeks . org/计算-阶乘-使用-斯特林-近似/](https://www.geeksforgeeks.org/calculating-factorials-using-stirling-approximation/)

我们知道使用循环或递归来计算阶乘，但是如果要求我们在不使用任何循环或递归的情况下计算阶乘。是的，这可以通过一种众所周知的近似算法[斯特林近似](https://en.wikipedia.org/wiki/Stirling%27s_approximation)来实现。
**例:**

```
Input : n = 6
Output : 720

Input : n = 2
Output : 2
```

**斯特林近似:**是计算阶乘的近似。它对于近似阶乘的对数也很有用。
T3【n！~ sqrt(2*pi*n) * pow((n/e)，n)
**注:**这个公式不会给出阶乘的确切值，因为它只是阶乘的近似值。

## C++

```
// CPP program for calculating factorial
// of a number using Stirling
// Approximation
#include<bits/stdc++.h>
using namespace std;

// function for calculating factorial
long int stirlingFactorial(int n)
{
    if (n == 1)
        return 1;
    long int z;
    float e = 2.71; // value of natural e

    // evaluating factorial using
    // stirling approximation
    z = sqrt(2*3.14*n) * pow((n/e), n);
    return z;
}

// driver program
int main()
{
    cout << stirlingFactorial(1) << endl;
    cout << stirlingFactorial(2) << endl;
    cout << stirlingFactorial(3) << endl;
    cout << stirlingFactorial(4) << endl;
    cout << stirlingFactorial(5) << endl;
    cout << stirlingFactorial(6) << endl;
    cout << stirlingFactorial(7) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for calculating
// factorial of a number using
// Stirling Approximation
class GFG
{

// function for
// calculating factorial
public static int stirlingFactorial(double n)
{
    if (n == 1)
        return 1;
    double z;
    double e = 2.71; // value of natural e

    // evaluating factorial using
    // stirling approximation
    z = Math.sqrt(2 * 3.14 * n) *
        Math.pow((n / e), n);
    return (int)(z);
}

// Driver Code
public static void main(String[] args)
{
    System.out.println(stirlingFactorial(1));
    System.out.println(stirlingFactorial(2));
    System.out.println(stirlingFactorial(3));
    System.out.println(stirlingFactorial(4));
    System.out.println(stirlingFactorial(5));
    System.out.println(stirlingFactorial(6));
    System.out.println(stirlingFactorial(7));
}
}

// This code is contributed by mits.
```

## 蟒蛇 3

```
# Python3 program for calculating
# factorial of a number using
# Stirling Approximation
import math

# Function for calculating factorial
def stirlingFactorial(n):
    if (n == 1):
        return 1

    # value of natural e
    e = 2.71

    # evaluating factorial using
    # stirling approximation
    z = (math.sqrt(2 * 3.14 * n) * math.pow((n / e), n))
    return math.floor(z)

# Driver Code
print(stirlingFactorial(1))
print(stirlingFactorial(2))
print(stirlingFactorial(3))
print(stirlingFactorial(4))
print(stirlingFactorial(5))
print(stirlingFactorial(6))
print(stirlingFactorial(7))

# This code is contributed by mits
```

## C#

```
// C# program for calculating
// factorial of a number using
// Stirling Approximation

class GFG
{

// function for
// calculating factorial
public static int stirlingFactorial(double n)
{
    if (n == 1)
        return 1;
    double z;
    double e = 2.71; // value of natural e

    // evaluating factorial using
    // stirling approximation
    z = System.Math.Sqrt(2 * 3.14 * n) *
        System.Math.Pow((n / e), n);
    return (int)(z);
}

// Driver Code
public static void Main()
{
    System.Console.WriteLine(stirlingFactorial(1));
    System.Console.WriteLine(stirlingFactorial(2));
    System.Console.WriteLine(stirlingFactorial(3));
    System.Console.WriteLine(stirlingFactorial(4));
    System.Console.WriteLine(stirlingFactorial(5));
    System.Console.WriteLine(stirlingFactorial(6));
    System.Console.WriteLine(stirlingFactorial(7));
}
}

// This code is contributed by mits.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for calculating factorial
// of a number using Stirling
// Approximation

// Function for calculating factorial
function stirlingFactorial($n)
{
    if ($n == 1)
        return 1;
    $z;

    // value of natural e
    $e = 2.71;

    // evaluating factorial using
    // stirling approximation
    $z = sqrt(2 * 3.14 * $n) *
         pow(($n / $e), $n);
    return floor($z);
}

    // Driver Code
    echo stirlingFactorial(1),"\n";
    echo stirlingFactorial(2) ,"\n";
    echo stirlingFactorial(3) ,"\n";
    echo stirlingFactorial(4), "\n" ;
    echo stirlingFactorial(5) ,"\n";
    echo stirlingFactorial(6) ," \n";
    echo stirlingFactorial(7) ," \n";

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
// Javascript program for calculating factorial
// of a number using Stirling
// Approximation

// Function for calculating factorial
function stirlingFactorial(n)
{
    if (n == 1)
        return 1;
    let z;

    // value of natural e
    let e = 2.71;

    // evaluating factorial using
    // stirling approximation
    z = Math.sqrt(2 * 3.14 * n) *
         Math.pow((n / e), n);
    return Math.floor(z);
}

    // Driver Code
    document.write( stirlingFactorial(1) + "<br>");
    document.write( stirlingFactorial(2) + "<br>");
    document.write( stirlingFactorial(3) + "<br>");
    document.write( stirlingFactorial(4) + "<br>");
    document.write( stirlingFactorial(5) + "<br>");
    document.write( stirlingFactorial(6) + "<br>");
    document.write( stirlingFactorial(7) + "<br>");

// This code is contributed by _saurabh_jaiswal.
</script>
```

**输出:**

```
1
1
5
23
119
723
5086
```

本文由[**Shivam Pradhan(anuj _ charm)**](https://www.facebook.com/anuj.charm)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。