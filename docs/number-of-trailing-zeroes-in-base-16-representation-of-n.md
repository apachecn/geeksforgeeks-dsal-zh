# N 的 16 进制表示中尾随零的个数！

> 原文:[https://www . geeksforgeeks . org/n 的 16 进制表示的尾随零数/](https://www.geeksforgeeks.org/number-of-trailing-zeroes-in-base-16-representation-of-n/)

给定一个整数 **N** ，任务是在 **N** 的阶乘的 16 进制表示中找到尾随零的数量。
**例:**

> **输入:**N = 6
> T3】输出: 1
> 6！= 720(基数 10) = 2D0(基数 16)
> **输入:** N = 100
> **输出:** 24

**进场:**

*   尾随零的数量将是**基数 10** 中 **N** 的阶乘 **16** 的最高幂。
*   我们知道**16 = 2<sup>4</sup>T3。所以， **16** 的最高幂等于 **N** 除以 **4** 的阶乘中的最高幂 **2** 。**
*   计算 **N 中 **2** 的最高幂！**，我们可以用[勒让德公式](https://www.geeksforgeeks.org/given-p-and-n-find-the-largest-x-such-that-px-divides-n-2/)。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
#define ll long long int
using namespace std;

// Function to return the count of trailing zeroes
ll getTrailingZeroes(ll n)
{
    ll count = 0;
    ll val, powerTwo = 2;

    // Implementation of the Legendre's formula
    do {
        val = n / powerTwo;
        count += val;
        powerTwo *= 2;
    } while (val != 0);

    // Count has the highest power of 2
    // that divides n! in base 10
    return (count / 4);
}

// Driver code
int main()
{
    int n = 6;
    cout << getTrailingZeroes(n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GfG
{

// Function to return the count of trailing zeroes
static long getTrailingZeroes(long n)
{
    long count = 0;
    long val, powerTwo = 2;

    // Implementation of the Legendre's formula
    do
    {
        val = n / powerTwo;
        count += val;
        powerTwo *= 2;
    } while (val != 0);

    // Count has the highest power of 2
    // that divides n! in base 10
    return (count / 4);
}

// Driver code
public static void main(String[] args)
{
    int n = 6;
    System.out.println(getTrailingZeroes(n));
}
}

// This code is contributed by
// Prerna Saini.
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of
# trailing zeroes
def getTrailingZeroes(n):

    count = 0
    val, powerTwo = 1, 2

    # Implementation of the Legendre's
    # formula
    while (val != 0):
        val = n //powerTwo
        count += val
        powerTwo *= 2

    # Count has the highest power of 2
    # that divides n! in base 10
    return (count // 4)

# Driver code
n = 6
print(getTrailingZeroes(n))

# This code is contributed
# by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;
class GFG
{

// Function to return the count of
// trailing zeroes
static long getTrailingZeroes(long n)
{
    long count = 0;
    long val, powerTwo = 2;

    // Implementation of the
    // Legendre's formula
    do
    {
        val = n / powerTwo;
        count += val;
        powerTwo *= 2;
    } while (val != 0);

    // Count has the highest power of 2
    // that divides n! in base 10
    return (count / 4);
}

// Driver code
public static void Main()
{
    int n = 6;
    Console.Write(getTrailingZeroes(n));
}
}

// This code is contributed by
// Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the count of
// trailing zeroes
function getTrailingZeroes($n)
{
    $count = 0;
    $val; $powerTwo = 2;

    // Implementation of the Legendre's formula
    do
    {
        $val = (int)($n / $powerTwo);
        $count += $val;
        $powerTwo *= 2;
    } while ($val != 0);

    // Count has the highest power of 2
    // that divides n! in base 10
    return ($count / 4);
}

// Driver code
$n = 6;
echo(getTrailingZeroes($n));

// This code is contributed by
// Code_Mech.

?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the count of trailing zeroes
function getTrailingZeroes(n)
{
    let count = 0;
    let val, powerTwo = 2;

    // Implementation of the Legendre's formula
    do {
        val = Math.floor(n / powerTwo);
        count += val;
        powerTwo *= 2;
    } while (val != 0);

    // Count has the highest power of 2
    // that divides n! in base 10
    return (Math.floor(count / 4));
}

// Driver code

    let n = 6;
    document.write(getTrailingZeroes(n));

// This code is contributed by Surbhi Tyagi

</script>
```

**Output:** 

```
1
```