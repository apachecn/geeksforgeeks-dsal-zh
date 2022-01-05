# n 中素数‘r’的幂！

> 原文:[https://www . geesforgeks . org/质数幂-r-in-n/](https://www.geeksforgeeks.org/power-of-a-prime-number-r-in-n/)

给定一个整数 n，求 n 中给定素数(r)的幂！
**例:**

```
Input  : n = 6  r = 3
         Factorial of 6 is 720 = 2^4 * 3^2 *5 (prime factor 2,3,5)
         and power of 3 is 2 
Output : 2

Input  : n = 2000 r = 7
Output : 330
```

一个简单的方法是，首先计算 n 的阶乘，然后对其进行因子分解，求出一个素数的幂。
由于一个数的阶乘是一个大数，上述方法会导致稍大的数溢出。这个想法是考虑一个因子 n 的素因子
[**n 的勒让德因子分解！**](https://www.geeksforgeeks.org/given-p-and-n-find-the-largest-x-such-that-px-divides-n-2/)
对于任意素数 p 和任意整数 n，让 **Vp(n)** 为 p 除以 n 的最大幂的指数(即 n 的 p-adic 估值)。然后
VP(n)= floor(n/p^i)和 I 的和从 1 到无穷大
而右边的公式是一个无穷大的和，对于 n 和 p 的任何特定值，它只有有限多个非零项:对于每个足够大的 I，p^i > n，一个有 floor(n/p^i) = 0。因为，和是收敛的。

```
Power of ‘r’ in n! = floor(n/r) + floor(n/r^2) + floor(n/r^3) + ....
```

计算 n 中一个数字 r 的幂的程序！基于以上公式。

## C++

```
// C++ program to find power of
// a prime number ‘r’ in n!
#include <bits/stdc++.h>
using  namespace std;

// Function to return power of a
// no. 'r' in factorial of n
int power(int n, int r)
{          
    // Keep dividing n by powers of
    // 'r' and update count
    int count = 0;
    for (int i = r; (n / i) >= 1; i = i * r)   
        count += n / i;
    return count;
}

// Driver program to
// test above function
int main()
{
    int n = 6,  r = 3;  
    printf(" %d ", power(n, r));   
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find power of
// a prime number 'r' in n!

class GFG {

// Function to return power of a
// no. 'r' in factorial of n
static int power(int n, int r) {

    // Keep dividing n by powers of
    // 'r' and update count
    int count = 0;
    for (int i = r; (n / i) >= 1; i = i * r)
    count += n / i;
    return count;
}

// Driver code
public static void main(String[] args)
{
    int n = 6, r = 3;
    System.out.print(power(n, r));
}
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to find power
# of a prime number ‘r’ in n!

# Function to return power of a
# no. 'r' in factorial of n
def power(n, r):

    # Keep dividing n by powers of
    # 'r' and update count
    count = 0; i = r

    while((n / i) >= 1):
        count += n / i
        i = i * r

    return int(count)

# Driver Code
n = 6; r = 3
print(power(n, r))

# This code is contributed by Smitha Dinesh Semwal.
```

## C#

```
// C# program to find power of
// a prime number 'r' in n!
using System;

class GFG {

// Function to return power of a
// no. 'r' in factorial of n
static int power(int n, int r) {

    // Keep dividing n by powers of
    // 'r' and update count
    int count = 0;
    for (int i = r; (n / i) >= 1; i = i * r)
    count += n / i;
    return count;
}

// Driver code
public static void Main()
{
    int n = 6, r = 3;
    Console.WriteLine(power(n, r));
}
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
//PHP program to find power of
// a prime number ‘r’ in n!

// Function to return power of a
// no. 'r' in factorial of n
function power($n, $r)
{        

    // Keep dividing n by powers 
    // of 'r' and update count
    $count = 0;
    for ($i = $r; ($n / $i) >= 1;
                   $i = $i * $r)
        $count += $n / $i;
    return $count;
}

    // Driver Code
    $n = 6; $r = 3;
    echo power($n, $r);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// JavaScript program to find power of
// a prime number 'r' in n!

// Function to return power of a
// no. 'r' in factorial of n
function power(n, r) {

    // Keep dividing n by powers of
    // 'r' and update count
    let count = 0;
    for (let i = r; (n / i) >= 1; i = i * r)
    count += n / i;
    return count;
}

// Driver code

    let n = 6, r = 3;
    document.write(power(n, r));

// This code is contributed by souravghosh0416.
</script>
```

**输出:**

```
2
```