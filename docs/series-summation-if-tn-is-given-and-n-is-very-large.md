# 给定 T(n)且 n 很大时的级数求和

> 原文:[https://www . geesforgeks . org/series-summary-if-TN-is-give-and-n-is-非常大/](https://www.geeksforgeeks.org/series-summation-if-tn-is-given-and-n-is-very-large/)

给定一个序列，它的第 n 个术语是

> t(n)= n<sup>2</sup>–(n–1)<sup>2</sup>

任务是评估前 n 项之和，即

> S(n) = T(1) + T(2) + T(3) + … + T(n)

打印 **S(n) mod (10 <sup>9</sup> + 7)** 。
**例:**

> **输入:** n = 3
> **输出:**9
> S(3)= T(1)+T(2)+T(3)=(1<sup>2</sup>–0<sup>2</sup>)+(2<sup>2</sup>–1<sup>2</sup>)+(3<sup>2</sup>–2<sup>2</sup>)= 1+3+5 = 9

**方法:**如果我们试图通过将 **n = 1，2，3，…** 放入**T(n)= n<sup>2</sup>–(n–1)<sup>2</sup>**来找出序列的一些初始项，我们会找到序列 **1，3，5，…**
因此，我们会找到一个 A.P .其中**第一项**是 **1** 和

A . P 的 n 项之和的公式为

> s(n)= n/2[2 * a+(n–1)* d]

其中**一**是第一个名词。
所以，放 **a = 1** 和 **d = 2** ，我们得到

> S(n) = n <sup>2</sup>

。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define ll long long int
#define MOD 1000000007

// Function to return the sum
// of the given series
int sumOfSeries(int n)
{
    ll ans = (ll)pow(n % MOD, 2);

    return (ans % MOD);
}

// Driver code
int main()
{
    int n = 10;
    cout << sumOfSeries(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

public static final int MOD = 1000000007;

// Function to return the sum
// of the given series
static int sumOfSeries(int n)
{
    int ans = (int)Math.pow(n % MOD, 2);

    return (ans % MOD);
}

// Driver code
public static void main(String[] args)
{
    int n = 10;
    System.out.println(sumOfSeries(n));
}
}

// This code is contributed by Code_Mech.
```

## 蟒蛇 3

```
# Python 3 implementation of the approach
from math import pow

MOD = 1000000007

# Function to return the sum
# of the given series
def sumOfSeries(n):
    ans = pow(n % MOD, 2)

    return (ans % MOD)

# Driver code
if __name__ == '__main__':
    n = 10
    print(int(sumOfSeries(n)))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

const int MOD = 1000000007;

// Function to return the sum
// of the given series
static int sumOfSeries(int n)
{
    int ans = (int)Math.Pow(n % MOD, 2);

    return (ans % MOD);
}

// Driver code
public static void Main()
{
    int n = 10;
    Console.Write(sumOfSeries(n));
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach
$GLOBALS['MOD'] = 1000000007;

// Function to return the sum
// of the given series
function sumOfSeries($n)
{
    $ans = pow($n % $GLOBALS['MOD'], 2);

    return ($ans % $GLOBALS['MOD']);
}

// Driver code
$n = 10;
echo sumOfSeries($n);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// javascript program for the above approach

let MOD = 1000000007;

// Function to return the sum
// of the given series
function sumOfSeries(n)
{
    let ans = Math.pow(n % MOD, 2);

    return (ans % MOD);
}

// Driver Code

        let n = 10;
    document.write(sumOfSeries(n));

</script>
```

**Output:** 

```
100
```