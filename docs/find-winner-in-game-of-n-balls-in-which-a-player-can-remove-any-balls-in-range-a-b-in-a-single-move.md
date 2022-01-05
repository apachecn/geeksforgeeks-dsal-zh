# 在 N 球游戏中寻找赢家，玩家可以在单次移动

中移除范围【A，B】内的任何球

> 原文:[https://www . geesforgeks . org/find-n 球游戏中的赢家-玩家可以在单次移动中移除 a-b 范围内的任何球/](https://www.geeksforgeeks.org/find-winner-in-game-of-n-balls-in-which-a-player-can-remove-any-balls-in-range-a-b-in-a-single-move/)

给定两个整数 **A** 和 **B** ，并且还给定爱丽丝和鲍勃正在玩一个从包含 **N** 个球的袋子开始的游戏，其中，在单次移动中，玩家可以移除范围**【A，B】**之间的任意数量的球，并且如果玩家不能移除任何球，则玩家输了，任务是如果爱丽丝和鲍勃交替并且最优地玩游戏并且爱丽丝开始游戏，则找到游戏的赢家。

**示例:**

> **输入:** N = 2，A = 1，B = 1
> **输出:**鲍勃
> **解释:**
> 可以玩游戏的一种方式是:
> 
> 1.  爱丽丝移除 1 个球，所以剩下的球是 1 个。
> 2.  现在，鲍勃拿走了最后一个球。
> 3.  爱丽丝不能取出任何球，所以她输了。
> 
> **输入:** N = 3，A = 1，B = 2
> T3】输出:鲍勃

**天真法:**最简单的方法就是利用[斯普拉格-格鲁迪定理](https://www.geeksforgeeks.org/combinatorial-game-theory-set-4-sprague-grundy-theorem/?ref=rp)找到每个州的[格鲁迪数](https://www.geeksforgeeks.org/combinatorial-game-theory-set-3-grundy-numbersnimbers-and-mex/)并找到输赢州。

***时间复杂度:** O(N*N！)*
***辅助空间:** O(N)*

**高效方法:**上述方法可以基于以下观察进行优化:

> 1.  First of all, we can observe that **(a+b)** is always in a losing state, because no matter how many balls **x** ( **a ≤ x≤ b)** are currently selected by the player, the opponent can always empty the bag, because there will be **(a+b–x) [T7**
> 2.  Similarly, from the previous observation, it can be observed that for any multiple of **(a+b)** , such as **m * (a+b)** , the opponent can always lower the current player to the state of **(m–1) * (a+b)** , from
> ***   Therefore, extending the above observation, it can be said that for any multiple of **(a+b)** , the opponent can always reduce the current player to a state just like **(a+b)** , which is indeed a losing state. Therefore, all multiples of **(a+b)** are in a loss state.*   Therefore, the best choice for any player is to reduce the opponent to a multiple of **(a+b),** because after that, no matter what the opponent moves, the player can always win.*   Therefore, the state of losing now is a state in which one can never lower the opponent to a multiple of **(a+b)** .*   Therefore, any player whose status is **((a+b) * m+y)** , in which **(0 ≤ y ≤ a-1)** can never force the opponent to reduce to a multiple of **(a+b),** can only be selected at least **as any player.****

**按照以下步骤解决问题:**

*   **如果 **N%(A+B)** 小于 **A，**则打印“**鲍勃**”。**
*   **否则，打印“ **Alice** ”。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the winner of the
// game
string NimGame(int N, int A, int B)
{
    // Stores sum of A and B
    int sum = A + B;

    // If N is of the form
    // m*(A+B)+y
    if (N % sum <= A - 1)
        return "Bob";
    // Otherwise,
    else
        return "Alice";
}

// Driver code
int main()
{
    // Input
    int N = 3, A = 1, B = 2;
    // Function call
    cout << NimGame(N, A, B) << endl;

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java Program for the above approach
import java.io.*;

class GFG
{

  // Function to find the winner of the
  // game
  public static String NimGame(int N, int A, int B)
  {

    // Stores sum of A and B
    int sum = A + B;

    // If N is of the form
    // m*(A+B)+y
    if (N % sum <= A - 1)
      return "Bob";

    // Otherwise,
    else
      return "Alice";
  }

  public static void main (String[] args)
  {

    // Input
    int N = 3, A = 1, B = 2;

    // Function call
    System.out.println(NimGame(N, A, B));

  }
}

  // This code is contributed by Potta Lokesh
```

## **蟒蛇 3**

```
# Python3 program of the above approach

# Function to find the winner of the game
def NimGame(N, A, B):

    # Stores sum of A and B
    sum = A + B

    # If N is of the form
    # m*(A+B)+y
    if (N % sum <= A - 1):
        return "Bob"

    # Otherwise,
    else:
        return "Alice"

# Driver code

# Input
N = 3
A = 1
B = 2

# Function call
print(NimGame(N, A, B))

# This code is contributed by amreshkumar3
```

## **C#**

```
// C# program of the above approach
using System;

class GFG{

// Function to find the winner of the
// game
public static String NimGame(int N, int A, int B)
{

    // Stores sum of A and B
    int sum = A + B;

    // If N is of the form
    // m*(A+B)+y
    if (N % sum <= A - 1)
        return "Bob";

    // Otherwise,
    else
        return "Alice";
}

// Driver code
static void Main()
{

    // Input
    int N = 3, A = 1, B = 2;

    // Function call
    Console.Write(NimGame(N, A, B));
}
}

// This code is contributed by SoumikMondal
```

## **java 描述语言**

```
<script>
        // JavaScript program for the above approach

        // Function to find the winner of the
        // game
        function NimGame(N, A, B) {
            // Stores sum of A and B
            let sum = A + B;

            // If N is of the form
            // m*(A+B)+y
            if (N % sum <= A - 1)
                return "Bob";
            // Otherwise,
            else
                return "Alice";
        }

        // Driver code

        // Input
        let N = 3, A = 1, B = 2;
        // Function call
        document.write(NimGame(N, A, B) + "<br>");

  // This code is contributed by Potta Lokesh
    </script>
```

****Output**

```
Bob
```** 

*****时间复杂度:*** O(1)
***辅助空间:*** O(1)**