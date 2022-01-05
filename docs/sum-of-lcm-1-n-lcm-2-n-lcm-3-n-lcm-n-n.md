# LCM(1，n)、LCM(2，n)、LCM(3，n)、…、LCM(n，n)之和

> 原文:[https://www . geesforgeks . org/sum-of-LCM-1-n-LCM-2-n-LCM-3-n-LCM-n-n/](https://www.geeksforgeeks.org/sum-of-lcm-1-n-lcm-2-n-lcm-3-n-lcm-n-n/)

给定一个整数 **n** ，任务是求和:

> LCM(1，n) + LCM(2，n) + LCM(3，n) + … + LCM(n，n)
> 其中 LCM(i，n)是 I 和 n 的最小公倍数。

**示例:**

> **输入:**3
> T3】输出: 10
> LCM(1，3) + LCM(2，3) + LCM(3，3) = 3 + 6 + 3 = 12
> 
> **输入:**5
> T3】输出: 55
> LCM(1，5) + LCM(2，5) + LCM(3，5) + LCM(4，5) + LCM(5，5) = 55

**天真法:**两个数的 LCM**a**和 **b** = **(a * b) / gcd(a，b)** 其中 **gcd(a，b)** 是 **a** 和 **b** 的最大公约数。

*   从 **(1，n)** 到 **(n，n)** 计算所有对的单个 LCM 值。
*   将上一步的所有 LCM 结果相加。
*   最后打印**和**。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define ll long long int

// Function to calculate the required LCM sum
ll lcmSum(long long n)
{
    ll sum = 0;

    for (long long int i = 1; i <= n; i++) {

        // GCD of i and n
        long long int gcd = __gcd(i, n);

        // LCM of i and n i.e. (i * n) / gcd(i, n)
        long long int lcm = (i * n) / gcd;

        // Update sum
        sum = sum + lcm;
    }

    return sum;
}

// Driver code
int main()
{
    int n = 3;

    cout << lcmSum(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// return gcd of two numbers
static int gcd(int a,int b)
{

    // Everything divides 0
    if (a == 0)
        return b;
    if (b == 0)
        return a;

    // base case
    if (a == b)
        return a;

    // a is greater
    if (a > b)
        return gcd(a - b, b);
    return gcd(a, b - a);

}

// Function to calculate the required LCM sum
static int lcmSum(int n)
{
    int sum = 0;

    for (int i = 1; i <= n; i++)
    {

        // GCD of i and n
        int gcd = gcd(i, n);

        // LCM of i and n i.e. (i * n) / gcd(i, n)
        int lcm = (i * n) / gcd;

        // Update sum
        sum = sum + lcm;
    }

    return sum;
}

// Driver code
public static void main(String args[])
{
    int n = 3;

    System.out.println(lcmSum(n));
}
}

// This code is contributed by
// Surendra _Gangwar
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import math

# Function to calculate the required LCM sum
def lcmSum(n):

    Sum = 0
    for i in range(1, n + 1):

        # GCD of i and n
        gcd = math.gcd(i, n)

        # LCM of i and n i.e. (i * n) / gcd(i, n)
        lcm = (i * n) // gcd

        # Update sum
        Sum = Sum + lcm

    return Sum

# Driver code
if __name__ == "__main__":

    n = 3
    print(lcmSum(n))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the approach
class GFG
{

// return gcd of two numbers
static int gcd1(int a,int b)
{

    // Everything divides 0
    if (a == 0)
        return b;
    if (b == 0)
        return a;

    // base case
    if (a == b)
        return a;

    // a is greater
    if (a > b)
        return gcd1(a - b, b);
    return gcd1(a, b - a);

}

// Function to calculate the required LCM sum
static int lcmSum(int n)
{
    int sum = 0;

    for (int i = 1; i <= n; i++)
    {

        // GCD of i and n
        int gcd = gcd1(i, n);

        // LCM of i and n i.e. (i * n) / gcd(i, n)
        int lcm = (i * n) / gcd;

        // Update sum
        sum = sum + lcm;
    }

    return sum;
}

// Driver code
static void Main()
{
    int n = 3;

    System.Console.WriteLine(lcmSum(n));
}
}

// This code is contributed by chandan_jnu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

function __gcd($a, $b)
{
    if($b == 0)
    return $a;
    return __gcd($b, $a % $b);
}

// Function to calculate the required LCM sum
function lcmSum($n)
{
    $sum = 0;

    for ($i = 1; $i <= $n; $i++)
    {

        // GCD of i and n
        $gcd = __gcd($i, $n);

        // LCM of i and n i.e. (i * n) / gcd(i, n)
        $lcm = ($i * $n) / $gcd;

        // Update sum
        $sum = $sum + $lcm;
    }

    return $sum;
}

// Driver code
$n = 3;

echo lcmSum($n);

// This code is contributed by chandan_jnu
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// return gcd of two numbers
function gcd(a, b)
{

    // Everything divides 0
    if (a == 0)
        return b;
    if (b == 0)
        return a;

    // base case
    if (a == b)
        return a;

    // a is greater
    if (a > b)
        return gcd(a - b, b);

    return gcd(a, b - a);
}

// Function to calculate the required LCM sum
function lcmSum(n)
{
    var sum = 0;

    for(var i = 1; i <= n; i++)
    {

        // GCD of i and n
        var _gcd = gcd(i, n);

        // LCM of i and n i.e. (i * n) / gcd(i, n)
        var lcm = (i * n) / _gcd;

        // Update sum
        sum = sum + lcm;
    }
    return sum;
}

// Driver code
var n = 3;

document.write(lcmSum(n));

// This code is contributed by Ankita saini

</script>
```

**Output:** 

```
12
```

**高效方法:**使用[欧拉全能性函数](https://www.geeksforgeeks.org/eulers-totient-function/)、
T5】∑LCM(I，n)=(∑(d * ETF(d))+1)* n)/2
其中 **ETF(d)** 是 **d** 的欧拉全能性函数， **d** 属于 n 的**除数集合。**

**示例:**

> 设 n 为 5，则 LCM(1，5) + LCM(2，5) + LCM(3，5) + LCM(4，5) + LCM(5，5)
> = 5 + 10 + 15 + 20 + 5
> = 55
> 具有欧拉全能性的函数:
> 5 的所有除数都是{1，5}
> 因此，((1*ETF(1) + 5*ETF(5) + 1) * 5) / 2 = 55

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

#define n 1000002
#define ll long long int

ll phi[n + 2], ans[n + 2];

// Euler totient Function
void ETF()
{
    for (int i = 1; i <= n; i++) {
        phi[i] = i;
    }

    for (int i = 2; i <= n; i++) {
        if (phi[i] == i) {
            phi[i] = i - 1;
            for (int j = 2 * i; j <= n; j += i) {
                phi[j] = (phi[j] * (i - 1)) / i;
            }
        }
    }
}

// Function to return the required LCM sum
ll LcmSum(int m)
{
    ETF();

    for (int i = 1; i <= n; i++) {

        // Summation of d * ETF(d) where
        // d belongs to set of divisors of n
        for (int j = i; j <= n; j += i) {
            ans[j] += (i * phi[i]);
        }
    }

    ll answer = ans[m];
    answer = (answer + 1) * m;
    answer = answer / 2;
    return answer;
}

// Driver code
int main()
{
    int m = 5;

    cout << LcmSum(m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

static int n = 1000002;

static int[] phi = new int[n + 2];
static int[] ans = new int[n + 2];

// Euler totient Function
static void ETF()
{
    for (int i = 1; i <= n; i++)
    {
        phi[i] = i;
    }

    for (int i = 2; i <= n; i++)
    {
        if (phi[i] == i)
        {
            phi[i] = i - 1;
            for (int j = 2 * i; j <= n; j += i)
            {
                phi[j] = (phi[j] * (i - 1)) / i;
            }
        }
    }
}

// Function to return the required LCM sum
static int LcmSum(int m)
{
    ETF();

    for (int i = 1; i <= n; i++)
    {

        // Summation of d * ETF(d) where
        // d belongs to set of divisors of n
        for (int j = i; j <= n; j += i)
        {
            ans[j] += (i * phi[i]);
        }
    }

    int answer = ans[m];
    answer = (answer + 1) * m;
    answer = answer / 2;
    return answer;
}

// Driver code
public static void main (String[] args)
{
    int m = 5;
    System.out.println(LcmSum(m));
}
}

// This code is contributed by chandan_jnu
```

## 蟒蛇 3

```
# Python3 implementation of the approach
n = 100002;

phi = [0] * (n + 2);
ans = [0] * (n + 2);

# Euler totient Function
def ETF():

    for i in range(1, n + 1):
        phi[i] = i;

    for i in range(2, n + 1):
        if (phi[i] == i):
            phi[i] = i - 1;
            for j in range(2 * i, n + 1, i):
                phi[j] = (phi[j] * (i - 1)) // i;

# Function to return the required LCM sum
def LcmSum(m):
    ETF();

    for i in range(1, n + 1):

        # Summation of d * ETF(d) where
        # d belongs to set of divisors of n
        for j in range(i, n + 1, i):
            ans[j] += (i * phi[i]);

    answer = ans[m];
    answer = (answer + 1) * m;
    answer = answer // 2;
    return answer;

# Driver code
m = 5;
print(LcmSum(m));

# This code is contributed
# by chandan_jnu
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
static int n = 1000002;

static int[] phi = new int[n + 2];
static int[] ans = new int[n + 2];

// Euler totient Function
static void ETF()
{
    for (int i = 1; i <= n; i++)
    {
        phi[i] = i;
    }

    for (int i = 2; i <= n; i++)
    {
        if (phi[i] == i)
        {
            phi[i] = i - 1;
            for (int j = 2 * i; j <= n; j += i)
            {
                phi[j] = (phi[j] * (i - 1)) / i;
            }
        }
    }
}

// Function to return the required LCM sum
static int LcmSum(int m)
{
    ETF();

    for (int i = 1; i <= n; i++)
    {

        // Summation of d * ETF(d) where
        // d belongs to set of divisors of n
        for (int j = i; j <= n; j += i)
        {
            ans[j] += (i * phi[i]);
        }
    }

    int answer = ans[m];
    answer = (answer + 1) * m;
    answer = answer / 2;
    return answer;
}

// Driver code
static void Main()
{
    int m = 5;
    Console.WriteLine(LcmSum(m));
}
}

// This code is contributed by chandan_jnu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach
$n = 10002;

$phi = array_fill(0, $n + 2, 0);
$ans = array_fill(0, $n + 2, 0);

// Euler totient Function
function ETF()
{
    global $phi, $n;
    for ($i = 1; $i <= $n; $i++)
    {
        $phi[$i] = $i;
    }

    for ($i = 2; $i <= $n; $i++)
    {
        if ($phi[$i] == $i)
        {
            $phi[$i] = $i - 1;
            for ($j = 2 * $i; $j <= $n; $j += $i)
            {
                $phi[$j] = (int)(($phi[$j] *
                                 ($i - 1)) / $i);
            }
        }
    }
}

// Function to return the required LCM sum
function LcmSum($m)
{
    ETF();
    global $ans, $n, $phi;

    for ($i = 1; $i <= $n; $i++)
    {

        // Summation of d * ETF(d) where
        // d belongs to set of divisors of n
        for ($j = $i; $j <= $n; $j += $i)
        {
            $ans[$j] += ($i * $phi[$i]);
        }
    }

    $answer = $ans[$m];
    $answer = ($answer + 1) * $m;
    $answer = (int)($answer / 2);
    return $answer;
}

// Driver code
$m = 5;

echo LcmSum($m);

// This code is contributed by chandan_jnu
?>
```

## java 描述语言

```
<script>

// javascript implementation of the approach   
var n = 1000002;

    var phi = Array(n + 2).fill(0);
    var ans = Array(n + 2).fill(0);

    // Euler totient Function
    function ETF() {
        for (i = 1; i <= n; i++) {
            phi[i] = i;
        }

        for (i = 2; i <= n; i++) {
            if (phi[i] == i) {
                phi[i] = i - 1;
                for (j = 2 * i; j <= n; j += i) {
                    phi[j] = (phi[j] * (i - 1)) / i;
                }
            }
        }
    }

    // Function to return the required LCM sum
    function LcmSum(m) {
        ETF();

        for (i = 1; i <= n; i++) {

            // Summation of d * ETF(d) where
            // d belongs to set of divisors of n
            for (j = i; j <= n; j += i) {
                ans[j] += (i * phi[i]);
            }
        }

        var answer = ans[m];
        answer = (answer + 1) * m;
        answer = answer / 2;
        return answer;
    }

    // Driver code
        var m = 5;
        document.write(LcmSum(m));

// This code is contributed by aashish1995
</script>
```

**Output:** 

```
55
```

**时间复杂度:**O(N * logN)
T3】辅助空间: O(N)