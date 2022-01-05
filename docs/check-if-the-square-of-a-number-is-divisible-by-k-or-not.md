# 检查一个数的平方是否能被 K 整除

> 原文:[https://www . geeksforgeeks . org/check-如果一个数的平方被 k 整除或不整除/](https://www.geeksforgeeks.org/check-if-the-square-of-a-number-is-divisible-by-k-or-not/)

给定两个整数 **X** 和 **K** ，任务是找出**X<sup>2</sup>T7】是否能被 **K** 整除。这里 **K** 和 **X** 都可以位于**【1，10<sup>18</sup>**的范围内。**

**示例:**

> **输入:** X = 6，K = 9
> **输出:** YES
> **说明:**
> 因为 6 <sup>2</sup> 等于 36，可以被 9 整除。
> 
> **输入:** X = 7，K = 21
> **输出:** NO
> **说明:**
> 因为 7 <sup>2</sup> 等于 49，不能被 21 整除。

**方法:**
如上所述， **X** 可以位于**【1，10<sup>18</sup>**的范围内，所以我们不能直接检查 **X <sup>2</sup>** 是否可以被 **K** 整除，因为它会导致内存溢出。因此有效的方法是首先计算 **X** 和 **K** 的[最大公约数](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/)。计算出 GCD 后，我们将它作为我们可以从 **X** 和 **K** 中划分的最大部分。用 GCD 减少 K，检查 **X** 是否能被减少的 **K** 整除。

下面是上述方法的实现:

## C++

```
// C++ implementation to
// check if the square of X is
// divisible by K

#include <bits/stdc++.h>
using namespace std;

// Function to return if
// square of X is divisible
// by K
void checkDivisible(int x, int k)
{
    // Finding gcd of x and k
    int g = __gcd(x, k);

    // Dividing k by their gcd
    k /= g;

    // Check for divisibility of X
    // by reduced K
    if (x % k == 0) {
        cout << "YES\n";
    }
    else {
        cout << "NO\n";
    }
}

// Driver Code
int main()
{
    int x = 6, k = 9;
    checkDivisible(x, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to
// check if the square of X is
// divisible by K

class GFG{

// Function to return if
// square of X is divisible
// by K
static void checkDivisible(int x, int k)
{
    // Finding gcd of x and k
    int g = __gcd(x, k);

    // Dividing k by their gcd
    k /= g;

    // Check for divisibility of X
    // by reduced K
    if (x % k == 0)
    {
        System.out.print("YES\n");
    }
    else
    {
        System.out.print("NO\n");
    }
}
static int __gcd(int a, int b)
{
    return b == 0 ? a : __gcd(b, a % b);    
}

// Driver Code
public static void main(String[] args)
{
    int x = 6, k = 9;
    checkDivisible(x, k);
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 implementation to
# check if the square of X is
# divisible by K

from math import gcd

# Function to return if
# square of X is divisible
# by K
def checkDivisible(x, k):

    # Finding gcd of x and k
    g = gcd(x, k)

    # Dividing k by their gcd
    k //= g

    # Check for divisibility of X
    # by reduced K
    if (x % k == 0):
        print("YES")
    else:
        print("NO")

# Driver Code
if __name__ == '__main__':

    x = 6
    k = 9
    checkDivisible(x, k);

# This code is contributed by Bhupendra_Singh
```

## C#

```
// C# implementation to check
// if the square of X is
// divisible by K
using System;

class GFG{

// Function to return if
// square of X is divisible
// by K
static void checkDivisible(int x, int k)
{

    // Finding gcd of x and k
    int g = __gcd(x, k);

    // Dividing k by their gcd
    k /= g;

    // Check for divisibility of X
    // by reduced K
    if (x % k == 0)
    {
        Console.Write("YES\n");
    }
    else
    {
        Console.Write("NO\n");
    }
}

static int __gcd(int a, int b)
{
    return b == 0 ? a : __gcd(b, a % b);    
}

// Driver Code
public static void Main(String[] args)
{
    int x = 6, k = 9;

    checkDivisible(x, k);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript implementation to
// check if the square of X is
// divisible by K

// Return gcd of two numbers
function gcd(a, b)
{
    return b == 0 ? a : gcd(b, a % b);
}

// Function to return if
// square of X is divisible
// by K
function checkDivisible(x, k)
{

    // Finding gcd of x and k
    var g = gcd(x, k);

    // Dividing k by their gcd
    k /= g;

    // Check for divisibility of X
    // by reduced K
    if (x % k == 0)
    {
        document.write("YES");
    }
    else
    {
        document.write("NO");
    }
}

// Driver code
var x = 6, k = 9;
checkDivisible(x, k);

// This code is contributed by Ankita saini

</script>
```

**Output:** 

```
YES
```

时间复杂度:0(对数(最大值(x，k))

辅助空间；:O(1)