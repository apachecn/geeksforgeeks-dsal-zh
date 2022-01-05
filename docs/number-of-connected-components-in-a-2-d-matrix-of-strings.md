# 二维字符串矩阵中连接的组件数量

> 原文:[https://www . geesforgeks . org/2 维字符串矩阵中连接的组件数量/](https://www.geeksforgeeks.org/number-of-connected-components-in-a-2-d-matrix-of-strings/)

给定一个二维矩阵 **mat[][]** ，任务是计算矩阵中连接组件的数量。一个连接的组件由所有相等的元素组成，这些元素与同一组件的至少一个其他元素共享某个公共边。
**例:**

```
Input: mat[][] = {"bbba", 
                                   "baaa"}
Output: 2
The two connected components are:
bbb       
b

AND

  a
aaa

Input: mat[][] = {"aabba", 
                                   "aabba", 
                                   "aaaca"}
Output: 4
```

**方法:**对于每个在执行 [DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 之前没有访问过的小区。DFS 将以相同的值覆盖所有连接的单元格(上、左、右和下)。所以答案是 DFS 运行的总次数。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define maxRow 500
#define maxCol 500

bool visited[maxRow][maxCol] = { 0 };

// Function that return true if mat[row][col]
// is valid and hasn't been visited
bool isSafe(string M[], int row, int col, char c,
                                    int n, int l)
{
    // If row and column are valid and element
    // is matched and hasn't been visited then
    // the cell is safe
    return (row >= 0 && row < n)
           && (col >= 0 && col < l)
           && (M[row][col] == c && !visited[row][col]);
}

// Function for depth first search
void DFS(string M[], int row, int col, char c,
                                 int n, int l)
{
    // These arrays are used to get row and column
    // numbers of 4 neighbours of a given cell
    int rowNbr[] = { -1, 1, 0, 0 };
    int colNbr[] = { 0, 0, 1, -1 };

    // Mark this cell as visited
    visited[row][col] = true;

    // Recur for all connected neighbours
    for (int k = 0; k < 4; ++k)
        if (isSafe(M, row + rowNbr[k],
                  col + colNbr[k], c, n, l))

            DFS(M, row + rowNbr[k],
                col + colNbr[k], c, n, l);
}

// Function to return the number of
// connectewd components in the matrix
int connectedComponents(string M[], int n)
{
    int connectedComp = 0;
    int l = M[0].length();

    for (int i = 0; i < n; i++) {
        for (int j = 0; j < l; j++) {
            if (!visited[i][j]) {
                char c = M[i][j];
                DFS(M, i, j, c, n, l);
                connectedComp++;
            }
        }
    }

    return connectedComp;
}

// Driver code
int main()
{
    string M[] = {"aabba", "aabba", "aaaca"};
    int n = sizeof(M)/sizeof(M[0]);

    cout << connectedComponents(M, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
static final int maxRow = 500;
static final int maxCol = 500;

static boolean visited[][] = new boolean[maxRow][maxCol];

// Function that return true if mat[row][col]
// is valid and hasn't been visited
static boolean isSafe(String M[], int row, int col,
                                  char c, int n, int l)
{
    // If row and column are valid and element
    // is matched and hasn't been visited then
    // the cell is safe
    return (row >= 0 && row < n) &&
           (col >= 0 && col < l) &&
           (M[row].charAt(col) == c &&
           !visited[row][col]);
}

// Function for depth first search
static void DFS(String M[], int row, int col,
                        char c, int n, int l)
{
    // These arrays are used to get row and column
    // numbers of 4 neighbours of a given cell
    int rowNbr[] = {-1, 1, 0, 0};
    int colNbr[] = {0, 0, 1, -1};

    // Mark this cell as visited
    visited[row][col] = true;

    // Recur for all connected neighbours
    for (int k = 0; k < 4; ++k)
    {
        if (isSafe(M, row + rowNbr[k],
                      col + colNbr[k], c, n, l))
        {
            DFS(M, row + rowNbr[k],
                   col + colNbr[k], c, n, l);
        }
    }
}

// Function to return the number of
// connectewd components in the matrix
static int connectedComponents(String M[], int n)
{
    int connectedComp = 0;
    int l = M[0].length();

    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < l; j++)
        {
            if (!visited[i][j])
            {
                char c = M[i].charAt(j);
                DFS(M, i, j, c, n, l);
                connectedComp++;
            }
        }
    }

    return connectedComp;
}

// Driver code
public static void main(String[] args)
{
    String M[] = {"aabba", "aabba", "aaaca"};
    int n = M.length;
    System.out.println(connectedComponents(M, n));
}
}

// This code contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import numpy as np

maxRow = 500
maxCol = 500

visited = np.zeros((maxCol, maxRow))

# Function that return true if mat[row][col]
# is valid and hasn't been visited
def isSafe(M, row, col, c, n, l) :

    # If row and column are valid and element
    # is matched and hasn't been visited then
    # the cell is safe
    return ((row >= 0 and row < n) and
            (col >= 0 and col < l) and
            (M[row][col] == c and not
             visited[row][col]));

# Function for depth first search
def DFS(M, row, col, c, n, l) :

    # These arrays are used to get row
    # and column numbers of 4 neighbours
    # of a given cell
    rowNbr = [ -1, 1, 0, 0 ];
    colNbr = [ 0, 0, 1, -1 ];

    # Mark this cell as visited
    visited[row][col] = True;

    # Recur for all connected neighbours
    for k in range(4) :
        if (isSafe(M, row + rowNbr[k],
                   col + colNbr[k], c, n, l)) :

            DFS(M, row + rowNbr[k],
                col + colNbr[k], c, n, l);

# Function to return the number of
# connectewd components in the matrix
def connectedComponents(M, n) :

    connectedComp = 0;
    l = len(M[0]);

    for i in range(n) :
        for j in range(l) :
            if (not visited[i][j]) :
                c = M[i][j];
                DFS(M, i, j, c, n, l);
                connectedComp += 1;

    return connectedComp;

# Driver code
if __name__ == "__main__" :

    M = ["aabba", "aabba", "aaaca"];
    n = len(M)

    print(connectedComponents(M, n));

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

static readonly int maxRow = 500;
static readonly int maxCol = 500;

static bool [,]visited = new bool[maxRow,maxCol];

// Function that return true if mat[row,col]
// is valid and hasn't been visited
static bool isSafe(String []M, int row, int col,
                                char c, int n, int l)
{
    // If row and column are valid and element
    // is matched and hasn't been visited then
    // the cell is safe
    return (row >= 0 && row < n) &&
        (col >= 0 && col < l) &&
        (M[row][col] == c &&
        !visited[row,col]);
}

// Function for depth first search
static void DFS(String []M, int row, int col,
                        char c, int n, int l)
{
    // These arrays are used to get row and column
    // numbers of 4 neighbours of a given cell
    int []rowNbr = {-1, 1, 0, 0};
    int []colNbr = {0, 0, 1, -1};

    // Mark this cell as visited
    visited[row,col] = true;

    // Recur for all connected neighbours
    for (int k = 0; k < 4; ++k)
    {
        if (isSafe(M, row + rowNbr[k],
                    col + colNbr[k], c, n, l))
        {
            DFS(M, row + rowNbr[k],
                col + colNbr[k], c, n, l);
        }
    }
}

// Function to return the number of
// connectewd components in the matrix
static int connectedComponents(String []M, int n)
{
    int connectedComp = 0;
    int l = M[0].Length;

    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < l; j++)
        {
            if (!visited[i,j])
            {
                char c = M[i][j];
                DFS(M, i, j, c, n, l);
                connectedComp++;
            }
        }
    }

    return connectedComp;
}

