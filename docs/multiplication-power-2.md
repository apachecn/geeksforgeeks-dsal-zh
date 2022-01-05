# 2 次方乘法

> 原文:[https://www.geeksforgeeks.org/multiplication-power-2/](https://www.geeksforgeeks.org/multiplication-power-2/)

给定两个数字 x 和 n，我们需要将 x 乘以 2 <sup>n</sup>
**示例:**

```
Input  : x = 25, n = 3
Output : 200
25 multiplied by 2 raised to power 3
is 200.

Input : x = 70, n = 2
Output : 280

```

一个**简单的解决方案**是计算 2 的 n 次幂，然后乘以 x。

## C++

```
// Simple C/C++ program
// to compute x * (2^n)
#include <bits/stdc++.h>
using namespace std;
typedef long long int ll;

// Returns 2 raised to power n
ll power2(ll n)
{
    if (n == 0)
        return 1;

    if (n == 1)
        return 2;

    return power2(n / 2) *
                    power2(n / 2);
}

ll multiply(ll x, ll n)
{
    return x * power2(n);
}

// Driven program
int main()
{
    ll x = 70, n = 2;
    cout<<multiply(x, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Simple Java program
// to compute x * (2^n)
import java.util.*;

class GFG {

    // Returns 2 raised to power n
    static long power2(long n)
    {
        if (n == 0)
            return 1;

        if (n == 1)
            return 2;

        return power2(n / 2)
                          * power2(n / 2);
    }

    static long multiply(long x, long n)
    {
        return x * power2(n);
    }

    /* Driver program */
    public static void main(String[] args)
    {
        long x = 70, n = 2;

        System.out.println(multiply(x, n));
    }
}

// This code is contributed by Arnav Kr. Mandal.   
```

## 蟒蛇 3

```
# Simple Python program
# to compute x * (2^n)

# Returns 2 raised to power n
def power2(n):

    if (n == 0):
        return 1
    if (n == 1):
        return 2
    return power2(n / 2) *
                  power2(n / 2);

def multiply(x, n):
    return x * power2(n);

# Driven program
x = 70
n = 2
print(multiply(x, n))

# This code is contributed by Smitha Dinesh Semwal
```

## C#

```
// Simple C# program
// to compute x * (2^n)
using System;

class GFG {

    // Returns 2 raised to power n
    static long power2(long n)
    {
        if (n == 0)
            return 1;

        if (n == 1)
            return 2;

        return power2(n / 2)
                        * power2(n / 2);
    }

    static long multiply(long x, long n)
    {
        return x * power2(n);
    }

    /* Driver program */
    public static void Main()
    {
        long x = 70, n = 2;

        Console.WriteLine(multiply(x, n));
    }
}

// This code is contributed by Vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Simple PHP program
// to compute x * (2^n)

// Returns 2 raised to power n
function power2($n)
{
    if ($n == 0)
        return 1;

    if ($n == 1)
        return 2;

    return power2($n / 2) *
           power2($n / 2);
}

function multiply( $x, $n)
{
    return $x * power2($n);
}

// Driver Code
$x = 70; $n = 2;
echo multiply($x, $n);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Simple JavaScript program
// to compute x * (2^n)

// Returns 2 raised to power n
function power2(n)
{
    if (n == 0)
        return 1;

    if (n == 1)
        return 2;

    return power2(n / 2) *
        power2(n / 2);
}

function multiply( x, n)
{
    return x * power2(n);
}

// Driver Code
let x = 70
let n = 2;
document.write( multiply(x, n));

// This code is contributed by mohan

</script>
```

**输出:**

```
280
```

**时间复杂度:** O(Log n)
一个**高效的解决方案**是使用[按位左移位运算符](https://www.geeksforgeeks.org/interesting-facts-bitwise-operators-c/)。我们知道 1<T9【n】表示 2 的幂 n

## C++

```
// Efficient C/C++ program to compute x * (2^n)
#include <stdio.h>
typedef long long int ll;

ll multiply(ll x, ll n)
{
    return x << n;
}

// Driven program to check above function
int main()
{
    ll x = 70, n = 2;
    printf("%lld", multiply(x, n));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA Code for Multiplication with a
// power of 2
import java.util.*;

class GFG {

    static long multiply(long x, long n)
    {
        return x << n;
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        long x = 70, n = 2;
        System.out.println(multiply(x, n));
    }
}

//This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# Efficient Python3 code to compute x * (2^n)

def multiply( x , n ):
    return x << n

# Driven code to check above function
x = 70
n = 2
print( multiply(x, n))

# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```
// C# Code for Multiplication with a
// power of 2
using System;

class GFG {

    static int multiply(int x, int n)
    {
        return x << n;
    }

    /* Driver program to test above function */
    public static void Main()
    {
        int x = 70, n = 2;

        Console.WriteLine(multiply(x, n));
    }
}

//This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Efficient PHP program to compute x * (2^n)

function multiply($x, $n)
{
    return $x << $n;
}

    // Driver Code
    $x = 70;
    $n = 2;
    echo multiply($x, $n);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Efficient JavaScript program to compute x * (2^n)

function multiply(x, n)
{
    return x << n;
}

    // Driver Code
    let x = 70;
    let n = 2;
    document.write(multiply(x, n));

// This code is contributed by mohan

</script>
```

**输出:**

```
280
```

时间复杂度:O(1)