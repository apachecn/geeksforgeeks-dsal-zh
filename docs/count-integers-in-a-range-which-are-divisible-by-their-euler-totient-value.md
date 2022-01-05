# 计算可被欧拉全能值整除的范围内的整数

> 原文:[https://www . geeksforgeeks . org/count-范围内可被其欧拉全能值整除的整数/](https://www.geeksforgeeks.org/count-integers-in-a-range-which-are-divisible-by-their-euler-totient-value/)

给定 2 个整数 **L 和 R** ，任务是找出[L，R]范围内的整数个数，使它们能被其欧拉全能值完全整除。
**例:**

> **输入:** L = 2，R = 3
> T3】输出: 1
> 
> ```
> *** QuickLaTeX cannot compile formula:
>  
> 
> *** Error message:
> Error: Nothing to show, formula is empty
> 
> ```
> 
> **(2) = 2 = > 2 %**
> 
> ```
> *** QuickLaTeX cannot compile formula:
>  
> 
> *** Error message:
> Error: Nothing to show, formula is empty
> 
> ```
> 
> **(2) = 0**
> 
> ```
> *** QuickLaTeX cannot compile formula:
>  
> 
> *** Error message:
> Error: Nothing to show, formula is empty
> 
> ```
> 
> **(3) = 2 = > 3 %**
> 
> ```
> *** QuickLaTeX cannot compile formula:
>  
> 
> *** Error message:
> Error: Nothing to show, formula is empty
> 
> ```
> 
> **(3) = 1**
> 因此 2 满足条件。
> **输入:** L = 12，R = 21
> **输出:** 3
> 只有 12、16、18 满足条件。

**方法:**我们知道一个数的[欧拉全能函数](https://www.geeksforgeeks.org/eulers-totient-function/)给出如下:

重新排列术语，我们得到:

如果我们仔细观察 RHS，我们发现只有 **2 和 3 是满足 **n %** 的素数**

```
*** QuickLaTeX cannot compile formula:

*** Error message:
Error: Nothing to show, formula is empty

```

**= 0** 。这是因为对于素数 **p <sub>1</sub> = 2 和 p <sub>2</sub> = 3，p<sub>1</sub>–1 = 1 和 p<sub>2</sub>–1 = 2**。因此，只有表格 **2 <sup>p</sup> 3 <sup>q</sup> 中 p > = 1 和 q > = 0** 的数字需要在范围**【L，R】**内进行计数。
以下是上述办法的实施:

## C++

```
// C++ implementation of the above approach.
#include <bits/stdc++.h>

#define ll long long
using namespace std;

// Function to return a^n
ll power(ll a, ll n)
{
    if (n == 0)
        return 1;

    ll p = power(a, n / 2);
    p = p * p;

    if (n & 1)
        p = p * a;

    return p;
}

// Function to return count of integers
// that satisfy n % phi(n) = 0
int countIntegers(ll l, ll r)
{

    ll ans = 0, i = 1;
    ll v = power(2, i);

    while (v <= r) {

        while (v <= r) {

            if (v >= l)
                ans++;
            v = v * 3;
        }

        i++;
        v = power(2, i);
    }

    if (l == 1)
        ans++;

    return ans;
}

// Driver Code
int main()
{
    ll l = 12, r = 21;
    cout << countIntegers(l, r);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach.
class GFG
{

// Function to return a^n
static long power(long a, long n)
{
    if (n == 0)
        return 1;

    long p = power(a, n / 2);
    p = p * p;

    if (n%2== 1)
        p = p * a;

    return p;
}

// Function to return count of integers
// that satisfy n % phi(n) = 0
static int countIntegers(long l, long r)
{

    long ans = 0, i = 1;
    long v = power(2, i);

    while (v <= r)
    {
        while (v <= r)
        {

            if (v >= l)
                ans++;
            v = v * 3;
        }

        i++;
        v = power(2, i);
    }

    if (l == 1)
        ans++;

    return (int) ans;
}

// Driver Code
public static void main(String[] args)
{
    long l = 12, r = 21;
    System.out.println(countIntegers(l, r));
}
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return a^n
def power(a, n):

    if n == 0:
        return 1

    p = power(a, n // 2)
    p = p * p

    if n & 1:
        p = p * a

    return p

# Function to return count of integers
# that satisfy n % phi(n) = 0
def countIntegers(l, r):

    ans, i = 0, 1
    v = power(2, i)

    while v <= r:

        while v <= r:

            if v >= l:
                ans += 1

            v = v * 3

        i += 1
        v = power(2, i)

    if l == 1:
        ans += 1

    return ans

# Driver Code
if __name__ == "__main__":

    l, r = 12, 21
    print(countIntegers(l, r))

# This code is contributed
# by Rituraj Jain
```

## C#

```
// C# implementation of the above approach.
using System;

class GFG
{

// Function to return a^n
static long power(long a, long n)
{
    if (n == 0)
        return 1;

    long p = power(a, n / 2);
    p = p * p;

    if (n % 2 == 1)
        p = p * a;

    return p;
}

// Function to return count of integers
// that satisfy n % phi(n) = 0
static int countIntegers(long l, long r)
{

    long ans = 0, i = 1;
    long v = power(2, i);

    while (v <= r)
    {
        while (v <= r)
        {

            if (v >= l)
                ans++;
            v = v * 3;
        }

        i++;
        v = power(2, i);
    }

    if (l == 1)
        ans++;

    return (int) ans;
}

// Driver Code
public static void Main()
{
    long l = 12, r = 21;
    Console.WriteLine(countIntegers(l, r));
}
}

/* This code contributed by PrinciRaj1992 */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to return a^n
function power($a, $n)
{
    if ($n == 0)
        return 1;

    $p = power($a, $n / 2);
    $p = $p * $p;

    if ($n & 1)
        $p = $p * $a;

    return $p;
}

// Function to return count of integers
// that satisfy n % phi(n) = 0
function countIntegers($l, $r)
{
    $ans = 0 ;
    $i = 1;
    $v = power(2, $i);

    while ($v <= $r)
    {
        while ($v <= $r)
        {
            if ($v >= $l)
                $ans++;
            $v = $v * 3;
        }

        $i++;
        $v = power(2, $i);
    }

    if ($l == 1)
        $ans++;

    return $ans;
}

// Driver Code
$l = 12;
$r = 21;

echo countIntegers($l, $r);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach.   

// Function to return a^n
    function power(a , n) {
        if (n == 0)
            return 1;

        var p = power(a, parseInt(n / 2));
        p = p * p;

        if (n % 2 == 1)
            p = p * a;

        return p;
    }

    // Function to return count of integers
    // that satisfy n % phi(n) = 0
    function countIntegers(l , r) {

        var ans = 0, i = 1;
        var v = power(2, i);

        while (v <= r) {
            while (v <= r) {

                if (v >= l)
                    ans++;
                v = v * 3;
            }

            i++;
            v = power(2, i);
        }

        if (l == 1)
            ans++;

        return parseInt( ans);
    }

    // Driver Code

        var l = 12, r = 21;
        document.write(countIntegers(l, r));

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
3
```