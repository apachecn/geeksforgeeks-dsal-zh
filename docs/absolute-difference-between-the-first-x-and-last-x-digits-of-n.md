# N 的前 X 位和后 X 位的绝对差值

> 原文:[https://www . geesforgeks . org/n 的第一个 x 位数和最后一个 x 位数的绝对差值/](https://www.geeksforgeeks.org/absolute-difference-between-the-first-x-and-last-x-digits-of-n/)

给定两个整数 **N** 和 **X** 。任务是打印 **N** 中第一个 **X** 和最后一个 **X** 数字的绝对差值。考虑到位数至少是 2*x。

**示例:**

```
Input: N = 21546, X = 2
Output: 25
The first two digit in 21546 is 21.
The last two digit in 21546 is 46.
The absolute difference of 21 and 46 is 25.

Input: N = 351684617, X = 3
Output: 266
```

**简单方法:**

*   将数字的最后 x 位存储在最后。
*   找出数字中的位数。
*   去掉除第一个 x 以外的所有数字。
*   先存储数字的前 x 个整数。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the
// number of digits in the integer
long long digitsCount(long long n)
{
    int len = 0;
    while (n > 0) {
        len++;
        n /= 10;
    }
    return len;
}

// Function to find the absolute difference
long long absoluteFirstLast(long long n, int x)
{
    // Store the last x digits in last
    int i = 0, mod = 1;
    while (i < x) {
        mod *= 10;
        i++;
    }
    int last = n % mod;

    // Count the no. of digits in N
    long long len = digitsCount(n);

    // Remove the digits except the first x
    while (len != x) {
        n /= 10;
        len--;
    }

    // Store the first x digits in first
    int first = n;

    // Return the absolute difference between
    // the first and last
    return abs(first - last);
}

// Driver code
int main()
{
    long long n = 21546, x = 2;
    cout << absoluteFirstLast(n, x);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG
{

// Function to find the
// number of digits in the integer
static int digitsCount(int n)
{
    int len = 0;
    while (n > 0)
    {
        len++;
        n /= 10;
    }
    return len;
}

// Function to find the absolute difference
static int absoluteFirstLast(int n, int x)
{
    // Store the last x digits in last
    int i = 0, mod = 1;
    while (i < x)
    {
        mod *= 10;
        i++;
    }
    int last = n % mod;

    // Count the no. of digits in N
    int len = digitsCount(n);

    // Remove the digits except the first x
    while (len != x)
    {
        n /= 10;
        len--;
    }

    // Store the first x digits in first
    int first = n;

    // Return the absolute difference between
    // the first and last
    return Math.abs(first - last);
}

// Driver code
public static void main(String args[])
{
    int n = 21546, x = 2;
    System.out.println(absoluteFirstLast(n, x));
}
}

// This code is contributed by
// Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to find the
# number of digits in the integer
def digitsCount(n) :
    length = 0;
    while (n > 0) :
        length += 1;
        n //= 10;

    return length;

# Function to find the absolute difference
def absoluteFirstLast(n, x) :

    # Store the last x digits in last
    i = 0 ;
    mod = 1;
    while (i < x) :
        mod *= 10;
        i += 1;

    last = n % mod;

    # Count the no. of digits in N
    length = digitsCount(n);

    # Remove the digits except the first x
    while (length != x) :
        n //= 10;
        length -= 1;

    # Store the first x digits in first
    first = n;

    # Return the absolute difference between
    # the first and last
    return abs(first - last);

# Driver code
if __name__ == "__main__" :

    n = 21546 ;
    x = 2;
    print(absoluteFirstLast(n, x));

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to find the
// number of digits in the integer
static int digitsCount(int n)
{
    int len = 0;
    while (n > 0)
    {
        len++;
        n /= 10;
    }
    return len;
}

// Function to find the absolute difference
static int absoluteFirstLast(int n, int x)
{
    // Store the last x digits in last
    int i = 0, mod = 1;
    while (i < x)
    {
        mod *= 10;
        i++;
    }
    int last = n % mod;

    // Count the no. of digits in N
    int len = digitsCount(n);

    // Remove the digits except the first x
    while (len != x)
    {
        n /= 10;
        len--;
    }

    // Store the first x digits in first
    int first = n;

    // Return the absolute difference between
    // the first and last
    return Math.Abs(first - last);
}

// Driver code
public static void Main(String []args)
{
    int n = 21546, x = 2;
    Console.Write(absoluteFirstLast(n, x));
}
}

// This code has been contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to find the number of
// digits in the integer
function digitsCount($n)
{
    $len = 0;
    while ($n > 0)
    {
        $len++;
        $n = (int)($n / 10);
    }
    return $len;
}

// Function to find the absolute difference
function absoluteFirstLast($n, $x)
{
    // Store the last x digits in last
    $i = 0;
    $mod = 1;
    while ($i < $x)
    {
        $mod *= 10;
        $i++;
    }
    $last = $n % $mod;

    // Count the no. of digits in N
    $len = digitsCount($n);

    // Remove the digits except the first x
    while ($len != $x)
    {
        $n = (int)($n / 10);
        $len--;
    }

    // Store the first x digits in first
    $first = $n;

    // Return the absolute difference
    // between the first and last
    return abs($first - $last);
}

// Driver code
$n = 21546;
$x = 2;
echo absoluteFirstLast($n, $x);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to find the
// number of digits in the integer
function digitsCount(n)
{
    let len = 0;
    while (n > 0)
    {
        len++;
        n = Math.floor(n / 10);
    }
    return len;
}

// Function to find the absolute difference
function absoluteFirstLast(n, x)
{
    // Store the last x digits in last
    let i = 0, mod = 1;
    while (i < x)
    {
        mod *= 10;
        i++;
    }
    let last = n % mod;

    // Count the no. of digits in N
    let len = digitsCount(n);

    // Remove the digits except the first x
    while (len != x)
    {
        n = Math.floor(n / 10);
        len--;
    }

    // Store the first x digits in first
    let first = n;

    // Return the absolute difference between
    // the first and last
    return Math.abs(first - last);
}

// driver program

    let n = 21546, x = 2;
    document.write(absoluteFirstLast(n, x));

</script>
```

**Output:** 

```
25
```