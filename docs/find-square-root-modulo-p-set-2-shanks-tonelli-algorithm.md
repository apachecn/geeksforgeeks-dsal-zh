# 求模 p |集合 2 下的平方根(Shanks Tonelli 算法)

> 原文:[https://www . geesforgeks . org/find-平方根-模-p-set-2-shanks-tonelli-algorithm/](https://www.geeksforgeeks.org/find-square-root-modulo-p-set-2-shanks-tonelli-algorithm/)

给定一个数“n”和一个素数“p”，求模 p 下 n 的平方根，如果它存在的话。
**例:**

```
Input: n = 2, p = 113
Output: 62
62^2 = 3844  and  3844 % 113 = 2

Input:  n = 2, p = 7
Output: 3 or 4
3 and 4 both are square roots of 2 under modulo
7 because (3*3) % 7 = 2 and (4*4) % 7 = 2

Input:  n = 2, p = 5
Output: Square root doesn't exist
```

我们已经讨论了[欧拉准则](https://www.geeksforgeeks.org/eulers-criterion-check-if-square-root-under-modulo-p-exists/)来检查平方根是否存在。我们还讨论了[一个只有当 p 是 4*i + 3](https://www.geeksforgeeks.org/find-square-root-under-modulo-p-set-1-when-p-is-in-form-of-4i-3/)
形式时才起作用的解决方案。在这篇文章中，[讨论了适用于所有类型输入的 Shank Tonelli 算法](https://en.wikipedia.org/wiki/Tonelli%E2%80%93Shanks_algorithm)。
使用 shank Tonelli 算法求模平方根的算法步骤:
1)计算 n ^((p–1)/2)(mod p)，它必须是 1 或 p-1，如果是 p-1，那么模平方根是不可能的。
2)然后，对于某些整数 s 和 e，在将 p-1 写成(s * 2^e)之后，其中 s 必须是奇数，并且 s 和 e 都应该是正数。
3)然后找到一个数字 q，使得 q ^((p–1)/2)(mod p)=-1
4)通过以下值初始化变量 x、b、g 和 r

```
   x = n ^ ((s + 1) / 2 (first guess of square root)
   b = n ^ s                
   g = q ^ s
   r = e   (exponent e will decrease after each updation) 
```

5)现在循环直到 m > 0 并更新 x 的值，这将是我们的最终答案。

```
   Find least integer m such that b^(2^m) = 1(mod p)  and  0 <= m <= r – 1 
   If m = 0, then we found correct answer and return x as result
   Else update x, b, g, r as below
       x = x * g ^ (2 ^ (r – m - 1))
       b = b * g ^(2 ^ (r - m))
       g = g ^ (2 ^ (r - m))
       r = m 
```

所以如果 m 变成 0 或者 b 变成 1，我们终止并打印结果。这个循环保证终止，因为 m 的值在每次更新后都会减少。
以下是上述算法的实现。

## C++

