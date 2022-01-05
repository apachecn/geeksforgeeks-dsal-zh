# 找出从(0，0)到(N-1，M-1)

的最小差路径

> 原文:[https://www . geeksforgeeks . org/find-最小差异路径-从 0-0 到 n-1-m-1/](https://www.geeksforgeeks.org/find-the-minimum-difference-path-from-0-0-to-n-1-m-1/)

给定两个 2D 阵列 **b[][]** 和**c[][]****N**行和 **M** 列。任务是沿着从 **(0，0)** 到**(N–1，M–1)**的路径，最小化 **b[i][j]s** 之和与 **c[i][j]s** 之和的绝对差。
**示例:**

> **输入:** b[][] = {{1，4}，{2，4}}，c[][] = {{3，2}，{3，1}}
> **输出:** 0
> 选择路径(0，0) - > (1，0) - > (1，1)
> b[I][j]s 的和为= 1+2+4 = 7
> c[I][j]s 的和为= 3 + 3 + 1 = 7 【T8

**方法:**答案独立于决定 **b[i][j]** 和 **c[i][j]** 的顺序和路径。因此，让我们考虑一个布尔表，如果 **(i，j)** 能够以 **k** 的最小差异达到，则 **dp[i][j][k]** 将为真。
如果是真的，那么对于单元格 **(i + 1，j)** 来说，要么是 **k + |b <sub>i+1，j</sub>–c<sub>I+1，j</sub> |** 要么是**| k –| b<sub>I+1，j</sub>–c<sub>I+1，j</sub>|**。正方形 **(i，j + 1)** 也是如此。因此，表格可以按照 **i** 和 **j** 的递增顺序填写。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

#define MAXI 50

int dp[MAXI][MAXI][MAXI * MAXI];
int n, m;

// Function to return the minimum difference
// path from (0, 0) to (N - 1, M - 1)
int minDifference(int x, int y, int k,
                  vector<vector<int> > b,
                  vector<vector<int> > c)
{

    // Terminating case
    if (x >= n or y >= m)
        return INT_MAX;

    // Base case
    if (x == n - 1 and y == m - 1) {
        int diff = b[x][y] - c[x][y];

        return min(abs(k - diff), abs(k + diff));
    }

    int& ans = dp[x][y][k];

    // If it is already visited
    if (ans != -1)
        return ans;

    ans = INT_MAX;

    int diff = b[x][y] - c[x][y];

    // Recursive calls
    ans = min(ans, minDifference(x + 1, y,
                                 abs(k + diff), b, c));
    ans = min(ans, minDifference(x, y + 1,
                                 abs(k + diff), b, c));

    ans = min(ans, minDifference(x + 1, y,
                                 abs(k - diff), b, c));
    ans = min(ans, minDifference(x, y + 1,
                                 abs(k - diff), b, c));

    // Return the value
    return ans;
}

// Driver code
int main()
{
    n = 2, m = 2;

    vector<vector<int> > b = { { 1, 4 }, { 2, 4 } };

    vector<vector<int> > c = { { 3, 2 }, { 3, 1 } };

    memset(dp, -1, sizeof(dp));

    // Function call
    cout << minDifference(0, 0, 0, b, c);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
    final static int MAXI = 50 ;

    static int dp[][][] = new int[MAXI][MAXI][MAXI * MAXI];
    static int n, m;
    final static int INT_MAX = Integer.MAX_VALUE;

    // Function to return the minimum difference
    // path from (0, 0) to (N - 1, M - 1)
    static int minDifference(int x, int y, int k,
                             int b[][], int c[][])
    {

        // Terminating case
        if (x >= n || y >= m)
            return INT_MAX;

        // Base case
        if (x == n - 1 && y == m - 1)
        {
            int diff = b[x][y] - c[x][y];

            return Math.min(Math.abs(k - diff),
                            Math.abs(k + diff));
        }

        int ans = dp[x][y][k];

        // If it is already visited
        if (ans != -1)
            return ans;

        ans = INT_MAX;

        int diff = b[x][y] - c[x][y];

        // Recursive calls
        ans = Math.min(ans, minDifference(x + 1, y,
              Math.abs(k + diff), b, c));

        ans = Math.min(ans, minDifference(x, y + 1,
              Math.abs(k + diff), b, c));

        ans = Math.min(ans, minDifference(x + 1, y,
              Math.abs(k - diff), b, c));
        ans = Math.min(ans, minDifference(x, y + 1,
              Math.abs(k - diff), b, c));

        // Return the value
        return ans;
    }

    // Driver code
    public static void main (String[] args)
    {
        n = 2; m = 2;

        int b[][] = { { 1, 4 }, { 2, 4 } };

        int c[][] = { { 3, 2 }, { 3, 1 } };

        for(int i = 0; i < MAXI; i++)
        {
            for(int j = 0; j < MAXI; j++)
            {
                for(int k = 0; k < MAXI * MAXI; k++)
                {
                    dp[i][j][k] = -1;
                }
            }
        }

        // Function call
        System.out.println(minDifference(0, 0, 0, b, c));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import numpy as np
import sys

MAXI = 50

INT_MAX = sys.maxsize

dp = np.ones((MAXI, MAXI, MAXI * MAXI));
dp *= -1

# Function to return the minimum difference
# path from (0, 0) to (N - 1, M - 1)
def minDifference(x, y, k, b, c) :

    # Terminating case
    if (x >= n or y >= m) :
        return INT_MAX;

    # Base case
    if (x == n - 1 and y == m - 1) :
        diff = b[x][y] - c[x][y];

        return min(abs(k - diff), abs(k + diff));

    ans = dp[x][y][k];

    # If it is already visited
    if (ans != -1) :
        return ans;

    ans = INT_MAX;

    diff = b[x][y] - c[x][y];

    # Recursive calls
    ans = min(ans, minDifference(x + 1, y,
                      abs(k + diff), b, c));

    ans = min(ans, minDifference(x, y + 1,
                    abs(k + diff), b, c));

    ans = min(ans, minDifference(x + 1, y,
                    abs(k - diff), b, c));

    ans = min(ans, minDifference(x, y + 1,
                    abs(k - diff), b, c));

    # Return the value
    return ans;

# Driver code
if __name__ == "__main__" :

    n = 2; m = 2; b = [ [ 1, 4 ], [ 2, 4 ] ];

    c = [ [ 3, 2 ], [ 3, 1 ] ];

    # Function call
    print(minDifference(0, 0, 0, b, c));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    static int MAXI = 50 ;

    static int [,,]dp = new int[MAXI, MAXI,
                                MAXI * MAXI];
    static int n, m;
    static int INT_MAX = int.MaxValue;

    // Function to return the minimum difference
    // path from (0, 0) to (N - 1, M - 1)
    static int minDifference(int x, int y, int k,
                             int [,]b, int [,]c)
    {
        int diff = 0;

        // Terminating case
        if (x >= n || y >= m)
            return INT_MAX;

        // Base case
        if (x == n - 1 && y == m - 1)
        {
            diff = b[x, y] - c[x, y];

            return Math.Min(Math.Abs(k - diff),
                            Math.Abs(k + diff));
        }

        int ans = dp[x, y, k];

        // If it is already visited
        if (ans != -1)
            return ans;

        ans = INT_MAX;

        diff = b[x, y] - c[x, y];

        // Recursive calls
        ans = Math.Min(ans, minDifference(x + 1, y,
              Math.Abs(k + diff), b, c));

        ans = Math.Min(ans, minDifference(x, y + 1,
              Math.Abs(k + diff), b, c));

        ans = Math.Min(ans, minDifference(x + 1, y,
              Math.Abs(k - diff), b, c));

        ans = Math.Min(ans, minDifference(x, y + 1,
              Math.Abs(k - diff), b, c));

        // Return the value
        return ans;
    }

    // Driver code
    public static void Main ()
    {
        n = 2; m = 2;

        int [,]b = { { 1, 4 }, { 2, 4 } };

        int [,]c = { { 3, 2 }, { 3, 1 } };

        for(int i = 0; i < MAXI; i++)
        {
            for(int j = 0; j < MAXI; j++)
            {
                for(int k = 0; k < MAXI * MAXI; k++)
                {
                    dp[i, j, k] = -1;
                }
            }
        }

        // Function call
        Console.WriteLine(minDifference(0, 0, 0, b, c));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

    // JavaScript implementation of the approach

    let MAXI = 50 ;

    let dp = new Array(MAXI);
    let n, m;
    let INT_MAX = Number.MAX_VALUE;

    // Function to return the minimum difference
    // path from (0, 0) to (N - 1, M - 1)
    function minDifference(x, y, k, b, c)
    {

        // Terminating case
        if (x >= n || y >= m)
            return INT_MAX;

        // Base case
        if (x == n - 1 && y == m - 1)
        {
            let diff = b[x][y] - c[x][y];

            return Math.min(Math.abs(k - diff),
                            Math.abs(k + diff));
        }

        let ans = dp[x][y][k];

        // If it is already visited
        if (ans != -1)
            return ans;

        ans = INT_MAX;

        let diff = b[x][y] - c[x][y];

        // Recursive calls
        ans = Math.min(ans, minDifference(x + 1, y,
              Math.abs(k + diff), b, c));

        ans = Math.min(ans, minDifference(x, y + 1,
              Math.abs(k + diff), b, c));

        ans = Math.min(ans, minDifference(x + 1, y,
              Math.abs(k - diff), b, c));
        ans = Math.min(ans, minDifference(x, y + 1,
              Math.abs(k - diff), b, c));

        // Return the value
        return ans;
    }

    n = 2; m = 2;

    let b = [ [ 1, 4 ], [ 2, 4 ] ];

    let c = [ [ 3, 2 ], [ 3, 1 ] ];

    for(let i = 0; i < MAXI; i++)
    {
      dp[i] = new Array(MAXI);
      for(let j = 0; j < MAXI; j++)
      {
          dp[i][j] = new Array(MAXI * MAXI);
        for(let k = 0; k < MAXI * MAXI; k++)
        {
          dp[i][j][k] = -1;
        }
      }
    }

    // Function call
    document.write(minDifference(0, 0, 0, b, c));

</script>
```

**Output:** 

```
0
```