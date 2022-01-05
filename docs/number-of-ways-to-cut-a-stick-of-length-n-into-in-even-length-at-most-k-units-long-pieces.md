# 将一根长度为 N 的棍子切成长度最多为 K 个单位的偶数长段的方法数量

> 原文:[https://www . geeksforgeeks . org/将长度为 n 的棒切割成最多 k 个单位的偶数长片的方式数/](https://www.geeksforgeeks.org/number-of-ways-to-cut-a-stick-of-length-n-into-in-even-length-at-most-k-units-long-pieces/)

给定一个长度为 **N** 单位的杆，任务是找到将杆切割成若干部分的方法，使得每个部分的长度均匀，每个部分最多为 **K** 单位。
**例:**

> **输入:** N = 6，K = 4
> **输出:** 3
> **说明:**
> 长度为 6 个单位的杆需要加工成长度最多为 4 个单位的零件。因此，以三种方式切割棒:
> 方式 1: 2 个单位+ 2 个单位+ 2 个单位
> 方式 2: 2 个单位+ 4 个单位
> 方式 3: 4 个单位+ 2 个单位
> **输入:** N = 4，K = 2
> **输出:** 1
> **说明:**
> 长度为 4 个单位的棒需要分成长度最多为 2 个单位的部分。因此将棒切成 2 + 2 个单位。

**方法:**思路是使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)，其中[最优子结构](https://www.geeksforgeeks.org/optimal-substructure-property-in-dynamic-programming-dp-2/)是每个部分的长度应该为**甚至**。通过递归调用函数**对切割后获得的工件进行计数，一直到切割棒。
以下是上述方法的实施:**

## **C++14**

```
// C++14 program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Recursive Function to count
// the total number of ways
int solve(int n, int k, int mod, int dp[])
{
    // Base case if no-solution exist
    if (n < 0)
        return 0;

    // Condition if a solution exist
    if (n == 0)
        return 1;

    // Check if already calculated
    if (dp[n] != -1)
        return dp[n];

    // Initialize counter
    int cnt = 0;
    for (int i = 2; i <= k; i += 2) {
        // Recursive call
        cnt = (cnt % mod
               + solve(n - i, k, mod, dp)
                     % mod)
              % mod;
    }

    // Store the answer
    dp[n] = cnt;

    // Return the answer
    return cnt;
}

// Driver code
int main()
{

    const int mod = 1e9 + 7;
    int n = 4, k = 2;
    int dp[n + 1];
    memset(dp, -1, sizeof(dp));
    int ans = solve(n, k, mod, dp);
    cout << ans << '\n';

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.*;

class GFG{

// Recursive Function to count
// the total number of ways
static int solve(int n, int k, int mod, int dp[])
{

    // Base case if no-solution exist
    if (n < 0)
        return 0;

    // Condition if a solution exist
    if (n == 0)
        return 1;

    // Check if already calculated
    if (dp[n] != -1)
        return dp[n];

    // Initialize counter
    int cnt = 0;
    for(int i = 2; i <= k; i += 2)
    {

        // Recursive call
        cnt = (cnt % mod + solve(n - i, k, mod,
               dp) % mod) % mod;
    }

    // Store the answer
    dp[n] = cnt;

    // Return the answer
    return cnt;
}

// Driver code
public static void main(String[] args)
{
    int mod = (int)(1e9 + 7);
    int n = 4, k = 2;

    int []dp = new int[n + 1];
    for(int i = 0; i < n + 1; i++)
        dp[i] = -1;

    int ans = solve(n, k, mod, dp);

    System.out.println(ans);
}
}

// This code is contributed by Amit Katiyar
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Recursive function to count
# the total number of ways
def solve(n, k, mod, dp):

    # Base case if no-solution exist
    if (n < 0):
        return 0

    # Condition if a solution exist
    if (n == 0):
        return 1

    # Check if already calculated
    if (dp[n] != -1):
        return dp[n]

    # Initialize counter
    cnt = 0
    for i in range(2, k + 1, 2):

        # Recursive call
        cnt = ((cnt % mod +
                solve(n - i, k, mod, dp) %
                                    mod) % mod)

    # Store the answer
    dp[n] = cnt

    # Return the answer
    return int(cnt)

# Driver code
if __name__ == '__main__':

    mod = 1e9 + 7
    n = 4
    k = 2

    dp = [-1] * (n + 1)
    ans = solve(n, k, mod, dp)

    print(ans)

# This code is contributed by mohit kumar 29
```

## **C#**

```
// C# program for the above approach
using System;

class GFG{

// Recursive function to count
// the total number of ways
static int solve(int n, int k, int mod, int []dp)
{

    // Base case if no-solution exist
    if (n < 0)
        return 0;

    // Condition if a solution exist
    if (n == 0)
        return 1;

    // Check if already calculated
    if (dp[n] != -1)
        return dp[n];

    // Initialize counter
    int cnt = 0;
    for(int i = 2; i <= k; i += 2)
    {

        // Recursive call
        cnt = (cnt % mod + solve(n - i, k, mod,
               dp) % mod) % mod;
    }

    // Store the answer
    dp[n] = cnt;

    // Return the answer
    return cnt;
}

// Driver code
public static void Main(String[] args)
{
    int mod = (int)(1e9 + 7);
    int n = 4, k = 2;

    int []dp = new int[n + 1];
    for(int i = 0; i < n + 1; i++)
        dp[i] = -1;

    int ans = solve(n, k, mod, dp);

    Console.WriteLine(ans);
}
}

// This code is contributed by Amit Katiyar
```

## **java 描述语言**

```
<script>

// Javascript program to implement
// the above approach

// Recursive Function to count
// the total number of ways
function solve(n, k, mod, dp)
{

    // Base case if no-solution exist
    if (n < 0)
        return 0;

    // Condition if a solution exist
    if (n == 0)
        return 1;

    // Check if already calculated
    if (dp[n] != -1)
        return dp[n];

    // Initialize counter
    let cnt = 0;
    for(let i = 2; i <= k; i += 2)
    {

        // Recursive call
        cnt = (cnt % mod + solve(n - i, k, mod,
               dp) % mod) % mod;
    }

    // Store the answer
    dp[n] = cnt;

    // Return the answer
    return cnt;
}

    // Driver Code

    let mod = (1e9 + 7);
    let n = 4, k = 2;

    let dp = new Array(n+1).fill(0);
    for(let i = 0; i < n + 1; i++)
        dp[i] = -1;

    let ans = solve(n, k, mod, dp);

    document.write(ans);

</script>
```

****Output:** 

```
1
```**