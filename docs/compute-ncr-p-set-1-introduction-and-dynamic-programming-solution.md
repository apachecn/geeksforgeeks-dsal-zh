# 计算 nCr % p |集合 1(介绍和动态规划解决方案)

> 原文:[https://www . geesforgeks . org/compute-NCR-p-set-1-introduction-and-dynamic-programming-solution/](https://www.geeksforgeeks.org/compute-ncr-p-set-1-introduction-and-dynamic-programming-solution/)

给定三个数字 n、r 和 p，计算<sup>n</sup>C<sub>r</sub>mod p
T5】的值示例:

```
Input:  n = 10, r = 2, p = 13
Output: 6
Explanation: 10C2 is 45 and 45 % 13 is 6.
```

## [我们强烈建议您点击此处进行练习，然后再进入解决方案。](https://practice.geeksforgeeks.org/problems/ncr1019/1)

#### <u>方法 1:(使用动态规划)</u>

一个**简单的解决方案**是先计算 <sup>n</sup> C <sub>r</sub> ，然后计算 <sup>n</sup> C <sub>r</sub> % p，当 <sup>n</sup> C <sub>r</sub> 的值较小时，这个解决方案工作正常。
**nC<sub>r</sub>值大怎么办？**
当 <sup>n</sup> C <sub>r</sub> 无法拟合一个变量，导致溢出时，n 的大值一般需要 <sup>n</sup> C <sub>r</sub> %p 的值。因此，计算 <sup>n</sup> C <sub>r</sub> 然后使用模块化运算符并不是一个好主意，因为即使对于稍大的 n 和 r 值也会有溢出，例如这里讨论的方法和这里讨论的方法会导致 n = 50 和 r = 40 的溢出。
想法是使用以下公式计算 <sup>n</sup> C <sub>r</sub>

```
   C(n, r) = C(n-1, r-1) + C(n-1, r)
   C(n, 0) = C(n, n) = 1
```

**上式和帕斯卡三角形的工作原理:**
让我们看看上式如何适用于 C(4，3)
1 = = = = = = = = = = =>>n = 0，C(0，0) = 1
1–1 = = = = = = = = = = =>>n = 1，C(1，0)= 1，C(1，1)= 1
1–2–1 = = = = = = =>>n = 2，C(2，0) 2) = 3，C(3，3)= 1
1–4–6–4–1 = =>>n = 4，C(4，0) = 1，C(4，1) = 4，C(4，2) = 6，C(4，3)=4，C(4，4)=1
所以这里 I 上的每个循环，构建第 I 行帕斯卡三角形，使用上述公式的(i-1)行
**扩展进行模运算:**

```
   C(n, r)%p = [ C(n-1, r-1)%p + C(n-1, r)%p ] % p
   C(n, 0) = C(n, n) = 1
```