```
// C++ program to implement Shanks Tonelli algorithm for
// finding Modular  Square Roots
#include <bits/stdc++.h>
using namespace std;

//  utility function to find pow(base, exponent) % modulus
int pow(int base, int exponent, int modulus)
{
    int result = 1;
    base = base % modulus;
    while (exponent > 0)
    {
        if (exponent % 2 == 1)
           result = (result * base)% modulus;
        exponent = exponent >> 1;
        base = (base * base) % modulus;
    }
    return result;
}

//  utility function to find gcd
int gcd(int a, int b)
{
    if (b == 0)
        return a;
    else
        return gcd(b, a % b);
}

//  Returns k such that b^k = 1 (mod p)
int order(int p, int b)
{
    if (gcd(p, b) != 1)
    {
        printf("p and b are not co-prime.\n");
        return -1;
    }

    //  Initializing k with first odd prime number
    int k = 3;
    while (1)
    {
        if (pow(b, k, p) == 1)
            return k;
        k++;
    }
}

//  function return  p - 1 (= x argument) as  x * 2^e,
//  where x will be odd  sending e as reference because
//  updation is needed in actual e
int convertx2e(int x, int& e)
{
    e = 0;
    while (x % 2 == 0)
    {
        x /= 2;
        e++;
    }
    return x;
}

//  Main function for finding the modular square root
int STonelli(int n, int p)
{
    //  a and p should be coprime for finding the modular
    // square root
    if (gcd(n, p) != 1)
    {
        printf("a and p are not coprime\n");
        return -1;
    }

    //  If below expression return (p - 1)  then modular
    // square root is not possible
    if (pow(n, (p - 1) / 2, p) == (p - 1))
    {
        printf("no sqrt possible\n");
        return -1;
    }

    //  expressing p - 1, in terms of s * 2^e,  where s
    // is odd number
    int s, e;
    s = convertx2e(p - 1, e);

    //  finding smallest q such that q ^ ((p - 1) / 2)
    //  (mod p) = p - 1
    int q;
    for (q = 2; ; q++)
    {
        // q - 1 is in place of  (-1 % p)
        if (pow(q, (p - 1) / 2, p) == (p - 1))
            break;
    }

    //  Initializing variable x, b and g
    int x = pow(n, (s + 1) / 2, p);
    int b = pow(n, s, p);
    int g = pow(q, s, p);

    int r = e;

    // keep looping until b become 1 or m becomes 0
    while (1)
    {
        int m;
        for (m = 0; m < r; m++)
        {
            if (order(p, b) == -1)
                return -1;

            //  finding m such that b^ (2^m) = 1
            if (order(p, b) == pow(2, m))
                break;
        }
        if (m == 0)
            return x;

        // updating value of x, g and b according to
        // algorithm
        x = (x * pow(g, pow(2, r - m - 1), p)) % p;
        g = pow(g, pow(2, r - m), p);
        b = (b * g) % p;

        if (b == 1)
            return x;
        r = m;
    }
}

//  driver program to test above function
int main()
{
    int n = 2;

    // p should be prime
    int p = 113;

    int x = STonelli(n, p);

    if (x == -1)
        printf("Modular square root is not exist\n");
    else
        printf("Modular square root of %d and %d is %d\n",
                n, p, x);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement Shanks
// Tonelli algorithm for finding
// Modular Square Roots
class GFG
{
    static int z = 0;

// utility function to find
// pow(base, exponent) % modulus
static int pow1(int base1,
    int exponent, int modulus)
{
    int result = 1;
    base1 = base1 % modulus;
    while (exponent > 0)
    {
        if (exponent % 2 == 1)
            result = (result * base1) % modulus;
        exponent = exponent >> 1;
        base1 = (base1 * base1) % modulus;
    }
    return result;
}

// utility function to find gcd
static int gcd(int a, int b)
{
    if (b == 0)
        return a;
    else
        return gcd(b, a % b);
}

// Returns k such that b^k = 1 (mod p)
static int order(int p, int b)
{
    if (gcd(p, b) != 1)
    {
        System.out.println("p and b are" +
                            "not co-prime.");
        return -1;
    }

    // Initializing k with first
    // odd prime number
    int k = 3;
    while (true)
    {
        if (pow1(b, k, p) == 1)
            return k;
        k++;
    }
}

// function return p - 1 (= x argument)
// as x * 2^e, where x will be odd
// sending e as reference because
// updation is needed in actual e
static int convertx2e(int x)
{
    z = 0;
    while (x % 2 == 0)
    {
        x /= 2;
        z++;
    }
    return x;
}

// Main function for finding
// the modular square root
static int STonelli(int n, int p)
{
    // a and p should be coprime for 
    // finding the modular square root
    if (gcd(n, p) != 1)
    {
        System.out.println("a and p are not coprime");
        return -1;
    }

    // If below expression return (p - 1) then modular
    // square root is not possible
    if (pow1(n, (p - 1) / 2, p) == (p - 1))
    {
        System.out.println("no sqrt possible");
        return -1;
    }

    // expressing p - 1, in terms of 
    // s * 2^e, where s is odd number
    int s, e;
    s = convertx2e(p - 1);
    e = z;

    // finding smallest q such that q ^ ((p - 1) / 2)
    // (mod p) = p - 1
    int q;
    for (q = 2; ; q++)
    {
        // q - 1 is in place of (-1 % p)
        if (pow1(q, (p - 1) / 2, p) == (p - 1))
            break;
    }

    // Initializing variable x, b and g
    int x = pow1(n, (s + 1) / 2, p);
    int b = pow1(n, s, p);
    int g = pow1(q, s, p);

    int r = e;

    // keep looping until b
    // become 1 or m becomes 0
    while (true)
    {
        int m;
        for (m = 0; m < r; m++)
        {
            if (order(p, b) == -1)
                return -1;

            // finding m such that b^ (2^m) = 1
            if (order(p, b) == Math.pow(2, m))
                break;
        }
        if (m == 0)
            return x;

        // updating value of x, g and b
        // according to algorithm
        x = (x * pow1(g, (int)Math.pow(2,
                            r - m - 1), p)) % p;
        g = pow1(g, (int)Math.pow(2, r - m), p);
        b = (b * g) % p;

        if (b == 1)
            return x;
        r = m;
    }
}

// Driver code
public static void main (String[] args)
{

    int n = 2;

    // p should be prime
    int p = 113;

    int x = STonelli(n, p);

    if (x == -1)
        System.out.println("Modular square" +
                        "root is not exist\n");
    else
        System.out.println("Modular square root of " +
                            n + " and " + p + " is " +
                            x + "\n");
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 program to implement Shanks Tonelli
# algorithm for finding Modular Square Roots

# utility function to find pow(base,
# exponent) % modulus
def pow1(base, exponent, modulus):

    result = 1;
    base = base % modulus;
    while (exponent > 0):
        if (exponent % 2 == 1):
            result = (result * base) % modulus;
        exponent = int(exponent) >> 1;
        base = (base * base) % modulus;

    return result;

# utility function to find gcd
def gcd(a, b):
    if (b == 0):
        return a;
    else:
        return gcd(b, a % b);

# Returns k such that b^k = 1 (mod p)
def order(p, b):

    if (gcd(p, b) != 1):
        print("p and b are not co-prime.\n");
        return -1;

    # Initializing k with first
    # odd prime number
    k = 3;
    while (True):
        if (pow1(b, k, p) == 1):
            return k;
        k += 1;

# function return p - 1 (= x argument) as
# x * 2^e, where x will be odd sending e
# as reference because updation is needed
# in actual e
def convertx2e(x):
    z = 0;
    while (x % 2 == 0):
        x = x / 2;
        z += 1;

    return [x, z];

# Main function for finding the
# modular square root
def STonelli(n, p):

    # a and p should be coprime for
    # finding the modular square root
    if (gcd(n, p) != 1):
        print("a and p are not coprime\n");
        return -1;

    # If below expression return (p - 1) then
    # modular square root is not possible
    if (pow1(n, (p - 1) / 2, p) == (p - 1)):
        print("no sqrt possible\n");
        return -1;

    # expressing p - 1, in terms of s * 2^e,
    # where s is odd number
    ar = convertx2e(p - 1);
    s = ar[0];
    e = ar[1];

    # finding smallest q such that
    # q ^ ((p - 1) / 2) (mod p) = p - 1
    q = 2;
    while (True):

        # q - 1 is in place of (-1 % p)
        if (pow1(q, (p - 1) / 2, p) == (p - 1)):
            break;
        q += 1;

    # Initializing variable x, b and g
    x = pow1(n, (s + 1) / 2, p);
    b = pow1(n, s, p);
    g = pow1(q, s, p);

    r = e;

    # keep looping until b become
    # 1 or m becomes 0
    while (True):
        m = 0;
        while (m < r):
            if (order(p, b) == -1):
                return -1;

            # finding m such that b^ (2^m) = 1
            if (order(p, b) == pow(2, m)):
                break;
            m += 1;

        if (m == 0):
            return x;

        # updating value of x, g and b
        # according to algorithm
        x = (x * pow1(g, pow(2, r - m - 1), p)) % p;
        g = pow1(g, pow(2, r - m), p);
        b = (b * g) % p;

        if (b == 1):
            return x;
        r = m;

# Driver Code
n = 2;

# p should be prime
p = 113;

x = STonelli(n, p);

if (x == -1):
    print("Modular square root is not exist\n");
else:
    print("Modular square root of", n,
          "and", p, "is", x);

# This code is contributed by mits
```

