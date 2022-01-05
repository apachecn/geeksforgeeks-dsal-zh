# 计算阶乘中的位数|设置 1

> 原文:[https://www.geeksforgeeks.org/count-digits-factorial-set-1/](https://www.geeksforgeeks.org/count-digits-factorial-set-1/)

给定一个整数 n，求其阶乘中出现的位数，其中阶乘定义为，阶乘(n) = 1*2*3*4……..*n 和阶乘(0) = 1
**示例:**

```
Input :  n = 1
Output : 1
1! = 1 , hence number of digits is 1

Input :  5
Output : 3
5! = 120, i.e., 3 digits

Input : 10
Output : 7
10! = 3628800, i.e., 7 digits
```

一个天真的解决方案是计算 n！首先，然后计算其中的位数。然而作为 n 的值！可能非常大，将它们存储在变量中会变得很麻烦(除非您使用 python！) .
更好的解决方案是利用对数的有用性质来计算所需答案。

```
We know,
log(a*b) = log(a) + log(b)

Therefore
log( n! ) = log(1*2*3....... * n) 
          = log(1) + log(2) + ........ +log(n)

Now, observe that the floor value of log base 
10 increased by 1, of any number, gives the
number of digits present in that number.

Hence, output would be : floor(log(n!)) + 1.
```

下面是一个相同的实现。

## C++

```
// A C++ program to find the number of digits in
// a factorial
#include <bits/stdc++.h>
using namespace std;

// This function receives an integer n, and returns
// the number of digits present in n!
int findDigits(int n)
{
    // factorial exists only for n>=0
    if (n < 0)
        return 0;

    // base case
    if (n <= 1)
        return 1;

    // else iterate through n and calculate the
    // value
    double digits = 0;
    for (int i=2; i<=n; i++)
        digits += log10(i);

    return floor(digits) + 1;
}

// Driver code
int main()
{
    cout << findDigits(1) << endl;
    cout << findDigits(5) << endl;
    cout << findDigits(10) << endl;
    cout << findDigits(120) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the number
// of digits in a factorial

import java.io.*;
import java.util.*;

class GFG
{
    // returns the number of digits
    // present in n!
    static int findDigits(int n)
    {
        // factorial exists only for n>=0
        if (n < 0)
            return 0;

        // base case
        if (n <= 1)
            return 1;

        // else iterate through n and calculate the
        // value
        double digits = 0;
        for (int i=2; i<=n; i++)
            digits += Math.log10(i);

        return (int)(Math.floor(digits)) + 1;
    }

    // Driver code
    public static void main (String[] args)
    {
        System.out.println(findDigits(1));
        System.out.println(findDigits(5));
        System.out.println(findDigits(10));
        System.out.println(findDigits(120));
    }
}

// This code is contributed by Pramod Kumar
```

## 蟒蛇 3

```
# Python3 program to find the
# number of digits in a factorial
import math

# This function receives an integer
# n, and returns the number of
# digits present in n!

def findDigits(n):

    # factorial exists only for n>=0
    if (n < 0):
        return 0;

    # base case
    if (n <= 1):
        return 1;

    # else iterate through n and
    # calculate the value
    digits = 0;
    for i in range(2, n + 1):
        digits += math.log10(i);

    return math.floor(digits) + 1;

# Driver code
print(findDigits(1));
print(findDigits(5));
print(findDigits(10));
print(findDigits(120));

# This code is contributed by mits
```

## C#

```
// A C++ program to find the number
// of digits in a factorial
using System;

class GFG {

    // This function receives an integer
    // n, and returns the number of
    // digits present in n!
    static int findDigits(int n)
    {

        // factorial exists only for n>=0
        if (n < 0)
            return 0;

        // base case
        if (n <= 1)
            return 1;

        // else iterate through n and
        // calculate the value
        double digits = 0;
        for (int i = 2; i <= n; i++)
            digits += Math.Log10(i);

        return (int)Math.Floor(digits) + 1;
    }

    // Driver code
    public static void Main()
    {
        Console.Write(findDigits(1) + "\n");
        Console.Write(findDigits(5) + "\n");
        Console.Write(findDigits(10) + "\n");
        Console.Write(findDigits(120) + "\n");
    }
}

// This code is contributed by
// Smitha Dinesh Semwal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// the number of digits
// in a factorial

// This function receives
// an integer n, and returns
// the number of digits present in n!

function findDigits($n)
{
    // factorial exists only for n>=0
    if ($n < 0)
        return 0;

    // base case
    if ($n <= 1)
        return 1;

    // else iterate through n and
    // calculate the value
    $digits = 0;
    for ($i = 2; $i <= $n; $i++)
        $digits += log10($i);

    return floor($digits) + 1;
}

// Driver code
echo findDigits(1), "\n";
echo findDigits(5), "\n";
echo findDigits(10), "\n";
echo findDigits(120), "\n";

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// A Javascript program to find the number of digits in
// a factorial

// This function receives an integer n, and returns
// the number of digits present in n!
function findDigits(n)
{
    // factorial exists only for n>=0
    if (n < 0)
        return 0;

    // base case
    if (n <= 1)
        return 1;

    // else iterate through n and calculate the
    // value
    let digits = 0;
    for (let i=2; i<=n; i++)
        digits += Math.log10(i);

    return Math.floor(digits) + 1;
}

// Driver code

    document.write(findDigits(1) + "<br>");
    document.write(findDigits(5) + "<br>");
    document.write(findDigits(10) + "<br>");
    document.write(findDigits(120) + "<br>");

//This code is contributed by Mayank Tyagi

</script>
```

**输出:**

```
1
3
7
199
```

在下一集，我们将看到如何进一步优化我们的方法，并降低同一程序的时间复杂性。
本文由 [**阿舒托什·库马尔**](https://www.linkedin.com/in/ashutosh-kumar-9527a7105?trk=nav_responsive_tab_profile) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。