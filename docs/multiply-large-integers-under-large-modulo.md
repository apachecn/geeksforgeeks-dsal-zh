# 大模下乘大整数

> 原文:[https://www . geesforgeks . org/乘大整数下大模/](https://www.geeksforgeeks.org/multiply-large-integers-under-large-modulo/)

给定一个整数 a，b，m，求(a * b ) mod m，其中 a，b 可能很大，它们的直接相乘可能会导致溢出。但是，它们小于允许的最大 long long int 值的一半。

**示例:**

```
Input: a = 426, b = 964, m = 235
Output: 119
Explanation: (426 * 964) % 235  
            = 410664 % 235
            = 119

Input: a = 10123465234878998, 
       b = 65746311545646431
       m = 10005412336548794 
Output: 4652135769797794
```

一种**幼稚的**方法是使用任意精度的数据类型，比如 python 中的 **int** 或者 Java 中的[T5】big integer](https://www.geeksforgeeks.org/biginteger-class-in-java/)类。但是这种方法不会有成效，因为将字符串内部转换为 int 然后执行运算会导致二进制数系统中加法和乘法的计算速度变慢。

**高效解:**由于 a 和 b 可能是非常大的数字，如果我们试图直接相乘，那么它肯定会溢出。因此，我们使用乘法的基本方法，即
a * b = a + a + … + a (b 乘以)
这样我们可以很容易地计算加法的值(在模 m 下),而在计算中没有任何
溢出。但是如果我们试图将 **a** 的值重复增加到 **b** 次，那么对于 b 的大值，它肯定会超时，因为这种方法的时间复杂度会变成 O(b)。

所以我们以更简单的方式将上面重复的步骤**划分为**，即，

```
If b is even then 
  a * b = 2 * a * (b / 2), 
otherwise 
  a * b = a + a * (b - 1)
```

以下是描述上述解释的方法:

## C++

```
// C++ program of finding modulo multiplication
#include<bits/stdc++.h>

using namespace std;

// Returns (a * b) % mod
long long moduloMultiplication(long long a,
                            long long b,
                            long long mod)
{
    long long res = 0; // Initialize result

    // Update a if it is more than
    // or equal to mod
    a %= mod;

    while (b)
    {
        // If b is odd, add a with result
        if (b & 1)
            res = (res + a) % mod;

        // Here we assume that doing 2*a
        // doesn't cause overflow
        a = (2 * a) % mod;

        b >>= 1; // b = b / 2
    }

    return res;
}

// Driver program
int main()
{
    long long a = 426;
    long long b = 964;
    long long m = 235;
    cout << moduloMultiplication(a, b, m);
    return 0;
}

// This code is contributed
// by Akanksha Rai
```

## C

```
// C program of finding modulo multiplication
#include<stdio.h>

// Returns (a * b) % mod
long long moduloMultiplication(long long a,
                               long long b,
                               long long mod)
{
    long long res = 0;  // Initialize result

    // Update a if it is more than
    // or equal to mod
    a %= mod;

    while (b)
    {
        // If b is odd, add a with result
        if (b & 1)
            res = (res + a) % mod;

        // Here we assume that doing 2*a
        // doesn't cause overflow
        a = (2 * a) % mod;

        b >>= 1;  // b = b / 2
    }

    return res;
}

// Driver program
int main()
{
    long long a = 10123465234878998;
    long long b = 65746311545646431;
    long long m = 10005412336548794;
    printf("%lld", moduloMultiplication(a, b, m));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of finding modulo multiplication
class GFG
{

    // Returns (a * b) % mod
    static long moduloMultiplication(long a,
                            long b, long mod)
    {

        // Initialize result
        long res = 0; 

        // Update a if it is more than
        // or equal to mod
        a %= mod;

        while (b > 0)
        {

            // If b is odd, add a with result
            if ((b & 1) > 0)
            {
                res = (res + a) % mod;
            }

            // Here we assume that doing 2*a
            // doesn't cause overflow
            a = (2 * a) % mod;

            b >>= 1; // b = b / 2
        }
        return res;
    }

    // Driver code
    public static void main(String[] args)
    {
        long a = 10123465234878998L;
        long b = 65746311545646431L;
        long m = 10005412336548794L;
        System.out.print(moduloMultiplication(a, b, m));
    }
}

// This code is contributed by Rajput-JI
```

## 蟒蛇 3

```
# Python 3 program of finding
# modulo multiplication

# Returns (a * b) % mod
def moduloMultiplication(a, b, mod):

    res = 0; # Initialize result

    # Update a if it is more than
    # or equal to mod
    a = a % mod;

    while (b):

        # If b is odd, add a with result
        if (b & 1):
            res = (res + a) % mod;

        # Here we assume that doing 2*a
        # doesn't cause overflow
        a = (2 * a) % mod;

        b >>= 1; # b = b / 2

    return res;

# Driver Code
a = 10123465234878998;
b = 65746311545646431;
m = 10005412336548794;
print(moduloMultiplication(a, b, m));

# This code is contributed
# by Shivi_Aggarwal
```

## C#

```
// C# program of finding modulo multiplication
using System;

class GFG
{

// Returns (a * b) % mod
static long moduloMultiplication(long a,
                            long b,
                            long mod)
{
    long res = 0; // Initialize result

    // Update a if it is more than
    // or equal to mod
    a %= mod;

    while (b > 0)
    {
        // If b is odd, add a with result
        if ((b & 1) > 0)
            res = (res + a) % mod;

        // Here we assume that doing 2*a
        // doesn't cause overflow
        a = (2 * a) % mod;

        b >>= 1; // b = b / 2
    }

    return res;
}

// Driver code
static void Main()
{
    long a = 10123465234878998;
    long b = 65746311545646431;
    long m = 10005412336548794;
    Console.WriteLine(moduloMultiplication(a, b, m));
}
}

// This code is contributed
// by chandan_jnu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
//PHP program of finding
// modulo multiplication

// Returns (a * b) % mod
function moduloMultiplication($a, $b, $mod)
{
    $res = 0; // Initialize result

    // Update a if it is more than
    // or equal to mod
    $a %= $mod;

    while ($b)
    {

        // If b is odd,
        // add a with result
        if ($b & 1)
            $res = ($res + $a) % $mod;

        // Here we assume that doing 2*a
        // doesn't cause overflow
        $a = (2 * $a) % $mod;

        $b >>= 1; // b = b / 2
    }

    return $res;
}

    // Driver Code
    $a = 10123465234878998;
    $b = 65746311545646431;
    $m = 10005412336548794;
    echo moduloMultiplication($a, $b, $m);

// This oce is contributed by ajit
?>
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Returns (a * b) % mod
function moduloMultiplication(a, b, mod)
{

    // Initialize result
    let res = 0; 

    // Update a if it is more than
    // or equal to mod
    a = (a % mod);

    while (b > 0)
    {

        // If b is odd, add a with result
        if ((b & 1) > 0)
        {
            res = (res + a) % mod;
        }

        // Here we assume that doing 2*a
        // doesn't cause overflow
        a = (2 * a) % mod;

        b = (b >> 1); // b = b / 2
    }
    return res;
}

// Driver Code
let a = 426;
let b = 964;
let m = 235;

document.write(moduloMultiplication(a, b, m));

// This code is contributed by code_hunt

</script>
```

**Output**

```
4652135769797794
```

**时间复杂度:**O(log b)
T3】辅助空间: O(1)

**注意:**只有当 **2 * m** 可以用标准数据类型表示时，上述方法才有效，否则会导致溢出。

本文由 [Shubham Bansal](https://www.facebook.com/banalshubham) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。