# 检查棋盘上是否有任何国王不安全

> 原文： [https://www.geeksforgeeks.org/check-if-any-king-is-unsafe-on-the-chessboard-or-not/](https://www.geeksforgeeks.org/check-if-any-king-is-unsafe-on-the-chessboard-or-not/)

给定由字符`K`或`k`组成的矩阵 **board [] []** ，`Q`或`q`，`B`或`b`，`N`或`n`，`R`或`r`和`P`或`p`（大写白色和小写黑色）代表**国王**，**女王**， **Bishop** ，**骑士**， **Rook** 和**兵**分别具有**黑色**和**白色**颜色和 ****'-'**指示的空白**，任务是检查哪个国王（黑白色）不安全，即检查它是否受到其他任何部分的攻击（可以消除），以及 相应地打印答案。

**注意**：如果两个国王都安全，则输出“没有危险国王”。

**范例**：

```
Input: 
board[][] = {{- - - k - - - -}, 
             {p p p - p p p p}, 
             {- - - - - b - -}, 
             {- - - R - - - -}, 
             {- - - - - - - -}, 
             {- - - - - - - -}, 
             {P - P P P P P P}, 
             {K - - - - - - - }}
Output:White King in danger
Explanation: Black bishop can attack the white king.

Input:
board[][] = {{- - k - - - - -}, 
             {p p p - p p p p}, 
             {- - - - - - b -}, 
             {- - - R - - - -}, 
             {- - - - - - - -}, 
             {- - - - - - - -}
             {P - P P P P P P}, 
             {K - - - - - - -}}
Output: No King in danger
```

**方法**：

方法是检查棋盘上每个棋子的移动：

1.  检查白色和黑色国王的位置。

2.  对于每个国王，请检查相反颜色的 Rook，主教，骑士，国王，王后，典当，是否正在攻击国王。

3.  检查女王/王后的攻击是结合检查菜鸟和主教的攻击。 如果满足任何条件，则女王将进攻。

4.  如果两个国王中的任何一个都不满足进攻条件，那么两个国王都没有危险。

5.  否则，打印满足不安全条件的国王的答案。

下面是此方法的实现。

## C++

```cpp

// C++ program to implement the 
// above approach
#include <bits/stdc++.h>
using namespace std;

// Check if the indices 
// are within the matrix 
// or not
bool inBounds(int i, 
              int j)
{
  // Checking boundary 
  // conditions
  return i >= 0 && i < 8 && 
         j >= 0 && j < 8;
}

bool lookFork(char board[][8], 
              char c, int i, 
              int j)
{
  // Store all possible moves 
  // of the king
  int x[] = {-1, -1, -1, 0, 
             0, 1, 1, 1};
  int y[] = {-1, 0, 1, -1,
             1, -1, 0, 1};

  for (int k = 0; k < 8; k++) 
  {
    // incrementing index 
    // values
    int m = i + x[k];
    int n = j + y[k];

    // checking boundary 
    // conditions and 
    // character match
    if (inBounds(m, n) && 
        board[m][n] == c)
      return true;
  }
  return false;
}

// Function to check if bishop 
// can attack the king
bool lookForb(char board[][8], 
              char c, int i, 
              int j)
{
  // Check the lower right 
  // diagonal
  int k = 0;
  while (inBounds(i + ++k, j + k)) 
  {
    if (board[i + k][j + k] == c)
      return true;
    if (board[i + k][j + k] != '-')
      break;
  }

  // Check the lower left diagonal
  k = 0;
  while (inBounds(i + ++k, j - k)) 
  {

    if (board[i + k][j - k] == c)
      return true;
    if (board[i + k][j - k] != '-')
      break;
  }

  // Check the upper right 
  // diagonal
  k = 0;
  while (inBounds(i - ++k, j + k)) 
  {
    if (board[i - k][j + k] == c)
      return true;
    if (board[i - k][j + k] != '-')
      break;
  }

  // Check the upper left 
  // diagonal
  k = 0;
  while (inBounds(i - ++k, j - k))
  {
    if (board[i - k][j - k] == c)
      return true;
    if (board[i - k][j - k] != '-')
      break;
  }

  return false;
}

// Check if
bool lookForr(char board[][8], 
              char c, int i, 
              int j)
{
  // Check downwards
  int k = 0;
  while (inBounds(i + ++k, j)) 
  {
    if (board[i + k][j] == c)
      return true;
    if (board[i + k][j] != '-')
      break;
  }

  // Check upwards
  k = 0;
  while (inBounds(i + --k, j)) 
  {
    if (board[i + k][j] == c)
      return true;
    if (board[i + k][j] != '-')
      break;
  }

  // Check right
  k = 0;
  while (inBounds(i, j + ++k)) 
  {
    if (board[i][j + k] == c)
      return true;
    if (board[i][j + k] != '-')
      break;
  }

  // Check left
  k = 0;
  while (inBounds(i, j + --k)) 
  {
    if (board[i][j + k] == c)
      return true;
    if (board[i][j + k] != '-')
      break;
  }
  return false;
}

// Function to check if Queen 
// can attack the King
bool lookForq(char board[][8], 
              char c, int i, 
              int j)
{
  // Queen's moves are a combination
  // of both the Bishop and the Rook
  if (lookForb(board, c, i, j) || 
      lookForr(board, c, i, j))
    return true;

  return false;
}

// Check if the knight can 
// attack the king
bool lookForn(char board[][8], 
              char c, int i, 
              int j)
{
  // All possible moves of
  // the knight
  int x[] = {2, 2, -2, -2, 
             1, 1, -1, -1};
  int y[] = {1, -1, 1, -1, 
             2, -2, 2, -2};

  for (int k = 0; k < 8; k++) 
  {
    // Incrementing index 
    // values
    int m = i + x[k];
    int n = j + y[k];

    // Checking boundary conditions
    // and character match
    if (inBounds(m, n) && 
        board[m][n] == c)
      return true;
  }
  return false;
}

// Function to check if pawn 
// can attack the king
bool lookForp(char board[][8], 
              char c, int i, 
              int j)
{
  char lookFor;
  if (isupper(c)) 
  {
    // Check for white pawn
    lookFor = 'P';
    if (inBounds(i + 1, j - 1) && 
        board[i + 1][j - 1] == lookFor)
      return true;

    if (inBounds(i + 1, j + 1) && 
        board[i + 1][j + 1] == lookFor)
      return true;
  }
  else
  {
    // Check for black pawn
    lookFor = 'p';
    if (inBounds(i - 1, j - 1) && 
        board[i - 1][j - 1] == lookFor)
      return true;
    if (inBounds(i - 1, j + 1) && 
        board[i - 1][j + 1] == lookFor)
      return true;
  }
  return false;
}

// Function to check if any 
// of the two kings is unsafe
// or not
int checkBoard(char board[][8])
{
  // Find the position of both 
  // the kings
  for (int i = 0; i < 8; i++) 
  {
    for (int j = 0; j < 8; j++) 
    {
      // Check for all pieces which
      // can attack White King
      if (board[i][j] == 'k') 
      {
        // Check for Knight
        if (lookForn(board, 
                     'N', i, j))
          return 1;

        // Check for Pawn
        if (lookForp(board, 
                     'P', i, j))
          return 1;

        // Check for Rook
        if (lookForr(board, 
                     'R', i, j))
          return 1;

        // Check for Bishop
        if (lookForb(board, 
                     'B', i, j))
          return 1;

        // Check for Queen
        if (lookForq(board, 
                     'Q', i, j))
          return 1;

        // Check for King
        if (lookFork(board, 
                     'K', i, j))
          return 1;
      }

      // Check for all pieces which
      // can attack Black King
      if (board[i][j] == 'K') 
      {
        // Check for Knight
        if (lookForn(board, 
                     'n', i, j))
          return 2;

        // Check for Pawn
        if (lookForp(board, 
                     'p', i, j))
          return 2;

        // Check for Rook
        if (lookForr(board, 
                     'r', i, j))
          return 2;

        // Check for Bishop
        if (lookForb(board, 
                     'b', i, j))
          return 2;

        // Check for Queen
        if (lookForq(board, 
                     'q', i, j))
          return 2;

        // Check for King
        if (lookFork(board, 
                     'k', i, j))
          return 2;
      }
    }
  }
  return 0;
}

// Driver Code
int main()
{
  // Chessboard instance
  char board[][8] = {{'-', '-', '-', 'k', 
                      '-', '-', '-', '-'},
                     {'p', 'p', 'p', '-', 
                      'p', 'p', 'p', 'p'},
                     {'-', '-', '-', '-', 
                      '-', 'b', '-', '-'},
                     { '-', '-', '-', 'R', 
                      '-', '-', '-', '-'},
                     {'-', '-', '-', '-', 
                      '-', '-', '-', '-'}, 
                     {'-', '-', '-', '-', 
                      '-', '-', '-', '-'}, 
                     {'P', '-', 'P', 'P', 
                      'P', 'P', 'P', 'P'}, 
                     {'K', '-', '-', '-', 
                      '-', '-', '-', '-'}};

  if (checkBoard(board) == 0)
    cout << ("No king in danger");

  else if (checkBoard(board) == 1)
    cout << ("White king in danger");

  else
    cout << ("Black king in danger");
}

// This code is contributed by Chitranyal

```

## Java

```java

public class Gfg {

    // Function to check if any of the two
    // kings is unsafe or not
    private static int checkBoard(char[][] board)
    {

        // Find the position of both the kings
        for (int i = 0; i < 8; i++) {
            for (int j = 0; j < 8; j++) {

                // Check for all pieces which
                // can attack White King
                if (board[i][j] == 'k') {

                    // Check for Knight
                    if (lookForn(board, 'N', i, j))
                        return 1;

                    // Check for Pawn
                    if (lookForp(board, 'P', i, j))
                        return 1;

                    // Check for Rook
                    if (lookForr(board, 'R', i, j))
                        return 1;

                    // Check for Bishop
                    if (lookForb(board, 'B', i, j))
                        return 1;

                    // Check for Queen
                    if (lookForq(board, 'Q', i, j))
                        return 1;

                    // Check for King
                    if (lookFork(board, 'K', i, j))
                        return 1;
                }

                // Check for all pieces which
                // can attack Black King
                if (board[i][j] == 'K') {

                    // Check for Knight
                    if (lookForn(board, 'n', i, j))
                        return 2;

                    // Check for Pawn
                    if (lookForp(board, 'p', i, j))
                        return 2;

                    // Check for Rook
                    if (lookForr(board, 'r', i, j))
                        return 2;

                    // Check for Bishop
                    if (lookForb(board, 'b', i, j))
                        return 2;

                    // Check for Queen
                    if (lookForq(board, 'q', i, j))
                        return 2;

                    // Check for King
                    if (lookFork(board, 'k', i, j))
                        return 2;
                }
            }
        }
        return 0;
    }

    private static boolean lookFork(char[][] board,
                                    char c, int i, int j)
    {

        // Store all possible moves of the king
        int[] x = { -1, -1, -1, 0, 0, 1, 1, 1 };
        int[] y = { -1, 0, 1, -1, 1, -1, 0, 1 };

        for (int k = 0; k < 8; k++) {

            // incrementing index values
            int m = i + x[k];
            int n = j + y[k];

            // checking boundary conditions
            // and character match
            if (inBounds(m, n) && board[m][n] == c)
                return true;
        }
        return false;
    }

    // Function to check if Queen can attack the King
    private static boolean lookForq(char[][] board,
                                    char c, int i, int j)
    {

        // Queen's moves are a combination
        // of both the Bishop and the Rook
        if (lookForb(board, c, i, j) || lookForr(board, c, i, j))
            return true;

        return false;
    }

    // Function to check if bishop can attack the king
    private static boolean lookForb(char[][] board,
                                    char c, int i, int j)
    {

        // Check the lower right diagonal
        int k = 0;
        while (inBounds(i + ++k, j + k)) {

            if (board[i + k][j + k] == c)
                return true;
            if (board[i + k][j + k] != '-')
                break;
        }

        // Check the lower left diagonal
        k = 0;
        while (inBounds(i + ++k, j - k)) {

            if (board[i + k][j - k] == c)
                return true;
            if (board[i + k][j - k] != '-')
                break;
        }

        // Check the upper right diagonal
        k = 0;
        while (inBounds(i - ++k, j + k)) {

            if (board[i - k][j + k] == c)
                return true;
            if (board[i - k][j + k] != '-')
                break;
        }

        // Check the upper left diagonal
        k = 0;
        while (inBounds(i - ++k, j - k)) {

            if (board[i - k][j - k] == c)
                return true;
            if (board[i - k][j - k] != '-')
                break;
        }

        return false;
    }

    // Check if
    private static boolean lookForr(char[][] board,
                                    char c, int i, int j)
    {

        // Check downwards
        int k = 0;
        while (inBounds(i + ++k, j)) {
            if (board[i + k][j] == c)
                return true;
            if (board[i + k][j] != '-')
                break;
        }

        // Check upwards
        k = 0;
        while (inBounds(i + --k, j)) {
            if (board[i + k][j] == c)
                return true;
            if (board[i + k][j] != '-')
                break;
        }

        // Check right
        k = 0;
        while (inBounds(i, j + ++k)) {
            if (board[i][j + k] == c)
                return true;
            if (board[i][j + k] != '-')
                break;
        }

        // Check left
        k = 0;
        while (inBounds(i, j + --k)) {
            if (board[i][j + k] == c)
                return true;
            if (board[i][j + k] != '-')
                break;
        }
        return false;
    }

    // Check if the knight can attack the king
    private static boolean lookForn(char[][] board,
                                    char c, int i, int j)
    {

        // All possible moves of the knight
        int[] x = { 2, 2, -2, -2, 1, 1, -1, -1 };
        int[] y = { 1, -1, 1, -1, 2, -2, 2, -2 };

        for (int k = 0; k < 8; k++) {

            // Incrementing index values
            int m = i + x[k];
            int n = j + y[k];

            // Checking boundary conditions
            // and character match
            if (inBounds(m, n) && board[m][n] == c)
                return true;
        }
        return false;
    }

    // Function to check if pawn can attack the king
    private static boolean lookForp(char[][] board,
                                    char c, int i, int j)
    {

        char lookFor;
        if (Character.isUpperCase(c)) {

            // Check for white pawn
            lookFor = 'P';
            if (inBounds(i + 1, j - 1)
                && board[i + 1][j - 1] == lookFor)
                return true;

            if (inBounds(i + 1, j + 1)
                && board[i + 1][j + 1] == lookFor)
                return true;
        }
        else {

            // Check for black pawn
            lookFor = 'p';
            if (inBounds(i - 1, j - 1)
                && board[i - 1][j - 1] == lookFor)
                return true;
            if (inBounds(i - 1, j + 1)
                && board[i - 1][j + 1] == lookFor)
                return true;
        }
        return false;
    }

    // Check if the indices are within
    // the matrix or not
    private static boolean inBounds(int i, int j)
    {

        // Checking boundary conditions
        return i >= 0 && i < 8 && j >= 0 && j < 8;
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Chessboard instance
        char[][] board
            = { { '-', '-', '-', 'k', '-', '-', '-', '-' },
                { 'p', 'p', 'p', '-', 'p', 'p', 'p', 'p' },
                { '-', '-', '-', '-', '-', 'b', '-', '-' },
                { '-', '-', '-', 'R', '-', '-', '-', '-' },
                { '-', '-', '-', '-', '-', '-', '-', '-' },
                { '-', '-', '-', '-', '-', '-', '-', '-' },
                { 'P', '-', 'P', 'P', 'P', 'P', 'P', 'P' },
                { 'K', '-', '-', '-', '-', '-', '-', '-' } };

        if (checkBoard(board) == 0)
            System.out.println("No king in danger");

        else if (checkBoard(board) == 1)
            System.out.println("White king in danger");

        else
            System.out.println("Black king in danger");
    }
}

```

## C#

```cs

using System;

class GFG{ 

// Function to check if any of the two 
// kings is unsafe or not 
private static int checkBoard(char[,] board) 
{ 

    // Find the position of both the kings 
    for(int i = 0; i < 8; i++)
    { 
        for(int j = 0; j < 8; j++) 
        { 

            // Check for all pieces which 
            // can attack White King 
            if (board[i, j] == 'k')
            { 

                // Check for Knight 
                if (lookForn(board, 'N', i, j)) 
                    return 1; 

                // Check for Pawn 
                if (lookForp(board, 'P', i, j)) 
                    return 1; 

                // Check for Rook 
                if (lookForr(board, 'R', i, j)) 
                    return 1; 

                // Check for Bishop 
                if (lookForb(board, 'B', i, j)) 
                    return 1; 

                // Check for Queen 
                if (lookForq(board, 'Q', i, j)) 
                    return 1; 

                // Check for King 
                if (lookFork(board, 'K', i, j)) 
                    return 1; 
            } 

            // Check for all pieces which 
            // can attack Black King 
            if (board[i, j] == 'K') 
            { 

                // Check for Knight 
                if (lookForn(board, 'n', i, j)) 
                    return 2; 

                // Check for Pawn 
                if (lookForp(board, 'p', i, j)) 
                    return 2; 

                // Check for Rook 
                if (lookForr(board, 'r', i, j)) 
                    return 2; 

                // Check for Bishop 
                if (lookForb(board, 'b', i, j)) 
                    return 2; 

                // Check for Queen 
                if (lookForq(board, 'q', i, j)) 
                    return 2; 

                // Check for King 
                if (lookFork(board, 'k', i, j)) 
                    return 2; 
            } 
        } 
    } 
    return 0; 
} 

private static bool lookFork(char[,] board, 
                             char c, int i,
                             int j) 
{ 

    // Store all possible moves of the king 
    int[] x = { -1, -1, -1, 0, 0, 1, 1, 1 }; 
    int[] y = { -1, 0, 1, -1, 1, -1, 0, 1 }; 

    for(int k = 0; k < 8; k++) 
    { 

        // Incrementing index values 
        int m = i + x[k]; 
        int n = j + y[k]; 

        // Checking boundary conditions 
        // and character match 
        if (inBounds(m, n) && board[m, n] == c) 
            return true; 
    } 
    return false; 
} 

// Function to check if Queen can attack the King 
private static bool lookForq(char[,] board, 
                             char c, int i, 
                             int j) 
{ 

    // Queen's moves are a combination 
    // of both the Bishop and the Rook 
    if (lookForb(board, c, i, j) ||
        lookForr(board, c, i, j)) 
        return true; 

    return false; 
} 

// Function to check if bishop can attack the king 
private static bool lookForb(char[,] board, 
                             char c, int i, 
                             int j) 
{ 

    // Check the lower right diagonal 
    int k = 0; 
    while (inBounds(i + ++k, j + k))
    { 
        if (board[i + k, j + k] == c) 
            return true; 
        if (board[i + k, j + k] != '-') 
            break; 
    } 

    // Check the lower left diagonal 
    k = 0; 
    while (inBounds(i + ++k, j - k)) 
    { 
        if (board[i + k, j - k] == c) 
            return true; 
        if (board[i + k, j - k] != '-') 
            break; 
    } 

    // Check the upper right diagonal 
    k = 0; 
    while (inBounds(i - ++k, j + k))
    { 
        if (board[i - k, j + k] == c) 
            return true; 
        if (board[i - k, j + k] != '-') 
            break; 
    } 

    // Check the upper left diagonal 
    k = 0; 
    while (inBounds(i - ++k, j - k))
    { 
        if (board[i - k, j - k] == c) 
            return true; 
        if (board[i - k, j - k] != '-') 
            break; 
    } 
    return false; 
} 

// Check if 
private static bool lookForr(char[,] board, 
                             char c, int i,
                             int j) 
{ 

    // Check downwards 
    int k = 0; 
    while (inBounds(i + ++k, j)) 
    { 
        if (board[i + k, j] == c) 
            return true; 
        if (board[i + k, j] != '-') 
            break; 
    } 

    // Check upwards 
    k = 0; 
    while (inBounds(i + --k, j))
    { 
        if (board[i + k, j] == c) 
            return true; 
        if (board[i + k, j] != '-') 
            break; 
    } 

    // Check right 
    k = 0; 
    while (inBounds(i, j + ++k)) 
    { 
        if (board[i, j + k] == c) 
            return true; 
        if (board[i, j + k] != '-') 
            break; 
    } 

    // Check left 
    k = 0; 
    while (inBounds(i, j + --k))
    { 
        if (board[i, j + k] == c) 
            return true; 
        if (board[i, j + k] != '-') 
            break; 
    } 
    return false; 
} 

// Check if the knight can attack the king 
private static bool lookForn(char[,] board, 
                             char c, int i, 
                             int j) 
{ 

    // All possible moves of the knight 
    int[] x = { 2, 2, -2, -2, 1, 1, -1, -1 }; 
    int[] y = { 1, -1, 1, -1, 2, -2, 2, -2 }; 

    for(int k = 0; k < 8; k++)
    { 

        // Incrementing index values 
        int m = i + x[k]; 
        int n = j + y[k]; 

        // Checking boundary conditions 
        // and character match 
        if (inBounds(m, n) && board[m, n] == c) 
            return true; 
    } 
    return false; 
} 

// Function to check if pawn can attack the king 
private static bool lookForp(char[,] board, 
                             char c, int i, 
                             int j) 
{ 
    char lookFor; 
    if (char.IsUpper(c))
    { 

        // Check for white pawn 
        lookFor = 'P'; 
        if (inBounds(i + 1, j - 1) && 
               board[i + 1, j - 1] == lookFor) 
            return true; 

        if (inBounds(i + 1, j + 1) &&
               board[i + 1, j + 1] == lookFor) 
            return true; 
    } 
    else
    { 

        // Check for black pawn 
        lookFor = 'p'; 
        if (inBounds(i - 1, j - 1) &&
               board[i - 1, j - 1] == lookFor) 
            return true; 
        if (inBounds(i - 1, j + 1) && 
               board[i - 1, j + 1] == lookFor) 
            return true; 
    } 
    return false; 
} 

// Check if the indices are within 
// the matrix or not 
private static bool inBounds(int i, int j) 
{ 

    // Checking boundary conditions 
    return i >= 0 && i < 8 && j >= 0 && j < 8; 
} 

// Driver Code 
public static void Main(String[] args) 
{ 

    // Chessboard instance 
    char[,] board 
        = { { '-', '-', '-', 'k', '-', '-', '-', '-' }, 
            { 'p', 'p', 'p', '-', 'p', 'p', 'p', 'p' }, 
            { '-', '-', '-', '-', '-', 'b', '-', '-' }, 
            { '-', '-', '-', 'R', '-', '-', '-', '-' }, 
            { '-', '-', '-', '-', '-', '-', '-', '-' }, 
            { '-', '-', '-', '-', '-', '-', '-', '-' }, 
            { 'P', '-', 'P', 'P', 'P', 'P', 'P', 'P' }, 
            { 'K', '-', '-', '-', '-', '-', '-', '-' } }; 

    if (checkBoard(board) == 0) 
        Console.WriteLine("No king in danger"); 

    else if (checkBoard(board) == 1) 
        Console.WriteLine("White king in danger"); 

    else
        Console.WriteLine("Black king in danger"); 
} 
} 

// This code is contributed by 29AjayKumar

```

**Output:** 

```
White king in danger

```

**时间复杂度**：O（N <sup>3</sup> ）

**辅助空间**：`O(1)`



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。