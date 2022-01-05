# 求 x 和 y 的最小值，使得 ax–by = 0

> 原文:[https://www . geeksforgeeks . org/find-x 和 y 的最小值，即 ax 乘 0/](https://www.geeksforgeeks.org/find-smallest-values-of-x-and-y-such-that-ax-by-0/)

给定代表“ax–by = 0”中系数的两个值‘a’和‘b’，找到满足等式的 x 和 y 的最小值。也可以假设 x > 0，y > 0，a > 0，b > 0。

```
Input: a = 25, b = 35
Output: x = 7, y = 5
```

A **简单解法**是从 1，1 开始尝试 x 和 y 的每一个可能值，当方程满足时停止。
一个**直接解决方案**是使用最小公倍数(LCM)。“a”和“b”的 LCM 代表可以使两边相等的最小值。我们可以用下面的公式找到 LCM。

```
   LCM(a, b) = (a * b) / GCD(a, b) 
```

最大公约数(GCD)可以使用[欧几里德算法](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/)来计算。

## C++

```
// C++ program to find the smallest values of x and y that
// satisfy "ax - by = 0"
#include <iostream>
using namespace std;

// To find GCD using Eculcid's algorithm
int gcd(int a, int b)
{
    if (b == 0)
        return a;
    return (gcd(b, a % b));
}

// Prints smallest values of x and y that
// satisfy "ax - by = 0"
void findSmallest(int a, int b)
{
    // Find LCM
    int lcm = (a * b) / gcd(a, b);

    cout << "x = " << lcm / a
         << "\ny = " << lcm / b;
}

// Driver program
int main()
{
    int a = 25, b = 35;
    findSmallest(a, b);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the smallest values of
// x and y that satisfy "ax - by = 0"
class GFG {

    // To find GCD using Eculcid's algorithm
    static int gcd(int a, int b)
    {

        if (b == 0)
            return a;
        return (gcd(b, a % b));
    }

    // Prints smallest values of x and y that
    // satisfy "ax - by = 0"
    static void findSmallest(int a, int b)
    {

        // Find LCM
        int lcm = (a * b) / gcd(a, b);

        System.out.print("x = " + lcm / a
                         + "\ny = " + lcm / b);
    }

    // Driver code
    public static void main(String[] args)
    {
        int a = 25, b = 35;
        findSmallest(a, b);
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python program to find the
# smallest values of x and y that
# satisfy "ax - by = 0"

# To find GCD using Eculcid's algorithm
def gcd(a, b):
    if (b == 0):
        return a
    return(gcd(b, a % b))

# Prints smallest values of x and y that
# satisfy "ax - by = 0"
def findSmallest(a, b):

    # Find LCM
    lcm = (a * b)/gcd(a, b)
    print("x =", lcm / a, "\ny = ", lcm / b)

# Driver code
a = 25
b = 35
findSmallest(a, b)

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to find the smallest
// values of x and y that
// satisfy "ax - by = 0"
using System;

class GFG {

    // To find GCD using
    // Eculcid's algorithm
    static int gcd(int a, int b)
    {

        if (b == 0)
            return a;
        return (gcd(b, a % b));
    }

    // Prints smallest values of x and
    // y that satisfy "ax - by = 0"
    static void findSmallest(int a, int b)
    {

        // Find LCM
        int lcm = (a * b) / gcd(a, b);

        Console.Write("x = " + lcm / a + "\ny = " + lcm / b);
    }

    // Driver code
    public static void Main()
    {
        int a = 25, b = 35;
        findSmallest(a, b);
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the
// smallest values of x
// and y that satisfy
// "ax - by = 0"

// To find GCD using
// Eculcid's algorithm
function gcd($a, $b)
{
    if ($b == 0)
    return $a;
    return(gcd($b, $a % $b));
}

// Prints smallest values
// of x and y that
// satisfy "ax - by = 0"
function findSmallest($a, $b)
{

    // Find LCM
    $lcm = ($a * $b) / gcd($a, $b);

    echo "x = ", $lcm/$a, "\ny = ", $lcm/$b;
}

    // Driver Code
    $a = 25;
    $b = 35;
    findSmallest($a, $b);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

    // Javascript program to find the smallest
    // values of x and y that
    // satisfy "ax - by = 0"

    // To find GCD using
    // Eculcid's algorithm
    function gcd(a, b)
    {

        if (b == 0)
            return a;
        return (gcd(b, a % b));
    }

    // Prints smallest values of x and
    // y that satisfy "ax - by = 0"
    function findSmallest(a, b)
    {

        // Find LCM
        let lcm = parseInt((a * b) / gcd(a, b), 10);

        document.write("x = " + parseInt(lcm / a, 10) +
        "</br>y = " + parseInt(lcm / b, 10));
    }

    let a = 25, b = 35;
      findSmallest(a, b);

</script>
```

**输出:**

```
x = 7
y = 5
```

**以上 findSmallest()的代码可以简化:**

```
Since ax - by = 0,
ax = by, which means x/y = b/a
So we can calculate gcd and directly do as -

Value of x = b / gcd;
Value of y = a / gcd; 
```

## C

```
// Prints smallest values of x and y that
// satisfy "ax - by = 0"
void findSmallest(int a, int b)
{
    // Find GCD
    int g = gcd(a, b);

    cout << "x = " << b / g
         << "\ny = " << a / g;
}
```

本文由**阿卡斯·萨其德瓦**供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如发现任何不正确的地方，请写评论，或者您想分享更多关于上述话题的信息