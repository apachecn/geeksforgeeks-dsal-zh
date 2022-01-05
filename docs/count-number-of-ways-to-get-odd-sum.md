# 计数获得奇数和的方式数

> 原文:[https://www . geesforgeks . org/count-获得奇数和的途径数/](https://www.geeksforgeeks.org/count-number-of-ways-to-get-odd-sum/)

给定 **N** 对数字。任务是计算从每对中选择一个数字的方法，这样这些数字的总和就是奇数。
**例:**

> **输入:**
> N = 2
> 3 4
> 1 2
> **输出:** 2
> **说明:**
> 我们可以从第一对中选 3，从第二对中选 2，它们的和是 5，是奇数。
> 同样，我们可以从第一对中选择 4，从第二对中选择 1，它们的和是 5，是奇数。
> 所以总的可能途径是 2 个。
> **输入:**
> N = 2
> 2 2
> 2
> T21】输出: 0

**进场:**

*   我们将在这里使用[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)，其中 **dp[i][0]** 将存储获得第 I 对的偶数和的多种可能方式，而 **dp[i][1]** 将存储获得第 I 对的奇数和的多种可能方式。
*   **cnt[i][0]** 将存储第 I 对中偶数的计数， **cnt[i][1]** 将存储第 I 对中奇数的计数。
*   众所周知，两个偶数之和或两个奇数之和总是偶数，一个偶数和一个奇数之和总是奇数。
*   我们将此应用于存储 DP 数组中的计数。
*   获得第一对的偶数和的方法是**DP[I–1][0]* CNT[I][0]+DP[I–1][1]* CNT[I][1]。**
*   获得第一对奇数和的方法是**DP[I–1][1]* CNT[I][0]+DP[I–1][0]* CNT[I][1]。**

以下是上述方法的实施:

## C++

```
// C++ implementation
#include <bits/stdc++.h>
using namespace std;

// Count the ways to sum up with odd
// by choosing one element form each
// pair
int CountOfOddSum(int a[][2], int n)
{
    int dp[n][2], cnt[n][2];

    // Initialize two array with 0
    memset(dp, 0, sizeof(dp));
    memset(cnt, 0, sizeof(cnt));

    for (int i = 0; i < n; i++) {
        for (int j = 0; j < 2; j++) {

            // if element is even
            if (a[i][j] % 2 == 0) {

                // store count of even
                // number in i'th pair
                cnt[i][0]++;
            }

            // if the element is odd
            else {

                // store count of odd
                // number in i'th pair
                cnt[i][1]++;
            }
        }
    }

    // Initial state of dp array
    dp[0][0] = cnt[0][0], dp[0][1] = cnt[0][1];

    for (int i = 1; i < n; i++) {

        // dp[i][0] = total number of ways
        // to get even sum upto i'th pair
        dp[i][0] = (dp[i - 1][0] * cnt[i][0]
                    + dp[i - 1][1] * cnt[i][1]);

        // dp[i][1] = total number of ways
        // to odd even sum upto i'th pair
        dp[i][1] = (dp[i - 1][0] * cnt[i][1]
                    + dp[i - 1][1] * cnt[i][0]);
    }

    // dp[n - 1][1] = total number of ways
    // to get odd sum upto n'th pair
    return dp[n - 1][1];
}

// Driver code
int main()
{

    int a[][2] = { { 1, 2 }, { 3, 6 } };
    int n = sizeof(a) / sizeof(a[0]);

    int ans = CountOfOddSum(a, n);

    cout << ans << "\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
class GFG
{
    // Count the ways to sum up with odd
    // by choosing one element form each
    // pair
    static int CountOfOddSum(int a[][], int n)
    {
        int [][]dp = new int[n][2];
        int [][]cnt = new int[n][2];

        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < 2; j++)
            {

                // if element is even
                if (a[i][j] % 2 == 0)
                {

                    // store count of even
                    // number in i'th pair
                    cnt[i][0]++;
                }

                // if the element is odd
                else
                {

                    // store count of odd
                    // number in i'th pair
                    cnt[i][1]++;
                }
            }
        }

        // Initial state of dp array
        dp[0][0] = cnt[0][0];
        dp[0][1] = cnt[0][1];

        for (int i = 1; i < n; i++)
        {

            // dp[i][0] = total number of ways
            // to get even sum upto i'th pair
            dp[i][0] = (dp[i - 1][0] * cnt[i][0] +
                        dp[i - 1][1] * cnt[i][1]);

            // dp[i][1] = total number of ways
            // to odd even sum upto i'th pair
            dp[i][1] = (dp[i - 1][0] * cnt[i][1] +
                        dp[i - 1][1] * cnt[i][0]);
        }

        // dp[n - 1][1] = total number of ways
        // to get odd sum upto n'th pair
        return dp[n - 1][1];
    }

    // Driver code
    public static void main (String[] args)
    {
        int a[][] = {{ 1, 2 }, { 3, 6 }};
        int n = a.length;

        int ans = CountOfOddSum(a, n);

        System.out.println(ans);
    }
}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Count the ways to sum up with odd
# by choosing one element form each
# pair
def CountOfOddSum(a, n):

    dp = [[0 for i in range(2)]
             for i in range(n)]
    cnt = [[0 for i in range(2)]
              for i in range(n)]

    # Initialize two array with 0
    for i in range(n):
        for j in range(2):

            # if element is even
            if (a[i][j] % 2 == 0):

                #store count of even
                #number in i'th pair
                cnt[i][0] += 1

            # if the element is odd
            else :

                # store count of odd
                # number in i'th pair
                cnt[i][1] += 1

    # Initial state of dp array
    dp[0][0] = cnt[0][0]
    dp[0][1] = cnt[0][1]

    for i in range(1, n):

        # dp[i][0] = total number of ways
        # to get even sum upto i'th pair
        dp[i][0] = (dp[i - 1][0] * cnt[i][0] +
                    dp[i - 1][1] * cnt[i][1])

        # dp[i][1] = total number of ways
        # to odd even sum upto i'th pair
        dp[i][1] = (dp[i - 1][0] * cnt[i][1] +
                    dp[i - 1][1] * cnt[i][0])

    # dp[n - 1][1] = total number of ways
    # to get odd sum upto n'th pair
    return dp[n - 1][1]

# Driver code
a = [[1, 2] , [3, 6] ]
n = len(a)

ans = CountOfOddSum(a, n)

print(ans)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{
    // Count the ways to sum up with odd
    // by choosing one element form each
    // pair
    static int CountOfOddSum(int [ , ] a, int n)
    {
        int [ , ]dp = new int[n, 2];
        int [ , ]cnt = new int[n, 2];

        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < 2; j++)
            {

                // if element is even
                if (a[i, j] % 2 == 0)
                {

                    // store count of even
                    // number in i'th pair
                    cnt[i, 0]++;
                }

                // if the element is odd
                else
                {

                    // store count of odd
                    // number in i'th pair
                    cnt[i, 1]++;
                }
            }
        }

        // Initial state of dp array
        dp[0, 0] = cnt[0, 0];
        dp[0, 1] = cnt[0, 1];

        for (int i = 1; i < n; i++)
        {

            // dp[i, 0] = total number of ways
            // to get even sum upto i'th pair
            dp[i, 0] = (dp[i - 1, 0] * cnt[i, 0] +
                        dp[i - 1, 1] * cnt[i, 1]);

            // dp[i, 1] = total number of ways
            // to odd even sum upto i'th pair
            dp[i, 1] = (dp[i - 1, 0] * cnt[i, 1] +
                        dp[i - 1, 1] * cnt[i, 0]);
        }

        // dp[n - 1, 1] = total number of ways
        // to get odd sum upto n'th pair
        return dp[n - 1, 1];
    }

    // Driver code
    public static void Main ()
    {
        int [ , ] a = { { 1, 2 }, { 3, 6 } };
        int n = a.GetLength(1);

        int ans = CountOfOddSum(a, n);

        Console.WriteLine(ans);
    }
}

// This code is contributed by ihritik
```

## java 描述语言

```
<script>

// Javascript implementation

// Count the ways to sum up with odd
// by choosing one element form each
// pair
function CountOfOddSum(a, n)
{
    let dp = new Array(n), cnt = new Array(n);
    for (let i = 0; i < n; i++) {
        dp[i] = new Array(2).fill(0);
        cnt[i] = new Array(2).fill(0);
    }

    for (let i = 0; i < n; i++) {
        for (let j = 0; j < 2; j++) {

            // if element is even
            if (a[i][j] % 2 == 0) {

                // store count of even
                // number in i'th pair
                cnt[i][0]++;
            }

            // if the element is odd
            else {

                // store count of odd
                // number in i'th pair
                cnt[i][1]++;
            }
        }
    }

    // Initial state of dp array
    dp[0][0] = cnt[0][0], dp[0][1] = cnt[0][1];

    for (let i = 1; i < n; i++) {

        // dp[i][0] = total number of ways
        // to get even sum upto i'th pair
        dp[i][0] = (dp[i - 1][0] * cnt[i][0]
                    + dp[i - 1][1] * cnt[i][1]);

        // dp[i][1] = total number of ways
        // to odd even sum upto i'th pair
        dp[i][1] = (dp[i - 1][0] * cnt[i][1]
                    + dp[i - 1][1] * cnt[i][0]);
    }

    // dp[n - 1][1] = total number of ways
    // to get odd sum upto n'th pair
    return dp[n - 1][1];
}

// Driver code

    let a = [ [ 1, 2 ], [ 3, 6 ] ];
    let n = a.length;

    let ans = CountOfOddSum(a, n);

    document.write(ans);

</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(N)