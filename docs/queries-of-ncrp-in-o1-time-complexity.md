# O(1)时间复杂度中 nCr%p 的查询

> 原文:[https://www . geesforgeks . org/query-of-ncrp-in-O1-time-complexity/](https://www.geeksforgeeks.org/queries-of-ncrp-in-o1-time-complexity/)

给定 Q 个查询和 P，其中 P 是素数，每个查询有两个数字 N 和 R，任务是计算 nCr mod P
**约束:**

```
N <= 106
R <= 106
p is a prime number
```

**示例:**

> **输入:**
> Q = 2 p = 1000000007
> 第 1 次查询:N = 15，R = 4
> 第 2 次查询:N = 20，R = 3
> **输出:**
> 第 1 次查询:1365
> 第 2 次查询:1140
> 15！/(4!*(15-4)!)%1000000007 = 1365
> 20！/(20!*(20-3)!)%1000000007 = 1140

一种**天真的方法**是通过在任何时候应用模块化运算，使用[公式](https://www.geeksforgeeks.org/program-calculate-value-ncr/)计算 **nCr** 。因此时间复杂度为 0(q * n)。

一个**更好的方法**是使用[费马小定理](https://www.geeksforgeeks.org/fermats-little-theorem/)。根据它，nCr 也可以写成(n！/(r！*(n-r)！))mod 相当于 **(n！*逆(r！)*逆((n-r)！))mod p** 。因此，预计算从 1 到 n 的数字的阶乘将允许以 O(log n)回答查询。唯一需要做的计算就是计算 r 的倒数！和(n-r)！。因此整体复杂性将为 **q*( log(n))** 。

一种有效的方法是通过预先计算阶乘的倒数，将更好的方法简化为有效的方法。在 O(n)时间内预计算阶乘的倒数，然后可以在 O(1)时间内回答查询。使用[模乘逆](https://www.geeksforgeeks.org/modular-multiplicative-inverse-1-n/)，可以在 O(n)时间内计算 1 到 N 自然数的逆。使用阶乘的递归定义，可以写出以下内容:

```
n! = n * (n-1) !
taking inverse on both side 
inverse( n! ) = inverse( n ) * inverse( (n-1)! )
```

由于 N 的最大值是 10 <sup>6</sup> ，预计算到 10 <sup>6</sup> 就可以了。

下面是上述方法的实现:

## C++

```
// C++ program to answer queries
// of nCr in O(1) time.
#include <bits/stdc++.h>
#define ll long long
const int N = 1000001;
using namespace std;

// array to store inverse of 1 to N
ll factorialNumInverse[N + 1];

// array to precompute inverse of 1! to N!
ll naturalNumInverse[N + 1];

// array to store factorial of first N numbers
ll fact[N + 1];

// Function to precompute inverse of numbers
void InverseofNumber(ll p)
{
    naturalNumInverse[0] = naturalNumInverse[1] = 1;
    for (int i = 2; i <= N; i++)
        naturalNumInverse[i] = naturalNumInverse[p % i] * (p - p / i) % p;
}
// Function to precompute inverse of factorials
void InverseofFactorial(ll p)
{
    factorialNumInverse[0] = factorialNumInverse[1] = 1;

    // precompute inverse of natural numbers
    for (int i = 2; i <= N; i++)
        factorialNumInverse[i] = (naturalNumInverse[i] * factorialNumInverse[i - 1]) % p;
}

// Function to calculate factorial of 1 to N
void factorial(ll p)
{
    fact[0] = 1;

    // precompute factorials
    for (int i = 1; i <= N; i++) {
        fact[i] = (fact[i - 1] * i) % p;
    }
}

// Function to return nCr % p in O(1) time
ll Binomial(ll N, ll R, ll p)
{
    // n C r = n!*inverse(r!)*inverse((n-r)!)
    ll ans = ((fact[N] * factorialNumInverse[R])
              % p * factorialNumInverse[N - R])
             % p;
    return ans;
}

// Driver Code
int main()
{
    // Calling functions to precompute the
    // required arrays which will be required
    // to answer every query in O(1)
    ll p = 1000000007;
    InverseofNumber(p);
    InverseofFactorial(p);
    factorial(p);

    // 1st query
    ll N = 15;
    ll R = 4;
    cout << Binomial(N, R, p) << endl;

    // 2nd query
    N = 20;
    R = 3;
    cout << Binomial(N, R, p) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to answer queries
// of nCr in O(1) time
import java.io.*;

class GFG{

static int N = 1000001; 

// Array to store inverse of 1 to N
static long[] factorialNumInverse = new long[N + 1];

// Array to precompute inverse of 1! to N!
static long[] naturalNumInverse = new long[N + 1];

// Array to store factorial of first N numbers
static long[] fact = new long[N + 1];

// Function to precompute inverse of numbers
public static void InverseofNumber(int p)
{
    naturalNumInverse[0] = naturalNumInverse[1] = 1;

    for(int i = 2; i <= N; i++)
        naturalNumInverse[i] = naturalNumInverse[p % i] *
                                 (long)(p - p / i) % p;
}

// Function to precompute inverse of factorials
public static void InverseofFactorial(int p)
{
    factorialNumInverse[0] = factorialNumInverse[1] = 1;

    // Precompute inverse of natural numbers
    for(int i = 2; i <= N; i++)
        factorialNumInverse[i] = (naturalNumInverse[i] *
                           factorialNumInverse[i - 1]) % p;
}

// Function to calculate factorial of 1 to N
public static void factorial(int p)
{
    fact[0] = 1;

    // Precompute factorials
    for(int i = 1; i <= N; i++)
    {
        fact[i] = (fact[i - 1] * (long)i) % p;
    }
}

// Function to return nCr % p in O(1) time
public static long Binomial(int N, int R, int p)
{

    // n C r = n!*inverse(r!)*inverse((n-r)!)
    long ans = ((fact[N] * factorialNumInverse[R]) %
                       p * factorialNumInverse[N - R]) % p;

    return ans;
}

// Driver code
public static void main (String[] args)
{

    // Calling functions to precompute the
    // required arrays which will be required
    // to answer every query in O(1)
    int p = 1000000007;
    InverseofNumber(p);
    InverseofFactorial(p);
    factorial(p);

    // 1st query
    int n = 15;
    int R = 4;
    System.out.println(Binomial(n, R, p));

    // 2nd query
    n = 20;
    R = 3;
    System.out.println(Binomial(n, R, p));
}
}

// This code is contributed by RohitOberoi
```

## 蟒蛇 3

```
# Python3 program to answer queries
# of nCr in O(1) time.
N = 1000001

# array to store inverse of 1 to N
factorialNumInverse = [None] * (N + 1)

# array to precompute inverse of 1! to N!
naturalNumInverse = [None] * (N + 1)

# array to store factorial of
# first N numbers
fact = [None] * (N + 1)

# Function to precompute inverse of numbers
def InverseofNumber(p):
    naturalNumInverse[0] = naturalNumInverse[1] = 1
    for i in range(2, N + 1, 1):
        naturalNumInverse[i] = (naturalNumInverse[p % i] *
                                   (p - int(p / i)) % p)

# Function to precompute inverse
# of factorials
def InverseofFactorial(p):
    factorialNumInverse[0] = factorialNumInverse[1] = 1

    # precompute inverse of natural numbers
    for i in range(2, N + 1, 1):
        factorialNumInverse[i] = (naturalNumInverse[i] *
                                  factorialNumInverse[i - 1]) % p

# Function to calculate factorial of 1 to N
def factorial(p):
    fact[0] = 1

    # precompute factorials
    for i in range(1, N + 1):
        fact[i] = (fact[i - 1] * i) % p

# Function to return nCr % p in O(1) time
def Binomial(N, R, p):

    # n C r = n!*inverse(r!)*inverse((n-r)!)
    ans = ((fact[N] * factorialNumInverse[R])% p *
                      factorialNumInverse[N - R])% p
    return ans

# Driver Code
if __name__ == '__main__':

    # Calling functions to precompute the
    # required arrays which will be required
    # to answer every query in O(1)
    p = 1000000007
    InverseofNumber(p)
    InverseofFactorial(p)
    factorial(p)

    # 1st query
    N = 15
    R = 4
    print(Binomial(N, R, p))

    # 2nd query
    N = 20
    R = 3
    print(Binomial(N, R, p))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to answer queries 
// of nCr in O(1) time
using System;

class GFG{

static int N = 1000001;  

// Array to store inverse of 1 to N 
static long[] factorialNumInverse = new long[N + 1]; 

// Array to precompute inverse of 1! to N! 
static long[] naturalNumInverse = new long[N + 1];

// Array to store factorial of first N numbers 
static long[] fact = new long[N + 1]; 

// Function to precompute inverse of numbers 
static void InverseofNumber(int p) 
{ 
    naturalNumInverse[0] = naturalNumInverse[1] = 1; 

    for(int i = 2; i <= N; i++) 
        naturalNumInverse[i] = naturalNumInverse[p % i] *
                                 (long)(p - p / i) % p; 
} 

// Function to precompute inverse of factorials 
static void InverseofFactorial(int p) 
{ 
    factorialNumInverse[0] = factorialNumInverse[1] = 1; 

    // Precompute inverse of natural numbers 
    for(int i = 2; i <= N; i++) 
        factorialNumInverse[i] = (naturalNumInverse[i] * 
                            factorialNumInverse[i - 1]) % p; 
} 

// Function to calculate factorial of 1 to N 
static void factorial(int p) 
{ 
    fact[0] = 1; 

    // Precompute factorials 
    for(int i = 1; i <= N; i++)
    { 
        fact[i] = (fact[i - 1] * (long)i) % p; 
    } 
} 

// Function to return nCr % p in O(1) time 
static long Binomial(int N, int R, int p) 
{ 

    // n C r = n!*inverse(r!)*inverse((n-r)!) 
    long ans = ((fact[N] * factorialNumInverse[R]) % 
                       p * factorialNumInverse[N - R]) % p; 

    return ans; 
}

// Driver code
static void Main()
{

    // Calling functions to precompute the 
    // required arrays which will be required 
    // to answer every query in O(1) 
    int p = 1000000007; 
    InverseofNumber(p); 
    InverseofFactorial(p); 
    factorial(p); 

    // 1st query 
    int n = 15; 
    int R = 4; 
    Console.WriteLine(Binomial(n, R, p));

    // 2nd query 
    n = 20; 
    R = 3; 
    Console.WriteLine(Binomial(n, R, p));
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

// Javascript program to answer queries
// of nCr in O(1) time.
var N = 1000001;

// array to store inverse of 1 to N
factorialNumInverse = Array(N+1).fill(0);

// array to precompute inverse of 1! to N!
naturalNumInverse = Array(N+1).fill(0);

// array to store factorial of first N numbers
fact = Array(N+1).fill(0);

// Function to precompute inverse of numbers
function InverseofNumber(p)
{
    naturalNumInverse[0] = naturalNumInverse[1] = 1;
    for (var i = 2; i <= N; i++)
        naturalNumInverse[i] = (naturalNumInverse[p % i] * (p - parseInt(p / i))) % p;
}

// Function to precompute inverse of factorials
function InverseofFactorial(p)
{
    factorialNumInverse[0] = factorialNumInverse[1] = 1;

    // precompute inverse of natural numbers
    for (var i = 2; i <= N; i++)
        factorialNumInverse[i] = ((naturalNumInverse[i] * factorialNumInverse[i - 1])) % p;
}

// Function to calculate factorial of 1 to N
function factorial(p)
{
    fact[0] = 1;

    // precompute factorials
    for (var i = 1; i <= N; i++) {
        fact[i] = (fact[i - 1] * i) % p;
    }
}

// Function to return nCr % p in O(1) time
function Binomial(N, R, p)
{

    // n C r = n!*inverse(r!)*inverse((n-r)!)
    var ans = ((((fact[N] * factorialNumInverse[R])% p) * factorialNumInverse[N - R]))% p;
    return ans;
}

// Driver Code

// Calling functions to precompute the
// required arrays which will be required
// to answer every query in O(1)
p = 100000007;
InverseofNumber(p);
InverseofFactorial(p);
factorial(p);

// 1st query
N = 15;
R = 4;
document.write(Binomial(N, R, p)+"<br>")

// 2nd query
N = 20;
R = 3;
document.write(Binomial(N, R, p));

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
1365
1140
```

**时间复杂度:** O(N)为预计算，O(1)为每个查询。
**辅助空间:** O(N)