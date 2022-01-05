# 找到楼梯情况下到达第 Kth 步的路数

> 原文:[https://www . geeksforgeeks . org/find-the-number-to-reach-kth-step-in-step-case/](https://www.geeksforgeeks.org/find-the-number-of-ways-to-reach-kth-step-in-stair-case/)

给定一个大小为 **N** 的数组 **arr[]** 和一个整数 **K** 。数组表示楼梯中断裂的台阶。一步也迈不到。任务是找到从 **0** 开始的楼梯中第 **K <sup>第</sup>** 步到达的路数，此时在任何位置都可以走最大长度的一步 **2** 。答案可能非常大。所以，打印答案模 **10 <sup>9</sup> + 7** 。
**例:**

> **输入:** arr[] = {3}，K = 6
> **输出:**4
> 0->1->2->4->5->6
> 0->1->2->4->6
> 0->2->4->5->6
> 0->

**方法:**这个问题可以用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解决。创建一个 **dp[]** 数组，其中 **dp[i]** 将存储到达 **i <sup>第</sup>** 步的路数，并且只有当 **i <sup>第</sup>** 步未被打破时，循环关系才会为**DP[I]= DP[I–1]+DP[I–2]**，否则 **0** 。最终答案将是。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

const int MOD = 1000000007;

// Function to return the number
// of ways to reach the kth step
int number_of_ways(int arr[], int n, int k)
{
    if (k == 1)
        return 1;

    // Create the dp array
    int dp[k + 1];
    memset(dp, -1, sizeof dp);

    // Broken steps
    for (int i = 0; i < n; i++)
        dp[arr[i]] = 0;

    dp[0] = 1;
    dp[1] = (dp[1] == -1) ? 1 : dp[1];

    // Calculate the number of ways for
    // the rest of the positions
    for (int i = 2; i <= k; ++i) {

        // If it is a blocked position
        if (dp[i] == 0)
            continue;

        // Number of ways to get to the ith step
        dp[i] = dp[i - 1] + dp[i - 2];

        dp[i] %= MOD;
    }

    // Return the required answer
    return dp[k];
}

// Driver code
int main()
{
    int arr[] = { 3 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 6;

    cout << number_of_ways(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
    static final int MOD = 1000000007;

    // Function to return the number
    // of ways to reach the kth step
    static int number_of_ways(int arr[],
                              int n, int k)
    {
        if (k == 1)
            return 1;

        // Create the dp array
        int dp[] = new int[k + 1];

        int i;

        for(i = 0; i < k + 1; i++)
            dp[i] = -1 ;

        // Broken steps
        for (i = 0; i < n; i++)
            dp[arr[i]] = 0;

        dp[0] = 1;
        dp[1] = (dp[1] == -1) ? 1 : dp[1];

        // Calculate the number of ways for
        // the rest of the positions
        for (i = 2; i <= k; ++i)
        {

            // If it is a blocked position
            if (dp[i] == 0)
                continue;

            // Number of ways to get to the ith step
            dp[i] = dp[i - 1] + dp[i - 2];

            dp[i] %= MOD;
        }

        // Return the required answer
        return dp[k];
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = { 3 };
        int n = arr.length;
        int k = 6;

        System.out.println(number_of_ways(arr, n, k));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach
MOD = 1000000007;

# Function to return the number
# of ways to reach the kth step
def number_of_ways(arr, n, k) :

    if (k == 1) :
        return 1;

    # Create the dp array
    dp = [-1] * (k + 1);

    # Broken steps
    for i in range(n) :
        dp[arr[i]] = 0;

    dp[0] = 1;
    dp[1] = 1 if (dp[1] == -1) else dp[1];

    # Calculate the number of ways for
    # the rest of the positions
    for i in range(2, k + 1) :

        # If it is a blocked position
        if (dp[i] == 0) :
            continue;

        # Number of ways to get to the ith step
        dp[i] = dp[i - 1] + dp[i - 2];

        dp[i] %= MOD;

    # Return the required answer
    return dp[k];

# Driver code
if __name__ == "__main__" :

    arr = [ 3 ];
    n = len(arr);
    k = 6;

    print(number_of_ways(arr, n, k));

# This code is contributed by kanugargng
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    static readonly int MOD = 1000000007;

    // Function to return the number
    // of ways to reach the kth step
    static int number_of_ways(int []arr,
                              int n, int k)
    {
        if (k == 1)
            return 1;

        // Create the dp array
        int []dp = new int[k + 1];

        int i;

        for(i = 0; i < k + 1; i++)
            dp[i] = -1 ;

        // Broken steps
        for (i = 0; i < n; i++)
            dp[arr[i]] = 0;

        dp[0] = 1;
        dp[1] = (dp[1] == -1) ? 1 : dp[1];

        // Calculate the number of ways for
        // the rest of the positions
        for (i = 2; i <= k; ++i)
        {

            // If it is a blocked position
            if (dp[i] == 0)
                continue;

            // Number of ways to get to the ith step
            dp[i] = dp[i - 1] + dp[i - 2];

            dp[i] %= MOD;
        }

        // Return the required answer
        return dp[k];
    }

    // Driver code
    public static void Main (String[] args)
    {
        int []arr = { 3 };
        int n = arr.Length;
        int k = 6;

        Console.WriteLine(number_of_ways(arr, n, k));
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

    // JavaScript implementation of the approach

    let MOD = 1000000007;

    // Function to return the number
    // of ways to reach the kth step
    function number_of_ways(arr, n, k)
    {
        if (k == 1)
            return 1;

        // Create the dp array
        let dp = new Array(k + 1);

        let i;

        for(i = 0; i < k + 1; i++)
            dp[i] = -1 ;

        // Broken steps
        for (i = 0; i < n; i++)
            dp[arr[i]] = 0;

        dp[0] = 1;
        dp[1] = (dp[1] == -1) ? 1 : dp[1];

        // Calculate the number of ways for
        // the rest of the positions
        for (i = 2; i <= k; ++i)
        {

            // If it is a blocked position
            if (dp[i] == 0)
                continue;

            // Number of ways to get to the ith step
            dp[i] = dp[i - 1] + dp[i - 2];

            dp[i] %= MOD;
        }

        // Return the required answer
        return dp[k];
    }

    let arr = [ 3 ];
    let n = arr.length;
    let k = 6;

    document.write(number_of_ways(arr, n, k));

</script>
```

**Output:** 

```
4
```