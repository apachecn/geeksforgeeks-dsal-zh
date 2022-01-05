# 平均值最大的路径

> 原文:[https://www.geeksforgeeks.org/path-maximum-average-value/](https://www.geeksforgeeks.org/path-maximum-average-value/)

给定一个大小为 N*N 的正方形矩阵，其中每个单元格都与一个特定的成本相关联。路径被定义为特定的单元格序列，从左上角的单元格开始仅向右或向下移动，并在右下角的单元格结束。我们希望找到一条在所有现有路径上具有最大平均值的路径。平均值计算为总成本除以路径中访问的单元数。
**例:**

```
Input : Matrix = [1, 2, 3
                  4, 5, 6
                  7, 8, 9]
Output : 5.8
Path with maximum average is, 1 -> 4 -> 7 -> 8 -> 9
Sum of the path is 29 and average is 29/5 = 5.8
```

一个有趣的观察是，唯一允许的移动是向下和向右，我们需要 N-1 次向下移动和 N-1 次向右移动才能到达目的地(最右下方)。因此，从左上角到右下角的任何路径都需要 2N–1 个单元格。在平均值中，分母是固定的，我们只需要最大化分子。因此我们基本上需要找到最大和路径。计算路径的最大和是一个经典的动态规划问题，如果 dp[i][j]表示从(0，0)到单元(I，j)的最大和，那么在每个单元(I，j)，我们如下更新 dp[i][j]，

```
for all i, 1 <= i <= N
   dp[i][0] = dp[i-1][0] + cost[i][0];    
for all j, 1 <= j <= N
   dp[0][j] = dp[0][j-1] + cost[0][j];            
otherwise    
   dp[i][j] = max(dp[i-1][j], dp[i][j-1]) + cost[i][j]; 
```

一旦我们得到所有路径的最大和，我们将这个和除以(2N–1)，我们将得到我们的最大平均值。

## C++

```
//    C/C++ program to find maximum average cost path
#include <bits/stdc++.h>
using namespace std;

// Maximum number of rows and/or columns
const int M = 100;

// method returns maximum average of all path of
// cost matrix
double maxAverageOfPath(int cost[M][M], int N)
{
    int dp[N+1][N+1];
    dp[0][0] = cost[0][0];

    /* Initialize first column of total cost(dp) array */
    for (int i = 1; i < N; i++)
        dp[i][0] = dp[i-1][0] + cost[i][0];

    /* Initialize first row of dp array */
    for (int j = 1; j < N; j++)
        dp[0][j] = dp[0][j-1] + cost[0][j];

    /* Construct rest of the dp array */
    for (int i = 1; i < N; i++)
        for (int j = 1; j <= N; j++)
            dp[i][j] = max(dp[i-1][j],
                          dp[i][j-1]) + cost[i][j];

    // divide maximum sum by constant path
    // length : (2N - 1) for getting average
    return (double)dp[N-1][N-1] / (2*N-1);
}

/* Driver program to test above functions */
int main()
{
    int cost[M][M] = { {1, 2, 3},
        {6, 5, 4},
        {7, 3, 9}
    };
    printf("%f", maxAverageOfPath(cost, 3));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA Code for Path with maximum average
// value
class GFG {

    // method returns maximum average of all
    // path of cost matrix
    public static double maxAverageOfPath(int cost[][],
                                               int N)
    {
        int dp[][] = new int[N+1][N+1];
        dp[0][0] = cost[0][0];

        /* Initialize first column of total cost(dp)
           array */
        for (int i = 1; i < N; i++)
            dp[i][0] = dp[i-1][0] + cost[i][0];

        /* Initialize first row of dp array */
        for (int j = 1; j < N; j++)
            dp[0][j] = dp[0][j-1] + cost[0][j];

        /* Construct rest of the dp array */
        for (int i = 1; i < N; i++)
            for (int j = 1; j < N; j++)
                dp[i][j] = Math.max(dp[i-1][j],
                           dp[i][j-1]) + cost[i][j];

        // divide maximum sum by constant path
        // length : (2N - 1) for getting average
        return (double)dp[N-1][N-1] / (2 * N - 1);
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        int cost[][] = {{1, 2, 3},
                        {6, 5, 4},
                        {7, 3, 9}};

        System.out.println(maxAverageOfPath(cost, 3));
    }
}
// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# Python program to find
# maximum average cost path

# Maximum number of rows
# and/or columns
M = 100

# method returns maximum average of
# all path of cost matrix
def maxAverageOfPath(cost, N):

    dp = [[0 for i in range(N + 1)] for j in range(N + 1)]
    dp[0][0] = cost[0][0]

    # Initialize first column of total cost(dp) array
    for i in range(1, N):
        dp[i][0] = dp[i - 1][0] + cost[i][0]

    # Initialize first row of dp array
    for j in range(1, N):
        dp[0][j] = dp[0][j - 1] + cost[0][j]

    # Construct rest of the dp array
    for i in range(1, N):
        for j in range(1, N):
            dp[i][j] = max(dp[i - 1][j],
                        dp[i][j - 1]) + cost[i][j]

    # divide maximum sum by constant path
    # length : (2N - 1) for getting average
    return dp[N - 1][N - 1] / (2 * N - 1)

# Driver program to test above function
cost = [[1, 2, 3],
        [6, 5, 4],
        [7, 3, 9]]

print(maxAverageOfPath(cost, 3))

# This code is contributed by Soumen Ghosh.
```

## C#

```
// C# Code for Path with maximum average
// value
using System;
class GFG {

    // method returns maximum average of all
    // path of cost matrix
    public static double maxAverageOfPath(int [,]cost,
                                               int N)
    {
        int [,]dp = new int[N+1,N+1];
        dp[0,0] = cost[0,0];

        /* Initialize first column of total cost(dp)
           array */
        for (int i = 1; i < N; i++)
            dp[i, 0] = dp[i - 1,0] + cost[i, 0];

        /* Initialize first row of dp array */
        for (int j = 1; j < N; j++)
            dp[0, j] = dp[0,j - 1] + cost[0, j];

        /* Construct rest of the dp array */
        for (int i = 1; i < N; i++)
            for (int j = 1; j < N; j++)
                dp[i, j] = Math.Max(dp[i - 1, j],
                        dp[i,j - 1]) + cost[i, j];

        // divide maximum sum by constant path
        // length : (2N - 1) for getting average
        return (double)dp[N - 1, N - 1] / (2 * N - 1);
    }

    // Driver Code
    public static void Main()
    {
        int [,]cost = {{1, 2, 3},
                       {6, 5, 4},
                       {7, 3, 9}};

        Console.Write(maxAverageOfPath(cost, 3));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Php program to find maximum average cost path

// method returns maximum average of all path of
// cost matrix
function maxAverageOfPath($cost, $N)
{
    $dp = array(array()) ;
    $dp[0][0] = $cost[0][0];

    /* Initialize first column of total cost(dp) array */
    for ($i = 1; $i < $N; $i++)
        $dp[$i][0] = $dp[$i-1][0] + $cost[$i][0];

    /* Initialize first row of dp array */
    for ($j = 1; $j < $N; $j++)
        $dp[0][$j] = $dp[0][$j-1] + $cost[0][$j];

    /* Construct rest of the dp array */
    for ($i = 1; $i < $N; $i++)
    {
        for ($j = 1; $j <= $N; $j++)
            $dp[$i][$j] = max($dp[$i-1][$j],$dp[$i][$j-1]) + $cost[$i][$j];
    }
    // divide maximum sum by constant path
    // length : (2N - 1) for getting average
    return $dp[$N-1][$N-1] / (2*$N-1);
}

    // Driver code
    $cost = array(array(1, 2, 3),
            array( 6, 5, 4),
            array(7, 3, 9) ) ;

    echo maxAverageOfPath($cost, 3) ;

    // This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

    // JavaScript Code for Path with maximum average value

    // method returns maximum average of all
    // path of cost matrix
    function maxAverageOfPath(cost, N)
    {
        let dp = new Array(N+1);
        for (let i = 0; i < N + 1; i++)
        {
            dp[i] = new Array(N + 1);
            for (let j = 0; j < N + 1; j++)
            {
                dp[i][j] = 0;
            }
        }
        dp[0][0] = cost[0][0];

        /* Initialize first column of total cost(dp)
           array */
        for (let i = 1; i < N; i++)
            dp[i][0] = dp[i-1][0] + cost[i][0];

        /* Initialize first row of dp array */
        for (let j = 1; j < N; j++)
            dp[0][j] = dp[0][j-1] + cost[0][j];

        /* Construct rest of the dp array */
        for (let i = 1; i < N; i++)
            for (let j = 1; j < N; j++)
                dp[i][j] = Math.max(dp[i-1][j],
                           dp[i][j-1]) + cost[i][j];

        // divide maximum sum by constant path
        // length : (2N - 1) for getting average
        return dp[N-1][N-1] / (2 * N - 1);
    }

    let cost = [[1, 2, 3],
                [6, 5, 4],
                [7, 3, 9]];

      document.write(maxAverageOfPath(cost, 3));

</script>
```

**输出:**

```
5.2
```

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。