# 到达矩阵任何边界边的最小步数|设置 1

> 原文:[https://www . geeksforgeeks . org/到达矩阵任何边界边缘的最小步骤/](https://www.geeksforgeeks.org/minimum-steps-to-reach-any-of-the-boundary-edges-of-a-matrix/)

给定一个 N×M 矩阵，其中 a <sub>i，j</sub> = 1 表示单元格不为空，a <sub>i，j</sub> = 0 表示单元格为空，a <sub>i，j</sub> = 2 表示您正站在该单元格处。您可以垂直向上或向下移动，水平向左或向右移动到任何空单元格。任务是找到到达矩阵任何边界边的最小步数。如果无法到达任何边界边缘，打印-1。
**注意**:整个矩阵中只会有一个值为 2 的单元格。
**举例:**

```
Input: matrix[] = {1, 1, 1, 0, 1}
                  {1, 0, 2, 0, 1} 
                  {0, 0, 1, 0, 1}
                  {1, 0, 1, 1, 0} 
Output: 2
Move to the right and then move 
upwards to reach the nearest boundary
edge. 

Input: matrix[] = {1, 1, 1, 1, 1}
                  {1, 0, 2, 0, 1} 
                  {1, 0, 1, 0, 1}
                  {1, 1, 1, 1, 1}
Output: -1 
```

**方法**:问题可以用动态规划的方法解决。下面给出的是解决上述问题的算法。

*   找出矩阵中有“2”的位置。
*   初始化两个与矩阵大小相同的二维数组。存储到达任何索引 I、j 和 *vis[][]* 的最小步数的 *dp[][]* 标记之前是否访问过任何特定的 I、j 位置。
*   调用具有*基本情况*的递归函数如下:
    1.  如果在任意点的遍历到达任意边界边，返回 0。
    2.  如果点位置 n，m 先前已经存储了最小步数，则返回 dp[n][m]。
*   用从位置 n，m 可以完成的所有可能的四个移动再次调用递归。这些移动只有在 *mat[n][m]* 为 0 并且该位置以前没有被访问过时才是可能的。
*   存储四个移动中的最小值。
*   如果递归返回任何小于 1e9 的值，我们将它存储为最大值，那么就有一个答案，否则就没有任何答案。

以下是上述方法的实现:

## C++

```
// C++ program to find Minimum steps
// to reach any of the boundary
// edges of a matrix
#include <bits/stdc++.h>
using namespace std;
#define r 4
#define col 5

// Function to find out minimum steps
int findMinSteps(int mat[r][col], int n, int m, int dp[r][col], bool vis[r][col])
{
    // boundary edges reached
    if (n == 0 || m == 0 || n == (r - 1) || m == (col - 1)) {
        return 0;
    }

    // already had a route through this
    // point, hence no need to re-visit
    if (dp[n][m] != -1)
        return dp[n][m];

    // visiting a position
    vis[n][m] = true;

    int ans1, ans2, ans3, ans4;

    ans1 = ans2 = ans3 = ans4 = 1e9;

    // vertically up
    if (mat[n - 1][m] == 0) {
        if (!vis[n - 1][m])
            ans1 = 1 + findMinSteps(mat, n - 1, m, dp, vis);
    }

    // horizontally right
    if (mat[n][m + 1] == 0) {
        if (!vis[n][m + 1])
            ans2 = 1 + findMinSteps(mat, n, m + 1, dp, vis);
    }

    // horizontally left
    if (mat[n][m - 1] == 0) {
        if (!vis[n][m - 1])
            ans3 = 1 + findMinSteps(mat, n, m - 1, dp, vis);
    }

    // vertically down
    if (mat[n + 1][m] == 0) {
        if (!vis[n + 1][m])
            ans4 = 1 + findMinSteps(mat, n + 1, m, dp, vis);
    }

    // minimum of every path
    dp[n][m] = min(ans1, min(ans2, min(ans3, ans4)));
    return dp[n][m];
}

// Function that returns the minimum steps
int minimumSteps(int mat[r][col], int n, int m)
{
    // index to store the location at
    // which you are standing
    int twox = -1;
    int twoy = -1;

    // find '2' in the matrix
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            if (mat[i][j] == 2) {
                twox = i;
                twoy = j;
                break;
            }
        }
        if (twox != -1)
            break;
    }

    // Initialize dp matrix with -1
    int dp[r][col];
    memset(dp, -1, sizeof dp);

    // Initialize vis matrix with false
    bool vis[r][col];
    memset(vis, false, sizeof vis);

    // Call function to find out minimum steps
    // using memoization and recursion
    int res = findMinSteps(mat, twox, twoy, dp, vis);

    // if not possible
    if (res >= 1e9)
        return -1;
    else
        return res;
}

// Driver Code
int main()
{
    int mat[r][col] = { { 1, 1, 1, 0, 1 },
                      { 1, 0, 2, 0, 1 },
                      { 0, 0, 1, 0, 1 },
                      { 1, 0, 1, 1, 0 } };

    cout << minimumSteps(mat, r, col);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find Minimum steps
// to reach any of the boundary
// edges of a matrix
class Solution
{
static final int  r=4,c=5;

// Function to find out minimum steps
static int findMinSteps(int mat[][], int n, int m, int dp[][], boolean vis[][])
{
    // boundary edges reached
    if (n == 0 || m == 0 || n == (r - 1) || m == (c - 1)) {
        return 0;
    }

    // already had a route through this
    // point, hence no need to re-visit
    if (dp[n][m] != -1)
        return dp[n][m];

    // visiting a position
    vis[n][m] = true;

    int ans1, ans2, ans3, ans4;

    ans1 = ans2 = ans3 = ans4 = (int)1e9;

    // vertically up
    if (mat[n - 1][m] == 0) {
        if (!vis[n - 1][m])
            ans1 = 1 + findMinSteps(mat, n - 1, m, dp, vis);
    }

    // horizontally right
    if (mat[n][m + 1] == 0) {
        if (!vis[n][m + 1])
            ans2 = 1 + findMinSteps(mat, n, m + 1, dp, vis);
    }

    // horizontally left
    if (mat[n][m - 1] == 0) {
        if (!vis[n][m - 1])
            ans3 = 1 + findMinSteps(mat, n, m - 1, dp, vis);
    }

    // vertically down
    if (mat[n + 1][m] == 0) {
        if (!vis[n + 1][m])
            ans4 = 1 + findMinSteps(mat, n + 1, m, dp, vis);
    }

    // minimum of every path
    dp[n][m] = Math.min(ans1, Math.min(ans2, Math.min(ans3, ans4)));
    return dp[n][m];
}

// Function that returns the minimum steps
static int minimumSteps(int mat[][], int n, int m)
{
    // index to store the location at
    // which you are standing
    int twox = -1;
    int twoy = -1;

    // find '2' in the matrix
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            if (mat[i][j] == 2) {
                twox = i;
                twoy = j;
                break;
            }
        }
        if (twox != -1)
            break;
    }

    // Initialize dp matrix with -1
    int dp[][]=new int[r][r];
    for(int j=0;j<r;j++)
    for(int i=0;i<r;i++)dp[j][i]=-1;

    // Initialize vis matrix with false
    boolean vis[][]= new boolean[r][r];
    for(int j=0;j<r;j++)
    for(int i=0;i<r;i++)vis[j][i]=false;

    // Call function to find out minimum steps
    // using memoization and recursion
    int res = findMinSteps(mat, twox, twoy, dp, vis);

    // if not possible
    if (res >= 1e9)
        return -1;
    else
        return res;
}

// Driver Code
public static void main(String args[])
{
    int mat[][] = { { 1, 1, 1, 0, 1 },
                      { 1, 0, 2, 0, 1 },
                      { 0, 0, 1, 0, 1 },
                      { 1, 0, 1, 1, 0 } };

    System.out.println( minimumSteps(mat, r, c));
}
}
//contributed by Arnab Kundu
```

## 计算机编程语言

```
# Python program to find Minimum steps
# to reach any of the boundary
# edges of a matrix

r=4
col=5

# Function to find out minimum steps
def findMinSteps(mat, n, m, dp,vis):

    # boundary edges reached
    if (n == 0 or m == 0 or n == (r - 1) or m == (col - 1)):
        return 0

    # already had a route through this
    # point, hence no need to re-visit
    if (dp[n][m] != -1):
        return dp[n][m]

    # visiting a position
    vis[n][m] = True

    ans1, ans2, ans3, ans4=10**9,10**9,10**9,10**9

    # vertically up
    if (mat[n - 1][m] == 0):
        if (vis[n - 1][m]==False):
            ans1 = 1 + findMinSteps(mat, n - 1, m, dp, vis)

    # horizontally right
    if (mat[n][m + 1] == 0):
        if (vis[n][m + 1]==False):
            ans2 = 1 + findMinSteps(mat, n, m + 1, dp, vis)

    # horizontally left
    if (mat[n][m - 1] == 0):
        if (vis[n][m - 1]==False):
            ans3 = 1 + findMinSteps(mat, n, m - 1, dp, vis)

    # vertically down
    if (mat[n + 1][m] == 0):
        if (vis[n + 1][m]==False):
            ans4 = 1 + findMinSteps(mat, n + 1, m, dp, vis)

    # minimum of every path
    dp[n][m] = min(ans1, min(ans2, min(ans3, ans4)))
    return dp[n][m]

# Function that returns the minimum steps
def minimumSteps(mat, n, m):

    # index to store the location at
    # which you are standing
    twox = -1
    twoy = -1

    # find '2' in the matrix
    for i in range(n):
        for j in range(m):
            if (mat[i][j] == 2):
                twox = i
                twoy = j
                break

        if (twox != -1):
            break

    # Initialize dp matrix with -1
    dp=[[-1 for i in range(col)] for i in range(r)]

    # Initialize vis matrix with false
    vis=[[False for i in range(col)] for i in range(r)]

    # Call function to find out minimum steps
    # using memoization and recursion
    res = findMinSteps(mat, twox, twoy, dp, vis)

    # if not possible
    if (res >= 10**9):
        return -1
    else:
        return res

# Driver Code

mat= [ [ 1, 1, 1, 0, 1 ],
      [ 1, 0, 2, 0, 1 ],
      [ 0, 0, 1, 0, 1 ],
      [ 1, 0, 1, 1, 0 ] ]

print(minimumSteps(mat, r, col))

#this is contributed by Mohit kumar 29
```

## C#

```
// C# program to find Minimum steps
// to reach any of the boundary
// edges of a matrix

using System;

class Solution
{
static int r=4,c=5;

    // Function to find out minimum steps
    static int findMinSteps(int [,]mat, int n, int m, int [,]dp, bool [,]vis)
    {
        // boundary edges reached
        if (n == 0 || m == 0 || n == (r - 1) || m == (c - 1)) {
            return 0;
        }

        // already had a route through this
        // point, hence no need to re-visit
        if (dp[n,m] != -1)
            return dp[n,m];

        // visiting a position
        vis[n,m] = true;

        int ans1, ans2, ans3, ans4;

        ans1 = ans2 = ans3 = ans4 = (int)1e9;

        // vertically up
        if (mat[n - 1,m] == 0) {
            if (!vis[n - 1,m])
                ans1 = 1 + findMinSteps(mat, n - 1, m, dp, vis);
        }

        // horizontally right
        if (mat[n,m + 1] == 0) {
            if (!vis[n,m + 1])
                ans2 = 1 + findMinSteps(mat, n, m + 1, dp, vis);
        }

        // horizontally left
        if (mat[n,m - 1] == 0) {
            if (!vis[n,m - 1])
                ans3 = 1 + findMinSteps(mat, n, m - 1, dp, vis);
        }

        // vertically down
        if (mat[n + 1,m] == 0) {
            if (!vis[n + 1,m])
                ans4 = 1 + findMinSteps(mat, n + 1, m, dp, vis);
        }

        // minimum of every path
        dp[n,m] = Math.Min(ans1, Math.Min(ans2, Math.Min(ans3, ans4)));
        return dp[n,m];
    }

    // Function that returns the minimum steps
    static int minimumSteps(int [,]mat, int n, int m)
    {
        // index to store the location at
        // which you are standing
        int twox = -1;
        int twoy = -1;

        // find '2' in the matrix
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (mat[i,j] == 2) {
                    twox = i;
                    twoy = j;
                    break;
                }
            }
            if (twox != -1)
                break;
        }

        // Initialize dp matrix with -1
        int [,]dp = new int[r,r];
        for(int j=0;j<r;j++)
            for(int i=0;i<r;i++)
                dp[j,i]=-1;

        // Initialize vis matrix with false
        bool [,]vis= new bool [r,r];
        for(int j=0;j<r;j++)
            for(int i=0;i<r;i++)
                vis[j,i]=false;

        // Call function to find out minimum steps
        // using memoization and recursion
        int res = findMinSteps(mat, twox, twoy, dp, vis);

        // if not possible
        if (res >= 1e9)
            return -1;
        else
            return res;
    }

    // Driver Code
    public static void Main()
    {
        int [,]mat = { { 1, 1, 1, 0, 1 },
                        { 1, 0, 2, 0, 1 },
                        { 0, 0, 1, 0, 1 },
                        { 1, 0, 1, 1, 0 }, };

        Console.WriteLine(minimumSteps(mat, r, c));
    }
    // This code is contributed by Ryuga

}
```

## java 描述语言

```
<script>
    // Javascript program to find Minimum steps
    // to reach any of the boundary
    // edges of a matrix

    let  r=4,c=5;

    // Function to find out minimum steps
    function findMinSteps(mat, n, m, dp, vis)
    {
        // boundary edges reached
        if (n == 0 || m == 0 || n == (r - 1) || m == (c - 1)) {
            return 0;
        }

        // already had a route through this
        // point, hence no need to re-visit
        if (dp[n][m] != -1)
            return dp[n][m];

        // visiting a position
        vis[n][m] = true;

        let ans1, ans2, ans3, ans4;

        ans1 = ans2 = ans3 = ans4 = 1e9;

        // vertically up
        if (mat[n - 1][m] == 0) {
            if (!vis[n - 1][m])
                ans1 = 1 + findMinSteps(mat, n - 1, m, dp, vis);
        }

        // horizontally right
        if (mat[n][m + 1] == 0) {
            if (!vis[n][m + 1])
                ans2 = 1 + findMinSteps(mat, n, m + 1, dp, vis);
        }

        // horizontally left
        if (mat[n][m - 1] == 0) {
            if (!vis[n][m - 1])
                ans3 = 1 + findMinSteps(mat, n, m - 1, dp, vis);
        }

        // vertically down
        if (mat[n + 1][m] == 0) {
            if (!vis[n + 1][m])
                ans4 = 1 + findMinSteps(mat, n + 1, m, dp, vis);
        }

        // minimum of every path
        dp[n][m] = Math.min(ans1, Math.min(ans2, Math.min(ans3, ans4)));
        return dp[n][m];
    }

    // Function that returns the minimum steps
    function minimumSteps(mat, n, m)
    {
        // index to store the location at
        // which you are standing
        let twox = -1;
        let twoy = -1;

        // find '2' in the matrix
        for (let i = 0; i < n; i++) {
            for (let j = 0; j < m; j++) {
                if (mat[i][j] == 2) {
                    twox = i;
                    twoy = j;
                    break;
                }
            }
            if (twox != -1)
                break;
        }

        // Initialize dp matrix with -1
        let dp = new Array(r);
        for(let j=0;j<r;j++)
        {
            dp[j] = new Array(r);
            for(let i=0;i<r;i++)
            {
                dp[j][i]=-1;
            }
        }

        // Initialize vis matrix with false
        let vis = new Array(r);
        for(let j=0;j<r;j++)
        {
            vis[j] = new Array(r);
            for(let i=0;i<r;i++)
            {
                vis[j][i]=false;
            }
        }

        // Call function to find out minimum steps
        // using memoization and recursion
        let res = findMinSteps(mat, twox, twoy, dp, vis);

        // if not possible
        if (res >= 1e9)
            return -1;
        else
            return res;
    }

    let mat = [ [ 1, 1, 1, 0, 1 ],
               [ 1, 0, 2, 0, 1 ],
               [ 0, 0, 1, 0, 1 ],
               [ 1, 0, 1, 1, 0 ] ];

    document.write( minimumSteps(mat, r, c));

// This code is contributed by suresh07.
</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(N^2)
**辅助空间:** O(N^2)
[到达矩阵任意边界边的最小步数| Set-2](https://www.geeksforgeeks.org/minimum-steps-to-reach-any-of-the-boundary-edges-of-a-matrix-set-2/)