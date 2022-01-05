# 一系列先奇数后偶数的自然数范围之和

> 原文:[https://www . geeksforgeeks . org/先奇数后偶数自然数数列范围总和/](https://www.geeksforgeeks.org/sum-of-range-in-a-series-of-first-odd-then-even-natural-numbers/)

序列首先由从 1 到 n 开始的所有奇数组成，然后是从 2 到 n 开始的剩余偶数。让我们假设 n 为 1000。那么序列就变成了 1 3 5 7….999 2 4 6….1000
我们给定了一个范围(L，R)，我们需要求这个序列在给定范围内的数的和。
**注:这里给出的范围为(L，R) L 和 R 都包含在范围内**
例:

```
Input  : n = 10
         Range 1 6
Output : 27
Explanation:
Sequence is 1 3 5 7 9 2 4 6 8 10
Sum in range (2, 6) 
= 1 + 3 + 5 + 7 + 9 + 2 
= 27

Input  : n = 5
         Range 1 2
Output : 4
Explanation:
sequence is 1 3 5 2 4
sum = 1 + 3 = 4
```

思路是先求左前(不含左)数的和，再求右前(含右)数的和。我们得到的结果是第二个和减去第一个和。
**如何求和直到极限？**
我们先数一数有多少个奇数，然后用[奇数自然数之和](https://www.geeksforgeeks.org/sum-first-n-odd-numbers-o1-complexity/)和[偶数自然数之和](https://www.geeksforgeeks.org/sum-first-n-even-numbers/)的公式求结果。
奇数的计数怎么找？

*   如果 n 是奇数，那么奇数的数目是((n/2) + 1)
*   如果 n 是偶数，那么奇数的数目是(n/2)

通过简单的观察，我们得到奇数的个数是 ceil(n/2)。所以，偶数的数量是 n–ceil(n/2)。

*   前 n 个奇数之和为(N^2)

*   前 n 个偶数之和为(N^2) + N

对于一个给定的数 x，我们如何在从 1 到 x 的序列中找到和？
假设 x 小于奇数个数。

*   然后我们简单地返回(x*x)

如果 x 大于奇数数量

*   var = x-奇数;

*   这意味着我们首先需要改变偶数

*   我们返回(奇数*奇数)+(var * var)+var；

## C++

```
// CPP program to find sum in the given range in
// the sequence 1 3 5 7.....N 2 4 6...N-1
#include <bits/stdc++.h>
using namespace std;

// For our convenience
#define ll long long

// Function that returns sum
// in the range 1 to x in the
// sequence 1 3 5 7.....N 2 4 6...N-1
ll sumTillX(ll x, ll n)
{
    // number of odd numbers
    ll odd = ceil(n / 2.0);

    if (x <= odd)
       return x * x;

    // number of extra even
    // numbers required
    ll even = x - odd;

    return ((odd * odd) + (even * even) + even);
}

int rangeSum(int N, int L, int R)
{
   return sumTillX(R, N) - sumTillX(L-1, N);
}

// Driver code
int main()
{
    ll N = 10, L = 1, R = 6;   
    cout << rangeSum(N, L, R);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find
// sum in the given
// range in the sequence
// 1 3 5 7.....N
// 2 4 6...N-1

class GFG {

    // Function that returns sum
    // in the range 1 to x in the
    // sequence 1 3 5 7.....N 2 4 6...N-1
    static double sumTillX(double x,
                           double n)
    {

        // number of odd numbers
        double odd = Math.ceil(n / 2.0);

        if (x <= odd)
            return x * x;

        // number of extra even
        // numbers required
        double even = x - odd;

        return ((odd * odd) + (even *
                       even) + even);
    }

    static double rangeSum(double N,
                           double L,
                           double R)
    {
        return sumTillX(R, N) -
               sumTillX(L-1, N);
    }

    // Driver Code
    public static void main(String args[])
    {
        long N = 10, L = 1, R = 6;
        int n = 101;
        System.out.println((int)rangeSum(N, L, R));

    }
}

// This code is contributed by Sam007
```

## 蟒蛇 3

```
# Python 3 program to find sum in the
# given range in the sequence 1 3 5 7
# .....N 2 4 6...N-1
import math

# For our convenience
#define ll long long

# Function that returns sum in the
# range 1 to x in the sequence
# 1 3 5 7.....N 2 4 6...N-1
def sumTillX(x, n):

    # number of odd numbers
    odd = math.ceil(n / 2.0)

    if (x <= odd):
        return x * x;

    # number of extra even
    # numbers required
    even = x - odd;

    return ((odd * odd) +
            (even * even) + even);

def rangeSum(N, L, R):

    return (sumTillX(R, N) - 
                sumTillX(L-1, N));

# Driver code
N = 10
L = 1
R = 6
print(rangeSum(N, L, R))

# This code is contributed by
# Smitha
```

## C#

```
// C# program to find sum in the given
// range in the sequence 1 3 5 7.....N
// 2 4 6...N-1
using System;

public class GFG {

    // Function that returns sum
    // in the range 1 to x in the
    // sequence 1 3 5 7.....N 2 4 6...N-1
    static double sumTillX(double x, double n)
    {

        // number of odd numbers
        double odd = Math.Ceiling(n / 2.0);

        if (x <= odd)
            return x * x;

        // number of extra even
        // numbers required
        double even = x - odd;

        return ((odd * odd) + (even * even)
                                    + even);
    }

    static double rangeSum(double N, double L,
                                       double R)
    {
        return sumTillX(R, N) - sumTillX(L-1, N);
    }

    // Driver code
    public static void Main()
    {
        long N = 10, L = 1, R = 6;
        Console.Write(rangeSum(N, L, R));
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find sum
// in the given range in the
// sequence 1 3 5 7.....
// N 2 4 6...N-1

// Function that returns sum
// in the range 1 to x in the
// sequence 1 3 5 7.....
// N 2 4 6...N-1
function sumTillX($x, $n)
{

    // number of odd numbers
    $odd = ceil($n / 2.0);

    if ($x <= $odd)
    return $x * $x;

    // number of extra even
    // numbers required
    $even = $x - $odd;

    return (($odd * $odd) +
            ($even * $even) +
             $even);
}

function rangeSum($N, $L, $R)
{
    return sumTillX($R, $N) -
           sumTillX($L-1, $N);
}

// Driver code
$N = 10; $L = 1; $R = 6;
echo(rangeSum($N, $L, $R));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>
// javascript program to find sum in the given range in
// the sequence 1 3 5 7.....N 2 4 6...N-1

// Function that returns sum
// in the range 1 to x in the
// sequence 1 3 5 7.....N 2 4 6...N-1
function sumTillX( x,  n)
{

    // number of odd numbers
    let odd = Math.ceil(n / 2.0);

    if (x <= odd)
       return x * x;

    // number of extra even
    // numbers required
    let even = x - odd;

    return ((odd * odd) + (even * even) + even);
}

function rangeSum( N,  L,  R)
{
   return sumTillX(R, N) - sumTillX(L-1, N);
}

// Driver code
    let N = 10, L = 1, R = 6;   
     document.write(rangeSum(N, L, R));

// This code is contributed by Rajput-Ji

</script>
```

**Output:** 

```
27
```