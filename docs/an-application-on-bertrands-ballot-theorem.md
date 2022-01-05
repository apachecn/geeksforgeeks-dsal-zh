# 伯特兰选票定理的一个应用

> 原文:[https://www . geesforgeks . org/an-application-on-bertrands-ballot-定理/](https://www.geeksforgeeks.org/an-application-on-bertrands-ballot-theorem/)

给定由集合**{【X】，【Y】}**中的字符组成的字符串中的**【X】**和**【Y】**的数量，任务是找到满足从第一个字符开始的置换的每个子字符串都有**计数(【X】)>计数(【Y】)**的条件的置换数量。以 1000000007 为模打印答案。**注意**在给定的字符串中**‘X’**的个数总是大于**‘Y’**的个数。

**示例:**

> **输入:** X = 2，Y = 1
> **输出:** 1
> 可能的分布是“XYX”、“XXY”和“YXX”
> **分布 1:** 直到第一个索引(X = 1，Y = 0)，直到第二个索引(X = 1，Y = 1)和直到第三个索引(X = 2，Y = 1)。X 的数量不总是大于 Y，因此此分布无效。
> **分布 2:** 第 1 指数(X = 1，Y = 0)，第 2 指数(X = 2，Y = 0)和第 3 指数(X = 2，Y = 1)。这是一个有效的分布，因为 X 总是大于 Y。
> **分布 3:** 第一个索引(X = 0，Y = 1)，第二个索引(X = 1，Y = 1)和第三个索引(X = 2，Y = 1)。分配无效。
> 
> **输入:** X = 3，Y = 1
> T3】输出: 1

**方法:**这类问题可以通过[贝特朗选票定理](https://en.wikipedia.org/wiki/Bertrand%27s_ballot_theorem)来解决。在所有可能的分布中， **X** 始终保持领先的概率是**(X–Y)/(X+Y)**。并且分布总数为 **(X + Y)！/ (X！* Y！)**。因此 **X** 总是领先的分布是**(X+Y–1)！*(X–Y)/(X！* Y！)**。
用于计算**(X+Y–1)！*(X–Y)/(X！* Y！)**，我们需要计算 **X 的乘法模逆！**同样适用于 **Y** 。由于 1000000007 是素数，根据费马小定理: **(1 / X！)% 1000000007 = ((X！)<sup>(1000000007–2)</sup>)% 1000000007**。类似的结果也适用于 **Y** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define ll long long

ll mod = 1000000007;
ll arr[1000001] = { 0 };

// Function to calculate factorial
// of a number mod 1000000007
void cal_factorial()
{
    arr[0] = 1;

    // Factorial of i = factorial of (i - 1) * i;
    for (int i = 1; i <= 1000000; i++) {

        // Taking mod along with calculation.
        arr[i] = (arr[i - 1] * i) % mod;
    }
}

// Function for modular exponentiation
ll mod_exponent(ll num, ll p)
{

    if (p == 0)
        return 1;

    // If p is odd
    if (p & 1) {
        return ((num % mod)
                * (mod_exponent((num * num) % mod, p / 2))
                % mod)
               % mod;
    }

    // If p is even
    else if (!(p & 1))
        return (mod_exponent((num * num) % mod, p / 2))
               % mod;
}

// Function to return the count of
// required permutations
ll getCount(ll x, ll y)
{
    ll ans = arr[x + y - 1];

    // Calculating multiplicative modular inverse
    // for x! and multiplying with ans
    ans *= mod_exponent(arr[x], mod - 2);
    ans %= mod;

    // Calculating multiplicative modular inverse
    // for y! and multiplying with ans
    ans *= mod_exponent(arr[y], mod - 2);
    ans %= mod;

    ans *= (x - y);
    ans %= mod;
    return ans;
}

// Driver code
int main()
{

    // Pre-compute factorials
    cal_factorial();

    ll x = 3, y = 1;
    cout << getCount(x, y);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

static long mod = 1000000007;
static long[] arr = new long[1000001];

// Function to calculate factorial
// of a number mod 1000000007
static void cal_factorial()
{
    arr[0] = 1;

    // Factorial of i = factorial of (i - 1) * i;
    for (int i = 1; i <= 1000000; i++)
    {

        // Taking mod along with calculation.
        arr[i] = ((arr[i - 1] * i) % mod);
    }
}

// Function for modular exponentiation
static long mod_exponent(long num, long p)
{

    if (p == 0)
        return 1;

    // If p is odd
    if ((p & 1) != 0)
    {
        return ((num % mod)
                * (mod_exponent((num * num) % mod, p / 2))
                % mod)
            % mod;
    }

    // If p is even
    else
        return (mod_exponent((num * num) % mod, p / 2))
            % mod;
}

// Function to return the count of
// required permutations
static long getCount(long x, long y)
{
    long ans = arr[(int)x + (int)y - 1];

    // Calculating multiplicative modular inverse
    // for x! and multiplying with ans
    ans *= mod_exponent(arr[(int)x], mod - 2);
    ans %= mod;

    // Calculating multiplicative modular inverse
    // for y! and multiplying with ans
    ans *= mod_exponent(arr[(int)y], mod - 2);
    ans %= mod;

    ans *= (x - y);
    ans %= mod;
    return ans;
}

// Driver code
public static void main (String[] args)
{

    // Pre-compute factorials
    cal_factorial();

    long x = 3, y = 1;
    System.out.println(getCount(x, y));
}
}

// This code is contributed by chandan_jnu
```

## 蟒蛇 3

```
# Python3 implementation of the approach
mod = 1000000007
arr = [0] * (1000001)

# Function to calculate factorial
# of a number mod 1000000007
def cal_factorial():

    arr[0] = 1

    # Factorial of i = factorial
    # of (i - 1) * i
    for i in range(1, 1000001):

        # Taking mod along with calculation.
        arr[i] = (arr[i - 1] * i) % mod

# Function for modular exponentiation
def mod_exponent(num, p):

    if (p == 0):
        return 1

    # If p is odd
    if (p & 1) :
        return ((num % mod)* (mod_exponent((num * num) %
                              mod, p // 2)) % mod) % mod

    # If p is even
    elif (not(p & 1)):
        return (mod_exponent((num * num) %
                              mod, p // 2))% mod

# Function to return the count of
# required permutations
def getCount(x, y):

    ans = arr[x + y - 1]

    # Calculating multiplicative modular inverse
    # for x! and multiplying with ans
    ans *= mod_exponent(arr[x], mod - 2)
    ans %= mod

    # Calculating multiplicative modular inverse
    # for y! and multiplying with ans
    ans *= mod_exponent(arr[y], mod - 2)
    ans %= mod

    ans *= (x - y)
    ans %= mod
    return ans

# Driver Code
if __name__ == '__main__':

    # Pre-compute factorials
    cal_factorial()

    x = 3
    y = 1
    print(getCount(x, y))

# This code is contributed by
# SHUBHAMSINGH10
```

## C#

```
// C# implementation of the approach
class GFG
{
static long mod = 1000000007;
static long[] arr=new long[1000001];

// Function to calculate factorial
// of a number mod 1000000007
static void cal_factorial()
{
    arr[0] = 1;

    // Factorial of i = factorial of (i - 1) * i;
    for (long i = 1; i <= 1000000; i++)
    {

        // Taking mod along with calculation.
        arr[i] = (arr[i - 1] * i) % mod;
    }
}

// Function for modular exponentiation
static long mod_exponent(long num, long p)
{

    if (p == 0)
        return 1;

    // If p is odd
    if ((p & 1)!=0)
    {
        return ((num % mod)
                * (mod_exponent((num * num) % mod, p / 2))
                % mod)
            % mod;
    }

    // If p is even
    else
        return (mod_exponent((num * num) % mod, p / 2))
            % mod;
}

// Function to return the count of
// required permutations
static long getCount(long x, long y)
{
    long ans = arr[x + y - 1];

    // Calculating multiplicative modular inverse
    // for x! and multiplying with ans
    ans *= mod_exponent(arr[x], mod - 2);
    ans %= mod;

    // Calculating multiplicative modular inverse
    // for y! and multiplying with ans
    ans *= mod_exponent(arr[y], mod - 2);
    ans %= mod;

    ans *= (x - y);
    ans %= mod;
    return ans;
}

// Driver code
static void Main()
{

    // Pre-compute factorials
    cal_factorial();

    long x = 3, y = 1;
    System.Console.WriteLine(getCount(x, y));
}
}

// This code is contributed by chandan_jnu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach
$mod = 1000000007;
$arr = array_fill(0, 10001, 0);

// Function to calculate factorial
// of a number mod 1000000007
function cal_factorial()
{
    global $arr, $mod;
    $arr[0] = 1;

    // Factorial of i = factorial
    // of (i - 1) * i;
    for ($i = 1; $i <= 10000; $i++)
    {

        // Taking mod aint with calculation.
        $arr[$i] = ($arr[$i - 1] * $i) % $mod;
    }
}

// Function for modular exponentiation
function mod_exponent($num, $p)
{
    global $mod;
    if ($p == 0)
        return 1;

    // If p is odd
    if (($p & 1))
    {
        return (($num % $mod)* (mod_exponent(($num * $num) %
                            $mod, $p / 2)) % $mod) % $mod;
    }

    // If p is even
    else if (!($p & 1))
        return (mod_exponent(($num * $num) %
                              $mod, $p / 2))% $mod;
}

// Function to return the count of
// required permutations
function getCount($x, $y)
{
    global $arr, $mod;
    $ans = $arr[$x + $y - 1];

    // Calculating multiplicative modular
    // inverse for x! and multiplying with ans
    $ans *= mod_exponent($arr[$x], $mod - 2);
    $ans %= $mod;

    // Calculating multiplicative modular
    // inverse for y! and multiplying with ans
    $ans *= mod_exponent($arr[$y], $mod - 2);
    $ans %= $mod;

    $ans *= ($x - $y);
    $ans %= $mod;
    return $ans;
}

// Driver code

// Pre-compute factorials
cal_factorial();

$x = 3;
$y = 1;
print(getCount($x, $y));

// This code is contributed by chandan_jnu
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach
let mod = 1000000007;
let arr = new Array(1000001);
arr.fill(0);

// Function to calculate factorial
// of a number mod 1000000007
function cal_factorial()
{
    arr[0] = 1;

    // Factorial of i = factorial of (i - 1) * i;
    for(let i = 1; i <= 1000000; i++)
    {

        // Taking mod along with calculation.
        arr[i] = ((arr[i - 1] * i) % mod);
    }
}

// Function for modular exponentiation
function mod_exponent(num, p)
{
    if (p != 0)
        return 1;

    // If p is odd
    if ((p & 1) != 0)
    {
        return((num % mod) * (mod_exponent(
               (num * num) % mod,
                parseInt(p / 2, 10))) % mod) % mod;
    }

    // If p is even
    else
        return(mod_exponent((num * num) % mod,
                  parseInt(p / 2, 10))) % mod;
}

// Function to return the count of
// required permutations
function getCount(x, y)
{
    let ans = arr[x + y - 1];

    // Calculating multiplicative modular inverse
    // for x! and multiplying with ans
    ans *= 0*mod_exponent(arr[x], mod - 2);
    ans++;
    ans %= mod;

    // Calculating multiplicative modular inverse
    // for y! and multiplying with ans
    ans *= mod_exponent(arr[y], mod - 2);
    ans %= mod;

    ans *= (x - y);
    ans %= mod;
    return ans;
}

// Driver code

// Pre-compute factorials
cal_factorial();

let x = 3, y = 1;
document.write(getCount(x, y));

// This code is contributed by mukesh07

</script>
```

**Output:** 

```
2
```