## C#

```
// C# program to implement Shanks
// Tonelli algorithm for finding
// Modular Square Roots
using System;

class GFG
{

static int z=0;

// utility function to find
// pow(base, exponent) % modulus
static int pow1(int base1,
        int exponent, int modulus)
{
    int result = 1;
    base1 = base1 % modulus;
    while (exponent > 0)
    {
        if (exponent % 2 == 1)
            result = (result * base1) % modulus;
        exponent = exponent >> 1;
        base1 = (base1 * base1) % modulus;
    }
    return result;
}

// utility function to find gcd
static int gcd(int a, int b)
{
    if (b == 0)
        return a;
    else
        return gcd(b, a % b);
}

// Returns k such that b^k = 1 (mod p)
static int order(int p, int b)
{
    if (gcd(p, b) != 1)
    {
        Console.WriteLine("p and b are" +
                            "not co-prime.");
        return -1;
    }

    // Initializing k with
    // first odd prime number
    int k = 3;
    while (true)
    {
        if (pow1(b, k, p) == 1)
            return k;
        k++;
    }
}

// function return p - 1 (= x argument)
// as x * 2^e, where x will be odd sending
// e as reference because updation is
// needed in actual e
static int convertx2e(int x)
{
    z = 0;
    while (x % 2 == 0)
    {
        x /= 2;
        z++;
    }
    return x;
}

// Main function for finding
// the modular square root
static int STonelli(int n, int p)
{
    // a and p should be coprime for
    // finding the modular square root
    if (gcd(n, p) != 1)
    {
        Console.WriteLine("a and p are not coprime");
        return -1;
    }

    // If below expression return (p - 1) then
    // modular square root is not possible
    if (pow1(n, (p - 1) / 2, p) == (p - 1))
    {
        Console.WriteLine("no sqrt possible");
        return -1;
    }

    // expressing p - 1, in terms of s * 2^e,
    //  where s is odd number
    int s, e;
    s = convertx2e(p - 1);
    e=z;

    // finding smallest q such that q ^ ((p - 1) / 2)
    // (mod p) = p - 1
    int q;
    for (q = 2; ; q++)
    {
        // q - 1 is in place of (-1 % p)
        if (pow1(q, (p - 1) / 2, p) == (p - 1))
            break;
    }

    // Initializing variable x, b and g
    int x = pow1(n, (s + 1) / 2, p);
    int b = pow1(n, s, p);
    int g = pow1(q, s, p);

    int r = e;

    // keep looping until b become
    // 1 or m becomes 0
    while (true)
    {
        int m;
        for (m = 0; m < r; m++)
        {
            if (order(p, b) == -1)
                return -1;

            // finding m such that b^ (2^m) = 1
            if (order(p, b) == Math.Pow(2, m))
                break;
        }
        if (m == 0)
            return x;

        // updating value of x, g and b 
        // according to algorithm
        x = (x * pow1(g, (int)Math.Pow(2, r - m - 1), p)) % p;
        g = pow1(g, (int)Math.Pow(2, r - m), p);
        b = (b * g) % p;

        if (b == 1)
            return x;
        r = m;
    }
}

// Driver code
static void Main()
{
    int n = 2;

    // p should be prime
    int p = 113;

    int x = STonelli(n, p);

    if (x == -1)
        Console.WriteLine("Modular square root" +
                            "is not exist\n");
    else
        Console.WriteLine("Modular square root of" +
                        "{0} and {1} is {2}\n", n, p, x);
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to implement Shanks Tonelli
// algorithm for finding Modular Square Roots

// utility function to find pow(base,
// exponent) % modulus
function pow1($base, $exponent, $modulus)
{
    $result = 1;
    $base = $base % $modulus;
    while ($exponent > 0)
    {
        if ($exponent % 2 == 1)
        $result = ($result * $base) % $modulus;
        $exponent = $exponent >> 1;
        $base = ($base * $base) % $modulus;
    }
    return $result;
}

// utility function to find gcd
function gcd($a, $b)
{
    if ($b == 0)
        return $a;
    else
        return gcd($b, $a % $b);
}

// Returns k such that b^k = 1 (mod p)
function order($p, $b)
{
    if (gcd($p, $b) != 1)
    {
        print("p and b are not co-prime.\n");
        return -1;
    }

    // Initializing k with first
    // odd prime number
    $k = 3;
    while (1)
    {
        if (pow1($b, $k, $p) == 1)
            return $k;
        $k++;
    }
}

// function return p - 1 (= x argument) as
// x * 2^e, where x will be odd sending e
// as reference because updation is needed
// in actual e
function convertx2e($x, &$e)
{
    $e = 0;
    while ($x % 2 == 0)
    {
        $x = (int)($x / 2);
        $e++;
    }
    return $x;
}

// Main function for finding the
// modular square root
function STonelli($n, $p)
{
    // a and p should be coprime for
    // finding the modular square root
    if (gcd($n, $p) != 1)
    {
        print("a and p are not coprime\n");
        return -1;
    }

    // If below expression return (p - 1) then
    // modular square root is not possible
    if (pow1($n, ($p - 1) / 2, $p) == ($p - 1))
    {
        printf("no sqrt possible\n");
        return -1;
    }

    // expressing p - 1, in terms of s * 2^e,
    // where s is odd number
    $e = 0;
    $s = convertx2e($p - 1, $e);

    // finding smallest q such that
    // q ^ ((p - 1) / 2) (mod p) = p - 1
    $q = 2;
    for (; ; $q++)
    {
        // q - 1 is in place of (-1 % p)
        if (pow1($q, ($p - 1) / 2, $p) == ($p - 1))
            break;
    }

    // Initializing variable x, b and g
    $x = pow1($n, ($s + 1) / 2, $p);
    $b = pow1($n, $s, $p);
    $g = pow1($q, $s, $p);

    $r = $e;

    // keep looping until b become
    // 1 or m becomes 0
    while (1)
    {
        $m = 0;
        for (; $m < $r; $m++)
        {
            if (order($p, $b) == -1)
                return -1;

            // finding m such that b^ (2^m) = 1
            if (order($p, $b) == pow(2, $m))
                break;
        }
        if ($m == 0)
            return $x;

        // updating value of x, g and b
        // according to algorithm
        $x = ($x * pow1($g, pow(2, $r - $m - 1), $p)) % $p;
        $g = pow1($g, pow(2, $r - $m), $p);
        $b = ($b * $g) % $p;

        if ($b == 1)
            return $x;
        $r = $m;
    }
}

// Driver Code
$n = 2;

// p should be prime
$p = 113;

$x = STonelli($n, $p);

if ($x == -1)
    print("Modular square root is not exist\n");
else
    print("Modular square root of " .
          "$n and $p is $x\n");

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// JavaScript program to implement Shanks
// Tonelli algorithm for finding
// Modular Square Roots

    let z = 0;

// utility function to find
// pow(base, exponent) % modulus
function pow1(base1,
    exponent, modulus)
{
    let result = 1;
    base1 = base1 % modulus;
    while (exponent > 0)
    {
        if (exponent % 2 == 1)
            result = (result * base1) % modulus;
        exponent = exponent >> 1;
        base1 = (base1 * base1) % modulus;
    }
    return result;
}

// utility function to find gcd
function gcd(a, b)
{
    if (b == 0)
        return a;
    else
        return gcd(b, a % b);
}

// Returns k such that b^k = 1 (mod p)
function order(p, b)
{
    if (gcd(p, b) != 1)
    {
        document.write("p and b are" +
                            "not co-prime." + "<br/>");
        return -1;
    }

    // Initializing k with first
    // odd prime number
    let k = 3;
    while (true)
    {
        if (pow1(b, k, p) == 1)
            return k;
        k++;
    }
}

// function return p - 1 (= x argument)
// as x * 2^e, where x will be odd
// sending e as reference because
// updation is needed in actual e
function convertx2e(x)
{
    z = 0;
    while (x % 2 == 0)
    {
        x /= 2;
        z++;
    }
    return x;
}

// Main function for finding
// the modular square root
function STonelli(n, p)
{
    // a and p should be coprime for 
    // finding the modular square root
    if (gcd(n, p) != 1)
    {
        System.out.prletln("a and p are not coprime");
        return -1;
    }

    // If below expression return (p - 1) then modular
    // square root is not possible
    if (pow1(n, (p - 1) / 2, p) == (p - 1))
    {
        document.write("no sqrt possible" + "<br/>");
        return -1;
    }

    // expressing p - 1, in terms of 
    // s * 2^e, where s is odd number
    let s, e;
    s = convertx2e(p - 1);
    e = z;

    // finding smallest q such that q ^ ((p - 1) / 2)
    // (mod p) = p - 1
    let q;
    for (q = 2; ; q++)
    {
        // q - 1 is in place of (-1 % p)
        if (pow1(q, (p - 1) / 2, p) == (p - 1))
            break;
    }

    // Initializing variable x, b and g
    let x = pow1(n, (s + 1) / 2, p);
    let b = pow1(n, s, p);
    let g = pow1(q, s, p);

    let r = e;

    // keep looping until b
    // become 1 or m becomes 0
    while (true)
    {
        let m;
        for (m = 0; m < r; m++)
        {
            if (order(p, b) == -1)
                return -1;

            // finding m such that b^ (2^m) = 1
            if (order(p, b) == Math.pow(2, m))
                break;
        }
        if (m == 0)
            return x;

        // updating value of x, g and b
        // according to algorithm
        x = (x * pow1(g, Math.pow(2,
                            r - m - 1), p)) % p;
        g = pow1(g, Math.pow(2, r - m), p);
        b = (b * g) % p;

        if (b == 1)
            return x;
        r = m;
    }
}

// Driver Code

     let n = 2;

    // p should be prime
    let p = 113;

    let x = STonelli(n, p);

    if (x == -1)
        document.write("Modular square" +
                        "root is not exist\n");
    else
        document.write("Modular square root of " +
                            n + " and " + p + " is " +
                            x + "\n");

</script>
```

**输出:**

```
Modular square root of 2 and 113 is 62
```

有关上述算法的更多详细信息，请访问:
[【http://cs.indstate.edu/~sgali1/Shanks_Tonelli.pdf】](http://cs.indstate.edu/~sgali1/Shanks_Tonelli.pdf)
有关示例(2，113)的详细信息，请参见:
[http://www . math . vt . edu/people/brown/class _ home page/shanks _ tonelli . pdf](http://www.math.vt.edu/people/brown/class_homepages/shanks_tonelli.pdf)
本文由 Utkarsh Trivedi 供稿。如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息