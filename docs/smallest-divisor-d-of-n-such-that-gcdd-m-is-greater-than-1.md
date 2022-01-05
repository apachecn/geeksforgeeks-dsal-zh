# N 的最小除数 D，使得 gcd(D，M)大于 1

> 原文:[https://www . geesforgeks . org/最小除数-d of-n-so-gcdd-m-大于-1/](https://www.geeksforgeeks.org/smallest-divisor-d-of-n-such-that-gcdd-m-is-greater-than-1/)

给定两个正整数 **N** 和 **M** 。，任务是找到 N 的最小除数 D，使得 **gcd(D，M) > 1** 。如果没有这样的除数，那么打印-1。
**举例:**

> **输入:** N = 8，M = 10
> **输出:** 2
> **输入:** N = 8，M = 1
> **输出:** -1

一种**天真的方法**是对每个因子进行迭代，计算因子和 M 的 gcd，如果超过 M，那么我们就有答案了。
**时间复杂度:** O(N * log max(N，M))
一种高效的**方法是迭代直到 sqrt(n)并检查 gcd(i，M)。如果 gcd(i，m) > 1，那么我们打印并打破它，否则我们检查 gcd(n/i，m)并存储它们的最小值。
以下是上述办法的实施情况。** 

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum divisor
int findMinimum(int n, int m)
{
    int mini = m;

    // Iterate for all factors of N
    for (int i = 1; i * i <= n; i++) {
        if (n % i == 0) {
            int sec = n / i;

            // Check for gcd > 1
            if (__gcd(m, i) > 1) {
                return i;
            }

            // Check for gcd > 1
            else if (__gcd(sec, m) > 1) {
                mini = min(sec, mini);
            }
        }
    }

    // If gcd is m itself
    if (mini == m)
        return -1;
    else
        return mini;
}
// Drivers code
int main()
{
    int n = 8, m = 10;
    cout << findMinimum(n, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{

static int __gcd(int a, int b)
{
    if (b == 0)
        return a;
    return __gcd(b, a % b);

}

// Function to find the minimum divisor
static int findMinimum(int n, int m)
{
    int mini = m;

    // Iterate for all factors of N
    for (int i = 1; i * i <= n; i++)
    {
        if (n % i == 0)
        {
            int sec = n / i;

            // Check for gcd > 1
            if (__gcd(m, i) > 1)
            {
                return i;
            }

            // Check for gcd > 1
            else if (__gcd(sec, m) > 1)
            {
                mini = Math.min(sec, mini);
            }
        }
    }

    // If gcd is m itself
    if (mini == m)
        return -1;
    else
        return mini;
}

// Driver code
public static void main (String[] args)
{
    int n = 8, m = 10;
    System.out.println(findMinimum(n, m));
}
}

// This code is contributed by chandan_jnu
```

## 蟒蛇 3

```
# Python3 implementation of the above approach
import math

# Function to find the minimum divisor
def findMinimum(n, m):

    mini, i = m, 1

    # Iterate for all factors of N
    while i * i <= n:
        if n % i == 0:
            sec = n // i

            # Check for gcd > 1
            if math.gcd(m, i) > 1:
                return i

            # Check for gcd > 1
            elif math.gcd(sec, m) > 1:
                mini = min(sec, mini)

        i += 1

    # If gcd is m itself
    if mini == m:
        return -1
    else:
        return mini

# Drivers code
if __name__ == "__main__":

    n, m = 8, 10
    print(findMinimum(n, m))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

static int __gcd(int a, int b)
{
    if (b == 0)
        return a;
    return __gcd(b, a % b);

}

// Function to find the minimum divisor
static int findMinimum(int n, int m)
{
    int mini = m;

    // Iterate for all factors of N
    for (int i = 1; i * i <= n; i++)
    {
        if (n % i == 0)
        {
            int sec = n / i;

            // Check for gcd > 1
            if (__gcd(m, i) > 1)
            {
                return i;
            }

            // Check for gcd > 1
            else if (__gcd(sec, m) > 1)
            {
                mini = Math.Min(sec, mini);
            }
        }
    }

    // If gcd is m itself
    if (mini == m)
        return -1;
    else
        return mini;
}

// Driver code
static void Main()
{
    int n = 8, m = 10;
    Console.WriteLine(findMinimum(n, m));
}
}

// This code is contributed by chandan_jnu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach
function __gcd($a, $b)
{
    if ($b == 0)
        return $a;
    return __gcd($b, $a % $b);

}

// Function to find the minimum divisor
function findMinimum($n, $m)
{
    $mini = $m;

    // Iterate for all factors of N
    for ($i = 1; $i * $i <= $n; $i++)
    {
        if ($n % $i == 0)
        {
            $sec = $n / $i;

            // Check for gcd > 1
            if (__gcd($m, $i) > 1)
            {
                return $i;
            }

            // Check for gcd > 1
            else if (__gcd($sec, $m) > 1)
            {
                $mini = min($sec, $mini);
            }
        }
    }

    // If gcd is m itself
    if ($mini == $m)
        return -1;
    else
        return $mini;
}

// Driver code
$n = 8; $m = 10;
echo(findMinimum($n, $m));

// This code is contributed by Code_Mech.
```

## java 描述语言

```
<script>
// javascript implementation of the above approach   
function __gcd(a , b) {
        if (b == 0)
            return a;
        return __gcd(b, a % b);

    }

    // Function to find the minimum divisor
    function findMinimum(n , m) {
        var mini = m;

        // Iterate for all factors of N
        for (var i = 1; i * i <= n; i++) {
            if (n % i == 0) {
                var sec = n / i;

                // Check for gcd > 1
                if (__gcd(m, i) > 1) {
                    return i;
                }

                // Check for gcd > 1
                else if (__gcd(sec, m) > 1) {
                    mini = Math.min(sec, mini);
                }
            }
        }

        // If gcd is m itself
        if (mini == m)
            return -1;
        else
            return mini;
    }

    // Driver code

        var n = 8, m = 10;
        document.write(findMinimum(n, m));

// This code is contributed by todaysgaurav
</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(sqrt N * log max(N，M))