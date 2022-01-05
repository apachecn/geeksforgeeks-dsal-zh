# 在 2*N 矩阵中精确制造 C 成分的方法数量

> 原文:[https://www . geeksforgeeks . org/精确制造 c-in-a-2n-matrix 组件的方法数量/](https://www.geeksforgeeks.org/number-of-ways-to-make-exactly-c-components-in-a-2n-matrix/)

给定两个正整数 **N** 和 **C** 。有一个 2*N 矩阵，其中矩阵的每个单元可以用 0 或 1 着色。任务是找到许多方法，形成 2*N 矩阵，正好有 c 个分量。

> 如果一个像元与另一个像元(直接相邻的像元)共享一条边，并且颜色相同，则称该像元与另一个像元在同一分量中。

**例:**

> **输入:** N = 2，C = 1
> **输出:** 2
> **解释:**
> C = 1 当矩阵的所有单元格都用相同的颜色着色时是可能的。
> 我们有 2 个颜色选择 0 和 1。因此答案是 2。
> **输入:** N = 1，C = 2
> **输出:** 2

**方法:**解决这个问题的思路是使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)。构建一个![(N+1) * (C+1) * 2 * 2 ](img/b4590cad48e7b082612d9e215e8983a1.png "Rendered by QuickLaTeX.com")大小的 4D 动力定位矩阵，其中 N 是列数，C 是组件数，2*2 维是最后一列的排列。最后一列可以有四种不同的组合。他们是 00，01，10，11。
矩阵的每个单元 **dp[i][j][row1][row2]** 给出了当最后一列中的排列是 row1，row2 时，在 I 列中具有 j 个分量的方式的数量。如果当前子问题已经过评估，即 DP[列][组件][行 1][行 2]！= -1，然后使用这个结果，否则递归计算值。

*   **基本情况:**当列数变得大于 N 时，则返回 0。如果列的数量等于 N，那么答案取决于组件的数量。如果分量等于 C，则返回 1，否则返回 0。
*   **情况 1** :前一列所在行颜色相同({0，0}或{1，1})时。
    在这种情况下，如果当前列的行中有不同的值({0，1}或{1，0})，则组件将增加 1。如果当前列具有相反的颜色，但其行中具有相同的值，则组件也将增加 1。也就是说，当前列有{1，1}，而前一列有{0，0}。或者当前列有{0，0}，而前一列有{1，1}。当前列与前一列的组合相同时，组件保持不变。
*   **情况 2** :上一列所在行颜色不同({0，1}或{1，0})时。
    在这种情况下，如果当前列的组合与其前一列完全相反，则组件将增加 2。即当前列为{1，0}而前一列为{0，1}时。或者当前列为{0，1}，前一列为{1，0}。在所有其他情况下，组件保持不变。

以下是上述方法的实现:

## C++

