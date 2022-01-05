# 骑士到达目标的最小步数|设定 2

> 原文:[https://www . geesforgeks . org/mining-steps-reach-target-knight-set-2/](https://www.geeksforgeeks.org/minimum-steps-reach-target-knight-set-2/)

给定一个 N×N 大小的正方形棋盘，给出骑士的位置和目标的位置，任务是找出骑士到达目标位置所需的最小步数。

![](img/88301109434eddfe29a6d6bb31330d19.png)

示例:

```
Input : (2, 4) - knight's position, (6, 4) - target cell
Output : 2

Input : (4, 5) (1, 1)
Output : 3
```

解决上述问题的 BFS 方法已经在[之前的](https://www.geeksforgeeks.org/minimum-steps-reach-target-knight/)帖子中讨论过。在这篇文章中，讨论了动态规划解决方案。
**进场说明:**

*   **情况 1 :** 如果目标不在骑士位置的一行或一列。
    让一块 8×8 格的棋盘。现在，假设骑士在(3，3)，目标在(7，8)。距离骑士当前位置可能有 8 步，即(2，1)，(1，2)，(4，1)，(1，4)，(5，2)，(2，5)，(5，4，5)。但是，在这些动作中，只有两个动作(5，4)和(4，5)将朝向目标，而所有其他动作都远离目标。因此，要找到最小步数，请转到(4，5)或(5，4)。现在，计算从(4，5)和(5，4)到达到目标所采取的最小步骤。这是通过动态编程计算的。因此，这导致从(3，3)到(7，8)的最小步长。
*   **情况 2 :** 如果目标是沿着骑士位置的一行或一列。
    让一块 8×8 格的棋盘。现在，假设骑士在(4，3)，目标在(4，7)。可能有 8 次移动，但朝向目标，只有 4 次移动，即(5，5)，(3，5)，(2，4)，(6，4)。As，(5，5)相当于(3，5)而(2，4)相当于(6，4)。所以，从这 4 点，可以换算成 2 点。取(5，5)和(6，4)(此处)。现在，计算从这两点到达目标所采取的最小步骤。这是通过动态编程计算的。因此，这导致从(4，3)到(4，7)的最小步长。

**异常:**当骑士将在拐角处且目标为 x、y 坐标与骑士位置之差为(1，1)时，反之亦然。那么最少的步骤是 4 步。
**动态规划方程:**

> 1) **dp[diffOfX][diffOfY]** 是从骑士位置到目标位置所走的最小步数。
> 2)**DP[diffOfX][diffOfY]= DP[diffOfY][diffOfX]**。
> 其中，diffOfX =骑士 x 坐标与目标 x 坐标之差
> diffOfY =骑士 y 坐标与目标 y 坐标之差

以下是上述方法的实现:

## C++

