# 画 N 幅画使相邻的画没有相同颜色的方法

> 原文:[https://www . geeksforgeeks . org/绘画方式-n-绘画-这样-相邻的绘画-没有相同的颜色/](https://www.geeksforgeeks.org/ways-to-paint-n-paintings-such-that-adjacent-paintings-dont-have-same-colors/)

给定两个整数 n 和 m，其中 n 代表从 1 到 n 的一些画，m 代表从 1 到 m 的一些颜色，数量不限。任务是找到画的方法的数量，使得没有两个连续的画有相同的颜色。
**注意:**答案必须以 10^9 +7 为模计算，因为答案可以很大。
**示例:**

```
Input: n = 4, m = 2 
Output: 2

Input: n = 4, m = 6
Output: 750
```

问于:民族乐器
**途径:**
给定颜色总数为 **m** ，绘画总数为 1 至 **n** 。根据相邻两幅画不具有相同颜色的条件，第一幅画可以由 m 种颜色中的任何一种绘制，其余的任何一幅画可以由 m-1 种颜色中的任何一种绘制，除了前一幅画所使用的颜色。因此，如果我们推导出总路数的解，

> **m * (m-1)^(n-1)** 是实际答案。

现在，这既可以通过简单的迭代计算，也可以通过 **O(logn)** 时间内的有效功率计算方法计算。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
#define modd 1000000007
using namespace std;

// Function for finding the power
unsigned long power(unsigned long x,
                    unsigned long y, unsigned long p)
{
    unsigned long res = 1; // Initialize result

    x = x % p; // Update x if it is more than or
    // equal to p

    while (y > 0) {

        // If y is odd, multiply x with result
        if (y & 1)
            res = (res%p * x%p) % p;

        // y must be even now
        y = y >> 1; // y = y/2
        x = (x%p * x%p) % p;
    }
    return res;
}

// Function to calculate the number of ways
int ways(int n, int m)
{
    // Answer must be modulo of 10^9 + 7
    return power(m - 1, n - 1, modd) * m % modd;
}

// Driver code
int main()
{
    int n = 5, m = 5;
    cout << ways(n, m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach

class GFG
{
    static final int modd = 1000000007;

    // Function for finding the power
    static long power(long x, long y, long p)
    {
        long res = 1; // Initialize result

        // Update x if it is more than or
        // equal to p
        x = x % p;

        while (y > 0)
        {
            // If y is odd, multiply x with result
            if (y % 2 == 1)
            {
                res = (res%p * x%p) % p;
            }

            // y must be even now
            y = y >> 1; // y = y/2
            x = (x%p * x%p) % p;
        }
        return res;
    }

    // Function to calculate the number of ways
    static int ways(int n, int m)
    {
        // Answer must be modulo of 10^9 + 7
        return (int) (power(m - 1, n - 1, modd)
                            * m % modd);
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 5, m = 5;
        System.out.println(ways(n, m));

    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach

modd = 1000000007

# Function for finding the power
def power(x, y, p):

    res = 1 # Initialize result

    x = x % p # Update x if it is more
              # than or equal to p

    while (y > 0):

        # If y is odd, multiply x with result
        if (y & 1):
            res = (res%p * x%p) % p

        # y must be even now
        y = y >> 1 # y = y/2
        x = (x%p * x%p) % p

    return res

# Function to calculate the number of ways
def ways(n, m):

    # Answer must be modulo of 10^9 + 7
    return power(m - 1, n - 1, modd) * m % modd

# Driver code
n, m = 5, 5
print(ways(n, m))

# This code is contributed
# by Mohit Kumar 29
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{
    static int modd = 1000000007;

    // Function for finding the power
    static long power(long x, long y, long p)
    {
        long res = 1; // Initialize result

        // Update x if it is more than or
        // equal to p
        x = x % p;

        while (y > 0)
        {
            // If y is odd, multiply x with result
            if (y % 2 == 1)
            {
                res = (res%p * x%p) % p;
            }

            // y must be even now
            y = y >> 1; // y = y/2
            x = (x%p * x%p) % p;
        }
        return res;
    }

    // Function to calculate the number of ways
    static int ways(int n, int m)
    {
        // Answer must be modulo of 10^9 + 7
        return (int) (power(m - 1, n - 1, modd)
                            * m % modd);
    }

    // Driver code
    static public void Main ()
    {
            int n = 5, m = 5;
        Console.WriteLine(ways(n, m));
    }
}

// This code is contributed by ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Iterative Function to calculate
// (x^y)%p in O(log y)
function power($x, $y, $p)
{
    // Initialize result
    $res = 1;

    // Update x if it is more
    // than or equal to p
    $x = $x % $p;

    while ($y > 0)
    {
        // If y is odd, multiply
        // x with result
        if ($y & 1)
            $res = ($res % $p * $x % $p) % $p;

        // y must be even now

        // y = $y/2
        $y = $y >> 1;
        $x = ($x % $p * $x % $p) % $p;
    }
    return $res;
}

// Function to calculate the number of ways
function ways($n, $m)
{
    $modd =1000000007;

    // Answer must be modulo of 10^9 + 7
    return (power($m - 1, $n - 1,
                  $modd) * $m ) % $modd;
}

// Driver code
$n = 5;
$m = 5;
echo ways($n, $m);

// This code is contributed
// by Arnab Kundu
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of the above approach

    let modd = 1000000007;

    // Function for finding the power
    function power(x, y, p)
    {
        let res = 1; // Initialize result

        // Update x if it is more than or
        // equal to p
        x = x % p;

        while (y > 0)
        {
            // If y is odd, multiply x with result
            if (y % 2 == 1)
            {
                res = (res%p * x%p) % p;
            }

            // y must be even now
            y = y >> 1; // y = y/2
            x = (x%p * x%p) % p;
        }
        return res;
    }

    // Function to calculate the number of ways
    function ways(n, m)
    {
        // Answer must be modulo of 10^9 + 7
        return (power(m - 1, n - 1, modd) * m % modd);
    }

    let n = 5, m = 5;
      document.write(ways(n, m));

</script>
```

**Output:** 

```
1280
```

**时间复杂度:**O(logN)
T3】辅助空间: O(1)