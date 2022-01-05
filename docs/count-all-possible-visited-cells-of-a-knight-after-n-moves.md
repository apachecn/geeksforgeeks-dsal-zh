# 计算骑士 N 次移动后所有可能被访问的细胞

> 原文:[https://www . geeksforgeeks . org/count-所有可能访问的 n 次移动后骑士的细胞/](https://www.geeksforgeeks.org/count-all-possible-visited-cells-of-a-knight-after-n-moves/)

给定骑士的当前位置为(I，j)，计算 N 次移动后骑士可能访问的不同位置的数量(在 10×10 的棋盘中)。

**示例:**

> **输入:** i = 3，j = 3，n = 1
> **输出:** 9
> 骑士最初在位置【3】【3】。一次移动后，它可以再访问 8 个细胞
> 
> **输入:** i = 3，j = 3，n = 2
> T3】输出: 35

**进场:**思路很简单，我们从一个给定的位置出发，尝试所有可能的招式。每次移动后，递归调用 n-1 次移动。我们需要确保我们再也不去牢房了。我们制作一个访问布尔矩阵，作为访问矩阵，这样位置就不会重复。当我们访问一个位置时，在矩阵中将该位置标记为真。

步骤:-

1.  取一个布尔访问矩阵(10X10)并将所有单元格初始化为假(非访问)
2.  用骑士所有可能的动作创建两个向量。我们发现骑士有 8 种可能的移动方式。
3.  有效位置=骑士在棋盘的边界内，并且该单元未被访问。
4.  调用 n = n-1 的下一个有效位置的方法。
5.  如果 n == 0，则返回。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

const int N = 10;

// All possible moves of the knight.

// In X axis.
vector<int> X = { 2, 1, -1, -2, -2, -1, 1, 2 };

// In Y axis.
vector<int> Y = { 1, 2, 2, 1, -1, -2, -2, -1 };

void getCountRec(vector<vector<bool> >& board,
                 int i, int j, int n)
{
    // if n=0, we have our result.
    if (n == 0)
        return;

    for (int k = 0; k < 8; k++) {
        int p = i + X[k];
        int q = j + Y[k];

        // Condition for valid cells.
        if (p >= 0 && q >= 0
            && p < 10 && q < N) {
            board[p][q] = true;
            getCountRec(board, p, q, n - 1);
        }
    }
}

int getCount(int i, int j, int n)
{
    vector<vector<bool> > board(N, vector<bool>(N));
    board[i][j] = true;

    // Call the recursive function to mark
    // visited cells.
    getCountRec(board, i, j, n);

    int cnt = 0;
    for (auto row : board) {
        for (auto cell : row) {
            if (cell)
                cnt++;
        }
    }
    return cnt;
}

// Driver Code
int main()
{
    int i = 3, j = 3, N = 2;
    cout << getCount(i, j, N) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

static int N = 10;

// All possible moves of the knight.

// In X axis.
static int[] X = { 2, 1, -1, -2, -2, -1, 1, 2 };

// In Y axis.
static int[] Y = { 1, 2, 2, 1, -1, -2, -2, -1 };

static void getCountRec(boolean[][] board,
                        int i, int j, int n)
{

    // If n=0, we have our result.
    if (n == 0)
        return;

    for(int k = 0; k < 8; k++)
    {
        int p = i + X[k];
        int q = j + Y[k];

        // Condition for valid cells.
        if (p >= 0 && q >= 0 &&
            p < 10 && q < N)
        {
            board[p][q] = true;
            getCountRec(board, p, q, n - 1);
        }
    }
}

static int getCount(int i, int j, int n)
{
    boolean[][] board = new boolean[N][N];
    board[i][j] = true;

    // Call the recursive function to mark
    // visited cells.
    getCountRec(board, i, j, n);

    int cnt = 0;
    for(boolean[] row : board)
    {
        for(boolean cell : row)
        {
            if (cell != false)
                cnt++;
        }
    }
    return cnt;
}

// Driver code
public static void main(String[] args)
{
    int i = 3, j = 3, N = 2;

    System.out.println(getCount(i, j, N));
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python program for the above approach
SIZE = 10

# All possible moves of the knight.
# In X axis.
X = [2, 1, -1, -2, -2, -1, 1, 2]

# In Y axis.
Y = [1, 2, 2, 1, -1, -2, -2, -1]

def getCountRec(board, i, j, n):

    # If n=0, we have our result.
    if n == 0:
        return

    for k in range(8):
        p = i + X[k]
        q = j + Y[k]

        # Condition for valid cells.
        if p >= 0 and q >= 0 and p < 10 and q < SIZE:
            board[p][q] = True
            getCountRec(board,p,q,n-1)

def getCount(i, j, n):
    board = [[False for i in range(SIZE)] for j in range(SIZE)]
    board[i][j] = True

    # Call the recursive function to mark
    # visited cells.
    getCountRec(board, i, j, n)
    cnt = 0

    for row in board:
        for cell in row:
            if cell != False:
                cnt += 1

    return cnt

# Driver code   
i = 3
j = 3
N = 2
print(getCount(i, j, N))

# This code is contributed by rdtank.
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

  static int N = 10;

  // All possible moves of the knight.

  // In X axis.
  static int [] X = { 2, 1, -1, -2, -2, -1, 1, 2 };

  // In Y axis.
  static int [] Y = { 1, 2, 2, 1, -1, -2, -2, -1 };

  static void getCountRec(bool[,] board,
                          int i, int j, int n)
  {

      // If n=0, we have our result.
      if (n == 0)
          return;

      for(int k = 0; k < 8; k++)
      {
          int p = i + X[k];
          int q = j + Y[k];

          // Condition for valid cells.
          if (p >= 0 && q >= 0 &&
              p < 10 && q < N)
          {
              board[p, q] = true;
              getCountRec(board, p, q, n - 1);
          }
      }
  }

  static int getCount(int i, int j, int n)
  {
      bool [, ] board = new bool[N, N];
      board[i, j] = true;

      // Call the recursive function to mark
      // visited cells.
      getCountRec(board, i, j, n);

      int cnt = 0;
      foreach(bool cell in board)
      {
          if(cell != false)
            cnt++;
      }
      return cnt;
  }

  // Driver code
  public static void Main()
  {
      int i = 3, j = 3, N = 2;

      Console.WriteLine(getCount(i, j, N));
  }
}

// This code is contributed by ihritik
```

**Output:** 

```
35
```