上面的公式可以使用 2D 阵列的动态编程来实现。
通过一次构造一行，可以进一步优化基于 2D 阵列的动态规划解决方案。有关详细信息，请参见下面帖子中的空间优化版本。
[使用动态规划的二项式系数](https://www.geeksforgeeks.org/dynamic-programming-set-9-binomial-coefficient/)
以下是基于上文中讨论的空间优化版本的实现。

## C++

```
// A Dynamic Programming based solution to compute nCr % p
#include <bits/stdc++.h>
using namespace std;

// Returns nCr % p
int nCrModp(int n, int r, int p)
{
    // Optimization for the cases when r is large
    if (r > n - r)
        r = n - r;

    // The array C is going to store last row of
    // pascal triangle at the end. And last entry
    // of last row is nCr
    int C[r + 1];
    memset(C, 0, sizeof(C));

    C[0] = 1; // Top row of Pascal Triangle

    // One by constructs remaining rows of Pascal
    // Triangle from top to bottom
    for (int i = 1; i <= n; i++) {

        // Fill entries of current row using previous
        // row values
        for (int j = min(i, r); j > 0; j--)

            // nCj = (n-1)Cj + (n-1)C(j-1);
            C[j] = (C[j] + C[j - 1]) % p;
    }
    return C[r];
}

// Driver program
int main()
{
    int n = 10, r = 2, p = 13;
    cout << "Value of nCr % p is " << nCrModp(n, r, p);
    return 0;
}
```

## Java 语言（一种计算机语言，尤用于创建网站）

```
// A Dynamic Programming based
// solution to compute nCr % p
import java.io.*;
import java.util.*;
import java.math.*;

class GFG {

    // Returns nCr % p
    static int nCrModp(int n, int r, int p)
    {
        if (r > n - r)
            r = n - r;

        // The array C is going to store last
        // row of pascal triangle at the end.
        // And last entry of last row is nCr
        int C[] = new int[r + 1];

        C[0] = 1; // Top row of Pascal Triangle

        // One by constructs remaining rows of Pascal
        // Triangle from top to bottom
        for (int i = 1; i <= n; i++) {

            // Fill entries of current row using previous
            // row values
            for (int j = Math.min(i, r); j > 0; j--)

                // nCj = (n-1)Cj + (n-1)C(j-1);
                C[j] = (C[j] + C[j - 1]) % p;
        }
        return C[r];
    }

    // Driver program
    public static void main(String args[])
    {
        int n = 10, r = 2, p = 13;
        System.out.println("Value of nCr % p is "
                           + nCrModp(n, r, p));
    }
}

// This code is contributed by Nikita Tiwari.
```

## 蟒蛇 3

```
# A Dynamic Programming based solution to compute nCr % p

# Returns nCr % p
def nCrModp(n, r, p):

    # Optimization for the cases when r is large
    # compared to n-r
    if (r > n- r):
        r = n - r 

    # The array C is going to store last row of
    # pascal triangle at the end. And last entry
    # of last row is nCr.
    C = [0 for i in range(r + 1)]

    C[0] = 1 # Top row of Pascal Triangle

    # One by constructs remaining rows of Pascal
    # Triangle from top to bottom
    for i in range(1, n + 1):

        # Fill entries of current row
        # using previous row values
        for j in range(min(i, r), 0, -1):

            # nCj = (n - 1)Cj + (n - 1)C(j - 1)
            C[j] = (C[j] + C[j-1]) % p

    return C[r]

# Driver Program
n = 10
r = 2
p = 13
print('Value of nCr % p is', nCrModp(n, r, p))

# This code is contributed by Soumen Ghosh
```

## C#

```
// A Dynamic Programming based
// solution to compute nCr % p
using System;

class GFG {

    // Returns nCr % p
    static int nCrModp(int n, int r, int p)
    {

        // Optimization for the cases when r is large
        if (r > n - r)
            r = n - r;

        // The array C is going to store last
        // row of pascal triangle at the end.
        // And last entry of last row is nCr
        int[] C = new int[r + 1];

        for (int i = 0; i < r + 1; i++)
            C[i] = 0;

        C[0] = 1; // Top row of Pascal Triangle

        // One by constructs remaining rows
        // of Pascal Triangle from top to bottom
        for (int i = 1; i <= n; i++) {

            // Fill entries of current row using
            // previous row values
            for (int j = Math.Min(i, r); j > 0; j--)

                // nCj = (n-1)Cj + (n-1)C(j-1);
                C[j] = (C[j] + C[j - 1]) % p;
        }

        return C[r];
    }

    // Driver program
    public static void Main()
    {
        int n = 10, r = 2, p = 13;

        Console.Write("Value of nCr % p is "
                      + nCrModp(n, r, p));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A Dynamic Programming based
// solution to compute nCr % p

// Returns nCr % p
function nCrModp($n, $r, $p)
{

// Optimization for the cases when r is large
if ($r > $n - $r)
    $r = $n - $r;

// The array C is going
// to store last row of
// pascal triangle at
// the end. And last entry
// of last row is nCr
$C = array();

for( $i = 0; $i < $r + 1; $i++)
    $C[$i] = 0;

// Top row of Pascal
// Triangle
$C[0] = 1;

// One by constructs remaining
// rows of Pascal Triangle from
// top to bottom
for ($i = 1; $i <= $n; $i++)
{

    // Fill entries of current
    // row using previous row values
    for ($j = Min($i, $r); $j > 0; $j--)

        // nCj = (n-1)Cj + (n-1)C(j-1);
        $C[$j] = ($C[$j] +
                  $C[$j - 1]) % $p;
}

return $C[$r];
}

// Driver Code
$n = 10; $r = 2;$p = 13;

echo "Value of nCr % p is ",
         nCrModp($n, $r, $p);

// This code is contributed
// by anuj_67.
?>
```

## java 描述语言

```
<script>
// A Dynamic Programming based
// solution to compute nCr % p

// Returns nCr % p
function nCrModp(n,r,p)
{
    if (r > n - r)
            r = n - r;

        // The array C is going to store last
        // row of pascal triangle at the end.
        // And last entry of last row is nCr
        let C = new Array(r + 1);
         for(let i = 0; i < r + 1; i++)
            C[i] = 0;
        C[0] = 1; // Top row of Pascal Triangle

        // One by constructs remaining rows of Pascal
        // Triangle from top to bottom
        for (let i = 1; i <= n; i++) {

            // Fill entries of current row using previous
            // row values
            for (let j = Math.min(i, r); j > 0; j--)

                // nCj = (n-1)Cj + (n-1)C(j-1);
                C[j] = (C[j] + C[j - 1]) % p;
        }
        return C[r];
}

// Driver program
let n = 10, r = 2, p = 13;
document.write("Value of nCr % p is "
                   + nCrModp(n, r, p));

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output**

```
Value of nCr % p is 6
```

上述解的时间复杂度为 O(n*r)，需要 O(r)空间。以上问题有更多更好的解决方案。
[Compute nCr % p | Set 2 (Lucas 定理)](https://www.geeksforgeeks.org/compute-ncr-p-set-2-lucas-theorem/)
如果发现有不正确的地方，请写评论，或者想分享更多关于上述话题的信息。

#### <u>方法 2(使用帕斯卡三角形和动态专业版)</u>

另一种方法是利用帕斯卡三角形的概念。该方法不是从 n=0 到 n=n 开始为每 n 计算<sup>n</sup>C<sub>r</sub><sup>T5】值，而是旨在使用第 n 行本身进行计算。该方法通过找出 <sup>n</sup> C <sub>r</sub> 和 <sup>n</sup> C <sub>r-1</sub> 之间的一般关系来进行。</sup>

```
***FORMULA: C(n,r)=C(n,r-1)* (n-r+1)/r***

Example:

For instance, take n=5 and r=3.

Input:  n = 5, r = 3, p = 1000000007
Output: 6
Explanation: 5C3 is 10 and 10 % 100000007 is 10.

As per the formula,
C(5,3)=5!/(3!)*(2!)
C(5,3)=10

Also,
C(5,2)=5!/(2!)*(3!)
C(5,2)=10

Let's try applying the above formula.

C(n,r)=C(n,r-1)* (n-r+1)/r
C(5,3)=C(5,2)*(5-3+1)/3
C(5,3)=C(5,2)*1
C(5,3)=10*1
```

上面的例子表明，C(n，r)可以通过计算 C(n，r-1)并将结果与项(n-r+1)/r 相乘来轻松计算。但是，对于大的 n 值，这种乘法可能会导致整数溢出。为了解决这种情况，请使用模乘法和模除法概念，以便在整数溢出方面实现优化。

**我们来看看如何为同一个三角形建立帕斯卡三角。**

![{1}\\ {1\hspace{0.1cm} 1}\\ {1\hspace{0.1cm} 2\hspace{0.1cm} 1}\\ {1\hspace{0.1cm} 3\hspace{0.1cm} 3\hspace{0.1cm} 1}\\ {1 \hspace{0.1cm}4\hspace{0.1cm} 6\hspace{0.1cm} 4\hspace{0.1cm} 1}\\ {1\hspace{0.1cm} 5\hspace{0.1cm} 10\hspace{0.1cm} 10\hspace{0.1cm} 5\hspace{0.1cm} 1}](img/0d45d01e284b456bd45c5a55b475b4ba.png "Rendered by QuickLaTeX.com")

通过仅声明一个变量来执行计算，可以进一步优化 1D 数组声明。然而，对于最终实现，整数溢出也需要其他函数。

下面的帖子提到了二进制系数计算的**空间和时间优化的**实现。

## C++

```
// C++ program to find the nCr%p
// based on optimal Dynamic
// Programming implementation and
// Pascal Triangle concepts
#include <bits/stdc++.h>
using namespace std;

// Returns (a * b) % mod
long long moduloMultiplication(long long a, long long b,
                               long long mod)
{

    // Initialize result
    long long res = 0;

    // Update a if it is more than
    // or equal to mod
    a %= mod;

    while (b) {

        // If b is odd, add a with result
        if (b & 1)
            res = (res + a) % mod;

        // Here we assume that doing 2*a
        // doesn't cause overflow
        a = (2 * a) % mod;
        b >>= 1; // b = b / 2
    }
    return res;
}

// C++ function for extended Euclidean Algorithm
long long int gcdExtended(long long int a, long long int b,
                          long long int* x,
                          long long int* y);

// Function to find modulo inverse of b. It returns
// -1 when inverse doesn't exists
long long int modInverse(long long int b, long long int m)
{

    long long int x, y; // used in extended GCD algorithm
    long long int g = gcdExtended(b, m, &x, &y);

    // Return -1 if b and m are not co-prime
    if (g != 1)
        return -1;

    // m is added to handle negative x
    return (x % m + m) % m;
}

// C function for extended Euclidean Algorithm (used to
// find modular inverse.
long long int gcdExtended(long long int a, long long int b,
                          long long int* x,
                          long long int* y)
{

    // Base Case
    if (a == 0) {
        *x = 0, *y = 1;
        return b;
    }

    // To store results of recursive call
    long long int x1, y1;

    long long int gcd = gcdExtended(b % a, a, &x1, &y1);

    // Update x and y using results of recursive
    // call
    *x = y1 - (b / a) * x1;
    *y = x1;
    return gcd;
}

// Function to compute a/b under modlo m
long long int modDivide(long long int a, long long int b,
                        long long int m)
{

    a = a % m;
    long long int inv = modInverse(b, m);
    if (inv == -1)
        // cout << "Division not defined";
        return 0;
    else
        return (inv * a) % m;
}

// Function to calculate nCr % p
int nCr(int n, int r, int p)
{

    // Edge Case which is not possible
    if (r > n)
        return 0;

    // Optimization for the cases when r is large
    if (r > n - r)
        r = n - r;

    // x stores the current result at
    long long int x = 1;

    // each iteration
    // Initialized to 1 as nC0 is always 1.
    for (int i = 1; i <= r; i++) {

        // Formula derived for calculating result is
        // C(n,r-1)*(n-r+1)/r
        // Function calculates x*(n-i+1) % p.
        x = moduloMultiplication(x, (n + 1 - i), p);

        // Function calculates x/i % p.
        x = modDivide(x, i, p);
    }
    return x;
}

// Driver Code
int main()
{

    long long int n = 5, r = 3, p = 1000000007;
    cout << "Value of nCr % p is " << nCr(n, r, p);
    return 0;
}
```

**Output**

```
Value of nCr % p is 10
```

#### **复杂度分析:**

*   上面的代码需要额外的 0(1)空间进行计算。
*   计算 nCr % p 所涉及的时间约为 O(n)。

本文由 [**雅利安古普塔**](https://auth.geeksforgeeks.org/user/aryangupta18/profile) 改进而来。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。