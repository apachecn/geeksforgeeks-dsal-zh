# 金矿问题

> 原文:[https://www.geeksforgeeks.org/gold-mine-problem/](https://www.geeksforgeeks.org/gold-mine-problem/)

给定一个 n*m 维度的金矿。这个矿坑中的每个区域都包含一个正整数，即以吨为单位的黄金数量。最初，矿工在第一列，但可以在任何一行。他只能移动(右->，右向上/，右向下\)也就是说，从一个给定的单元格开始，矿工可以向右斜上或向右斜下移动到该单元格。找出他能收集的最大黄金量。
**例:**

```
Input : mat[][] = {{1, 3, 3},
                   {2, 1, 4},
                  {0, 6, 4}};
Output : 12 
{(1,0)->(2,1)->(1,2)}

Input: mat[][] = { {1, 3, 1, 5},
                   {2, 2, 4, 1},
                   {5, 0, 2, 3},
                   {0, 6, 1, 2}};
Output : 16
(2,0) -> (1,1) -> (1,2) -> (0,3) OR
(2,0) -> (3,1) -> (2,2) -> (2,3)

Input : mat[][] = {{10, 33, 13, 15},
                  {22, 21, 04, 1},
                  {5, 0, 2, 3},
                  {0, 6, 14, 2}};
Output : 83
```

来源 [Flipkart 访谈](https://www.geeksforgeeks.org/flipkart-interview-set-2-sde-2/)

创建与给定矩阵矩阵[]相同的二维矩阵金表[][])。如果我们仔细观察这个问题，我们会注意到以下几点。

1.  黄金数量为正数，因此我们希望在给定的约束条件下覆盖最大值的最大单元格。
2.  每一步，我们都向右侧移动一步。所以我们总是排在最后一列。如果我们在最后一列，那么我们不能向右移动

如果我们在第一行或最后一列，那么我们不能向右上方移动，所以只需分配 0，否则将 goldTable[row-1][col+1]的值分配给 right_up。如果我们在最后一行或最后一列，那么我们就不能向右下移动，所以只需赋值 0，否则就将 goldTable[row+1][col+1]的值赋值为向右上。
现在求右、右上、右下的最大值，然后和那个 mat[row][col]相加。最后，找到所有行和第一列的最大值并返回。

## C++

```
// C++ program to solve Gold Mine problem
#include<bits/stdc++.h>
using namespace std;

const int MAX = 100;

// Returns maximum amount of gold that can be collected
// when journey started from first column and moves
// allowed are right, right-up and right-down
int getMaxGold(int gold[][MAX], int m, int n)
{
    // Create a table for storing intermediate results
    // and initialize all cells to 0\. The first row of
    // goldMineTable gives the maximum gold that the miner
    // can collect when starts that row
    int goldTable[m][n];
    memset(goldTable, 0, sizeof(goldTable));

    for (int col=n-1; col>=0; col--)
    {
        for (int row=0; row<m; row++)
        {
            // Gold collected on going to the cell on the right(->)
            int right = (col==n-1)? 0: goldTable[row][col+1];

            // Gold collected on going to the cell to right up (/)
            int right_up = (row==0 || col==n-1)? 0:
                            goldTable[row-1][col+1];

            // Gold collected on going to the cell to right down (\)
            int right_down = (row==m-1 || col==n-1)? 0:
                             goldTable[row+1][col+1];

            // Max gold collected from taking either of the
            // above 3 paths
            goldTable[row][col] = gold[row][col] +
                              max(right, max(right_up, right_down));

        }
    }

    // The max amount of gold collected will be the max
    // value in first column of all rows
    int res = goldTable[0][0];
    for (int i=1; i<m; i++)
        res = max(res, goldTable[i][0]);
    return res;
}

// Driver Code
int main()
{
    int gold[MAX][MAX]= { {1, 3, 1, 5},
        {2, 2, 4, 1},
        {5, 0, 2, 3},
        {0, 6, 1, 2}
    };
    int m = 4, n = 4;
    cout << getMaxGold(gold, m, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to solve Gold Mine problem
import java.util.Arrays;

class GFG {

    static final int MAX = 100;

    // Returns maximum amount of gold that
    // can be collected when journey started
    // from first column and moves allowed
    // are right, right-up and right-down
    static int getMaxGold(int gold[][],
                              int m, int n)
    {

        // Create a table for storing
        // intermediate results and initialize
        // all cells to 0\. The first row of
        // goldMineTable gives the maximum
        // gold that the miner can collect
        // when starts that row
        int goldTable[][] = new int[m][n];

        for(int[] rows:goldTable)
            Arrays.fill(rows, 0);

        for (int col = n-1; col >= 0; col--)
        {
            for (int row = 0; row < m; row++)
            {

                // Gold collected on going to
                // the cell on the right(->)
                int right = (col == n-1) ? 0
                        : goldTable[row][col+1];

                // Gold collected on going to
                // the cell to right up (/)
                int right_up = (row == 0 ||
                               col == n-1) ? 0 :
                        goldTable[row-1][col+1];

                // Gold collected on going to
                // the cell to right down (\)
                int right_down = (row == m-1
                            || col == n-1) ? 0 :
                          goldTable[row+1][col+1];

                // Max gold collected from taking
                // either of the above 3 paths
                goldTable[row][col] = gold[row][col]
                 + Math.max(right, Math.max(right_up,
                                       right_down));

            }
        }

        // The max amount of gold collected will be
        // the max value in first column of all rows
        int res = goldTable[0][0];

        for (int i = 1; i < m; i++)
            res = Math.max(res, goldTable[i][0]);

        return res;
    }

    //driver code
    public static void main(String arg[])
    {
        int gold[][]= { {1, 3, 1, 5},
                        {2, 2, 4, 1},
                        {5, 0, 2, 3},
                        {0, 6, 1, 2} };

        int m = 4, n = 4;

        System.out.print(getMaxGold(gold, m, n));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python program to solve
# Gold Mine problem

MAX = 100

# Returns maximum amount of
# gold that can be collected
# when journey started from
# first column and moves
# allowed are right, right-up
# and right-down
def getMaxGold(gold, m, n):

    # Create a table for storing
    # intermediate results
    # and initialize all cells to 0.
    # The first row of
    # goldMineTable gives the
    # maximum gold that the miner
    # can collect when starts that row
    goldTable = [[0 for i in range(n)]
                        for j in range(m)]

    for col in range(n-1, -1, -1):
        for row in range(m):

            # Gold collected on going to
            # the cell on the right(->)
            if (col == n-1):
                right = 0
            else:
                right = goldTable[row][col+1]

            # Gold collected on going to
            # the cell to right up (/)
            if (row == 0 or col == n-1):
                right_up = 0
            else:
                right_up = goldTable[row-1][col+1]

            # Gold collected on going to
            # the cell to right down (\)
            if (row == m-1 or col == n-1):
                right_down = 0
            else:
                right_down = goldTable[row+1][col+1]

            # Max gold collected from taking
            # either of the above 3 paths
            goldTable[row][col] = gold[row][col] + max(right, right_up, right_down)

    # The max amount of gold
    # collected will be the max
    # value in first column of all rows
    res = goldTable[0][0]
    for i in range(1, m):
        res = max(res, goldTable[i][0])

    return res

# Driver code
gold = [[1, 3, 1, 5],
    [2, 2, 4, 1],
    [5, 0, 2, 3],
    [0, 6, 1, 2]]

m = 4
n = 4

print(getMaxGold(gold, m, n))

# This code is contributed
# by Soumen Ghosh.             
```

## C#

```
// C# program to solve Gold Mine problem
using System;

class GFG
{
    static int MAX = 100;

    // Returns maximum amount of gold that
    // can be collected when journey started
    // from first column and moves allowed are
    // right, right-up and right-down
    static int getMaxGold(int[,] gold,
                            int m, int n)
    {

        // Create a table for storing intermediate
        // results and initialize all cells to 0.
        // The first row of goldMineTable gives
        // the maximum gold that the miner
        // can collect when starts that row
        int[,] goldTable = new int[m, n];

        for(int i = 0; i < m; i++)
            for(int j = 0; j < n; j++)
                goldTable[i, j] = 0;

        for (int col = n - 1; col >= 0; col--)
        {
            for (int row = 0; row < m; row++)
            {
                // Gold collected on going to
                // the cell on the right(->)
                int right = (col == n - 1) ? 0 :
                            goldTable[row, col + 1];

                // Gold collected on going to
                // the cell to right up (/)
                int right_up = (row == 0 || col == n - 1)
                            ? 0 : goldTable[row-1,col+1];

                // Gold collected on going
                // to the cell to right down (\)
                int right_down = (row == m - 1 || col == n - 1)
                                ? 0 : goldTable[row + 1, col + 1];

                // Max gold collected from taking
                // either of the above 3 paths
                goldTable[row, col] = gold[row, col] +
                                Math.Max(right, Math.Max(right_up,
                                                    right_down));
            }
        }

        // The max amount of gold collected will be the max
        // value in first column of all rows
        int res = goldTable[0, 0];
        for (int i = 1; i < m; i++)
            res = Math.Max(res, goldTable[i, 0]);
        return res;
    }

    // Driver Code
    static void Main()
    {
        int[,] gold = new int[,]{{1, 3, 1, 5},
                                {2, 2, 4, 1},
                                {5, 0, 2, 3},
                                {0, 6, 1, 2}
                                };
        int m = 4, n = 4;
        Console.Write(getMaxGold(gold, m, n));
    }
}

// This code is contributed by DrRoot_
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Php program to solve Gold Mine problem

// Returns maximum amount of gold that
// can be collected when journey started
// from first column and moves allowed are
// right, right-up and right-down
function getMaxGold($gold, $m, $n)
{
    $MAX = 100 ;

    // Create a table for storing intermediate
    // results and initialize all cells to 0.
    // The first row of goldMineTable gives the
    // maximum gold that the miner can collect
    // when starts that row
    $goldTable = array(array());
    for ($i = 0; $i < $m ; $i ++)
        for($j = 0; $j < $n ; $j ++)
            $goldTable[$i][$j] = 0 ;

    for ($col = $n - 1; $col >= 0 ; $col--)
    {
        for ($row = 0 ; $row < $m ; $row++)
        {

            // Gold collected on going to
            // the cell on the right(->)
            if ($col == $n - 1)
                $right = 0 ;
            else
                $right = $goldTable[$row][$col + 1];

            // Gold collected on going to
            // the cell to right up (/)
            if ($row == 0 or $col == $n - 1)
                $right_up = 0 ;
            else
                $right_up = $goldTable[$row - 1][$col + 1];

            // Gold collected on going to
            // the cell to right down (\)
            if ($row == $m - 1 or $col == $n - 1)
                $right_down = 0 ;
            else
                $right_down = $goldTable[$row + 1][$col + 1];

            // Max gold collected from taking
            // either of the above 3 paths
            $goldTable[$row][$col] = $gold[$row][$col] +
                                 max($right, $right_up,
                                             $right_down);
        }
    }

    // The max amount of gold collected will be the
    // max value in first column of all rows
    $res = $goldTable[0][0] ;
    for ($i = 0; $i < $m; $i++)
        $res = max($res, $goldTable[$i][0]);

    return $res;
}

// Driver code
$gold = array(array(1, 3, 1, 5),
              array(2, 2, 4, 1),
              array(5, 0, 2, 3),
              array(0, 6, 1, 2));

$m = 4 ;
$n = 4 ;

echo getMaxGold($gold, $m, $n) ;

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

    // JavaScript program to solve Gold Mine problem

    let MAX = 100;

    // Returns maximum amount of gold that
    // can be collected when journey started
    // from first column and moves allowed
    // are right, right-up and right-down
    function getMaxGold(gold, m, n)
    {

        // Create a table for storing
        // intermediate results and initialize
        // all cells to 0\. The first row of
        // goldMineTable gives the maximum
        // gold that the miner can collect
        // when starts that row
        let goldTable = new Array(m);

        for(let i = 0; i < m; i++)
        {
            goldTable[i] = new Array(n);
            for(let j = 0; j < n; j++)
            {
                goldTable[i][j] = 0;
            }
        }

        for (let col = n-1; col >= 0; col--)
        {
            for (let row = 0; row < m; row++)
            {

                // Gold collected on going to
                // the cell on the right(->)
                let right = (col == n-1) ? 0
                        : goldTable[row][col+1];

                // Gold collected on going to
                // the cell to right up (/)
                let right_up = (row == 0 ||
                               col == n-1) ? 0 :
                        goldTable[row-1][col+1];

                // Gold collected on going to
                // the cell to right down (\)
                let right_down = (row == m-1
                            || col == n-1) ? 0 :
                          goldTable[row+1][col+1];

                // Max gold collected from taking
                // either of the above 3 paths
                goldTable[row][col] = gold[row][col]
                 + Math.max(right, Math.max(right_up,
                                       right_down));

            }
        }

        // The max amount of gold collected will be
        // the max value in first column of all rows
        let res = goldTable[0][0];

        for (let i = 1; i < m; i++)
            res = Math.max(res, goldTable[i][0]);

        return res;
    }

    let gold = [ [1, 3, 1, 5],
                  [2, 2, 4, 1],
                  [5, 0, 2, 3],
                  [0, 6, 1, 2] ];

    let m = 4, n = 4;

    document.write(getMaxGold(gold, m, n));

</script>
```

**Output**

```
16
```

**时间复杂度:**O(m * n)
T3】空间复杂度: O(m*n)
本文由 **Rakesh Kumar** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。