```
// C++ implementation to find the
// number of ways to make exactly
// C components in a 2 * N matrix

#include <bits/stdc++.h>
using namespace std;

// row1 and row2 are one
// when both are same colored
int n, k;
int dp[1024][2048][2][2];

// Function to find the number of
// ways to make exactly C components
// in a 2 * N matrix
int Ways(int col, int comp,
         int row1, int row2)
{

    // if No of components
    // at any stage exceeds
    // the given number
    // then base case
    if (comp > k)
        return 0;

    if (col > n) {
        if (comp == k)
            return 1;
        else
            return 0;
    }

    // Condition to check
    // if already visited
    if (dp[col][comp][row1][row2] != -1)
        return dp[col][comp][row1][row2];

    // if not visited previously
    else {
        int ans = 0;

        // At the first column
        if (col == 1) {

            // color {white, white} or
            // {black, black}
            ans
                = (ans
                   + Ways(col + 1, comp + 1, 0, 0)
                   + Ways(col + 1, comp + 1, 1, 1));

            // Color {white, black} or
            // {black, white}
            ans
                = (ans
                   + Ways(col + 1, comp + 2, 0, 1)
                   + Ways(col + 1, comp + 2, 1, 0));
        }
        else {

            // If previous both
            // rows have same color
            if ((row1 && row2)
                || (!row1 && !row2)) {

                // Fill with {same, same} and
                // {white, black} and {black, white}
                ans = (((ans
                         + Ways(col + 1, comp + 1, 0, 0))
                        + Ways(col + 1, comp + 1, 1, 0))
                       + Ways(col + 1, comp + 1, 0, 1));

                // Fill with same without
                // increase in component
                // as it has been
                // counted previously
                ans = (ans
                       + Ways(col + 1, comp, 1, 1));
            }

            // When previous rows
            // had {white, black}
            if (row1 && !row2) {
                ans = (((ans
                         + Ways(col + 1, comp, 0, 0))
                        + Ways(col + 1, comp, 1, 1))
                       + Ways(col + 1, comp, 1, 0));
                ans = (ans
                       + Ways(col + 1, comp + 2, 0, 1));
            }

            // When previous rows
            // had {black, white}
            if (!row1 && row2) {
                ans = (((ans
                         + Ways(col + 1, comp, 0, 0))
                        + Ways(col + 1, comp, 1, 1))
                       + Ways(col + 1, comp, 0, 1));
                ans = (ans
                       + Ways(col + 1, comp + 2, 1, 0));
            }
        }

        // Memoization
        return dp[col][comp][row1][row2] = ans;
    }
}

// Driver Code
signed main()
{
    n = 2;
    k = 1;
    memset(dp, -1, sizeof(dp));

    // Initially at first column
    // with 0 components
    cout << Ways(1, 0, 0, 0);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// number of ways to make exactly
// C components in a 2 * N matrix
class GFG{

// row1 and row2 are one
// when both are same colored
static int n, k;
static int [][][][]dp = new int[1024][2048][2][2];

// Function to find the number of
// ways to make exactly C components
// in a 2 * N matrix
static int Ways(int col, int comp,
                int row1, int row2)
{

    // if No of components
    // at any stage exceeds
    // the given number
    // then base case
    if (comp > k)
        return 0;

    if (col > n)
    {
        if (comp == k)
            return 1;
        else
            return 0;
    }

    // Condition to check
    // if already visited
    if (dp[col][comp][row1][row2] != -1)
        return dp[col][comp][row1][row2];

    // if not visited previously
    else
    {
        int ans = 0;

        // At the first column
        if (col == 1)
        {

            // color {white, white} or
            // {black, black}
            ans = (ans + Ways(col + 1, comp + 1, 0, 0) +
                         Ways(col + 1, comp + 1, 1, 1));

            // Color {white, black} or
            // {black, white}
            ans = (ans + Ways(col + 1, comp + 2, 0, 1) +
                         Ways(col + 1, comp + 2, 1, 0));
        }
        else
        {

            // If previous both
            // rows have same color
            if ((row1 > 0 && row2 > 0) ||
                (row1 == 0 && row2 ==0))
            {

                // Fill with {same, same} and
                // {white, black} and {black, white}
                ans = (((ans +
                         Ways(col + 1, comp + 1, 0, 0)) +
                         Ways(col + 1, comp + 1, 1, 0)) +
                         Ways(col + 1, comp + 1, 0, 1));

                // Fill with same without
                // increase in component
                // as it has been
                // counted previously
                ans = (ans +
                       Ways(col + 1, comp, 1, 1));
            }

            // When previous rows
            // had {white, black}
            if (row1 > 0 && row2 == 0)
            {
                ans = (((ans +
                         Ways(col + 1, comp, 0, 0)) +
                         Ways(col + 1, comp, 1, 1)) +
                         Ways(col + 1, comp, 1, 0));
                ans = (ans +
                       Ways(col + 1, comp + 2, 0, 1));
            }

            // When previous rows
            // had {black, white}
            if (row1 ==0 && row2 > 0)
            {
                ans = (((ans +
                         Ways(col + 1, comp, 0, 0)) +
                         Ways(col + 1, comp, 1, 1)) +
                         Ways(col + 1, comp, 0, 1));
                ans = (ans +
                       Ways(col + 1, comp + 2, 1, 0));
            }
        }

        // Memoization
        return dp[col][comp][row1][row2] = ans;
    }
}

// Driver Code
public static void main(String[] args)
{
    n = 2;
    k = 1;
    for (int i = 0; i < 1024; i++)
        for (int j = 0; j < 2048; j++)
            for (int k = 0; k < 2; k++)
                for (int l = 0; l < 2; l++)
                    dp[i][j][k][l] = -1;

    // Initially at first column
    // with 0 components
    System.out.print(Ways(1, 0, 0, 0));
}
}

// This code is contributed by Rajput-Ji
```

