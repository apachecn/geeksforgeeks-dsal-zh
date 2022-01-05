# 尼姆游戏中的变异

> 原文:[https://www.geeksforgeeks.org/variation-nim-game/](https://www.geeksforgeeks.org/variation-nim-game/)

**先决条件:**
[斯普拉格格朗西定理](https://www.geeksforgeeks.org/combinatorial-game-theory-set-4-sprague-grundy-theorem/)
[格朗迪数字](https://www.geeksforgeeks.org/combinatorial-game-theory-set-3-grundy-numbersnimbers-and-mex/)
[尼姆](https://www.geeksforgeeks.org/combinatorial-game-theory-set-2-game-nim/)是一款著名的游戏，两个玩家轮流从不同的堆中取出物品。在每个回合中，玩家必须从一个非空堆中移除一个或多个物品。游戏的赢家是从最后一个非空堆中移除最后一个物品的玩家。

现在，对于每一个非空堆，任何一个玩家都可以从该堆中移除零个物品，并将其算作他们的移动；不过，这一招每堆只能由任一玩家执行一次。
给定每堆物品的数量，确定谁将赢得比赛；玩家 1 或玩家 2。如果玩家 1 开始游戏并且两者都以最佳方式玩。

示例:

```
Input : 3 [18, 47, 34]
Output : Player 2 wins
G = g(18)^g(47)^g(34) = (17)^(48)^(33) = 0
Grundy number(G), for this game is zero.
Player 2 wins. 

Input : 3 [32, 49, 58]
Output : Player 1 wins
G = g(31)^g(50)^g(57) = (17)^(48)^(33) = 20
Grundy number(G), for this game is non-zero.
Player 1 wins. 
```

**进场:**
每堆的 Grundy 数是根据石子数计算的。为了补偿零移动，我们将不得不修改我们在标准 nim 游戏中使用的 grundy 值。
如果桩的尺寸是奇数；grundy 数字为 size+1，如果桩的大小为偶数，则为
；grundy 数字是 1 号。
我们对所有的 grundy 数值进行异或运算，检查游戏的最终 Grundy 数(G)是否为非零，以决定谁是游戏的赢家。

**说明:**
一个状态的 Grundy 数是**最小的正整数，不能在一次有效的移动中到达**。
因此，我们需要自下而上计算每个 n 的 **mex 值**，这样我们就可以推导出每个 n 的 grundy 数，其中 n 是桩的大小。

**获胜状态**:无论对手做什么，当前玩家都将赢得游戏的一组值。(If G！=0)
**失败状态**:无论对手怎么做，当前玩家都会输掉游戏的一组数值。(如果 G=0)

```
For a given pile size n, we have two states:
(1) n with no zero moves available, 
grundy number will same as standard nim game.
(2) n with zero moves available, we can
reach above state and other states with 
zero moves remaining. 

For, n = 0, g(0) = 0, empty pile

For, n = 1, we can reach two states:
(1) n = 0 (zero move not used)
(2) n = 1 (zero move used)   
Therefore, g(1) = mex{0, 1} which implies
that g(1)=2.

For, n = 2, we can reach :
(1) n = 0 (zero move not used) state 
because this is a valid move.
(2) n = 1 (zero move not used) is a valid
 move, whose grundy number is 2.
Therefore, g(2) = mex{0,2} which implies 
that g(2)=1\. 
note that n=1 (zero move used) is not a valid
move.

If we try to build a solution bottom-up
like this, it turns out that if n is even, 
the grundy number is n - 1 and when it is odd,
the grundy is n + 1.
```

下面是上述方法的实现:

## C++

```
// CPP program for the variation
// in nim game
#include <bits/stdc++.h>
using namespace std;

// Function to return final
// grundy Number(G) of game
int solve(int p[], int n)
{
    int G = 0;
    for (int i = 0; i < n; i++) {

        // if pile size is odd
        if (p[i] & 1)

            // We XOR pile size+1
            G ^= (p[i] + 1);

        else // if pile size is even

            // We XOR pile size-1
            G ^= (p[i] - 1);
    }
    return G;
}

// driver program
int main()
{
    // Game with 3 piles
    int n = 3;

    // pile with different sizes
    int p[3] = { 32, 49, 58 };

    // Function to return result of game
    int res = solve(p, n);

    if (res == 0) // if G is zero
        cout << "Player 2 wins";
    else // if G is non zero
        cout << "Player 1 wins";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the variation
// in nim game
class GFG {

    // Function to return final
    // grundy Number(G) of game
    static int solve(int p[], int n)
    {

        int G = 0;
        for (int i = 0; i < n; i++) {

            // if pile size is odd
            if (p[i]%2!=0)

                // We XOR pile size+1
                G ^= (p[i] + 1);

            else // if pile size is even

                // We XOR pile size-1
                G ^= (p[i] - 1);
        }

        return G;
    }

    //Driver code
    public static void main (String[] args)
    {

        // Game with 3 piles
        int n = 3;

        // pile with different sizes
        int p[] = { 32, 49, 58 };

        // Function to return result of game
        int res = solve(p, n);

        if (res == 0) // if G is zero
            System.out.print("Player 2 wins");
        else // if G is non zero
            System.out.print("Player 1 wins");
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program for the
# variation in nim game

# Function to return final
# grundy Number(G) of game
def solve(p, n):
    G = 0
    for i in range(n):

        # if pile size is odd
        if (p[i] % 2 != 0):

            # We XOR pile size+1
            G ^= (p[i] + 1)

        # if pile size is even
        else:

            # We XOR pile size-1
            G ^= (p[i] - 1)

    return G

# Driver code

# Game with 3 piles
n = 3

# pile with different sizes
p = [32, 49, 58]

# Function to return result of game
res = solve(p, n)

if (res == 0): # if G is zero
    print("Player 2 wins")

else: # if G is non zero
    print("Player 1 wins")

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# program for the variation
// in nim game
using System;
class GFG {

    // Function to return final
    // grundy Number(G) of game
    static int solve(int[] p, int n)
    {

        int G = 0;
        for (int i = 0; i < n; i++) {

            // if pile size is odd
            if (p[i] % 2 != 0)

                // We XOR pile size+1
                G ^= (p[i] + 1);

            else // if pile size is even

                // We XOR pile size-1
                G ^= (p[i] - 1);
        }

        return G;
    }

    // Driver code
    public static void Main()
    {

        // Game with 3 piles
        int n = 3;

        // pile with different sizes
        int[] p = { 32, 49, 58 };

        // Function to return result of game
        int res = solve(p, n);

        if (res == 0) // if G is zero
            Console.WriteLine("Player 2 wins");

        else // if G is non zero
            Console.WriteLine("Player 1 wins");
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// php program for the variation
// in nim game

// Function to return final
// grundy Number(G) of game
function solve($p,$n)
{
    $G = 0;
    for ($i = 0; $i < $n; $i++)
    {

        // if pile size is odd
        if ($p[$i] & 1)

            // We XOR pile size+1
            $G ^= ($p[$i] + 1);

        else // if pile size is even

            // We XOR pile size-1
            $G ^= ($p[$i] - 1);
    }
    return $G;
}

    // Driver Code
    // Game with 3 piles
    $n = 3;

    // pile with different sizes
    $p= array( 32, 49, 58 );

    // Function to return result of game
    $res = solve($p, $n);

    if ($res == 0) // if G is zero
        echo "Player 2 wins";
    else // if G is non zero
        echo "Player 1 wins";

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program for the variation
// in nim game

// Function to return final
// grundy Number(G) of game
function solve(p, n)
{
    let G = 0;
    for(let i = 0; i < n; i++)
    {

        // If pile size is odd
        if (p[i] % 2 != 0)

            // We XOR pile size+1
            G ^= (p[i] + 1);

        // If pile size is even
        else

            // We XOR pile size-1
            G ^= (p[i] - 1);
    }
    return G;
}

// Driver code

// Game with 3 piles
let n = 3;

// Pile with different sizes
let p = [ 32, 49, 58 ];

// Function to return result of game
let res = solve(p, n);

// If G is zero
if (res == 0)
    document.write("Player 2 wins");

// If G is non zero
else
    document.write("Player 1 wins");

// This code is contributed by sanjoy_62

</script>
```

**输出:**

```
Player 1 wins
```

**时间复杂度:** O(n)