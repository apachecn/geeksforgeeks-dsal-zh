# 通过移除最后一张给定的 N 张牌

找到赢得游戏的玩家

> 原文:[https://www . geesforgeks . org/通过移除最后一张给定的 n 张牌来找到赢得游戏的玩家/](https://www.geeksforgeeks.org/find-the-player-who-wins-the-game-by-removing-the-last-of-given-n-cards/)

给定两个整数 **N** 和 **K** ，其中 **N** 表示游戏开始时出现的牌总数， **K** 表示单回合可以移除的最大牌数。两名玩家 **A** 和 **B** 轮流最多移除 **K** 张牌，从玩家 A 开始逐一移除，移除最后一张牌的玩家即为赢家。任务是检查 **A** 能否赢得比赛。如果发现是真的，打印**‘A’**作为答案。否则，打印**‘B’**。

**示例:**

> **输入:** N = 14，K = 10
> **输出:**是
> **说明:**
> 回合 1: A 第一回合移除 3 张牌。
> 第 2 回合:B 从范围【1–10】
> 中移除任意数量的牌，最后 A 可以移除所有剩余牌并赢得游戏，因为第 2 回合后剩余牌的数量将≤ 10
> 
> **输入:** N = 11，K=10
> **输出:**否

**进场:**这里的思路是观察每当**的值为 N % (K + 1) = 0** 时，那么 **A** 将永远无法赢得比赛。否则 **A** 永远赢不了比赛。
**证明:**

> 1.  **If N ≤ K:** The person who has the first round will win the game, that is, A. 。
> 2.  **If n = k+1:** A can remove any number of cards within the range of **[1, k]** . So the total number of cards left after the first round is also in the range of **[1,k]** . B now gets the turn, and the number of cards left is within the range of **[1, k]** . So, B will win the game.
> 3.  **If K+2 ≤ N ≤ 2K+1:** A removes N -( K+1) cards in the first round. B Any number of cards within the range of **[1,k]** can be removed in the next round. So now the total number of cards left is within the range of **[1,k]** . Now, because the remaining cards are in the range of **[1, k]** , A can remove all the cards and win the game.

所以思路是检查 **N % (K + 1)** 是否等于 0。如果发现是真的，打印 B 作为获胜者。否则，打印 A 作为获胜者。
以下是上述办法的实施情况:

## C++

```
// C++ Program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check which
// player can win the game
void checkWinner(int N, int K)
{
    if (N % (K + 1)) {
        cout << "A";
    }
    else {
        cout << "B";
    }
}

// Driver code
int main()
{

    int N = 50;
    int K = 10;
    checkWinner(N, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to check which
// player can win the game
static void checkWinner(int N, int K)
{
    if (N % (K + 1) > 0)
    {
        System.out.print("A");
    }
    else
    {
        System.out.print("B");
    }
}

// Driver code
public static void main(String[] args)
{
    int N = 50;
    int K = 10;

    checkWinner(N, K);
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to check which
# player can win the game
def checkWinner(N, K):

    if(N % (K + 1)):
        print("A")
    else:
        print("B")

# Driver Code
N = 50
K = 10

# Function call
checkWinner(N, K)

# This code is contributed by Shivam Singh
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to check which
// player can win the game
static void checkWinner(int N, int K)
{
    if (N % (K + 1) > 0)
    {
        Console.Write("A");
    }
    else
    {
        Console.Write("B");
    }
}

// Driver code
public static void Main(String[] args)
{
    int N = 50;
    int K = 10;

    checkWinner(N, K);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
    // Javascript Program to implement
// the above approach

// Function to check which
// player can win the game
function checkWinner(N, K)
{
    if (N % (K + 1)) {
        document.write("A");
    }
    else {
        document.write("B");
    }
}

// Driver code

    let N = 50;
    let K = 10;
    checkWinner(N, K);

// This code is contributed by Saurabh Jaiswal
</script>
```

**Output:** 

```
A
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)