```
// C++ code for minimum steps for
// a knight to reach target position
#include <bits/stdc++.h>

using namespace std;

// initializing the matrix.
int dp[8][8] = { 0 };

int getsteps(int x, int y,
             int tx, int ty)
{
    // if knight is on the target
    // position return 0.
    if (x == tx && y == ty)
        return dp[0][0];
    else {

        // if already calculated then return
        // that value. Taking absolute difference.
        if (dp[abs(x - tx)][abs(y - ty)] != 0)
            return dp[abs(x - tx)][abs(y - ty)];

        else {

            // there will be two distinct positions
            // from the knight towards a target.
            // if the target is in same row or column
            // as of knight than there can be four
            // positions towards the target but in that
            // two would be the same and the other two
            // would be the same.
            int x1, y1, x2, y2;

            // (x1, y1) and (x2, y2) are two positions.
            // these can be different according to situation.
            // From position of knight, the chess board can be
            // divided into four blocks i.e.. N-E, E-S, S-W, W-N .
            if (x <= tx) {
                if (y <= ty) {
                    x1 = x + 2;
                    y1 = y + 1;
                    x2 = x + 1;
                    y2 = y + 2;
                } else {
                    x1 = x + 2;
                    y1 = y - 1;
                    x2 = x + 1;
                    y2 = y - 2;
                }
            } else {
                if (y <= ty) {
                    x1 = x - 2;
                    y1 = y + 1;
                    x2 = x - 1;
                    y2 = y + 2;
                } else {
                    x1 = x - 2;
                    y1 = y - 1;
                    x2 = x - 1;
                    y2 = y - 2;
                }
            }

            // ans will be, 1 + minimum of steps
            // required from (x1, y1) and (x2, y2).
            dp[abs(x - tx)][abs(y - ty)] =
                           min(getsteps(x1, y1, tx, ty),
                           getsteps(x2, y2, tx, ty)) + 1;

            // exchanging the coordinates x with y of both
            // knight and target will result in same ans.
            dp[abs(y - ty)][abs(x - tx)] =
                           dp[abs(x - tx)][abs(y - ty)];
            return dp[abs(x - tx)][abs(y - ty)];
        }
    }
}

// Driver Code
int main()
{
    int i, n, x, y, tx, ty, ans;

    // size of chess board n*n
    n = 100;

    // (x, y) coordinate of the knight.
    // (tx, ty) coordinate of the target position.
    x = 4;
    y = 5;
    tx = 1;
    ty = 1;

    // (Exception) these are the four corner points
    // for which the minimum steps is 4.
    if ((x == 1 && y == 1 && tx == 2 && ty == 2) ||
        (x == 2 && y == 2 && tx == 1 && ty == 1))
            ans = 4;
    else if ((x == 1 && y == n && tx == 2 && ty == n - 1) ||
             (x == 2 && y == n - 1 && tx == 1 && ty == n))
                ans = 4;
    else if ((x == n && y == 1 && tx == n - 1 && ty == 2) ||
             (x == n - 1 && y == 2 && tx == n && ty == 1))
                ans = 4;
    else if ((x == n && y == n && tx == n - 1 && ty == n - 1) ||
             (x == n - 1 && y == n - 1 && tx == n && ty == n))
                ans = 4;
    else {
        // dp[a][b], here a, b is the difference of
        // x & tx and y & ty respectively.
        dp[1][0] = 3;
        dp[0][1] = 3;
        dp[1][1] = 2;
        dp[2][0] = 2;
        dp[0][2] = 2;
        dp[2][1] = 1;
        dp[1][2] = 1;

        ans = getsteps(x, y, tx, ty);
    }

    cout << ans << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java code for minimum steps for
// a knight to reach target position
public class GFG {

// initializing the matrix.
    static int dp[][] = new int[8][8];

    static int getsteps(int x, int y,
            int tx, int ty) {
        // if knight is on the target
        // position return 0.
        if (x == tx && y == ty) {
            return dp[0][0];
        } else // if already calculated then return
        // that value. Taking absolute difference.
        if (dp[ Math.abs(x - tx)][ Math.abs(y - ty)] != 0) {
            return dp[ Math.abs(x - tx)][ Math.abs(y - ty)];
        } else {

            // there will be two distinct positions
            // from the knight towards a target.
            // if the target is in same row or column
            // as of knight than there can be four
            // positions towards the target but in that
            // two would be the same and the other two
            // would be the same.
            int x1, y1, x2, y2;

            // (x1, y1) and (x2, y2) are two positions.
            // these can be different according to situation.
            // From position of knight, the chess board can be
            // divided into four blocks i.e.. N-E, E-S, S-W, W-N .
            if (x <= tx) {
                if (y <= ty) {
                    x1 = x + 2;
                    y1 = y + 1;
                    x2 = x + 1;
                    y2 = y + 2;
                } else {
                    x1 = x + 2;
                    y1 = y - 1;
                    x2 = x + 1;
                    y2 = y - 2;
                }
            } else if (y <= ty) {
                x1 = x - 2;
                y1 = y + 1;
                x2 = x - 1;
                y2 = y + 2;
            } else {
                x1 = x - 2;
                y1 = y - 1;
                x2 = x - 1;
                y2 = y - 2;
            }

            // ans will be, 1 + minimum of steps
            // required from (x1, y1) and (x2, y2).
            dp[ Math.abs(x - tx)][ Math.abs(y - ty)]
                    = Math.min(getsteps(x1, y1, tx, ty),
                            getsteps(x2, y2, tx, ty)) + 1;

            // exchanging the coordinates x with y of both
            // knight and target will result in same ans.
            dp[ Math.abs(y - ty)][ Math.abs(x - tx)]
                    = dp[ Math.abs(x - tx)][ Math.abs(y - ty)];
            return dp[ Math.abs(x - tx)][ Math.abs(y - ty)];
        }
    }

// Driver Code
    static public void main(String[] args) {
        int i, n, x, y, tx, ty, ans;

        // size of chess board n*n
        n = 100;

        // (x, y) coordinate of the knight.
        // (tx, ty) coordinate of the target position.
        x = 4;
        y = 5;
        tx = 1;
        ty = 1;

        // (Exception) these are the four corner points
        // for which the minimum steps is 4.
        if ((x == 1 && y == 1 && tx == 2 && ty == 2)
                || (x == 2 && y == 2 && tx == 1 && ty == 1)) {
            ans = 4;
        } else if ((x == 1 && y == n && tx == 2 && ty == n - 1)
                || (x == 2 && y == n - 1 && tx == 1 && ty == n)) {
            ans = 4;
        } else if ((x == n && y == 1 && tx == n - 1 && ty == 2)
                || (x == n - 1 && y == 2 && tx == n && ty == 1)) {
            ans = 4;
        } else if ((x == n && y == n && tx == n - 1 && ty == n - 1)
                || (x == n - 1 && y == n - 1 && tx == n && ty == n)) {
            ans = 4;
        } else {
            // dp[a][b], here a, b is the difference of
            // x & tx and y & ty respectively.
            dp[1][0] = 3;
            dp[0][1] = 3;
            dp[1][1] = 2;
            dp[2][0] = 2;
            dp[0][2] = 2;
            dp[2][1] = 1;
            dp[1][2] = 1;

            ans = getsteps(x, y, tx, ty);
        }

        System.out.println(ans);
    }
}

/*This code is contributed by PrinciRaj1992*/
```

