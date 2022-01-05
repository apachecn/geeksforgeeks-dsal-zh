# 阶乘中至少有 n 位数的最小数

> 原文:[https://www . geeksforgeeks . org/最小数-最小 n 位数-阶乘/](https://www.geeksforgeeks.org/smallest-number-least-n-digits-factorial/)

给定一个数 n，任务是找出阶乘至少包含 n 位的最小数。
**例:**

```
Input : n = 1
Output : 0
0! = 1, hence it has 1 digit.

Input : n = 2
Output : 4
4! = 24 and 3! = 6, hence 4 is 
the smallest number having 2 
digits in its factorial

Input : n = 5
Output : 8
```

在文章[计算一个数的阶乘](https://www.geeksforgeeks.org/count-digits-factorial-set-2/)中的位数时，我们讨论了如何有效地找到阶乘中的位数。
我们用下面的公式求数字的个数

```
Kamenetsky’s formula approximates the number
of digits in a factorial by :
f(x) = log10(((n/e)n) * sqrt(2*pi*n))

Thus, we can pretty easily use the property of logarithms to ,
f(x) = n*log10((n/e)) + log10(2*pi*n)/2 
```

现在我们需要确定一个区间，在这个区间内我们可以找到一个至少有 n 位数的阶乘。以下是一些观察结果:

*   对于一个大数，我们总是可以说它的阶乘比数本身有更多的位数。例如，阶乘 100 有 158 个大于 100 的数字。
*   然而，对于较小的数字，情况可能并非如此。例如，阶乘 8 只有 5 位数字，小于 8。事实上，多达 21 个国家遵循这一趋势。

因此如果我们从 0 开始搜索！去 n！要找到至少有 n 位数的结果，我们将无法找到较小数字的结果。
例如，假设 n = 5，现在当我们在[0，n]中搜索时，我们可以获得的最大位数是 3，(在 5 中找到！= 120).然而，如果我们在[0，2*n] (0 到 10)中搜索，我们可以找到 8！有 5 位数。
因此，如果我们可以搜索从 0 到 2*n 的所有阶乘，那么总会有一个数字 k，它的阶乘中至少有 n 个数字。(建议读者自己去尝试弄清楚这个事实)

```
We can say conclude if we have to find a number k,
such that k! has at least n digits, we can be sure
that k lies in [0,2*n]

i.e., 0<= k <= 2*n
```

因此，我们可以做一个 0 到 2*n 之间的二分搜索法运算，找出至少有 n 位数的最小数。

## C++

```
// A C++ program to find the smallest number
// having at least n digits in factorial
#include <bits/stdc++.h>
using namespace std;

// Returns the number of digits present in n!
int findDigitsInFactorial(int n)
{
    // factorial of -ve number doesn't exists
    if (n < 0)
        return 0;

    // base case
    if (n <= 1)
        return 1;

    // Use Kamenetsky formula to calculate the
    // number of digits
    double x = ((n*log10(n/M_E)+log10(2*M_PI*n)/2.0));

    return floor(x)+1;
}

// This function receives an integer n and returns
// an integer whose factorial has at least n digits
int findNum(int n)
{
    // (2*n)! always has more digits than n
    int low = 0, hi = 2*n;

    // n <= 0
    if (n <= 0)
        return -1;

    // case for n = 1
    if (findDigitsInFactorial(low) == n)
        return low;

    // now use binary search to find the number
    while (low <= hi)
    {
        int mid = (low+hi) / 2;

        // if (mid-1)! has lesser digits than n
        // and mid has n or more then mid is the
        // required number
        if (findDigits(mid) >= n && findDigits(mid-1)<n)
            return mid;

        else if (findDigits(mid) < n)
            low = mid+1;

        else
            hi = mid-1;
    }
    return low;
}

// Driver program to check the above functions
int main()
{
    cout << findNum(1) << endl;
    cout << findNum(2) << endl;
    cout << findNum(5) << endl;
    cout << findNum(24) << endl;
    cout << findNum(100) << endl;
    cout << findNum(1221) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java program to find the
// smallest number having at
// least n digits in factorial
class GFG
{
// Returns the number of
// digits present in n!
static int findDigitsInFactorial(int n)
{
    // factorial of -ve number
    // doesn't exists
    if (n < 0)
        return 0;

    // base case
    if (n <= 1)
        return 1;

    // Use Kamenetsky formula to
    // calculate the number of digits
    double x = ((n * Math.log10(n / Math.E) +
                     Math.log10(2 * Math.PI * n) / 2.0));

    return (int)(Math.floor(x) + 1);
}

// This function receives an integer
// n and returns an integer whose
// factorial has at least n digits
static int findNum(int n)
{
    // (2*n)! always has
    // more digits than n
    int low = 0, hi = 2 * n;

    // n <= 0
    if (n <= 0)
        return -1;

    // case for n = 1
    if (findDigitsInFactorial(low) == n)
        return low;

    // now use binary search
    // to find the number
    while (low <= hi)
    {
        int mid = (low + hi) / 2;

        // if (mid-1)! has lesser digits
        // than n and mid has n or more
        // then mid is the required number
        if (findDigitsInFactorial(mid) >= n &&
            findDigitsInFactorial(mid - 1) < n)
            return mid;

        else if (findDigitsInFactorial(mid) < n)
            low = mid + 1;

        else
            hi = mid - 1;
    }
    return low;
}

// Driver Code
public static void main(String[] args)
{
    System.out.println(findNum(1));
    System.out.println(findNum(2));
    System.out.println(findNum(5));
    System.out.println(findNum(24));
    System.out.println(findNum(100));
    System.out.println(findNum(1221));
}
}

// This Code is Contributed by mits
```

## 蟒蛇 3

```
# Python3 program to find the
# smallest number
# having at least n digits
# in factorial

import math

# Returns the number of digits
# present in n!
def findDigitsInFactorial(n):

    # factorial of -ve number
    # doesn't exists
    if (n < 0):
        return 0

    # base case
    if (n <= 1):
        return 1

    # Use Kamenetsky formula to calculate the
    # number of digits
    M_E=2.7182818284590452354
    M_PI=3.14159265358979323846
    x = ((n*math.log10(n/M_E)+math.log10(2*M_PI*n)/2.0))

    return int(math.floor(x)+1)

# This function receives an
# integer n and returns
# an integer whose factorial has
# at least n digits
def findNum(n):

    # (2*n)! always has more
    # digits than n
    low = 0
    hi = 2*n

    # n <= 0
    if (n <= 0):
        return -1

    # case for n = 1
    if (findDigitsInFactorial(low) == n):
        return int(round(low))

    # now use binary search to
    # find the number
    while (low <= hi):
        mid = int((low+hi) / 2)

        # if (mid-1)! has lesser digits than n
        # and mid has n or more then mid is the
        # required number
        if ((findDigitsInFactorial(mid) >= n and
            findDigitsInFactorial(mid-1)<n)):
            return int(round(mid))

        elif (findDigitsInFactorial(mid) < n):
            low = mid+1

        else:
            hi = mid-1

    return int(round(low))

# Driver code
if __name__=='__main__':
    print(findNum(1));
    print(findNum(2));
    print(findNum(5));
    print(findNum(24));
    print(findNum(100));
    print(findNum(1221));

# this code is contributed by
# mits
```

## C#

```
// A C# program to find the
// smallest number having at
// least n digits in factorial
using System;

class GFG
{

// Returns the number of
// digits present in n!
static int findDigitsInFactorial(int n)
{
    // factorial of -ve number
    // doesn't exists
    if (n < 0)
        return 0;

    // base case
    if (n <= 1)
        return 1;

    // Use Kamenetsky formula to
    // calculate the number of digits
    double x = ((n * Math.Log10(n / Math.E) +
                     Math.Log10(2 * Math.PI * n) / 2.0));

    return (int)(Math.Floor(x) + 1);
}

// This function receives an integer
// n and returns an integer whose
// factorial has at least n digits
static int findNum(int n)
{
    // (2*n)! always has
    // more digits than n
    int low = 0, hi = 2 * n;

    // n <= 0
    if (n <= 0)
        return -1;

    // case for n = 1
    if (findDigitsInFactorial(low) == n)
        return low;

    // now use binary search
    // to find the number
    while (low <= hi)
    {
        int mid = (low + hi) / 2;

        // if (mid-1)! has lesser digits
        // than n and mid has n or more
        // then mid is the required number
        if (findDigitsInFactorial(mid) >= n &&
            findDigitsInFactorial(mid - 1) < n)
            return mid;

        else if (findDigitsInFactorial(mid) < n)
            low = mid + 1;

        else
            hi = mid - 1;
    }
    return low;
}

// Driver Code
static public void Main ()
{
    Console.WriteLine(findNum(1));
    Console.WriteLine(findNum(2));
    Console.WriteLine(findNum(5));
    Console.WriteLine(findNum(24));
    Console.WriteLine(findNum(100));
    Console.WriteLine(findNum(1221));
}
}

// This code is contributed by akt_mit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A PHP program to find the smallest number
// having at least n digits in factorial

// Returns the number of digits
// present in n!
function findDigitsInFactorial($n)
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
                log10(2 * M_PI * $n) / 2.0));

    return (int)(floor($x) + 1);
}

// This function receives an integer
// n and returns an integer whose
// factorial has at least n digits
function findNum($n)
{
    // (2*n)! always has more
    // digits than n
    $low = 0;
    $hi = 2 * $n;

    // n <= 0
    if ($n <= 0)
        return -1;

    // case for n = 1
    if (findDigitsInFactorial($low) == $n)
        return (int)round($low);

    // now use binary search to
    // find the number
    while ($low <= $hi)
    {
        $mid = ($low + $hi) / 2;

        // if (mid-1)! has lesser digits
        // than n and mid has n or more
        // then mid is the required number
        if (findDigitsInFactorial($mid) >= $n &&
            findDigitsInFactorial($mid - 1) < $n)
            return (int)round($mid);

        else if (findDigitsInFactorial($mid) < $n)
            $low = $mid + 1;

        else
            $hi = $mid - 1;
    }
    return (int)round($low);
}

// Driver Code
echo findNum(1) . "\n";
echo findNum(2) . "\n";
echo findNum(5) . "\n";
echo findNum(24) . "\n";
echo findNum(100) . "\n";
echo findNum(1221) . "\n";

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// A Javascript program to find the smallest number
// having at least n digits in factorial

// Returns the number of digits present in n!
function findDigitsInFactorial(n)
{
    // factorial of -ve number doesn't exists
    if (n < 0)
        return 0;

    // base case
    if (n <= 1)
        return 1;

    // Use Kamenetsky formula to calculate the
    // number of digits
    let x = (n*Math.log10(n/Math.E)+Math.log10(2*Math.PI*n)/2.0);

    return Math.floor(x)+1;
}

// This function receives an integer n and returns
// an integer whose factorial has at least n digits
function findNum(n)
{
    // (2*n)! always has more digits than n
    let low = 0, hi = 2*n;

    // n <= 0
    if (n <= 0)
        return -1;

    // case for n = 1
    if (findDigitsInFactorial(low) == n)
        return low;

    // now use binary search to find the number
    while (low <= hi)
    {
        let mid = (low+hi) / 2;

        // if (mid-1)! has lesser digits than n
        // and mid has n or more then mid is the
        // required number
        if (findDigitsInFactorial(mid) >= n && findDigitsInFactorial(mid-1)<n)
            return Math.floor(mid);

        else if (findDigitsInFactorial(mid) < n)
            low = mid+1;

        else
            hi = mid-1;
    }
    return low;
}

// Driver program to check the above functions

    document.write(findNum(1) + "<br>");
    document.write(findNum(2) + "<br>");
    document.write(findNum(5) + "<br>");
    document.write(findNum(24) + "<br>");
    document.write(findNum(100) + "<br>");
    document.write(findNum(1221) + "<br>");

// This code is contributed by Mayank Tyagi

</script>
```

**输出:**

```
0
4
8
24
70
532
```

**复杂度分析**
如果我们忽略对数函数的复杂度，二分搜索法的复杂度是 O(log(2*n))。因此，整体复杂性为 0(对数(n))。
本文由[T5】Ashutosh Kumar](https://in.linkedin.com/in/ashutosh-kumar-9527a7105)投稿如果你喜欢 GeeksforGeeks 并且愿意投稿，也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。