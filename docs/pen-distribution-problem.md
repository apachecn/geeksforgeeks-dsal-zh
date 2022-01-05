# 笔分配问题

> 原文:[https://www.geeksforgeeks.org/pen-distribution-problem/](https://www.geeksforgeeks.org/pen-distribution-problem/)

给定一个整数 **N** 表示一支笔的盒数，两个玩家 **P1** 和 **P2** 按照以下规则在他们之间玩分发 **N** 支笔的游戏:

*   **P1** 拿着**2<sup>X</sup>T5】笔先动。(最初， **X** = 0)**
*   **P2** 带**3<sup>X</sup>T5】笔。**
*   每次移动后 **X** 的值增加 1。
*   **P1** 和 **P2** 交替移动。
*   如果当前玩家不得不拿走比盒子里剩余笔数更多的笔，那么他们就退出。
*   当两个玩家都退出或者盒子变空时，游戏就结束了。

游戏结束后打印以下详细信息的任务:

1.  盒子里剩余的钢笔数量。
2.  **P1** 收集的笔数。
3.  **P2** 收集的笔数。

**例:**

> ***输入:** N = 22*
> ***输出:***
> *箱内剩余笔数:14*
> *P1 收藏笔数:5*
> *P2 收藏笔数:3*
> *T20】说明:*
> 
> *   移动 1: X = 0，P1 从盒子里拿出一支笔。因此，N = 22–1 = 21。
> *   移动 2: X = 1，P2 从盒子里拿出 3 支笔。因此，N = 21–3 = 18。
> *   移动 3: X = 2，P1 从盒子里拿出 4 支笔。因此，N = 18–4 = 14。
> *   第 4 步:X = 3，P2 以 27 > 14 退出。
> *   移动 5: X = 4，P1 以 16 > 14 退出。
> *   游戏结束！两位选手都退出了。
> 
> ***输入:** N = 1*
> ***输出:***
> *箱内剩余笔数:0*
> *P1 采集笔数:1*
> *P2 采集笔数:0*

**逼近**:思路是用[递归](https://www.geeksforgeeks.org/recursion/)。按照步骤解决问题:

1.定义递归函数:

> Game_Move(N、P1、P2、X、Move、QuitP1、QuitP2)
> 其中，
> **N :** 笔数合计
> **P1**:P1
> **P2**评分:P2
> **X** 评分:初始化为零
> **Move** = 0 : P1 的回合
> **Move** = 1 : P2 的回合
> t29

2.最后，在游戏结束后打印最终值

以下是上述方法的实现:

## C++

```
// C++ implementation of the
// above approach

#include <bits/stdc++.h>
using namespace std;

// N = Total number of Pens
// P1 : Score of P1
// P2 : Score of P2
// X : Initialized to zero
// Move = 0 : P1's turn
// Move = 1 : P2's turn
// QuitP1 : Has P1 quit
// QuitP2 : Has P2 quit

// Recursive function to play Game
void solve(int& N, int& P1, int& P2, int& X, bool Move,
           bool QuitP1, bool QuitP2)
{
    if (N == 0 or (QuitP1 and QuitP2)) {

        // Box is empty, Game Over! or
        // Both have quit, Game Over!
        cout << "Number of pens remaining"
             << " in the box: " << N << endl;
        cout << "Number of pens collected"
             << " by P1: " << P1 << endl;
        cout << "Number of pens collected"
             << " by P2: " << P2 << endl;
        return;
    }

    if (Move == 0 and QuitP1 == false) {

        // P1 moves
        int req_P1 = pow(2, X);

        if (req_P1 <= N) {
            P1 += req_P1;
            N -= req_P1;
        }
        else {
            QuitP1 = true;
        }
    }

    else if (Move == 1 and QuitP2 == false) {

        // P2 moves
        int req_P2 = pow(3, X);

        if (req_P2 <= N) {
            P2 += req_P2;
            N -= req_P2;
        }
        else {
            QuitP2 = true;
        }
    }

    // Increment X
    X++;

    // Switch moves between P1 and P2
    Move = ((Move == 1) ? 0 : 1);

    solve(N, P1, P2, X, Move, QuitP1, QuitP2);
}

// Function to find the number of
// pens remaining in the box and
// calculate score for each player
void PenGame(int N)
{
    // Score of P1
    int P1 = 0;

    // Score of P2
    int P2 = 0;

    // Initialized to zero
    int X = 0;

    // Move = 0, P1's turn
    // Move = 1, P2's turn
    bool Move = 0;

    // Has P1 quit
    bool QuitP1 = 0;

    // Has P2 quit
    bool QuitP2 = 0;

    // Recursively continue the game
    solve(N, P1, P2, X, Move,
          QuitP1, QuitP2);
}

// Driver Code
int main()
{
    int N = 22;
    PenGame(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the
// above approach
import java.util.*;
import java.lang.*;
public class GFG
{

  // N = Total number of Pens
  // P1 : Score of P1
  // P2 : Score of P2
  // X : Initialized to zero
  // Move = 0 : P1's turn
  // Move = 1 : P2's turn
  // QuitP1 : Has P1 quit
  // QuitP2 : Has P2 quit

  // Recursive function to play Game
  static void solve(int N, int P1, int P2, int X,
                    int Move, boolean QuitP1, boolean QuitP2)
  {
    if (N == 0 || (QuitP1 && QuitP2))
    {

      // Box is empty, Game Over! or
      // Both have quit, Game Over!
      System.out.println("Number of pens remaining"
                         + " in the box: " + N);
      System.out.println("Number of pens collected"
                         + " by P1: " + P1);
      System.out.println("Number of pens collected"
                         + " by P2: " + P2);
      return;
    }
    if (Move == 0 && QuitP1 == false)
    {

      // P1 moves
      int req_P1 = (int)(Math.pow(2, X));
      if (req_P1 <= N)
      {
        P1 += req_P1;
        N -= req_P1;
      }
      else
      {
        QuitP1 = true;
      }
    }
    else if (Move == 1 && QuitP2 == false)
    {

      // P2 moves
      int req_P2 = (int)(Math.pow(3, X));
      if (req_P2 <= N)
      {
        P2 += req_P2;
        N -= req_P2;
      }
      else
      {
        QuitP2 = true;
      }
    }

    // Increment X
    X++;

    // Switch moves between P1 and P2
    Move = ((Move == 1) ? 0 : 1);
    solve(N, P1, P2, X, Move, QuitP1, QuitP2);
  }

  // Function to find the number of
  // pens remaining in the box and
  // calculate score for each player
  static void PenGame(int N)
  {

    // Score of P1
    int P1 = 0;

    // Score of P2
    int P2 = 0;

    // Initialized to zero
    int X = 0;

    // Move = 0, P1's turn
    // Move = 1, P2's turn
    int Move = 0;

    // Has P1 quit
    boolean QuitP1 = false;

    // Has P2 quit
    boolean QuitP2 = false;

    // Recursively continue the game
    solve(N, P1, P2, X, Move, QuitP1, QuitP2);
  }

  // Driver Code
  public static void main (String[] args)
  {
    int N = 22;
    PenGame(N);
  }
}

// This code is contributed by jana_sayantan.
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach

# N = Total number of Pens
# P1 : Score of P1
# P2 : Score of P2
# X : Initialized to zero
# Move = 0 : P1's turn
# Move = 1 : P2's turn
# QuitP1 : Has P1 quit
# QuitP2 : Has P2 quit

# Recursive function to play Game
def solve(N, P1, P2, X, Move,
          QuitP1, QuitP2):

    if (N == 0 or (QuitP1 and QuitP2)):

        # Box is empty, Game Over! or
        # Both have quit, Game Over!
        print("Number of pens remaining in the box: ", N)
        print("Number of pens collected by P1: ", P1)
        print("Number of pens collected by P2: ", P2)
        return
    if (Move == 0 and QuitP1 == False):

        # P1 moves
        req_P1 = int(pow(2, X))

        if (req_P1 <= N):
            P1 += req_P1
            N -= req_P1
        else:
            QuitP1 = True
    elif (Move == 1 and QuitP2 == False):

        # P2 moves
        req_P2 = int(pow(3, X))
        if (req_P2 <= N):
            P2 += req_P2
            N -= req_P2
        else:
            QuitP2 = True

    # Increment X
    X += 1

    # Switch moves between P1 and P2
    if(Move == 1):
        Move = 0
    else:
        Move = 1
    solve(N, P1, P2, X, Move, QuitP1, QuitP2)

# Function to find the number of
# pens remaining in the box and
# calculate score for each player
def PenGame(N):

    # Score of P1
    P1 = 0

    # Score of P2
    P2 = 0

    # Initialized to zero
    X = 0

    # Move = 0, P1's turn
    # Move = 1, P2's turn
    Move = False

    # Has P1 quit
    QuitP1 = False

    # Has P2 quit
    QuitP2 = False

    # Recursively continue the game
    solve(N, P1, P2, X, Move,
          QuitP1, QuitP2)

# Driver Code
N = 22
PenGame(N)

# This code is contributed by Dharanendra L V.
```

## C#

```
// C# implementation of the
// above approach
using System;
class GFG {

    // N = Total number of Pens
    // P1 : Score of P1
    // P2 : Score of P2
    // X : Initialized to zero
    // Move = 0 : P1's turn
    // Move = 1 : P2's turn
    // QuitP1 : Has P1 quit
    // QuitP2 : Has P2 quit

    // Recursive function to play Game
    static void solve(int N, int P1, int P2, int X,
                      int Move, bool QuitP1, bool QuitP2)
    {
        if (N == 0 || (QuitP1 && QuitP2)) {

            // Box is empty, Game Over! or
            // Both have quit, Game Over!
            Console.WriteLine("Number of pens remaining"
                              + " in the box: " + N);
            Console.WriteLine("Number of pens collected"
                              + " by P1: " + P1);
            Console.WriteLine("Number of pens collected"
                              + " by P2: " + P2);
            return;
        }

        if (Move == 0 && QuitP1 == false) {

            // P1 moves
            int req_P1 = (int)(Math.Pow(2, X));

            if (req_P1 <= N) {
                P1 += req_P1;
                N -= req_P1;
            }
            else {
                QuitP1 = true;
            }
        }

        else if (Move == 1 && QuitP2 == false)
        {

            // P2 moves
            int req_P2 = (int)(Math.Pow(3, X));

            if (req_P2 <= N)
            {
                P2 += req_P2;
                N -= req_P2;
            }
            else
            {
                QuitP2 = true;
            }
        }

        // Increment X
        X++;

        // Switch moves between P1 and P2
        Move = ((Move == 1) ? 0 : 1);
        solve(N, P1, P2, X, Move, QuitP1, QuitP2);
    }

    // Function to find the number of
    // pens remaining in the box and
    // calculate score for each player
    static void PenGame(int N)
    {
        // Score of P1
        int P1 = 0;

        // Score of P2
        int P2 = 0;

        // Initialized to zero
        int X = 0;

        // Move = 0, P1's turn
        // Move = 1, P2's turn
        int Move = 0;

        // Has P1 quit
        bool QuitP1 = false;

        // Has P2 quit
        bool QuitP2 = false;

        // Recursively continue the game
        solve(N, P1, P2, X, Move, QuitP1, QuitP2);
    }

    // Driver Code
    public static void Main()
    {
        int N = 22;
        PenGame(N);
    }
}

// This code is contributed by chitranayal.
```

## java 描述语言

```
<script>
// javascript program of the above approach

  // N = Total number of Pens
  // P1 : Score of P1
  // P2 : Score of P2
  // X : Initialized to zero
  // Move = 0 : P1's turn
  // Move = 1 : P2's turn
  // QuitP1 : Has P1 quit
  // QuitP2 : Has P2 quit

  // Recursive function to play Game
  function solve(N, P1, P2, X,
                    Move, QuitP1, QuitP2)
  {
    if (N == 0 || (QuitP1 && QuitP2))
    {

      // Box is empty, Game Over! or
      // Both have quit, Game Over!
      document.write("Number of pens remaining"
                         + " in the box: " + N + "<br/>");
      document.write("Number of pens collected"
                         + " by P1: " + P1+ "<br/>");
      document.write("Number of pens collected"
                         + " by P2: " + P2+ "<br/>");
      return;
    }
    if (Move == 0 && QuitP1 == false)
    {

      // P1 moves
      let req_P1 = (Math.pow(2, X));
      if (req_P1 <= N)
      {
        P1 += req_P1;
        N -= req_P1;
      }
      else
      {
        QuitP1 = true;
      }
    }
    else if (Move == 1 && QuitP2 == false)
    {

      // P2 moves
      let req_P2 = (Math.pow(3, X));
      if (req_P2 <= N)
      {
        P2 += req_P2;
        N -= req_P2;
      }
      else
      {
        QuitP2 = true;
      }
    }

    // Increment X
    X++;

    // Switch moves between P1 and P2
    Move = ((Move == 1) ? 0 : 1);
    solve(N, P1, P2, X, Move, QuitP1, QuitP2);
  }

  // Function to find the number of
  // pens remaining in the box and
  // calculate score for each player
  function PenGame(N)
  {

    // Score of P1
    let P1 = 0;

    // Score of P2
    let P2 = 0;

    // Initialized to zero
    let X = 0;

    // Move = 0, P1's turn
    // Move = 1, P2's turn
    let Move = 0;

    // Has P1 quit
    let QuitP1 = false;

    // Has P2 quit
    let QuitP2 = false;

    // Recursively continue the game
    solve(N, P1, P2, X, Move, QuitP1, QuitP2);
  }

    // Driver Code

    let N = 22;
    PenGame(N);

</script>
```

**Output:** 

```
Number of pens remaining in the box: 14
Number of pens collected by P1: 5
Number of pens collected by P2: 3
```

***时间复杂度:** O(Log(N))*
***辅助空间:** O(1)*