## 蟒蛇 3

```
# Python3 code for minimum steps for
# a knight to reach target position

# initializing the matrix.
dp = [[0 for i in range(8)] for j in range(8)];

def getsteps(x, y, tx, ty):

    # if knight is on the target
    # position return 0.
    if (x == tx and y == ty):
        return dp[0][0];

    # if already calculated then return
    # that value. Taking absolute difference.
    elif(dp[abs(x - tx)][abs(y - ty)] != 0):
        return dp[abs(x - tx)][abs(y - ty)];
    else:

        # there will be two distinct positions
        # from the knight towards a target.
        # if the target is in same row or column
        # as of knight than there can be four
        # positions towards the target but in that
        # two would be the same and the other two
        # would be the same.
        x1, y1, x2, y2 = 0, 0, 0, 0;

        # (x1, y1) and (x2, y2) are two positions.
        # these can be different according to situation.
        # From position of knight, the chess board can be
        # divided into four blocks i.e.. N-E, E-S, S-W, W-N .
        if (x <= tx):
            if (y <= ty):
                x1 = x + 2;
                y1 = y + 1;
                x2 = x + 1;
                y2 = y + 2;
            else:
                x1 = x + 2;
                y1 = y - 1;
                x2 = x + 1;
                y2 = y - 2;

        elif (y <= ty):
            x1 = x - 2;
            y1 = y + 1;
            x2 = x - 1;
            y2 = y + 2;
        else:
            x1 = x - 2;
            y1 = y - 1;
            x2 = x - 1;
            y2 = y - 2;

        # ans will be, 1 + minimum of steps
        # required from (x1, y1) and (x2, y2).
        dp[abs(x - tx)][abs(y - ty)] = \
        min(getsteps(x1, y1, tx, ty),
        getsteps(x2, y2, tx, ty)) + 1;

        # exchanging the coordinates x with y of both
        # knight and target will result in same ans.
        dp[abs(y - ty)][abs(x - tx)] = \
        dp[abs(x - tx)][abs(y - ty)];
        return dp[abs(x - tx)][abs(y - ty)];

# Driver Code
if __name__ == '__main__':

    # size of chess board n*n
    n = 100;

    # (x, y) coordinate of the knight.
    # (tx, ty) coordinate of the target position.
    x = 4;
    y = 5;
    tx = 1;
    ty = 1;

    # (Exception) these are the four corner points
    # for which the minimum steps is 4.
    if ((x == 1 and y == 1 and tx == 2 and ty == 2) or
            (x == 2 and y == 2 and tx == 1 and ty == 1)):
        ans = 4;
    elif ((x == 1 and y == n and tx == 2 and ty == n - 1) or
        (x == 2 and y == n - 1 and tx == 1 and ty == n)):
        ans = 4;
    elif ((x == n and y == 1 and tx == n - 1 and ty == 2) or
        (x == n - 1 and y == 2 and tx == n and ty == 1)):
        ans = 4;
    elif ((x == n and y == n and tx == n - 1 and ty == n - 1)
        or (x == n - 1 and y == n - 1 and tx == n and ty == n)):
        ans = 4;
    else:

        # dp[a][b], here a, b is the difference of
        # x & tx and y & ty respectively.
        dp[1][0] = 3;
        dp[0][1] = 3;
        dp[1][1] = 2;
        dp[2][0] = 2;
        dp[0][2] = 2;
        dp[2][1] = 1;
        dp[1][2] = 1;

        ans = getsteps(x, y, tx, ty);

    print(ans);

# This code is contributed by PrinciRaj1992
```

