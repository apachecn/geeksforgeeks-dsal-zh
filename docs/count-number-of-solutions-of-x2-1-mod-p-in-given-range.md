# 计算给定范围内 x^2 = 1 (mod p)的解的数量

> 原文:[https://www . geeksforgeeks . org/count-number-of-x2-1-mod-p-in-给定范围/](https://www.geeksforgeeks.org/count-number-of-solutions-of-x2-1-mod-p-in-given-range/)

给定两个整数 n 和 p，求闭区间[1，n]中 x <sup>2</sup> = 1 (mod p)的积分解个数。

**示例:**

```
Input : n = 10, p = 5
Output : 4
There are four integers that satisfy the equation
x2 = 1\. The numbers are 1, 4, 6 and 9.

Input : n = 15, p = 7
Output : 5
There are five integers that satisfy the equation
x2 = 1\. The numbers are 1, 8, 15, 6 and 13\.   
```

一个简单的解决方案是遍历从 1 到 n 的所有数字。对于每个数字，检查它是否满足等式。我们可以避免遍历整个范围。这个想法是基于这样一个事实，如果一个数 x 满足这个方程，那么 x + i*p 形式的所有数也满足这个方程。我们遍历从 1 到 p 的所有数字，对于满足等式的每个数字 x，我们找到 x + i*p 形式的数字计数。要找到计数，我们首先找到给定 x 的最大数字，然后将(最大数字–x)/p 添加到结果中。

下面是这个想法的实现。

## C++

```
// C++ program to count number of values
// that satisfy x^2  = 1 mod p where x lies
// in range [1, n]
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;

int findCountOfSolutions(int n, int p)
{
    // Initialize result
    ll ans = 0;

    // Traverse all numbers smaller than
    // given number p. Note that we don't
    // traverse from 1 to n, but 1 to p
    for (ll x=1; x<p; x++)
    {
        // If x is a solution, then count all
        // numbers of the form x + i*p such
        // that x + i*p is in range [1,n]
        if ((x*x)%p == 1)
        {
            // The largest number in the
            // form of x + p*i in range
            // [1, n]
            ll last = x + p * (n/p);
            if (last > n)
                last -= p;

            // Add count of numbers of the form
            // x + p*i. 1 is added for x itself.
            ans += ((last-x)/p + 1);
        }
    }
    return ans;
}

// Driver code
int main()
{
    ll n = 10, p = 5;
    printf("%lld\n", findCountOfSolutions(n, p));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count
// number of values that
// satisfy x^2 = 1 mod p
// where x lies in range [1, n]
import java.io.*;

class GFG
{
static int findCountOfSolutions(int n,
                                int p)
{
    // Initialize result
    int ans = 0;

    // Traverse all numbers
    // smaller than given
    // number p. Note that
    // we don't traverse from
    // 1 to n, but 1 to p
    for (int x = 1; x < p; x++)
    {
        // If x is a solution,
        // then count all numbers
        // of the form x + i*p
        // such that x + i*p is
        // in range [1,n]
        if ((x * x) % p == 1)
        {
            // The largest number
            // in the form of x +
            // p*i in range [1, n]
            int last = x + p * (n / p);
            if (last > n)
                last -= p;

            // Add count of numbers
            // of the form x + p*i.
            // 1 is added for x itself.
            ans += ((last - x) / p + 1);
        }
    }
    return ans;
}

// Driver code
public static void main (String[] args)
{
    int n = 10;
    int p = 5;
    System.out.println(
               findCountOfSolutions(n, p));
}
}

// This code is contributed by ajit
```

## 蟒蛇 3

```
# Program to count number of
# values that satisfy x^2 = 1
# mod p where x lies in range [1, n]

def findCountOfSolutions(n, p):

    # Initialize result
    ans = 0;

    # Traverse all numbers smaller
    # than given number p. Note
    # that we don't traverse from
    # 1 to n, but 1 to p
    for x in range(1, p):

        # If x is a solution, then
        # count all numbers of the
        # form x + i*p such that
        # x + i*p is in range [1,n]
        if ((x * x) % p == 1):

            # The largest number in the
            # form of x + p*i in range
            # [1, n]
            last = x + p * (n / p);
            if (last > n):
                last -= p;

            # Add count of numbers of
            # the form x + p*i. 1 is
            # added for x itself.
            ans += ((last - x) / p + 1);
    return int(ans);

# Driver code
n = 10;
p = 5;
print(findCountOfSolutions(n, p));

# This code is contributed by mits
```

## C#

```
// C# program to count
// number of values that
// satisfy x^2 = 1 mod p
// where x lies in range [1, n]
using System;

class GFG
{
static int findCountOfSolutions(int n,
                                int p)
{
    // Initialize result
    int ans = 0;

    // Traverse all numbers
    // smaller than given
    // number p. Note that
    // we don't traverse from
    // 1 to n, but 1 to p
    for (int x = 1; x < p; x++)
    {
        // If x is a solution,
        // then count all numbers
        // of the form x + i*p
        // such that x + i*p is
        // in range [1,n]
        if ((x * x) % p == 1)
        {
            // The largest number
            // in the form of x +
            // p*i in range [1, n]
            int last = x + p * (n / p);
            if (last > n)
                last -= p;

            // Add count of numbers
            // of the form x + p*i.
            // 1 is added for x itself.
            ans += ((last - x) / p + 1);
        }
    }
    return ans;
}

// Driver code
static public void Main ()
{
    int n = 10;
    int p = 5;
    Console.WriteLine(
            findCountOfSolutions(n, p));
}
}

// This code is contributed by ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Program to count number of
// values that satisfy x^2 = 1
// mod p where x lies in range [1, n]

function findCountOfSolutions($n, $p)
{
    // Initialize result
    $ans = 0;

    // Traverse all numbers smaller
    // than given number p. Note
    // that we don't traverse from
    // 1 to n, but 1 to p
    for ($x = 1; $x < $p; $x++)
    {
        // If x is a solution, then
        // count all numbers of the
        // form x + i*p such that
        // x + i*p is in range [1,n]
        if (($x * $x) % $p == 1)
        {
            // The largest number in the
            // form of x + p*i in range
            // [1, n]
            $last = $x + $p * ($n / $p);
            if ($last > $n)
                $last -= $p;

            // Add count of numbers of
            // the form x + p*i. 1 is
            // added for x itself.
            $ans += (($last - $x) / $p + 1);
        }
    }
    return $ans;
}

// Driver code
$n = 10;
$p = 5;
echo findCountOfSolutions($n, $p);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Javascript program to count number
// of values that satisfy x^2 = 1 mod p
// where x lies in range [1, n]
function findCountOfSolutions(n, p)
{

    // Initialize result
    let ans = 0;

    // Traverse all numbers smaller
    // than given number p. Note that
    // we don't traverse from 1 to n,
    // but 1 to p
    for(let x = 1; x < p; x++)
    {

        // If x is a solution,
        // then count all numbers
        // of the form x + i*p
        // such that x + i*p is
        // in range [1,n]
        if ((x * x) % p == 1)
        {

            // The largest number
            // in the form of x +
            // p*i in range [1, n]
            let last = x + p * (n / p);

            if (last > n)
                last -= p;

            // Add count of numbers
            // of the form x + p*i.
            // 1 is added for x itself.
            ans += ((last - x) / p + 1);
        }
    }
    return ans;
}

// Driver code
let n = 10;
let p = 5;

document.write(findCountOfSolutions(n, p));

// This code is contributed by susmitakundugoaldanga

</script>
```

**输出:**

```
4
```

本文由 **Shubham Agrawal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。