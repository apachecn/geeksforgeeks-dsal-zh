# N 以下两个数的倍数之和

> 原文:[https://www . geeksforgeeks . org/n 以下两个数字的倍数之和/](https://www.geeksforgeeks.org/sum-of-the-multiples-of-two-numbers-below-n/)

给定三个整数 **A** 、 **B** 和 **N** 。任务是找出 **N** 以下所有元素的和，这些元素是 **A** 或 **B** 的倍数。

**示例:**

> **输入:** N = 10，A = 3，B = 5
> **输出:** 23
> 3、5、6 和 9 是 10 以下仅有的 3 或 5 的倍数
> 
> **输入:** N = 50，A = 8，B = 15
> T3】输出: 258

**天真的方法:**

*   初始化变量**总和= 0** 。
*   从 **0** 到 **n** 循环每个 **i** 检查 **i % A = 0** 还是 **i % B = 0** 。
*   如果满足以上条件，更新 **sum = sum + i** 。
*   最后返回**总和**。

下面是上述方法的实现:

## C++

```
// C++ program to find the
// sum of all the integers
// below N which are multiples
// of either A or B
#include <iostream>
using namespace std;

// Function to return the
// sum of all the integers
// below N which are multiples
// of either A or B
int findSum(int n, int a, int b)
{
    int sum = 0;
    for (int i = 0; i < n; i++)

        // If i is a multiple of a or b
        if (i % a == 0 || i % b == 0)
            sum += i;

    return sum;
}

// Driver code
int main()
{
    int n = 10, a = 3, b = 5;
    cout << findSum(n, a, b);
    return 0;
}
```

## C

```
// C program for above approach
#include <stdio.h>

// Function to return the
// sum of all the integers
// below N which are multiples
// of either A or B
int findSum(int n, int a, int b)
{
    int sum = 0;
    for (int i = 0; i < n; i++)

        // If i is a multiple of a or b
        if (i % a == 0 || i % b == 0)
            sum += i;

    return sum;
}

// Driver Code
int main()
{
      int n = 10, a = 3, b = 5;
    printf("%d",findSum(n, a, b));
    return 0;
}

//This code is contributed by Shivshanker Singh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the
// sum of all the integers
// below N which are multiples
// of either A or B

import java.io.*;

class GFG
{

    // Function to return the
    // sum of all the integers
    // below N which are multiples
    // of either A or B
    static int findSum(int n, int a, int b)
    {
        int sum = 0;
        for (int i = 0; i < n; i++)

            // If i is a multiple of a or b
            if (i % a == 0 || i % b == 0)
                sum += i;

        return sum;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 10, a = 3, b = 5;
        System.out.println(findSum(n, a, b));
    }
}
// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python 3 program to find the sum of
# all the integers below N which are
# multiples of either A or B

# Function to return the sum of all
# the integers below N which are
# multiples of either A or B
def findSum(n, a, b):
    sum = 0
    for i in range(0, n, 1):

        # If i is a multiple of a or b
        if (i % a == 0 or i % b == 0):
            sum += i

    return sum

# Driver code
if __name__ == '__main__':
    n = 10
    a = 3
    b = 5
    print(findSum(n, a, b))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find the sum
// of all the integers
// below N which are multiples
// of either A or B
using System;

class GFG
{

    // Function to return the sum
    // of all the integers
    // below N which are multiples
    // of either A or B
    static int findSum(int n, int a, int b)
    {
        int sum = 0;
        for (int i = 0; i < n; i++)

            // If i is a multiple of a or b
            if (i % a == 0 || i % b == 0)
                sum += i;

        return sum;
    }

    // Driver code
    static void Main()
    {
        int n = 10, a = 3, b = 5;
        Console.WriteLine(findSum(n, a, b));
    }
    // This code is contributed by Ryuga
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the sum of all
// the integers below N which are
// multiples of either A or B

// Function to return the sum of all
// the integers below N which are
// multiples of either A or B
function findSum($n, $a, $b)
{
    $sum = 0;
    for ($i = 0; $i < $n; $i++)

        // If i is a multiple of a or b
        if ($i % $a == 0 || $i % $b == 0)
            $sum += $i;

    return $sum;
}

// Driver code
$n = 10;
$a = 3;
$b = 5;
echo findSum($n, $a, $b);

// This code is contributed by Sachin
?>
```

## java 描述语言

```
<script>

// Javascript program to find the sum of all
// the integers below N which are multiples
// of either A or B

// Function to return the sum of all
// the integers below N which are
// multiples of either A or B
function findSum(n, a, b)
{
    let sum = 0;
    for(let i = 0; i < n; i++)

        // If i is a multiple of a or b
        if (i % a == 0 || i % b == 0)
            sum += i;

    return sum;
}

// Driver code
let n = 10;
let a = 3;
let b = 5;

document.write( findSum(n, a, b));

// This code is contributed by mohan

</script>
```

**Output:** 

```
23
```

**时间复杂度:** O(N)

**辅助空间:** O(1)

**高效方法:**
为了更好地理解高效方法，让我们从头开始——

我们有**数= 1，2，3，4，…。，N-1，N**

所有能被 A 整除的数字**A = A，2A，3A，……..⌊N/A⌋*A**

让我们称之为， **sum1 =A + 2A + 3A+ ………..+ ⌊N/A⌋*A**

**sum1 = A(1 + 2 + 3 厖..-什么+⌊n/a)**

sum 1 = a *√n/a *(√n/a *+1)/2

其中 **⌊ ⌋** 是楼层(或最小整数)函数。

并且使用 n 个自然数的和公式 n*(n+1)/2。

类似地，可被 B 除尽的数的和–

sum 2 = b *√n/b *(√n/b *+1)/2

所以总计**和= sum1 + sum2** 但是可能有两者都通用的和数，

例如，假设 N=10，A=2，B=3

那么 sum1 = 2+4+6+8+10+12+14+16+18+20

sum2 = 3+6+9+12+15+18

我们可以清楚地看到数字 6、12、18 是重复的，所有其他数字都是 6 的倍数，这就是 **A** 和 **B** 的 LCM

设**LCM = A 和 B 的 LCM**

sum 3 = LCM *√n/LCM *(√n/LCM *+1)/2

最后，我们可以通过使用

**sum = sum 1+sum 2–sum 3**

我们可以通过以下方法计算寿命周期成本

**lcm = (A*B)/gcd**

其中 gcd = A 和 B 的 GCD

下面是上述方法的实现:

## C++

```
// C++ program to find the
// sum of all the integers
// below N which are multiples
// of either A or B
#include <bits/stdc++.h>
#include <algorithm>
using namespace std;

// Function to find sum of AP series
long long sumAP(long long n, long long d)
{
    // Number of terms
    n /= d;

    return (n) * (1 + n) * d / 2;
}

// Function to find the sum of all
// multiples of a and b below n
long long sumMultiples(long long n, long long a,
                                    long long b)
{

    // Since, we need the sum of
    // multiples less than N
    n--;
    long lcm = (a*b)/__gcd(a,b);
    return sumAP(n, a) + sumAP(n, b) -
                        sumAP(n, lcm);
}

// Driver code
int main()
{
    long long n = 10, a = 3, b = 5;

    cout << sumMultiples(n, a, b);

    return 0;
}
// This code is Modified by Shivshanker Singh.
```

## C

```
// C program to find the
// sum of all the integers
// below N which are multiples
// of either A or B
#include <stdio.h>

// Function to find sum of AP series
long long sumAP(long long n, long long d)
{
    // Number of terms
    n /= d;

    return (n) * (1 + n) * d / 2;
}

// Function to find the gcd of A and B.
long gcd(int p, int q)
{
    if (p == 0)
        return q;
    return gcd(q % p, p);
}

// Function to find the sum of all
// multiples of a and b below n
long long sumMultiples(long long n, long long a,
                                   long long b)
{
    // Since, we need the sum of
    // multiples less than N
    n--;
    long lcm = (a*b)/gcd(a,b);
    return sumAP(n, a) + sumAP(n, b) - sumAP(n, lcm);
}

// Driver code
int main()
{
    long long n = 10, a = 3, b = 5;

    printf("%lld", sumMultiples(n, a, b));

    return 0;
}
// This code is Contributed by Shivshanker Singh.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java  program to find the
// sum of all the integers
// below N which are multiples
// of either A or B
import java.io.*;

class GFG
{

    // Function to find sum of AP series
    static long sumAP(long n, long d)
    {
        // Number of terms
        n = (int)n / d;

        return (n) * (1 + n) * d / 2;
    }

    // Function to find gcd of A and B
    public static long gcd(long p, long q)
    {
        if (p == 0)
            return q;
        return gcd(q % p, p);
    }

    // Function to find the sum of all
    // multiples of a and b below n
    static long sumMultiples(long n, long a,
                                     long b)
    {

        // Since, we need the sum of
        // multiples less than N
        n--;
        long lcm = (a * b) / gcd(a, b);
        return sumAP(n, a) + sumAP(n, b) -
                              sumAP(n, lcm);
    }

    // Driver code
    public static void main(String[] args)
    {

        long n = 10, a = 3, b = 5;

        System.out.println(sumMultiples(n, a, b));
    }
    // This code is Modified by Shivshanker Singh.
}
```

## 蟒蛇 3

```
import math
# Python3 program to find the sum of
# all the integers below N which are
# multiples of either A or B

# Function to find sum of AP series
def sumAP(n, d):

    # Number of terms
    n = n//d

    return (n) * (1 + n) * d // 2

# Function to find the sum of all
# multiples of a and b below n
def sumMultiples(n, a, b):

    # Since, we need the sum of
    # multiples less than N
    n = n-1
    lcm = (a*b)//math.gcd(a, b)
    return sumAP(n, a) + sumAP(n, b) - \
                         sumAP(n, lcm)

# Driver code
n = 10
a = 3
b = 5
print(sumMultiples(n, a, b))

# This code is Modified by Shivshanker Singh.
```

## C#

```
// C#  program to find the
// sum of all the integers
// below N which are multiples
// of either A or B
using System;

public class GFG
{

    // Function to find sum of AP series
    static long sumAP(long n, long d)
    {
        // Number of terms
        n = (int)n / d;

        return (n) * (1 + n) * d / 2;
    }

    // Function to find gcd of A and B
    static long gcd(long p, long q)
    {
        if (p == 0)
            return q;
        return gcd(q % p, p);
    }

    // Function to find the sum of all
    // multiples of a and b below n
    static long sumMultiples(long n, long a,
                                     long b)
    {

        // Since, we need the sum of
        // multiples less than N
        n--;
        long lcm = (a * b) / gcd(a, b);
        return sumAP(n, a) + sumAP(n, b) -
                             sumAP(n, lcm);
    }

    // Driver code
    static public void Main()
    {

        long n = 10, a = 3, b = 5;

        Console.WriteLine(sumMultiples(n, a, b));
    }
    // This code is Modified by Shivshanker Singh.
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the
// sum of all the integers
// below N which are multiples
// of either A or B
// Function to find sum of AP series
function sumAP( $n, $d)
{
    // Number of terms
    $n = (int)($n / $d);

    return ($n) * (1 + $n) * $d / 2;
}

// Function to find the sum of all
// multiples of a and b below n
function sumMultiples( $n, $a, $b)
{
    // Since, we need the sum of
    // multiples less than N
    $n--;

    return sumAP($n, $a) + sumAP($n, $b) -
                       sumAP($n, $a * $b);
}

// Driver code
{
    $n = 10;
    $a = 3;
    $b = 5;

    echo(sumMultiples($n, $a, $b));

    return 0;
}
//This code is contributed by Shivshanker Singh
```

## java 描述语言

```
<script>

// Javascript program to find the
// sum of all the integers
// below N which are multiples
// of either A or B

// Function to find sum of AP series
function sumAP(n, d)
{

    // Number of terms
    n = parseInt(n / d);

    return (n) * (1 + n) * d / 2;
}

// Function to find gcd of A and B
function gcd(p, q)
{
    if (p == 0)
        return q;

    return gcd(q % p, p);
}

// Function to find the sum of all
// multiples of a and b below n
function sumMultiples(n, a, b)
{

    // Since, we need the sum of
    // multiples less than N
    n--;
    var lcm = (a * b) / gcd(a, b);
    return sumAP(n, a) + sumAP(n, b) -
           sumAP(n, lcm);
}

// Driver code
{
    let n = 10;
    let a = 3;
    let b = 5;

    document.write(sumMultiples(n, a, b));
}

// This code is contributed by mohan

</script>
```

**Output:** 

```
23
```

**时间复杂度:** O(log(N))

**辅助空间:** O(1)