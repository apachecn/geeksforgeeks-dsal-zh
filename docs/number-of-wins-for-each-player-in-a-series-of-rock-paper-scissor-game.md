# 一系列石头-纸-剪刀游戏中每个玩家的获胜次数

> 原文:[https://www . geeksforgeeks . org/一系列石头纸剪刀游戏中每个玩家的获胜次数/](https://www.geeksforgeeks.org/number-of-wins-for-each-player-in-a-series-of-rock-paper-scissor-game/)

两名玩家正在玩[石头-纸-剪刀](https://en.wikipedia.org/wiki/Rock%E2%80%93paper%E2%80%93scissors)系列游戏。一共玩了 **K** 游戏。玩家 1 有一系列由弦 **A** 表示的动作，类似地，玩家 2 有弦 **B** 。如果任何一个玩家到达了他们的绳子的末端，他们就会回到绳子的起点。任务是计算每个玩家在玩 **K** 游戏时的游戏数量。

**示例:**

> **输入:** k = 4，a = "SR "，b = " R "
> T3】输出: 0 2
> 游戏 1:玩家 1 = S，玩家 2 = R，胜者=玩家 2
> 游戏 2:玩家 1 = R，玩家 2 = R，胜者=平局
> 游戏 3:玩家 1 = S，玩家 2 = R，胜者=玩家 2
> 游戏 4:玩家 1 = R，玩家 2 = R，胜者=平局
> 
> **输入:** k = 3，a =“S”，b =“SSS”
> T3】输出: 0 0
> 所有游戏均为平局。

**进场:**让弦长 **a** 为 **n** ，弦长 **b** 为 **m** 。这里的观察是游戏会在 **n * m** 移动后重复。所以，我们可以模拟 **n * m** 游戏的过程，然后统计它被重复的次数。对于剩下的游戏，我们可以再次模拟这个过程，因为它现在将小于 **n * m** 。例如，在上面的第一个例子中， **n = 2** 和 **m = 1** 。所以，游戏会在每一次 **n * m = 2 * 1 = 2** 移动后重复，即**(玩家 2，抽奖)**、**(玩家 2，抽奖)**、…..，**(玩家 2，抽奖)**。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns 1 if first player wins,
// 0 in case of a draw and -1 if second player wins
int compare(char first, char second)
{
    // If both players have the same move
    // then it's a draw
    if (first == second)
        return 0;

    if (first == 'R') {
        if (second == 'S')
            return 1;
        else
            return -1;
    }
    if (first == 'P') {
        if (second == 'R')
            return 1;
        else
            return -1;
    }
    if (first == 'S') {
        if (second == 'P')
            return 1;
        else
            return -1;
    }
}

// Function that returns the count of games
// won by both the players
pair<int, int> countWins(int k, string a, string b)
{
    int n = a.length();
    int m = b.length();
    int i = 0, j = 0;

    // Total distinct games that can be played
    int moves = n * m;
    pair<int, int> wins = { 0, 0 };
    while (moves--) {
        int res = compare(a[i], b[j]);

        // Player 1 wins the current game
        if (res == 1)
            wins.first++;

        // Player 2 wins the current game
        if (res == -1)
            wins.second++;
        i = (i + 1) % n;
        j = (j + 1) % m;
    }

    // Number of times the above n * m games repeat
    int repeat = k / (n * m);

    // Update the games won
    wins.first *= repeat;
    wins.second *= repeat;

    // Remaining number of games after
    // removing repeated games
    int rem = k % (n * m);
    while (rem--) {
        int res = compare(a[i], b[j]);

        // Player 1 wins the current game
        if (res == 1)
            wins.first++;

        // Player 2 wins the current game
        if (res == -1)
            wins.second++;
        i = (i + 1) % n;
        j = (j + 1) % m;
    }
    return wins;
}

// Driver code
int main()
{
    int k = 4;
    string a = "SR", b = "R";
    auto wins = countWins(k, a, b);
    cout << wins.first << " " << wins.second;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;
import java.awt.Point;

class GFG{

// Function that returns 1 if first player wins,
// 0 in case of a draw and -1 if second player wins
public static int compare(char first, char second)
{

    // If both players have the same move
    // then it's a draw
    if (first == second)
        return 0;

    if (first == 'R')
    {
        if (second == 'S')
            return 1;
        else
            return -1;
    }
    if (first == 'P')
    {
        if (second == 'R')
            return 1;
        else
            return -1;
    }
    if (first == 'S')
    {
        if (second == 'P')
            return 1;
        else
            return -1;
    }

    return 0;
}

// Function that returns the count of games
// won by both the players
public static Point countWins(int k, String a,
                                     String b)
{
    int n = a.length();
    int m = b.length();
    int i = 0, j = 0;

    // Total distinct games that
    // can be played
    int moves = n * m;
    Point wins = new Point (0, 0);

    while (moves-- > 0)
    {
        int res = compare(a.charAt(i),
                          b.charAt(j));

        // Player 1 wins the current game
        if (res == 1)
            wins = new Point(wins.x + 1,
                             wins.y);

        // Player 2 wins the current game
        if (res == -1)
            wins = new Point(wins.x,
                             wins.y + 1);

        i = (i + 1) % n;
        j = (j + 1) % m;
    }

    // Number of times the above
    // n * m games repeat
    int repeat = k / (n * m);

    // Update the games won
    wins = new Point(wins.x * repeat,
                     wins.y * repeat);

    // Remaining number of games after
    // removing repeated games
    int rem = k % (n * m);

    while (rem-- > 0)
    {
        int res = compare(a.charAt(i),
                          b.charAt(j));

        // Player 1 wins the current game
        if (res == 1)
            wins = new Point(wins.x + 1,
                             wins.y);

        // Player 2 wins the current game
        if (res == -1)
            wins = new Point(wins.x,
                             wins.y + 1);

        i = (i + 1) % n;
        j = (j + 1) % m;
    }
    return wins;
} 

// Driver code
public static void main(String[] args)
{
    int k = 4;
    String a = "SR", b = "R";
    Point wins = countWins(k, a, b);

    System.out.println(wins.x + " " + wins.y);
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function that returns 1 if first
# player wins, 0 in case of a draw
# and -1 if second player wins
def compare(first, second):

    # If both players have the same
    # move then it's a draw
    if (first == second):
        return 0

    if (first == 'R'):
        if (second == 'S'):
            return 1
        else:
            return -1

    if (first == 'P'):
        if (second == 'R'):
            return 1
        else:
            return -1

    if (first == 'S'):
        if (second == 'P'):
            return 1
        else:
            return -1

# Function that returns the count
# of games won by both the players
def countWins(k, a, b):

    n = len(a)
    m = len(b)
    i = 0
    j = 0

    # Total distinct games that
    # can be played
    moves = n * m
    wins = [ 0, 0 ]

    while (moves > 0):
        res = compare(a[i], b[j])

        # Player 1 wins the current game
        if (res == 1):
            wins[0] += 1

        # Player 2 wins the current game
        if (res == -1):
            wins[1] += 1

        i = (i + 1) % n
        j = (j + 1) % m
        moves -= 1

    # Number of times the above
    # n * m games repeat
    repeat = k // (n * m)

    # Update the games won
    wins[0] *= repeat
    wins[1] *= repeat

    # Remaining number of games after
    # removing repeated games
    rem = k % (n * m)
    while (rem > 0):
        res = compare(a[i], b[j])

        # Player 1 wins the current game
        if (res == 1):
            wins[0] += 1

        # Player 2 wins the current game
        if (res == -1):
            wins[1] += 1

        i = (i + 1) % n
        j = (j + 1) % m

    return wins

# Driver code
if __name__ == "__main__":

    k = 4
    a = "SR"
    b = "R"

    wins = countWins(k, a, b);

    print(wins[0], wins[1])

# This code is contributed by chitranayal
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections.Generic; 

class GFG{

// Function that returns 1 if first player
// wins, 0 in case of a draw and -1 if
// second player wins
static int compare(char first, char second)
{

    // If both players have the same
    // move then it's a draw
    if (first == second)
        return 0;

    if (first == 'R')
    {
        if (second == 'S')
            return 1;
        else
            return -1;
    }
    if (first == 'P')
    {
        if (second == 'R')
            return 1;
        else
            return -1;
    }
    if (first == 'S')
    {
        if (second == 'P')
            return 1;
        else
            return -1;
    }
    return 0;
}

// Function that returns the count of games
// won by both the players
static Tuple<int, int> countWins(int k, string a,
                                        string b)
{
    int n = a.Length;
    int m = b.Length;
    int i = 0, j = 0;

    // Total distinct games that
    // can be played
    int moves = n * m;
    Tuple<int, int> wins = Tuple.Create(0, 0);

    while (moves-- > 0)
    {
        int res = compare(a[i], b[j]);

        // Player 1 wins the current game
        if (res == 1)
            wins = Tuple.Create(wins.Item1 + 1,
                                wins.Item2);

        // Player 2 wins the current game
        if (res == -1)
            wins = Tuple.Create(wins.Item1,
                                wins.Item2 + 1);

        i = (i + 1) % n;
        j = (j + 1) % m;
    }

    // Number of times the above
    // n * m games repeat
    int repeat = k / (n * m);

    // Update the games won
    wins = Tuple.Create(wins.Item1 * repeat,
                        wins.Item2 * repeat);

    // Remaining number of games after
    // removing repeated games
    int rem = k % (n * m);

    while (rem-- > 0)
    {
        int res = compare(a[i], b[j]);

        // Player 1 wins the current game
        if (res == 1)
            wins = Tuple.Create(wins.Item1 + 1,
                                wins.Item2);

        // Player 2 wins the current game
        if (res == -1)
            wins = Tuple.Create(wins.Item1,
                                wins.Item2 + 1);

        i = (i + 1) % n;
        j = (j + 1) % m;
    }
    return wins;
}

// Driver Code
static void Main()
{
    int k = 4;
    string a = "SR", b = "R";
    Tuple<int, int> wins = countWins(k, a, b);

    Console.WriteLine(wins.Item1 + " " +
                      wins.Item2);
}
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function that returns 1 if first player wins,
// 0 in case of a draw and -1 if second player wins
function compare(first,second)
{
    // If both players have the same move
    // then it's a draw
    if (first == second)
        return 0;

    if (first == 'R')
    {
        if (second == 'S')
            return 1;
        else
            return -1;
    }
    if (first == 'P')
    {
        if (second == 'R')
            return 1;
        else
            return -1;
    }
    if (first == 'S')
    {
        if (second == 'P')
            return 1;
        else
            return -1;
    }

    return 0;
}

// Function that returns the count of games
// won by both the players
function countWins(k,a,b)
{
    let n = a.length;
    let m = b.length;
    let i = 0, j = 0;

    // Total distinct games that
    // can be played
    let moves = n * m;
    let wins = [0, 0];

    while (moves-- > 0)
    {
        let res = compare(a[i],
                          b[j]);

        // Player 1 wins the current game
        if (res == 1)
            wins = [wins[0] + 1,
                             wins[1]];

        // Player 2 wins the current game
        if (res == -1)
            wins =[wins[0],
                             wins[1] + 1];

        i = (i + 1) % n;
        j = (j + 1) % m;
    }

    // Number of times the above
    // n * m games repeat
    let repeat = k / (n * m);

    // Update the games won
    wins = [wins[0] * repeat,
                     wins[1] * repeat];

    // Remaining number of games after
    // removing repeated games
    let rem = k % (n * m);

    while (rem-- > 0)
    {
        let res = compare(a[i],
                          b[j]);

        // Player 1 wins the current game
        if (res == 1)
            wins = [wins[0] + 1,
                             wins[1]];

        // Player 2 wins the current game
        if (res == -1)
            wins = [wins[0],
                             wins[1] + 1];

        i = (i + 1) % n;
        j = (j + 1) % m;
    }
    return wins;
}

// Driver code
let k = 4;
let a = "SR", b = "R";
let wins = countWins(k, a, b);
document.write(wins[0] + " " + wins[1]);

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
0 2
```

**时间复杂度:**O(N * M)
T3】辅助空间: O(1)