# 模幂运算(模运算中的幂)

> 原文:[https://www . geesforgeks . org/模幂运算-模幂运算/](https://www.geeksforgeeks.org/modular-exponentiation-power-in-modular-arithmetic/)

给定三个数字 x，y 和 p，计算(x <sup>y</sup> ) % p。

**示例:**

```
Input:  x = 2, y = 3, p = 5
Output: 3
Explanation: 2^3 % 5 = 8 % 5 = 3.

Input:  x = 2, y = 5, p = 13
Output: 6
Explanation: 2^5 % 13 = 32 % 13 = 6.
```

我们已经讨论了[递归](https://www.geeksforgeeks.org/write-a-c-program-to-calculate-powxn/)和[迭代](https://www.geeksforgeeks.org/write-an-iterative-olog-y-function-for-powx-y/)功率解决方案。

下面讨论迭代解。

## C++

```
/* Iterative Function to calculate (x^y) in O(log y) */
int power(int x, int y)
{

    // Initialize answer
    int res = 1;

    // Check till the number becomes zero
    while (y)
    {

        // If y is odd, multiply x with result
        if (y % 2 == 1)
            res = (res * x);

        // y = y/2
        y = y >> 1;

        // Change x to x^2
        x = (x * x);
    }
    return res;
}

// This code is contributed by yaswanth0412
```

## C

```
/* Iterative Function to calculate (x^y) in O(log y) */
int power(int x, unsigned int y)
{
    int res = 1;     // Initialize result

    while (y > 0)
    {
        // If y is odd, multiply x with result
        if (y & 1)
            res = res*x;

        // y must be even now
        y = y>>1; // y = y/2
        x = x*x;  // Change x to x^2
    }
    return res;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Iterative Function to calculate (x^y) in O(log y) */
static int power(int x, int y)
{
    int res = 1;     // Initialize result

    while (y > 0)
    {

        // If y is odd, multiply x with result
        if ((y & 1) != 0)
            res = res * x;

        // y must be even now
        y = y >> 1; // y = y/2
        x = x * x;  // Change x to x^2
    }
    return res;
}

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# Iterative Function to calculate (x^y) in O(log y)
def power(x, y):

    # Initialize result
    res = 1   

    while (y > 0):

        # If y is odd, multiply x with result
        if ((y & 1) != 0):
            res = res * x

        # y must be even now
        y = y >> 1 # y = y/2
        x = x * x  # Change x to x^2

    return res

# This code is contributed by Khushboogoyal499
```

## C#

```
/* Iterative Function to calculate (x^y) in O(log y) */
static int power(int x, int y)
{
    int res = 1;     // Initialize result

    while (y > 0)
    {
        // If y is odd, multiply x with result
        if ((y & 1) != 0)
            res = res * x;

        // y must be even now
        y = y >> 1; // y = y/2
        x = x * x;  // Change x to x^2
    }
    return res;
}

// This code is contributed by Dharanendra L V.
```

## java 描述语言

```
<script>
/* Iterative Function to calculate (x^y) in O(log y) */
function power(x, y)
{
    let res = 1;     // Initialize result

    while (y > 0)
    {
        // If y is odd, multiply x with result
        if (y & 1)
            res = res*x;

        // y must be even now
        y = y>>1; // y = y/2
        x = x*x; // Change x to x^2
    }
    return res;
}

// This code is contributed by _saurabh_jaiswal
</script>
```

**有效方法:**

上述解决方案的问题是，对于大的 n 或 x 值，可能会发生溢出。因此，功率通常在大数模下评估。

下面是基本的模块化属性，用于在模块化算法下有效地计算能力。

```
(ab) mod p = ( (a mod p) (b mod p) ) mod p 

For example a = 50,  b = 100, p = 13
50  mod 13  = 11
100 mod 13  = 9

(50 * 100) mod 13 = ( (50 mod 13) * (100 mod 13) ) mod 13 
or (5000) mod 13 = ( 11 * 9 ) mod 13
or 8 = 8
```

下面是基于上述属性的实现。

## C++14

```
// Iterative C++ program to compute modular power
#include <iostream>
using namespace std;

/* Iterative Function to calculate (x^y)%p in O(log y) */
int power(long long x, unsigned int y, int p)
{
    int res = 1;     // Initialize result

    x = x % p; // Update x if it is more than or
                // equal to p

    if (x == 0) return 0; // In case x is divisible by p;

    while (y > 0)
    {
        // If y is odd, multiply x with result
        if (y & 1)
            res = (res*x) % p;

        // y must be even now
        y = y>>1; // y = y/2
        x = (x*x) % p;
    }
    return res;
}

// Driver code
int main()
{
    int x = 2;
    int y = 5;
    int p = 13;
    cout << "Power is " << power(x, y, p);
    return 0;
}

// This code is contributed by shubhamsingh10
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Iterative Java program to compute modular power
import java.io.*;
class GFG
{

  /* Iterative Function to calculate (x^y) in O(log y) */
  static int power(int x, int y, int p)
  {
    int res = 1; // Initialize result

    x = x % p; // Update x if it is more than or
    // equal to p

    if (x == 0)
      return 0; // In case x is divisible by p;

    while (y > 0)
    {

      // If y is odd, multiply x with result
      if ((y & 1) != 0)
        res = (res * x) % p;

      // y must be even now
      y = y >> 1; // y = y/2
      x = (x * x) % p;
    }
    return res;
  }

  // Driver Code
  public static void main(String[] args)
  {
    int x = 2;
    int y = 5;
    int p = 13;
    System.out.print("Power is " + power(x, y, p));
  }
}

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# Iterative Python3 program
# to compute modular power

# Iterative Function to calculate
# (x^y)%p in O(log y)
def power(x, y, p) :
    res = 1     # Initialize result

    # Update x if it is more
    # than or equal to p
    x = x % p

    if (x == 0) :
        return 0

    while (y > 0) :

        # If y is odd, multiply
        # x with result
        if ((y & 1) == 1) :
            res = (res * x) % p

        # y must be even now
        y = y >> 1      # y = y/2
        x = (x * x) % p

    return res

# Driver Code

x = 2; y = 5; p = 13
print("Power is ", power(x, y, p))

# This code is contributed by Nikita Tiwari.
```

## C#

```
using System;
public class GFG
{

  /* Iterative Function to calculate (x^y) in O(log y) */
  static int power(int x, int y, int p)
  {
    int res = 1; // Initialize result

    x = x % p; // Update x if it is more than or
    // equal to p

    if (x == 0)
      return 0; // In case x is divisible by p;

    while (y > 0)
    {

      // If y is odd, multiply x with result
      if ((y & 1) != 0)
        res = (res * x) % p;

      // y must be even now
      y = y >> 1; // y = y/2
      x = (x * x) % p;
    }
    return res;
  }

  // Driver Code
  static public void Main ()
  {
    int x = 2;
    int y = 5;
    int p = 13;
    Console.Write("Power is " + power(x, y, p));
  }
}

// This code is contributed by Dharanendra L V.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Iterative PHP program to
// compute modular power

// Iterative Function to
// calculate (x^y)%p in O(log y)
function power($x, $y, $p)
{
    // Initialize result
    $res = 1;

    // Update x if it is more
    // than or equal to p
    $x = $x % $p;

    if ($x == 0)
        return 0;

    while ($y > 0)
    {
        // If y is odd, multiply
        // x with result
        if ($y & 1)
            $res = ($res * $x) % $p;

        // y must be even now

        // y = $y/2
        $y = $y >> 1;
        $x = ($x * $x) % $p;
    }
    return $res;
}

// Driver Code
$x = 2;
$y = 5;
$p = 13;
echo "Power is ", power($x, $y, $p);

// This code is contributed by aj_36
?>
```

## java 描述语言

```
// Iterative Javascript program to
// compute modular power

// Iterative Function to
// calculate (x^y)%p in O(log y)
function power(x, y, p)
{
    // Initialize result
    let res = 1;

    // Update x if it is more
    // than or equal to p
    x = x % p;

    if (x == 0)
        return 0;

    while (y > 0)
    {
        // If y is odd, multiply
        // x with result
        if (y & 1)
            res = (res * x) % p;

        // y must be even now

        // y = $y/2
        y = y >> 1;
        x = (x * x) % p;
    }
    return res;
}

// Driver Code
let x = 2;
let y = 5;
let p = 13;
document.write("Power is " + power(x, y, p));

// This code is contributed by _saurabh_jaiswal
```

**Output**

```
Power is 6
```

上述解决方案的时间复杂度为 0(对数 y)。

[**【模幂运算(递归)**](https://www.geeksforgeeks.org/modular-exponentiation-recursive/)
本文由 **Shivam Agrawal** 供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。