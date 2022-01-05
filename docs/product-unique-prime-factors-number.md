# 一个数的唯一质因数的乘积

> 原文:[https://www . geesforgeks . org/product-unique-prime-factors-number/](https://www.geeksforgeeks.org/product-unique-prime-factors-number/)

给定一个数 n，我们需要找到它所有唯一素因子的乘积。[质因数:](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)基本上是数本身就是质数的一个因数。
**例:**

```
Input: num = 10
Output: Product is 10
Explanation:
Here, the input number is 10 having only 2 prime factors and they are 5 and 2.
And hence their product is 10.

Input : num = 25
Output: Product is 5
Explanation:
Here, for the input to be 25  we have only one unique prime factor i.e 5.
And hence the required product is 5.
```

**方法 1(简单)**
使用从 i = 2 到 n 的循环，检查 I 是否是 n 的因子，然后检查 I 是否是质数本身，如果是，则将乘积存储在乘积变量中，并继续该过程，直到 I = n。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to find product of
// unique prime factors of a number
#include <bits/stdc++.h>
using namespace std;

long long int productPrimeFactors(int n)
{
    long long int product = 1;

    for (int i = 2; i <= n; i++) {

        // Checking if 'i' is factor of num
        if (n % i == 0) {

            // Checking if 'i' is a Prime number
            bool isPrime = true;
            for (int j = 2; j <= i / 2; j++) {
                if (i % j == 0) {
                    isPrime = false;
                    break;
                }
            }

            // condition if 'i' is Prime number
            // as well as factor of num
            if (isPrime) {
                product = product * i;
            }
        }
    }

    return product;
}

// driver function
int main()
{
    int n = 44;
    cout << productPrimeFactors(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find product of
// unique prime factors of a number.

class GFG {
    public static long productPrimeFactors(int n)
    {
        long product = 1;

        for (int i = 2; i <= n; i++) {
            // Checking if 'i' is factor of num
            if (n % i == 0) {

                // Checking if 'i' is a Prime number
                boolean isPrime = true;
                for (int j = 2; j <= i / 2; j++) {
                    if (i % j == 0) {
                        isPrime = false;
                        break;
                    }
                }

                // condition if 'i' is Prime number
                // as well as factor of num
                if (isPrime) {
                    product = product * i;
                }
            }
        }
        return product;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 44;
        System.out.print(productPrimeFactors(n));
    }
}

// This code is contributed by _omg
```

## 蟒蛇 3

```
# Python program to find sum of given
# series.

def productPrimeFactors(n):
    product = 1

    for i in range(2, n + 1):
        if (n % i == 0):
            isPrime = 1

            for j in range(2, int(i / 2 + 1)):
                if (i % j == 0):
                    isPrime = 0
                    break

            # condition if 'i' is Prime number
            # as well as factor of num
            if (isPrime):
                product = product * i

    return product 

# main()
n = 44
print (productPrimeFactors(n))

# Contributed by _omg
```

## C#

```
// C# program to find product of
// unique prime factors of a number.
using System;

class GFG {

    // Function to find product of unique
    // prime factors of a number
    public static long productPrimeFactors(int n)
    {
        long product = 1;

        for (int i = 2; i <= n; i++) {

            // Checking if 'i' is factor of num
            if (n % i == 0) {

                // Checking if 'i' is a Prime number
                bool isPrime = true;
                for (int j = 2; j <= i / 2; j++) {
                    if (i % j == 0) {
                        isPrime = false;
                        break;
                    }
                }

                // condition if 'i' is Prime number
                // as well as factor of num
                if (isPrime) {
                    product = product * i;
                }
            }
        }
        return product;
    }

    // Driver Code
    public static void Main()
    {
        int n = 44;
        Console.Write(productPrimeFactors(n));
    }
}

// This code is contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// product of unique
// prime factors of a number

function productPrimeFactors($n)
{
    $product = 1;

    for ($i = 2; $i <= $n; $i++)
    {

        // Checking if 'i' is
        // factor of num
        if ($n % $i == 0)
        {

            // Checking if 'i' is
            // a Prime number
            $isPrime = true;
            for ($j = 2; $j <= $i / 2; $j++)
            {
                if ($i % $j == 0)
                {
                    $isPrime = false;
                    break;        
                }
            }

            // condition if 'i' is
            // Prime number as well
            // as factor of num
            if ($isPrime)
            {
                $product = $product * $i;
            }
        }
    }

    return $product;
}

// Driver Code
$n = 44;
echo(productPrimeFactors($n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// JavaScript program to find product of
// unique prime factors of a number.

    function productPrimeFactors(n)
    {
        let product = 1;

        for (let i = 2; i <= n; i++) {
            // Checking if 'i' is factor of num
            if (n % i == 0) {

                // Checking if 'i' is a Prime number
                let isPrime = true;
                for (let j = 2; j <= i / 2; j++) {
                    if (i % j == 0) {
                        isPrime = false;
                        break;
                    }
                }

                // condition if 'i' is Prime number
                // as well as factor of num
                if (isPrime) {
                    product = product * i;
                }
            }
        }
        return product;
    }

// Driver Code

        let n = 44;
        document.write(productPrimeFactors(n));

// This code is contributed by avijitmondal1998.
</script>
```

**Output :** 

```
22
```

**方法 2(高效)**
这个想法是基于[高效程序打印给定数字的所有质因数](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to find product of
// unique prime factors of a number
#include <bits/stdc++.h>
using namespace std;

// A function to print all prime
// factors of a given number n
long long int productPrimeFactors(int n)
{
    long long int product = 1;

    // Handle prime factor 2 explicitly
    // so that can optimally handle
    // other prime factors.
    if (n % 2 == 0) {
        product *= 2;
        while (n % 2 == 0)
            n = n / 2;
    }

    // n must be odd at this point.
    // So we can skip one element
    // (Note i = i + 2)
    for (int i = 3; i <= sqrt(n); i = i + 2) {
        // While i divides n, print
        // i and divide n
        if (n % i == 0) {
            product = product * i;
            while (n % i == 0)
                n = n / i;
        }
    }

    // This condition is to handle the
    // case when n is a prime number
    // greater than 2
    if (n > 2)
        product = product * n;

    return product;
}

// Driver Code
int main()
{
    int n = 44;
    cout << productPrimeFactors(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find product of
// unique prime factors of a number.
import java.util.*;
import java.lang.*;

class GFG {
    public static long productPrimeFactors(int n)
    {
        long product = 1;
        // Handle prime factor 2
        // explicitly so that can
        // optimally handle other
        // prime factors.
        if (n % 2 == 0) {
            product *= 2;
            while (n % 2 == 0)
                n = n / 2;
        }

        // n must be odd at this point.
        // So we can skip one element
        // (Note i = i +2)
        for (int i = 3; i <= Math.sqrt(n); i = i + 2) {
            // While i divides n, print
            // i and divide n
            if (n % i == 0) {
                product = product * i;
                while (n % i == 0)
                    n = n / i;
            }
        }

        // This condition is to handle
        // the case when n is a prime
        // number greater than 2
        if (n > 2)
            product = product * n;

        return product;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 44;
        System.out.print(productPrimeFactors(n));
    }
}

// This code is contributed by _omg
```

## 蟒蛇 3

```
# Python program to find product of
# unique prime factors of a number

import math

def productPrimeFactors(n):
    product = 1

    # Handle prime factor 2 explicitly so that
    # can optimally handle other prime factors.
    if (n % 2 == 0):
        product *= 2
        while (n % 2 == 0):
            n = n / 2

    # n must be odd at this point. So we can
    # skip one element (Note i = i + 2)
    for i in range (3, int(math.sqrt(n))+1, 2):
        # While i divides n, print i and
        # divide n
        if (n % i == 0):
            product = product * i
            while (n % i == 0):
                n = n / i

    # This condition is to handle the case when n
    # is a prime number greater than 2
    if (n > 2):
        product = product * n

    return product    

# main()
n = 44
print (int(productPrimeFactors(n)))

# Contributed by _omg
```

## C#

```
// C# program to find product
// of unique prime factors
// of a number.
using System;

public class GFG {

    // Function to find product
    // of prime factors
    public static long productPrimeFactors(int n)
    {
        long product = 1;

        // Handle prime factor 2 explicitly
        // so that can optimally handle
        // other prime factors.
        if (n % 2 == 0) {
            product *= 2;
            while (n % 2 == 0)
                n = n / 2;
        }

        // n must be odd at this point.
        // So we can skip one
        // element (Note i = i + 2)
        for (int i = 3; i <= Math.Sqrt(n);
             i = i + 2) {

            // While i divides n, print
            // i and divide n
            if (n % i == 0) {
                product = product * i;
                while (n % i == 0)
                    n = n / i;
            }
        }

        // This condition is to handle
        // the case when n is a prime
        // number greater than 2
        if (n > 2)
            product = product * n;

        return product;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int n = 44;
        Console.Write(productPrimeFactors(n));
    }
}

// This code is contributed by parashar...
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find product of
// unique prime factors of a number

// A function to print all prime
// factors of a given number n
function productPrimeFactors( $n)
{
    $product = 1;

    // Handle prime factor 2 
    // explicitly so that can
    // optimally handle other
    // prime factors.
    if ($n % 2 == 0)
    {
        $product *= 2;
        while ($n % 2 == 0)
            $n = $n / 2;
    }

    // n must be odd at this point.
    // So we can skip one element
    // (Note i = i + 2)
    for ($i = 3; $i <= sqrt($n); $i = $i + 2)
    {
        // While i divides n, print
        // i and divide n
        if ($n % $i == 0)
        {
            $product = $product * $i;
            while ($n % $i == 0)
                $n = $n / $i;
        }
    }

    // This condition is to handle the
    // case when n is a prime number
    // greater than 2
    if ($n > 2)
        $product = $product * $n;

    return $product;
}

// Driver Code
$n = 44;
echo productPrimeFactors($n);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Javascript program to find product of
// unique prime factors of a number.

    function productPrimeFactors(n)
    {
        var product = 1;
        // Handle prime factor 2
        // explicitly so that can
        // optimally handle other
        // prime factors.
        if (n % 2 == 0) {
            product *= 2;
            while (n % 2 == 0)
                n = n / 2;
        }

        // n must be odd at this point.
        // So we can skip one element
        // (Note i = i +2)
        for (i = 3; i <= Math.sqrt(n); i = i + 2)
        {
            // While i divides n, print
            // i and divide n
            if (n % i == 0) {
                product = product * i;
                while (n % i == 0)
                    n = n / i;
            }
        }

        // This condition is to handle
        // the case when n is a prime
        // number greater than 2
        if (n > 2)
            product = product * n;

        return product;
    }

    // Driver Code

        var n = 44;
        document.write(productPrimeFactors(n));

// This code contributed by aashish1995

</script>
```

**Output :** 

```
22
```