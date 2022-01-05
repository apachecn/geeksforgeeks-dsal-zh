# 选择球的方式，以便至少选择一个球

> 原文:[https://www . geeksforgeeks . org/选择球的方法-至少选择一个球/](https://www.geeksforgeeks.org/ways-to-choose-balls-such-that-at-least-one-ball-is-chosen/)

给定一个整数 **N** ，任务是找到从给定的 **N** 个球中选择一些球的方法，以便至少选择一个球。由于该值可能很大，因此打印该值模 **1000000007** 。
**例:**

> **输入:** N = 2
> **输出:** 3
> 三路为“*”, ".*”和“**”其中“*”表示
> 选择的球和“.”表示没有被选中的球。
> **输入:** N = 30000
> **输出:** 165890098

**进场:**有 **N** 个球，每个球可以选也可以不选。不同配置的总数为**2 * 2 * 2 *……* N**。我们可以把这个写成**2<sup>N</sup>T9】。但是没有选择球的状态必须从答案中减去。所以，结果将是**(2<sup>N</sup>–1)% 1000000007**。
以下是上述方法的实施:** 

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

const int MOD = 1000000007;

// Function to return the count of
// ways to choose the balls
int countWays(int n)
{

    // Calculate (2^n) % MOD
    int ans = 1;
    for (int i = 0; i < n; i++) {
        ans *= 2;
        ans %= MOD;
    }

    // Subtract the only where
    // no ball was chosen
    return ((ans - 1 + MOD) % MOD);
}

// Driver code
int main()
{
    int n = 3;

    cout << countWays(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
static int MOD = 1000000007;

// Function to return the count of
// ways to choose the balls
static int countWays(int n)
{

    // Calculate (2^n) % MOD
    int ans = 1;
    for (int i = 0; i < n; i++)
    {
        ans *= 2;
        ans %= MOD;
    }

    // Subtract the only where
    // no ball was chosen
    return ((ans - 1 + MOD) % MOD);
}

// Driver code
public static void main(String[] args)
{
    int n = 3;

    System.out.println(countWays(n));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

MOD = 1000000007

# Function to return the count of
# ways to choose the balls
def countWays(n):

    # Return ((2 ^ n)-1) % MOD
    return (((2**n) - 1) % MOD)

# Driver code
n = 3
print(countWays(n))
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
static int MOD = 1000000007;

// Function to return the count of
// ways to choose the balls
static int countWays(int n)
{

    // Calculate (2^n) % MOD
    int ans = 1;
    for (int i = 0; i < n; i++)
    {
        ans *= 2;
        ans %= MOD;
    }

    // Subtract the only where
    // no ball was chosen
    return ((ans - 1 + MOD) % MOD);
}

// Driver code
public static void Main(String[] args)
{
    int n = 3;

    Console.WriteLine(countWays(n));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// javascript implementation of the approach

     MOD = 1000000007;

    // Function to return the count of
    // ways to choose the balls
    function countWays(n) {

        // Calculate (2^n) % MOD
        var ans = 1;
        for (i = 0; i < n; i++) {
            ans *= 2;
            ans %= MOD;
        }

        // Subtract the only where
        // no ball was chosen
        return ((ans - 1 + MOD) % MOD);
    }

    // Driver code

        var n = 3;

        document.write(countWays(n));

// This code contributed by gauravrajput1
</script>
```

**Output:** 

```
7
```