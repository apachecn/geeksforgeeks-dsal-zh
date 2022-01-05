# 硬币游戏赢家，每个玩家有三个选择

> 原文:[https://www . geesforgeks . org/coin-game-winner-ever-player-三选一/](https://www.geeksforgeeks.org/coin-game-winner-every-player-three-choices/)

甲和乙正在玩游戏。一开始有 **n** 个硬币。再给两个数字 x 和 y。在每一步中，玩家可以选择 x 或 y 或 1 个硬币。a 总是开始游戏。选择最后一枚硬币的玩家赢得游戏，或者不能选择任何硬币的人输掉游戏。对于给定的 n 值，找出如果 A 和 b 都以最佳状态玩游戏，A 是否会赢。

示例:

```
Input :  n = 5, x = 3, y = 4
Output : A
There are 5 coins, every player can pick 1 or
3 or 4 coins on his/her turn.
A can win by picking 3 coins in first chance.
Now 2 coins will be left so B will pick one 
coin and now A can win by picking the last coin.

Input : 2 3 4
Output : B
```

让我们举几个 x = 3，y = 4 的 n 值的例子。
n = 0 A 不能挑任何硬币所以他输了
n = 1 A 可以挑 1 个硬币赢游戏
n = 2 A 只能挑 1 个硬币。现在 B 将选择 1 枚硬币并赢得游戏
n = 3 4 A 将通过选择 3 或 4 枚硬币
n = 5 赢得游戏，6 A 将选择 3 或 4 枚硬币。现在 B 必须从 2 个硬币中选择，所以 A 会赢。
我们可以观察到，只有当 B 输掉 n-1 或 n-x 或 n-y 的硬币时，A 才会赢得 n 个硬币的游戏。

## C++

```
// C++ program to find winner of game
// if player can pick 1, x, y coins
#include <bits/stdc++.h>
using namespace std;

// To find winner of game
bool findWinner(int x, int y, int n)
{
    // To store results
    int dp[n + 1];

    // Initial values
    dp[0] = false;
    dp[1] = true;

    // Computing other values.
    for (int i = 2; i <= n; i++) {

        // If A losses any of i-1 or i-x
        // or i-y game then he will
        // definitely win game i
        if (i - 1 >= 0 and !dp[i - 1])
            dp[i] = true;
        else if (i - x >= 0 and !dp[i - x])
            dp[i] = true;
        else if (i - y >= 0 and !dp[i - y])
            dp[i] = true;

        // Else A loses game.
        else
            dp[i] = false;
    }

    // If dp[n] is true then A will
    // game otherwise  he losses
    return dp[n];
}

// Driver program to test findWinner();
int main()
{
    int x = 3, y = 4, n = 5;
    if (findWinner(x, y, n))
        cout << 'A';
    else
        cout << 'B';

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find winner of game
// if player can pick 1, x, y coins
import java.util.Arrays;

public class GFG {

    // To find winner of game
    static boolean findWinner(int x, int y, int n)
    {
        // To store results
        boolean[] dp = new boolean[n + 1];

        Arrays.fill(dp, false);

        // Initial values
        dp[0] = false;
        dp[1] = true;

        // Computing other values.
        for (int i = 2; i <= n; i++) {

            // If A losses any of i-1 or i-x
            // or i-y game then he will
            // definitely win game i
            if (i - 1 >= 0 && dp[i - 1] == false)
                dp[i] = true;
            else if (i - x >= 0 && dp[i - x] == false)
                dp[i] = true;
            else if (i - y >= 0 && dp[i - y] == false)
                dp[i] = true;

            // Else A loses game.
            else
                dp[i] = false;
        }

        // If dp[n] is true then A will
        // game otherwise  he losses
        return dp[n];
    }

    // Driver program to test findWinner();
    public static void main(String args[])
    {
        int x = 3, y = 4, n = 5;
        if (findWinner(x, y, n) == true)
            System.out.println('A');
        else
            System.out.println('B');
    }
}
// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Python3 program to find winner of game
# if player can pick 1, x, y coins

# To find winner of game
def findWinner(x, y, n):

    # To store results
    dp = [0 for i in range(n + 1)]

    # Initial values
    dp[0] = False
    dp[1] = True

    # Computing other values.
    for i in range(2, n + 1):

        # If A losses any of i-1 or i-x
        # or i-y game then he will
        # definitely win game i
        if (i - 1 >= 0 and not dp[i - 1]):
            dp[i] = True
        elif (i - x >= 0 and not dp[i - x]):
            dp[i] = True
        elif (i - y >= 0 and not dp[i - y]):
            dp[i] = True

        # Else A loses game.
        else:
            dp[i] = False

    # If dp[n] is true then A will
    # game otherwise he losses
    return dp[n]

# Driver Code
x = 3; y = 4; n = 5
if (findWinner(x, y, n)):
    print('A')
else:
    print('B')

# This code is contributed by Azkia Anam
```

## C#

```
// C# program to find winner of game
// if player can pick 1, x, y coins
using System;

public class GFG {

    // To find winner of game
    static bool findWinner(int x, int y, int n)
    {

        // To store results
        bool[] dp = new bool[n + 1];

        for(int i = 0; i < n+1; i++)
            dp[i] =false;

        // Initial values
        dp[0] = false;
        dp[1] = true;

        // Computing other values.
        for (int i = 2; i <= n; i++)
        {

            // If A losses any of i-1 or i-x
            // or i-y game then he will
            // definitely win game i
            if (i - 1 >= 0 && dp[i - 1] == false)
                dp[i] = true;
            else if (i - x >= 0 && dp[i - x] == false)
                dp[i] = true;
            else if (i - y >= 0 && dp[i - y] == false)
                dp[i] = true;

            // Else A loses game.
            else
                dp[i] = false;
        }

        // If dp[n] is true then A will
        // game otherwise he losses
        return dp[n];
    }

    // Driver program to test findWinner();
    public static void Main()
    {
        int x = 3, y = 4, n = 5;

        if (findWinner(x, y, n) == true)
            Console.WriteLine('A');
        else
            Console.WriteLine('B');
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find winner of game
// if player can pick 1, x, y coins

// To find winner of game
function findWinner( $x, $y, $n)
{

    // To store results
    $dp= array();

    // Initial values
    $dp[0] = false;
    $dp[1] = true;

    // Computing other values.
    for ($i = 2; $i <= $n; $i++)
    {

        // If A losses any of i-1 or i-x
        // or i-y game then he will
        // definitely win game i
        if ($i - 1 >= 0 and !$dp[$i - 1])
            $dp[$i] = true;
        else if ($i - $x >= 0 and !$dp[$i - $x])
            $dp[$i] = true;
        else if ($i - $y >= 0 and !$dp[$i - $y])
            $dp[$i] = true;

        // Else A loses game.
        else
            $dp[$i] = false;
    }

    // If dp[n] is true then A will
    // game otherwise he losses
    return $dp[$n];
}

// Driver program to test findWinner();
    $x = 3; $y = 4; $n = 5;
    if (findWinner($x, $y, $n))
        echo 'A';
    else
        echo 'B';

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Javascript program to find winner of game
// if player can pick 1, x, y coins

// To find winner of game
function findWinner(x, y, n)
{

    // To store results
    var dp = Array(n + 1).fill(0);

    // Initial values
    dp[0] = false;
    dp[1] = true;

    // Computing other values.
    for(var i = 2; i <= n; i++)
    {

        // If A losses any of i-1 or i-x
        // or i-y game then he will
        // definitely win game i
        if (i - 1 >= 0 && !dp[i - 1])
            dp[i] = true;
        else if (i - x >= 0 && !dp[i - x])
            dp[i] = true;
        else if (i - y >= 0 && !dp[i - y])
            dp[i] = true;

        // Else A loses game.
        else
            dp[i] = false;
    }

    // If dp[n] is true then A will
    // game otherwise he losses
    return dp[n];
}

// Driver code
var x = 3, y = 4, n = 5;
if (findWinner(x, y, n))
    document.write('A');
else
    document.write('B');

// This code is contributed by noob2000

</script>
```

**输出:**

```
A
```

本文由 [**核素**](https://www.facebook.com/nuclode) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。