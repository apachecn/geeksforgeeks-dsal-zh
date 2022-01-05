# 带有修改的游戏的最优策略

> 原文:[https://www . geesforgeks . org/优化策略-带修改的游戏/](https://www.geeksforgeeks.org/optimal-strategy-for-a-game-with-modifications/)

**问题陈述**:考虑一排价值 v1 的 n 枚硬币。。。vn，其中 n 是偶数。我们轮流和对手比赛。在每一回合中，玩家执行以下操作 **K 次**。
玩家从该行中选择第一枚或最后一枚硬币，将其从该行中永久移除，并获得硬币的价值。
确定如果用户先出手，用户肯定能赢的最大可能金额。
**注:**对手和用户一样聪明。
**举例:**

> **输入:**数组= {10，15，20，9，2，5}，k=2
> **输出:** 32
> **解释:**
> 假设用户最初选择了 10 和 15。
> 用户拥有的硬币值为 25，
> {20，9，2，5}剩余在数组中。
> 第二轮，对手挑 20 和 9，使其值 29。
> 第三轮，用户选择 2 和 5，使他的总值为 32。
> **输入:**数组= {10，15，20，9，2}，k=1
> **输出:** 32

**方法:**
需要形成一个**递归解**，需要存储子问题的值来计算结果。
以**为例**得出递归解；
arr = {10，15，20，9，2，5}，k=2
所以如果用户在第一圈选择了 10，15，那么数组中还剩下 20，9，2，5。
但如果用户选择 10、5；那么数组中还剩下 15，20，9，2。
最后，如果用户选择 5，2；那么数组中还剩下 10，15，20，9。
因此在选择 k 个元素后的任何迭代中，长度为 n-k 的连续子阵列被保留用于下一次计算。
所以递归解可以形成在:

> **S(l，r) = (sum(l，r)–sum(l+I，l+i+n-k-1))+(sum(l+i，l+I+n-k-1)–S(l+I，l+i+n-k-1))**
> 其中 **l+i+n-k-1 < =r**

所选元素之和 **Sc=(和(l，r)–和(l+i，l+i+n-k-1))**
现在对手将执行下一回合，因此
下一步所选元素之和=当前数组从 l 到 r 的总和–
下一步对手所选元素之和等于

```
Nc=(sum(l+i, l+i+n-k-1) - S(l+i, l+i+n-k-1)).
S(l, r) = Sc + Nc
where,
Nc=(sum(l+i, l+i+n-k-1) - S(l+i, l+i+n-k-1))
Sc=(sum(l, r) - sum(l+i, l+i+n-k-1))
```

以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;
#define ll long long int

// Function to return sum of subarray from l to r
ll sum(int arr[], int l, int r)
{
    // calculate sum by a loop from l to r
    ll s = 0;
    for (int i = l; i <= r; i++) {
        s += arr[i];
    }
    return s;
}

// dp to store the values of sub problems
ll dp[101][101][101] = { 0 };

ll solve(int arr[], int l, int r, int k)
{
    // if length of the array is less than k
    // return the sum
    if (r - l + 1 <= k)
        return sum(arr, l, r);

    // if the value is previously calculated
    if (dp[l][r][k])
        return dp[l][r][k];

    // else calculate the value
    ll sum_ = sum(arr, l, r);
    ll len_r = (r - l + 1) - k;
    ll len = (r - l + 1);
    ll ans = 0;

    // select all the sub array of length len_r
    for (int i = 0; i < len - len_r + 1; i++) {
        // get the sum of that sub array
        ll sum_sub = sum(arr, i + l, i + l + len_r - 1);

        // check if it is the maximum or not
        ans = max(ans, (sum_ - sum_sub) + (sum_sub -
                  solve(arr, i + l, i + l + len_r - 1, k)));
    }

    // store it in the table
    dp[l][r][k] = ans;

    return ans;
}

// Driver code
int main()
{
    int arr[] = { 10, 15, 20, 9, 2, 5 }, k = 2;
    int n = sizeof(arr) / sizeof(int);
    memset(dp, 0, sizeof(dp));

    cout << solve(arr, 0, n - 1, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{

    // Function to return sum of subarray from l to r
    static int sum(int arr[], int l, int r)
    {
        // calculate sum by a loop from l to r
        int s = 0;
        for (int i = l; i <= r; i++)
        {
            s += arr[i];
        }
        return s;
    }

    // dp to store the values of sub problems
    static int dp[][][] = new int[101][101][101] ;

    static int solve(int arr[], int l, int r, int k)
    {
        // if length of the array is less than k
        // return the sum
        if (r - l + 1 <= k)
            return sum(arr, l, r);

        // if the value is previously calculated
        if (dp[l][r][k] != 0)
            return dp[l][r][k];

        // else calculate the value
        int sum_ = sum(arr, l, r);
        int len_r = (r - l + 1) - k;
        int len = (r - l + 1);
        int ans = 0;

        // select all the sub array of length len_r
        for (int i = 0; i < len - len_r + 1; i++)
        {
            // get the sum of that sub array
            int sum_sub = sum(arr, i + l, i + l + len_r - 1);

            // check if it is the maximum or not
            ans = Math.max(ans, (sum_ - sum_sub) + (sum_sub -
                    solve(arr, i + l, i + l + len_r - 1, k)));
        }

        // store it in the table
        dp[l][r][k] = ans;

        return ans;
    }

    // Driver code
    public static void main (String[] args)
    {

        int arr[] = { 10, 15, 20, 9, 2, 5 }, k = 2;
        int n = arr.length;

        System.out.println(solve(arr, 0, n - 1, k));

    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the above approach
import numpy as np

# Function to return sum of subarray from l to r
def Sum(arr, l, r) :

    # calculate sum by a loop from l to r
    s = 0;
    for i in range(l, r + 1) :
        s += arr[i];

    return s;

# dp to store the values of sub problems
dp = np.zeros((101, 101, 101));

def solve(arr, l, r, k) :

    # if length of the array is less than k
    # return the sum
    if (r - l + 1 <= k) :
        return Sum(arr, l, r);

    # if the value is previously calculated
    if (dp[l][r][k]) :
        return dp[l][r][k];

    # else calculate the value
    sum_ = Sum(arr, l, r);
    len_r = (r - l + 1) - k;
    length = (r - l + 1);
    ans = 0;

    # select all the sub array of length len_r
    for i in range(length - len_r + 1) :

        # get the sum of that sub array
        sum_sub = Sum(arr, i + l, i + l + len_r - 1);

        # check if it is the maximum or not
        ans = max(ans, (sum_ - sum_sub) + (sum_sub -
                            solve(arr, i + l, i + l + len_r - 1, k)));

    # store it in the table
    dp[l][r][k] = ans;

    return ans;

# Driver code
if __name__ == "__main__" :

    arr = [ 10, 15, 20, 9, 2, 5 ]; k = 2;

    n = len(arr);

    print(solve(arr, 0, n - 1, k));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    // Function to return sum of subarray from l to r
    static int sum(int []arr, int l, int r)
    {
        // calculate sum by a loop from l to r
        int s = 0;
        for (int i = l; i <= r; i++)
        {
            s += arr[i];
        }
        return s;
    }

    // dp to store the values of sub problems
    static int [,,]dp = new int[101, 101, 101] ;

    static int solve(int []arr, int l, int r, int k)
    {
        // if length of the array is less than k
        // return the sum
        if (r - l + 1 <= k)
            return sum(arr, l, r);

        // if the value is previously calculated
        if (dp[l, r, k] != 0)
            return dp[l, r, k];

        // else calculate the value
        int sum_ = sum(arr, l, r);
        int len_r = (r - l + 1) - k;
        int len = (r - l + 1);
        int ans = 0;

        // select all the sub array of length len_r
        for (int i = 0; i < len - len_r + 1; i++)
        {
            // get the sum of that sub array
            int sum_sub = sum(arr, i + l, i + l + len_r - 1);

            // check if it is the maximum or not
            ans = Math.Max(ans, (sum_ - sum_sub) + (sum_sub -
                    solve(arr, i + l, i + l + len_r - 1, k)));
        }

        // store it in the table
        dp[l, r, k] = ans;

        return ans;
    }

    // Driver code
    public static void Main ()
    {
        int []arr = { 10, 15, 20, 9, 2, 5 };
        int k = 2;
        int n = arr.Length;

        Console.WriteLine(solve(arr, 0, n - 1, k));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

    // JavaScript implementation of the above approach

    // Function to return sum of subarray from l to r
    function sum(arr, l, r)
    {
        // calculate sum by a loop from l to r
        let s = 0;
        for (let i = l; i <= r; i++)
        {
            s += arr[i];
        }
        return s;
    }

    // dp to store the values of sub problems
    let dp = new Array(101);
    for (let i = 0; i < 101; i++)
    {
        dp[i] = new Array(101);
        for (let j = 0; j < 101; j++)
        {
            dp[i][j] = new Array(101);
            for (let k = 0; k < 101; k++)
            {
                dp[i][j][k] = 0;
            }
        }
    }

    function solve(arr, l, r, k)
    {
        // if length of the array is less than k
        // return the sum
        if (r - l + 1 <= k)
            return sum(arr, l, r);

        // if the value is previously calculated
        if (dp[l][r][k] != 0)
            return dp[l][r][k];

        // else calculate the value
        let sum_ = sum(arr, l, r);
        let len_r = (r - l + 1) - k;
        let len = (r - l + 1);
        let ans = 0;

        // select all the sub array of length len_r
        for (let i = 0; i < len - len_r + 1; i++)
        {
            // get the sum of that sub array
            let sum_sub = sum(arr, i + l, i + l + len_r - 1);

            // check if it is the maximum or not
            ans = Math.max(ans, (sum_ - sum_sub) + (sum_sub -
                    solve(arr, i + l, i + l + len_r - 1, k)));
        }

        // store it in the table
        dp[l][r][k] = ans;

        return ans;
    }

    let arr = [ 10, 15, 20, 9, 2, 5 ], k = 2;
    let n = arr.length;

    document.write(solve(arr, 0, n - 1, k));

</script>
```

**Output:** 

```
32
```