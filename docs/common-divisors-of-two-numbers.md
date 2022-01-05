# 两个数的公约数

> 原文:[https://www . geeksforgeeks . org/两个数字的公约数/](https://www.geeksforgeeks.org/common-divisors-of-two-numbers/)

给定两个整数，任务是求给定数的所有公约数？

**示例:**

```
Input : a = 12, b = 24
Output: 6
// all common divisors are 1, 2, 3, 
// 4, 6 and 12

Input : a = 3, b = 17
Output: 1
// all common divisors are 1

Input : a = 20, b = 36
Output: 3
// all common divisors are 1, 2, 4
```

建议参考[给定数的所有除数](https://www.geeksforgeeks.org/find-all-divisors-of-a-natural-number-set-2/)作为本文的前提。

**天真的解决方案**
一个简单的解决方案是首先找到第一个数的所有除数，并将它们存储在数组或散列中。然后找到第二个数的公约数并存储。最后打印两个存储数组或散列的公共元素。关键是一个除数的素因子的幂的大小应该等于 a 和 b 两个素因子的最小幂。

*   利用[素分解](prime factorization)求 a 的素因子。
*   找出 **a** 的每个质因数的个数，并存储在 Hashmap 中。
*   使用 **a** 的不同素因子对 **b** 进行素因子分解。
*   那么除数的总数将等于每个因子的**(计数+ 1)**
    的乘积。
*   **计数**是 **a** 和**b**的每个质因数的最小计数
*   这给出了 **a** 和 **b** 的所有约数。

## C++

```
// C++ implementation of program
#include <bits/stdc++.h>
using namespace std;

// Map to store the count of each
// prime factor of a
map<int, int> ma;

// Function that calculate the count of
// each prime factor of a number
void primeFactorize(int a)
{
    for(int i = 2; i * i <= a; i += 2)
    {
        int cnt = 0;
        while (a % i == 0)
        {
            cnt++;
            a /= i;
        }
        ma[i] = cnt;
    }
    if (a > 1)
    {
        ma[a] = 1;
    }
}

// Function to calculate all common
// divisors of two given numbers
// a, b --> input integer numbers
int commDiv(int a, int b)
{

    // Find count of each prime factor of a
    primeFactorize(a);

    // stores number of common divisors
    int res = 1;

    // Find the count of prime factors
    // of b using distinct prime factors of a
    for(auto m = ma.begin();
             m != ma.end(); m++)
    {
        int cnt = 0;
        int key = m->first;
        int value = m->second;

        while (b % key == 0)
        {
            b /= key;
            cnt++;
        }

        // Prime factor of common divisor
        // has minimum cnt of both a and b
        res *= (min(cnt, value) + 1);
    }
    return res;
}

// Driver code   
int main()
{
    int a = 12, b = 24;

    cout << commDiv(a, b) << endl;

    return 0;
}

// This code is contributed by divyeshrabadiya07
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of program
import java.util.*;
import java.io.*;

class GFG {
    // map to store the count of each prime factor of a
    static HashMap<Integer, Integer> ma = new HashMap<>();

    // method that calculate the count of
    // each prime factor of a number
    static void primeFactorize(int a)
    {
        for (int i = 2; i * i <= a; i += 2) {
            int cnt = 0;
            while (a % i == 0) {
                cnt++;
                a /= i;
            }
            ma.put(i, cnt);
        }
        if (a > 1)
            ma.put(a, 1);
    }

    // method to calculate all common divisors
    // of two given numbers
    // a, b --> input integer numbers
    static int commDiv(int a, int b)
    {
        // Find count of each prime factor of a
        primeFactorize(a);

        // stores number of common divisors
        int res = 1;

        // Find the count of prime factors of b using
        // distinct prime factors of a
        for (Map.Entry<Integer, Integer> m : ma.entrySet()) {
            int cnt = 0;

            int key = m.getKey();
            int value = m.getValue();

            while (b % key == 0) {
                b /= key;
                cnt++;
            }

            // prime factor of common divisor
            // has minimum cnt of both a and b
            res *= (Math.min(cnt, value) + 1);
        }
        return res;
    }

    // Driver method
    public static void main(String args[])
    {
        int a = 12, b = 24;
        System.out.println(commDiv(a, b));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of program
import math

# Map to store the count of each
# prime factor of a
ma = {}

# Function that calculate the count of
# each prime factor of a number
def primeFactorize(a):

    sqt = int(math.sqrt(a))
    for i in range(2, sqt, 2):
        cnt = 0

        while (a % i == 0):
            cnt += 1
            a /= i

        ma[i] = cnt

    if (a > 1):
        ma[a] = 1

# Function to calculate all common
# divisors of two given numbers
# a, b --> input integer numbers
def commDiv(a, b):

    # Find count of each prime factor of a
    primeFactorize(a)

    # stores number of common divisors
    res = 1

    # Find the count of prime factors
    # of b using distinct prime factors of a
    for key, value in ma.items():
        cnt = 0

        while (b % key == 0):
            b /= key
            cnt += 1

        # Prime factor of common divisor
        # has minimum cnt of both a and b
        res *= (min(cnt, value) + 1)

    return res

# Driver code   
a = 12
b = 24

print(commDiv(a, b))

# This code is contributed by Stream_Cipher
```

## C#

```
// C# implementation of program
using System;
using System.Collections.Generic;

class GFG{

// Map to store the count of each
// prime factor of a
static Dictionary<int,
                  int> ma = new Dictionary<int,
                                           int>();

// Function that calculate the count of
// each prime factor of a number
static void primeFactorize(int a)
{
    for(int i = 2; i * i <= a; i += 2)
    {
        int cnt = 0;
        while (a % i == 0)
        {
            cnt++;
            a /= i;
        }
        ma.Add(i, cnt);
    }

    if (a > 1)
        ma.Add(a, 1);
}

// Function to calculate all common
// divisors of two given numbers
// a, b --> input integer numbers
static int commDiv(int a, int b)
{

    // Find count of each prime factor of a
    primeFactorize(a);

    // Stores number of common divisors
    int res = 1;

    // Find the count of prime factors
    // of b using distinct prime factors of a
    foreach(KeyValuePair<int, int> m in ma)
    {
        int cnt = 0;
        int key = m.Key;
        int value = m.Value;

        while (b % key == 0)
        {
            b /= key;
            cnt++;
        }

        // Prime factor of common divisor
        // has minimum cnt of both a and b
        res *= (Math.Min(cnt, value) + 1);
    }
    return res;
}

// Driver code   
static void Main()
{
    int a = 12, b = 24;

    Console.WriteLine(commDiv(a, b));
}
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>   

    // JavaScript implementation of program

    // Map to store the count of each
    // prime factor of a
      let ma = new Map();

    // Function that calculate the count of
    // each prime factor of a number
    function primeFactorize(a)
    {
        for(let i = 2; i * i <= a; i += 2)
        {
            let cnt = 0;
            while (a % i == 0)
            {
                cnt++;
                a = parseInt(a / i, 10);
            }
            ma.set(i, cnt);
        }
        if (a > 1)
        {
            ma.set(a, 1);
        }
    }

    // Function to calculate all common
    // divisors of two given numbers
    // a, b --> input integer numbers
    function commDiv(a,b)
    {

        // Find count of each prime factor of a
        primeFactorize(a);

        // stores number of common divisors
        let res = 1;

        // Find the count of prime factors
        // of b using distinct prime factors of a
        ma.forEach((values,keys)=>{
            let cnt = 0;
            let key = keys;
            let value = values;

            while (b % key == 0)
            {
                b = parseInt(b / key, 10);
                cnt++;
            }

            // Prime factor of common divisor
            // has minimum cnt of both a and b
            res *= (Math.min(cnt, value) + 1);
        })
        return res;
    }

    // Driver code

    let a = 12, b = 24;

    document.write(commDiv(a, b));

</script>
```

**输出:**

```
6
```

**有效解–**
更好的解是计算给定两个数的[最大公约数(gcd)](https://www.geeksforgeeks.org/sum-of-all-proper-divisors-of-a-natural-number/) ，然后计算该 gcd 的除数。

## C++

```
// C++ implementation of program
#include <bits/stdc++.h>
using namespace std;

// Function to calculate gcd of two numbers
int gcd(int a, int b)
{
    if (a == 0)
        return b;
    return gcd(b % a, a);
}

// Function to calculate all common divisors
// of two given numbers
// a, b --> input integer numbers
int commDiv(int a, int b)
{
    // find gcd of a, b
    int n = gcd(a, b);

    // Count divisors of n.
    int result = 0;
    for (int i = 1; i <= sqrt(n); i++) {
        // if 'i' is factor of n
        if (n % i == 0) {
            // check if divisors are equal
            if (n / i == i)
                result += 1;
            else
                result += 2;
        }
    }
    return result;
}

// Driver program to run the case
int main()
{
    int a = 12, b = 24;
    cout << commDiv(a, b);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of program

class Test {
    // method to calculate gcd of two numbers
    static int gcd(int a, int b)
    {
        if (a == 0)
            return b;

        return gcd(b % a, a);
    }
    // method to calculate all common divisors
    // of two given numbers
    // a, b --> input integer numbers
    static int commDiv(int a, int b)
    {
        // find gcd of a, b
        int n = gcd(a, b);

        // Count divisors of n.
        int result = 0;
        for (int i = 1; i <= Math.sqrt(n); i++) {
            // if 'i' is factor of n
            if (n % i == 0) {
                // check if divisors are equal
                if (n / i == i)
                    result += 1;
                else
                    result += 2;
            }
        }
        return result;
    }

    // Driver method
    public static void main(String args[])
    {
        int a = 12, b = 24;
        System.out.println(commDiv(a, b));
    }
}
```

## 蟒蛇 3

```
# Python implementation of program
from math import sqrt

# Function to calculate gcd of two numbers
def gcd(a, b):

    if a == 0:
        return b
    return gcd(b % a, a)

# Function to calculate all common divisors
# of two given numbers
# a, b --> input integer numbers
def commDiv(a, b):

    # find GCD of a, b
    n = gcd(a, b)

    # Count divisors of n
    result = 0
    for i in range(1,int(sqrt(n))+1):

        # if i is a factor of n
        if n % i == 0:

            # check if divisors are equal
            if n/i == i:
                result += 1
            else:
                result += 2

    return result

# Driver program to run the case
if __name__ == "__main__":
    a = 12
    b = 24;
    print(commDiv(a, b))
```

## C#

```
// C# implementation of program
using System;

class GFG {

    // method to calculate gcd
    // of two numbers
    static int gcd(int a, int b)
    {
        if (a == 0)
            return b;

        return gcd(b % a, a);
    }

    // method to calculate all
    // common divisors of two
    // given numbers a, b -->
    // input integer numbers
    static int commDiv(int a, int b)
    {

        // find gcd of a, b
        int n = gcd(a, b);

        // Count divisors of n.
        int result = 0;
        for (int i = 1; i <= Math.Sqrt(n); i++) {

            // if 'i' is factor of n
            if (n % i == 0) {

                // check if divisors are equal
                if (n / i == i)
                    result += 1;
                else
                    result += 2;
            }
        }

        return result;
    }

    // Driver method
    public static void Main(String[] args)
    {

        int a = 12, b = 24;

        Console.Write(commDiv(a, b));
    }
}

// This code contributed by parashar.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of program

// Function to calculate
// gcd of two numbers
function gcd($a, $b)
{
    if ($a == 0)
        return $b;
    return gcd($b % $a, $a);
}

// Function to calculate all common
// divisors of two given numbers
// a, b --> input integer numbers
function commDiv($a, $b)
{
    // find gcd of a, b
    $n = gcd($a, $b);

    // Count divisors of n.
    $result = 0;
    for ($i = 1; $i <= sqrt($n);
                 $i++)
    {
        // if 'i' is factor of n
        if ($n % $i == 0)
        {
            // check if divisors
            // are equal
            if ($n / $i == $i)
                $result += 1;
            else
                $result += 2;
        }
    }
    return $result;
}

// Driver Code
$a = 12; $b = 24;
echo(commDiv($a, $b));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of program

    // Function to calculate gcd of two numbers
    function gcd(a, b)
    {
        if (a == 0)
            return b;
        return gcd(b % a, a);
    }

    // Function to calculate all common divisors
    // of two given numbers
    // a, b --> input integer numbers
    function commDiv(a, b)
    {
        // find gcd of a, b
        let n = gcd(a, b);

        // Count divisors of n.
        let result = 0;
        for (let i = 1; i <= Math.sqrt(n); i++) {
            // if 'i' is factor of n
            if (n % i == 0) {
                // check if divisors are equal
                if (n / i == i)
                    result += 1;
                else
                    result += 2;
            }
        }
        return result;
    }

    let a = 12, b = 24;
    document.write(commDiv(a, b));

</script>
```

**输出:**

```
6
```

时间复杂度:O(log(n)+ n <sup>1/2</sup> )，其中 n 为两个数的 gcd。

本文由 [**沙莎克·米什拉(古卢)**](https://practice.geeksforgeeks.org/user-profile.php?user=Shashank%20Mishra) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。