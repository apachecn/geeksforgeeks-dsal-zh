# 将 A 转换为 B 的最小素数运算

> 原文:[https://www . geesforgeks . org/minimum-prime-number-operations-convert-a-b/](https://www.geeksforgeeks.org/minimum-prime-number-operations-to-convert-a-to-b/)

给定两个整数 **A** 和 **B** ，任务是将 **A** 转换为 **B** ，最小操作次数如下:

1.  将 **A** 乘以任意**素数**。
2.  将 **A** 除以它的一个**质因数**。

打印所需的最小操作数。
**例:**

> **输入:** A = 10，B = 15
> **输出:** 2
> 运算 1: 10 / 2 = 5
> 运算 2: 5 * 3 = 15
> **输入:** A = 9，B = 7
> **输出:** 3

**天真的做法:**若素因式分解**A = p<sub>1</sub>T5】q<sub>T8】1T10】* p<sub>2</sub>T13】qT15<sup>2</sup>T18】*…* p<sub>n</sub>T21】qT23<sup>n</sup>T26</sub>**。如果我们将 **A** 乘以某个质数，那么该质数的 **q <sub>i</sub>** 将增加 **1** ，如果我们将 **A** 除以其质数之一，那么该质数的 **q <sub>i</sub>** 将减少 **1** 。所以对于一个素数 **p** 如果它在 **A** 的素数因式分解中出现**q<sub>A</sub>**次，在 **B** 的素数因式分解中出现**q<sub>B</sub>**次，那么我们只需要求| q<sub>A</sub>–q<sub>B</sub>|的**和即可** 

**有效方法:**通过将 **A** 和 **B** 除以它们的 GCD，消除 **A** 和 **B** 的所有共同因素。如果 **A** 和 **B** 没有共同的因子，那么我们只需要将 **A** 转换为 **B** 就可以了。

以下是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of
// prime factors of a number
int countFactors(int n)
{
    int factors = 0;

    for (int i = 2; i * i <= n; i++) {
        while (n % i == 0) {
            n /= i;
            factors += 1;
        }
    }

    if (n != 1)
        factors++;

    return factors;
}

// Function to return the minimum number of
// given operations required to convert A to B
int minOperations(int A, int B)
{
    int g = __gcd(A, B); // gcd(A, B);

    // Eliminate the common
    // factors of A and B
    A /= g;
    B /= g;

    // Sum of prime factors
    return countFactors(A) + countFactors(B);
}

// Driver code
int main()
{
    int A = 10, B = 15;

    cout << minOperations(A, B);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java .io.*;

class GFG
{

// Function to return the count of
// prime factors of a number
static int countFactors(int n)
{
    int factors = 0;

    for (int i = 2; i * i <= n; i++)
    {
        while (n % i == 0)
        {
            n /= i;
            factors += 1;
        }
    }

    if (n != 1)
        factors++;

        return factors;
}

static int __gcd(int a, int b)
{
    if (b == 0)
    return a;
    return __gcd(b, a % b);
}

// Function to return the minimum
// number of given operations
// required to convert A to B
static int minOperations(int A, int B)
{
    int g = __gcd(A, B); // gcd(A, B);

    // Eliminate the common
    // factors of A and B
    A /= g;
    B /= g;

    // Sum of prime factors
    return countFactors(A) + countFactors(B);
}

// Driver code
public static void main(String[] args)
{
    int A = 10, B = 15;

    System.out.println(minOperations(A, B));
}
}

// This code is contributed
// by Code_Mech
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# from math lib import sqrt
# and gcd function
from math import sqrt, gcd

# Function to return the count of
# prime factors of a number
def countFactors(n) :
    factors = 0;

    for i in range(2, int(sqrt(n)) + 1) :
        while (n % i == 0) :
            n //= i
            factors += 1

    if (n != 1) :
        factors += 1

    return factors

# Function to return the minimum number of
# given operations required to convert A to B
def minOperations(A, B) :

    g = gcd(A, B)

    # Eliminate the common
    # factors of A and B
    A //= g
    B //= g

    # Sum of prime factors
    return countFactors(A) + countFactors(B)

# Driver code
if __name__ == "__main__" :

    A, B = 10, 15

    print(minOperations(A, B))

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

    // Function to return the count of
    // prime factors of a number
    static int countFactors(int n)
    {
        int factors = 0;
        for (int i = 2; i * i <= n; i++)
        {
            while (n % i == 0)
            {
                n /= i;
                factors += 1;
            }
        }

        if (n != 1)
            factors++;

        return factors;
    }

    static int __gcd(int a, int b)
    {
        if (b == 0)
            return a;
        return __gcd(b, a % b);
    }

    // Function to return the minimum
    // number of given operations
    // required to convert A to B
    static int minOperations(int A, int B)
    {
        int g = __gcd(A, B); // gcd(A, B);

        // Eliminate the common
        // factors of A and B
        A /= g;
        B /= g;

        // Sum of prime factors
        return countFactors(A) + countFactors(B);
    }

    // Driver code
    public static void Main()
    {
        int A = 10, B = 15;
        Console.WriteLine(minOperations(A, B));
    }
}

// This code is contributed by
// PrinciRaj1992
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Function to calculate gcd
function __gcd($a, $b)
{

    // Everything divides 0
    if ($a == 0 || $b == 0)
        return 0;

    // base case
    if ($a == $b)
        return $a;

    // a is greater
    if ($a > $b)
        return __gcd($a - $b, $b);

    return __gcd($a, $b - $a);
}

// Function to return the count of
// prime factors of a number
function countFactors($n)
{
    $factors = 0;

    for ($i = 2; $i * $i <= $n; $i++)
    {
        while ($n % $i == 0)
        {
            $n /= $i;
            $factors += 1;
        }
    }

    if ($n != 1)
        $factors++;

    return $factors;
}

// Function to return the minimum number of
// given operations required to convert A to B
function minOperations($A, $B)
{
    $g = __gcd($A, $B); // gcd(A, B);

    // Eliminate the common
    // factors of A and B
    $A /= $g;
    $B /= $g;

    // Sum of prime factors
    return countFactors($A) +
           countFactors($B);
}

// Driver code
$A = 10; $B = 15;

echo minOperations($A, $B);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>
// javascript implementation of above approach

    // Function to return the count of
    // prime factors of a number
    function countFactors(n) {
        var factors = 0;

        for (i = 2; i * i <= n; i++) {
            while (n % i == 0) {
                n /= i;
                factors += 1;
            }
        }

        if (n != 1)
            factors++;

        return factors;
    }

    function __gcd(a , b) {
        if (b == 0)
            return a;
        return __gcd(b, a % b);
    }

    // Function to return the minimum
    // number of given operations
    // required to convert A to B
    function minOperations(A , B) {
        var g = __gcd(A, B); // gcd(A, B);

        // Eliminate the common
        // factors of A and B
        A /= g;
        B /= g;

        // Sum of prime factors
        return countFactors(A) + countFactors(B);
    }

    // Driver code

        var A = 10, B = 15;

        document.write(minOperations(A, B));

// This code contributed by Rajput-Ji
</script>
```

**Output:** 

```
2
```