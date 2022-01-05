# 从 L 到 R 的所有自然数的和(对于 L 和 R 的大值)

> 原文:[https://www . geeksforgeeks . org/所有自然数的总和-从-l 到-r-对于-l 和-r 的大值/](https://www.geeksforgeeks.org/sum-of-all-natural-numbers-from-l-to-r-for-large-values-of-l-and-r/)

给定两个非常大的数字 **L** 和 **R** ，其中 **L ≤ R** ，任务是计算从 **L** 到 **R** 的所有自然数的和。金额可能很大，所以打印**金额% 100000007**。
**示例:**

> **输入:** L = "8894" R = "98592"
> **输出:** 820693329
> **输入:**L = " 88949273204 " R = " 98429729474298592 "
> **输出:** 252666158

**进场:**

*   设**和(N)** 是一个返回第一个 **N** 个自然数之和的函数。
*   第一个 **N 个**自然数之和为**和(N) = (N * (N + 1)) / 2** 。
*   **L 到 R** 范围内的数字之和将是**范围总和=总和(R)–总和(L–1)**

*   答案用模 **10 <sup>9</sup> + 7** 计算，所以，

> **mod = 10<sup>9</sup>+7**
> **range sum =(sum(R)–sum(L-1)+mod)% mod；**
> 这个也可以写成**range sum =(sum(R)% mod–sum(L-1)% mod+mod)% mod；**
> 现在， **sum(R) % mod** 可以写成 **((R * (R + 1)) / 2) % mod**
> 或**((R % mod)*((R+1)% mod)* invmod(2))% mod**
> 由于 R 较大，所以 R 的模可以按这里所述进行计算。
> 倒三角(2)的值= 500000004 ，可以用[费马小定理](https://en.wikipedia.org/wiki/Fermat%27s_little_theorem)计算。
> 同样，也可以计算**和(L–1)% mod**。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

#define mod 1000000007

// Value of inverse modulo
// 2 with 10^9 + 7
const long long inv2 = 500000004;

// Function to return num % 1000000007
// where num is a large number
long long int modulo(string num)
{
    // Initialize result
    long long int res = 0;

    // One by one process all the
    // digits of string 'num'
    for (long long int i = 0;
         i < num.length();
         i++)
        res = (res * 10
               + (long long int)num[i]
               - '0')
              % mod;
    return res;
}

// Function to return the sum of the
// integers from the given range
// modulo 1000000007
long long int findSum(string L,
                      string R)
{
    long long int a, b, l, r, ret;

    // a stores the value of
    // L modulo 10^9 + 7
    a = modulo(L);

    // b stores the value of
    // R modulo 10^9 + 7
    b = modulo(R);

    // l stores the sum of natural
    // numbers from 1 to (a - 1)
    l = ((a * (a - 1))
         % mod * inv2)
        % mod;

    // r stores the sum of natural
    // numbers from 1 to b
    r = ((b * (b + 1))
         % mod * inv2)
        % mod;

    ret = (r % mod - l % mod);

    // If the result is negative
    if (ret < 0)
        ret = ret + mod;
    else
        ret = ret % mod;
    return ret;
}

// Driver code
int main()
{
    string L = "88949273204";
    string R = "98429729474298592";

    cout << findSum(L, R) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{
static long mod = 1000000007;

// Value of inverse modulo
// 2 with 10^9 + 7
static long inv2 = 500000004;

// Function to return num % 1000000007
// where num is a large number
static long modulo(String num)
{
    // Initialize result
    long res = 0;

    // One by one process all the
    // digits of string 'num'
    for (int i = 0;
             i < num.length(); i++)
        res = (res * 10 +
              (long)num.charAt(i) - '0') % mod;
    return res;
}

// Function to return the sum of the
// longegers from the given range
// modulo 1000000007
static long findSum(String L, String R)
{
    long a, b, l, r, ret;

    // a stores the value of
    // L modulo 10^9 + 7
    a = modulo(L);

    // b stores the value of
    // R modulo 10^9 + 7
    b = modulo(R);

    // l stores the sum of natural
    // numbers from 1 to (a - 1)
    l = ((a * (a - 1)) % mod * inv2) % mod;

    // r stores the sum of natural
    // numbers from 1 to b
    r = ((b * (b + 1)) % mod * inv2) % mod;

    ret = (r % mod - l % mod);

    // If the result is negative
    if (ret < 0)
        ret = ret + mod;
    else
        ret = ret % mod;
    return ret;
}

// Driver code
public static void main(String[] args)
{
    String L = "88949273204";
    String R = "98429729474298592";

    System.out.println(findSum(L, R));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach
mod = 1000000007

# Value of inverse modulo
# 2 with 10^9 + 7
inv2 = 500000004;

# Function to return num % 1000000007
# where num is a large number
def modulo(num) :

    # Initialize result
    res = 0;

    # One by one process all the
    # digits of string 'num'
    for i in range(len(num)) :
        res = (res * 10 + int(num[i]) - 0) % mod;

    return res;

# Function to return the sum of the
# integers from the given range
# modulo 1000000007
def findSum(L, R) :

    # a stores the value of
    # L modulo 10^9 + 7
    a = modulo(L);

    # b stores the value of
    # R modulo 10^9 + 7
    b = modulo(R);

    # l stores the sum of natural
    # numbers from 1 to (a - 1)
    l = ((a * (a - 1)) % mod * inv2) % mod;

    # r stores the sum of natural
    # numbers from 1 to b
    r = ((b * (b + 1)) % mod * inv2) % mod;

    ret = (r % mod - l % mod);

    # If the result is negative
    if (ret < 0) :
        ret = ret + mod;
    else :
        ret = ret % mod;

    return ret;

# Driver code
if __name__ == "__main__" :

    L = "88949273204";
    R = "98429729474298592";

    print(findSum(L, R)) ;

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
static long mod = 1000000007;

// Value of inverse modulo
// 2 with 10^9 + 7
static long inv2 = 500000004;

// Function to return num % 1000000007
// where num is a large number
static long modulo(String num)
{
    // Initialize result
    long res = 0;

    // One by one process all the
    // digits of string 'num'
    for (int i = 0;
             i < num.Length; i++)
        res = (res * 10 +
              (long)num[i] - '0') % mod;
    return res;
}

// Function to return the sum of the
// longegers from the given range
// modulo 1000000007
static long findSum(String L, String R)
{
    long a, b, l, r, ret;

    // a stores the value of
    // L modulo 10^9 + 7
    a = modulo(L);

    // b stores the value of
    // R modulo 10^9 + 7
    b = modulo(R);

    // l stores the sum of natural
    // numbers from 1 to (a - 1)
    l = ((a * (a - 1)) % mod * inv2) % mod;

    // r stores the sum of natural
    // numbers from 1 to b
    r = ((b * (b + 1)) % mod * inv2) % mod;

    ret = (r % mod - l % mod);

    // If the result is negative
    if (ret < 0)
        ret = ret + mod;
    else
        ret = ret % mod;
    return ret;
}

// Driver code
public static void Main(String[] args)
{
    String L = "88949273204";
    String R = "98429729474298592";

    Console.WriteLine(findSum(L, R));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    let mod = 1000000007;

    // Value of inverse modulo
    // 2 with 10^9 + 7
    let inv2 = 500000004;

    // Function to return num % 1000000007
    // where num is a large number
    function modulo(num)
    {
        // Initialize result
        let res = 0;

        // One by one process all the
        // digits of string 'num'
        for (let i = 0;
                 i < num.length; i++)
            res = (res * 10 + num[i].charCodeAt() - '0'.charCodeAt()) % mod;
        return res;
    }

    // Function to return the sum of the
    // longegers from the given range
    // modulo 1000000007
    function findSum(L, R)
    {
        let a, b, l, r, ret;

        // a stores the value of
        // L modulo 10^9 + 7
        a = modulo(L);

        // b stores the value of
        // R modulo 10^9 + 7
        b = modulo(R);

        // l stores the sum of natural
        // numbers from 1 to (a - 1)
        l = ((a * (a - 1)) % mod * inv2) % mod;

        // r stores the sum of natural
        // numbers from 1 to b
        r = ((b * (b + 1)) % mod * inv2) % mod;

        ret = (r % mod - l % mod);

        // If the result is negative
        if (ret < 0)
            ret = ret + mod;
        else
            ret = ret % mod - 6;
        return ret;
    }

    let L = "88949273204";
    let R = "98429729474298592";

    document.write(findSum(L, R));

// This code is contributed by decode2207.
</script>
```

**Output:** 

```
252666158
```