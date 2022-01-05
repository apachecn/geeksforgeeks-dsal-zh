# 找到将赢得硬币游戏的玩家

> 原文:[https://www . geeksforgeeks . org/find-the-player-what-will-the-wind-the-player-what-coin-game/](https://www.geeksforgeeks.org/find-the-player-who-will-win-the-coin-game/)

给定 **N** 个硬币，任务是找出硬币游戏谁赢。
硬币游戏是一种游戏，其中每个玩家从给定的 **N** 硬币中挑选硬币，这样他可以一次挑选 1 到 5 个硬币，游戏对两个玩家都继续。选择最后一枚硬币的玩家输掉游戏。
**例:**

```
Input: N = 4
Output: First Player
Explanation:
Player 1 pick 3 coins and 
Player 2 pick last coin

Input: N = 7
Output: Second Player
```

**进场:**

*   因为玩家可以拿 1 到 5 个硬币，如果一个玩家输了，这意味着他只有 1 个硬币，否则，他可能比可用硬币少拿 1 个硬币，迫使另一个玩家输。所以现在我们将考虑第二个玩家将要赢的情况，这意味着第一个玩家只有一枚硬币。
*   对于 N = 1，第二个玩家要赢了，对于 N = 2 到 6，第一个玩家可以选择比 N 少 1 个硬币，并强制第二个玩家输，所以丢弃它们，对于 N = 7，第一个玩家可以选择硬币 1 到 5，这将留下 6 到 2 之间的硬币，然后第二个玩家可以选择 1 到 5，要赢，第二个玩家将智能地选择少 1 个硬币，强制第一个松动， 所以基本上从 1 开始，所有差距为 6 的数字(无论第一个玩家选择什么，第二个玩家都会选择等于 6 的硬币和第一个玩家选择的硬币)将是第二个玩家的赢家。
*   最后，我们只需要检查 n 是否是 6*c+1 的形式，如果是，那么第二个玩家会赢，否则，第一个玩家会赢。

以下是上述方法的实现:

## C++

```
// C++ program to find the player
// who wins the game

#include <bits/stdc++.h>
using namespace std;

// Function to check the
// wining player
void findWinner(int n)
{
    // As discussed in the
    // above approach
    if ((n - 1) % 6 == 0) {
        cout << "Second Player wins the game";
    }
    else {
        cout << "First Player wins the game";
    }
}

// Driver function
int main()
{

    int n = 7;
    findWinner(n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the player
// who wins the game
class GFG
{

// Function to check the
// wining player
static void findWinner(int n)
{
    // As discussed in the
    // above approach
    if ((n - 1) % 6 == 0)
    {
        System.out.println("Second Player wins the game");
    }
    else
    {
        System.out.println("First Player wins the game");
    }
}

// Driver Code
public static void main(String[] args)
{
    int n = 7;
    findWinner(n);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to find the player
# who wins the game

# Function to check the
# wining player
def findWinner(n):

    # As discussed in the
    # above approach
    if ((n - 1) % 6 == 0):
        print("Second Player wins the game");
    else:
        print("First Player wins the game");

# Driver Code
if __name__ == '__main__':
    n = 7;
    findWinner(n);

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program to find the player
// who wins the game

using System;

class GFG
{

    // Function to check the
    // wining player
    static void findWinner(int n)
    {
        // As discussed in the
        // above approach
        if ((n - 1) % 6 == 0)
        {
            Console.WriteLine("Second Player wins the game");
        }
        else
        {
            Console.WriteLine("First Player wins the game");
        }
    }

    // Driver Code
    public static void Main()
    {
        int n = 7;
        findWinner(n);
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// JavaScript program to find the player
// who wins the game

// Function to check the
// wining player
function findWinner(n)
{
    // As discussed in the
    // above approach
    if ((n - 1) % 6 == 0) {
        document.write("Second Player wins the game");
    }
    else {
        document.write("First Player wins the game");
    }
}

// Driver function
var n = 7;
findWinner(n);

</script>
```

**输出:**

```
Second Player wins the game
```

**时间复杂度:** ![O(1)  ](img/9cbdffa02bee5194f6140e6dd1bd796e.png "Rendered by QuickLaTeX.com")