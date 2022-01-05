# 强大的数字

> 原文:[https://www.geeksforgeeks.org/powerful-number/](https://www.geeksforgeeks.org/powerful-number/)

如果一个数 n 的每一个质因数 p，p <sup>2</sup> 也对其进行除法运算，则称它为幂数。例如:- 36 是一个强大的数字。它可以被 3 和 3 的平方整除，即 9。
前几个强力数字是:
1、4、8、9、16、25、27、32、36、49、64……。
给定一个数字 n，我们的任务是检查这个是否强大。
**例:**

```
Input: 27
Output: YES

Input: 32
Output: YES

Input: 12
Output: NO
```

这个想法是基于这样一个事实，如果一个数 n 是强大的，那么它的所有质因数和它们的平方应该可以被 n 整除。我们[找到给定数](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)的所有质因数。而对于每一个质因数，我们找到了它的最高乘方除以 n，如果我们找到了一个质因数，它的最高乘方是 1，我们返回 false。如果所有质因数的最高除幂大于 1，我们返回真。
以下是上述想法的实现。

## C++

```
// C++ program to find if a number is powerful or not.
#include <bits/stdc++.h>
using namespace std;

// function to check if the number is powerful
bool isPowerful(int n)
{
    // First divide the number repeatedly by 2
    while (n % 2 == 0) {
        int power = 0;
        while (n % 2 == 0) {
            n /= 2;
            power++;
        }

        // If only 2^1 divides n (not higher powers),
        // then return false
        if (power == 1)
            return false;
    }

    // if n is not a power of 2 then this loop will execute
    // repeat above process
    for (int factor = 3; factor <= sqrt(n); factor += 2) {
        // Find highest power of "factor" that divides n
        int power = 0;
        while (n % factor == 0) {
            n = n / factor;
            power++;
        }

        // If only factor^1 divides n (not higher powers),
        // then return false
        if (power == 1)
            return false;
    }

    // n must be 1 now if it is not a prime numenr.
    // Since prime numbers are not powerful, we return
    // false if n is not 1.
    return (n == 1);
}

// Driver program to test above function
int main()
{
    isPowerful(20) ? cout << "YES\n" : cout << "NO\n";
    isPowerful(27) ? cout << "YES\n" : cout << "NO\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find if a
// number is powerful or not.

class GFG {
    // function to check if the
    // number is powerful
    static boolean isPowerful(int n)
    {
        // First divide the number
        // repeatedly by 2
        while (n % 2 == 0) {
            int power = 0;
            while (n % 2 == 0) {
                n /= 2;
                power++;
            }

            // If only 2^1 divides n (not higher powers),
            // then return false
            if (power == 1)
                return false;
        }

        // if n is not a power of 2 then this loop will execute
        // repeat above process
        for (int factor = 3; factor <= Math.sqrt(n); factor += 2) {
            // Find highest power of "factor" that divides n
            int power = 0;
            while (n % factor == 0) {
                n = n / factor;
                power++;
            }

            // If only factor^1 divides n (not higher powers),
            // then return false
            if (power == 1)
                return false;
        }

        // n must be 1 now if it is not a prime numenr.
        // Since prime numbers are not powerful, we return
        // false if n is not 1.
        return (n == 1);
    }

    // Driver code
    public static void main(String[] args)
    {
        if (isPowerful(20))
            System.out.print("YES\n");
        else
            System.out.print("NO\n");
        if (isPowerful(27))
            System.out.print("YES\n");
        else
            System.out.print("NO\n");
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python program to find
# if a number is powerful or not.
import math

# function to check if
# the number is powerful
def isPowerful(n):

    # First divide the number repeatedly by 2
    while (n % 2 == 0):

        power = 0
        while (n % 2 == 0):

            n = n//2
            power = power + 1

        # If only 2 ^ 1 divides
        # n (not higher powers),
        # then return false
        if (power == 1):
            return False

    # if n is not a power of 2
    # then this loop will execute
    # repeat above process
    for factor in range(3, int(math.sqrt(n))+1, 2):

        # Find highest power of
        # "factor" that divides n
        power = 0
        while (n % factor == 0):

            n = n//factor
            power = power + 1

        # If only factor ^ 1 divides
        # n (not higher powers),
        # then return false
        if (power == 1):
            return false

     # n must be 1 now if it
     # is not a prime numenr.
     # Since prime numbers are
     # not powerful, we return
     # false if n is not 1.
    return (n == 1)

# Driver code

print("YES" if isPowerful(20) else "NO")
print("YES" if isPowerful(27) else "NO")

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to find if a
// number is powerful or not.
using System;

class GFG {

    // function to check if the
    // number is powerful
    static bool isPowerful(int n)
    {
        // First divide the number
        // repeatedly by 2
        while (n % 2 == 0) {
            int power = 0;
            while (n % 2 == 0) {
                n /= 2;
                power++;
            }

            // If only 2^1 divides n
            // (not higher powers),
            // then return false
            if (power == 1)
                return false;
        }

        // if n is not a power of 2 then
        // this loop will execute repeat
        // above process
        for (int factor = 3; factor <= Math.Sqrt(n); factor += 2) {
            // Find highest power of "factor"
            // that divides n
            int power = 0;
            while (n % factor == 0) {
                n = n / factor;
                power++;
            }

            // If only factor^1 divides n
            // (not higher powers), then
            // return false
            if (power == 1)
                return false;
        }

        // n must be 1 now if it is not
        // a prime numenr.
        // Since prime numbers are not
        // powerful, we return false if
        // n is not 1.
        return (n == 1);
    }

    // Driver code
    public static void Main()
    {
        if (isPowerful(20))
            Console.WriteLine("YES");
        else
            Console.WriteLine("NO");

        if (isPowerful(27))
            Console.WriteLine("YES");
        else
            Console.WriteLine("NO");
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find if a
// number is powerful or not

// function to check if
// the number is powerful
function isPowerful($n)
{
    // First divide the
    // number repeatedly by 2
    while ($n % 2 == 0)
    {
        $power = 0;
        while ($n % 2 == 0)
        {
            $n /= 2;
            $power++;
        }

        // If only 2^1 divides
        // n (not higher powers),
        // then return false
        if ($power == 1)
        return false;
    }

    // if n is not a power of 2
    // then this loop will execute
    // repeat above process
    for ($factor = 3;
         $factor <= sqrt($n);
         $factor += 2)
    {
        // Find highest power of
        // "factor" that divides n
        $power = 0;
        while ($n % $factor == 0)
        {
            $n = $n / $factor;
            $power++;
        }

        // If only factor^1 divides
        // n (not higher powers),
        // then return false
        if ($power == 1)
        return false;
    }

    // n must be 1 now if it is
    // not a prime number. Since
    // prime numbers are not powerful,
    // we return false if n is not 1.
    return ($n == 1);
}

// Driver Code
$d = isPowerful(20) ?
            "YES\n" :
              "NO\n";
    echo $d;
$d = isPowerful(27) ?
            "YES\n" :
              "NO\n";
    echo $d;

// This code is contributed by ajit.    
?>
```

## java 描述语言

```
<script>

// Javascript program to find if a
// number is powerful or not.

    // function to check if the
    // number is powerful
    function isPowerful(n)
    {
        // First divide the number
        // repeatedly by 2
        while (n % 2 == 0) {
            let power = 0;
            while (n % 2 == 0) {
                n /= 2;
                power++;
            }

            // If only 2^1 divides n (not higher powers),
            // then return false
            if (power == 1)
                return false;
        }

        // if n is not a power of 2 then this loop will execute
        // repeat above process
        for (let factor = 3; factor <= Math.sqrt(n); factor += 2) {
            // Find highest power of "factor" that divides n
            let power = 0;
            while (n % factor == 0) {
                n = n / factor;
                power++;
            }

            // If only factor^1 divides n (not higher powers),
            // then return false
            if (power == 1)
                return false;
        }

        // n must be 1 now if it is not a prime numenr.
        // Since prime numbers are not powerful, we return
        // false if n is not 1.
        return (n == 1);
    }

// Driver code to test above methods

        if (isPowerful(20))
           document.write("YES" + "<br>");
        else
            document.write("NO" + "<br>");
        if (isPowerful(27))
            document.write("YES" + "<br>");
        else
            document.write("NO" + "<br>");

// This code is contributed by avijitmondal1998.
</script>
```

**输出:**

```
NO
YES
```

**参考文献:**
[【https://en.wikipedia.org/wiki/Powerful_number】](https://en.wikipedia.org/wiki/Powerful_number)
本文由 [**Harsh Agarwal**](https://www.facebook.com/harsh.agarwal.16752) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。