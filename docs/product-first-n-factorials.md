# 第一个 N 因子的乘积

> 原文:[https://www.geeksforgeeks.org/product-first-n-factorials/](https://www.geeksforgeeks.org/product-first-n-factorials/)

给定一个数 N，求模 1000000007 的第一个 N 阶乘的乘积。

> **约束:** 1 ≤ N ≤ 1e6

**示例:**

```
Input : 3
Output : 12
Explanation: 1! * 2! * 3! = 12 mod (1e9 + 7) = 12

Input : 5
Output : 34560
```

**先决条件:** [模乘](https://www.geeksforgeeks.org/how-to-avoid-overflow-in-modular-multiplication/)
**方法:**解决这个问题背后的基本思路就是只考虑这样大数乘法时的溢出问题，即阶乘。因此，它需要通过递归相乘来解决溢出的困难。此外，在迭代计算阶乘和模乘时，我们必须在每一步取模。

```
facti = facti-1 * i
where facti is the factorial of ith number

prodi = prodi-1 * facti
where prodi is the product of first i factorials
```

为了求模下两个大数的乘积，我们使用与模下[求幂相同的方法……在乘法函数中，我们使用+代替*。
以下是上述办法的实施情况。](https://www.geeksforgeeks.org/modular-exponentiation-power-in-modular-arithmetic/)

## C++

```
// CPP Program to find the
// product of first N factorials
#include <bits/stdc++.h>

using namespace std;

// To compute (a * b) % MOD
long long int mulmod(long long int a, long long int b,
                                    long long int mod)
{
    long long int res = 0; // Initialize result
    a = a % mod;
    while (b > 0) {

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

// This function computes factorials and
// product by using above function i.e.
// modular multiplication
long long int findProduct(long long int N)
{
    // Initialize product and fact with 1
    long long int product = 1, fact = 1;
    long long int MOD = 1e9 + 7;
    for (int i = 1; i <= N; i++) {

        // ith factorial
        fact = mulmod(fact, i, MOD);

        // product of first i factorials
        product = mulmod(product, fact, MOD);

        // If at any iteration, product becomes
        // divisible by MOD, simply return 0;
        if (product == 0)
            return 0;
    }
    return product;
}

// Driver Code to Test above functions
int main()
{
    long long int N = 3;
    cout << findProduct(N) << endl;

    N = 5;
    cout << findProduct(N) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the
// product of first N factorials

class GFG{
// To compute (a * b) % MOD
static double mulmod(long a, long b,
                                    long mod)
{
    long res = 0; // Initialize result
    a = a % mod;
    while (b > 0) {

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

// This function computes factorials and
// product by using above function i.e.
// modular multiplication
static long findProduct(long N)
{
    // Initialize product and fact with 1
    long product = 1, fact = 1;
    long MOD = (long)(1e9 + 7);
    for (int i = 1; i <= N; i++) {

        // ith factorial
        fact = (long)mulmod(fact, i, MOD);

        // product of first i factorials
        product = (long)mulmod(product, fact, MOD);

        // If at any iteration, product becomes
        // divisible by MOD, simply return 0;
        if (product == 0)
            return 0;
    }
    return product;
}

// Driver Code to Test above functions
public static void main(String[] args)
{
    long N = 3;
    System.out.println(findProduct(N));

    N = 5;
    System.out.println(findProduct(N));

}
}
// this Code is contributed by mits
```

## 蟒蛇 3

```
# Python Program to find the
# product of first N factorials

# To compute (a * b) % MOD
def mulmod(a, b, mod):
    res = 0 # Initialize result
    a = a % mod
    while (b > 0):

        # If b is odd, add 'a' to result
        if (b % 2 == 1):
            res = (res + a) % mod

        # Multiply 'a' with 2
        a = (a * 2) % mod

        # Divide b by 2
        b //= 2

    # Return result
    return res % mod

# This function computes factorials and
# product by using above function i.e.
# modular multiplication
def findProduct(N):
    # Initialize product and fact with 1
    product = 1; fact = 1
    MOD = 1e9 + 7
    for i in range(1, N+1):

        # ith factorial
        fact = mulmod(fact, i, MOD)

        # product of first i factorials
        product = mulmod(product, fact, MOD)

        # If at any iteration, product becomes
        # divisible by MOD, simply return 0
        if not product:
            return 0
    return int(product)

# Driver Code to Test above functions
N = 3
print(findProduct(N))
N = 5
print(findProduct(N))

# This code is contributed by Ansu Kumari
```

## C#

```
// C#  Program to find the
// product of first N factorials

using System;

public class GFG{
    // To compute (a * b) % MOD
static double mulmod(long a, long b,
                                    long mod)
{
    long res = 0; // Initialize result
    a = a % mod;
    while (b > 0) {

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

// This function computes factorials and
// product by using above function i.e.
// modular multiplication
static long findProduct(long N)
{
    // Initialize product and fact with 1
    long product = 1, fact = 1;
    long MOD = (long)(1e9 + 7);
    for (int i = 1; i <= N; i++) {

        // ith factorial
        fact = (long)mulmod(fact, i, MOD);

        // product of first i factorials
        product = (long)mulmod(product, fact, MOD);

        // If at any iteration, product becomes
        // divisible by MOD, simply return 0;
        if (product == 0)
            return 0;
    }
    return product;
}

// Driver Code to Test above functions
    static public void Main (){
        long N = 3;
        Console.WriteLine(findProduct(N));
        N = 5;
        Console.WriteLine(findProduct(N));

}
}
//This Code is contributed by ajit.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find the
// product of first N factorials

// To compute (a * b) % MOD
function mulmod($a, $b, $mod)
{
    $res = 0; // Initialize result
    $a = $a % $mod;
    while ($b > 0)
    {

        // If b is odd, add 'a' to result
        if ($b % 2 == 1)
            $res = ($res + $a) % $mod;

        // Multiply 'a' with 2
        $a = ($a * 2) % $mod;

        // Divide b by 2
        $b /= 2;
    }

    // Return result
    return $res % $mod;
}

// This function computes factorials and
// product by using above function i.e.
// modular multiplication
function findProduct($N)
{
    // Initialize product and fact with 1
    $product = 1;
    $fact = 1;
    $MOD = 1000000000;
    for ($i = 1; $i <= $N; $i++)
    {

        // ith factorial
        $fact = mulmod($fact, $i, $MOD);

        // product of first i factorials
        $product = mulmod($product, $fact, $MOD);

        // If at any iteration, product becomes
        // divisible by MOD, simply return 0;
        if ($product == 0)
            return 0;
    }
    return $product;
}

// Driver Code
$N = 3;
echo findProduct($N),"\n";

$N = 5;
echo findProduct($N),"\n";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
    // Javascript Program to find the
    // product of first N factorials

    // To compute (a * b) % MOD
    function mulmod(a, b, mod)
    {
        let res = 0; // Initialize result
        a = a % mod;
        while (b > 0) {

            // If b is odd, add 'a' to result
            if (b % 2 == 1)
                res = (res + a) % mod;

            // Multiply 'a' with 2
            a = (a * 2) % mod;

            // Divide b by 2
            b = parseInt(b / 2, 10);
        }

        // Return result
        return res % mod;
    }

    // This function computes factorials and
    // product by using above function i.e.
    // modular multiplication
    function findProduct(N)
    {
        // Initialize product and fact with 1
        let product = 1, fact = 1;
        let MOD = (1e9 + 7);
        for (let i = 1; i <= N; i++) {

            // ith factorial
            fact = mulmod(fact, i, MOD);

            // product of first i factorials
            product = mulmod(product, fact, MOD);

            // If at any iteration, product becomes
            // divisible by MOD, simply return 0;
            if (product == 0)
                return 0;
        }
        return product;
    }

    let N = 3;
    document.write(findProduct(N) + "</br>");

    N = 5;
    document.write(findProduct(N));

</script>
```

**Output:** 

```
12
34560
```

**时间复杂度:** O(N * logN)，其中 O(log N)为模乘的时间复杂度。