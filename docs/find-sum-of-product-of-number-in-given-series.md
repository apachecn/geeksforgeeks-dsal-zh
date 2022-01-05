# 求给定数列中数的乘积之和

> 原文:[https://www . geesforgeks . org/find-给定系列中产品数量的总和/](https://www.geeksforgeeks.org/find-sum-of-product-of-number-in-given-series/)

给定两个数字 **N** 和 **T** 其中，![1\leq N\leq 10000000000  ](img/6deee27813101142ee0c4249c70b53b3.png "Rendered by QuickLaTeX.com")和![1\leq T \leq 1000  ](img/13362d17bd06cfe6c8fb5df56344bd39.png "Rendered by QuickLaTeX.com")。任务是找到![sum = \sum_{i=1}^{i=N}\prod_{j=1}^{j=T} (i+j)  ](img/31b780adc2441e070357427360891195.png "Rendered by QuickLaTeX.com")的价值。
由于和可以很大，以 **10 <sup>9</sup> +7** 为模输出。
**示例:**

```
Input : 3 2
Output : 38
2*3 + 3*4 + 4*5 = 38

Input : 4 2
Output : 68
```

> 在给定的样本情况下 **n = 3** 和 **t = 2** 。
> 总和= **2*3+3*4+4*5** 。
> 注意:
> ![1*2 = \frac{2!}{0!}  ](img/348457ea81bc1cb622d641d45530d316.png "Rendered by QuickLaTeX.com")
> ![2*3 = \frac{3!}{1!}  ](img/215700f161b89285eaaf36d5fbccc769.png "Rendered by QuickLaTeX.com")
> ![3*4 = \frac{4!}{2!}  ](img/222819535461118f4dc8d95a43d36ce5.png "Rendered by QuickLaTeX.com")
> ![4*5 = \frac{5!}{3!} ](img/2ca6e66b47ebf9f52f43012d86400714.png "Rendered by QuickLaTeX.com")

所以如果我们用 **t 乘和除，每个项都是![\frac{x!}{(x-t)!}  ](img/d16d82c650f73b5c40a13f26aa412cb2.png "Rendered by QuickLaTeX.com")
的形式！**就变成了![t!*\frac{x!}{(x-t)!*t!}  ](img/d50ee086d7e79d4dfa49d25b3591f097.png "Rendered by QuickLaTeX.com")
这无非就是![t!*\;_{t}^{x}\textrm{C}  ](img/c3d0958151a2cf1bc77d17708e8668aa.png "Rendered by QuickLaTeX.com")
所以，![sum = t!\;*\;\sum_{x=t+1}^{n+t}\; _{t}^{x}\textrm{C}  ](img/7f327f0863d6bd9853fba6ad1b788d69.png "Rendered by QuickLaTeX.com")
但是我们知道![\sum_{x=t}^{N}\;_{t}^{x}\textrm{C}\;=\;_{t+1}^{N+1}\textrm{C}  ](img/649a6a19cbee3a2c230410da8f988b5a.png "Rendered by QuickLaTeX.com")
所以![\sum_{x=t+1}^{n+t} _{k}^{x}\textrm{C}\; =\; _{t+1}^{n+t+1}\textrm{C}-1  ](img/8997c90008701094befbb8ecc85e0b93.png "Rendered by QuickLaTeX.com")
所以最终的表达式出来就是![t!*\;_{t+1}^{n+t+1}\textrm{C}-t!  ](img/d70405d9abd915735ed5f9462de1c21e.png "Rendered by QuickLaTeX.com")
但是由于 **n** 那么大我们不能直接计算出来，我们就要把上面的表达式简化一下。
关于简化，我们得到![\frac{\prod_{i=1}^{t+1}*(n+i)}{t+1} - t!  ](img/8d57d0b6b0beefb136d942579aa19892.png "Rendered by QuickLaTeX.com")。
以下是上述办法的实施情况

## C++

```
// C++ program to find sum of product
// of number in given series
#include <bits/stdc++.h>
using namespace std;

typedef long long ll;
const long long MOD = 1000000007;

// function to calculate (a^b)%p
ll power(ll x, unsigned long long y, ll p)
{
    ll res = 1; // Initialize result

    // Update x if it is more than or equal to p
    x = x % p;

    while (y > 0) {

        // If y is odd, multiply x with result
        if (y & 1)
            res = (res * x) % p;

        // y must be even now
        y = y >> 1; // y = y/2
        x = (x * x) % p;
    }

    return res;
}

// function to return required answer
ll sumProd(ll n, ll t)
{
    // modulo inverse of denominator
    ll dino = power(t + 1, MOD - 2, MOD);

    // calculating commentator part
    unsigned long long ans = 1;
    for (ll i = n + t + 1; i > n; --i)
        ans = (ans % MOD * i % MOD) % MOD;

    // calculating t!
    ll tfact = 1;
    for (int i = 1; i <= t; ++i)
        tfact = (tfact * i) % MOD;

    // accumulating the final answer
    ans = ans * dino - tfact + MOD;

    return ans % MOD;
}
int main()
{
    ll n = 3, t = 2;

    // function call to print required sum
    cout << sumProd(n, t);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of product
// of number in given series

public class GFG {

     static long MOD = 1000000007;

    //function to calculate (a^b)%p
     static long power(long x, long y, long p)
     {
      long res = 1; // Initialize result

      // Update x if it is more than or equal to p
      x = x % p;

      while (y > 0) {

          // If y is odd, multiply x with result
          if ((y & 1)!= 0)
              res = (res * x) % p;

          // y must be even now
          y = y >> 1; // y = y/2
          x = (x * x) % p;
      }

      return res;
     }

     //function to return required answer
     static long sumProd(long n, long t)
     {
      // modulo inverse of denominator
      long dino = power(t + 1, MOD - 2, MOD);

      // calculating commentator part
      long ans = 1;
      for (long i = n + t + 1; i > n; --i)
          ans = (ans % MOD * i % MOD) % MOD;

      // calculating t!
      long tfact = 1;
      for (int i = 1; i <= t; ++i)
          tfact = (tfact * i) % MOD;

      // accumulating the final answer
      ans = ans * dino - tfact + MOD;

      return ans % MOD;
     }

     // Driver program
    public static void main(String[] args) {

        long n = 3, t = 2;

         // function call to print required sum
         System.out.println(sumProd(n, t));
    }
}
```

## 蟒蛇 3

```
# Python 3 program to find sum of product
# of number in given series

MOD = 1000000007

# function to calculate (a^b)%p
def power(x, y, p) :

    # Initialize result
    res = 1

    # Update x if it is more than or equal to p
    x = x % p

    # If y is odd, multiply x with result
    while y > 0 :

        if y & 1 :
            res = (res * x) % p

        #  y must be even now
        y = y >> 1 # y = y/2
        x = (x * x) % p

    return res

# function to return required answer
def sumProd(n, t) :

    # modulo inverse of denominator
    dino = power(t + 1, MOD - 2, MOD)

    ans = 1

    # calculating commentator part
    for i in range(n + t + 1 , n, -1) :
        ans = (ans % MOD * i % MOD) % MOD

    # calculating t!
    tfact = 1
    for i in range(1, t+1) :
        tfact = (tfact * i) % MOD

    # accumulating the final answer
    ans = ans * dino - tfact + MOD

    return ans % MOD

# Driver Code
if __name__ == "__main__" :

    n, t = 3, 2

    # function call to print required sum
    print(sumProd(n, t))

# This code is contributed by ANKITRAI1
```

## C#

```
// C# program to find sum of product
// of number in given series
using System;
class GFG
{
static long MOD = 1000000007;

// function to calculate (a^b)%p
static long power(long x, long y,
                  long p)
{
    long res = 1; // Initialize result

    // Update x if it is more
    // than or equal to p
    x = x % p;

    while (y > 0)
    {

        // If y is odd, multiply x
        // with result
        if ((y & 1) != 0)
            res = (res * x) % p;

        // y must be even now
        y = y >> 1; // y = y/2
        x = (x * x) % p;
    }

    return res;
}

// function to return required answer
static long sumProd(long n, long t)
{

// modulo inverse of denominator
long dino = power(t + 1, MOD - 2, MOD);

// calculating commentator part
long ans = 1;
for (long i = n + t + 1; i > n; --i)
    ans = (ans % MOD * i % MOD) % MOD;

// calculating t!
long tfact = 1;
for (int i = 1; i <= t; ++i)
    tfact = (tfact * i) % MOD;

// accumulating the final answer
ans = ans * dino - tfact + MOD;

return ans % MOD;
}

// Driver Code
public static void Main()
{
    long n = 3, t = 2;

    // function call to print required sum
    Console.WriteLine(sumProd(n, t));
}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find sum of product
// of number in given series

// function to calculate (a^b)%p
function power($x, $y, $p)
{
    $res = 1; // Initialize result

    // Update x if it is more
    // than or equal to p
    $x = $x % $p;

    while ($y > 0)
    {

        // If y is odd, multiply
        // x with result
        if ($y & 1)
            $res = ($res * $x) % $p;

        // y must be even now
        $y = $y >> 1; // y = y/2
        $x = ($x * $x) % $p;
    }

    return $res;
}

// function to return required answer
function sumProd($n, $t)
{
    $MOD = 1000000007;

    // modulo inverse of denominator
    $dino = power($t + 1, $MOD - 2, $MOD);

    // calculating commentator part
    $ans = 1;
    for ($i = $n + $t + 1; $i > $n; --$i)
        $ans = ($ans % $MOD * $i %
                       $MOD) % $MOD;

    // calculating t!
    $tfact = 1;
    for ($i = 1; $i <= $t; ++$i)
        $tfact = ($tfact * $i) % $MOD;

    // accumulating the final answer
    $ans = $ans * $dino - $tfact + $MOD;

    return $ans % $MOD;
}

// Driver code
$n = 3;
$t = 2;

// function call to print
// required sum
echo sumProd($n, $t);

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

// Javascript program to find sum of product
// of number in given series
var MOD = 100000007;

// function to calculate (a^b)%p
function power(x, y, p)
{
    var res = 1; // Initialize result

    // Update x if it is more than or equal to p
    x = x % p;

    while (y > 0) {

        // If y is odd, multiply x with result
        if (y & 1)
            res = (res * x) % p;

        // y must be even now
        y = y >> 1; // y = y/2
        x = (x * x) % p;
    }

    return res;
}

// function to return required answer
function sumProd(n, t)
{
    // modulo inverse of denominator
    var dino = power(t + 1, MOD - 2, MOD);

    // calculating commentator part
    var ans = 1;
    for (var i = n + t + 1; i > n; --i)
        ans = (ans % MOD * i % MOD) % MOD;

    // calculating t!
    var tfact = 1;
    for (var i = 1; i <= t; ++i)
        tfact = (tfact * i) % MOD;

    // accumulating the final answer
    ans = ans * dino - tfact + MOD;

    return ans % MOD;
}

var n = 3, t = 2;
// function call to print required sum
document.write( sumProd(n, t));

// This code is contributed by noob2000.
</script>
```

**输出:**

```
38
```

**时间复杂度:** O(T)