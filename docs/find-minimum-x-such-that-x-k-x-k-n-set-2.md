# 求最小值 x，使得(x % k)*(x/k)= n | Set-2

> 原文:[https://www . geesforgeks . org/find-minimum-x-so-x-k-x-k-n-set-2/](https://www.geeksforgeeks.org/find-minimum-x-such-that-x-k-x-k-n-set-2/)

给定两个正整数 n 和 k，求最小正整数 x，使得(x % k) * (x / k) == n，其中%是模运算符，/是整数除法运算符。
**例:**

> **输入:** n = 4，k = 6
> **输出:** 10
> **解释:** (10 % 6) * (10 / 6) = (4) * (1) = 4 等于 n
> **输入:** n = 5，k = 5
> **输出:** 26

**方法:**使用[集合-1](https://www.geeksforgeeks.org/find-minimum-x-such-that-x-k-x-k-n/) 中的 K 值解决了问题。在本文中，我们将使用因子方法来解决上述问题。下面给出了解决上述问题的步骤。

*   因为方程的形式是 a*b = N，所以 a 和 b 是 N 的因子。
*   从 1 迭代到 sqrt(N)得到所有的因子。
*   因子 I 和 n/i 可以是 A，也可以是 b。
    1.  如果 I 是 A，n/i 是 B，那么这个数就是 **i*k + (n/i)** 。我们可以通过与 N 比较来检查这个数是否是 1，如果是，那么它就是一个满足方程的数。
    2.  如果 I 是 B，n/i 是 A，那么这个数字就是 **(n/i)*k + (i)** 。我们可以通过与 N 比较来检查这个数是否是 1，如果是，那么它就是一个满足方程的数。
*   获取所有满足方程的数字，并打印其中最小的数字。

下面是上述方法的实现。

## C++

```
// CPP Program to find the minimum
// positive X such that the given
// equation holds true
#include <bits/stdc++.h>
using namespace std;

// This function gives the required
// answer
int minimumX(int n, int k)
{
    int mini = INT_MAX;

    // Iterate for all the factors
    for (int i = 1; i * i <= n; i++) {

        // Check if i is a factor
        if (n % i == 0) {
            int fir = i;
            int sec = n / i;
            int num1 = fir * k + sec;

            // Consider i to be A and n/i to be B
            int res = (num1 / k) * (num1 % k);
            if (res == n)
                mini = min(num1, mini);

            int num2 = sec * k + fir;
            res = (num2 / k) * (num2 % k);

            // Consider i to be B and n/i to be A
            if (res == n)
                mini = min(num2, mini);
        }
    }
    return mini;
}

// Driver Code to test above function
int main()
{
    int n = 4, k = 6;
    cout << minimumX(n, k) << endl;

    n = 5, k = 5;
    cout << minimumX(n, k) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the minimum
// positive X such that the given
// equation holds true
import java.util.*;

class solution
{

// This function gives the required
// answer
static int minimumX(int n, int k)
{
    int mini = Integer.MAX_VALUE;

    // Iterate for all the factors
    for (int i = 1; i * i <= n; i++) {

        // Check if i is a factor
        if (n % i == 0) {
            int fir = i;
            int sec = n / i;
            int num1 = fir * k + sec;

            // Consider i to be A and n/i to be B
            int res = (num1 / k) * (num1 % k);
            if (res == n)
                mini = Math.min(num1, mini);

            int num2 = sec * k + fir;
            res = (num2 / k) * (num2 % k);

            // Consider i to be B and n/i to be A
            if (res == n)
                mini = Math.min(num2, mini);
        }
    }
    return mini;
}

// Driver Code to test above function
public static void main(String args[])
{
    int n = 4, k = 6;
    System.out.println(minimumX(n, k));

    n = 5;
    k = 5;
    System.out.println(minimumX(n, k));
}
}
```

## 蟒蛇 3

```
# Python3 program to find the minimum
# positive X such that the given
# equation holds true
import sys

# This function gives the required
# answer
def minimumX(n, k):

    mini = sys.maxsize

    # Iterate for all the factors
    i = 1
    while i * i <= n :

        # Check if i is a factor
        if (n % i == 0) :
            fir = i
            sec = n // i
            num1 = fir * k + sec

            # Consider i to be A and n/i to be B
            res = (num1 // k) * (num1 % k)
            if (res == n):
                mini = min(num1, mini)

            num2 = sec * k + fir
            res = (num2 // k) * (num2 % k)

            # Consider i to be B and n/i to be A
            if (res == n):
                mini = min(num2, mini)

        i += 1

    return mini

# Driver Code
if __name__ == "__main__":

    n = 4
    k = 6
    print (minimumX(n, k))

    n = 5
    k = 5
    print (minimumX(n, k))

# This code is contributed by ita_c    
```

## C#

```
// C# Program to find the minimum
// positive X such that the given
// equation holds true

using System;

class solution
{

// This function gives the required
// answer
static int minimumX(int n, int k)
{
    int mini = int.MaxValue;

    // Iterate for all the factors
    for (int i = 1; i * i <= n; i++) {

        // Check if i is a factor
        if (n % i == 0) {
            int fir = i;
            int sec = n / i;
            int num1 = fir * k + sec;

            // Consider i to be A and n/i to be B
            int res = (num1 / k) * (num1 % k);
            if (res == n)
                mini = Math.Min(num1, mini);

            int num2 = sec * k + fir;
            res = (num2 / k) * (num2 % k);

            // Consider i to be B and n/i to be A
            if (res == n)
                mini = Math.Min(num2, mini);
        }
    }
    return mini;
}

// Driver Code to test above function
public static void Main()
{
    int n = 4, k = 6;
    Console.WriteLine(minimumX(n, k));

    n = 5;
    k = 5;
    Console.WriteLine(minimumX(n, k));
}
// This code is contributed by Ryuga
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find the minimum
// positive X such that the given
// equation holds true

// Function gives the required
// answer
function minimumX($n, $k)
{
    $mini = PHP_INT_MAX;

    // Iterate for all the factors
    for ($i = 1; $i * $i <= $n; $i++)
    {

        // Check if i is a factor
        if ($n % $i == 0)
        {
            $fir = $i;
            $sec = (int)$n / $i;
            $num1 = $fir * $k + $sec;

            // Consider i to be A and n/i to be B
            $res = (int)($num1 / $k) *
                        ($num1 % $k);
            if ($res == $n)
                $mini = min($num1, $mini);

            $num2 = $sec * $k + $fir;
            $res = (int)($num2 / $k) *
                        ($num2 % $k);

            // Consider i to be B and n/i to be A
            if ($res == $n)
                $mini = min($num2, $mini);
        }
    }
    return $mini;
}

// Driver Code
$n = 4;
$k = 6;
echo minimumX($n, $k), "\n";

$n = 5;
$k = 5;
echo minimumX($n, $k), "\n";

// This code is contributed
// by Sach_Code
?>
```

## java 描述语言

```
<script>

    // Javascript Program to find the minimum
    // positive X such that the given
    // equation holds true

    // This function gives the required
    // answer
    function minimumX(n, k)
    {
        let mini = Number.MAX_VALUE;

        // Iterate for all the factors
        for (let i = 1; i * i <= n; i++) {

            // Check if i is a factor
            if (n % i == 0) {
                let fir = i;
                let sec = parseInt(n / i, 10);
                let num1 = fir * k + sec;

                // Consider i to be A and n/i to be B
                let res = parseInt((num1 / k), 10) * (num1 % k);
                if (res == n)
                    mini = Math.min(num1, mini);

                let num2 = sec * k + fir;
                res = parseInt((num2 / k), 10) * (num2 % k);

                // Consider i to be B and n/i to be A
                if (res == n)
                    mini = Math.min(num2, mini);
            }
        }
        return mini;
    }

    let n = 4, k = 6;
    document.write(minimumX(n, k) + "<br>");

    n = 5, k = 5;
    document.write(minimumX(n, k));

</script>
```

**Output:** 

```
10
26
```

**时间复杂度:** O(sqrt(N))，其中 N 为给定正整数。