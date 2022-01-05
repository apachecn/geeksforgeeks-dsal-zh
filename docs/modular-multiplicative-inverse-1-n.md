# 从 1 到 n 的模乘逆

> 原文:[https://www . geesforgeks . org/modular-乘法-逆-1-n/](https://www.geeksforgeeks.org/modular-multiplicative-inverse-1-n/)

给一个正整数 n，求 1 到 n 的所有整数相对于一个大质数的[模乘逆](https://www.geeksforgeeks.org/multiplicative-inverse-under-modulo-m/)，比如说‘质数’。

a 的模乘逆是一个整数“x ”,这样。

```
 a x ≡ 1 (mod prime) 
```

**示例:**

```
Input : n = 10, prime = 17
Output : 1 9 6 13 7 3 5 15 2 12
Explanation :
For 1, modular inverse is 1 as (1 * 1)%17 is 1
For 2, modular inverse is 9 as (2 * 9)%17 is 1
For 3, modular inverse is 6 as (3 * 6)%17 is 1
....... 

Input : n = 5, prime = 7
Output : 1 4 5 2 3
```

一个**简单的解决方法**就是对每个数字逐个求模逆。

## C++

```
// C++ program to find modular inverse of
// all numbers from 1 to n using naive
// method
#include<iostream>
using namespace std;

// A naive method to find modular
// multiplicative inverse of 'a'
// under modulo 'prime'
int modInverse(int a, int prime)
{
    a = a % prime;
    for (int x=1; x<prime; x++)
       if ((a*x) % prime == 1)
          return x;

    return -1;
}

void printModIverses(int n, int prime)
{
    for (int i=1; i<=n; i++)
      cout << modInverse(i, prime) << " ";
}

// Driver Program
int main()
{
    int n = 10, prime = 17;
    printModIverses(n, prime);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find modular inverse of
// all numbers from 1 to n using naive
// method
import java.io.*;

class GFG {

    // A naive method to find modular
    // multiplicative inverse of 'a'
    // under modulo 'prime'
    static int modInverse(int a, int prime)
    {
        a = a % prime;
        for (int x = 1; x  <prime; x++)
        if ((a * x) % prime == 1)
            return x;

        return -1;
    }

    static void printModIverses(int n, int prime)
    {
        for (int i = 1; i <= n; i++)
        System.out.print(modInverse(i, prime) + " ");
    }

    // Driver Program
    public static void main(String args[])
    {
        int n = 10, prime = 17;
        printModIverses(n, prime);
    }
}

// This code is contributed by Nikita Tiwari.
```

## 蟒蛇 3

```
# Python 3 program to find
# modular inverse of
# all numbers from 1
# to n using naive
# method

# A naive method to find modular
# multiplicative inverse of 'a'
# under modulo 'prime'

def modInverse(a, prime) :
    a = a % prime
    for x in range(1,prime) :
        if ((a*x) % prime == 1) :
            return x

    return -1

def printModIverses(n, prime) :
    for i in range(1,n+1) :
        print( modInverse(i, prime) ,end= " ")

# Driver Program
n = 10
prime = 17

printModIverses(n, prime)

# This code is contributed
# by Nikita Tiwari.
```

## C#

```
// C# program to find modular inverse of
// all numbers from 1 to n using naive
// method
using System;

class GFG {

    // A naive method to find modular
    // multiplicative inverse of 'a'
    // under modulo 'prime'
    static int modInverse(int a, int prime)
    {
        a = a % prime;
        for (int x = 1; x <prime; x++)
            if ((a * x) % prime == 1)
                return x;

        return -1;
    }

    static void printModIverses(int n, int prime)
    {
        for (int i = 1; i <= n; i++)
            Console.Write(modInverse(i, prime) + " ");
    }

    // Driver Program
    public static void Main()
    {
        int n = 10, prime = 17;

        printModIverses(n, prime);
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find modular inverse of
// all numbers from 1 to n using naive
// method

// A naive method to find modular
// multiplicative inverse of 'a'
// under modulo 'prime'
function modInverse(int $a, int $prime)
{
    $a = $a % $prime;
    for ( $x = 1; $x < $prime; $x++)
    if (($a * $x) % $prime == 1)
        return $x;

    return -1;
}

function printModIverses( $n, $prime)
{
    for ( $i = 1; $i <= $n; $i++)
    echo modInverse($i, $prime) , " ";
}

// Driver Program

    $n = 10; $prime = 17;
    printModIverses($n, $prime);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Javascript program to find modular
// inverse of all numbers from 1 to n
// using naive method

// A naive method to find modular
// multiplicative inverse of 'a'
// under modulo 'prime'
function modInverse(a, prime)
{
    a = a % prime;

    for(let x = 1; x < prime; x++)
        if ((a * x) % prime == 1)
            return x;

    return -1;
}

function printModIverses( n, prime)
{
    for(let i = 1; i <= n; i++)
        document.write(modInverse(i, prime) + " ");
}

// Driver code
let n = 10;
let prime = 17;

printModIverses(n, prime);

// This code is contributed by _saurabh_jaiswal

</script>
```

**输出:**

```
1 9 6 13 7 3 5 15 2 12
```

一个**高效的解决方案**是基于[扩展欧几里德算法](https://www.geeksforgeeks.org/euclidean-algorithms-basic-and-extended/)。
扩展欧几里德算法找到整数系数 x 和 y，从而:

```
  ax + by = gcd(a, b)

Let us put b = prime, we get
  ax + prime * y = gcd(a, prime)

We know gcd(a, prime) = 1 because
on of the numbers is prime. So we
know
  ax + prime * y = 1

Since prime * y is a multiple of prime,
x is modular multiplicative inverse of a.

 ax  ≡ 1 (mod prime) 

```

我们可以使用下面的表达式递归地找到 x(详见[扩展欧几里德算法](https://www.geeksforgeeks.org/euclidean-algorithms-basic-and-extended/))。
扩展欧氏算法使用递归调用 gcd(b%a，a)计算的结果更新 gcd(a，b)的结果。让递归调用计算的 x 和 y 的值为 x <sub>prev</sub> 和 y <sub>prev</sub> 。使用以下表达式更新 x 和 y。

```
x = yprev - ⌊prime/a⌋ * xprev
y = xprev
```

我们使用上面的关系来使用先前计算的值计算逆。

```
inverse(a) = (inverse(prime % a) *
              (prime - prime/a)) % prime
```

我们使用使用上述递归结构的动态编程方法。
**动态进场:**
dp[1] = 1、
DP[2]= DP[17% 2]*(17-17/2)% 17 = 9
DP[3]= DP[17% 3]*(17-17/3)% 17 = 6
以此类推..

## C++

```
// CPP code to find modular inverse
// from 1 to n w.r.t a big prime number
#include <iostream>
using namespace std;

// Function to calculate modular
// inverse using D.P
void modularInverse(int n, int prime)
{
    int dp[n + 1];
    dp[0] = dp[1] = 1;
    for (int i = 2; i <= n; i++)
        dp[i] = dp[prime % i] *
               (prime - prime / i) % prime;   

    for (int i = 1; i <= n; i++)
        cout << dp[i] << ' ';   
}

// Driver code
int main()
{
    int n = 10, prime = 17;
    modularInverse(n, prime);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find modular inverse
// from 1 to n w.r.t a big prime number
import java.io.*;

class GFG {

    // Function to calculate modular
    // inverse using D.P
    static void modularInverse(int n, int prime)
    {
        int dp[]=new int[n + 1];
        dp[0] = dp[1] = 1;
        for (int i = 2; i <= n; i++)
            dp[i] = dp[prime % i] *
                (prime - prime / i) % prime;

        for (int i = 1; i <= n; i++)
            System.out.print(dp[i] + " ");
    }

    // Driver Program
    public static void main(String args[])
    {
        int n = 10, prime = 17;
        modularInverse(n, prime);
    }
}

// This code is contributed by Nikita Tiwari.
```

## 蟒蛇 3

```
# Python 3 code to find
# modular inverse
# from 1 to n w.r.t a
# big prime number

# Function to calculate modular
# inverse using D.P
def modularInverse( n, prime) :

    dp =[0]*(n+1)
    dp[0] = dp[1] = 1
    for i in range( 2, n+1) :
        dp[i] = dp[prime % i] *(prime - prime // i) % prime

    for i in range( 1, n+1) :
        print(dp[i] ,end=" ")

# Driver code
n = 10
prime = 17

modularInverse(n, prime)

# This code is contributed
# by Nikita Tiwari.
```

## C#

```
// C# code to find modular inverse
// from 1 to n w.r.t a big prime number
using System;

class GFG {

    // Function to calculate modular
    // inverse using D.P
    static void modularInverse(int n, int prime)
    {
        int []dp=new int[n + 1];
        dp[0] = dp[1] = 1;

        for (int i = 2; i <= n; i++)
            dp[i] = dp[prime % i] *
                (prime - prime / i) % prime;

        for (int i = 1; i <= n; i++)
            Console.Write(dp[i] + " ");
    }

    // Driver Program
    public static void Main()
    {
        int n = 10, prime = 17;

        modularInverse(n, prime);
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to find modular
// inverse from 1 to n w.r.t
// a big prime number

// Function to calculate
// modular inverse using D.P
function modularInverse($n, $prime)
{
    $dp = array();
    $dp[0] = $dp[1] = 1;
    for ($i = 2; $i <= $n; $i++)
        $dp[$i] = $dp[$prime % $i] *
                     ($prime -
               intval($prime / $i)) %
                      $prime;

    for ($i = 1; $i <= $n; $i++)
        echo ($dp[$i].' ');
}

// Driver code
$n = 10; $prime = 17;
modularInverse($n, $prime);

// This code is contributed by
// Manish Shaw(manishshaw1)
?>
```

## java 描述语言

```
<script>

// Javascript code to find modular
// inverse from 1 to n w.r.t
// a big prime number

// Function to calculate
// modular inverse using D.P
function modularInverse(n, prime)
{
    let dp = [];
    dp[0] = dp[1] = 1;

    for(let i = 2; i <= n; i++)
        dp[i] = dp[prime % i] * (prime -
         parseInt(prime / i)) % prime;

    for(let i = 1; i <= n; i++)
        document.write(dp[i] + ' ');
}

// Driver code
let n = 10;
let prime = 17;

modularInverse(n, prime);

// This code is contributed by _saurabh_jaiswal

</script>
```

**输出:**

```
1 9 6 13 7 3 5 15 2 12
```

**时间复杂度:**O(n)
T3】辅助空间: O(n)