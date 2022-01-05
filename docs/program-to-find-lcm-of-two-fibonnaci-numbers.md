# 程序求两个斐波那契数的 LCM

> 原文:[https://www . geesforgeks . org/program-to-find-LCM-of-two-fibonnaci-numbers/](https://www.geeksforgeeks.org/program-to-find-lcm-of-two-fibonnaci-numbers/)

这里给出了两个正数 **a** 和 **b** 。任务是打印第**个**和第**个**斐波那契数的最小公倍数。
前几个斐波那契数是 **0、1、1、2、3、5、8、13、21、34、55、89、144、……**
注意 **0** 被认为是 **0'th** 斐波那契数。
**举例:**

```
Input : a = 3, b = 12
Output : 144

Input : a = 8, b = 37
Output : 507314157
```

**接近**:问题的简单解决方法是，

1.  找到第**个**斐波那契数。
2.  找到第**个**斐波那契数。
3.  找到他们的 [GCD](https://www.geeksforgeeks.org/gcd-and-fibonacci-numbers/) ，在 GCD 的帮助下找到他们的 LCM。关系为 **LCM(a，b) = (a x b) / GCD(a，b)** [(请参考此处)](https://www.geeksforgeeks.org/program-to-find-lcm-of-two-numbers/)。

以下是上述方法的实现:

## C++

```
// C++ Program to find LCM of Fib(a)
// and Fib(b)
#include <bits/stdc++.h>
using namespace std;
const int MAX = 1000;

// Create an array for memorization
int f[MAX] = { 0 };

// Function to return the n'th Fibonacci
// number using table f[].
int fib(int n)
{
    // Base cases
    if (n == 0)
        return 0;
    if (n == 1 || n == 2)
        return (f[n] = 1);

    // If fib(n) is already computed
    if (f[n])
        return f[n];

    int k = (n & 1) ? (n + 1) / 2 : n / 2;

    // Applying recursive formula
    // Note value n&1 is 1
    // if n is odd, else 0.
    f[n] = (n & 1) ? (fib(k) * fib(k) + fib(k - 1) * fib(k - 1))
                   : (2 * fib(k - 1) + fib(k)) * fib(k);

    return f[n];
}

// Function to return gcd of a and b
int gcd(int a, int b)
{
    if (a == 0)
        return b;

    return gcd(b % a, a);
}

// Function to return the LCM of
// Fib(a) and Fib(a)
int findLCMFibonacci(int a, int b)
{
    return (fib(a) * fib(b)) / fib(gcd(a, b));
}

// Driver code
int main()
{
    int a = 3, b = 12;

    cout << findLCMFibonacci(a, b);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find LCM of Fib(a)
// and Fib(b)
import java.util.*;

class GFG
{

static int MAX = 1000;

// Create an array for memoization
static int[] f = new int[MAX];

// Function to return the n'th Fibonacci
// number using table f[].
static int fib(int n)
{
    // Base cases
    if (n == 0)
        return 0;
    if (n == 1 || n == 2)
        return (f[n] = 1);

    // If fib(n) is already computed
    if (f[n] != 0)
        return f[n];
    int k = 0;
    if ((n & 1) != 0)
        k = (n + 1) / 2;
    else
        k = n / 2;

    // Applying recursive formula
    // Note value n&1 is 1
    // if n is odd, else 0.
    if((n & 1 ) != 0)
        f[n] = (fib(k) * fib(k) +
                fib(k - 1) * fib(k - 1));
    else
        f[n] = (2 * fib(k - 1) +
                    fib(k)) * fib(k);

    return f[n];
}

// Function to return gcd of a and b
static int gcd(int a, int b)
{
    if (a == 0)
        return b;

    return gcd(b % a, a);
}

// Function to return the LCM of
// Fib(a) and Fib(a)
static int findLCMFibonacci(int a, int b)
{
    return (fib(a) * fib(b)) / fib(gcd(a, b));
}

// Driver code
public static void main(String args[])
{
    int a = 3, b = 12;

    System.out.println(findLCMFibonacci(a, b));
}
}

// This code is contributed by
// Surendra_Gangwar
```

## 蟒蛇 3

```
# Python 3 Program to find LCM of
# Fib(a) and Fib(b)
MAX = 1000

# Create an array for memoization
f = [0] * MAX

# Function to return the n'th
# Fibonacci number using table f[].
def fib(n):

    # Base cases
    if (n == 0):
        return 0
    if (n == 1 or n == 2):
        f[n] = 1
        return f[n]

    # If fib(n) is already computed
    if (f[n]):
        return f[n]

    k = (n + 1) // 2 if (n & 1) else n // 2

    # Applying recursive formula
    # Note value n&1 is 1
    # if n is odd, else 0.
    if (n & 1):
        f[n] = (fib(k) * fib(k) +
                fib(k - 1) * fib(k - 1))
    else:
        f[n] = (2 * fib(k - 1) + fib(k)) * fib(k)

    return f[n]

# Function to return gcd of a and b
def gcd(a, b):
    if (a == 0):
        return b

    return gcd(b % a, a)

# Function to return the LCM of
# Fib(a) and Fib(a)
def findLCMFibonacci(a, b):

    return (fib(a) * fib(b)) // fib(gcd(a, b))

# Driver code
if __name__ == "__main__":
    a = 3
    b = 12

    print (findLCMFibonacci(a, b))

# This code is contributed by ita_c
```

## C#

```
// C# program to find LCM of Fib(a)
// and Fib(b)
using System;

class GFG
{

static int MAX = 1000;

// Create an array for memoization
static int[] f = new int[MAX];

// Function to return the n'th Fibonacci
// number using table f[].
static int fib(int n)
{
    // Base cases
    if (n == 0)
        return 0;
    if (n == 1 || n == 2)
        return (f[n] = 1);

    // If fib(n) is already computed
    if (f[n] != 0)
        return f[n];
    int k = 0;
    if ((n & 1) != 0)
        k = (n + 1) / 2;
    else
        k = n / 2;

    // Applying recursive formula
    // Note value n&1 is 1
    // if n is odd, else 0.
    if((n & 1 ) != 0)
        f[n] = (fib(k) * fib(k) +
                fib(k - 1) * fib(k - 1));
    else
        f[n] = (2 * fib(k - 1) +
                    fib(k)) * fib(k);

    return f[n];
}

// Function to return gcd of a and b
static int gcd(int a, int b)
{
    if (a == 0)
        return b;

    return gcd(b % a, a);
}

// Function to return the LCM of
// Fib(a) and Fib(a)
static int findLCMFibonacci(int a, int b)
{
    return (fib(a) * fib(b)) / fib(gcd(a, b));
}

// Driver code
static void Main()
{
    int a = 3, b = 12;

    Console.WriteLine(findLCMFibonacci(a, b));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find LCM of Fib(a)
// and Fib(b)

$GLOBALS['MAX'] = 1000;

// Create an array for memoization
$GLOBALS['f'] = array();

for($i = 0; $i < $GLOBALS['MAX']; $i++)
    $GLOBALS['f'][$i] = 0;

// Function to return the n'th Fibonacci
// number using table f[].
function fib($n)
{
    // Base cases
    if ($n == 0)
        return 0;
    if ($n == 1 || $n == 2)
        return ($GLOBALS['f'][$n] = 1);

    // If fib(n) is already computed
    if ($GLOBALS['f'][$n])
        return $GLOBALS['f'][$n];

    $k = ($n & 1) ? ($n + 1) / 2 : $n / 2;

    // Applying recursive formula
    // Note value n&1 is 1
    // if n is odd, else 0.
    $GLOBALS['f'][$n] = ($n & 1) ?
                        (fib($k) * fib($k) +
                         fib($k - 1) * fib($k - 1)) :
                        (2 * fib($k - 1) + fib($k)) * fib($k);

    return $GLOBALS['f'][$n];
}

// Function to return gcd of a and b
function gcd($a, $b)
{
    if ($a == 0)
        return $b;

    return gcd($b % $a, $a);
}

// Function to return the LCM of
// Fib(a) and Fib(a)
function findLCMFibonacci($a, $b)
{
    return (fib($a) * fib($b)) /
            fib(gcd($a, $b));
}

// Driver code
$a = 3;
$b = 12;

echo findLCMFibonacci($a, $b);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
// Javascript program to find LCM of Fib(a)
// and Fib(b)

let MAX = 1000;

// Create an array for memoization
let f = new Array(MAX);
for(let i=0;i<MAX;i++)
{
    f[i]=0;
}

// Function to return the n'th Fibonacci
// number using table f[].
function fib(n)
{
    // Base cases
    if (n == 0)
        return 0;
    if (n == 1 || n == 2)
        return (f[n] = 1);

    // If fib(n) is already computed
    if (f[n] != 0)
        return f[n];
    let k = 0;
    if ((n & 1) != 0)
        k = (n + 1) / 2;
    else
        k = n / 2;

    // Applying recursive formula
    // Note value n&1 is 1
    // if n is odd, else 0.
    if((n & 1 ) != 0)
        f[n] = (fib(k) * fib(k) +
                fib(k - 1) * fib(k - 1));
    else
        f[n] = (2 * fib(k - 1) +
                    fib(k)) * fib(k);

    return f[n];
}

// Function to return gcd of a and b
function gcd(a,b)
{
    if (a == 0)
        return b;

    return gcd(b % a, a);
}

// Function to return the LCM of
// Fib(a) and Fib(a)
function findLCMFibonacci(a,b)
{
    return (fib(a) * fib(b)) / fib(gcd(a, b));
}

// Driver code
let a = 3, b = 12;
document.write(findLCMFibonacci(a, b));

// This code is contributed by rag2127
</script>
```

**Output:** 

```
144
```