## C#

```
// C# code for minimum steps for
// a knight to reach target position

using System;
public class GFG{

// initializing the matrix.
    static int [ , ]dp = new int[8 , 8];

    static int getsteps(int x, int y,
            int tx, int ty) {
        // if knight is on the target
        // position return 0.
        if (x == tx && y == ty) {
            return dp[0 , 0];
        } else // if already calculated then return
        // that value. Taking  Absolute difference.
        if (dp[ Math. Abs(x - tx) , Math. Abs(y - ty)] != 0) {
            return dp[ Math. Abs(x - tx) , Math. Abs(y - ty)];
        } else {

            // there will be two distinct positions
            // from the knight towards a target.
            // if the target is in same row or column
            // as of knight than there can be four
            // positions towards the target but in that
            // two would be the same and the other two
            // would be the same.
            int x1, y1, x2, y2;

            // (x1, y1) and (x2, y2) are two positions.
            // these can be different according to situation.
            // From position of knight, the chess board can be
            // divided into four blocks i.e.. N-E, E-S, S-W, W-N .
            if (x <= tx) {
                if (y <= ty) {
                    x1 = x + 2;
                    y1 = y + 1;
                    x2 = x + 1;
                    y2 = y + 2;
                } else {
                    x1 = x + 2;
                    y1 = y - 1;
                    x2 = x + 1;
                    y2 = y - 2;
                }
            } else if (y <= ty) {
                x1 = x - 2;
                y1 = y + 1;
                x2 = x - 1;
                y2 = y + 2;
            } else {
                x1 = x - 2;
                y1 = y - 1;
                x2 = x - 1;
                y2 = y - 2;
            }

            // ans will be, 1 + minimum of steps
            // required from (x1, y1) and (x2, y2).
            dp[ Math. Abs(x - tx) , Math. Abs(y - ty)]
                    = Math.Min(getsteps(x1, y1, tx, ty),
                            getsteps(x2, y2, tx, ty)) + 1;

            // exchanging the coordinates x with y of both
            // knight and target will result in same ans.
            dp[ Math. Abs(y - ty) , Math. Abs(x - tx)]
                    = dp[ Math. Abs(x - tx) , Math. Abs(y - ty)];
            return dp[ Math. Abs(x - tx) , Math. Abs(y - ty)];
        }
    }

// Driver Code
    static public void Main() {
        int i, n, x, y, tx, ty, ans;

        // size of chess board n*n
        n = 100;

        // (x, y) coordinate of the knight.
        // (tx, ty) coordinate of the target position.
        x = 4;
        y = 5;
        tx = 1;
        ty = 1;

        // (Exception) these are the four corner points
        // for which the minimum steps is 4.
        if ((x == 1 && y == 1 && tx == 2 && ty == 2)
                || (x == 2 && y == 2 && tx == 1 && ty == 1)) {
            ans = 4;
        } else if ((x == 1 && y == n && tx == 2 && ty == n - 1)
                || (x == 2 && y == n - 1 && tx == 1 && ty == n)) {
            ans = 4;
        } else if ((x == n && y == 1 && tx == n - 1 && ty == 2)
                || (x == n - 1 && y == 2 && tx == n && ty == 1)) {
            ans = 4;
        } else if ((x == n && y == n && tx == n - 1 && ty == n - 1)
                || (x == n - 1 && y == n - 1 && tx == n && ty == n)) {
            ans = 4;
        } else {
            // dp[a , b], here a, b is the difference of
            // x & tx and y & ty respectively.
            dp[1 , 0] = 3;
            dp[0 , 1] = 3;
            dp[1 , 1] = 2;
            dp[2 , 0] = 2;
            dp[0 , 2] = 2;
            dp[2 , 1] = 1;
            dp[1 , 2] = 1;

            ans = getsteps(x, y, tx, ty);
        }

        Console.WriteLine(ans);
    }
}

/*This code is contributed by PrinciRaj1992*/
```

**Output:** 

```
3
```

**时间复杂度:** O(N * M)其中 N 为总行数，M 为总列数
T3】辅助空间: O(N * M)