# 用 N 堆箱子找到游戏的赢家

> 原文:[https://www . geeksforgeeks . org/找到 n 堆盒子游戏的赢家/](https://www.geeksforgeeks.org/find-the-winner-of-the-game-with-n-piles-of-boxes/)

给定仅包含白色(W)和黑色(B)盒子的 **N** 堆，两个玩家 A 和 B 玩一个游戏。
玩家 A 可以从最上面盒子为白色的堆的顶部移除任意数量的盒子，玩家 B 可以从最上面盒子为黑色的堆的顶部移除任意数量的盒子。如果有一堆顶部为 W，那么玩家 A 必须移除一个或多个盒子。同样，如果有一堆顶部为 B 的，那么玩家 B 必须移除一个或多个盒子。他们交替上场，由**选手甲**率先移动。两位选手都打得很好。
任务是找到游戏的赢家(不能做最后一招的)。**最后移动的玩家输掉游戏**。
**举例:**

> 输入:N = 2
> BWB WBW
> 输出:A
> 玩家 A 可以从 1 号堆中移除所有箱子。现在玩家 B 要从 2 堆中做出选择。无论玩家 B 做出什么选择，他/她都必须做出最后一步。
> 输入:N = 3
> WWWW、WB、WBBW
> 输出:B

**进场:**最后一招的玩家输掉比赛的博弈论问题，叫做米塞尼姆的游戏。

1.  如果在任何一堆中有连续出现的同一个盒子，我们可以简单地用同一个盒子的一个副本来替换它们，因为移除出现在顶部的盒子的所有出现是最佳的。所以，我们可以压缩所有的桩，得到 BWBWBW 或 WBWB 形式的桩。
2.  现在，假设有一个堆，它的最上面的盒子不同于它最下面的盒子，我们可以证明即使没有这个堆，答案仍然是一样的，因为如果一个玩家在这个堆上移动，另一个玩家通过从同一个堆中移除盒子来进行下一个移动，导致第一个玩家的位置完全相同。
3.  如果一个筹码堆的最上面和最下面的方块相同，它需要一个或者玩家多走一步。所以，只要数一数每个玩家必须额外移动的次数。没有多余招式的玩家先赢。

**以下是上述办法的实施情况。**

## C++

```
// Program to find winner of the game
#include <bits/stdc++.h>
using namespace std;

// Function to return find winner of game
string Winner(int n, string pile[])
{

    int a = 0, b = 0;
    for (int i = 0; i < n; ++i) {
        int l = pile[i].length();

        // Piles begins and ends with White box 'W'
        if (pile[i][0] == pile[i][l - 1] && pile[i][0] == 'W')
            a++;

        // Piles begins and ends with Black box 'B'
        if (pile[i][0] == pile[i][l - 1] && pile[i][0] == 'B')
            b++;
    }
    if (a <= b)
        return "A";
    else
        return "B";
}

// Driver code
int main()
{

    int n = 2;
    string pile[n] = { "WBW", "BWB" };

    // function to print required answer
    cout << Winner(n, pile);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Program to find winner of the game
class GFG
{

// Function to return find winner of game
static String Winner(int n, String []pile)
{

    int a = 0, b = 0;
    for (int i = 0; i < n; ++i)
    {
        int l = pile[i].length();

        // Piles begins and ends with White box 'W'
        if (pile[i].charAt(0) == pile[i].charAt(l - 1) &&
            pile[i].charAt(0) == 'W')
            a++;

        // Piles begins and ends with Black box 'B'
        if (pile[i].charAt(0) == pile[i].charAt(l - 1) &&
            pile[i].charAt(0) == 'B')
            b++;
    }
    if (a <= b)
        return "A";
    else
        return "B";
}

// Driver code
public static void main(String[] args)
{
    int n = 2;
    String pile[] = { "WBW", "BWB" };

    // function to print required answer
    System.out.println(Winner(n, pile));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 code to find winner of the game

# Function to return find winner of game
def Winner(n, pile):

    a, b = 0, 0
    for i in range(0, n):
        l = len(pile[i])

        # Piles begins and ends with White box 'W'
        if (pile[i][0] == pile[i][l - 1] and
            pile[i][0] == 'W'):
            a += 1

        # Piles begins and ends with Black box 'B'
        if (pile[i][0] == pile[i][l - 1] and
            pile[i][0] == 'B'):
            b += 1

    if a <= b:
        return "A"
    else:
        return "B"

# Driver code
if __name__ == "__main__":

    n = 2
    pile = ["WBW", "BWB"]

    # function to print required answer
    print(Winner(n, pile))

# This code is contributed by Rituraj Jain
```

## C#

```
// Program to find winner of the game
using System;

class GFG
{

// Function to return find winner of game
static String Winner(int n, String []pile)
{
    int a = 0, b = 0;
    for (int i = 0; i < n; ++i)
    {
        int l = pile[i].Length;

        // Piles begins and ends with White box 'W'
        if (pile[i][0] == pile[i][l - 1] &&
            pile[i][0] == 'W')
            a++;

        // Piles begins and ends with Black box 'B'
        if (pile[i][0] == pile[i][l - 1] &&
            pile[i][0] == 'B')
            b++;
    }
    if (a <= b)
        return "A";
    else
        return "B";
}

// Driver code
public static void Main(String[] args)
{
    int n = 2;
    String []pile = { "WBW", "BWB" };

    // function to print required answer
    Console.WriteLine(Winner(n, pile));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Program to find winner of the game

// Function to return find winner of game
function Winner(n, pile)
{

    var a = 0, b = 0;
    for (var i = 0; i < n; ++i) {
        var l = pile[i].length;

        // Piles begins and ends with White box 'W'
        if (pile[i][0] == pile[i][l - 1] && pile[i][0] == 'W')
            a++;

        // Piles begins and ends with Black box 'B'
        if (pile[i][0] == pile[i][l - 1] && pile[i][0] == 'B')
            b++;
    }
    if (a <= b)
        return "A";
    else
        return "B";
}

// Driver code
var n = 2;
var pile = ["WBW", "BWB"];

// function to print required answer
document.write( Winner(n, pile));

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
A
```

**时间复杂度:** O(N)