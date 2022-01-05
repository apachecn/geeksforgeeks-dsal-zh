# 从一组中挑选男女组成一个团队的方式

> 原文:[https://www . geeksforgeeks . org/从一个小组到一个团队的男女选择方式/](https://www.geeksforgeeks.org/ways-of-selecting-men-and-women-from-a-group-to-make-a-team/)

给定四个整数 n，w，m 和 k，其中，

*   m 是男人的总数。
*   w 是女性的总数。
*   n 是需要被选中组成团队的总人数。
*   k 是必须选出的最少人数。

任务是找到组建团队的方法。
**例:**

> **输入:** m = 2，w = 2，n = 3，k = 1
> **输出:** 4
> 有 2 男 2 女。我们需要组建一支至少有一男一女的 3 人团队。我们可以通过以下方式组建团队。
> m1 m2 w1
> m1 w1 w2
> m2 w1 w2
> m1 m2 w2
> **输入:** m = 7，w = 6，n = 5，k = 3
> **输出:** 756
> **输入:** m = 5，w = 6，n = 6，k = 3
> **输出:** 281

**进场:**既然来了，我们至少要带 k 个人。

> 总计方式=选择“k”人时的方式+选择“k+1”人时的方式+ … +选择“n”人时的方式

。
从上面的第一个例子来看，7 男 6 女，总共需要选 5 个人，至少有 3 个男的，
路数=(7 C3 x 6 C2)+(7 C4 x 6 C1)+(7 C5)
= 7 x 6 x 5 x 6 x 5+(7 C3 x 6 C1)+(7 C2)
= 525+7 x 6 x 5 x 6+7 x 6
=(525+210+21)
= 756

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Returns factorial
// of the number
int fact(int n)
{
    int fact = 1;
    for (int i = 2; i <= n; i++)
        fact *= i;
    return fact;
}

// Function to calculate ncr
int ncr(int n, int r)
{
    int ncr = fact(n) / (fact(r) * fact(n - r));
    return ncr;
}

// Function to calculate
// the total possible ways
int ways(int m, int w, int n, int k)
{

    int ans = 0;
    while (m >= k) {
        ans += ncr(m, k) * ncr(w, n - k);
        k += 1;
    }

    return ans;
}

// Driver code
int main()
{

    int m, w, n, k;
    m = 7;
    w = 6;
    n = 5;
    k = 3;
    cout << ways(m, w, n, k);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

import java.io.*;

class GFG {

// Returns factorial
// of the number
static int fact(int n)
{
    int fact = 1;
    for (int i = 2; i <= n; i++)
        fact *= i;
    return fact;
}

// Function to calculate ncr
static int ncr(int n, int r)
{
    int ncr = fact(n) / (fact(r) * fact(n - r));
    return ncr;
}

// Function to calculate
// the total possible ways
static int ways(int m, int w, int n, int k)
{

    int ans = 0;
    while (m >= k) {
        ans += ncr(m, k) * ncr(w, n - k);
        k += 1;
    }

    return ans;
}

// Driver code
    public static void main (String[] args) {

    int m, w, n, k;
    m = 7;
    w = 6;
    n = 5;
    k = 3;
    System.out.println( ways(m, w, n, k));
    }
}
// This Code is contributed
// by shs
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Returns factorial of the number
def fact(n):
    fact = 1
    for i in range(2, n + 1):
        fact *= i
    return fact

# Function to calculate ncr
def ncr(n, r):
    ncr = fact(n) // (fact(r) * fact(n - r))
    return ncr

# Function to calculate
# the total possible ways
def ways(m, w, n, k):
    ans = 0
    while (m >= k):
        ans += ncr(m, k) * ncr(w, n - k)
        k += 1

    return ans;

# Driver code
m = 7
w = 6
n = 5
k = 3
print(ways(m, w, n, k))

# This code is contributed by sahishelangia
```

## C#

```
// C# implementation of the approach

class GFG {

// Returns factorial
// of the number
static int fact(int n)
{
    int fact = 1;
    for (int i = 2; i <= n; i++)
        fact *= i;
    return fact;
}

// Function to calculate ncr
static int ncr(int n, int r)
{
    int ncr = fact(n) / (fact(r) * fact(n - r));
    return ncr;
}

// Function to calculate
// the total possible ways
static int ways(int m, int w, int n, int k)
{

    int ans = 0;
    while (m >= k) {
        ans += ncr(m, k) * ncr(w, n - k);
        k += 1;
    }

    return ans;
}

// Driver code
    static void Main () {

    int m, w, n, k;
    m = 7;
    w = 6;
    n = 5;
    k = 3;
    System.Console.WriteLine( ways(m, w, n, k));
    }
}
// This Code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Returns factorial of the number
function fact($n)
{
    $fact = 1;
    for ($i = 2; $i <= $n; $i++)
        $fact *= $i;
    return $fact;
}

// Function to calculate ncr
function ncr($n, $r)
{
    $ncr = (int)(fact($n) / (fact($r) *
                 fact($n - $r)));
    return $ncr;
}

// Function to calculate the total
// possible ways
function ways($m, $w, $n, $k)
{
    $ans = 0;
    while ($m >= $k)
    {
        $ans += ncr($m, $k) *
                ncr($w, $n - $k);
        $k += 1;
    }

    return $ans;
}

// Driver code
$m = 7;
$w = 6;
$n = 5;
$k = 3;
echo ways($m, $w, $n, $k);

// This Code is contributed
// by Mukul Singh
```

## java 描述语言

```
<script>
// javascript implementation of the approach

// Returns factorial
// of the number
function fact(n)
{
    var fact = 1;
    for (i = 2; i <= n; i++)
        fact *= i;
    return fact;
}

// Function to calculate ncr
function ncr(n , r)
{
    var ncr = fact(n) / (fact(r) * fact(n - r));
    return parseInt(ncr);
}

// Function to calculate
// the total possible ways
function ways(m , w , n , k)
{

    var ans = 0;
    while (m >= k)
    {
        ans += ncr(m, k) * ncr(w, n - k);
        k += 1;
    }

    return parseInt(ans);
}

// Driver code
var m, w, n, k;
m = 7;
w = 6;
n = 5;
k = 3;
document.write( ways(m, w, n, k));

// This code is contributed by 29AjayKumar.
</script>
```

**Output:** 

```
756
```

**进一步优化:**上述代码可以使用[二项式系数计算的更快算法](https://www.geeksforgeeks.org/space-and-time-efficient-binomial-coefficient/)进行优化。