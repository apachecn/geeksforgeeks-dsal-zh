# 翻转数组元素的最小符号以获得可能的正元素的最小和

> 原文:[https://www . geesforgeks . org/flip-数组元素的最小符号-获得最小正元素和-可能/](https://www.geeksforgeeks.org/flip-minimum-signs-of-array-elements-to-get-minimum-sum-of-positive-elements-possible/)

给定一个正元素数组，你必须翻转它的一些元素的符号，这样数组元素的合成和应该是最小非负的(尽可能接近零)。返回符号需要翻转的元素的最小数量，以使结果总和最小非负。注意所有数组元素的总和不会超过 10 <sup>4</sup> 。
**例:**

> **输入:** arr[] = {15，10，6}
> **输出:** 1
> 在这里，我们将翻转 15
> 的符号，结果总和为 1。
> **输入:** arr[] = [14，10，4]
> **输出:** 1
> 这里，我们将翻转 14 的符号，结果和为 0。
> 请注意，翻转 10 和 4 的符号也会使
> 的结果总和为 0，但翻转元素的数量不是最小的。

**天真方法:**对于数组的每个元素 A[i]，0 ≤ i < n，我们有 2 个选项。

1.  A[i]的符号翻转(-ve)。
2.  A[i]的符号没有翻转(+ve)。

所以我们总共可以有 2 <sup>n</sup> 个可能的阵列配置。我们可以保持每个配置中元素和翻转次数的总和，并跟踪最小总和(平局被最小翻转次数打破)。最小和配置中的翻转次数将是答案。
**时间复杂度:** O(2 <sup>n</sup> )，其中 n 为数组中的元素个数。
**高效途径:**这个问题可以用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解决，是标准 [0/1 背包问题](https://www.geeksforgeeks.org/0-1-knapsack-problem-dp-10/)的变种。不同的是，我们有两个选项，即要么在背包中包含一个项目，要么排除它，这里就像翻转元素的符号或不。而不是背包问题中的包重，这里是数组所有元素的总和，不翻转(问题陈述中给出的最大 10 <sup>4</sup> )。
**最优子结构:**设 dp[i][j]为数组前 I 个元素中使和等于 j 所需的最小翻转次数，
1 ≤ i ≤ n 和-sum ≤ j ≤ sum 其中 sum 为数组中所有没有翻转的元素的和。

> 如果 ar[I–1]的符号未翻转为 sum = j
> DP[I][j]= DP[I–1][j–A[I–1]]
> 如果 ar[I–1]的符号翻转为 sum = j
> dp[i][j] = min(dp[i][j]，DP[I–1][j+A[I–1]]+1)

**注意:**因为翻转后数组元素的和可能为负。所以我们不能用 2D 数组来制表，因为在 dp[i][j]中，j 是数组的和，索引不能为负。因此，我们将使用哈希映射数组。数组的大小将为 n + 1。
**重叠子问题:**就像 0/1 背包问题一样，这里也有重叠子问题。我们不需要一次又一次地评估结果，而是可以将子问题的结果存储在表中。
**时间复杂度:** O(n * sum)
**辅助空间:** O(n * sum)
其中 n 为元素个数，sum 为未翻转数组的元素之和。
**空间优化:**如果仔细看最优子结构，dp[i][j]将仅取决于 DP[I–1][j–A[I–1]]/DP[I–1][j+A[I–1]]。因此，只有 2 行 I 和 I–1 参与。因此，我们只需要 2 行而不是 n + 1 行。
以下是我们需要优化空间的变化。

1.  不是取数组大小=n+1，而是声明大小=2 的数组。
2.  引入布尔变量(比如标志)在地图之间切换。我们可以初始化 dp[0]映射并开始填充 dp[1]。在下一次迭代中，dp[0]是当前映射，dp[1]是先前映射。这样，我们可以继续在两个地图之间切换。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the
// minimum number of elements
// whose sign must be flipped
// to get the positive
// sum of array elements as close
// to 0 as possible
int solve(int A[], int n)
{

    // Array of unordered_map of size=2.
    unordered_map<int, int> dp[2];

    // boolean variable used for
    // toggling between maps
    bool flag = 1;

    // Calculate the sum of all
    // elements of the array
    int sum = 0;
    for (int i = 0; i < n; i++)
        sum += A[i];

    // Initializing first map(dp[0])
    // with INT_MAX because
    // for i=0, there are no elements
    // in the array to flip
    for (int i = -sum; i <= sum; i++)
        dp[0][i] = INT_MAX;

    // Base Case
    dp[0][0] = 0;

    for (int i = 1; i <= n; i++) {
        for (int j = -sum; j <= sum; j++) {
            dp[flag][j] = INT_MAX;
            if (j - A[i - 1] <= sum && j - A[i - 1] >= -sum)
                dp[flag][j] = dp[flag ^ 1][j - A[i - 1]];
            if (j + A[i - 1] <= sum && j + A[i - 1] >= -sum
                && dp[flag ^ 1][j + A[i - 1]] != INT_MAX)
                dp[flag][j]
                    = min(dp[flag][j],
                          dp[flag ^ 1][j + A[i - 1]] + 1);
        }

        // For toggling
        flag = flag ^ 1;
    }

    // Required sum is minimum non-negative
    // So, we iterate from i=0 to sum and find
    // the first i where dp[flag ^ 1][i] != INT_MAX
    for (int i = 0; i <= sum; i++) {
        if (dp[flag ^ 1][i] != INT_MAX)
            return dp[flag ^ 1][i];
    }

    // In worst case we will flip max n-1 elements
    return n - 1;
}

// Driver code
int main()
{
    int arr[] = { 10, 22, 9, 33, 21, 50, 41, 60 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << solve(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// the above approach:
class GFG {

    // Function to return the
    // minimum number of elements
    // whose sign must be flipped
    // to get the positive
    // sum of array elements as close
    // to 0 as possible
    public static int solve(int[] A, int n)
    {
        int[][] dp = new int[2000][2000];

        // boolean variable used for
        // toggling between maps
        int flag = 1;

        // Calculate the sum of all
        // elements of the array
        int sum = 0;
        for (int i = 0; i < n; i++)
            sum += A[i];

        // Initializing first map(dp[0])
        // with INT_MAX because for i=0,
        // there are no elements in the
        // array to flip
        for (int i = -sum; i <= sum; i++) {
            try {
                dp[0][i] = Integer.MAX_VALUE;
            }
            catch (Exception e) {
            }
        }

        // Base Case
        dp[0][0] = 0;

        for (int i = 1; i <= n; i++) {
            for (int j = 0; j <= sum; j++) {
                try {
                    dp[flag][j] = Integer.MAX_VALUE;
                    if (j - A[i - 1] <= sum
                        && j - A[i - 1] >= -sum)
                        dp[flag][j]
                            = dp[flag ^ 1][j - A[i - 1]];
                    if (j + A[i - 1] <= sum
                        && j + A[i - 1] >= -sum
                        && dp[flag ^ 1][j + A[i - 1]]
                               != Integer.MAX_VALUE)
                        dp[flag][j] = Math.min(
                            dp[flag][j],
                            dp[flag ^ 1][j + A[i - 1]] + 1);
                }
                catch (Exception e) {
                }
            }

            // For toggling
            flag = flag ^ 1;
        }

        // Required sum is minimum non-negative
        // So, we iterate from i=0 to sum and find
        // the first i where dp[flag ^ 1][i] != INT_MAX
        for (int i = 0; i <= sum; i++) {
            if (dp[flag ^ 1][i] != Integer.MAX_VALUE)
                return dp[flag ^ 1][i];
        }

        // In worst case we will flip max n-1 elements
        return n - 1;
    }

    // Driver code
    public static void main(String[] args)
    {
        int[] arr = { 10, 22, 9, 33, 21, 50, 41, 60 };
        int n = arr.length;
        System.out.println(solve(arr, n));
    }
}

// This code is contributed by sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the minimum
# number of elements
# whose sign must be flipped
# to get the positive
# sum of array elements as close
# to 0 as possible
def solve(A, n):

    dp = [[0 for i in range(2000)] for i in range(2000)]

    # boolean variable used for
    # toggling between maps
    flag = 1

    # Calculate the sum of all
    # elements of the array
    sum = 0
    for i in range(n):
        sum += A[i]

    # Initializing first map(dp[0])
    # with INT_MAX because
    # for i=0, there are no elements
    # in the array to flip
    for i in range(-sum, sum+1):
        dp[0][i] = 10**9

    # Base Case
    dp[0][0] = 0

    for i in range(1, n+1):
        for j in range(-sum, sum+1):
            dp[flag][j] = 10**9
            if (j - A[i - 1] <= sum and j - A[i - 1] >= -sum):
                dp[flag][j] = dp[flag ^ 1][j - A[i - 1]]
            if (j + A[i - 1] <= sum
                and j + A[i - 1] >= -sum
                    and dp[flag ^ 1][j + A[i - 1]] != 10**9):
                dp[flag][j] = min(dp[flag][j],
                                  dp[flag ^ 1][j + A[i - 1]] + 1)

        # For toggling
        flag = flag ^ 1

    # Required sum is minimum non-negative
    # So, we iterate from i=0 to sum and find
    # the first i where dp[flag ^ 1][i] != INT_MAX
    for i in range(sum+1):
        if (dp[flag ^ 1][i] != 10**9):
            return dp[flag ^ 1][i]

    # In worst case we will flip max n-1 elements
    return n - 1

# Driver code
arr = [10, 22, 9, 33, 21, 50, 41, 60]
n = len(arr)

print(solve(arr, n))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the above approach:
using System;

class GFG
{

// Function to return the minimum number
// of elements whose sign must be flipped
// to get the positive sum of array elements
// as close to 0 as possible
public static int solve(int[] A, int n)
{
    int[,] dp = new int[2000, 2000];

    // boolean variable used for
    // toggling between maps
    int flag = 1;

    // Calculate the sum of all elements
    // of the array
    int sum = 0;
    for (int i = 0; i < n; i++)
        sum += A[i];

    // Initializing first map(dp[0]) with
    // INT_MAX because for i=0, there are
    // no elements in the array to flip
    for (int i = -sum; i <= sum; i++)
    {
        try
        {
            dp[0, i] = int.MaxValue;
        }
        catch (Exception e){}
    }

    // Base Case
    dp[0, 0] = 0;

    for (int i = 1; i <= n; i++)
    {
        for (int j = 0; j <= sum; j++)
        {
            try
            {
                dp[flag, j] = int.MaxValue;
                if (j - A[i - 1] <= sum &&
                    j - A[i - 1] >= -sum)
                    dp[flag, j] = dp[flag ^ 1,
                                     j - A[i - 1]];
                if (j + A[i - 1] <= sum &&
                    j + A[i - 1] >= -sum &&
                    dp[flag ^ 1,
                       j + A[i - 1]] != int.MaxValue)
                    dp[flag, j] = Math.Min(dp[flag, j],
                                           dp[flag ^ 1,
                                           j + A[i - 1]] + 1);
            } catch (Exception e) {}
        }

        // For toggling
        flag = flag ^ 1;
    }

    // Required sum is minimum non-negative
    // So, we iterate from i=0 to sum and find
    // the first i where dp[flag ^ 1,i] != INT_MAX
    for (int i = 0; i <= sum; i++)
    {
        if (dp[flag ^ 1, i] != int.MaxValue)
            return dp[flag ^ 1, i];
    }

    // In worst case we will flip
    // max n-1 elements
    return n - 1;
}

// Driver code
public static void Main(String[] args)
{
    int[] arr = { 10, 22, 9, 33,
                  21, 50, 41, 60 };
    int n = arr.Length;
    Console.WriteLine(solve(arr, n));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// JS implementation of the approach

// Function to return the
// minimum number of elements
// whose sign must be flipped
// to get the positive
// sum of array elements as close
// to 0 as possible
function solve(A, n)
{

    // Array of unordered_map of size=2.
    let dp =  [],
    H = 2000, // 4 rows
    W = 2000; // of 6 cells

for ( var y = 0; y < H; y++ ) {
    dp[ y ] = [];
    for ( var x = 0; x < W; x++ ) {
        dp[ y ][ x ] = 0;
    }
}
    // boolean variable used for
    // toggling between maps
    let flag = 1;

    // Calculate the sum of all
    // elements of the array
    let sum = 0;
    for (let i = 0; i < n; i++)
        sum += A[i];

    // Initializing first map(dp[0])
    // with INT_MAX because
    // for i=0, there are no elements
    // in the array to flip
    for (let i = -sum; i <= sum; i++)
        dp[0][i] = Number.MAX_VALUE;

    // Base Case
    dp[0][0] = 0;

    for (let i = 1; i <= n; i++) {
        for (let j = -sum; j <= sum; j++) {
            dp[flag][j] = Number.MAX_VALUE;
            if (j - A[i - 1] <= sum && j - A[i - 1] >= -sum)
                dp[flag][j] = dp[flag ^ 1][j - A[i - 1]];
            if (j + A[i - 1] <= sum && j + A[i - 1] >= -sum
                && dp[flag ^ 1][j + A[i - 1]] != Number.MAX_VALUE)
                dp[flag][j]
                    = Math.min(dp[flag][j],
                          dp[flag ^ 1][j + A[i - 1]] + 1);
        }

        // For toggling
        flag = flag ^ 1;
    }

    // Required sum is minimum non-negative
    // So, we iterate from i=0 to sum and find
    // the first i where dp[flag ^ 1][i] != MAX_VALUE
    for (let i = 0; i <= sum; i++) {
        if (dp[flag ^ 1][i] != Number.MAX_VALUE)
            return dp[flag ^ 1][i];
    }

    // In worst case we will flip max n-1 elements
    return n - 1;
}

// Driver code
let arr = [ 10, 22, 9, 33, 21, 50, 41, 60 ];
let n = arr.length;
document.write(solve(arr, n));

// This code is contributed by rohitsingh07052.
</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(n *和)。
**辅助空间:** O(sum)其中 n 为元素个数，sum 为无翻转数组元素的和。