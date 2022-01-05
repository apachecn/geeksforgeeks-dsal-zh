# 通过使用动态编程的给定操作将 N 转换为 M

> 原文:[https://www . geesforgeks . org/convert-n-to-m-with-给定-operations-use-dynamic-programming/](https://www.geeksforgeeks.org/convert-n-to-m-with-given-operations-using-dynamic-programming/)

给定两个整数 **N** 和 **M** ，任务是通过以下操作将 **N** 转换为 **M** :

1.  将 **N** 乘以 **2** ，即 **N = N * 2** 。
2.  从 **N** 中减去 **1** ，即**N = N–1**。

**示例:**

> **输入:** N = 4，M = 6
> T3】输出: 2
> 执行操作 2:N = N–1 = 4–1 = 3
> 执行操作 1: N = N * 2 = 3 * 2 = 6
> 
> **输入:** N = 10，M = 1
> T3】输出: 9

**方法:**创建一个大小为 **MAX = 10 <sup>5</sup> + 5** 的数组 **dp[]** 来存储答案，以防止一次又一次的相同计算，并用-1 初始化所有数组元素。

*   如果 **N ≤ 0** 或 **N ≥ MAX** 表示不能转换为 **M** ，那么返回 **MAX** 。
*   如果 **N = M** 则返回 0，因为 **N** 被转换为 **M** 。
*   否则在**DP【N】**找到值，如果不是 **-1** ，说明计算的比较早，所以返回**DP【N】**。
*   如果是 **-1** ，那么将调用递归函数作为 **2 * N** 和**N–1**并返回最小值，因为如果 **N** 是奇数，那么只能通过执行**N–1**操作来达到，如果 **N** 是偶数，那么必须执行 **2 * N** 操作，因此检查两种可能性并返回最小值。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

const int N = 1e5 + 5;

int n, m;
int dp[N];

// Function to return the minimum
// number of given operations
// required to convert n to m
int minOperations(int k)
{
    // If k is either 0 or out of range
    // then return max
    if (k <= 0 || k >= 2e4) {
        return 1e9;
    }

    // If k = m then conversion is
    // complete so return 0
    if (k == m) {
        return 0;
    }

    int& ans = dp[k];

    // If it has been calculated earlier
    if (ans != -1) {
        return ans;
    }
    ans = 1e9;

    // Call for 2*k and k-1 and return
    // the minimum of them. If k is even
    // then it can be reached by 2*k operations
    // and If k is odd then it can be reached
    // by k-1 operations so try both cases
    // and return the minimum of them
    ans = 1 + min(minOperations(2 * k),
                  minOperations(k - 1));
    return ans;
}

// Driver code
int main()
{
    n = 4, m = 6;
    memset(dp, -1, sizeof(dp));

    cout << minOperations(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{
    static final int N = 10000;
    static int n, m;
    static int[] dp = new int[N];

    // Function to return the minimum
    // number of given operations
    // required to convert n to m
    static int minOperations(int k)
    {

        // If k is either 0 or out of range
        // then return max
        if (k <= 0 || k >= 10000)
            return 1000000000;

        // If k = m then conversion is
        // complete so return 0
        if (k == m)
            return 0;

        dp[k] = dp[k];

        // If it has been calculated earlier
        if (dp[k] != -1)
            return dp[k];
        dp[k] = 1000000000;

        // Call for 2*k and k-1 and return
        // the minimum of them. If k is even
        // then it can be reached by 2*k operations
        // and If k is odd then it can be reached
        // by k-1 operations so try both cases
        // and return the minimum of them
        dp[k] = 1 + Math.min(minOperations(2 * k),
                             minOperations(k - 1));
        return dp[k];
    }

    // Driver Code
    public static void main(String[] args)
    {
        n = 4;
        m = 6;
        Arrays.fill(dp, -1);
        System.out.println(minOperations(n));
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of the approach
N = 1000
dp = [-1] * N

# Function to return the minimum
# number of given operations
# required to convert n to m
def minOperations(k):

    # If k is either 0 or out of range
    # then return max
    if (k <= 0 or k >= 1000):
        return 1e9

    # If k = m then conversion is
    # complete so return 0
    if (k == m):
        return 0

    dp[k] = dp[k]

    # If it has been calculated earlier
    if (dp[k] != -1):
        return dp[k]

    dp[k] = 1e9

    # Call for 2*k and k-1 and return
    # the minimum of them. If k is even
    # then it can be reached by 2*k operations
    # and If k is odd then it can be reached
    # by k-1 operations so try both cases
    # and return the minimum of them
    dp[k] = 1 + min(minOperations(2 * k),
                    minOperations(k - 1))
    return dp[k]

# Driver code
if __name__ == '__main__':
    n = 4
    m = 6
    print(minOperations(n))

# This code is contributed by ashutosh450
```

## C#

```
// C# implementation of the approach
using System;
using System.Linq;

class GFG
{
    static int N = 10000;
    static int n, m;
    static int[] dp = Enumerable.Repeat(-1, N).ToArray();

    // Function to return the minimum
    // number of given operations
    // required to convert n to m
    static int minOperations(int k)
    {

        // If k is either 0 or out of range
        // then return max
        if (k <= 0 || k >= 10000)
            return 1000000000;

        // If k = m then conversion is
        // complete so return 0
        if (k == m)
            return 0;

        dp[k] = dp[k];

        // If it has been calculated earlier
        if (dp[k] != -1)
            return dp[k];
        dp[k] = 1000000000;

        // Call for 2*k and k-1 and return
        // the minimum of them. If k is even
        // then it can be reached by 2*k operations
        // and If k is odd then it can be reached
        // by k-1 operations so try both cases
        // and return the minimum of them
        dp[k] = 1 + Math.Min(minOperations(2 * k),
                             minOperations(k - 1));
        return dp[k];
    }

    // Driver Code
    public static void Main(String[] args)
    {
        n = 4;
        m = 6;

        //Arrays.fill(dp, -1);
        Console.Write(minOperations(n));
    }
}

// This code is contributed by
// Mohit kumar 29
```

## java 描述语言

```
<script>

    let N = 10000;
    let n, m;
    let dp = new Array(N);

    function minOperations(k)
    {

        // If k is either 0 or out of range
        // then return max
        if (k <= 0 || k >= 10000)
            return 1000000000;

        // If k = m then conversion is
        // complete so return 0
        if (k == m)
            return 0;

        dp[k] = dp[k];

        // If it has been calculated earlier
        if (dp[k] != -1)
            return dp[k];
        dp[k] = 1000000000;

        // Call for 2*k and k-1 and return
        // the minimum of them. If k is even
        // then it can be reached by 2*k operations
        // and If k is odd then it can be reached
        // by k-1 operations so try both cases
        // and return the minimum of them
        dp[k] = 1 + Math.min(minOperations(2 * k),
                             minOperations(k - 1));
        return dp[k];
    }

    // Driver Code
    n = 4;
    m = 6;
    for(let i = 0; i < dp.length; i++)
    {
        dp[i] = -1;
    }
    document.write(minOperations(n));

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
2
```