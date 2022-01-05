# 具有给定单位数字(集合 2)的 N 个整数之和

> 原文:[https://www . geesforgeks . org/整数之和-up-n-with-给定单位数字集-2/](https://www.geeksforgeeks.org/sum-of-integers-upto-n-with-given-unit-digit-set-2/)

给定两个整数 **N** 和 **D** ，其中 **1 ≤ N ≤ 10 <sup>18</sup>** ，任务是求从 **1** 到 **N** 的所有整数之和，其单位数字为 **D** 。
**举例:**

> **输入:** N = 30，D = 3
> **输出:** 39
> 3 + 13 + 23 = 39
> **输入:** N = 5，D = 7
> **输出:** 0

**方法:**在[第 1 集](https://www.geeksforgeeks.org/sum-of-integers-upto-n-with-given-unit-digit/)中，我们看到了两种求所需和的基本方法，但复杂度是 **O(N)** ，对于更大的 **N** 需要更多的时间。这里有一个更有效的方法，假设给我们 **N = 30** 和 **D = 3** :

> sum = 3+13+23
> sum = 3+(10+3)+(20+3)
> sum = 3 *(3)+(10+20)

从上面的观察，我们可以通过以下步骤找到总和:

*   递减 **N** 直到 **N % 10！= D** 。
*   求 **K = N / 10** 。
*   现在，**sum =(K+1)* D+((K * 10)+(10 * K * K))/2)**。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define ll long long int

// Function to return the required sum
ll getSum(ll n, int d)
{
    if (n < d)
        return 0;

    // Decrement N
    while (n % 10 != d)
        n--;

    ll k = n / 10;

    return (k + 1) * d + (k * 10 + 10 * k * k) / 2;
}

// Driver code
int main()
{
    ll n = 30;
    int d = 3;
    cout << getSum(n, d);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java  implementation of the approach

import java.io.*;

class GFG {

// Function to return the required sum
static long getSum(long n, int d)
{
    if (n < d)
        return 0;

    // Decrement N
    while (n % 10 != d)
        n--;

    long k = n / 10;

    return (k + 1) * d + (k * 10 + 10 * k * k) / 2;
}

// Driver code

    public static void main (String[] args) {
     long n = 30;
    int d = 3;
    System.out.println(getSum(n, d));    }
}
//This code is contributed by inder_verma..
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the required sum
def getSum(n, d) :

    if (n < d) :
        return 0

    # Decrement N
    while (n % 10 != d) :
        n -= 1

    k = n // 10

    return ((k + 1) * d +
            (k * 10 + 10 * k * k) // 2)

# Driver code
if __name__ == "__main__" :

    n = 30
    d = 3
    print(getSum(n, d))

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach

class GFG {

// Function to return the required sum
static int getSum(int n, int d)
{
    if (n < d)
        return 0;

    // Decrement N
    while (n % 10 != d)
        n--;

    int k = n / 10;

    return (k + 1) * d + (k * 10 + 10 * k * k) / 2;
}

// Driver code

    public static void Main () {
    int n = 30;
    int d = 3;
    System.Console.WriteLine(getSum(n, d)); }
}
//This code is contributed by mits.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the required sum
function getSum($n, $d)
{
    if ($n < $d)
        return 0;

    // Decrement N
    while ($n % 10 != $d)
        $n--;

    $k = (int)($n / 10);

    return ($k + 1) * $d +
           ($k * 10 + 10 * $k * $k) / 2;
}

// Driver code
$n = 30;
$d = 3;
echo getSum($n, $d);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// java script  implementation of the approach

// Function to return the required sum
function getSum(n, d)
{
    if (n < d)
        return 0;

    // Decrement N
    while (n % 10 != d)
        n--;

    k = parseInt(n / 10);

    return (k + 1) * d +
        (k * 10 + 10 * k * k) / 2;
}

// Driver code
let n = 30;
let d = 3;
document.write( getSum(n, d));

// This code is contributed
// by bobby
</script>
```

**Output:** 

```
39
```