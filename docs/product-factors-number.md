# 数的因子的乘积

> 原文:[https://www.geeksforgeeks.org/product-factors-number/](https://www.geeksforgeeks.org/product-factors-number/)

给定一个数 n，求 n 的所有因子的乘积，由于乘积可以很大，所以求它的模 10^9 + 7。
**例:**

```
Input : 12
Output : 1728
1 * 2 * 3 * 4 * 6 * 12 = 1728

Input : 18
Output : 5832
1 * 2 * 3 * 6 * 9 * 18 = 5832
```

**方法 1(天真的方法):**
我们可以对 I 运行从 1 到 n 的循环，如果 n 可被 I 整除，则乘以数字。该解决方案的时间复杂度为 0(n)。
但是这种方法对于大的 n 值是不够的。
**方法 2(更好的方法):**
更好的方法是运行 I 从 1 到 sqrt(n)的循环。如果数能被 I 整除，用 I 和 n/i 相乘，
这个解的时间复杂度是 O(sqrt(n))。

## C++

```
// C++ program to calculate product
// of factors of number
#include <bits/stdc++.h>
#define M 1000000007
using namespace std;

// function to product the factors
long long multiplyFactors(int n)
{
    long long prod = 1;
    for (int i = 1; i * i <= n; i++)
    {
        if (n % i == 0)
        {
            // If factors are equal,
            // multiply only once
            if (n / i == i)
                prod = (prod * i) % M;

            // Otherwise multiply both
            else {
                prod = (prod * i) % M;
                prod = (prod * n / i) % M;
            }
        }
    }
    return prod;
}

// Driver code
int main()
{
    int n = 12;

    cout << multiplyFactors(n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate product
// of factors of number
class GFG
{
public static final long M = 1000000007;

    // function to product the factors
    static long multiplyFactors(int n)
    {
        long prod = 1;
        for (int i = 1; i * i <= n; i++)
        {
            if (n % i == 0)
            {

                // If factors are equal,
                // multiply only once
                if (n / i == i)
                    prod = (prod * i) % M;

                // Otherwise multiply both
                else {
                    prod = (prod * i) % M;
                    prod = (prod * n / i) % M;
                }
            }
        }
        return prod;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 12;
        System.out.println(multiplyFactors(n));
    }
}
```

## 计算机编程语言

```
# Python program to calculate product
# of factors of number

M = 1000000007

# function to product the factors
def multiplyFactors(n) :
    prod = 1

    i = 1
    while i * i <= n :
        if (n % i == 0) :

            # If factors are equal,
            # multiply only once
            if (n / i == i) :
                prod = (prod * i) % M

            #Otherwise multiply both
            else :
                prod = (prod * i) % M
                prod = (prod * n / i) % M
        i = i + 1

    return prod

# Driver Code

n = 12
print (multiplyFactors(n))

# This code is contributed by Nikita Tiwari.
```

## C#

```
//C# program to calculate product
// of factors of number
using System;

class GFG
{
public static long M = 1000000007;

    // function to product the factors
    static long multiplyFactors(int n)
    {
        long prod = 1;
        for (int i = 1; i * i <= n; i++)
        {
            if (n % i == 0)
            {

                // If factors are equal,
                // multiply only once
                if (n / i == i)
                    prod = (prod * i) % M;

                // Otherwise multiply both
                else {
                    prod = (prod * i) % M;
                    prod = (prod * n / i) % M;
                }
            }
        }
        return prod;
    }

    // Driver Code
    public static void Main()
    {
        int n = 12;
        Console.Write(multiplyFactors(n));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to calculate product
// of factors of number

$M = 1000000007;

// function to product the factors
function multiplyFactors( $n)
{
    global $M;
    $prod = 1;
    for($i = 1; $i * $i <= $n; $i++)
    {
        if ($n % $i == 0)
        {

            // If factors are equal,
            // multiply only once
            if ($n / $i == $i)
                $prod = ($prod * $i) % $M;

            // Otherwise multiply both
            else
            {
                $prod = ($prod * $i) % $M;
                $prod = ($prod * $n / $i) % $M;
            }
        }
    }
    return $prod;
}

    // Driver Code
    $n = 12;
    echo multiplyFactors($n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// JavaScript program to calculate product
// of factors of number

// function to product the factors
function multiplyFactors( n)
{
    let M = 1000000007;
    let i;
    prod = 1;
    for(i = 1; i * i <= n; i++)
    {
        if (n % i == 0)
        {

            // If factors are equal,
            // multiply only once
            if (n / i == i)
                prod = (prod * i) % M;

            // Otherwise multiply both
            else
            {
                prod = (prod * i) % M;
                prod = (prod * n / i) % M;
            }
        }
    }
    return prod;
}

    // Driver Code
    n = 12;
    document.write(multiplyFactors(n));

// This code is contributed by sravan

</script>
```

**输出:**

```
1728
```

**方法 3(另一种方法):**
让我们观察一件事:

```
All factors of 12 are: 1, 2, 3, 4, 6, 12
1 * 2 * 3 * (2*2) * (2*3) * (2*2*3) = 2^6 * 3^3 = 12^3
and number of factors are 6
```

所以我们可以观察到因子的乘积将是因子/2 的 n^(number)。但是当因子数是奇数时(这意味着该数是完美平方)，在这种情况下，乘积将是因子/2 的 n^(number)* sqrt(n)。我们可以计算类似上述方法的因素数量。我们可以使用[模幂](https://www.geeksforgeeks.org/modular-exponentiation-power-in-modular-arithmetic/)
高效地计算功率

## C++

```
// C++ program to calculate product
// of factors of number
#include <bits/stdc++.h>
#define M 1000000007
using namespace std;

// Iterative Function to calculate
// (x^y) in O(log y)
long long power(long long x, long long y)
{
    long long res = 1;

    while (y > 0)
    {
        if (y & 1)
            res = (res * x) % M;
        y = (y >> 1) % M;
        x = (x * x) % M;
    }
    return res;
}

// function to count the factors
int countFactors(int n)
{
    int count = 0;
    for (int i = 1; i * i <= n; i++)
    {
        if (n % i == 0)
        {

            // If factors are equal,
            // count only once
            if (n / i == i)
                count++;

            // Otherwise count both
            else
                count += 2;
        }
    }
    return count;
}

long long multiplyFactors(int n)
{
    int numFactor = countFactors(n);

    // Calculate product of factors
    long long product = power(n, numFactor / 2);

    // If numFactor is odd return
    // power(n, numFactor/2) * sqrt(n)
    if (numFactor & 1)
        product = (product * (int)sqrt(n)) % M;

    return product;
}

// Driver code
int main()
{
    int n = 12;
    cout << multiplyFactors(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate product
// of factors of number
class GFG
{
public static final long M = 1000000007;

    // Iterative Function to calculate
    // (x^y) in O(log y)
    static long power(long x, long y)
    {
        long res = 1;

        while (y > 0)
        {
            if (y % 2 == 1)
                res = (res * x) % M;
            y = (y >> 1) % M;
            x = (x * x) % M;
        }
        return res;
    }

    // function to count the factors
    static int countFactors(int n)
    {
        int count = 0;
        for (int i = 1; i * i <= n; i++)
        {
            if (n % i == 0)
            {

                // If factors are equal,
                // count only once
                if (n / i == i)
                    count++;

                // Otherwise count both
                else
                    count += 2;
            }
        }
        return count;
    }

    static long multiplyFactors(int n)
    {
        int numFactor = countFactors(n);

        // Calculate product of factors
        long product = power(n, numFactor / 2);

        // If numFactor is odd return
        // power(n, numFactor/2) * sqrt(n)
        if (numFactor % 2 == 1)
            product = (product * (int)Math.sqrt(n)) % M;

        return product;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 12;
        System.out.println(multiplyFactors(n));
    }
}
```

## 计算机编程语言

```
# Python program to calculate product
# of factors of number

M = 1000000007

# Iterative Function to calculate
# (x^y) in O(log y)
def power(x, y) :

    res = 1
    while (y > 0) :

        if (y % 2 == 1) :
            res = (res * x) % M
        y = (y >> 1) % M
        x = (x * x) % M

    return res

# function to count the factors
def countFactors(n) :
    count = 0
    i = 1
    while i * i <= n :
        if (n % i == 0) :
            # If factors are equal,
            # count only once
            if (n / i == i) :
                count = count + 1

            # Otherwise count both
            else :
                count = count + 2
        i = i + 1
    return count

def multiplyFactors(n) :

    numFactor = countFactors(n)

    # Calculate product of factors
    product = power(n, numFactor / 2)

    # If numFactor is odd return
    # power(n, numFactor/2) * sqrt(n)
    if (numFactor % 2 == 1) :
        product = (product *
                (int)(math.sqrt(n))) % M

    return product

# Driver Code
n = 12
print multiplyFactors(n)

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to calculate product
// of factors of number
using System;

class GFG {

    public static long M = 1000000007;

    // Iterative Function to calculate
    // (x^y) in O(log y)
    static long power(long x, long y)
    {
        long res = 1;

        while (y > 0)
        {
            if (y % 2 == 1)
                res = (res * x) % M;
            y = (y >> 1) % M;
            x = (x * x) % M;
        }
        return res;
    }

    // function to count the factors
    static int countFactors(int n)
    {
        int count = 0;
        for (int i = 1; i * i <= n; i++)
        {
            if (n % i == 0)
            {

                // If factors are equal,
                // count only once
                if (n / i == i)
                    count++;

                // Otherwise count both
                else
                    count += 2;
            }
        }

        return count;
    }

    static long multiplyFactors(int n)
    {
        int numFactor = countFactors(n);

        // Calculate product of factors
        long product = power(n, numFactor / 2);

        // If numFactor is odd return
        // power(n, numFactor/2) * sqrt(n)
        if (numFactor % 2 == 1)
            product = (product *
                       (int)Math.Sqrt(n)) % M;

        return product;
    }

    // Driver Code
    public static void Main()
    {
        int n = 12;
        Console.Write(multiplyFactors(n));
    }
}

// This code is contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to calculate product
// of factors of number

$M = 1000000007;

// Iterative Function to calculate
// (x^y) in O(log y)
function power( $x, $y)
{
    global $M;
    $res = 1;

    while ($y > 0)
    {
        if ($y & 1)
            $res = ($res * $x) % $M;
        $y = ($y >> 1) % $M;
        $x = ($x *$x) % $M;
    }
    return $res;
}

// function to count the factors
function countFactors( $n)
{
    $count = 0;
    for ($i = 1; $i * $i <= $n; $i++)
    {
        if ($n % $i == 0)
        {

            // If factors are equal,
            // count only once
            if ($n / $i == $i)
                $count++;

            // Otherwise count both
            else
                $count += 2;
        }
    }
    return $count;
}

function multiplyFactors( $n)
{
    $numFactor = countFactors($n);

    // Calculate product of factors
    $product = power($n, $numFactor / 2);

    // If numFactor is odd return
    // power(n, numFactor/2) * sqrt(n)
    if ($numFactor & 1)
        $product = ($product * sqrt($n)) % $M;

    return $product;
}

    // Driver code
    $n = 12;
    echo multiplyFactors($n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
// Javascript program to calculate product
// of factors of number

let M = 1000000007;

    // Iterative Function to calculate
    // (x^y) in O(log y)
    function power(x, y)
    {
        let res = 1;

        while (y > 0)
        {
            if (y % 2 == 1)
                res = (res * x) % M;
            y = (y >> 1) % M;
            x = (x * x) % M;
        }
        return res;
    }

    // function to count the factors
    function countFactors(n)
    {
        let count = 0;
        for (let i = 1; i * i <= n; i++)
        {
            if (n % i == 0)
            {

                // If factors are equal,
                // count only once
                if (n / i == i)
                    count++;

                // Otherwise count both
                else
                    count += 2;
            }
        }
        return count;
    }

    function multiplyFactors(n)
    {
        let numFactor = countFactors(n);

        // Calculate product of factors
        let product = power(n, numFactor / 2);

        // If numFactor is odd return
        // power(n, numFactor/2) * sqrt(n)
        if (numFactor % 2 == 1)
            product = (product * Math.sqrt(n)) % M;

        return product;
    }

// driver function

        let n = 12;
        document.write(multiplyFactors(n));

</script>   
```

**输出:**

```
1728
```

本文由**核素**投稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。