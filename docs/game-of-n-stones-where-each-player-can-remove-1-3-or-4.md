# N 块石头的游戏，每个玩家可以移除 1、3 或 4 块

> 原文:[https://www . geesforgeks . org/n-stones 游戏-每个玩家可以移除-1-3-或-4/](https://www.geeksforgeeks.org/game-of-n-stones-where-each-player-can-remove-1-3-or-4/)

两个玩家在玩一个有 n 块石头的游戏，其中玩家 1 总是先玩。两位选手轮流移动，发挥最佳。在一次移动中，玩家可以从石头堆中移除 1、3 或 4 块石头。如果一个玩家不能移动，那么这个玩家就输了。给定 n 小于等于 200 的石头数量，找到并打印获胜者的名字。
示例:

```
Input : 4
Output : player 1

Input : 7
Output : player 2
```

为了解决这个问题，我们需要找到 n 的每个可能值作为一个输赢位置。由于上述游戏是[不偏不倚组合游戏](https://www.geeksforgeeks.org/introduction-to-combinatorial-game-theory/)之一，因此输赢位置的刻画是有效的。
**输赢状态的特征属性为:**

*   所有终端位置都在失去位置。
*   从每个赢的位置，至少有一个移动到一个输的位置。
*   从每一个失败的位置，每一个动作都是走向一个胜利的位置。

如果一个玩家能够移动，使得下一步是输的状态，而不是处于赢的状态。找到玩家 1 的状态，如果玩家 1 处于获胜状态，则玩家 1 赢得游戏，否则玩家 2 将获胜。
**考虑以下基本位置:**

1.  **位置 0** 是输的状态，如果石头数比 0，玩家 1 将无法移动，因此玩家 1 输了。
2.  **位置 1** 为获胜状态，如果石头数量比玩家 1 多 1，玩家 1 将移除石头并赢得游戏。
3.  **位置 2** 是输的状态，如果石头数量比玩家 1 多 2 块，玩家 1 将移除 1 块石头，然后玩家 2 移除第二块石头，赢得游戏。
4.  **位置 3** 是赢的状态，如果玩家能够采取一个移动，使得下一个移动是输的状态，而不是玩家处于赢的状态，玩家 1 将移除所有 3 块石头
5.  **位置 4** 是赢的状态，如果玩家能够采取一个移动，使得下一个移动是输的状态，而不是玩家处于赢的状态，玩家 1 将移除所有 4 块石头
6.  **位置 5** 是赢的状态，如果玩家能够采取一个移动，使得下一个移动是输的状态，而不是玩家处于赢的状态，玩家 1 将移除 3 个石头，留下 2 个石头，这是输的状态
7.  **位置 6** 是赢的状态，如果玩家能够采取一个移动，使得下一个移动是输的状态，而不是玩家处于赢的状态，玩家 1 将移除 4 个石头，留下 2 个石头，这是输的状态
8.  **位置 7** 为输球状态，如果石头数比玩家 1 多 7 块，可以移除 1、3 或 4 块石头，这都导致输球状态，因此玩家 1 会输球。

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// CPP program to find winner of
// the game of N stones
#include <bits/stdc++.h>
using namespace std;

const int MAX = 200;

// finds the winning and losing
// states for the 200 stones.
void findStates(int position[])
{
    // 0 means losing state
    // 1 means winning state
    position[0] = 0;
    position[1] = 1;
    position[2] = 0;
    position[3] = 1;
    position[4] = 1;
    position[5] = 1;
    position[6] = 1;
    position[7] = 0;

    // find states for other positions
    for (int i = 8; i <= MAX; i++) {
        if (!position[i - 1] || !position[i - 3]
            || !position[i - 4])
            position[i] = 1;
        else
            position[i] = 0;
    }
}

// driver function
int main()
{
    int N = 100;
    int position[MAX] = { 0 };

    findStates(position);

    if (position[N] == 1)
        cout << "Player 1";
    else
        cout << "Player 2";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the variation
// in nim game
class GFG {

    static final int MAX = 200;

    // finds the winning and losing
    // states for the 200 stones.
    static void findStates(int position[])
    {

        // 0 means losing state
        // 1 means winning state
        position[0] = 0;
        position[1] = 1;
        position[2] = 0;
        position[3] = 1;
        position[4] = 1;
        position[5] = 1;
        position[6] = 1;
        position[7] = 0;

        // find states for other positions
        for (int i = 8; i < MAX; i++) {

            if (position[i - 1]!=1 ||
                    position[i - 3]!=1
                  || position[i - 4]!=1)
                position[i] = 1;
            else
                position[i] = 0;
        }
    }

    //Driver code
    public static void main (String[] args)
    {

        int N = 100;
        int position[]=new int[MAX];

        findStates(position);

        if (position[N] == 1)
            System.out.print("Player 1");
        else
            System.out.print("Player 2");
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to find winner of
# the game of N stones

MAX = 200

# finds the winning and losing
# states for the 200 stones.
def findStates(position):

    # 0 means losing state
    # 1 means winning state
    position[0] = 0;
    position[1] = 1;
    position[2] = 0;
    position[3] = 1;
    position[4] = 1;
    position[5] = 1;
    position[6] = 1;
    position[7] = 0

    # find states for other positions
    for i in range(8,MAX+1):
        if not(position[i - 1]) or not(position[i - 3]) or not(position[i - 4]):
            position[i] = 1;
        else:
            position[i] = 0;

#driver function
N = 100
position = [0] * (MAX+1)

findStates(position)

if (position[N] == 1):
        print("Player 1")
else:
        print("Player 2")

# This code is contributed by
# Smitha Dinesh Semwal
```

## C#

```
// C# program for the variation
// in nim game
using System;

class GFG {

    static int MAX = 200;

    // finds the winning and losing
    // states for the 200 stones.
    static void findStates(int []position)
    {

        // 0 means losing state
        // 1 means winning state
        position[0] = 0;
        position[1] = 1;
        position[2] = 0;
        position[3] = 1;
        position[4] = 1;
        position[5] = 1;
        position[6] = 1;
        position[7] = 0;

        // find states for other positions
        for (int i = 8; i < MAX; i++)
        {
            if (position[i - 1] != 1
                  || position[i - 3] != 1
                   || position[i - 4]!=1)
                position[i] = 1;
            else
                position[i] = 0;
        }
    }

    // Driver code
    public static void Main ()
    {
        int N = 100;
        int []position = new int[MAX];

        findStates(position);

        if (position[N] == 1)
            Console.WriteLine("Player 1");
        else
            Console.WriteLine("Player 2");
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP  program to find winner of
// the game of N stones
$MAX = 200;

// finds the winning and losing
// states for the 200 stones.
function  findStates($position)
{
    global $MAX;
    // 0 means losing state
    // 1 means winning state
    $position[0] = 0;
    $position[1] = 1;
    $position[2] = 0;
    $position[3] = 1;
    $position[4] = 1;
    $position[5] = 1;
    $position[6] = 1;
    $position[7] = 0;

    // find states for other positions
    for ($i = 8; $i <= $MAX; $i++) {
        if (!$position[$i - 1] || !$position[$i - 3]
            || !$position[$i - 4])
            $position[$i] = 1;
        else
            $position[$i] = 0;
    }
}

// driver function

    $N = 100;
    $position[$MAX] = array(0);

    findStates($position);

    if ($position == 1)
         echo  "Player 1";
    else
        echo  "Player 2";

#This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Javascript program for the variation
// in nim game

     let MAX = 200;

    // finds the winning and losing
    // states for the 200 stones.
    function findStates(position)
    {

        // 0 means losing state
        // 1 means winning state
        position[0] = 0;
        position[1] = 1;
        position[2] = 0;
        position[3] = 1;
        position[4] = 1;
        position[5] = 1;
        position[6] = 1;
        position[7] = 0;

        // find states for other positions
        for (let i = 8; i < MAX; i++)
        {
            if (position[i - 1] != 1
                  || position[i - 3] != 1
                   || position[i - 4]!=1)
                position[i] = 1;
            else
                position[i] = 0;
        }
    }

// Driver code

        let N = 100;
        let position = [];

        findStates(position);

        if (position[N] == 1)
            document.write("Player 1");
        else
            document.write("Player 2");

  // This code is contributed by code_hunt.
</script>
```

**输出:**

```
Player 2
```

本文由 [**ARSHPREET_SINGH**](https://www.hackerrank.com/arshpreets713) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。