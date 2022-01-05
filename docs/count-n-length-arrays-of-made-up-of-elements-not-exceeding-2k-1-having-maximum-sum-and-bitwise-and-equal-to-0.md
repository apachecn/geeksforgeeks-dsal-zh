# 计数由不超过 2^k-1 的元素组成的 n 长度数组，这些元素具有最大和，按位等于 0

> 原文:[https://www . geesforgeks . org/count-n-length-由元素组成的数组-不超过-2k-1-具有-最大和-按位和-等于-0/](https://www.geeksforgeeks.org/count-n-length-arrays-of-made-up-of-elements-not-exceeding-2k-1-having-maximum-sum-and-bitwise-and-equal-to-0/)

给定两个整数 **N** 和 **K，**任务是找到满足以下条件的**N**-长度[数组](https://www.geeksforgeeks.org/array-data-structure/)的个数:

*   数组元素的总和是最大可能值。
*   对于 **i** ( *1 ≤ i ≤ N* )的每个可能值，**I<sup>th</sup>T7】元素应位于 **0** 和**2<sup>K</sup>–1**之间。**
*   此外，所有数组元素的[位“与”](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)应为 0。

***注:**既然，答案可以大，那么打印答案* [*取模 10^9 + 7*](https://www.geeksforgeeks.org/modulo-1097-1000000007/) *。*

**示例:**

> **输入:** N=2 K =2
> **输出:** 4
> **说明:**所需数组为({1，2}、{2，1}、{0，3}、{3，0})
> 
> **输入:**N = 1k = 1
> T3】输出: 1

**方法:**想法是观察如果[数组](https://www.geeksforgeeks.org/array-data-structure/)中所有元素的所有位都是 **1** ，那么所有元素的[位“与”](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)不会是 **0** ，尽管总和会最大化。因此，对于每个位，在至少一个元素中的每个位翻转 **1** 至 **0** ，使[按位“与”](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)等于 **0** ，同时保持总和最大。所以对于每一位，只选择一个元素，然后在那里翻转该位。既然有 **K** 位和 **N** 元素，答案就只有 **N^K** 。按照以下步骤解决问题:

*   定义一个[功能](https://www.geeksforgeeks.org/functions-in-c/) **功率(长长 x，长长 y，int p)** 并执行以下任务:
    *   将变量 **res** 初始化为 **1** 来存储结果。
    *   将 **x** 的值更新为**x % p**
    *   如果 **x** 等于 **0，**则返回 **0。**
    *   [循环迭代](https://www.geeksforgeeks.org/c-c-while-loop-with-examples/)直到 **y** 大于 **0** ，执行以下任务。
        *   如果 **y** 为奇数，则将 **res** 的值设置为 **(res*x)%p.**
        *   将 **y** 除以 **2。**
        *   将 **x** 的值设置为 **(x*x)%p.**
*   将变量 **mod** 初始化为 **1e9+7。**
*   将变量**和**初始化为[函数](https://www.geeksforgeeks.org/functions-in-c/) **幂(N，K，mod)返回的值。**
*   执行上述步骤后，打印**和**的值作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the power of n^k % p
int power(long long x, unsigned int y, int p)
{
    int res = 1;

    // Update x if it is more
    // than or equal to p
    x = x % p;

    // In case x is divisible by p;
    if (x == 0)
        return 0;

    while (y > 0) {

        // If y is odd, multiply
        // x with result
        if (y & 1)
            res = (res * x) % p;

        // y must be even now
        y = y >> 1; // y = y/2
        x = (x * x) % p;
    }
    return res;
}

// Function to count the number of
// arrays satisfying required conditions
int countArrays(int n, int k)
{
    int mod = 1000000007;
    // Calculating N^K
    int ans = power(n, k, mod);
    return ans;
}

// Driver Code
int main()
{
    int n = 3, k = 5;

    int ans = countArrays(n, k);
    cout << ans << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to calculate the power of n^k % p
static int power(int x, int y, int p)
{
    int res = 1;

    // Update x if it is more
    // than or equal to p
    x = x % p;

    // In case x is divisible by p;
    if (x == 0)
        return 0;

    while (y > 0)
    {

        // If y is odd, multiply
        // x with result
        if ((y & 1) == 1)
            res = (res * x) % p;

        // y must be even now
        y = y >> 1; // y = y/2
        x = (x * x) % p;
    }
    return res;
}

// Function to count the number of
// arrays satisfying required conditions
static int countArrays(int n, int k)
{
    int mod = 1000000007;

    // Calculating N^K
    int ans = power(n, k, mod);
    return ans;
}

// Driver Code
public static void main (String[] args)
{
    int n = 3, k = 5;
    int ans = countArrays(n, k);

    System.out.println(ans);
}
}

// This code is contributed by shubhamsingh10
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to calculate the power of n^k % p
def power(x, y, p):
    res = 1

    # Update x if it is more
    # than or equal to p
    x = x % p

    # In case x is divisible by p;
    if (x == 0):
        return 0
    while (y > 0):

        # If y is odd, multiply
        # x with result
        if (y & 1):
            res = (res * x) % p

        # y must be even now
        y = y >> 1  # y = y/2
        x = (x * x) % p
    return res

# Function to count the number of
# arrays satisfying required conditions
def countArrays(n, k):
    mod = 1000000007

    # Calculating N^K
    ans = power(n, k, mod)
    return ans

# Driver Code
n = 3
k = 5

ans = countArrays(n, k)
print(ans)

# This code is contributed by gfgking
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to calculate the power of n^k % p
static int power(int x, int y, int p)
{
    int res = 1;

    // Update x if it is more
    // than or equal to p
    x = x % p;

    // In case x is divisible by p;
    if (x == 0)
        return 0;

    while (y > 0) {

        // If y is odd, multiply
        // x with result
        if ((y & 1) !=0)
            res = (res * x) % p;

        // y must be even now
        y = y >> 1; // y = y/2
        x = (x * x) % p;
    }
    return res;
}

// Function to count the number of
// arrays satisfying required conditions
static int countArrays(int n, int k)
{
    int mod = 1000000007;
    // Calculating N^K
    int ans = power(n, k, mod);
    return ans;
}

// Driver Code
public static void Main()
{
    int n = 3, k = 5;
    int ans = countArrays(n, k);
    Console.Write(ans);
}
}

// This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>

        // JavaScript program for the above approach

        // Function to calculate the power of n^k % p
        function power(x, y, p) {
            let res = 1;

            // Update x if it is more
            // than or equal to p
            x = x % p;

            // In case x is divisible by p;
            if (x == 0)
                return 0;

            while (y > 0) {

                // If y is odd, multiply
                // x with result
                if (y & 1)
                    res = (res * x) % p;

                // y must be even now
                y = y >> 1; // y = y/2
                x = (x * x) % p;
            }
            return res;
        }

        // Function to count the number of
        // arrays satisfying required conditions
        function countArrays(n, k) {
            let mod = 1000000007;
            // Calculating N^K
            let ans = power(n, k, mod);
            return ans;
        }

        // Driver Code

        let n = 3, k = 5;

        let ans = countArrays(n, k);
        document.write(ans);

// This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
243
```

***时间复杂度:** O(log(K))*
***辅助空间:** O(1)*