# 打印手机小键盘形成的所有 n 位数字图案

> 原文:[https://www . geesforgeks . org/print-n-digital-patterns-formed-mobile-keypad/](https://www.geeksforgeeks.org/print-n-digit-patterns-formed-mobile-keypad/)

给定一个数字 N，我们需要打印所有由手机键盘形成的 N 个数字模式。
注意:我们可以从手机小键盘的任意一个按键上、下、左、右移动，每个图案都包含唯一的按键。

![Mobile-keypad](img/7e82a5f8eea3ad5277c67de46daa9a8e.png)

**示例:**

```

Input :   N = 3   
Output :  all 3 digit Pattern are : 
           123, 125, 145, 147 
           236, 214, 258, 256, 254
           321, 325, 369, 365 
           412, 456, 452, 458, 478
           and so on ..
```

这个解决方案的想法是基于 DFS 的。我们一个接一个地选择所有键盘按键作为 N 位数的起始数字，之后，我们试图生成由该按键形成的所有 N 位数模式(使用 DFS，因为我们只能从该按键向上、向左、向右或向下移动)。

```
 PrintPattern Function (DFS Function) 
  Add current key to pattern
  Pattern += Keypad[x][y]
 .... make current key as visited 
  visited[x][y] = true;
 ... Print pattern if size of Pattern == N 
 Call DFS for all 4 adjacent keypad key 
 __DFS_function
```

下面是上述想法的实现:

## C++

```
// C++ program to print all n digit patterns
// formed by mobile keypad.
#include <bits/stdc++.h>
using namespace std;

// A function to check if a given cell (row, col)
// can be included in DFS
bool isSafe(int x, int y, bool Visited[][3])
{
    // row number is in range, column number
    // is in range and not yet visited
    return (x >= 0 && x < 4 && y >= 0 &&
            y < 3 && !Visited[x][y]);
}

// A utility function to do DFS for a mobile Keypad
// matrix. It only considers the 4 neighbors as
// adjacent vertice and print pattern of size n
void DFS(bool visited[][3], int Keypad[][3], int n,
         string pattern, int x, int y)
{

    // add current number to string
    pattern.push_back((Keypad[x][y] + '0'));

    // print pattern
    if (pattern.size() == n) {
        cout << pattern << " ";
        return;
    }

    // These arrays are used to get row and
    // column
    // numbers of 4 neighbours of a given cell
    static int row[] = { 0, 1, 0, -1 };
    static int col[] = { 1, 0, -1, 0 };

    // Mark this cell as visited
    visited[x][y] = true;

    // Recur for all connected neighbours
    for (int k = 0; k < 4; k++)
        if (isSafe(x + row[k], y + col[k], visited)
            && Keypad[x + row[k]][y + col[k]] != -1)
            DFS(visited, Keypad, n, pattern,
                       x + row[k], y + col[k]);

    // unvisited
    visited[x][y] = false;
    pattern.pop_back();
}

void patternOfSizeK(int Keypad[][3], int n)
{
    // Make a bool array to mark visited cells.
    // Initially all cells are unvisited
    bool visited[4][3];
    memset(visited, false, sizeof(visited));

    // try to generate all pattern of size n
    // by making every key of keypad as
    // starting char of pattern
    for (int i = 0; i < 4; i++)
        for (int j = 0; j < 3; j++)
            if (Keypad[i][j] != -1)
                DFS(visited, Keypad, n, "", i, j);
}

// Drive program to test above function.
int main()
{
    int Keypad[4][3] = { { 1, 2, 3 },
                         { 4, 5, 6 },
                         { 7, 8, 9 },
                         { -1, 0, -1 } };
    int n = 3;
    patternOfSizeK(Keypad, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all n digit patterns
// formed by mobile keypad.
public class Main
{
    // A function to check if a given cell (row, col)
    // can be included in DFS
    static boolean isSafe(int x, int y, boolean[][] Visited)
    {

        // row number is in range, column number
        // is in range and not yet visited
        return (x >= 0 && x < 4 && y >= 0 &&
                y < 3 && !Visited[x][y]);
    }

    // A utility function to do DFS for a mobile Keypad
    // matrix. It only considers the 4 neighbors as
    // adjacent vertice and print pattern of size n
    static void DFS(boolean[][] visited, int[][] Keypad, int n,
             String pattern, int x, int y)
    {

        // add current number to string
        pattern = pattern + Integer.toString(Keypad[x][y]);

        // print pattern
        if (pattern.length() == n) {
            System.out.print(pattern + " ");
            return;
        }

        // These arrays are used to get row and
        // column
        // numbers of 4 neighbours of a given cell
        int[] row = { 0, 1, 0, -1 };
        int[] col = { 1, 0, -1, 0 };

        // Mark this cell as visited
        visited[x][y] = true;

        // Recur for all connected neighbours
        for (int k = 0; k < 4; k++)
            if (isSafe(x + row[k], y + col[k], visited)
                && Keypad[x + row[k]][y + col[k]] != -1)
                DFS(visited, Keypad, n, pattern,
                           x + row[k], y + col[k]);

        // unvisited
        visited[x][y] = false;
        pattern = pattern.substring(0, pattern.length() - 1);
    }

    static void patternOfSizeK(int[][] Keypad, int n)
    {

        // Make a bool array to mark visited cells.
        // Initially all cells are unvisited
        boolean[][] visited = new boolean[4][3];
        for (int i = 0; i < 4; i++)
        {
            for (int j = 0; j < 3; j++)
            {
                visited[i][j] = false;
            }
        }

        // try to generate all pattern of size n
        // by making every key of keypad as
        // starting char of pattern
        for (int i = 0; i < 4; i++)
        {
            for (int j = 0; j < 3; j++)
            {
                if (Keypad[i][j] != -1)
                    DFS(visited, Keypad, n, "", i, j);
            }
        }
    }

  // Driver code
    public static void main(String[] args) {
        int[][] Keypad = { { 1, 2, 3 },
                         { 4, 5, 6 },
                         { 7, 8, 9 },
                         { -1, 0, -1 } };
        int n = 3;
        patternOfSizeK(Keypad, n);
    }
}

// This code is contributed by divyesh072019.
```

## 蟒蛇 3

```
# Python3 program to print all n digit patterns
# formed by mobile keypad.

# A function to check if a given cell
# (row, col) can be included in DFS
def isSafe(x, y, Visited):

    # row number is in range, column number
    # is in range and not yet visited
    return (x >= 0 and x < 4 and
            y >= 0 and y < 3 and not Visited[x][y])

# A utility function to do DFS for a mobile Keypad
# matrix. It only considers the 4 neighbors as
# adjacent vertice and print pattern of size n
def DFS(visited, Keypad, n, pattern, x, y):

    # Add current number to string
    pattern = pattern + str(Keypad[x][y])

    # Print pattern
    if (len(pattern) == n):
        print(pattern, end = ' ')
        return

    # These arrays are used to get row and
    # column
    # numbers of 4 neighbours of a given cell
    row = [ 0, 1, 0, -1 ]
    col = [ 1, 0, -1, 0 ]

    # Mark this cell as visited
    visited[x][y] = True

    # Recur for all connected neighbours
    for k in range(0, 4):

        if (isSafe(x + row[k],
                   y + col[k], visited) and
            Keypad[x + row[k]][y + col[k]] != -1):
            DFS(visited, Keypad, n, pattern,
                x + row[k], y + col[k])

    # unvisited
    visited[x][y] = False;
    pattern = pattern[:-1]

def patternOfSizeK(Keypad, n):

    # Make a bool array to mark visited cells.
    # Initially all cells are unvisited
    visited = [[False for i in range(3)]
                      for j in range(4)]

    # Try to generate all pattern of size n
    # by making every key of keypad as
    # starting char of pattern
    for i in range(4):
        for j in range(3):
            if (Keypad[i][j] != -1):
                DFS(visited, Keypad, n,
                    "", i, j)

# Drive code
if __name__=='__main__':

    Keypad = [ [ 1, 2, 3 ],
               [ 4, 5, 6 ],
               [ 7, 8, 9 ],
               [ -1, 0, -1 ] ]
    n = 3

    patternOfSizeK(Keypad, n)

# This code is contributed by rutvik_56
```

## C#

```
// C# program to print all n digit patterns
// formed by mobile keypad.
using System;
class GFG {

    // A function to check if a given cell (row, col)
    // can be included in DFS
    static bool isSafe(int x, int y, bool[,] Visited)
    {
        // row number is in range, column number
        // is in range and not yet visited
        return (x >= 0 && x < 4 && y >= 0 &&
                y < 3 && !Visited[x,y]);
    }

    // A utility function to do DFS for a mobile Keypad
    // matrix. It only considers the 4 neighbors as
    // adjacent vertice and print pattern of size n
    static void DFS(bool[,] visited, int[,] Keypad, int n,
             string pattern, int x, int y)
    {

        // add current number to string
        pattern = pattern + (Keypad[x,y]).ToString();

        // print pattern
        if (pattern.Length == n) {
            Console.Write(pattern + " ");
            return;
        }

        // These arrays are used to get row and
        // column
        // numbers of 4 neighbours of a given cell
        int[] row = { 0, 1, 0, -1 };
        int[] col = { 1, 0, -1, 0 };

        // Mark this cell as visited
        visited[x,y] = true;

        // Recur for all connected neighbours
        for (int k = 0; k < 4; k++)
            if (isSafe(x + row[k], y + col[k], visited)
                && Keypad[x + row[k],y + col[k]] != -1)
                DFS(visited, Keypad, n, pattern,
                           x + row[k], y + col[k]);

        // unvisited
        visited[x,y] = false;
        pattern = pattern.Substring(0, pattern.Length - 1);
    }

    static void patternOfSizeK(int[,] Keypad, int n)
    {
        // Make a bool array to mark visited cells.
        // Initially all cells are unvisited
        bool[,] visited = new bool[4,3];
        for (int i = 0; i < 4; i++)
        {
            for (int j = 0; j < 3; j++)
            {
                visited[i,j] = false;
            }
        }

        // try to generate all pattern of size n
        // by making every key of keypad as
        // starting char of pattern
        for (int i = 0; i < 4; i++)
        {
            for (int j = 0; j < 3; j++)
            {
                if (Keypad[i,j] != -1)
                    DFS(visited, Keypad, n, "", i, j);
            }
        }
    }

  static void Main() {
    int[,] Keypad = { { 1, 2, 3 },
                         { 4, 5, 6 },
                         { 7, 8, 9 },
                         { -1, 0, -1 } };
    int n = 3;
    patternOfSizeK(Keypad, n);
  }
}

// This code is contributed by suresh07.
```

## java 描述语言

```
<script>

// Javascript program to print all n digit patterns
// formed by mobile keypad.

// A function to check if a given cell (row, col)
// can be included in DFS
function isSafe(x, y, Visited)
{
    // row number is in range, column number
    // is in range and not yet visited
    return (x >= 0 && x < 4 && y >= 0 &&
            y < 3 && !Visited[x][y]);
}

// A utility function to do DFS for a mobile Keypad
// matrix. It only considers the 4 neighbors as
// adjacent vertice and print pattern of size n
function DFS(visited, Keypad, n, pattern, x, y)
{

    // add current number to string
    pattern+=String.fromCharCode(Keypad[x][y] +
    '0'.charCodeAt(0));

    // print pattern
    if (pattern.length == n) {
        document.write( pattern + " ");
        return;
    }

    // These arrays are used to get row and
    // column
    // numbers of 4 neighbours of a given cell
    var row = [ 0, 1, 0, -1 ];
    var col = [ 1, 0, -1, 0 ];

    // Mark this cell as visited
    visited[x][y] = true;

    // Recur for all connected neighbours
    for (var k = 0; k < 4; k++)
        if (isSafe(x + row[k], y + col[k], visited)
            && Keypad[x + row[k]][y + col[k]] != -1)
            DFS(visited, Keypad, n, pattern,
                       x + row[k], y + col[k]);

    // unvisited
    visited[x][y] = false;
    pattern = pattern.substring(0,pattern.length-2);
}

function patternOfSizeK( Keypad, n)
{
    // Make a bool array to mark visited cells.
    // Initially all cells are unvisited
    var visited = Array.from(Array(4),
    ()=>Array(3).fill(false));

    // try to generate all pattern of size n
    // by making every key of keypad as
    // starting char of pattern
    for (var i = 0; i < 4; i++)
        for (var j = 0; j < 3; j++)
            if (Keypad[i][j] != -1)
                DFS(visited, Keypad, n, "", i, j);
}

// Drive program to test above function.
var Keypad = [ [ 1, 2, 3 ],
                     [ 4, 5, 6 ],
                     [ 7, 8, 9 ],
                     [ -1, 0, -1 ] ];
var n = 3;
patternOfSizeK(Keypad, n);

</script>
```

**输出:**

```
123 125 145 147 236 256 258 254 214 369 365 325 321 
456 458 452 478 412 569 563 589 580 587 547 541 523 521 
698 658 654 652 632 789 780 785 745 741 896 874 856 854 852 
980 987 985 965 963 089 087 085
```