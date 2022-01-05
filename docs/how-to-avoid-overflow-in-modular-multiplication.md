# 模乘中如何避免溢出？

> 原文:[https://www . geeksforgeeks . org/如何避免模乘溢出/](https://www.geeksforgeeks.org/how-to-avoid-overflow-in-modular-multiplication/)

下面考虑一下**简单的**两个数相乘的方法。

## C

```
// A Simple solution that causes overflow when
// value of (a % mod) * (b % mod) becomes more than
// maximum value of long long int
#define ll long long

ll multiply(ll a, ll b, ll mod)
{
   return ((a % mod) * (b % mod)) % mod;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Simple solution that causes overflow when
// value of (a % mod) * (b % mod) becomes more than
// maximum value of long int

static long multiply(long a, long b, long mod)
{
   return ((a % mod) * (b % mod)) % mod;
}

// This code contributed by gauravrajput1
```

## java 描述语言

```
<script>

function multiply(a,b,mod)
{
    return ((a % mod) * (b % mod)) % mod;
}

// This code is contributed by rag2127
</script>
```

当乘法不会导致溢出时，上述函数工作正常。但是如果输入的数字使得乘法的结果超过最大极限。
例如，当 mod = 10 <sup>11</sup> ，a = 9223372036854775807 ( [最大长长 int](https://en.wikipedia.org/wiki/9223372036854775807) )和 b = 9223372036854775807 ( [最大长 int](https://en.wikipedia.org/wiki/9223372036854775807) )时，上述方法失败。请注意，可能会有较小的值失败。更小的值可以有更多的例子。事实上，任何一组值的乘法都可能导致一个值大于最大极限。
**如何避免溢出？**
我们可以递归乘法来克服溢出的困难。要乘以 a*b，首先计算 a*b/2，然后将其相加两次。用于计算 a*b/2 计算 a*b/4 等等(类似于[对数 n 次幂运算算法](https://www.geeksforgeeks.org/modular-exponentiation-power-in-modular-arithmetic/))。

```
// To compute (a * b) % mod
multiply(a,  b, mod)
1)  ll res = 0; // Initialize result
2)  a = a % mod.
3)  While (b > 0)
        a) If b is odd, then add 'a' to result.
               res = (res + a) % mod
        b) Multiply 'a' with 2
           a = (a * 2) % mod
        c) Divide 'b' by 2
           b = b/2  
4)  Return res 
```

下面是实现。

## C++

```
// C++ program for modular multiplication without
// any overflow
#include<iostream>
using namespace std;

typedef long long int ll;

// To compute (a * b) % mod
ll mulmod(ll a, ll b, ll mod)
{
    ll res = 0; // Initialize result
    a = a % mod;
    while (b > 0)
    {
        // If b is odd, add 'a' to result
        if (b % 2 == 1)
            res = (res + a) % mod;

        // Multiply 'a' with 2
        a = (a * 2) % mod;

        // Divide b by 2
        b /= 2;
    }

    // Return result
    return res % mod;
}

// Driver program
int main()
{
   ll a = 9223372036854775807, b = 9223372036854775807;
   cout << mulmod(a, b, 100000000000);
   return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for modular multiplication 
// without any overflow

class GFG
{

    // To compute (a * b) % mod
    static long mulmod(long a, long b,
                            long mod)
    {
        long res = 0; // Initialize result
        a = a % mod;
        while (b > 0)
        {
            // If b is odd, add 'a' to result
            if (b % 2 == 1)
            {
                res = (res + a) % mod;
            }

            // Multiply 'a' with 2
            a = (a * 2) % mod;

            // Divide b by 2
            b /= 2;
        }

        // Return result
        return res % mod;
    }

    // Driver code
    public static void main(String[] args)
    {

        long a = 9223372036854775807L, b = 9223372036854775807L;
        System.out.println(mulmod(a, b, 100000000000L));
    }
}

// This code is contributed by Rajput-JI
```

## 蟒蛇 3

```
# Python3 program for modular multiplication
# without any overflow

# To compute (a * b) % mod
def mulmod(a, b, mod):

    res = 0; # Initialize result
    a = a % mod;
    while (b > 0):

        # If b is odd, add 'a' to result
        if (b % 2 == 1):
            res = (res + a) % mod;

        # Multiply 'a' with 2
        a = (a * 2) % mod;

        # Divide b by 2
        b //= 2;

    # Return result
    return res % mod;

# Driver Code
a = 9223372036854775807;
b = 9223372036854775807;
print(mulmod(a, b, 100000000000));

# This code is contributed by mits
```

## C#

```
// C# program for modular multiplication
// without any overflow
using System;

class GFG
{

// To compute (a * b) % mod
static long mulmod(long a, long b, long mod)
{
    long res = 0; // Initialize result
    a = a % mod;
    while (b > 0)
    {
        // If b is odd, add 'a' to result
        if (b % 2 == 1)
        {
            res = (res + a) % mod;
        }

        // Multiply 'a' with 2
        a = (a * 2) % mod;

        // Divide b by 2
        b /= 2;
    }

    // Return result
    return res % mod;
}

// Driver code
public static void Main(String[] args)
{
    long a = 9223372036854775807L,
         b = 9223372036854775807L;
    Console.WriteLine(mulmod(a, b, 100000000000L));
}
}

// This code is contributed by 29AjayKumar
```

**输出:**

```
84232501249
```

感谢乌卡什·特里维迪提出上述解决方案。
发现有不正确的地方请写评论，或者想分享更多以上讨论话题的信息