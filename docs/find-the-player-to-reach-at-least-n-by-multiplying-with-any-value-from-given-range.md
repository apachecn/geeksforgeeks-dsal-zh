# 通过与给定范围内的任意值相乘找到至少达到 N 的玩家

> 原文:[https://www . geesforgeks . org/find-the-player-to-reach-at-n-by-乘以给定范围内的任何值/](https://www.geeksforgeeks.org/find-the-player-to-reach-at-least-n-by-multiplying-with-any-value-from-given-range/)

给定一个整数 **N** ，两个玩家 A 和 B 的任务是通过将 **X** 与**【2，9】**范围内的任意数字交替相乘，使 **X** ( *用 **1*** 初始化)的值至少为 **N** 。假设两个玩家都玩得很好。任务是先找到玩家获得一个值 **≥ N** 。

**示例:**

> **输入:** N = 12
> **输出:**玩家 B
> **说明:**
> 最初，X = 1。
> A 将 X 乘以 9。因此，X = 1 * 9 = 9。
> 第二回合，B 将 X 乘以 2。故 X = 9*2 = 18
> 故 B 胜。
> 
> **输入:**N = 10
> T3】输出:玩家 B

**进场:**思路是用[组合博弈论的概念](https://www.geeksforgeeks.org/introduction-to-combinatorial-game-theory/)。如果一个数字乘以 **X** 得出胜利的位置，找出导致失败的位置。以下是步骤:

*   在组合博弈理论中，我们定义一个 **N 位置**是一个位置，下一个要移动的玩家如果打得最优就赢，而 **P 位置**是一个位置，如果对手打得最优，下一个要移动的玩家总是输。
*   可以到达 **N** 的最低位置是，比方说 **res** = **ceil(N/9)** 。因此，从**开始的所有位置【res，res + 1，res + 2，…..，N–1]**为 **N** 位置。
*   唯一被迫移动到**【RES，res + 1，…，(N–1)】**的位置是当乘以 **2** 时的位置，它们位于由 **Y** = **ceil(res/2)** 给出的区间内，
*   因此，**【Y，Y + 1，…，(RES–1)】**都是 **P 位**。
*   重复上述步骤直到找到包含 **1** 的区间后，如果 1 是 **N 位**，则 **A 赢**，否则 **B 赢**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the winner
char Winner(int N)
{
    bool player = true;

    // Backtrack from N to 1
    while(N > 1)
    {
        int den = (player) ? 9 : 2;
        int X = N/den, Y = N%den;
        N = (Y)? X + 1: X;
        player = !player;
    }
    if (player)
      return 'B';
    else
      return 'A';
}

// Driver Code
int main()
{
  int N = 10;
  cout << Winner(N);
  return 0;
}

// This code is contributed by mohit kumar 29.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

  // Function to find the winner
  static char Winner(int N)
  {
    boolean player = true;

    // Backtrack from N to 1
    while(N > 1)
    {
      int den = (player) ? 9 : 2;
      int X = N / den;
      int Y = N % den;
      N = (Y > 0) ? X + 1: X;
      player = !player;
    }
    if (player)
      return 'B';
    else
      return 'A';
  }

  // Driver Code
  public static void main(String[] args)
  {
    int N = 10;
    System.out.print(Winner(N));
  }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the winner
def Winner(N):
    player = True

    # Backtrack from N to 1
    while N > 1:

        X, Y = divmod(N, (9 if player else 2))

        N = X + 1 if Y else X
        player = not player

    if player:
      return 'B'
    else:
      return 'A'

# Driver Code
N = 10
print(Winner(N))
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

  // Function to find the winner
  static char Winner(int N)
  {
      bool player = true;

      // Backtrack from N to 1
      while (N > 1)
      {
          int den = (player) ? 9 : 2;
          int X = N / den;
          int Y = N % den;
          N = (Y > 0) ? X + 1 : X;
          player = !player;
      }
      if (player)
          return 'B';
      else
          return 'A';
  }

  // Driver Code
  static public void Main()
  {
    int N = 10;
    Console.WriteLine(Winner(N));
  }
}

// This code is contributed by Dharanendra L V
```

## java 描述语言

```
<script>
// Javascript program for the above approach
function Winner(N)
{
    var player = Boolean(true);

    // Backtrack from N to 1
    while(N > 1)
    {
        var den = (player) ? 9 : 2;
        var X = parseInt(N/den), Y = parseInt(N%den);
        N = (Y)? X + 1: X;
        player = !player;
    }
    if (player)
      document.write( 'B');
    else
      document.write( 'A');
}
var N = 10;
Winner(N);

// This code is contributed by SoumikMondal
</script>
```

**Output:** 

```
B
```

***时间复杂度:** O(log N)*
***辅助空间:** O(1)*