// Driver code
public static void Main(String[] args)
{
    String []M = {"aabba", "aabba", "aaaca"};
    int n = M.Length;
    Console.WriteLine(connectedComponents(M, n));
}
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

      var maxRow = 500;
      var maxCol = 500;

    var visited =
    Array(maxRow).fill().map(()=>Array(maxCol).fill(false));

    // Function that return true if mat[row][col]
    // is valid and hasn't been visited
    function isSafe( M , row , col,  c , n , l) {
        // If row and column are valid and element
        // is matched and hasn't been visited then
        // the cell is safe
        return (row >= 0 && row < n) &&
        (col >= 0 && col < l) && (M[row].charAt(col) == c
        && !visited[row][col]);
    }

    // Function for depth first search
    function DFS( M , row , col,  c , n , l) {
        // These arrays are used to get row and column
        // numbers of 4 neighbours of a given cell
        var rowNbr = [ -1, 1, 0, 0 ];
        var colNbr = [ 0, 0, 1, -1 ];

        // Mark this cell as visited
        visited[row][col] = true;

        // Recur for all connected neighbours
        for (var k = 0; k < 4; ++k) {
            if (isSafe(M, row + rowNbr[k], col +
            colNbr[k], c, n, l))
            {
                DFS(M, row + rowNbr[k], col +
                colNbr[k], c, n, l);
            }
        }
    }

    // Function to return the number of
    // connectewd components in the matrix
    function connectedComponents( M , n) {
        var connectedComp = 0;
        var l = M[0].length;

        for (var i = 0; i < n; i++) {
            for (j = 0; j < l; j++) {
                if (!visited[i][j]) {
                    var c = M[i].charAt(j);
                    DFS(M, i, j, c, n, l);
                    connectedComp++;
                }
            }
        }

        return connectedComp;
    }

    // Driver code

        var M = [ "aabba", "aabba", "aaaca" ];
        var n = M.length;
        document.write(connectedComponents(M, n));

// This code contributed by gauravrajput1

</script>
```

**Output:** 

```
4
```

**时间复杂度:** O(行*列)
T3】辅助空间: O(行*列)