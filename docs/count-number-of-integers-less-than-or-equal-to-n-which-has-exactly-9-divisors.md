# 计算小于或等于 N 的整数个数，正好有 9 个除数

> 原文:[https://www . geesforgeks . org/count-number-of-integer-小于或等于-n-其中-恰好有-9 个除数/](https://www.geeksforgeeks.org/count-number-of-integers-less-than-or-equal-to-n-which-has-exactly-9-divisors/)

给定一个数 N(1 <=N<=10 <sup>9</sup> ，任务是找出小于等于 N 的整数的总数，这些整数正好有 9 个除数。

**示例:**

> **输入:**N = 100
> T3】输出: 2
> 正好有 9 除数的两个数是 36 和 100。
> **输入:** N = 1000
> **输出:** 8
> 数字为 36 100 196 225 256 441 484 676

一种**天真的方法**是对所有数字进行迭代，直到 N，并计算正好有 9 个除数的数字。为了计算除数，人们可以很容易地迭代到 N，检查 N 是否能被 I 整除，并保持计数。

下面是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count factors in O(N)
int numberOfDivisors(int num)
{
    int c = 0;

    // iterate and check if factor or not
    for (int i = 1; i <= num; i++) {
        if (num % i == 0) {
            c += 1;
        }
    }
    return c;
}

// Function to count numbers having
// exactly 9 divisors
int countNumbers(int n)
{
    int c = 0;

    // check for all numbers <=N
    for (int i = 1; i <= n; i++) {
        // check if exactly 9 factors or not
        if (numberOfDivisors(i) == 9)
            c += 1;
    }
    return c;
}

// Driver Code
int main()
{
    int n = 1000;

    cout << countNumbers(n);

return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach

import java.io.*;

class GFG {

// Function to count factors in O(N)
static int numberOfDivisors(int num)
{
    int c = 0;

    // iterate and check if factor or not
    for (int i = 1; i <= num; i++) {
        if (num % i == 0) {
            c += 1;
        }
    }
    return c;
}

// Function to count numbers having
// exactly 9 divisors
static int countNumbers(int n)
{
    int c = 0;

    // check for all numbers <=N
    for (int i = 1; i <= n; i++) {
        // check if exactly 9 factors or not
        if (numberOfDivisors(i) == 9)
            c += 1;
    }
    return c;
}

       // Driver Code
    public static void main (String[] args) {
    int n = 1000;

    System.out.print(countNumbers(n));
    }
}

// This code is contributed by inder_verma..
```

## 蟒蛇 3

```
# Python 3 implementation of
# above approach

# Function to count factors in O(N)
def numberOfDivisors(num):
    c = 0

    # iterate and check if
    # factor or not
    for i in range(1, num + 1) :
        if (num % i == 0) :
            c += 1

    return c

# Function to count numbers having
# exactly 9 divisors
def countNumbers(n):

    c = 0

    # check for all numbers <=N
    for i in range(1, n + 1) :

        # check if exactly 9 factors or not
        if (numberOfDivisors(i) == 9):
            c += 1
    return c

# Driver Code
if __name__ == "__main__":
    n = 1000

    print(countNumbers(n))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

// Function to count factors in O(N)
static int numberOfDivisors(int num)
{
    int c = 0;

    // iterate and check if factor or not
    for (int i = 1; i <= num; i++)
    {
        if (num % i == 0)
        {
            c += 1;
        }
    }
    return c;
}

// Function to count numbers having
// exactly 9 divisors
static int countNumbers(int n)
{
    int c = 0;

    // check for all numbers <=N
    for (int i = 1; i <= n; i++) {
        // check if exactly 9 factors or not
        if (numberOfDivisors(i) == 9)
            c += 1;
    }
    return c;
}

// Driver Code
public static void Main ()
{
int n = 1000;

Console.Write(countNumbers(n));
}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Function to count factors in O(N)
Function numberOfDivisors($num)
{
    $c = 0;

    // iterate and check
    // if factor or not
    for ($i = 1; $i <= $num; $i++) {

        if ($num % $i == 0) {
            $c += 1;
        }
    }
    return $c;
}

// Function to count numbers
// having exactly 9 divisors
Function countNumbers($n)
{
    $c = 0;

    // check for all numbers <=N
    for ($i = 1; $i <= $n; $i++) {

        // check if exactly 9 factors or not
        if (numberOfDivisors($i) == 9)
            $c += 1;
    }
    return $c;
}

// Driver Code
$n = 1000;

echo countNumbers($n);

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

    // Javascript implementation of above approach

    // Function to count factors in O(N)
    function numberOfDivisors(num)
    {
        let c = 0;

        // iterate and check if factor or not
        for (let i = 1; i <= num; i++)
        {
            if (num % i == 0)
            {
                c += 1;
            }
        }
        return c;
    }

    // Function to count numbers having
    // exactly 9 divisors
    function countNumbers(n)
    {
        let c = 0;

        // check for all numbers <=N
        for (let i = 1; i <= n; i++) {
            // check if exactly 9 factors or not
            if (numberOfDivisors(i) == 9)
                c += 1;
        }
        return c;
    }

    let n = 1000;

    document.write(countNumbers(n));

</script>
```

**Output:** 

```
8
```

一种有效的方法是利用质因数的性质来计算一个数的除数。方法可以在[这里](https://www.geeksforgeeks.org/total-number-divisors-given-number/)找到。如果任何数(让 x)可以用(p^2 * q^2)或(p^8)表示，其中 p 和 q 是 x 的质因数，那么 x 总共有 9 个除数。可以遵循以下步骤来解决上述问题。

1.  使用[筛选技术](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)标记一个数的最小质因数。
2.  我们只需要检查**范围内所有可以用 p*q 表示的数字【1-sqrt(n)】**，因为 **(p^2*q^2)** 有 9 个因子，因此**(p*q)^2)**也正好有 9 个因子。
3.  从 1 迭代到 sqrt(n)，检查 I 是否可以表示为 **p*q** ，其中 p 和 q 是质数。
4.  此外，检查 I 是否为素数，然后再计算 I(8)的幂(I，8) < =n 的幂，如果是，也计算这个数。
5.  可以用 p*q 和 p^8 的形式表示的数的总和就是我们的答案。

以下是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count numbers having
// exactly 9 divisors
int countNumbers(int n)
{
    int c = 0;

    int limit = sqrt(n);

    // Sieve array
    int prime[limit + 1];

    // initially prime[i] = i
    for (int i = 1; i <= limit; i++)
        prime[i] = i;

    // use sieve concept to store the
    // first prime factor of every number
    for (int i = 2; i * i <= limit; i++) {
        if (prime[i] == i) {
            // mark all factors of i
            for (int j = i * i; j <= limit; j += i)
                if (prime[j] == j)
                    prime[j] = i;
        }
    }

    // check for all numbers if they can be
    // expressed in form p*q
    for (int i = 2; i <= limit; i++) {
        // p prime factor
        int p = prime[i];

        // q prime factor
        int q = prime[i / prime[i]];

        // if both prime factors are different
        // if p*q<=n and q!=
        if (p * q == i && q != 1 && p != q) {
            c += 1;
        }
        else if (prime[i] == i) {

            // Check if it can be expressed as p^8
            if (pow(i, 8) <= n) {

                c += 1;
            }
        }
    }

    return c;
}

// Driver Code
int main()
{
    int n = 1000;

    cout << countNumbers(n);

return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
public class GFG {

// Function to count numbers having
// exactly 9 divisors
    static int countNumbers(int n) {
        int c = 0;

        int limit = (int) Math.sqrt(n);

        // Sieve array
        int prime[] = new int[limit + 1];

        // initially prime[i] = i
        for (int i = 1; i <= limit; i++) {
            prime[i] = i;
        }

        // use sieve concept to store the
        // first prime factor of every number
        for (int i = 2; i * i <= limit; i++) {
            if (prime[i] == i) {
                // mark all factors of i
                for (int j = i * i; j <= limit; j += i) {
                    if (prime[j] == j) {
                        prime[j] = i;
                    }
                }
            }
        }

        // check for all numbers if they can be
        // expressed in form p*q
        for (int i = 2; i <= limit; i++) {
            // p prime factor
            int p = prime[i];

            // q prime factor
            int q = prime[i / prime[i]];

            // if both prime factors are different
            // if p*q<=n and q!=
            if (p * q == i && q != 1 && p != q) {
                c += 1;
            } else if (prime[i] == i) {

                // Check if it can be expressed as p^8
                if (Math.pow(i, 8) <= n) {

                    c += 1;
                }
            }
        }

        return c;
    }

// Driver Code
    public static void main(String[] args) {
        int n = 1000;

        System.out.println(countNumbers(n));

    }
}
/*This code is contributed by PrinciRaj1992*/
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to count numbers
# having exactly 9 divisors
def countNumbers(n):

    c = 0
    limit = int(n ** (0.5))

    # Sieve array, initially prime[i] = i
    prime = [i for i in range(limit + 1)]

    # use sieve concept to store the
    # first prime factor of every number
    i = 2
    while i * i <= limit:
        if prime[i] == i:

            # mark all factors of i
            for j in range(i * i, limit + 1, i):
                if prime[j] == j:
                    prime[j] = i

        i += 1

    # check for all numbers if they
    # can be expressed in form p*q
    for i in range(2, limit + 1):

        # p prime factor
        p = prime[i]

        # q prime factor
        q = prime[i // prime[i]]

        # if both prime factors are different
        # if p*q<=n and q!=
        if p * q == i and q != 1 and p != q:
            c += 1

        elif prime[i] == i:

            # Check if it can be
            # expressed as p^8
            if i ** 8 <= n:
                c += 1

    return c

# Driver Code
if __name__ == "__main__":

    n = 1000
    print(countNumbers(n))

# This code is contributed
# by Rituraj Jain
```

## C#

```
// C# implementation of above approach
using System;

public class GFG {

// Function to count numbers having
// exactly 9 divisors
    static int countNumbers(int n) {
        int c = 0;

        int limit = (int) Math.Sqrt(n);

        // Sieve array
        int []prime = new int[limit + 1];

        // initially prime[i] = i
        for (int i = 1; i <= limit; i++) {
            prime[i] = i;
        }

        // use sieve concept to store the
        // first prime factor of every number
        for (int i = 2; i * i <= limit; i++) {
            if (prime[i] == i) {
                // mark all factors of i
                for (int j = i * i; j <= limit; j += i) {
                    if (prime[j] == j) {
                        prime[j] = i;
                    }
                }
            }
        }

        // check for all numbers if they can be
        // expressed in form p*q
        for (int i = 2; i <= limit; i++) {
            // p prime factor
            int p = prime[i];

            // q prime factor
            int q = prime[i / prime[i]];

            // if both prime factors are different
            // if p*q<=n and q!=
            if (p * q == i && q != 1 && p != q) {
                c += 1;
            } else if (prime[i] == i) {

                // Check if it can be expressed as p^8
                if (Math.Pow(i, 8) <= n) {

                    c += 1;
                }
            }
        }

        return c;
    }

// Driver Code
    public static void Main() {
        int n = 1000;

        Console.WriteLine(countNumbers(n));

    }
}
/*This code is contributed by PrinciRaj1992*/
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach
// Function to count numbers having
// exactly 9 divisors

function countNumbers($n)
{
    $c = 0;
    $limit = sqrt($n);

    // Sieve array
    $prime[$limit + 1] = array(0);

    // initially prime[i] = i
    for ($i = 1; $i <= $limit; $i++)
        $prime[$i] = $i;

    // use sieve concept to store the
    // first prime factor of every number
    for ($i = 2; $i * $i <= $limit; $i++)
    {
        if ($prime[$i] == $i)
        {
            // mark all factors of i
            for ($j = $i * $i;
                 $j <= $limit; $j += $i)
                if ($prime[$j] == $j)
                    $prime[$j] = $i;
        }
    }

    // check for all numbers if they
    // can be expressed in form p*q
    for ($i = 2; $i <= $limit; $i++)
    {
        // p prime factor
        $p = $prime[$i];

        // q prime factor
        $q = $prime[$i / $prime[$i]];

        // if both prime factors are different
        // if p*q<=n and q!=
        if ($p * $q == $i && $q != 1 && $p != $q)
        {
            $c += 1;
        }
        else if ($prime[$i] == $i)
        {

            // Check if it can be expressed as p^8
            if (pow($i, 8) <= $n)
            {

                $c += 1;
            }
        }
    }

    return $c;
}

// Driver Code
$n = 1000;
echo countNumbers($n);

// This code is contributed by jit_t
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of above approach

    // Function to count numbers having
    // exactly 9 divisors
    function countNumbers(n) {
        let c = 0;

        let limit = parseInt(Math.sqrt(n), 10);

        // Sieve array
        let prime = new Array(limit + 1);
        prime.fill(0);

        // initially prime[i] = i
        for (let i = 1; i <= limit; i++) {
            prime[i] = i;
        }

        // use sieve concept to store the
        // first prime factor of every number
        for (let i = 2; i * i <= limit; i++) {
            if (prime[i] == i) {
                // mark all factors of i
                for (let j = i * i; j <= limit; j += i) {
                    if (prime[j] == j) {
                        prime[j] = i;
                    }
                }
            }
        }

        // check for all numbers if they can be
        // expressed in form p*q
        for (let i = 2; i <= limit; i++) {
            // p prime factor
            let p = prime[i];

            // q prime factor
            let q = prime[parseInt(i / prime[i], 10)];

            // if both prime factors are different
            // if p*q<=n and q!=
            if (p * q == i && q != 1 && p != q) {
                c += 1;
            } else if (prime[i] == i) {

                // Check if it can be expressed as p^8
                if (Math.pow(i, 8) <= n) {

                    c += 1;
                }
            }
        }

        return c;
    }

    let n = 1000;

    document.write(countNumbers(n));

</script>
```

**Output:** 

```
8
```

**时间复杂度:** O(sqrt(N))
**辅助空间:** O(sqrt(N))