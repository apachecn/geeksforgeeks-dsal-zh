# 给定 N 个简化形式分数的乘积

> 原文:[https://www . geesforgeks . org/product-given-n-fractions-reduced-form/](https://www.geeksforgeeks.org/product-given-n-fractions-reduced-form/)

给定 N 个分数的分子和分母。任务是找到 N 分数的乘积，并以简化形式输出答案。
**例:**

```
Input : N = 3
        num[] = { 1, 2, 5 }
        den[] = { 2, 1, 6 }
Output : 5/6
Product of 1/2 * 2/1 * 5/6 is 10/12.
Reduced form of 10/12 is 5/6.

Input : N = 4
        num[] = { 1, 2, 5, 9 }
        den[] = { 2, 1, 6, 27 }
Output : 5/18
```

想法是在一个变量中找到分子的乘积，比如 new_num。现在，在另一个变量中找到分母的乘积，比如 new_den。
现在，要以约简形式求答案，求 new_num 和 new_den 的最大公约数，并用计算出的 GCD 除 new_num 和 new_den。
以下是本办法的实施:

## C++

```
// CPP program to find product of N
// fractions in reduced form.
#include <bits/stdc++.h>
using namespace std;

// Function to return gcd of a and b
int gcd(int a, int b)
{
    if (a == 0)
        return b;
    return gcd(b % a, a);
}

// Print the Product of N fraction in Reduced Form.
void productReduce(int n, int num[], int den[])
{
    int new_num = 1, new_den = 1;

    // finding the product of all N
    // numerators and denominators.
    for (int i = 0; i < n; i++) {
        new_num *= num[i];
        new_den *= den[i];
    }

    // Finding GCD of new numerator and
    // denominator
    int GCD = gcd(new_num, new_den);

    // Converting into reduced form.
    new_num /= GCD;
    new_den /= GCD;

    cout << new_num << "/" << new_den << endl;
}

// Driven Program
int main()
{
    int n = 3;
    int num[] = { 1, 2, 5 };
    int den[] = { 2, 1, 6 };

    productReduce(n, num, den);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find product of N
// fractions in reduced form.

import java.io.*;

class GFG {
// Function to return gcd of a and b
static int gcd(int a, int b)
{
    if (a == 0)
        return b;
    return gcd(b % a, a);
}

// Print the Product of N fraction in
// Reduced Form.
static void productReduce(int n, int num[],
                                   int den[])
{
    int new_num = 1, new_den = 1;

    // finding the product of all N
    // numerators and denominators.
    for (int i = 0; i < n; i++) {
        new_num *= num[i];
        new_den *= den[i];
    }

    // Finding GCD of new numerator and
    // denominator
    int GCD = gcd(new_num, new_den);

    // Converting into reduced form.
    new_num /= GCD;
    new_den /= GCD;

    System.out.println(new_num + "/" +new_den);
}

    // Driven Program
    public static void main (String[] args) {

        int n = 3;
        int num[] = { 1, 2, 5 };
        int den[] = { 2, 1, 6 };

        productReduce(n, num, den);

    }
}

//This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python3 program to find
# product of N fractions
# in reduced form.

# Function to return
# gcd of a and b
def gcd(a, b):
    if (a == 0):
        return b;
    return gcd(b % a, a);

# Print the Product of N
# fraction in Reduced Form.
def productReduce(n, num, den):
    new_num = 1;
    new_den = 1;

    # finding the product
    # of all N numerators
    # and denominators.
    for i in range(n):
        new_num = new_num * num[i];
        new_den = new_den * den[i];

    # Finding GCD of
    # new numerator
    # and denominator
    GCD = gcd(new_num, new_den);

    # Converting into
    # reduced form.
    new_num = new_num / GCD;
    new_den = new_den / GCD;

    print(int(new_num), "/",
              int(new_den));

# Driver Code
n = 3;
num = [1, 2, 5];
den = [2, 1, 6];
productReduce(n, num, den);

# This code is contributed
# by mits
```

## C#

```
// C# program to find product of N
// fractions in reduced form.

using System;

class GFG {

    // Function to return gcd of a and b
    static int gcd(int a, int b)
    {
        if (a == 0)
            return b;

        return gcd(b % a, a);
    }

    // Print the Product of N fraction in
    // Reduced Form.
    static void productReduce(int n, int []num,
                                    int []den)
    {
        int new_num = 1, new_den = 1;

        // finding the product of all N
        // numerators and denominators.
        for (int i = 0; i < n; i++) {
            new_num *= num[i];
            new_den *= den[i];
        }

        // Finding GCD of new numerator and
        // denominator
        int GCD = gcd(new_num, new_den);

        // Converting into reduced form.
        new_num /= GCD;
        new_den /= GCD;

        Console.WriteLine(new_num + "/" +new_den);
    }

    // Driven Program
    public static void Main () {

        int n = 3;
        int []num = { 1, 2, 5 };
        int []den = { 2, 1, 6 };

        productReduce(n, num, den);

    }
}

//This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find product of N
// fractions in reduced form.

// Function to return
// gcd of a and b
function gcd($a, $b)
{
    if ($a == 0)
        return $b;
    return gcd($b % $a, $a);
}

// Print the Product of N
// fraction in Reduced Form.
function productReduce($n, $num, $den)
{
    $new_num = 1; $new_den = 1;

    // finding the product of all N
    // numerators and denominators.
    for ($i = 0; $i < $n; $i++)
    {
        $new_num *= $num[$i];
        $new_den *= $den[$i];
    }

    // Finding GCD of new
    // numerator and denominator
    $GCD = gcd($new_num, $new_den);

    // Converting into reduced form.
    $new_num /= $GCD;
    $new_den /= $GCD;

    echo $new_num , "/" , $new_den ,"\n";
}

    // Driver Code
    $n = 3;
    $num = array(1, 2, 5);
    $den = array(2, 1, 6);

    productReduce($n, $num, $den);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// JavaScript program to find product of N
// fractions in reduced form.

// Function to return gcd of a and b
function  gcd( a,  b)
{
    if (a == 0)
        return b;
    return gcd(b % a, a);
}

// Print the Product of N fraction in Reduced Form.

function  productReduce( n,  num , den)
{
     let new_num = 1, new_den = 1;

    // finding the product of all N
    // numerators and denominators.
    for (let i = 0; i < n; i++) {
        new_num *= num[i];
        new_den *= den[i];
    }

    // Finding GCD of new numerator and
    // denominator
    let GCD = gcd(new_num, new_den);

    // Converting into reduced form.
    new_num /= GCD;
    new_den /= GCD;

    document.write( new_num + "/" + new_den);
}

// Driven Program

    let n = 3;
    let num = [ 1, 2, 5 ];
    let den = [ 2, 1, 6 ];

    productReduce(n, num, den);

// This code contributed by aashish1995

</script>
```

**输出:**

```
5/6
```

**如何避免溢出？**
上述解决方案导致大量溢出。我们可以通过首先找到所有记数器和分母的质因数来避免溢出。一旦我们找到了素因子，我们就可以取消常见的素因子。
**注意:**当要求你以{ p \u q } ^ {-1 } }的形式表示答案时。
对于这些问题，首先将分子和分母以可约形式 P / Q 转换，如上所述。然后，求 q 相对于一个质数 m(一般是 10^9 + 7)的模乘逆。求 Q 的模乘逆后，与 P 相乘，取给定素数 m 的模，得到我们需要的输出。
//感谢 [VaiBzZk](https://auth.geeksforgeeks.org/user/VaiBzZk/articles) 提示此情况。