## C#

```
// C# implementation to find the
// number of ways to make exactly
// C components in a 2 * N matrix
using System;

class GFG{

// row1 and row2 are one
// when both are same colored
static int n, k;
static int [,,,]dp = new int[ 1024, 2048, 2, 2 ];

// Function to find the number of
// ways to make exactly C components
// in a 2 * N matrix
static int Ways(int col, int comp,
                int row1, int row2)
{

    // If No of components
    // at any stage exceeds
    // the given number
    // then base case
    if (comp > k)
        return 0;

    if (col > n)
    {
        if (comp == k)
            return 1;
        else
            return 0;
    }

    // Condition to check
    // if already visited
    if (dp[ col, comp, row1, row2 ] != -1)
        return dp[ col, comp, row1, row2 ];

    // If not visited previously
    else
    {
        int ans = 0;

        // At the first column
        if (col == 1)
        {

            // color {white, white} or
            // {black, black}
            ans = (ans + Ways(col + 1, comp + 1, 0, 0) +
                         Ways(col + 1, comp + 1, 1, 1));

            // Color {white, black} or
            // {black, white}
            ans = (ans + Ways(col + 1, comp + 2, 0, 1) +
                         Ways(col + 1, comp + 2, 1, 0));
        }
        else
        {

            // If previous both
            // rows have same color
            if ((row1 > 0 && row2 > 0) ||
                (row1 == 0 && row2 == 0))
            {

                // Fill with {same, same} and
                // {white, black} and {black, white}
                ans = (((ans +
                         Ways(col + 1, comp + 1, 0, 0)) +
                         Ways(col + 1, comp + 1, 1, 0)) +
                         Ways(col + 1, comp + 1, 0, 1));

                // Fill with same without
                // increase in component
                // as it has been
                // counted previously
                ans = (ans +
                       Ways(col + 1, comp, 1, 1));
            }

            // When previous rows
            // had {white, black}
            if (row1 > 0 && row2 == 0)
            {
                ans = (((ans +
                         Ways(col + 1, comp, 0, 0)) +
                         Ways(col + 1, comp, 1, 1)) +
                         Ways(col + 1, comp, 1, 0));
                ans = (ans +
                       Ways(col + 1, comp + 2, 0, 1));
            }

            // When previous rows
            // had {black, white}
            if (row1 == 0 && row2 > 0)
            {
                ans = (((ans +
                         Ways(col + 1, comp, 0, 0)) +
                         Ways(col + 1, comp, 1, 1)) +
                         Ways(col + 1, comp, 0, 1));
                ans = (ans +
                       Ways(col + 1, comp + 2, 1, 0));
            }
        }

        // Memoization
        return dp[ col, comp, row1, row2 ] = ans;
    }
}

// Driver Code
public static void Main(String[] args)
{
    n = 2;
    k = 1;

    for(int i = 0; i < 1024; i++)
       for(int j = 0; j < 2048; j++)
          for(int K = 0; K < 2; K++)
             for(int l = 0; l < 2; l++)
                dp[ i, j, K, l ] = -1;

    // Initially at first column
    // with 0 components
    Console.Write(Ways(1, 0, 0, 0));
}
}

// This code is contributed by Rajput-Ji
```

**Output:** 

```
2
```

**时间竞争:O(N * C)**T2】