# 元素为正整数且和为 K 的大小为 N 的数组个数

> 原文:[https://www . geesforgeks . org/number-arrays-size-n-what-elements-正整数-sum-k/](https://www.geeksforgeeks.org/number-arrays-size-n-whose-elements-positive-integers-sum-k/)

给定两个正整数 **N** 和 **K** 。任务是找到大小为 N 的数组的数量，这些数组的元素应该是正整数，并且元素的总和等于 k。
**示例:**

```
Input : N = 2, K = 3
Output : 2
Explanation: [1, 2] and [2, 1] are the only arrays of size 2 whose sum is 3.

Input : n = 3, k = 7
Output : 15
```

**先决条件:** [星条旗](https://en.wikipedia.org/wiki/Stars_and_bars_(combinatorics))

假设有 K 个相同的对象需要放置在 N 个容器(数组的 N 个索引)中，这样每个容器至少有一个对象。我们不是开始将对象放入箱中，而是开始将对象放在一条线上，其中第一个箱的对象将从左边开始，然后是第二个箱的对象，以此类推。因此，一旦知道什么是去往第二箱的第一对象，什么是去往第三箱的第一对象，等等，就将确定配置。我们可以通过在两个物体之间的某些地方放置 N×1 个分隔条来表明这一点；因为不允许任何箱是空的，所以在给定的一对对象之间最多只能有一个条。所以，我们有 K 个物体在一条直线上，有 K–1 个间隙。现在我们必须选择 N–1 个间隙来放置 K–1 个间隙中的条。这可以通过<sup>K–1</sup>C<sub>N–1</sub>选择。
以下是本办法的实施情况:

## C++

```
// CPP Program to find the number of arrays of
// size N whose elements are positive integers
// and sum is K
#include <bits/stdc++.h>
using namespace std;

// Return nCr
int binomialCoeff(int n, int k)
{
    int C[k + 1];
    memset(C, 0, sizeof(C));

    C[0] = 1; // nC0 is 1

    for (int i = 1; i <= n; i++) {
        // Compute next row of pascal triangle using
        // the previous row
        for (int j = min(i, k); j > 0; j--)
            C[j] = C[j] + C[j - 1];
    }
    return C[k];
}

// Return the number of array that can be
// formed of size n and sum equals to k.
int countArray(int N, int K)
{
    return binomialCoeff(K - 1, N - 1);
}

// Driver Code
int main()
{
    int N = 2, K = 3;

    cout << countArray(N, K) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the
// number of arrays of size
// N whose elements are positive
// integers and sum is K
import java.io.*;

class GFG
{

// Return nCr
static int binomialCoeff(int n,
                         int k)
{
    int []C = new int[k + 1];

    C[0] = 1; // nC0 is 1

    for (int i = 1; i <= n; i++)
    {
        // Compute next row of pascal
        // triangle using the previous row
        for (int j = Math.min(i, k); j > 0; j--)
            C[j] = C[j] + C[j - 1];
    }
    return C[k];
}

// Return the number of
// array that can be
// formed of size n and
// sum equals to k.
static int countArray(int N, int K)
{
    return binomialCoeff(K - 1, N - 1);
}

// Driver Code
public static void main (String[] args)
{
        int N = 2, K = 3;

System.out.println( countArray(N, K));
}
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python3 Program to find the number
# of arrays of size N whose elements
# are positive integers and sum is K

# Return nCr
def binomialCoeff(n, k):

    C = [0] * (k + 1);

    C[0] = 1; # nC0 is 1

    for i in range(1, n + 1):

        # Compute next row of pascal
        # triangle using the previous row
        for j in range(min(i, k), 0, -1):
            C[j] = C[j] + C[j - 1];
    return C[k];

# Return the number of array that
# can be formed of size n and
# sum equals to k.
def countArray(N, K):

    return binomialCoeff(K - 1, N - 1);

# Driver Code
N = 2;
K = 3;

print(countArray(N, K));

# This code is contributed by mits
```

## C#

```
// C# Program to find the
// number of arrays of size
// N whose elements are positive
// integers and sum is K
using System;

class GFG
{
// Return nCr
static int binomialCoeff(int n,
                         int k)
{
    int []C = new int[k + 1];

    C[0] = 1; // nC0 is 1

    for (int i = 1; i <= n; i++)
    {
        // Compute next row of
        // pascal triangle using
        // the previous row
        for (int j = Math.Min(i, k);
                         j > 0; j--)
            C[j] = C[j] + C[j - 1];
    }
    return C[k];
}

// Return the number of
// array that can be
// formed of size n and
// sum equals to k.
static int countArray(int N,
                      int K)
{
    return binomialCoeff(K - 1,
                         N - 1);
}

// Driver Code
static public void Main ()
{
    int N = 2, K = 3;

    Console.WriteLine(
            countArray(N, K));
}
}

// This code is contributed by ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find the
// number of arrays of size
// N whose elements are
// positive integers and
// sum is K

// Return nCr
function binomialCoeff($n, $k)
{
    $C = array_fill(0, ($k + 1), 0);

    $C[0] = 1; // nC0 is 1

    for ($i = 1; $i <= $n; $i++)
    {
        // Compute next row
        // of pascal triangle
        // using the previous row
        for ($j = min($i, $k);
             $j > 0; $j--)
            $C[$j] = $C[$j] +
                     $C[$j - 1];
    }
    return $C[$k];
}

// Return the number of
// array that can be
// formed of size n and
// sum equals to k.
function countArray($N, $K)
{
    return binomialCoeff($K - 1,
                         $N - 1);
}

// Driver Code
$N = 2;
$K = 3;

echo countArray($N, $K);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript Program to find the number of arrays of
// size N whose elements are positive integers
// and sum is K

// Return nCr
function binomialCoeff(n, k)
{
    var C = Array(k+1).fill(0);

    C[0] = 1; // nC0 is 1

    for (var i = 1; i <= n; i++) {
        // Compute next row of pascal triangle using
        // the previous row
        for (var j = Math.min(i, k); j > 0; j--)
            C[j] = C[j] + C[j - 1];
    }
    return C[k];
}

// Return the number of array that can be
// formed of size n and sum equals to k.
function countArray(N, K)
{
    return binomialCoeff(K - 1, N - 1);
}

// Driver Code
var N = 2, K = 3;
document.write( countArray(N, K));

</script>
```

**输出:**

```
2
```