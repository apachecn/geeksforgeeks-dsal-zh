# 计算阶乘中的位数|设置 2

> 原文:[https://www.geeksforgeeks.org/count-digits-factorial-set-2/](https://www.geeksforgeeks.org/count-digits-factorial-set-2/)

给定一个整数 n(可能非常大)，求其阶乘中出现的位数，其中阶乘定义为，阶乘(n) = 1*2*3*4……..*n 和阶乘(0) = 1
**示例:**

```
Input :  n = 1
Output : 1
1! = 1, hence number of digits is 1

Input :  5
Output : 3
5! = 120, i.e., 3 digits

Input : 10
Output : 7
10! = 3628800, i.e., 7 digits

Input : 50000000
Output : 363233781

Input : 1000000000
Output : 8565705523
```

我们已经讨论了在阶乘|集合 1 中计算数字的 [**中 n 的小值的解决方案。然而，该解决方案无法处理 n > 10^6
的情况，那么，我们能改进我们的解决方案吗？
是的！我们可以。
我们可以用 Kamenetsky 的公式找到我们的答案！**](https://www.geeksforgeeks.org/count-digits-factorial-set-1/) 

```
It approximates the number of digits in a factorial by :
f(x) =    log10( ((n/e)^n) * sqrt(2*pi*n))

Thus, we can pretty easily use the property of logarithms to,
f(x) = n* log10(( n/ e)) + log10(2*pi*n)/2 
```

就这样！
我们的解决方案可以处理非常大的输入，可以容纳在 32 位整数中，
甚至更大！。
以下是以上想法的实现:

## C++

```
// A optimised program to find the
// number of digits in a factorial
#include <bits/stdc++.h>
using namespace std;

// Returns the number of digits present
// in n! Since the result can be large
// long long is used as return type
long long findDigits(int n)
{
    // factorial of -ve number
    // doesn't exists
    if (n < 0)
        return 0;

    // base case
    if (n <= 1)
        return 1;

    // Use Kamenetsky formula to calculate
    // the number of digits
    double x = ((n * log10(n / M_E) +
                 log10(2 * M_PI * n) /
                 2.0));

    return floor(x) + 1;
}

// Driver Code
int main()
{
    cout << findDigits(1) << endl;
    cout << findDigits(50000000) << endl;
    cout << findDigits(1000000000) << endl;
    cout << findDigits(120) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// An optimised java program to find the
// number of digits in a factorial
import java.io.*;
import java.util.*;

class GFG {
    public static double M_E = 2.71828182845904523536;
    public static double M_PI = 3.141592654;

     // Function returns the number of
     // digits present in n! since the
     // result can be large, long long
     // is used as return type
    static long findDigits(int n)
    {
        // factorial of -ve number doesn't exists
        if (n < 0)
            return 0;

        // base case
        if (n <= 1)
            return 1;

        // Use Kamenetsky formula to calculate
        // the number of digits
        double x = (n * Math.log10(n / M_E) +
                    Math.log10(2 * M_PI * n) /
                    2.0);

        return (long)Math.floor(x) + 1;
    }

    // Driver Code
    public static void main(String[] args)
    {
        System.out.println(findDigits(1));
        System.out.println(findDigits(50000000));
        System.out.println(findDigits(1000000000));
        System.out.println(findDigits(120));
    }
}

// This code is contributed by Pramod Kumar.
```

## 蟒蛇 3

```
# A optimised Python3 program to find
# the number of digits in a factorial
import math

# Returns the number of digits present
# in n! Since the result can be large
# long long is used as return type
def findDigits(n):

    # factorial of -ve number
    # doesn't exists
    if (n < 0):
        return 0;

    # base case
    if (n <= 1):
        return 1;

    # Use Kamenetsky formula to
    # calculate the number of digits
    x = ((n * math.log10(n / math.e) +
              math.log10(2 * math.pi * n) /2.0));

    return math.floor(x) + 1;

# Driver Code
print(findDigits(1));
print(findDigits(50000000));
print(findDigits(1000000000));
print(findDigits(120));

# This code is contributed by mits
```

## C#

```
// An optimised C# program to find the
// number of digits in a factorial.
using System;

class GFG {
    public static double M_E = 2.71828182845904523536;
    public static double M_PI = 3.141592654;

    // Function returns the number of
    // digits present in n! since the
    // result can be large, long long
    // is used as return type
    static long findDigits(int n)
    {
        // factorial of -ve number
        // doesn't exists
        if (n < 0)
            return 0;

        // base case
        if (n <= 1)
            return 1;

        // Use Kamenetsky formula to calculate
        // the number of digits
        double x = (n * Math.Log10(n / M_E) +
                    Math.Log10(2 * M_PI * n) /
                    2.0);

        return (long)Math.Floor(x) + 1;
    }

    // Driver Code
    public static void Main()
    {
        Console.WriteLine(findDigits(1));
        Console.WriteLine(findDigits(50000000));
        Console.WriteLine(findDigits(1000000000));
        Console.Write(findDigits(120));
    }
}

// This code is contributed by Nitin Mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A optimised PHP program to find the
// number of digits in a factorial

// Returns the number of digits present
// in n! Since the result can be large
// long long is used as return type
function findDigits($n)
{

    // factorial of -ve number
    // doesn't exists
    if ($n < 0)
        return 0;

    // base case
    if ($n <= 1)
        return 1;

    // Use Kamenetsky formula to
    // calculate the number of digits
    $x = (($n * log10($n / M_E) +
                log10(2 * M_PI * $n) /
                2.0));

    return floor($x) + 1;
}

    // Driver Code
    echo findDigits(1)."\n" ;
    echo findDigits(50000000)."\n" ;
    echo findDigits(1000000000)."\n" ;
    echo findDigits(120) ;

// This code is contributed by nitin mittal
?>
```

## java 描述语言

```
<script>

// A optimised Javascript program to find the
// number of digits in a factorial 

// Returns the number of digits present
// in n! Since the result can be large
// long long is used as return type
function findDigits(n)
{
    // factorial of -ve number
    // doesn't exists
    if (n < 0)
        return 0;

    // base case
    if (n <= 1)
        return 1;

    // Use Kamenetsky formula to calculate
    // the number of digits
    let x = ((n * Math.log10(n / Math.E) +
                Math.log10(2 * Math.PI * n) /
                2.0));

    return Math.floor(x) + 1;
}

// Driver Code

    document.write(findDigits(1) + "<br>");
    document.write(findDigits(50000000) + "<br>");
    document.write(findDigits(1000000000) + "<br>");
    document.write(findDigits(120) + "<br>");

// This code is contributed by Mayank Tyagi

</script>
```

**输出:**

```
1
363233781
8565705523
199
```

参考文献:[oeis.org](http://oeis.org)
本文由 [**阿舒托什·库马尔**](https://www.linkedin.com/in/ashutosh-kumar-9527a7105?trk=nav_responsive_tab_profile) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。