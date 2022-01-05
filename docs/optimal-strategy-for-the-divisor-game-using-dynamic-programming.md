# 使用动态规划的除数游戏的最优策略

> 原文:[https://www . geeksforgeeks . org/最优策略除数游戏使用动态编程/](https://www.geeksforgeeks.org/optimal-strategy-for-the-divisor-game-using-dynamic-programming/)

给定一个**整数 N** 和两个玩家，A 和 B 在玩一个游戏。在每个玩家的回合中，该玩家通过**从当前 N 中减去当前 N 的除数**(小于 N)，从而**形成下一回合的新 n** 。没有任何除数可减的玩家输掉游戏。任务是告诉哪一个玩家赢了游戏，如果玩家 A 第一个回合，假设两个玩家都玩得最好。
**举例:**

> **输入:** N = 2
> **输出:**A 玩家赢
> **说明:**
> A 玩家选择 1，B 没有更多招式。
> **输入:** N = 3
> **输出:**玩家 B 胜
> **说明:**
> 玩家 A 选 1，玩家 B 选 1，A 没有更多的招式。

**方法:**
上面提到的这个问题可以用**动态规划来解决。**

*   我们将采用一个具有 2 个状态的 DP，即

> N ->当前数字左
> A - >布尔值决定是否轮到玩家 A

*   在每个状态下，我们将尝试找到 N 的所有除数，并将尝试找到当前玩家获胜的下一个状态。对于玩家 A，我们将尝试找到返回值为真的下一个状态，而对于玩家 B，我们将尝试找到返回值为假的下一个状态(因为假代表玩家 A 的损失)。
*   基本情况是 N=1，玩家 A 总是会输，N=2，玩家 B 总是会输。
*   要找到答案，我们只需要找到 DP[ N ][ 1 ]的值。

**以下是上述方法的实施:**

## C++

```
// C++ program for implementation of
// Optimal Strategy for the Divisor
// Game using Dynamic Programming
#include <bits/stdc++.h>
using namespace std;

// Recursive function to find the winner
bool divisorGame(int N, bool A, int dp[][2])
{

    // check if N=1 or N=3 then player B wins
    if (N == 1 or N == 3)
        return false;

    // check if N=2 then player A wins
    if (N == 2)
        return true;

    // check if current state already visited
    // then return the previously obtained ans
    if (dp[N][A] != -1)
        return dp[N][A];

    // check if currently it is player A's turn
    // then initialise the ans to 0
    int ans = (A == 1) ? 0 : 1;

    // Traversing across all the divisors of N
    // which are less than N
    for (int i = 1; i * i <= N; i++) {

        // check if current value of
        // i is a divisor of N
        if (N % i == 0) {

            // check if it is player A's turn
            // then we need at least one true
            if (A)
                ans |= divisorGame(N - i, 0, dp);

            // Else if it is player B's turn
            // then we need at least one false
            else
                ans &= divisorGame(N - i, 1, dp);
        }
    }

    // Return the current ans
    return dp[N][A] = ans;
}

// Driver code
int main()
{
    // initialise N
    int N = 3;

    int dp[N + 1][2];

    memset(dp, -1, sizeof(dp));

    if (divisorGame(N, 1, dp) == true)
        cout << "Player A wins";
    else
        cout << "Player B wins";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for implementation of
// optimal strategy for the divisor
// game using dynamic programming

import java.util.*;

class GFG {

    // Recursive function to find the winner
    static int divisorGame(int N, int A, int dp[][]) {

        // Check if N = 1 or N = 3 then player B wins
        if (N == 1 || N == 3)
            return 0;

        // Check if N = 2 then player A wins
        if (N == 2)
            return 1;

        // Check if current state already visited
        // then return the previously obtained ans
        if (dp[N][A] != -1)
            return dp[N][A];

        // Check if currently it is player A's turn
        // then initialise the ans to 0
        int ans = (A == 1) ? 0 : 1;

        // Traversing across all the divisors of N
        // which are less than N
        for (int i = 1; i * i <= N; i++) {

            // Check if current value of
            // i is a divisor of N
            if (N % i == 0) {

                // Check if it is player A's turn
                // then we need at least one true
                if (A == 1)
                    ans |= divisorGame(N - i, 0, dp);

                // Else if it is player B's turn
                // then we need at least one false
                else
                   ans &= divisorGame(N - i, 1, dp);
            }
        }

        // Return the current ans
        return dp[N][A] = ans;
    }

    // Driver code
    public static void main(String[] args) {

        // Initialise N
        int N = 3;

        int[][] dp = new int[N + 1][2];

        for (int i = 0; i < N + 1; i++) {
             for (int j = 0; j < 2; j++) {
                  dp[i][j] = -1;
            }
        }

        if (divisorGame(N, 1, dp) == 1)
            System.out.print("Player A wins");
        else
            System.out.print("Player B wins");

    }
}

// This code contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 program for implementation of
# Optimal Strategy for the Divisor
# Game using Dynamic Programming

from math import sqrt

# Recursive function to find the winner
def divisorGame(N,A,dp):
    # check if N=1 or N=3 then player B wins
    if (N == 1 or N == 3):
        return False

    # check if N=2 then player A wins
    if (N == 2):
        return True

    # check if current state already visited
    # then return the previously obtained ans
    if (dp[N][A] != -1):
        return dp[N][A]

    # check if currently it is player A's turn
    # then initialise the ans to 0
    if(A == 1):
        ans = 0
    else:
        ans = 1

    # Traversing across all the divisors of N
    # which are less than N
    for i in range(1,int(sqrt(N))+1,1):
        # check if current value of
        # i is a divisor of N
        if (N % i == 0):
            # check if it is player A's turn
            # then we need at least one true
            if (A):
                ans |= divisorGame(N - i, 0, dp)

            # Else if it is player B's turn
            # then we need at least one false
            else:
                ans &= divisorGame(N - i, 1, dp)

    dp[N][A] = ans

    # Return the current ans
    return dp[N][A]

# Driver code
if __name__ == '__main__':
    # initialise N
    N = 3

    dp = [[-1 for i in range(2)] for j in range(N+1)]

    if (divisorGame(N, 1, dp) == True):
        print("Player A wins")
    else:
        print("Player B wins")

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# program for implementation of
// optimal strategy for the divisor
// game using dynamic programming
using System;

class GFG {

// Recursive function to find the winner
static int divisorGame(int N, int A,
                       int [,]dp)
{

    // Check if N = 1 or N = 3
    // then player B wins
    if (N == 1 || N == 3)
        return 0;

    // Check if N = 2 then player A wins
    if (N == 2)
        return 1;

    // Check if current state already visited
    // then return the previously obtained ans
    if (dp[N, A] != -1)
        return dp[N, A];

    // Check if currently it is player A's turn
    // then initialise the ans to 0
    int ans = (A == 1) ? 0 : 1;

    // Traversing across all the divisors of N
    // which are less than N
    for(int i = 1; i * i <= N; i++)
    {

       // Check if current value of
       // i is a divisor of N
       if (N % i == 0)
       {

           // Check if it is player A's turn
           // then we need at least one true
           if (A == 1)
               ans |= divisorGame(N - i, 0, dp);

           // Else if it is player B's turn
           // then we need at least one false
           else
              ans &= divisorGame(N - i, 1, dp);
       }
    }

    // Return the current ans
    return dp[N, A] = ans;
}

// Driver code
public static void Main(String[] args)
{

    // Initialise N
    int N = 3;
    int[,] dp = new int[N + 1, 2];

    for(int i = 0; i < N + 1; i++)
    {
       for(int j = 0; j < 2; j++)
       {
          dp[i, j] = -1;
       }
    }

    if (divisorGame(N, 1, dp) == 1)
    {
        Console.Write("Player A wins");
    }
    else
    {
        Console.Write("Player B wins");
    }
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>
// Javascript program for implementation of
// Optimal Strategy for the Divisor
// Game using Dynamic Programming

// Recursive function to find the winner
function divisorGame(N, A, dp) {

    // check if N=1 or N=3 then player B wins
    if (N == 1 || N == 3)
        return false;

    // check if N=2 then player A wins
    if (N == 2)
        return true;

    // check if current state already visited
    // then return the previously obtained ans
    if (dp[N][A] != -1)
        return dp[N][A];

    // check if currently it is player A's turn
    // then initialise the ans to 0
    let ans = (A == 1) ? 0 : 1;

    // Traversing across all the divisors of N
    // which are less than N
    for (let i = 1; i * i <= N; i++) {

        // check if current value of
        // i is a divisor of N
        if (N % i == 0) {

            // check if it is player A's turn
            // then we need at least one true
            if (A)
                ans |= divisorGame(N - i, 0, dp);

            // Else if it is player B's turn
            // then we need at least one false
            else
                ans &= divisorGame(N - i, 1, dp);
        }
    }

    // Return the current ans
    return dp[N][A] = ans;
}

// Driver code

// initialise N
let N = 3;

let dp = [];

for (let i = 0; i < N + 1; i++) {
    let temp = [-1]
    for (let j = 0; j < 2; j++) {
        temp.push([-1])
    }
    dp.push(temp)
}

// memset(dp, -1, sizeof(dp));

if (divisorGame(N, 1, dp) == true)
    document.write("Player A wins");
else
    document.write("Player B wins");

// This code is contributed by gfgking
</script>
```

**Output:** 

```
Player B wins
```