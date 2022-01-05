# 骑士留在棋盘上的概率

> 原文:[https://www . geeksforgeeks . org/probability-knight-retain-checkboard/](https://www.geeksforgeeks.org/probability-knight-remain-chessboard/)

给定 NxN 棋盘和位置(x，y)的骑士。骑士必须精确地走 K 步，在每一步中，他均匀地随机选择 8 个方向中的任何一个。骑士走完 K 步后留在棋盘上的概率是多少，条件是一旦离开就不能再进入棋盘？
**例:**

```
Let's take:
8x8 chessboard,
initial position of the knight : (0, 0),
number of steps : 1
At each step, the Knight has 8 different positions to choose from. 

If it starts from (0, 0), after taking one step it will lie inside the
board only at 2 out of 8 positions, and will lie outside at other positions.
So, the probability is 2/8 = 0.25
```

**进场:**

我们可以观察到的一件事是，在每一步，骑士都有 8 个选择。假设，骑士必须走 k 步，在走完第 k 步后，骑士到达(x，y)。从 Knight 可以一步到达(x，y)的位置有 8 个不同的位置，分别是:(x+1，y+2)，(x+2，y+1)，(x+2，y-1)，(x+1，y-2)，(x-1，y-2)，(x-2，y-1)，(x-2，y-1)，(x-2，y+1)，(x-1，y+2)。
如果我们已经知道 K-1 步后到达这 8 个位置的概率会怎样？

那么，K 步之后的最终概率将简单地等于(K-1 步之后到达这 8 个位置中每一个的σ概率)/8；

这里我们除以 8，因为这 8 个位置中的每一个都有 8 个选择，位置(x，y)是其中一个选择。

对于位于板外的位置，我们要么将它们的概率取为 0，要么干脆忽略它。

因为我们需要跟踪每一步的每个位置的概率，所以我们需要动态规划来解决这个问题。
我们将取一个数组 dp[x][y][steps]，它将存储在(steps)次移动后达到(x，y)的概率。

基本情况:如果步数为 0，那么骑士留在棋盘内的概率为 1。
下面是上述方法的实现:

## C++

```
// C++ program to find the probability of the
// Knight to remain inside the chessboard after
// taking exactly K number of steps
#include <bits/stdc++.h>
using namespace std;

// size of the chessboard
#define N 8

// direction vector for the Knight
int dx[] = { 1, 2, 2, 1, -1, -2, -2, -1 };
int dy[] = { 2, 1, -1, -2, -2, -1, 1, 2 };

// returns true if the knight is inside the chessboard
bool inside(int x, int y)
{
    return (x >= 0 and x < N and y >= 0 and y < N);
}

// Bottom up approach for finding the probability to
// go out of chessboard.
double findProb(int start_x, int start_y, int steps)
{
    // dp array
    double dp1[N][N][steps + 1];

    // for 0 number of steps, each position
    // will have probability 1
    for (int i = 0; i < N; ++i)
        for (int j = 0; j < N; ++j)
            dp1[i][j][0] = 1;

    // for every number of steps s
    for (int s = 1; s <= steps; ++s) {

        // for every position (x,y) after
        // s number of steps
        for (int x = 0; x < N; ++x) {
            for (int y = 0; y < N; ++y) {
                double prob = 0.0;

                // for every position reachable from (x,y)
                for (int i = 0; i < 8; ++i) {
                    int nx = x + dx[i];
                    int ny = y + dy[i];

                    // if this position lie inside the board
                    if (inside(nx, ny))
                        prob += dp1[nx][ny][s - 1] / 8.0;
                }

                // store the result
                dp1[x][y][s] = prob;
            }
        }
    }

    // return the result
    return dp1[start_x][start_y][steps];
}

// Driver Code
int main()
{
    // number of steps
    int K = 3;

    // Function Call
    cout << findProb(0, 0, K) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the probability
// of the Knight to remain inside the
// chessboard after taking exactly K
// number of steps
class GFG {

    // size of the chessboard
    static final int N = 8;

    // direction vector for the Knight
    static int dx[] = { 1, 2, 2, 1, -1, -2, -2, -1 };

    static int dy[] = { 2, 1, -1, -2, -2, -1, 1, 2 };

    // returns true if the knight is
    // inside the chessboard
    static boolean inside(int x, int y)
    {
        return (x >= 0 && x < N && y >= 0 && y < N);
    }

    // Bottom up approach for finding
    // the probability to go out of
    // chessboard.
    static double findProb(int start_x, int start_y,
                           int steps)
    {

        // dp array
        double dp1[][][] = new double[N][N][steps + 1];

        // for 0 number of steps, each position
        // will have probability 1
        for (int i = 0; i < N; ++i)
            for (int j = 0; j < N; ++j)
                dp1[i][j][0] = 1;

        // for every number of steps s
        for (int s = 1; s <= steps; ++s) {

            // for every position (x, y) after
            // s number of steps
            for (int x = 0; x < N; ++x) {

                for (int y = 0; y < N; ++y) {

                    double prob = 0.0;

                    // for every position reachable
                    // from (x, y)
                    for (int i = 0; i < 8; ++i) {
                        int nx = x + dx[i];
                        int ny = y + dy[i];

                        // if this position lie
                        // inside the board
                        if (inside(nx, ny))
                            prob
                                += dp1[nx][ny][s - 1] / 8.0;
                    }

                    // store the result
                    dp1[x][y][s] = prob;
                }
            }
        }

        // return the result
        return dp1[start_x][start_y][steps];
    }

    // Driver code
    public static void main(String[] args)
    {

        // number of steps
        int K = 3;

        // Function Call
        System.out.println(findProb(0, 0, K));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to find the probability of
# the Knight to remain inside the chessboard
# after taking exactly K number of steps
# size of the chessboard
N = 8

# Direction vector for the Knight
dx = [1, 2, 2, 1, -1, -2, -2, -1]
dy = [2, 1, -1, -2, -2, -1, 1, 2]

# returns true if the knight
# is inside the chessboard

def inside(x, y):
    return (x >= 0 and x < N and y >= 0 and y < N)

# Bottom up approach for finding the
# probability to go out of chessboard.

def findProb(start_x, start_y, steps):

    # dp array
    dp1 = [[[0 for i in range(N+5)]
            for j in range(N+5)]
            for k in range(steps + 5)]

    # For 0 number of steps, each
    # position will have probability 1
    for i in range(N):
        for j in range(N):
            dp1[i][j][0] = 1

    # for every number of steps s
    for s in range(1, steps + 1):

        # for every position (x,y) after
        # s number of steps
        for x in range(N):

            for y in range(N):
                prob = 0.0

                # For every position reachable from (x,y)
                for i in range(8):
                    nx = x + dx[i]
                    ny = y + dy[i]

                    # if this position lie inside the board
                    if (inside(nx, ny)):
                        prob += dp1[nx][ny][s-1] / 8.0

                # store the result
                dp1[x][y][s] = prob

    # return the result
    return dp1[start_x][start_y][steps]

# Driver code

# number of steps
K = 3

# Function Call
print(findProb(0, 0, K))

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# program to find the
// probability of the Knight
// to remain inside the
// chessboard after taking
// exactly K number of steps
using System;

class GFG {

    // size of the chessboard
    static int N = 8;

    // direction vector
    // for the Knight
    static int[] dx = { 1, 2, 2, 1, -1, -2, -2, -1 };

    static int[] dy = { 2, 1, -1, -2, -2, -1, 1, 2 };

    // returns true if the
    // knight is inside the
    // chessboard
    static bool inside(int x, int y)
    {
        return (x >= 0 && x < N && y >= 0 && y < N);
    }

    // Bottom up approach for
    // finding the probability
    // to go out of chessboard.
    static double findProb(int start_x, int start_y,
                           int steps)
    {

        // dp array
        double[, , ] dp1 = new double[N, N, steps+1];

        // for 0 number of steps,
        // each position will have
        // probability 1
        for (int i = 0; i < N; ++i)
            for (int j = 0; j < N; ++j)
                dp1[i, j, 0] = 1;

        // for every number
        // of steps s
        for (int s = 1; s <= steps; ++s) {

            // for every position (x, y)
            // after s number of steps
            for (int x = 0; x < N; ++x) {
                for (int y = 0; y < N; ++y) {
                    double prob = 0.0;

                    // for every position
                    // reachable from (x, y)
                    for (int i = 0; i < 8; ++i) {
                        int nx = x + dx[i];
                        int ny = y + dy[i];

                        // if this position lie
                        // inside the board
                        if (inside(nx, ny))
                            prob
                                += dp1[nx, ny, s - 1] / 8.0;
                    }

                    // store the result
                    dp1[x, y, s] = prob;
                }
            }
        }

        // return the result
        return dp1[start_x, start_y, steps];
    }

    // Driver code
    static void Main()
    {
        // number of steps
        int K = 3;

        // Function Call
        Console.WriteLine(findProb(0, 0, K));
    }
}

// This code is contributed
// by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the probability
// of the Knight to remain inside the
// chessboard after taking exactly K
// number of steps

// size of the chessboard
$N = 8;

// direction vector for the Knight
$dx = array(1, 2, 2, 1, -1, -2, -2, -1 );
$dy = array(2, 1, -1, -2, -2, -1, 1, 2 );

// returns true if the knight is
// inside the chessboard
function inside($x, $y)
{
    global $N;
    return ($x >= 0 and $x < $N and
            $y >= 0 and $y < $N);
}

// Bottom up approach for finding the
// probability to go out of chessboard.
function findProb($start_x, $start_y, $steps)
{
    global $N, $dx, $dy;

    // dp array
    $dp1 = array_fill(0, $N,
           array_fill(0, $N,
           array_fill(0, $steps+1, NULL)));

    // for 0 number of steps, each
    // position will have probability 1
    for ($i = 0; $i < $N; ++$i)
        for ($j = 0; $j < $N; ++$j)
            $dp1[$i][$j][0] = 1;

    // for every number of steps s
    for ($s = 1; $s <= $steps; ++$s)
    {
        // for every position (x,y) after
        // s number of steps
        for ($x = 0; $x < $N; ++$x)
        {
            for ($y = 0; $y < $N; ++$y)
            {
                $prob = 0.0;

                // for every position
                // reachable from (x,y)
                for ($i = 0; $i < 8; ++$i)
                {
                    $nx = $x + $dx[$i];
                    $ny = $y + $dy[$i];

                    // if this position lie inside
                    // the board
                    if (inside($nx, $ny))
                        $prob += $dp1[$nx][$ny][$s - 1] / 8.0;
                }

                // store the result
                $dp1[$x][$y][$s] = $prob;
            }
        }
    }

    // return the result
    return $dp1[$start_x][$start_y][$steps];
}

// Driver Code

// number of steps
$K = 3;

// Function Call
echo findProb(0, 0, $K) . "\n";

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>

// Javascript program to find the probability
// of the Knight to remain inside the
// chessboard after taking exactly K
// number of steps

    // size of the chessboard
    let N = 8;

    // direction vector for the Knight
    let dx = [ 1, 2, 2, 1, -1, -2, -2, -1 ];

    let dy = [2, 1, -1, -2, -2, -1, 1, 2];

    // returns true if the knight is
    // inside the chessboard
    function inside(x,y)
    {
        return (x >= 0 && x < N && y >= 0 && y < N);
    }

    // Bottom up approach for finding
    // the probability to go out of
    // chessboard.
    function findProb(start_x, start_y, steps)
    {
        // dp array
        let dp1 = new Array(N);
        for(let i = 0; i < N; i++)
        {
            dp1[i] = new Array(N);
            for(let j = 0; j < N; j++)
            {
                dp1[i][j] = new Array(steps + 1);
                for(let k = 0; k < steps + 1; k++)
                {
                    dp1[i][j][k] = 0;
                }
            }
        }

        // for 0 number of steps, each position
        // will have probability 1
        for (let i = 0; i < N; ++i)
            for (let j = 0; j < N; ++j)
                dp1[i][j][0] = 1;

        // for every number of steps s
        for (let s = 1; s <= steps; ++s)
        {

            // for every position (x, y) after
            // s number of steps
            for (let x = 0; x < N; ++x)
            {

                for (let y = 0; y < N; ++y)
                {

                    let prob = 0.0;

                    // for every position reachable
                    // from (x, y)
                    for (let i = 0; i < 8; ++i)
                    {
                        let nx = x + dx[i];
                        let ny = y + dy[i];

                        // if this position lie
                        // inside the board
                        if (inside(nx, ny))
                            prob
                                += dp1[nx][ny][s - 1] / 8.0;
                    }

                    // store the result
                    dp1[x][y][s] = prob;
                }
            }
        }

        // return the result
        return dp1[start_x][start_y][steps];
    }

     // Driver code

    // number of steps
    let K = 3;

    // Function Call
    document.write(findProb(0, 0, K));

    // This code is contributed by rag2127
</script>
```

**Output**

```
0.125
```

**时间复杂度** : O(NxNxKx8)也就是 O(NxNxK)，其中 N 是板子的大小，K 是步数。
**空间复杂度** : O(NxNxK)

本文由**阿维纳什库马尔锯**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。