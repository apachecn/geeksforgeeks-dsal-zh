# 生成长度为 N 的二进制字符串的方法的数量，使得 0 总是一起出现在大小为 K 的组中

> 原文:[https://www . geeksforgeeks . org/二进制长度字符串 n-这样-0-总是在大小为 k 的组中一起出现的方式数/](https://www.geeksforgeeks.org/number-of-ways-to-make-binary-string-of-length-n-such-that-0s-always-occur-together-in-groups-of-size-k/)

给定两个整数 **N 和 K** ，任务是计算生成长度为 N 的二进制字符串的方法数量，使得 0 总是一起出现在一组大小为 K 的字符串中。
**示例:**

> **输入:** N = 3，K = 2
> **输出:** 3
> 二进制字符串数:
> 111
> 100
> 001
> **输入:** N = 4，K = 2
> **输出:** 5

这个问题使用**动态编程**很容易解决。设 **dp[i]** 为满足条件的长度为 **i** 的二进制串的个数。
从条件可以推断:

*   **dp[i] = 1 对 1 < = i < k** 。
*   同样 **dp[k] = 2** 因为长度为 K 的二进制串要么是只有 0 的串，要么是只有 1 的串。
*   现在，如果我们考虑 i > k。如果我们决定第 i <sup>个</sup>字符为“1”，那么 **dp[i] = dp[i-1]** ，因为二进制字符串的数量不会改变。然而，如果我们决定第 i <sup>个</sup>字符为“0”，那么我们要求**个先前的 k-1 字符也应为“0”，因此 dp[i] = dp[i-k]** 。因此，dp[i]将是这两个值的总和。

**因此**，

```
dp[i] = dp[i - 1] + dp[i - k]
```

以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
using namespace std;

const int mod = 1000000007;

// Function to return no of ways to build a binary
// string of length N such that 0s always occur
// in groups of size K
int noOfBinaryStrings(int N, int k)
{
    int dp[100002];
    for (int i = 1; i <= k - 1; i++) {
        dp[i] = 1;
    }

    dp[k] = 2;

    for (int i = k + 1; i <= N; i++) {
        dp[i] = (dp[i - 1] + dp[i - k]) % mod;
    }

    return dp[N];
}

// Driver Code
int main()
{
    int N = 4;
    int K = 2;
    cout << noOfBinaryStrings(N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

static int mod = 1000000007;

// Function to return no of ways to build a binary
// string of length N such that 0s always occur
// in groups of size K
static int noOfBinaryStrings(int N, int k)
{
    int dp[] = new int[100002];
    for (int i = 1; i <= k - 1; i++)
    {
        dp[i] = 1;
    }

    dp[k] = 2;

    for (int i = k + 1; i <= N; i++)
    {
        dp[i] = (dp[i - 1] + dp[i - k]) % mod;
    }

    return dp[N];
}

// Driver Code
public static void main(String[] args)
{
    int N = 4;
    int K = 2;
    System.out.println(noOfBinaryStrings(N, K));
}
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 iimplementation of the
# above approach
mod = 1000000007;

# Function to return no of ways to
# build a binary string of length N
# such that 0s always occur in
# groups of size K
def noOfBinaryStrings(N, k) :
    dp = [0] * 100002;
    for i in range(1, K) :
        dp[i] = 1;

    dp[k] = 2;

    for i in range(k + 1, N + 1) :
        dp[i] = (dp[i - 1] + dp[i - k]) % mod;

    return dp[N];

# Driver Code
if __name__ == "__main__" :

    N = 4;
    K = 2;

    print(noOfBinaryStrings(N, K));

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

static int mod = 1000000007;

// Function to return no of ways to build
// a binary string of length N such that
// 0s always occur in groups of size K
static int noOfBinaryStrings(int N, int k)
{
    int []dp = new int[100002];
    for (int i = 1; i <= k - 1; i++)
    {
        dp[i] = 1;
    }

    dp[k] = 2;

    for (int i = k + 1; i <= N; i++)
    {
        dp[i] = (dp[i - 1] + dp[i - k]) % mod;
    }

    return dp[N];
}

// Driver Code
public static void Main()
{
    int N = 4;
    int K = 2;
    Console.WriteLine(noOfBinaryStrings(N, K));
}
}

/* This code contributed by PrinciRaj1992 */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach
$mod = 1000000007;

// Function to return no of ways to
// build a binary string of length N
// such that 0s always occur in groups
// of size K
function noOfBinaryStrings($N, $k)
{
    global $mod;
    $dp = array(0, 100002, NULL);
    for ($i = 1; $i <= $k - 1; $i++)
    {
        $dp[$i] = 1;
    }

    $dp[$k] = 2;

    for ($i = $k + 1; $i <= $N; $i++)
    {
        $dp[$i] = ($dp[$i - 1] +
                   $dp[$i - $k]) % $mod;
    }

    return $dp[$N];
}

// Driver Code
$N = 4;
$K = 2;
echo noOfBinaryStrings($N, $K);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

let mod = 1000000007;

// Function to return no of ways to build a binary
// string of length N such that 0s always occur
// in groups of size K
function noOfBinaryStrings(N,k)
{
    let dp = new Array(100002);
    for (let i = 1; i <= k - 1; i++)
    {
        dp[i] = 1;
    }

    dp[k] = 2;

    for (let i = k + 1; i <= N; i++)
    {
        dp[i] = (dp[i - 1] + dp[i - k]) % mod;
    }

    return dp[N];
}

// Driver Code
let N = 4;
let K = 2;
document.write(noOfBinaryStrings(N, K));

// This code is contributed by rag2127.
</script>
```

**Output:** 

```
5
```