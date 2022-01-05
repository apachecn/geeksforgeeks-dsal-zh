# 表示为字符串的大数的模幂

> 原文:[https://www . geeksforgeeks . org/大数模幂-表示为字符串/](https://www.geeksforgeeks.org/modulo-power-for-large-numbers-represented-as-strings/)

给定两个表示为字符串的数字 **sa** 和 **sb** ，找到一个 <sup>b</sup> % MOD，其中 MOD 为 1e9 + 7。数字 a 和 b 最多可包含 10 个<sup>和 6 个</sup>数字。
**举例:**

> 输入:sa = 2，sb = 3
> 输出:8
> 输入:sa = 100000000000000000000000000000000000000000
> sb = 1000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000

因为 **a** 和 **b** 非常大(每个最多可包含 10^6 数字)。所以我们能做的，就是应用[费马小定理](https://www.geeksforgeeks.org/fermats-little-theorem/)和模的性质来约简 **a** 和 **b** 。
**减一:**
众所周知，

```
(ab) % MOD = ((a % MOD)b) % MOD
```

**减少 b:**
如何减少 **b** ，我们已经在[中讨论过了 Find (a^b)%m 这里的‘b’很大](https://www.geeksforgeeks.org/find-abm-where-b-is-very-large/)
现在终于我们既有 **a** 又有 **b** 都在 1 <的范围内=a，b < =10^9+7.因此，我们现在可以使用模幂运算来计算所需的答案。

## C++

```
// CPP program to find (a^b) % MOD where a and
// b may be very large and represented as strings.
#include <bits/stdc++.h>
using namespace std;

#define ll long long int
const ll MOD = 1e9 + 7;

// Returns modulo exponentiation for two numbers
// represented as long long int. It is used by
// powerStrings(). Its complexity is log(n)
ll powerLL(ll x, ll n)
{
    ll result = 1;
    while (n) {
        if (n & 1)
            result = result * x % MOD;
        n = n / 2;
        x = x * x % MOD;
    }
    return result;
}

// Returns modulo exponentiation for two numbers
// represented as strings. It is used by
// powerStrings()
ll powerStrings(string sa, string sb)
{
    // We convert strings to number

    ll a = 0, b = 0;

    // calculating  a % MOD
    for (int i = 0; i < sa.length(); i++)
        a = (a * 10 + (sa[i] - '0')) % MOD;

    // calculating  b % (MOD - 1)
    for (int i = 0; i < sb.length(); i++)
        b = (b * 10 + (sb[i] - '0')) % (MOD - 1);

    // Now a and b are long long int. We
    // calculate a^b using modulo exponentiation
    return powerLL(a, b);
}

int main()
{
    // As numbers are very large
    // that is it may contains upto
    // 10^6 digits. So, we use string.
    string sa = "2", sb = "3";

    cout << powerStrings(sa, sb) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find (a^b) % MOD
// where a and b may be very large
// and represented as strings.
import java.util.*;

class GFG
{

    static long MOD = (long) (1e9 + 7);

    // Returns modulo exponentiation for two numbers
    // represented as long long int. It is used by
    // powerStrings(). Its complexity is log(n)
    static long powerLL(long x, long n)
    {
        long result = 1;
        while (n > 0)
        {
            if (n % 2 == 1)
            {
                result = result * x % MOD;
            }
            n = n / 2;
            x = x * x % MOD;
        }
        return result;
    }

    // Returns modulo exponentiation for
    // two numbers  represented as strings. 
    // It is used by powerStrings()
    static long powerStrings(String sa, String sb)
    {
        // We convert strings to number
        long a = 0, b = 0;

        // calculating a % MOD
        for (int i = 0; i < sa.length(); i++)
        {
            a = (a * 10 + (sa.charAt(i) - '0')) %
                                               MOD;
        }

        // calculating b % (MOD - 1)
        for (int i = 0; i < sb.length(); i++)
        {
            b = (b * 10 + (sb.charAt(i) - '0')) %
                                        (MOD - 1);
        }

        // Now a and b are long long int. We
        // calculate a^b using modulo exponentiation
        return powerLL(a, b);
    }

    // Driver code
    public static void main(String[] args)
    {

        // As numbers are very large
        // that is it may contains upto
        // 10^6 digits. So, we use string.
        String sa = "2", sb = "3";
        System.out.println(powerStrings(sa, sb));
    }
}

// This code is contributed by Rajput-JI
```

## 蟒蛇 3

```
# Python3 program to find (a^b) % MOD
# where a and b may be very large
# and represented as strings.
MOD = 1000000007;

# Returns modulo exponentiation
# for two numbers represented as
# long long int. It is used by
# powerStrings(). Its complexity
# is log(n)
def powerLL(x, n):

    result = 1;
    while (n):
        if (n & 1):
            result = result * x % MOD;
        n = int(n / 2);
        x = x * x % MOD;
    return result;

# Returns modulo exponentiation
# for two numbers represented as
# strings. It is used by powerStrings()
def powerStrings(sa, sb):

    # We convert strings to number
    a = 0;
    b = 0;

    # calculating a % MOD
    for i in range(len(sa)):
        a = (a * 10 + (ord(sa[i]) -
                       ord('0'))) % MOD;

    # calculating b % (MOD - 1)
    for i in range(len(sb)):
        b = (b * 10 + (ord(sb[i]) -
                       ord('0'))) % (MOD - 1);

    # Now a and b are long long int.
    # We calculate a^b using modulo
    # exponentiation
    return powerLL(a, b);

# Driver code

# As numbers are very large
# that is it may contains upto
# 10^6 digits. So, we use string.
sa = "2";
sb = "3";

print(powerStrings(sa, sb));

# This code is contributed by mits
```

## C#

```
// C# program to find (a^b) % MOD where a and b 
// may be very large and represented as strings.
using System;

class GFG
{
    static long MOD = (long) (1e9 + 7);

    // Returns modulo exponentiation for two numbers
    // represented as long long int. It is used by
    // powerStrings(). Its complexity is log(n)
    static long powerLL(long x, long n)
    {
        long result = 1;
        while (n > 0)
        {
            if (n % 2 == 1)
            {
                result = result * x % MOD;
            }
            n = n / 2;
            x = x * x % MOD;
        }
        return result;
    }

    // Returns modulo exponentiation for
    // two numbers represented as strings.
    // It is used by powerStrings()
    static long powerStrings(String sa, String sb)
    {
        // We convert strings to number
        long a = 0, b = 0;

        // calculating a % MOD
        for (int i = 0; i < sa.Length; i++)
        {
            a = (a * 10 + (sa[i] - '0')) % MOD;
        }

        // calculating b % (MOD - 1)
        for (int i = 0; i < sb.Length; i++)
        {
            b = (b * 10 + (sb[i] - '0')) % (MOD - 1);
        }

        // Now a and b are long long int. We
        // calculate a^b using modulo exponentiation
        return powerLL(a, b);
    }

    // Driver code
    public static void Main(String[] args)
    {

        // As numbers are very large
        // that is it may contains upto
        // 10^6 digits. So, we use string.
        String sa = "2", sb = "3";
        Console.WriteLine(powerStrings(sa, sb));
    }
}

// This code is contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find (a^b) % MOD
// where a and b may be very large
// and represented as strings.
$MOD = 1000000007;

// Returns modulo exponentiation
// for two numbers represented as
// long long int. It is used by
// powerStrings(). Its complexity
// is log(n)
function powerLL($x, $n)
{
    global $MOD;
    $result = 1;
    while ($n)
    {
        if ($n & 1)
            $result = $result * $x % $MOD;
        $n = (int)$n / 2;
        $x = $x * $x % $MOD;
    }
    return $result;
}

// Returns modulo exponentiation
// for two numbers represented as
// strings. It is used by powerStrings()
function powerStrings($sa, $sb)
{
    global $MOD;

    // We convert strings to number
    $a = 0;
    $b = 0;

    // calculating a % MOD
    for ($i = 0; $i < strlen($sa); $i++)
        $a = ($a * 10 + ($sa[$i] -
                     '0')) % $MOD;

    // calculating b % (MOD - 1)
    for ($i = 0; $i < strlen($sb); $i++)
        $b = ($b * 10 + ($sb[$i] - '0')) %
                        ($MOD - 1);

    // Now a and b are long long int.
    // We calculate a^b using modulo
    // exponentiation
    return powerLL($a, $b);
}

// Driver code

// As numbers are very large
// that is it may contains upto
// 10^6 digits. So, we use string.
$sa = "2";
$sb = "3";

echo powerStrings($sa, $sb);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to find (a^b) % MOD where a and b 
// may be very large and represented as strings. 

let MOD = (1e9 + 7);

    // Returns modulo exponentiation for two numbers
    // represented as long long let. It is used by
    // powerStrings(). Its complexity is log(n)
    function powerLL(x, n)
    {
        let result = 1;
        while (n > 0)
        {
            if (n % 2 == 1)
            {
                result = result * x % MOD;
            }
            n = Math.floor(n / 2);
            x = x * x % MOD;
        }
        return result;
    }

    // Returns modulo exponentiation for
    // two numbers represented as strings.
    // It is used by powerStrings()
    function powerStrings(sa, sb)
    {
        // We convert strings to number
        let a = 0, b = 0;

        // calculating a % MOD
        for (let i = 0; i < sa.length; i++)
        {
            a = (a * 10 + (sa[i] - '0')) % MOD;
        }

        // calculating b % (MOD - 1)
        for (let i = 0; i < sb.length; i++)
        {
            b = (b * 10 + (sb[i] - '0')) % (MOD - 1);
        }

        // Now a and b are long long let. We
        // calculate a^b using modulo exponentiation
        return powerLL(a, b);
    }

// Driver Code

         // As numbers are very large
        // that is it may contains upto
        // 10^6 digits. So, we use string.
        let sa = "2", sb = "3";
        document.write(powerStrings(sa, sb));

</script>
```

**Output:** 

```
8
```