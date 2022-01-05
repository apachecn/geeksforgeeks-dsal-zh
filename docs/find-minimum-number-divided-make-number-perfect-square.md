# 求最小的待除数，使一个数成为一个完美的正方形

> 原文:[https://www . geesforgeks . org/find-最小数-除法-生成数-完美平方/](https://www.geeksforgeeks.org/find-minimum-number-divided-make-number-perfect-square/)

给定正整数 **n** 。找出除以 n 的最小数，使其成为[完美正方形](https://en.wikipedia.org/wiki/Perfect_square)。
**例:**

```
Input : n = 50
Output : 2
By Dividing n by 2, we get which is a perfect square.

Input : n = 6
Output : 6
By Dividing n by 6, we get which is a perfect square.

Input : n = 36
Output : 1
```

如果所有质因数出现偶数次，那么一个数就是完美平方。其思想是求 n 的素因子，求每个素因子的幂。现在，求幂为奇数的所有质因数并相乘。乘法的结果就是答案。

## C++

```
// C++ program to find minimum number which divide n
// to make it a perfect square.
#include<bits/stdc++.h>
using namespace std;

// Return the minimum number to be divided to make
// n a perfect square.
int findMinNumber(int n)
{
    int count = 0, ans = 1;

    // Since 2 is only even prime, compute its
    // power separately.
    while (n%2 == 0)
    {
        count++;
        n /= 2;
    }

    // If count is odd, it must be removed by dividing
    // n by prime number.
    if (count%2)
        ans *= 2;

    for (int i = 3; i <= sqrt(n); i += 2)
    {
        count = 0;
        while (n%i == 0)
        {
            count++;
            n /= i;
        }

        // If count is odd, it must be removed by
        // dividing n by prime number.
        if (count%2)
            ans *= i;
    }

    if (n > 2)
        ans *= n;

    return ans;
}

// Driven Program
int main()
{
    int n = 72;
    cout << findMinNumber(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum number
// which divide n to make it a perfect square.

class GFG
{
    // Return the minimum number to be
    // divided to make n a perfect square.
    static int findMinNumber(int n)
    {
        int count = 0, ans = 1;

        // Since 2 is only even prime,
        // compute its power separately.
        while (n % 2 == 0)
        {
            count++;
            n /= 2;
        }

        // If count is odd, it must be removed by dividing
        // n by prime number.
        if (count % 2 == 1)
            ans *= 2;

        for (int i = 3; i <= Math.sqrt(n); i += 2)
        {
            count = 0;
            while (n % i == 0)
            {
                count++;
                n /= i;
            }

            // If count is odd, it must be removed by
            // dividing n by prime number.
            if (count % 2 == 1)
                ans *= i;
        }

        if (n > 2)
            ans *= n;

        return ans;
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 72;
        System.out.println(findMinNumber(n));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python program to find
# minimum number which
# divide n to make it a
# perfect square.
import math

# Return the minimum
# number to be divided
# to make n a perfect
# square.
def findMinNumber(n):
    count = 0
    ans = 1

    # Since 2 is only
    # even prime, compute
    # its power separately.
    while n % 2 == 0:
        count += 1
        n //= 2

    # If count is odd,
    # it must be removed
    # by dividing n by
    # prime number.
    if count % 2 is not 0:
        ans *= 2

    for i in range(3, (int)(math.sqrt(n)) + 1, 2):
        count = 0
        while n % i == 0:
            count += 1
            n //= i

        # If count is odd, it
        # must be removed by
        # dividing n by prime
        # number.
        if count % 2 is not 0:
            ans *= i

    if n > 2:
        ans *= n

    return ans

# Driver Code
n = 72
print(findMinNumber(n))

# This code is contributed
# by Sanjit_Prasad.
```

## C#

```
// C# program to find minimum
// number which divide n to
// make it a perfect square.
using System;

class GFG
{

    // Return the minimum number
    // to be divided to make
    // n a perfect square.
    static int findMinNumber(int n)
    {
        int count = 0, ans = 1;

        // Since 2 is only even prime,
        // compute its power separately.
        while (n % 2 == 0)
        {
            count++;
            n /= 2;
        }

        // If count is odd, it must
        // be removed by dividing
        // n by prime number.
        if (count % 2 == 1)
            ans *= 2;

        for (int i = 3; i <= Math.Sqrt(n);
                                  i += 2)
        {
            count = 0;
            while (n % i == 0)
            {
                count++;
                n /= i;
            }

            // If count is odd, it must
            // be removed by dividing n
            // by prime number.
            if (count % 2 == 1)
                ans *= i;
        }

        if (n > 2)
            ans *= n;

        return ans;
    }

    // Driver code
    public static void Main ()
    {
        int n = 72;
        Console.WriteLine(findMinNumber(n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum
// number which divide n
// to make it a perfect square.

// Return the minimum number
// to be divided to make
// n a perfect square.
function findMinNumber($n)
{
    $count = 0;
    $ans = 1;

    // Since 2 is only
    // even prime,
    // compute its
    // power separately.
    while ($n % 2 == 0)
    {
        $count++;
        $n /= 2;
    }

    // If count is odd,
    // it must be removed
    // by dividing n by
    // prime number.
    if ($count % 2)
        $ans *= 2;

    for ($i = 3; $i <= sqrt($n); $i += 2)
    {
        $count = 0;
        while ($n % $i == 0)
        {
            $count++;
            $n /= $i;
        }

        // If count is odd,
        // it must be removed
        // by dividing n by
        // prime number.
        if ($count % 2)
            $ans *= $i;
    }

    if ($n > 2)
        $ans *= $n;

    return $ans;
}

    // Driver Code
    $n = 72;
    echo findMinNumber($n), "\n";

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>

// Javascript program to find minimum
// number which divide n
// to make it a perfect square.

// Return the minimum number
// to be divided to make
// n a perfect square.
function findMinNumber(n)
{
    let count = 0;
    let ans = 1;

    // Since 2 is only
    // even prime,
    // compute its
    // power separately.
    while (n % 2 == 0)
    {
        count++;
        n /= 2;
    }

    // If count is odd,
    // it must be removed
    // by dividing n by
    // prime number.
    if (count % 2)
        ans *= 2;

    for (let i = 3; i <= Math.sqrt(n); i += 2)
    {
        count = 0;
        while (n % i == 0)
        {
            count++;
            n /= i;
        }

        // If count is odd,
        // it must be removed
        // by dividing n by
        // prime number.
        if (count % 2)
            ans *= i;
    }

    if (n > 2)
        ans *= n;

    return ans;
}

    // Driver Code
    let n = 72;
    document.write(findMinNumber(n) + "\n");

// This code is contributed by _saurabh_jaiswal.

</script>
```

**输出:**

```
2
```

本文由 [**Anuj Chauhan**](https://www.facebook.com/anuj0503) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。