# 模乘逆

> 原文:[https://www . geeksforgeeks . org/乘法-逆-下模-m/](https://www.geeksforgeeks.org/multiplicative-inverse-under-modulo-m/)

给定两个整数‘a’和‘m’，求模‘m’下‘a’的模乘逆。
模乘逆是一个整数‘x’，这样。

```
a x ≅ 1 (mod m)
```

x 的值应该在{ 1，2，… m-1}内，即在整数模 m 的范围内(注意 x 不能为 0 作为*0 mod m 永远不会为 1 )
当且仅当 a 和 m 相对素数(即 gcd(a，m) = 1)时，“a 模 m”的乘法逆存在。

**示例:**

```
Input:  a = 3, m = 11
Output: 4
Since (4*3) mod 11 = 1, 4 is modulo inverse of 3(under 11).
One might think, 15 also as a valid output as "(15*3) mod 11" 
is also 1, but 15 is not in ring {1, 2, ... 10}, so not 
valid.

Input:  a = 10, m = 17
Output: 12
Since (10*12) mod 17 = 1, 12 is modulo inverse of 10(under 17).
```

**方法 1(天真)**
天真的方法是尝试从 1 到 m 的所有数字，对于每个数字 x，检查(a*x)%m 是否为 1。

下面是这个方法的实现。

## C++

```
// C++ program to find modular
// inverse of a under modulo m
#include <iostream>
using namespace std;

// A naive method to find modular
// multiplicative inverse of 'a'
// under modulo 'm'
int modInverse(int a, int m)
{
    for (int x = 1; x < m; x++)
        if (((a%m) * (x%m)) % m == 1)
            return x;
}

// Driver code
int main()
{
    int a = 3, m = 11;

    // Function call
    cout << modInverse(a, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find modular inverse
// of a under modulo m
import java.io.*;

class GFG {

    // A naive method to find modulor
    // multiplicative inverse of 'a'
    // under modulo 'm'
    static int modInverse(int a, int m)
    {

        for (int x = 1; x < m; x++)
            if (((a%m) * (x%m)) % m == 1)
                return x;
        return 1;
    }

    // Driver Code
    public static void main(String args[])
    {
        int a = 3, m = 11;

        // Function call
        System.out.println(modInverse(a, m));
    }
}

/*This code is contributed by Nikita Tiwari.*/
```

## 蟒蛇 3

```
# Python3 program to find modular
# inverse of a under modulo m

# A naive method to find modulor
# multiplicative inverse of 'a'
# under modulo 'm'

def modInverse(a, m):

    for x in range(1, m):
        if (((a%m) * (x%m)) % m == 1):
            return x
    return -1

# Driver Code
a = 3
m = 11

# Function call
print(modInverse(a, m))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to find modular inverse
// of a under modulo m
using System;

class GFG {

    // A naive method to find modulor
    // multiplicative inverse of 'a'
    // under modulo 'm'
    static int modInverse(int a, int m)
    {

        for (int x = 1; x < m; x++)
            if (((a%m) * (x%m)) % m == 1)
                return x;
        return 1;
    }

    // Driver Code
    public static void Main()
    {
        int a = 3, m = 11;

        // Function call
        Console.WriteLine(modInverse(a, m));
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<≅php
// PHP program to find modular
// inverse of a under modulo m

// A naive method to find modulor
// multiplicative inverse of
// 'a' under modulo 'm'
function modInverse( $a, $m)
{

    for ($x = 1; $x < $m; $x++)
        if ((($a%$m) * ($x%$m)) % $m == 1)
            return $x;
}

    // Driver Code
    $a = 3;
    $m = 11;

    // Function call
    echo modInverse($a, $m);

// This code is contributed by anuj_67.
≅>
```

## java 描述语言

```
<script>

// Javascript program to find modular
// inverse of a under modulo m

// A naive method to find modulor
// multiplicative inverse of
// 'a' under modulo 'm'
function modInverse(a, m)
{
    for(let x = 1; x < m; x++)
        if (((a % m) * (x % m)) % m == 1)
            return x;
}

// Driver Code
let a = 3;
let m = 11;

// Function call
document.write(modInverse(a, m));

// This code is contributed by _saurabh_jaiswal.

</script>
```

**Output**

```
4
```

**时间复杂度:** O(m)。

**方法 2(当 m 和 a 是互素时有效)**
想法是使用 [**扩展欧几里德算法**](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) ，该算法采用两个整数‘a’和‘b’，找到它们的 gcd，还找到‘x’和‘y ’,这样

```
ax + by = gcd(a, b)
```

为了在“m”下找到“a”的乘法逆，我们在上面的公式中放入了 b = m。既然我们知道 a 和 m 是相对素数，我们可以把 gcd 的值设为 1。

```
ax + my = 1
```

如果我们在两边取模 m，我们得到

```
ax + my ≅ 1 (mod m)
```

我们可以去掉左边的第二项，因为“my (mod m)”对于整数 y 总是 0。

```
ax  ≅ 1 (mod m)
```

所以我们可以用[扩展欧几里德算法](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/)找到的“x”是“a”的乘法逆

下面是上述算法的实现。

## C++

```
// C++ program to find multiplicative modulo
// inverse using Extended Euclid algorithm.
#include <iostream>
using namespace std;

// Function for extended Euclidean Algorithm
int gcdExtended(int a, int b, int* x, int* y);

// Function to find modulo inverse of a
void modInverse(int a, int m)
{
    int x, y;
    int g = gcdExtended(a, m, &x, &y);
    if (g != 1)
        cout << "Inverse doesn't exist";
    else
    {

        // m is added to handle negative x
        int res = (x % m + m) % m;
        cout << "Modular multiplicative inverse is " << res;
    }
}

// Function for extended Euclidean Algorithm
int gcdExtended(int a, int b, int* x, int* y)
{

    // Base Case
    if (a == 0)
    {
        *x = 0, *y = 1;
        return b;
    }

    // To store results of recursive call
    int x1, y1;
    int gcd = gcdExtended(b % a, a, &x1, &y1);

    // Update x and y using results of recursive
    // call
    *x = y1 - (b / a) * x1;
    *y = x1;

    return gcd;
}

// Driver Code
int main()
{
    int a = 3, m = 11;

    // Function call
    modInverse(a, m);
    return 0;
}

// This code is contributed by khushboogoyal499
```

## C

```
// C program to find multiplicative modulo inverse using
// Extended Euclid algorithm.
#include <stdio.h>

// C function for extended Euclidean Algorithm
int gcdExtended(int a, int b, int* x, int* y);

// Function to find modulo inverse of a
void modInverse(int a, int m)
{
    int x, y;
    int g = gcdExtended(a, m, &x, &y);
    if (g != 1)
        printf("Inverse doesn't exist");
    else
    {
        // m is added to handle negative x
        int res = (x % m + m) % m;
        printf("Modular multiplicative inverse is %d", res);
    }
}

// C function for extended Euclidean Algorithm
int gcdExtended(int a, int b, int* x, int* y)
{
    // Base Case
    if (a == 0)
    {
        *x = 0, *y = 1;
        return b;
    }

    int x1, y1; // To store results of recursive call
    int gcd = gcdExtended(b % a, a, &x1, &y1);

    // Update x and y using results of recursive
    // call
    *x = y1 - (b / a) * x1;
    *y = x1;

    return gcd;
}

// Driver Code
int main()
{
    int a = 3, m = 11;

    // Function call
    modInverse(a, m);
    return 0;
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<≅php
// PHP program to find multiplicative modulo
// inverse using Extended Euclid algorithm.
// Function to find modulo inverse of a
function modInverse($a, $m)
{
    $x = 0;
    $y = 0;
    $g = gcdExtended($a, $m, $x, $y);
    if ($g != 1)
        echo "Inverse doesn't exist";
    else
    {
        // m is added to handle negative x
        $res = ($x % $m + $m) % $m;
        echo "Modular multiplicative " .
                   "inverse is " . $res;
    }
}

// function for extended Euclidean Algorithm
function gcdExtended($a, $b, &$x, &$y)
{
    // Base Case
    if ($a == 0)
    {
        $x = 0;
        $y = 1;
        return $b;
    }

    $x1;
    $y1; // To store results of recursive call
    $gcd = gcdExtended($b%$a, $a, $x1, $y1);

    // Update x and y using results of
    // recursive call
    $x = $y1 - (int)($b/$a) * $x1;
    $y = $x1;

    return $gcd;
}

// Driver Code
$a = 3;
$m = 11;

// Function call
modInverse($a, $m);

// This code is contributed by chandan_jnu
≅>
```

**Output**

```
Modular multiplicative inverse is 4
```

**迭代实现:**

## C++

```
// Iterative C++ program to find modular
// inverse using extended Euclid algorithm
#include <bits/stdc++.h>
using namespace std;

// Returns modulo inverse of a with respect
// to m using extended Euclid Algorithm
// Assumption: a and m are coprimes, i.e.,
// gcd(a, m) = 1
int modInverse(int a, int m)
{
    int m0 = m;
    int y = 0, x = 1;

    if (m == 1)
        return 0;

    while (a > 1) {
        // q is quotient
        int q = a / m;
        int t = m;

        // m is remainder now, process same as
        // Euclid's algo
        m = a % m, a = t;
        t = y;

        // Update y and x
        y = x - q * y;
        x = t;
    }

    // Make x positive
    if (x < 0)
        x += m0;

    return x;
}

// Driver Code
int main()
{
    int a = 3, m = 11;

    // Function call
    cout << "Modular multiplicative inverse is "<< modInverse(a, m);
    return 0;
}
// this code is contributed by shivanisinghss2110
```

## C

```
// Iterative C program to find modular
// inverse using extended Euclid algorithm
#include <stdio.h>

// Returns modulo inverse of a with respect
// to m using extended Euclid Algorithm
// Assumption: a and m are coprimes, i.e.,
// gcd(a, m) = 1
int modInverse(int a, int m)
{
    int m0 = m;
    int y = 0, x = 1;

    if (m == 1)
        return 0;

    while (a > 1) {
        // q is quotient
        int q = a / m;
        int t = m;

        // m is remainder now, process same as
        // Euclid's algo
        m = a % m, a = t;
        t = y;

        // Update y and x
        y = x - q * y;
        x = t;
    }

    // Make x positive
    if (x < 0)
        x += m0;

    return x;
}

// Driver Code
int main()
{
    int a = 3, m = 11;

    // Function call
    printf("Modular multiplicative inverse is %d\n",
           modInverse(a, m));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Iterative Java program to find modular
// inverse using extended Euclid algorithm

class GFG {

    // Returns modulo inverse of a with
    // respect to m using extended Euclid
    // Algorithm Assumption: a and m are
    // coprimes, i.e., gcd(a, m) = 1
    static int modInverse(int a, int m)
    {
        int m0 = m;
        int y = 0, x = 1;

        if (m == 1)
            return 0;

        while (a > 1) {
            // q is quotient
            int q = a / m;

            int t = m;

            // m is remainder now, process
            // same as Euclid's algo
            m = a % m;
            a = t;
            t = y;

            // Update x and y
            y = x - q * y;
            x = t;
        }

        // Make x positive
        if (x < 0)
            x += m0;

        return x;
    }

    // Driver code
    public static void main(String args[])
    {
        int a = 3, m = 11;

        // Function call
        System.out.println("Modular multiplicative "
                           + "inverse is "
                           + modInverse(a, m));
    }
}

/*This code is contributed by Nikita Tiwari.*/
```

## 蟒蛇 3

```
# Iterative Python 3 program to find
# modular inverse using extended
# Euclid algorithm

# Returns modulo inverse of a with
# respect to m using extended Euclid
# Algorithm Assumption: a and m are
# coprimes, i.e., gcd(a, m) = 1

def modInverse(a, m):
    m0 = m
    y = 0
    x = 1

    if (m == 1):
        return 0

    while (a > 1):

        # q is quotient
        q = a // m

        t = m

        # m is remainder now, process
        # same as Euclid's algo
        m = a % m
        a = t
        t = y

        # Update x and y
        y = x - q * y
        x = t

    # Make x positive
    if (x < 0):
        x = x + m0

    return x

# Driver code
a = 3
m = 11

# Function call
print("Modular multiplicative inverse is",
      modInverse(a, m))

# This code is contributed by Nikita tiwari.
```

## C#

```
// Iterative C# program to find modular
// inverse using extended Euclid algorithm
using System;
class GFG {

    // Returns modulo inverse of a with
    // respect to m using extended Euclid
    // Algorithm Assumption: a and m are
    // coprimes, i.e., gcd(a, m) = 1
    static int modInverse(int a, int m)
    {
        int m0 = m;
        int y = 0, x = 1;

        if (m == 1)
            return 0;

        while (a > 1) {
            // q is quotient
            int q = a / m;

            int t = m;

            // m is remainder now, process
            // same as Euclid's algo
            m = a % m;
            a = t;
            t = y;

            // Update x and y
            y = x - q * y;
            x = t;
        }

        // Make x positive
        if (x < 0)
            x += m0;

        return x;
    }

    // Driver Code
    public static void Main()
    {
        int a = 3, m = 11;

        // Function call
        Console.WriteLine("Modular multiplicative "
                          + "inverse is "
                          + modInverse(a, m));
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<≅php
// Iterative PHP program to find modular
// inverse using extended Euclid algorithm

// Returns modulo inverse of a with respect
// to m using extended Euclid Algorithm
// Assumption: a and m are coprimes, i.e.,
// gcd(a, m) = 1
function modInverse($a, $m)
{
    $m0 = $m;
    $y = 0;
    $x = 1;

    if ($m == 1)
    return 0;

    while ($a > 1)
    {

        // q is quotient
        $q = (int) ($a / $m);
        $t = $m;

        // m is remainder now,
        // process same as
        // Euclid's algo
        $m = $a % $m;
        $a = $t;
        $t = $y;

        // Update y and x
        $y = $x - $q * $y;
        $x = $t;
    }

    // Make x positive
    if ($x < 0)
    $x += $m0;

    return $x;
}

    // Driver Code
    $a = 3;
    $m = 11;

    // Function call
    echo "Modular multiplicative inverse is\n",
                            modInverse($a, $m);

// This code is contributed by Anuj_67
≅>
```

## java 描述语言

```
<script>

// Iterative Javascript program to find modular
// inverse using extended Euclid algorithm

// Returns modulo inverse of a with respect
// to m using extended Euclid Algorithm
// Assumption: a and m are coprimes, i.e.,
// gcd(a, m) = 1
function modInverse(a, m)
{
    let m0 = m;
    let y = 0;
    let x = 1;

    if (m == 1)
        return 0;

    while (a > 1)
    {

        // q is quotient
        let q = parseInt(a / m);
        let t = m;

        // m is remainder now,
        // process same as
        // Euclid's algo
        m = a % m;
        a = t;
        t = y;

        // Update y and x
        y = x - q * y;
        x = t;
    }

    // Make x positive
    if (x < 0)
        x += m0;

    return x;
}

// Driver Code
let a = 3;
let m = 11;

// Function call
document.write(`Modular multiplicative inverse is ${modInverse(a, m)}`);

// This code is contributed by _saurabh_jaiswal

</script>
```

**Output**

```
Modular multiplicative inverse is 4
```

**时间复杂度:** O(Log m)

**方法 3(m 为素数时有效)**
如果知道 m 为素数，那么也可以用 [**费马的小定理**](https://en.wikipedia.org/wiki/Fermat%27s_little_theorem) 求逆。

```
am-1 ≅ 1 (mod m)
```

如果我们将两边乘以一个 <sup>-1</sup> ，我们得到

```
a-1 ≅ a m-2 (mod m)
```

以下是上述想法的实现。

## C++

```
// C++ program to find modular inverse of a under modulo m
// This program works only if m is prime.
#include <iostream>
using namespace std;

// To find GCD of a and b
int gcd(int a, int b);

// To compute x raised to power y under modulo m
int power(int x, unsigned int y, unsigned int m);

// Function to find modular inverse of a under modulo m
// Assumption: m is prime
void modInverse(int a, int m)
{
    int g = gcd(a, m);
    if (g != 1)
        cout << "Inverse doesn't exist";
    else
    {
        // If a and m are relatively prime, then modulo
        // inverse is a^(m-2) mode m
        cout << "Modular multiplicative inverse is "
             << power(a, m - 2, m);
    }
}

// To compute x^y under modulo m
int power(int x, unsigned int y, unsigned int m)
{
    if (y == 0)
        return 1;
    int p = power(x, y / 2, m) % m;
    p = (p * p) % m;

    return (y % 2 == 0) ? p : (x * p) % m;
}

// Function to return gcd of a and b
int gcd(int a, int b)
{
    if (a == 0)
        return b;
    return gcd(b % a, a);
}

// Driver code
int main()
{
    int a = 3, m = 11;

    // Function call
    modInverse(a, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find modular
// inverse of a under modulo m
// This program works only if
// m is prime.
import java.io.*;

class GFG {

    // Function to find modular inverse of a
    // under modulo m Assumption: m is prime
    static void modInverse(int a, int m)
    {
        int g = gcd(a, m);
        if (g != 1)
            System.out.println("Inverse doesn't exist");
        else
        {
            // If a and m are relatively prime, then modulo
            // inverse is a^(m-2) mode m
            System.out.println(
                "Modular multiplicative inverse is "
                + power(a, m - 2, m));
        }
    }

      static int power(int x, int y, int m)
    {
        if (y == 0)
            return 1;
        int p = power(x, y / 2, m) % m;
        p = (int)((p * (long)p) % m);
        if (y % 2 == 0)
            return p;
        else
            return (int)((x * (long)p) % m);
    }

    // Function to return gcd of a and b
    static int gcd(int a, int b)
    {
        if (a == 0)
            return b;
        return gcd(b % a, a);
    }

    // Driver Code
    public static void main(String args[])
    {
        int a = 3, m = 11;

        // Function call
        modInverse(a, m);
    }
}

// This code is contributed by Nikita Tiwari.
```

## 蟒蛇 3

```
# Python3 program to find modular
# inverse of a under modulo m

# This program works only if m is prime.

# Function to find modular
# inverse of a under modulo m
# Assumption: m is prime

def modInverse(a, m):

    g = gcd(a, m)

    if (g != 1):
        print("Inverse doesn't exist")

    else:

        # If a and m are relatively prime,
        # then modulo inverse is a^(m-2) mode m
        print("Modular multiplicative inverse is ",
              power(a, m - 2, m))

# To compute x^y under modulo m

def power(x, y, m):

    if (y == 0):
        return 1

    p = power(x, y // 2, m) % m
    p = (p * p) % m

    if(y % 2 == 0):
        return p
    else:
        return ((x * p) % m)

# Function to return gcd of a and b

def gcd(a, b):
    if (a == 0):
        return b

    return gcd(b % a, a)

# Driver Code
a = 3
m = 11

# Function call
modInverse(a, m)

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to find modular
// inverse of a under modulo m
// This program works only if
// m is prime.
using System;
class GFG {

    // Function to find modular
    // inverse of a under modulo
    // m Assumption: m is prime
    static void modInverse(int a, int m)
    {
        int g = gcd(a, m);
        if (g != 1)
            Console.Write("Inverse doesn't exist");
        else {
            // If a and m are relatively
            // prime, then modulo inverse
            // is a^(m-2) mode m
            Console.Write(
                "Modular multiplicative inverse is "
                + power(a, m - 2, m));
        }
    }

    // To compute x^y under
    // modulo m
    static int power(int x, int y, int m)
    {
        if (y == 0)
            return 1;

        int p = power(x, y / 2, m) % m;
        p = (p * p) % m;

        if (y % 2 == 0)
            return p;
        else
            return (x * p) % m;
    }

    // Function to return
    // gcd of a and b
    static int gcd(int a, int b)
    {
        if (a == 0)
            return b;
        return gcd(b % a, a);
    }

    // Driver Code
    public static void Main()
    {
        int a = 3, m = 11;

        // Function call
        modInverse(a, m);
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<≅php
// PHP program to find modular
// inverse of a under modulo m
// This program works only if m
// is prime.

// Function to find modular inverse
// of a under modulo m
// Assumption: m is prime
function modInverse( $a, $m)
{
    $g = gcd($a, $m);
    if ($g != 1)
        echo "Inverse doesn't exist";
    else
    {

        // If a and m are relatively
        // prime, then modulo inverse
        // is a^(m-2) mode m
        echo "Modular multiplicative inverse is "
                        , power($a, $m - 2, $m);
    }
}

// To compute x^y under modulo m
function power( $x, $y, $m)
{
    if ($y == 0)
        return 1;
    $p = power($x, $y / 2, $m) % $m;
    $p = ($p * $p) % $m;

    return ($y % 2 == 0)? $p : ($x * $p) % $m;
}

// Function to return gcd of a and b
function gcd($a, $b)
{
    if ($a == 0)
        return $b;
    return gcd($b % $a, $a);
}

// Driver Code
$a = 3;
$m = 11;

// Function call
modInverse($a, $m);

// This code is contributed by anuj_67.
≅>
```

## java 描述语言

```
<script>
// Javascript program to find modular inverse of a under modulo m
// This program works only if m is prime.

// Function to find modular inverse of a under modulo m
// Assumption: m is prime
function modInverse(a, m)
{
    let g = gcd(a, m);
    if (g != 1)
        document.write("Inverse doesn't exist");
    else
    {
        // If a and m are relatively prime, then modulo
        // inverse is a^(m-2) mode m
        document.write("Modular multiplicative inverse is "
             + power(a, m - 2, m));
    }
}

// To compute x^y under modulo m
function power(x, y, m)
{
    if (y == 0)
        return 1;
    let p = power(x, parseInt(y / 2), m) % m;
    p = (p * p) % m;

    return (y % 2 == 0) ? p : (x * p) % m;
}

// Function to return gcd of a and b
function gcd(a, b)
{
    if (a == 0)
        return b;
    return gcd(b % a, a);
}

// Driver code
let a = 3, m = 11;

// Function call
modInverse(a, m);

// This code is contributed by subham348.
</script>
```

**Output**

```
Modular multiplicative inverse is 4
```

**时间复杂度:** O(Log m)

我们讨论了三种求乘法逆模 m 的方法。
1)天真法，O(m)
2)扩展欧拉 GCD 算法，O(Log m)【当 a 和 m 是互质时起作用】
3)费马小定理，O(Log m)【当‘m’是素数时起作用】

**应用:**
计算模乘逆是 [RSA 公钥加密方法](https://en.wikipedia.org/wiki/RSA_%28cryptosystem%29)中必不可少的一步。

**参考文献:**
[https://en . Wikipedia . org/wiki/Modular _ 乘法 _ 逆](https://en.wikipedia.org/wiki/Modular_multiplicative_inverse)
[http://e-maxx.ru/algo/reverse_element](http://e-maxx.ru/algo/reverse_element)
本文由 **Ankur** 供稿。如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息，请写评论