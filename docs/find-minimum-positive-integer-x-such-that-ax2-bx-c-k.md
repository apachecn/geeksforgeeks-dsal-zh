# 求最小正整数 x，使得 a(x^2) + b(x) + c > = k

> 原文:[https://www . geesforgeks . org/find-minimum-正整数-x-so-ax2-bx-c-k/](https://www.geeksforgeeks.org/find-minimum-positive-integer-x-such-that-ax2-bx-c-k/)

给定四个整数 **a** 、 **b** 、 **c** 和 **k** 。任务是找到 **x** 的最小正值，使得 **ax <sup>2</sup> + bx + c ≥ k** 。
**举例:**

> **输入:** a = 3，b = 4，c = 5，k = 6
> **输出:** 1
> 对于 x = 0，a * 0 + b * 0 + c = 5 < 6
> 对于 x = 1，a * 1+b * 1+c = 3+4+5 = 12>6
> T8】输入: a = 2，b = 7，c = 6，k = 3
> **输出:**

****进场:**思路是用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)。我们搜索的下限将是 **0** ，因为 **x** 必须是最小正整数。
以下是上述方法的实施:** 

## **C++**

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum positive
// integer satisfying the given equation
int MinimumX(int a, int b, int c, int k)
{
    int x = INT_MAX;

    if (k <= c)
        return 0;

    int h = k - c;
    int l = 0;

    // Binary search to find the value of x
    while (l <= h) {
        int m = (l + h) / 2;
        if ((a * m * m) + (b * m) > (k - c)) {
            x = min(x, m);
            h = m - 1;
        }
        else if ((a * m * m) + (b * m) < (k - c))
            l = m + 1;
        else
            return m;
    }

    // Return the answer
    return x;
}

// Driver code
int main()
{
    int a = 3, b = 2, c = 4, k = 15;
    cout << MinimumX(a, b, c, k);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java implementation of the approach
class GFG
{

// Function to return the minimum positive
// integer satisfying the given equation
static int MinimumX(int a, int b, int c, int k)
{
    int x = Integer.MAX_VALUE;

    if (k <= c)
        return 0;

    int h = k - c;
    int l = 0;

    // Binary search to find the value of x
    while (l <= h)
    {
        int m = (l + h) / 2;
        if ((a * m * m) + (b * m) > (k - c))
        {
            x = Math.min(x, m);
            h = m - 1;
        }
        else if ((a * m * m) + (b * m) < (k - c))
            l = m + 1;
        else
            return m;
    }

    // Return the answer
    return x;
}

// Driver code
public static void main(String[] args)
{
    int a = 3, b = 2, c = 4, k = 15;
    System.out.println(MinimumX(a, b, c, k));
}
}

// This code is contributed by Code_Mech.
```

## **蟒蛇 3**

```
# Python3 implementation of the approach

# Function to return the minimum positive
# integer satisfying the given equation
def MinimumX(a, b, c, k):

    x = 10**9

    if (k <= c):
        return 0

    h = k - c
    l = 0

    # Binary search to find the value of x
    while (l <= h):
        m = (l + h) // 2
        if ((a * m * m) + (b * m) > (k - c)):
            x = min(x, m)
            h = m - 1

        elif ((a * m * m) + (b * m) < (k - c)):
            l = m + 1
        else:
            return m

    # Return the answer
    return x

# Driver code
a, b, c, k = 3, 2, 4, 15
print(MinimumX(a, b, c, k))

# This code is contributed by mohit kumar
```

## **C#**

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the minimum positive
// integer satisfying the given equation
static int MinimumX(int a, int b, int c, int k)
{
    int x = int.MaxValue;

    if (k <= c)
        return 0;

    int h = k - c;
    int l = 0;

    // Binary search to find the value of x
    while (l <= h)
    {
        int m = (l + h) / 2;
        if ((a * m * m) + (b * m) > (k - c))
        {
            x = Math.Min(x, m);
            h = m - 1;
        }
        else if ((a * m * m) + (b * m) < (k - c))
            l = m + 1;
        else
            return m;
    }

    // Return the answer
    return x;
}

// Driver code
public static void Main()
{
    int a = 3, b = 2, c = 4, k = 15;
    Console.Write(MinimumX(a, b, c, k));
}
}

// This code is contributed by Akanksha Rai
```

## **服务器端编程语言（Professional Hypertext Preprocessor 的缩写）**

```
<?php
// PHP implementation of the approach

// Function to return the minimum positive
// integer satisfying the given equation
function MinimumX($a, $b, $c, $k)
{
    $x = PHP_INT_MAX;

    if ($k <= $c)
        return 0;

    $h = $k - $c;
    $l = 0;

    // Binary search to find the value of x
    while ($l <= $h)
    {
        $m = floor(($l + $h) / 2);
        if (($a * $m * $m) +
            ($b * $m) > ($k - $c))
        {
            $x = min($x, $m);
            $h = $m - 1;
        }
        else if (($a * $m * $m) +
                 ($b * $m) < ($k - $c))
            $l = $m + 1;
        else
            return $m;
    }

    // Return the answer
    return $x;
}

// Driver code
$a = 3; $b = 2; $c = 4; $k = 15;

echo MinimumX($a, $b, $c, $k);

// This code is contributed by Ryuga
?>
```

## **java 描述语言**

```
<script>
// Javascript implementation of the approach

// Function to return the minimum positive
// integer satisfying the given equation
function MinimumX(a,b,c,k)
{
    let x = Number.MAX_VALUE;

    if (k <= c)
        return 0;

    let h = k - c;
    let l = 0;

    // Binary search to find the value of x
    while (l <= h)
    {
        let m = Math.floor((l + h) / 2);
        if ((a * m * m) + (b * m) > (k - c))
        {
            x = Math.min(x, m);
            h = m - 1;
        }
        else if ((a * m * m) + (b * m) < (k - c))
            l = m + 1;
        else
            return m;
    }

    // Return the answer
    return x;
}

// Driver code
let a = 3, b = 2, c = 4, k = 15;
document.write(MinimumX(a, b, c, k));

// This code is contributed by patel2127
</script>
```

****Output:** 

```
2
```**