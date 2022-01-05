# 计算矩阵从左上角到右下角的所有可能路径，不要穿过对角线

> 原文:[https://www . geesforgeks . org/count-所有可能的路径-从矩阵的左上角到右下角-不交叉对角线/](https://www.geeksforgeeks.org/count-all-possible-paths-from-top-left-to-bottom-right-of-a-matrix-without-crossing-the-diagonal/)

给定一个整数 **N** ，它表示矩阵的大小，任务是找到从矩阵左上角到达右下角而不穿过矩阵对角线的可能方法的数量。来自矩阵的任何单元 **(i，j)** 的可能移动是 **(i，j + 1)** (右)或 **(i + 1，j)** (下)。

**示例:**

> **输入:**N = 4
> T3】输出: 5
> 
> **输入:**N = 3
> T3】输出: 3

**方法:**根据以下观察可以解决问题:

*   矩阵中允许的移动是向下或向右移动一个单元格，不跨越对角线。
*   因此，在任何时候，向下移动的次数总是大于或等于向右移动的次数。
*   因此，这遵循了 [**加泰罗尼亚数字**](https://www.geeksforgeeks.org/program-nth-catalan-number/) **的模式。**

因此，基于观察，问题简化为计算 [N <sup>th</sup> 加泰罗尼亚数字](https://www.geeksforgeeks.org/program-nth-catalan-number/)。仅考虑为上三角形计算的路径，因为不允许对角线交叉。如果从单元格 **(0，0)** 移动到 **(1，0)** 将导致对角线交叉。

> N <sup>th</sup> 加泰罗尼亚数字(K<sub>N)</sub>=(<sup>2N</sup>C<sub>N</sub>)/(N+1)，其中 <sup>2n</sup> C <sub>n</sub> 为二项式系数。
> 
> 总路数= K <sub>n</sub>

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate
// Binomial Coefficient C(n, r)
int binCoff(int n, int r)
{
    int val = 1;
    int i;
    if (r > (n - r)) {

        // C(n, r) = C(n, n-r)
        r = (n - r);
    }

    for (i = 0; i < r; i++) {

        // [n * (n-1) *---* (n-r+1)] /
        // [r * (r-1) *----* 1]
        val *= (n - i);
        val /= (i + 1);
    }
    return val;
}
// Function to calculate
// the total possible paths
int findWays(int n)
{
    // Update n to n - 1 as (N - 1)
    // catalan number is the result
    n--;

    int a, b, ans;

    // Stores 2nCn
    a = binCoff(2 * n, n);

    // Stores Nth Catalan
    // number
    b = a / (n + 1);

    // Stores the required
    // answer
    ans = b;

    return ans;
}

// Driver Code
int main()
{

    int n = 4;
    cout << findWays(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.util.*;
class GFG {

    // Function to calculate
    // Binomial Coefficient C(n, r)
    static int binCoff(int n, int r)
    {
        int val = 1;
        int i;
        if (r > (n - r)) {
            // C(n, r) = C(n, n-r)
            r = (n - r);
        }

        for (i = 0; i < r; i++) {
            // [n * (n - 1) *---* (n - r + 1)] /
            // [r * (r - 1) *----* 1]
            val *= (n - i);
            val /= (i + 1);
        }
        return val;
    }

    // Function to calculate
    // the total possible paths
    static int findWays(int n)
    {
        // Update n to n - 1 as (N - 1)
        // catalan number is the result
        n--;

        int a, b, ans;

        // Stores 2nCn
        a = binCoff(2 * n, n);

        // Stores Nth Catalan
        // number
        b = a / (n + 1);

        // Stores the required
        // answer
        ans = b;

        return ans;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 4;
        System.out.print(findWays(n));
    }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 Program to implement
# the above approach
# Function to calculate
# Binomial Coefficient C(n, r)
def binCoff(n, r):
    val = 1
    if (r > (n - r)):

        # C(n, r) = C(n, n-r)
        r = (n - r)

    for i in range (r):

        # [n * (n-1) *---* (n-r + 1)] /
        # [r * (r-1) *----* 1]
        val *= (n - i)
        val //= (i + 1)
    return val

# Function to calculate
# the total possible paths
def findWays(n):

    # Update n to n - 1
    n = n - 1

    # Stores 2nCn
    a = binCoff(2 * n, n)

    # Stores Nth Catalan
    # number
    b = a // (n + 1)

    # Stores the required
    # answer
    ans = b

    return ans

# Driver Code
if __name__ == "__main__":

    n = 4
    print(findWays(n))

# This code is contributed by Chitranayal
```

## C#

```
// C# Program to implement
// the above approach
using System;
class GFG {

    // Function to calculate
    // Binomial Coefficient C(n, r)
    static int binCoff(int n, int r)
    {
        int val = 1;
        int i;
        if (r > (n - r)) {
            // C(n, r) = C(n, n-r)
            r = (n - r);
        }

        for (i = 0; i < r; i++) {
            // [n * (n - 1) *---* (n - r + 1)] /
            // [r * (r - 1) *----* 1]
            val *= (n - i);
            val /= (i + 1);
        }
        return val;
    }

    // Function to calculate
    // the total possible paths
    static int findWays(int n)
    {
        // Update n to n - 1 as (N - 1)
        // catalan number is the result
        n--;

        int a, b, ans;

        // Stores 2nCn
        a = binCoff(2 * n, n);

        // Stores Nth Catalan
        // number
        b = a / (n + 1);

        // Stores the required
        // answer
        ans = 2 * b;

        return ans;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int n = 4;
        Console.Write(findWays(n));
    }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript Program to implement
// the above approach

// Function to calculate
// Binomial Coefficient C(n, r)
function binCoff(n, r)
{
    var val = 1;
    var i;
    if (r > (n - r)) {

        // C(n, r) = C(n, n-r)
        r = (n - r);
    }

    for (i = 0; i < r; i++) {

        // [n * (n-1) *---* (n-r+1)] /
        // [r * (r-1) *----* 1]
        val *= (n - i);
        val /= (i + 1);
    }
    return val;
}
// Function to calculate
// the total possible paths
function findWays(n)
{
    // Update n to n - 1 as (N - 1)
    // catalan number is the result
    n--;

    var a, b, ans;

    // Stores 2nCn
    a = binCoff(2 * n, n);

    // Stores Nth Catalan
    // number
    b = a / (n + 1);

    // Stores the required
    // answer
    ans = b;

    return ans;
}

// Driver Code
var n = 4;
document.write( findWays(n));

</script>
```

**Output:** 

```
5
```