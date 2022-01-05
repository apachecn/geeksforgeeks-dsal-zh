# 求第 n 项(矩阵求幂示例)

> 原文:[https://www . geeksforgeeks . org/find-n-term-a-matrix-求幂-示例/](https://www.geeksforgeeks.org/find-nth-term-a-matrix-exponentiation-example/)

给我们一个递归函数，它以其他项的形式描述第 n 个项。在本文中，我们举了一些具体的例子。
![T_{n} = 2*T_{n-1}+3*T{n-2} \\ Given, T_0=1 T_1=1  ](img/f80ad2f890cd5318f3c941247de2650e.png "Rendered by QuickLaTeX.com")
现在给你 n，你要用上面的公式找出第 n 项。

**示例:**

```
Input : n = 2
Output : 5

Input : n = 3
Output :13 
```

先决条件:
**基本方法:**这个问题可以通过简单地迭代 n 个项来解决。每次你找到一个术语，用这个术语找到下一个术语，以此类推。但是这个问题的时间复杂度是 O(n)级。

**优化方法**
所有这样的问题，其中一个项是其他项的线性函数。那么这些就可以用矩阵求解了(请参考:[矩阵求幂](https://www.geeksforgeeks.org/matrix-exponentiation/))。首先，我们制作一个变换矩阵，然后只使用矩阵幂运算来找到第 n 项。

**分步法包括:**

**第一步。确定 T(i)所依赖的项数。**
举个例子，T(i)取决于两个术语。所以，k = 2

**第二步。确定初始值**
如本文中给出的 T0=1，T1=1。

**第三步。确定 TM，即变换矩阵。**
这是解决递归关系最重要的一步。在这一步中，我们必须使维度 k*k.
的矩阵使得
T(i)=TM*(初始值向量)

这里**初始值向量**是包含初始值的向量。我们把这个向量命名为**首字母**。
![$ So, Initial Vector=\left[ \begin{array}{c} T_1 & T_0\\ \end{array} \right] $ Now find Transformation matrix. $TM=\left[ \begin{array}{cc} 2 & 3\\ 1 & 0 \\ \end{array} \right]$ Now, First row of T2 give us 2nd term. $T_2=\left[ \begin{array}{cc} 2 & 3\\ 1 & 0 \\ \end{array} \right]*\left[ \begin{array}{c} T_1 & T_0\\ \end{array} \right]$ So, general term will be, First row of Tn. $T_n=\left[ \begin{array}{cc} 2 & 3\\ 1 & 0 \\ \end{array} \right]^{n-1}*\left[ \begin{array}{c} T_1 & T_0\\ \end{array} \right]$ So, finally we have Tn=$TM^{n-1}*Intial Vector$ And this power of matrix can be calculated using matrix exponenciation in O(logn).  ](img/5280eb2a8618e7f2ce6c465593247a41.png "Rendered by QuickLaTeX.com")

下面是实现上述方法的程序。

## C++

```
// CPP program to find n-th term of a recursive
// function using matrix exponentiation.
#include <bits/stdc++.h>
using namespace std;
#define MOD 1000000009

#define ll long long int

ll power(ll n)
{
    if (n <= 1)
        return 1;

    // This power function returns first row of
    // {Transformation Matrix}^n-1*Initial Vector
    n--;

    // This is an identity matrix.
    ll res[2][2] = { 1, 0, 0, 1 };

    // this is Transformation matrix.
    ll tMat[2][2] = { 2, 3, 1, 0 };

    // Matrix exponentiation to calculate power of {tMat}^n-1
    // store res in "res" matrix.
    while (n) {

        if (n & 1) {
            ll tmp[2][2];
            tmp[0][0] = (res[0][0] * tMat[0][0] + res[0][1] * tMat[1][0]) % MOD;
            tmp[0][1] = (res[0][0] * tMat[0][1] + res[0][1] * tMat[1][1]) % MOD;
            tmp[1][0] = (res[1][0] * tMat[0][0] + res[1][1] * tMat[1][0]) % MOD;
            tmp[1][1] = (res[1][0] * tMat[0][1] + res[1][1] * tMat[1][1]) % MOD;
            res[0][0] = tmp[0][0];
            res[0][1] = tmp[0][1];
            res[1][0] = tmp[1][0];
            res[1][1] = tmp[1][1];
        }
        n = n / 2;
        ll tmp[2][2];
        tmp[0][0] = (tMat[0][0] * tMat[0][0] + tMat[0][1] * tMat[1][0]) % MOD;
        tmp[0][1] = (tMat[0][0] * tMat[0][1] + tMat[0][1] * tMat[1][1]) % MOD;
        tmp[1][0] = (tMat[1][0] * tMat[0][0] + tMat[1][1] * tMat[1][0]) % MOD;
        tmp[1][1] = (tMat[1][0] * tMat[0][1] + tMat[1][1] * tMat[1][1]) % MOD;
        tMat[0][0] = tmp[0][0];
        tMat[0][1] = tmp[0][1];
        tMat[1][0] = tmp[1][0];
        tMat[1][1] = tmp[1][1];
    }

    // res store {Transformation matrix}^n-1
    // hence will be first row of res*Initial Vector.
    return (res[0][0] * 1 + res[0][1] * 1) % MOD;
}

// Driver code
int main()
{
    ll n = 3;
    cout << power(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find n-th term of a recursive
// function using matrix exponentiation.
class GfG {

    static int MAX = 100;
    static int MOD = 1000000009;
    static int power(int n)
    {
        if (n <= 1) {
            return 1;
        }

        // This power function returns first row of
        // {Transformation Matrix}^n-1*Initial Vector
        n--;

        // This is an identity matrix.
        int res[][] = { { 1, 0 }, { 0, 1 } };

        // this is Transformation matrix.
        int tMat[][] = { { 2, 3 }, { 1, 0 } };

        // Matrix exponentiation to calculate power of {tMat}^n-1
        // store res in "res" matrix.
        while (n > 0) {

            if (n % 2 == 1) {
                int tmp[][] = new int[2][2];
                tmp[0][0] = (res[0][0] * tMat[0][0]
                             + res[0][1] * tMat[1][0])
                            % MOD;
                tmp[0][1] = (res[0][0] * tMat[0][1]
                             + res[0][1] * tMat[1][1])
                            % MOD;
                tmp[1][0] = (res[1][0] * tMat[0][0]
                             + res[1][1] * tMat[1][0])
                            % MOD;
                tmp[1][1] = (res[1][0] * tMat[0][1]
                             + res[1][1] * tMat[1][1])
                            % MOD;
                res[0][0] = tmp[0][0];
                res[0][1] = tmp[0][1];
                res[1][0] = tmp[1][0];
                res[1][1] = tmp[1][1];
            }

            n = n / 2;
            int tmp[][] = new int[2][2];
            tmp[0][0] = (tMat[0][0] * tMat[0][0]
                         + tMat[0][1] * tMat[1][0])
                        % MOD;
            tmp[0][1] = (tMat[0][0] * tMat[0][1]
                         + tMat[0][1] * tMat[1][1])
                        % MOD;
            tmp[1][0] = (tMat[1][0] * tMat[0][0]
                         + tMat[1][1] * tMat[1][0])
                        % MOD;
            tmp[1][1] = (tMat[1][0] * tMat[0][1]
                         + tMat[1][1] * tMat[1][1])
                        % MOD;
            tMat[0][0] = tmp[0][0];
            tMat[0][1] = tmp[0][1];
            tMat[1][0] = tmp[1][0];
            tMat[1][1] = tmp[1][1];
        }

        // res store {Transformation matrix}^n-1
        // hence wiint be first row of res*Initial Vector.
        return (res[0][0] * 1 + res[0][1] * 1) % MOD;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 3;
        System.out.println(power(n));
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to find n-th term of a recursive
# function using matrix exponentiation.
MOD = 1000000009;

def power(n):
    if (n <= 1):
        return 1;

    # This power function returns first row of
    # {Transformation Matrix}^n-1 * Initial Vector
    n-= 1;

    # This is an identity matrix.
    res = [[1, 0], [0, 1]];

    # this is Transformation matrix.
    tMat = [[2, 3], [1, 0]];

    # Matrix exponentiation to calculate
    # power of {tMat}^n-1 store res in "res" matrix.
    while (n):
        if (n & 1):
            tmp = [[0 for x in range(2)] for y in range(2)];
            tmp[0][0] = (res[0][0] * tMat[0][0] +
                        res[0][1] * tMat[1][0]) % MOD;
            tmp[0][1] = (res[0][0] * tMat[0][1] +
                        res[0][1] * tMat[1][1]) % MOD;
            tmp[1][0] = (res[1][0] * tMat[0][0] +
                        res[1][1] * tMat[1][0]) % MOD;
            tmp[1][1] = (res[1][0] * tMat[0][1] +
                        res[1][1] * tMat[1][1]) % MOD;
            res[0][0] = tmp[0][0];
            res[0][1] = tmp[0][1];
            res[1][0] = tmp[1][0];
            res[1][1] = tmp[1][1];

        n = n // 2;
        tmp = [[0 for x in range(2)] for y in range(2)];
        tmp[0][0] = (tMat[0][0] * tMat[0][0] +
                    tMat[0][1] * tMat[1][0]) % MOD;
        tmp[0][1] = (tMat[0][0] * tMat[0][1] +
                    tMat[0][1] * tMat[1][1]) % MOD;
        tmp[1][0] = (tMat[1][0] * tMat[0][0] +
                    tMat[1][1] * tMat[1][0]) % MOD;
        tmp[1][1] = (tMat[1][0] * tMat[0][1] +
                    tMat[1][1] * tMat[1][1]) % MOD;
        tMat[0][0] = tmp[0][0];
        tMat[0][1] = tmp[0][1];
        tMat[1][0] = tmp[1][0];
        tMat[1][1] = tmp[1][1];

    # res store {Transformation matrix}^n-1
    # hence will be first row of res * Initial Vector.
    return (res[0][0] * 1 + res[0][1] * 1) % MOD;

# Driver code
n = 3;
print(power(n));

# This code is contributed by mits
```

## C#

```
// C# program to find n-th term of a recursive
// function using matrix exponentiation.
using System;

class GfG {

    // static int MAX = 100;
    static int MOD = 1000000009;
    static int power(int n)
    {
        if (n <= 1) {
            return 1;
        }

        // This power function returns first row of
        // {Transformation Matrix}^n-1*Initial Vector
        n--;

        // This is an identity matrix.
        int[, ] res = { { 1, 0 }, { 0, 1 } };

        // this is Transformation matrix.
        int[, ] tMat = { { 2, 3 }, { 1, 0 } };

        // Matrix exponentiation to calculate power of {tMat}^n-1
        // store res in "res" matrix.
        while (n > 0) {

            if (n % 2 == 1) {
                int[, ] tmp = new int[2, 2];
                tmp[0, 0] = (res[0, 0] * tMat[0, 0]
                             + res[0, 1] * tMat[1, 0])
                            % MOD;
                tmp[0, 1] = (res[0, 0] * tMat[0, 1]
                             + res[0, 1] * tMat[1, 1])
                            % MOD;
                tmp[1, 0] = (res[1, 0] * tMat[0, 0]
                             + res[1, 1] * tMat[1, 0])
                            % MOD;
                tmp[1, 1] = (res[1, 0] * tMat[0, 1]
                             + res[1, 1] * tMat[1, 1])
                            % MOD;
                res[0, 0] = tmp[0, 0];
                res[0, 1] = tmp[0, 1];
                res[1, 0] = tmp[1, 0];
                res[1, 1] = tmp[1, 1];
            }

            n = n / 2;
            int[, ] tmp1 = new int[2, 2];
            tmp1[0, 0] = (tMat[0, 0] * tMat[0, 0]
                          + tMat[0, 1] * tMat[1, 0])
                         % MOD;
            tmp1[0, 1] = (tMat[0, 0] * tMat[0, 1]
                          + tMat[0, 1] * tMat[1, 1])
                         % MOD;
            tmp1[1, 0] = (tMat[1, 0] * tMat[0, 0]
                          + tMat[1, 1] * tMat[1, 0])
                         % MOD;
            tmp1[1, 1] = (tMat[1, 0] * tMat[0, 1]
                          + tMat[1, 1] * tMat[1, 1])
                         % MOD;
            tMat[0, 0] = tmp1[0, 0];
            tMat[0, 1] = tmp1[0, 1];
            tMat[1, 0] = tmp1[1, 0];
            tMat[1, 1] = tmp1[1, 1];
        }

        // res store {Transformation matrix}^n-1
        // hence wiint be first row of res*Initial Vector.
        return (res[0, 0] * 1 + res[0, 1] * 1) % MOD;
    }

    // Driver code
    public static void Main()
    {
        int n = 3;
        Console.WriteLine(power(n));
    }
}

// This code contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find n-th term of a recursive
// function using matrix exponentiation.
$MOD = 1000000009;

function power($n)
{
    global $MOD;
    if ($n <= 1)
        return 1;

    // This power function returns first row of
    // {Transformation Matrix}^n-1*Initial Vector
    $n--;

    // This is an identity matrix.
    $res = array(array(1, 0), array(0, 1));

    // this is Transformation matrix.
    $tMat= array(array(2, 3), array(1, 0));

    // Matrix exponentiation to calculate
    // power of {tMat}^n-1 store res in "res" matrix.
    while ($n)
    {
        if ($n & 1)
        {
            $tmp = array_fill(0, 2, array_fill(0, 2, 0));
            $tmp[0][0] = ($res[0][0] * $tMat[0][0] +
                          $res[0][1] * $tMat[1][0]) % $MOD;
            $tmp[0][1] = ($res[0][0] * $tMat[0][1] +
                          $res[0][1] * $tMat[1][1]) % $MOD;
            $tmp[1][0] = ($res[1][0] * $tMat[0][0] +
                          $res[1][1] * $tMat[1][0]) % $MOD;
            $tmp[1][1] = ($res[1][0] * $tMat[0][1] +
                          $res[1][1] * $tMat[1][1]) % $MOD;
            $res[0][0] = $tmp[0][0];
            $res[0][1] = $tmp[0][1];
            $res[1][0] = $tmp[1][0];
            $res[1][1] = $tmp[1][1];
        }
        $n = (int)($n / 2);
        $tmp = array_fill(0, 2, array_fill(0, 2, 0));
        $tmp[0][0] = ($tMat[0][0] * $tMat[0][0] +
                      $tMat[0][1] * $tMat[1][0]) % $MOD;
        $tmp[0][1] = ($tMat[0][0] * $tMat[0][1] +
                      $tMat[0][1] * $tMat[1][1]) % $MOD;
        $tmp[1][0] = ($tMat[1][0] * $tMat[0][0] +
                      $tMat[1][1] * $tMat[1][0]) % $MOD;
        $tmp[1][1] = ($tMat[1][0] * $tMat[0][1] +
                      $tMat[1][1] * $tMat[1][1]) % $MOD;
        $tMat[0][0] = $tmp[0][0];
        $tMat[0][1] = $tmp[0][1];
        $tMat[1][0] = $tmp[1][0];
        $tMat[1][1] = $tmp[1][1];
    }

    // res store {Transformation matrix}^n-1
    // hence will be first row of res*Initial Vector.
    return ($res[0][0] * 1 + $res[0][1] * 1) % $MOD;
}

// Driver code
$n = 3;
echo power($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to find n-th term of a recursive
// function using matrix exponentiation.
var MOD = 1000000009;

function power(n)
{
    if (n <= 1)
        return 1;

    // This power function returns first row of
    // {Transformation Matrix}^n-1*Initial Vector
    n--;

    // This is an identity matrix.
    var res = [[1, 0,], [0, 1]];

    // this is Transformation matrix.
    var tMat = [[2, 3],[1, 0]];

    // Matrix exponentiation to calculate power of {tMat}^n-1
    // store res in "res" matrix.
    while (n) {

        if (n & 1) {
            var tmp = Array.from(Array(2), ()=> Array(2));
            tmp[0][0] = (res[0][0] * tMat[0][0] + res[0][1] * tMat[1][0]) % MOD;
            tmp[0][1] = (res[0][0] * tMat[0][1] + res[0][1] * tMat[1][1]) % MOD;
            tmp[1][0] = (res[1][0] * tMat[0][0] + res[1][1] * tMat[1][0]) % MOD;
            tmp[1][1] = (res[1][0] * tMat[0][1] + res[1][1] * tMat[1][1]) % MOD;
            res[0][0] = tmp[0][0];
            res[0][1] = tmp[0][1];
            res[1][0] = tmp[1][0];
            res[1][1] = tmp[1][1];
        }
        n = parseInt(n / 2);
        var tmp = Array.from(Array(2), ()=> Array(2));
        tmp[0][0] = (tMat[0][0] * tMat[0][0] + tMat[0][1] * tMat[1][0]) % MOD;
        tmp[0][1] = (tMat[0][0] * tMat[0][1] + tMat[0][1] * tMat[1][1]) % MOD;
        tmp[1][0] = (tMat[1][0] * tMat[0][0] + tMat[1][1] * tMat[1][0]) % MOD;
        tmp[1][1] = (tMat[1][0] * tMat[0][1] + tMat[1][1] * tMat[1][1]) % MOD;
        tMat[0][0] = tmp[0][0];
        tMat[0][1] = tmp[0][1];
        tMat[1][0] = tmp[1][0];
        tMat[1][1] = tmp[1][1];
    }

    // res store {Transformation matrix}^n-1
    // hence will be first row of res*Initial Vector.
    return (res[0][0] * 1 + res[0][1] * 1) % MOD;
}

// Driver code
var n = 3;
document.write( power(n));

</script>
```

**Output:** 

```
13
```

**时间复杂度:** O(Log n)
同样的思路用于[在 O(Log n)](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/) 中寻找第 n 个斐波那契数