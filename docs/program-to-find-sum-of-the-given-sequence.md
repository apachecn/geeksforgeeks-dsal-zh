# 程序求给定序列的和

> 原文:[https://www . geesforgeks . org/program-to-find-sum-of-the-sequence/](https://www.geeksforgeeks.org/program-to-find-sum-of-the-given-sequence/)

给定两个数字![N  ](img/05447a6f3ec73065b361522074101320.png "Rendered by QuickLaTeX.com")和![K  ](img/aa076c3d3015a34419fb7cfa4831a2ac.png "Rendered by QuickLaTeX.com")。任务是找出下面给出的序列的和。

> **(1 * 2 * 3 *……* k)+(2 * 3 *……* k *(k+1))+(3 * 4 *..*(k+1)*(k+2)) +…..+((n-k+1)*(n-k+2)*……*(n-k+k))。**

由于输出可能很大，请在模 10^9+7.下打印答案
**例** :

```
Input : N = 3, K = 2
Output : 8

Input : N = 4, K = 2
Output : 20
```

让我们举一个例子，试着把它简化成一个通式。
在给定的例子中 **n = 3** 和 **k=2** ，

```
Sum = 1*2 + 2*3 
```

我们知道:
![$1\times2=2!\times 0!$\\ $2\times3=3!\times1!$\\  ](img/748d9acb1328cc27eea8c7dc42fa6fe0.png "Rendered by QuickLaTeX.com")
所以每个术语都是这样的形式:

![$\frac{x!}{\left(x-k\right)!}$  ](img/1d5a22ec516034805f69b5afc8e5a6b1.png "Rendered by QuickLaTeX.com")

如果我们乘和除![k!  ](img/1a94625d8f6df4a9c6cfbef5af1c15c9.png "Rendered by QuickLaTeX.com")，它就变成了

![$k!\cdot\frac{x!}{\left(x-k\right)!\cdot k!}$  ](img/def23e81a7e0e075a2b63bfba8695df5.png "Rendered by QuickLaTeX.com")

其中无非是，
![$k!\times$ ${N}\choose{k}$\\  ](img/0d6f16a8b03a796fc56be6fed6f31384.png "Rendered by QuickLaTeX.com")
所以，
![sum = $k\times \sum_{x=k}^{n}$ $ {x}\choose{k}$ =$ {n+1}\choose{k+1}$ $\times k! $\\  ](img/1cf78a4cd2ffa649ac6f533f19282791.png "Rendered by QuickLaTeX.com")
但是既然 n 这么大我们不能直接算出来，只好简化上面的表达式。
关于简化，我们得到:

![$\frac{\left(n\right) \cdot \left(n-1\right) \cdot \left(n-2\right) \dots \left(n-k+1\right)}{k+1}$  ](img/a3ebdba5308162210bb4371fa6214d6c.png "Rendered by QuickLaTeX.com")

以下是上述思路的实现:

## C++

```
// CPP program to find the sum of the
// given sequence

#include <bits/stdc++.h>
using namespace std;

const long long MOD = 1000000007;

// function to find moudulo inverse
// under 10^9+7
long long modInv(long long x)
{
    long long n = MOD - 2;
    long long result = 1;
    while (n) {
        if (n & 1)
            result = result * x % MOD;
        x = x * x % MOD;
        n = n / 2;
    }

    return result;
}

// Function to find the sum of the
// given sequence
long long getSum(long long n, long long k)
{
    long long ans = 1;

    for (long long i = n + 1; i > n - k; i--)
        ans = ans * i % MOD;
    ans = ans * modInv(k + 1) % MOD;

    return ans;
}

// Driver code
int main()
{
    long long n = 3, k = 2;

    cout<<getSum(n,k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the sum of the
// given sequence

class GFG {

    static long MOD = 1000000007;

// function to find moudulo inverse
// under 10^9+7
    static long modInv(long x) {
        long n = MOD - 2;
        long result = 1;
        while (n > 0) {
            if ((n & 1) > 0) {
                result = result * x % MOD;
            }
            x = x * x % MOD;
            n = n / 2;
        }

        return result;
    }

// Function to find the sum of the
// given sequence
    static long getSum(long n, long k) {
        long ans = 1;

        for (long i = n + 1; i > n - k; i--) {
            ans = ans * i % MOD;
        }
        ans = ans * modInv(k + 1) % MOD;

        return ans;
    }

// Driver code
    public static void main(String[] args) {
        long n = 3, k = 2;
        System.out.println(getSum(n, k));
    }
}
```

## 蟒蛇 3

```
# Python3 program to find the sum
# of the given sequence

MOD = 1000000007;

# function to find moudulo inverse
# under 10^9+7
def modInv(x):

    n = MOD - 2;
    result = 1;
    while (n):
        if (n&1):
            result = result * x % MOD;
        x = x * x % MOD;
        n = int(n / 2);

    return result;

# Function to find the sum of
# the given sequence
def getSum(n, k):

    ans = 1;

    for i in range(n + 1, n - k, -1):
        ans = ans * i % MOD;
    ans = ans * modInv(k + 1) % MOD;

    return ans;

# Driver code
n = 3;
k = 2;

print(getSum(n,k));

# This code is contributed by mits
```

## C#

```
// C# program to find the sum of the
// given sequence
using System;

// function to find moudulo inverse
// under 10^9+7
class gfg
{
    public long MOD = 1000000007;
 public long modInv(long x)
 {
    long n = MOD - 2;
    long result = 1;
    while (n >0) {
        if ((n & 1) > 0)
            result = result * x % MOD;
        x = x * x % MOD;
        n = n / 2;
    }

    return result;
}

// Function to find the sum of the
// given sequence
  public long getSum(long n, long k)
  {
    long ans = 1;

    for (long i = n + 1; i > n - k; i--)
        ans = ans * i % MOD;
    ans = ans * modInv(k + 1) % MOD;

    return ans;
 }
}

// Driver code
class geek
{
  public static int Main()
 {
     gfg g = new gfg();
    long n = 3, k = 2;

    Console.WriteLine(g.getSum(n,k));

    return 0;
 }
}
//This code is contributed by SoumikMondal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the sum of
// the given sequence

// function to find moudulo inverse
// under 10^9+7
function modInv($x)
{
    $MOD = 1000000007;
    $n = $MOD - 2;
    $result = 1;
    while ($n)
    {
        if ($n & 1)
            $result = $result * $x % $MOD;
        $x = $x * $x % $MOD;
        $n = $n / 2;
    }

    return $result;
}

// Function to find the sum of the
// given sequence
function getSum($n, $k)
{
    $MOD = 1000000007;
    $ans = 1;

    for ($i = $n + 1; $i > $n - $k; $i--)
        $ans = $ans * $i % $MOD;
    $ans = $ans * modInv($k + 1) % $MOD;

    return $ans;
}

// Driver code
$n = 3; $k = 2;

echo getSum($n, $k);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// Javascript program to find the sum of the
// given sequence

var MOD = 100000007;

// function to find moudulo inverse
// under 10^9+7
function modInv(x)
{
    var n = MOD - 2;
    var result = 1;
    while (n) {
        if (n & 1)
            result = result * x % MOD;
        x = x * x % MOD;
        n = n / 2;
    }

    return result;
}

// Function to find the sum of the
// given sequence
function getSum(n, k)
{
    var ans = 1;

    for (var i = n + 1; i > n - k; i--)
        ans = ans * i % MOD;
    ans = ans * modInv(k + 1) % MOD;

    return ans;
}

// Driver code
var n = 3, k = 2;

document.write( getSum(n,k));

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
8
```