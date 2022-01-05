# 检查棋盘上是否有王不安全

> 原文:[https://www . geesforgeks . org/check-if-any-king-is-unsafe-on-the-bottle-or-not/](https://www.geeksforgeeks.org/check-if-any-king-is-unsafe-on-the-chessboard-or-not/)

给定一个由字符 **K** 或 **k** 、 **Q** 或 **q** 、 **B** 或 **b** 、 **N** 或 **n** 、 **R** 或 **r** 、以及 **P** 或 **p【的矩阵**板】[]【】T1】 **骑士**、车**车**、**棋子**分别为**黑**和**白**颜色，**空格**由**'-**表示，任务是检查哪个王(黑的白的)不安全，即是否受到其他任何棋子的攻击(可以消灭)，并据此打印答案。
**注意:**如果两个国王都安全，那么输出“无国王有危险”。
**示例:******

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

**进场:**
进场是检查棋盘上每一个棋子的走法:

1.  检查白人和黑人国王的位置。
2.  对于每个国王，检查对面颜色的车、主教、骑士、国王、女王、棋子，不管他们是否在攻击国王。
3.  检查女王的攻击是车和主教检查攻击的组合。如果任何一个条件是真的，那么女王就会攻击。
4.  如果两个国王中的任何一个都不满足攻击条件，那么对两个国王都没有危险。
5.  否则，为满足不安全条件的国王打印答案。

下面是这个方法的实现。

## C++

```
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

## Java 语言(一种计算机语言，尤用于创建网站)

```
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

## 蟒蛇 3

```
# Python3 program to implement the above approach

# Function to check if any of the two
# kings is unsafe or not
def checkBoard(board):

    # Find the position of both the kings
    for i in range(8):
        for j in range(8):

            # Check for all pieces which
            # can attack White King
            if board[i][j] == 'k':

                # Check for Knight
                if lookForn(board, 'N', i, j):
                    return 1

                # Check for Pawn
                if lookForp(board, 'P', i, j):
                    return 1

                # Check for Rook
                if lookForr(board, 'R', i, j):
                    return 1

                # Check for Bishop
                if lookForb(board, 'B', i, j):
                    return 1

                # Check for Queen
                if lookForq(board, 'Q', i, j):
                    return 1

                # Check for King
                if lookFork(board, 'K', i, j):
                    return 1

            # Check for all pieces which
            # can attack Black King
            if board[i][j] == 'K':
                # Check for Knight
                if lookForn(board, 'n', i, j):
                    return 2

                # Check for Pawn
                if lookForp(board, 'p', i, j):
                    return 2

                # Check for Rook
                if lookForr(board, 'r', i, j):
                    return 2

                # Check for Bishop
                if lookForb(board, 'b', i, j):
                    return 2

                # Check for Queen
                if lookForq(board, 'q', i, j):
                    return 2

                # Check for King
                if lookFork(board, 'k', i, j):
                    return 2
    return 1

def lookFork(board, c, i, j):
    # Store all possible moves of the king
    x = [ -1, -1, -1, 0, 0, 1, 1, 1 ]
    y = [ -1, 0, 1, -1, 1, -1, 0, 1 ]

    for k in range(8):
        # incrementing index values
        m = i + x[k]
        n = j + y[k]

        # checking boundary conditions
        # and character match
        if inBounds(m, n) and board[m][n] == c:
            return True
    return False

# Function to check if Queen can attack the King
def lookForq(board, c, i, j):

    # Queen's moves are a combination
    # of both the Bishop and the Rook
    if lookForb(board, c, i, j) or lookForr(board, c, i, j):
        return True
    return False

# Function to check if bishop can attack the king
def lookForb(board, c, i, j):
    # Check the lower right diagonal
    k = 0
    while inBounds(i + ++k, j + k):
        if board[i + k][j + k] == c:
            return True
        if board[i + k][j + k] != '-':
            break

    # Check the lower left diagonal
    k = 0
    while inBounds(i + ++k, j - k):
        if board[i + k][j - k] == c:
            return True
        if board[i + k][j - k] != '-':
            break

    # Check the upper right diagonal
    k = 0
    while inBounds(i - ++k, j + k):
        if board[i - k][j + k] == c:
            return True
        if board[i - k][j + k] != '-':
            break

    # Check the upper left diagonal
    k = 0
    while inBounds(i - ++k, j - k):
        if board[i - k][j - k] == c:
            return True
        if board[i - k][j - k] != '-':
            break

    return False

# Check if
def lookForr(board, c, i, j):
    # Check downwards
    k = 0
    while inBounds(i + ++k, j):
        if board[i + k][j] == c:
            return True
        if board[i + k][j] != '-':
            break

    # Check upwards
    k = 0
    while inBounds(i + --k, j):
        if board[i + k][j] == c:
            return True
        if board[i + k][j] != '-':
            break

    # Check right
    k = 0
    while inBounds(i, j + ++k):
        if board[i][j + k] == c:
            return True
        if board[i][j + k] != '-':
            break

    # Check left
    k = 0
    while inBounds(i, j + --k):
        if board[i][j + k] == c:
            return True
        if board[i][j + k] != '-':
            break
    return False

# Check if the knight can attack the king
def lookForn(board, c, i, j):
    # All possible moves of the knight
    x = [ 2, 2, -2, -2, 1, 1, -1, -1 ]
    y = [ 1, -1, 1, -1, 2, -2, 2, -2 ]

    for k in range(8):
        # Incrementing index values
        m = i + x[k]
        n = j + y[k]

        # Checking boundary conditions
        # and character match
        if inBounds(m, n) and board[m][n] == c:
            return True
    return False

# Function to check if pawn can attack the king
def lookForp(board, c, i, j):
    if ord(c) >= 65 and ord(c) <= 90:
        # Check for white pawn
        lookFor = 'P'
        if inBounds(i + 1, j - 1) and board[i + 1][j - 1] == lookFor:
            return True

        if inBounds(i + 1, j + 1) and board[i + 1][j + 1] == lookFor:
            return True
    else:
        # Check for black pawn
        lookFor = 'p'
        if inBounds(i - 1, j - 1) and board[i - 1][j - 1] == lookFor:
            return True
        if inBounds(i - 1, j + 1) and board[i - 1][j + 1] == lookFor:
            return True
    return False

# Check if the indices are within
# the matrix or not
def inBounds(i, j):
    # Checking boundary conditions
    return i >= 0 and i < 8 and j >= 0 and j < 8

# Chessboard instance
board = [ [ '-', '-', '-', 'k', '-', '-', '-', '-' ],
  [ 'p', 'p', 'p', '-', 'p', 'p', 'p', 'p' ],
  [ '-', '-', '-', '-', '-', 'b', '-', '-' ],
  [ '-', '-', '-', 'R', '-', '-', '-', '-' ],
  [ '-', '-', '-', '-', '-', '-', '-', '-' ],
  [ '-', '-', '-', '-', '-', '-', '-', '-' ],
  [ 'P', '-', 'P', 'P', 'P', 'P', 'P', 'P' ],
  [ 'K', '-', '-', '-', '-', '-', '-', '-' ] ]

if checkBoard(board) == 0:
  print("No king in danger")
elif checkBoard(board) == 1:
  print("White king in danger")
else:
  print("Black king in danger")

  # This code is contributed by divyeshrabadiya07.
```

## C#

```
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

## java 描述语言

```
<script>
    // Javascript program to implement the above approach

    // Function to check if any of the two
    // kings is unsafe or not
    function checkBoard(board)
    {

        // Find the position of both the kings
        for (let i = 0; i < 8; i++) {
            for (let j = 0; j < 8; j++) {

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

    function lookFork(board, c, i, j)
    {

        // Store all possible moves of the king
        let x = [ -1, -1, -1, 0, 0, 1, 1, 1 ];
        let y = [ -1, 0, 1, -1, 1, -1, 0, 1 ];

        for (let k = 0; k < 8; k++) {

            // incrementing index values
            let m = i + x[k];
            let n = j + y[k];

            // checking boundary conditions
            // and character match
            if (inBounds(m, n) && board[m][n] == c)
                return true;
        }
        return false;
    }

    // Function to check if Queen can attack the King
    function lookForq(board, c, i, j)
    {

        // Queen's moves are a combination
        // of both the Bishop and the Rook
        if (lookForb(board, c, i, j) || lookForr(board, c, i, j))
            return true;

        return false;
    }

    // Function to check if bishop can attack the king
    function lookForb(board, c, i, j)
    {

        // Check the lower right diagonal
        let k = 0;
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
    function lookForr(board, c, i, j)
    {

        // Check downwards
        let k = 0;
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
    function lookForn(board, c, i, j)
    {

        // All possible moves of the knight
        let x = [ 2, 2, -2, -2, 1, 1, -1, -1 ];
        let y = [ 1, -1, 1, -1, 2, -2, 2, -2 ];

        for (let k = 0; k < 8; k++) {

            // Incrementing index values
            let m = i + x[k];
            let n = j + y[k];

            // Checking boundary conditions
            // and character match
            if (inBounds(m, n) && board[m][n] == c)
                return true;
        }
        return false;
    }

    // Function to check if pawn can attack the king
    function lookForp(board, c, i, j)
    {

        let lookFor;
        if (c.charCodeAt() >= 65 && c.charCodeAt() <= 90) {

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
    function inBounds(i, j)
    {

        // Checking boundary conditions
        return i >= 0 && i < 8 && j >= 0 && j < 8;
    }

    // Chessboard instance
    let board
      = [ [ '-', '-', '-', 'k', '-', '-', '-', '-' ],
      [ 'p', 'p', 'p', '-', 'p', 'p', 'p', 'p' ],
      [ '-', '-', '-', '-', '-', 'b', '-', '-' ],
      [ '-', '-', '-', 'R', '-', '-', '-', '-' ],
      [ '-', '-', '-', '-', '-', '-', '-', '-' ],
      [ '-', '-', '-', '-', '-', '-', '-', '-' ],
      [ 'P', '-', 'P', 'P', 'P', 'P', 'P', 'P' ],
      [ 'K', '-', '-', '-', '-', '-', '-', '-' ] ];

    if (checkBoard(board) == 0)
      document.write("No king in danger");

    else if (checkBoard(board) == 1)
      document.write("White king in danger");

    else
      document.write("Black king in danger");

    // This code is contributed by divyesh072019.
</script>
```

**Output:** 

```
White king in danger
```

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(1)*