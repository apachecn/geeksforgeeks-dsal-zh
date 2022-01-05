# 预测硬币游戏的赢家

> 原文:[https://www . geesforgeks . org/预测硬币游戏赢家/](https://www.geeksforgeeks.org/predict-the-winner-in-coin-game/)

有两个玩家 **P1** 和 **P2** 以及两堆分别由 **M** 和 **N** 硬币组成的硬币。在每个回合中，玩家只能从这些堆中选择一堆，并丢弃另一堆。这个丢弃的堆不能在游戏中进一步使用。堆玩家选择的进一步分为两堆非零部分。不能分堆即堆中硬币数为< 2 的玩家，输掉游戏。任务是确定如果 **P1** 开始游戏并且两个玩家都以最佳状态玩游戏，哪个玩家获胜。
**举例:**

> **输入:** M = 4，N = 4
> **输出:**玩家 1
> 玩家 1 可以选择任意一堆，因为两者包含相同数量的硬币
> 然后将选择的一堆(未选择的一堆被丢弃)分成两堆，每堆 1 枚硬币。
> 现在，玩家 2 没有移动(因为剩余的两堆都包含一枚硬币
> ，不能分成两组非零硬币)。
> **输入:** M = 1，N = 1
> **输出:**玩家 2
> 无招可使。

**方法:**只需检查任意一堆硬币是否由偶数硬币组成。如果是，则玩家 1 获胜，否则玩家 2 获胜。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the winner of the game
void findWinner(int M, int N)
{
    if (M % 2 == 0 || N % 2 == 0)
        cout << "Player 1";
    else
        cout << "Player 2";
}

// Driver code
int main()
{
    int M = 1, N = 2;
    findWinner(M, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG {

    // Function to print the winner of the game
    static void findWinner(int M, int N)
    {
        if (M % 2 == 0 || N % 2 == 0)
            System.out.println("Player 1");
        else
            System.out.println("Player 2");
    }

    // Driver code
    public static void main(String[] args)
    {
        int M = 1, N = 2;
        findWinner(M, N);
    }
}

// This code is contributed by ajit.
```

## 蟒蛇 3

```
# Python implementation of the approach
# Function to print the winner of the game

def findWinner(M, N):
    if (M % 2 == 0 or N % 2 == 0):
        print("Player 1");
    else:
        print("Player 2");

# Driver code
M = 1;
N = 2;
findWinner(M, N);

# This code contributed by PrinciRaj1992
```

## C#

```
// C# implementation of the approach
using System;

class GFG {

    // Function to print the winner of the game
    static void findWinner(int M, int N)
    {
        if (M % 2 == 0 || N % 2 == 0)
            Console.WriteLine("Player 1");
        else
            Console.WriteLine("Player 2");
    }

    // Driver code
    static public void Main()
    {
        int M = 1, N = 2;
        findWinner(M, N);
    }
}

// This code is contributed by Tushil..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
//PHP implementation of the approach
// Function to print the winner of the game

function findWinner($M, $N)
{
    if ($M % 2 == 0 || $N % 2 == 0)
        echo "Player 1";
    else
        echo "Player 2";
}

    // Driver code
    $M = 1;
    $N = 2;
    findWinner($M, $N);

// This code is contributed by Tushil.
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to print the winner of the game
function findWinner(M, N)
{
    if (M % 2 == 0 || N % 2 == 0)
        document.write(("Player 1"));
    else
        document.write(("Player 2"));
}

// Driver code
var M = 1, N = 2;
findWinner(M, N);

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
Player 1
```