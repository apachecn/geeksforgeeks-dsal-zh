# 叠瓦问题

> 原文:[https://www.geeksforgeeks.org/tile-stacking-problem/](https://www.geeksforgeeks.org/tile-stacking-problem/)

高度稳定的塔 **n** 是由正好 n 块单位高度的瓷砖垂直堆叠而成的塔，这样就不会有更大的瓷砖放在更小的瓷砖上。下面是一个例子:

![](img/96e81e46e8dea4b39400a8849b887831.png)

我们有无限数量的大小为 1、2、…、m 的瓦片，任务是计算由这些瓦片可以建造的高度为 n 的不同稳定塔的数量，有一个限制，即塔中最多可以使用每个大小的 **k** 个瓦片。
**注:**高度为 n 的两座塔，当且仅当存在高度 h (1 < = h < = n)时，高度为 n 的两座塔是不同的，使得两座塔在高度 h 处具有不同尺寸的瓦片
**示例:**

```
Input : n = 3, m = 3, k = 1.
Output : 1
Possible sequences: { 1, 2, 3}. 
Hence answer is 1.

Input : n = 3, m = 3, k = 2.
Output : 7
{1, 1, 2}, {1, 1, 3}, {1, 2, 2},
{1, 2, 3}, {1, 3, 3}, {2, 2, 3}, 
{2, 3, 3}.
```

我们基本上需要使用从 1 到 m 的数字来计数长度为 n 的递减序列，其中每个数字最多可以使用 k 次。我们可以使用 n-1 的计数递归计算 n 的计数。
思路是用动态规划。声明一个 2D 数组 dp[][]，其中每个状态 dp[i][j]表示使用从 j 到 m 的数字的长度为 I 的递减序列的数量。我们需要注意一个事实，即一个数字在 k 次中的大部分时间都可以使用。这可以通过考虑一个数字出现 1 到 k 次来实现。因此，我们的递归关系变成:
![{\huge DP[i][j] = \sum_{x=0}^{k}[i-x][j-1]}  ](img/1a064880554ce0c02498720f3b142f12.png "Rendered by QuickLaTeX.com")
此外，我们可以使用这样一个事实，即对于固定的 j，我们使用 I 的先前 k 值的连续值。因此，我们可以为每个状态维护前缀和数组。现在我们已经去掉了每个状态的 k 因子。
以下是本办法的实施情况:

## C++

```
// CPP program to find number of ways to make stable
// tower of given height.
#include <bits/stdc++.h>
using namespace std;
#define N 100

int possibleWays(int n, int m, int k)
{
    int dp[N][N];
    int presum[N][N];
    memset(dp, 0, sizeof dp);
    memset(presum, 0, sizeof presum);

    // Initialing 0th row to 0.
    for (int i = 1; i < n + 1; i++) {
        dp[0][i] = 0;
        presum[0][i] = 1;
    }

    // Initialing 0th column to 0.
    for (int i = 0; i < m + 1; i++)
        presum[i][0] = dp[i][0] = 1;

    // For each row from 1 to m
    for (int i = 1; i < m + 1; i++) {

        // For each column from 1 to n.
        for (int j = 1; j < n + 1; j++) {

            // Initialing dp[i][j] to presum of (i - 1, j).
            dp[i][j] = presum[i - 1][j];
            if (j > k) {
                dp[i][j] -= presum[i - 1][j - k - 1];
            }
        }

        // Calculating presum for each i, 1 <= i <= n.
        for (int j = 1; j < n + 1; j++)
            presum[i][j] = dp[i][j] + presum[i][j - 1];
    }

    return dp[m][n];
}

// Driver Program
int main()
{
    int n = 3, m = 3, k = 2;
    cout << possibleWays(n, m, k) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number of ways to make
// stable tower of given height.
class GFG
{

    static int N = 100;

    static int possibleWays(int n, int m, int k)
    {
        int[][] dp = new int[N][N];
        int[][] presum = new int[N][N];

        for (int i = 0; i < N; i++)
        {
            for (int j = 0; j < N; j++)
            {
                dp[i][j] = 0;
                presum[i][j] = 0;
            }
        }

        // Initialing 0th row to 0.
        for (int i = 1; i < n + 1; i++)
        {
            dp[0][i] = 0;
            presum[0][i] = 1;
        }

        // Initialing 0th column to 0.
        for (int i = 0; i < m + 1; i++)
        {
            presum[i][0] = dp[i][0] = 1;
        }

        // For each row from 1 to m
        for (int i = 1; i < m + 1; i++)
        {

            // For each column from 1 to n.
            for (int j = 1; j < n + 1; j++)
            {

                // Initialing dp[i][j] to presum of (i - 1, j).
                dp[i][j] = presum[i - 1][j];
                if (j > k)
                {
                    dp[i][j] -= presum[i - 1][j - k - 1];
                }
            }

            // Calculating presum for each i, 1 <= i <= n.
            for (int j = 1; j < n + 1; j++) {
                presum[i][j] = dp[i][j] + presum[i][j - 1];
            }
        }

        return dp[m][n];
    }

    // Driver Program
    public static void main(String[] args) {
        int n = 3, m = 3, k = 2;
        System.out.println(possibleWays(n, m, k));
    }
}
// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 code to find number of ways
# to make stable tower of given height
n = 100
def possibleWays(n, m, k):
    dp = [[0 for i in range(10)]
             for j in range(10)]
    presum=[[0 for i in range(10)]
               for j in range(10)]

    # initialing 0th row to 0
    for i in range(1, n + 1):
        dp[0][i] = 0
        presum[0][i] = 1

    # initialing 0th column to 0
    for i in range(0, m + 1):
        presum[i][0] = 1
        dp[i][0] = 1

    # for each from 1 to m
    for i in range(1, m + 1):

        # for each column from 1 to n.
        for j in range(1, n + 1):

            # for each column from 1 to n
            # Initialing dp[i][j] to presum
            # of (i-1,j).
            dp[i][j] = presum[i - 1][j]
            if j > k:
                dp[i][j] -= presum[i - 1][j - k - 1]

        for j in range(1, n + 1):
            presum[i][j] = dp[i][j] + presum[i][j - 1]

    return dp[m][n]

# Driver Code
n, m, k = 3, 3, 2

print(possibleWays(n, m, k))

# This code is contributed
# by Mohit kumar 29
```

## C#

```
// C# program to find number of ways to make
// stable tower of given height.
using System;

class GFG
{
    static int N = 100 ;

    static int possibleWays(int n, int m, int k)
    {
        int[,] dp = new int[N, N];
        int[,] presum = new int[N, N];

        for(int i = 0; i < N; i++)
        {
            for(int j = 0; j < N; j++)
            {
                dp[i, j] = 0;
                presum[i, j] = 0;
            }
        }

        // Initialing 0th row to 0.
        for (int i = 1; i < n + 1; i++)
        {
            dp[0, i] = 0;
            presum[0, i] = 1;
        }

        // Initialing 0th column to 0.
        for (int i = 0; i < m + 1; i++)
            presum[i, 0] = dp[i, 0] = 1;

        // For each row from 1 to m
        for (int i = 1; i < m + 1; i++)
        {

            // For each column from 1 to n.
            for (int j = 1; j < n + 1; j++)
            {

                // Initialing dp[i][j] to presum of (i - 1, j).
                dp[i, j] = presum[i - 1, j];
                if (j > k)
                {
                    dp[i, j] -= presum[i - 1, j - k - 1];
                }
            }

            // Calculating presum for each i, 1 <= i <= n.
            for (int j = 1; j < n + 1; j++)
                presum[i, j] = dp[i, j] + presum[i, j - 1];
        }

        return dp[m, n];
    }

    // Driver Program
    static void Main()
    {
        int n = 3, m = 3, k = 2;
        Console.Write(possibleWays(n, m, k));
    }
}

// This code is contributed by DrRoot_
```

<gfg-tab role="tab" slot="tab" id="gfg-tab-4">PHP</gfg-tab><gfg-panel role="tabpanel" slot="panel" id="gfg-panel-4" data-code-lang="php"></gfg-panel>

```
 <?php
// PHP program to find number of ways to make stable 
// tower of given height. 

function possibleWays($n, $m, $k) 
{ 
    $N = 100 ;

    $dp = array(array());

    for ($i = 0; $i < $N; $i++)
        for($j = 0; $j < $N; $j++)
            $dp[$i][$j] = 0 ;

    $presum = array(array()) ;
    for ($i = 0; $i < $N; $i++)
        for($j = 0; $j < $N; $j++)
            $presum[$i][$j] = 0 ;

    // Initialing 0th row to 0\. 
    for ($i = 1; $i < $n + 1; $i++) { 
        $dp[0][$i] = 0; 
        $presum[0][$i] = 1; 
    } 

    // Initialing 0th column to 0\. 
    for ($i = 0; $i < $m + 1; $i++) 
        $presum[$i][0] = $dp[$i][0] = 1; 

    // For each row from 1 to m 
    for ($i = 1; $i < $m + 1; $i++) { 

        // For each column from 1 to n. 
        for ($j = 1; $j < $n + 1; $j++) { 

            // Initialing dp[i][j] to presum of (i - 1, j). 
            $dp[$i][$j] = $presum[$i - 1][$j]; 
            if ($j > $k) { 
                $dp[$i][$j] -= $presum[$i - 1][$j - $k - 1]; 
            } 
        } 

        // Calculating presum for each i, 1 <= i <= n. 
        for ($j = 1; $j < $n + 1; $j++) 
            $presum[$i][$j] = $dp[$i][$j] + $presum[$i][$j - 1]; 
    } 

    return $dp[$m][$n]; 
} 

    // Driver Program 
    $n = 3 ;
    $m = 3 ;
    $k = 2; 
    echo possibleWays($n, $m, $k) ; 

    # this code is contributed by Ryuga    
?> 
```

## java 描述语言

```
<script>

// Javascript program to find
// number of ways to make
// stable tower of given height

let N = 100;

    function possibleWays(n, m, k)
    {
        let dp =  new Array(N);
        // Loop to create 2D array
        // using 1D array
        for (var i = 0; i < dp.length; i++)
        {
            dp[i] = new Array(2);
        }

        let presum = new Array(N);
        // Loop to create 2D array using 1D array
        for (var i = 0; i < presum.length; i++)
        {
            presum[i] = new Array(2);
        }

        for (let i = 0; i < N; i++)
        {
            for (let j = 0; j < N; j++)
            {
                dp[i][j] = 0;
                presum[i][j] = 0;
            }
        }

        // Initialing 0th row to 0.
        for (let i = 1; i < n + 1; i++)
        {
            dp[0][i] = 0;
            presum[0][i] = 1;
        }

        // Initialing 0th column to 0.
        for (let i = 0; i < m + 1; i++)
        {
            presum[i][0] = dp[i][0] = 1;
        }

        // For each row from 1 to m
        for (let i = 1; i < m + 1; i++)
        {

            // For each column from 1 to n.
            for (let j = 1; j < n + 1; j++)
            {

                // Initialing dp[i][j] to
                // presum of (i - 1, j).
                dp[i][j] = presum[i - 1][j];
                if (j > k)
                {
                    dp[i][j] -=
                    presum[i - 1][j - k - 1];
                }
            }

            // Calculating presum for each
            // i, 1 <= i <= n.
            for (let j = 1; j < n + 1; j++)
            {
                presum[i][j] = dp[i][j] +
                presum[i][j - 1];
            }
        }

        return dp[m][n];
    }

// driver program

    let n = 3, m = 3, k = 2;
    document.write(possibleWays(n, m, k));

</script>
```

**输出:**

```
7
```

本文由 **Anuj Chauhan** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。