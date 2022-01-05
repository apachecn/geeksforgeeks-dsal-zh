# 范围[L，R](华丽项链组合学问题)

内最多 N 位的排序数字总数

> 原文:[https://www . geesforgeks . org/total-count-of-sorted-numbers-up-n-digits-in-range-l-r-granular-项链-组合学-problem/](https://www.geeksforgeeks.org/total-count-of-sorted-numbers-upto-n-digits-in-range-l-r-magnificent-necklace-combinatorics-problem/)

给定三个整数 **N，L，**和 **R** ，任务是打印最多由 **N** 颗珍珠组成的项链的方式总数，使得一颗珍珠的值在**【L，R】**的范围内，并按升序排列。

**示例:**

> **输入:** N = 3，L = 6，R = 9
> **输出:** 34
> **说明:**
> 项链可以通过以下方式形成:
> 
> 1.  长度为 1 的项链可以做成{“6”、“7”、“8”、“9”}。
> 2.  长度为二的项链，可以做成{“66”、“67”、“68”、“69”、“77”、“78”、“79”、“88”、“89”、“99”}。
> 3.  长度三的项链，可以形成的有{“666”、“667”、“668”、“669”、“677”、“678”、“679”、“688”、“689”、“699”、“777”、“778”、“779”、“788”、“789”、“799”、“888”、“889”、“899”、“999”}。
> 
> 因此，总的来说，项链可以以(4+10+20 = 34)种方式形成。
> 
> **输入:** N = 1，L = 8，R = 9
> **输出:** 2
> **说明:**
> 项链可以通过以下方式形成:{“8”、“9”}。

**方法:**给定的问题可以基于以下观察来解决:

1.  使用带有[前缀和的 2 种状态](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)可以解决这个问题。
2.  假设 **Dp(i，j)** 存储形成大小为 **i** 的项链的方法计数，珍珠的价值在范围**【L，j】内。**
3.  那么在 **i <sup>th</sup>** 位置的过渡状态可以定义为:
    1.  对于范围**【左，右】**内的每个值 **j**
        1.  **Dp(i，j)= DP(I–1，l)+DP(I–1，l+1)…、DP(I–1，j–1)+DP(I–1，j)**
4.  通过对每个 **i** 使用[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)可以优化上述转换，如下所示:
    1.  **Dp(i，j) = Dp(i，L) + Dp(i，l+1)+DP(I，j–1)+DP(I，j)**
5.  因此，现在可以将过渡定义为:
    1.  **Dp(i，j) = Dp(i-1，j) + Dp(i，j-1)**

按照以下步骤解决问题:

*   初始化一个变量，说 **ans** 为 **0** ，存储结果。
*   初始化一个 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)，把维度**N *(R–L+1)**的 **Dp[][]** 说成 **0** 来存储所有的 Dp 状态。
*   [使用变量 **i、**迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N–1】**，并分配 **Dp[i][0] = 1。**
*   [使用变量 **i、**迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，R–L】**，并将 **Dp[0][i]** 更新为**Dp[0][I]= Dp[0][I–1]+1。**
*   将**DP[0][r–l]**分配给**年。**
*   [使用变量 **i、**迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，N–1】**，并执行以下操作:
    *   [使用变量 **j、**迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，R–L】**，并将 **Dp[i][j]** 更新为**Dp[I][j]= Dp[I][j–1]+Dp[I–1][j]。**
    *   将**和**增加**Dp[I][R–L]。**
*   最后，完成以上步骤后，打印 **ans** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count total number of ways
int Count(int N, int L, int R)
{
    // Stores all DP-states
    vector<vector<int> > dp(N,
                            vector<int>(R - L + 1, 0));
    // Stores the result
    int ans = 0;

    // Traverse the range [0, N]
    for (int i = 0; i < N; i++) {
        dp[i][0] = 1;
    }
    // Traverse the range [1, R - L]
    for (int i = 1; i < dp[0].size(); i++) {

        // Update dp[i][j]
        dp[0][i] = dp[0][i - 1] + 1;
    }

    // Assign dp[0][R-L] to ans
    ans = dp[0][R - L];

    // Traverse the range [1, N]
    for (int i = 1; i < N; i++) {

        // Traverse the range [1, R - L]
        for (int j = 1; j < dp[0].size(); j++) {

            // Update dp[i][j]
            dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
        }

        // Increment ans by dp[i-1][j]
        ans += dp[i][R - L];
    }

    // Return ans
    return ans;
}

// Driver Code
int main()
{
    // Input
    int N = 3;
    int L = 6;
    int R = 9;

    // Function call
    cout << Count(N, L, R);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to count total number of ways
static int Count(int N, int L, int R)
{

    // Stores all DP-states
    int[][] dp = new int[N][R - L + 1];

    // Stores the result
    int ans = 0;

    // Traverse the range [0, N]
    for(int i = 0; i < N; i++)
    {
        dp[i][0] = 1;
    }

    // Traverse the range [1, R - L]
    for(int i = 1; i < dp[0].length; i++)
    {

        // Update dp[i][j]
        dp[0][i] = dp[0][i - 1] + 1;
    }

    // Assign dp[0][R-L] to ans
    ans = dp[0][R - L];

    // Traverse the range [1, N]
    for(int i = 1; i < N; i++)
    {

        // Traverse the range [1, R - L]
        for(int j = 1; j < dp[0].length; j++)
        {

            // Update dp[i][j]
            dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
        }

        // Increment ans by dp[i-1][j]
        ans += dp[i][R - L];
    }

    // Return ans
    return ans;
}

// Driver Code
public static void main(String args[])
{

    // Input
    int N = 3;
    int L = 6;
    int R = 9;

    // Function call
    System.out.println(Count(N, L, R));
}
}

// This code is contributed by avijitmondal1998
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count total number of ways
def Count(N, L, R):

    # Stores all DP-states
    dp = [[0 for i in range(R - L + 1)]
             for i in range(N)]

    # Stores the result
    ans = 0

    # Traverse the range [0, N]
    for i in range(N):
        dp[i][0] = 1

    # Traverse the range [1, R - L]
    for i in range(1, len(dp[0])):

        # Update dp[i][j]
        dp[0][i] = dp[0][i - 1] + 1

    # Assign dp[0][R-L] to ans
    ans = dp[0][R - L]

    # Traverse the range [1, N]
    for i in range(1, N):

        # Traverse the range [1, R - L]
        for j in range(1, len(dp[0])):

            # Update dp[i][j]
            dp[i][j] = dp[i - 1][j] + dp[i][j - 1]

        # Increment ans by dp[i-1][j]
        ans += dp[i][R - L]

    # Return ans
    return ans

# Driver Code
if __name__ == '__main__':

    # Input
    N = 3
    L = 6
    R = 9

    # Function call
    print(Count(N, L, R))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to count total number of ways
static int Count(int N, int L, int R)
{

    // Stores all DP-states
    int[,] dp = new int[N, R - L + 1];

    // Stores the result
    int ans = 0;

    // Traverse the range [0, N]
    for(int i = 0; i < N; i++)
    {
        dp[i, 0] = 1;
    }

    // Traverse the range [1, R - L]
    for(int i = 1; i < dp.GetLength(1); i++)
    {

        // Update dp[i][j]
        dp[0, i] = dp[0, i - 1] + 1;
    }

    // Assign dp[0][R-L] to ans
    ans = dp[0, R - L];

    // Traverse the range [1, N]
    for(int i = 1; i < N; i++)
    {

        // Traverse the range [1, R - L]
        for(int j = 1; j < dp.GetLength(1); j++)
        {

            // Update dp[i][j]
            dp[i, j] = dp[i - 1, j] + dp[i, j - 1];
        }

        // Increment ans by dp[i-1][j]
        ans += dp[i, R - L];
    }

    // Return ans
    return ans;
}

// Driver Code
public static void Main()
{

    // Input
    int N = 3;
    int L = 6;
    int R = 9;

    // Function call
    Console.Write(Count(N, L, R));
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to count total number of ways
function Count(N, L, R) {
    // Stores all DP-states
    let dp = new Array(N).fill(0).map(() => new Array(R - L + 1).fill(0));

    // Stores the result
    let ans = 0;

    // Traverse the range [0, N]
    for (let i = 0; i < N; i++) {
        dp[i][0] = 1;
    }
    // Traverse the range [1, R - L]
    for (let i = 1; i < dp[0].length; i++) {

        // Update dp[i][j]
        dp[0][i] = dp[0][i - 1] + 1;
    }

    // Assign dp[0][R-L] to ans
    ans = dp[0][R - L];

    // Traverse the range [1, N]
    for (let i = 1; i < N; i++) {

        // Traverse the range [1, R - L]
        for (let j = 1; j < dp[0].length; j++) {

            // Update dp[i][j]
            dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
        }

        // Increment ans by dp[i-1][j]
        ans += dp[i][R - L];
    }

    // Return ans
    return ans;
}

// Driver Code

// Input
let N = 3;
let L = 6;
let R = 9;

// Function call
document.write(Count(N, L, R));

// This code is contributed by _saurabh_jaiswal.
</script>
```

**Output**

```
34
```

***时间复杂度:**O(N *(R–L))*
***辅助空间:**O(N *(R–L))*