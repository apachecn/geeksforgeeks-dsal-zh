# 分子和分母之和等于给定数的最大真分数

> 原文:[https://www . geesforgeks . org/最大-适当-分数-总和-分子-分母-相等-给定-数字/](https://www.geeksforgeeks.org/largest-proper-fraction-sum-numerator-denominator-equal-given-number/)

给我们提供一个数 n。求最大的适当分数 a/b，使得 a + b = N。下面是分数的约束。

1.  如果 a
2.  分子和分母之和等于一个给定的数，可以有多个适当的分数。主要任务是找到具有最大浮点值的分数。

**例:**

```
Input : N = 3
Output : 1 2

Input : N = 12
Output : 5 7
Explanation: In the second example N = 12
Possible a and b's are: 1 11 
                        5 7
But clearly 5/7 (=0.71..) is greater than 
1/11 (=0.09..). Hence answer for N = 12 
is 5 7\.   
```

这个问题的解决方案比算法更直观。
仔细考虑以下几点，理解后面给出的公式:

*   如果分子尽可能大，分母尽可能小，则分数具有最大值。
*   这里的约束是分子不能大于分母的事实，它们的总和应该等于 n。

记住这两点，我们可以得到这样一个事实:这个问题的答案将是天花板(n/2)-1 和地板(n/2)+1。
现在这个解将永远适用于奇数 N 和所有(N/2)为偶数的偶数 N。这是因为这两种情况总是会产生与上述公式相同的结果。
现在考虑下面的例子:
N = 10
天花板(10/2)-1 = 4
地板(10/2)+1 = 6
显然 4 和 6 是错误的答案，因为它们不是同频。正确答案是 3 和 7。
因此，对于奇数(N/2)的偶数 N，公式变为上限(n/2)-2 和下限(n/2)+2。

## C++

```
// CPP program to find the largest fraction
// a/b such that a+b is equal to given number
// and a < b.
#include <iostream>
#include <cmath>
using namespace std;

void solve(int n)
{
    // Calculate N/2;
    float a = (float)n / 2;

    // Check if N is odd or even
    if (n % 2 != 0)

        // If N is odd answer will be
        // ceil(n/2)-1 and floor(n/2)+1
        cout << ceil(a) - 1 << " "
             << floor(a) + 1 << endl;
    else {

        // If N is even check if N/2 i.e a
        // is even or odd
        if ((int)a % 2 == 0) {

            // If N/2 is even apply the
            // previous formula
            cout << ceil(a) - 1 << " "
                 << floor(a) + 1 << endl;
        }

        else {

            // If N/2 is odd answer will be
            // ceil(N/2)-2 and floor(N/2)+2
            cout << ceil(a) - 2 << " "
                 << floor(a) + 2 << endl;
        }
    }
}

// driver function
int main()
{
    int n = 34;
    solve(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the
// largest fraction a/b
// such that a+b is equal
// to given number and a < b.

class GFG
{
public static void solve(int n)
{
    // Calculate N/2;
    double a = n / 2;

    // Check if N is
    // odd or even
    if (n % 2 != 0)
    {
        // If N is odd answer
        // will be ceil(n/2)-1
        // and floor(n/2)+1
        System.out.println((Math.ceil(a) - 1) +
                         " " + (Math.floor(a) + 1));
    }
    else
    {

        // If N is even check
        // if N/2 i.e a
        // is even or odd
        if ((int)(a) % 2 == 0)
        {

            // If N/2 is even apply
            // the previous formula
            System.out.println((Math.ceil(a) - 1) +
                             " " + (Math.floor(a) + 1));
        }

        else
        {
            // If N/2 is odd answer
            // will be ceil(N/2)-2
            // and floor(N/2)+2
            System.out.println((Math.ceil(a) - 2) +
                             " " + (Math.floor(a) + 2));
        }
    }
}

// Driver code
public static void main(String[] args)
{
    int n = 34;
    solve(n);
}
}

// This code is contributed
// by mits
```

## 蟒蛇 3

```
# Python3 program to find
# the largest fraction a/b
# such that a+b is equal to
# given number and a < b.
import math

def solve(n):

    # Calculate N/2;
    a = float(n / 2);

    # Check if N is odd or even
    if (n % 2 != 0):

        # If N is odd answer
        # will be ceil(n/2)-1
        # and floor(n/2)+1
        print((math.ceil(a) - 1),
              (math.floor(a) + 1));
    else:

        # If N is even check if N/2
        # i.e a is even or odd
        if (a % 2 == 0):

            # If N/2 is even apply
            # the previous formula
            print((math.ceil(a) - 1),
                  (math.floor(a) + 1));

        else:

            # If N/2 is odd answer
            # will be ceil(N/2)-2
            # and floor(N/2)+2
            print((math.ceil(a) - 2),
                  (math.floor(a) + 2));

# Driver Code
n = 34;
solve(n);

# This code is contributed by mits
```

## C#

```
// C# program to find the
// largest fraction a/b
// such that a+b is equal
// to given number and a < b.
using System;
class GFG
{
public static void solve(int n)
{
    // Calculate N/2;
    double a = n / 2;

    // Check if N is
    // odd or even
    if (n % 2 != 0)
    {
        // If N is odd answer
        // will be ceil(n/2)-1
        // and floor(n/2)+1
        Console.WriteLine((Math.Ceiling(a) - 1) +
                           " " + (Math.Floor(a) + 1));
    }
    else
    {

        // If N is even check
        // if N/2 i.e a
        // is even or odd
        if ((int)(a) % 2 == 0)
        {

            // If N/2 is even apply
            // the previous formula
            Console.WriteLine((Math.Ceiling(a) - 1) +
                               " " + (Math.Floor(a) + 1));
        }

        else
        {
            // If N/2 is odd answer
            // will be ceil(N/2)-2
            // and floor(N/2)+2
            Console.WriteLine((Math.Ceiling(a) - 2) +
                               " " + (Math.Floor(a) + 2));
        }
    }
}

// Driver code
public static void Main()
{
    int n = 34;
    solve(n);
}
}

// This code is contributed
// by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the largest
// fraction a/b such that a+b is
// equal to given number and a < b.

function solve($n)
{

    // Calculate N/2;
    $a = (float)$n / 2;

    // Check if N is odd or even
    if ($n % 2 != 0)

        // If N is odd answer will
        // be ceil(n/2)-1 and
        // floor(n/2)+1
        echo ceil($a) - 1, " ",
            floor($a) + 1, "\n";
    else {

        // If N is even check if N/2
        // i.e a is even or odd
        if ($a % 2 == 0) {

            // If N/2 is even apply
            //  the previous formula
            echo ceil($a) - 1, " ",
                floor($a) + 1, "\n";
        }

        else {

            // If N/2 is odd answer
            // will be ceil(N/2)-2
            // and floor(N/2)+2
            echo ceil($a) - 2, " ",
               floor($a) + 2, "\n";
        }
    }
}

// driver function
    $n = 34;
    solve($n);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

    // Javascript program to find the
    // largest fraction a/b
    // such that a+b is equal
    // to given number and a < b.

    function solve(n)
    {
        // Calculate N/2;
        let a = n / 2;

        // Check if N is
        // odd or even
        if (n % 2 != 0)
        {
            // If N is odd answer
            // will be ceil(n/2)-1
            // and floor(n/2)+1
            document.write((Math.ceil(a) - 1) +
                     " " + (Math.floor(a) + 1));
        }
        else
        {

            // If N is even check
            // if N/2 i.e a
            // is even or odd
            if (parseInt(a, 10) % 2 == 0)
            {

                // If N/2 is even apply
                // the previous formula
                document.write((Math.ceil(a) - 1) +
                            " " + (Math.floor(a) + 1));
            }

            else
            {
                // If N/2 is odd answer
                // will be ceil(N/2)-2
                // and floor(N/2)+2
                document.write((Math.ceil(a) - 2) +
                        " " + (Math.floor(a) + 2));
            }
        }
    }

    let n = 34;
    solve(n);

</script>
```

**输出:**

```
15 19
```

本文由**vinet Joshi**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。