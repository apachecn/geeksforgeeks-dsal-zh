# 在有地雷的道路上寻找最短的安全路线

> 原文:[https://www . geeksforgeeks . org/find-最短安全路径中有地雷/](https://www.geeksforgeeks.org/find-shortest-safe-route-in-a-path-with-landmines/)

给定一个矩形矩阵形式的路径，其中任意放置的地雷很少(标记为 0)，计算从矩阵第一列的任何单元到最后一列的任何单元的最短安全路径的长度。我们必须避开地雷及其四个相邻的牢房(左、右、上、下)，因为它们也不安全。我们只被允许移动到邻近的非地雷的牢房。即路线不能包含任何对角线移动。

示例:

```
Input: 
A 12 x 10 matrix with landmines marked as 0

[ 1  1  1  1  1  1  1  1  1  1 ]
[ 1  0  1  1  1  1  1  1  1  1 ]
[ 1  1  1  0  1  1  1  1  1  1 ]
[ 1  1  1  1  0  1  1  1  1  1 ]
[ 1  1  1  1  1  1  1  1  1  1 ]
[ 1  1  1  1  1  0  1  1  1  1 ]
[ 1  0  1  1  1  1  1  1  0  1 ]
[ 1  1  1  1  1  1  1  1  1  1 ]
[ 1  1  1  1  1  1  1  1  1  1 ]
[ 0  1  1  1  1  0  1  1  1  1 ]
[ 1  1  1  1  1  1  1  1  1  1 ]
[ 1  1  1  0  1  1  1  1  1  1 ]

Output:  
Length of shortest safe route is 13 (Highlighted in Bold)
```

这个想法是使用回溯。我们首先将地雷的所有相邻单元标记为不安全。然后，对于矩阵第一列的每个安全单元，我们在所有允许的方向上向前移动，并递归检查它们是否通向目的地。如果找到了目的地，我们就更新最短路径的值，否则，如果上述解决方案都不起作用，我们就从函数中返回 false。

以下是上述想法的实施–

## C++

```
// C++ program to find shortest safe Route in
// the matrix with landmines
#include <bits/stdc++.h>
using namespace std;
#define R 12
#define C 10

// These arrays are used to get row and column
// numbers of 4 neighbours of a given cell
int rowNum[] = { -1, 0, 0, 1 };
int colNum[] = { 0, -1, 1, 0 };

// A function to check if a given cell (x, y)
// can be visited or not
bool isSafe(int mat[R][C], int visited[R][C],
            int x, int y)
{
    if (mat[x][y] == 0 || visited[x][y])
        return false;

    return true;
}

// A function to check if a given cell (x, y) is
// a valid cell or not
bool isValid(int x, int y)
{
    if (x < R && y < C && x >= 0 && y >= 0)
        return true;

    return false;
}

// A function to mark all adjacent cells of
// landmines as unsafe. Landmines are shown with
// number 0
void markUnsafeCells(int mat[R][C])
{
    for (int i = 0; i < R; i++)
    {
        for (int j = 0; j < C; j++)
        {
            // if a landmines is found
            if (mat[i][j] == 0)
            {
              // mark all adjacent cells
              for (int k = 0; k < 4; k++)
                if (isValid(i + rowNum[k], j + colNum[k]))
                    mat[i + rowNum[k]][j + colNum[k]] = -1;
            }
        }
    }

    // mark all found adjacent cells as unsafe
    for (int i = 0; i < R; i++)
    {
        for (int j = 0; j < C; j++)
        {
            if (mat[i][j] == -1)
                mat[i][j] = 0;
        }
    }

    // Uncomment below lines to print the path
    /*for (int i = 0; i < R; i++)
    {
        for (int j = 0; j < C; j++)
        {
            cout << std::setw(3) << mat[i][j];
        }
        cout << endl;
    }*/
}

// Function to find shortest safe Route in the
// matrix with landmines
// mat[][] - binary input matrix with safe cells marked as 1
// visited[][] - store info about cells already visited in
// current route
// (i, j) are coordinates of the current cell
// min_dist --> stores minimum cost of shortest path so far
// dist --> stores current path cost
void findShortestPathUtil(int mat[R][C], int visited[R][C],
                          int i, int j, int &min_dist, int dist)
{
    // if destination is reached
    if (j == C-1)
    {
        // update shortest path found so far
        min_dist = min(dist, min_dist);
        return;
    }

    // if current path cost exceeds minimum so far
    if (dist > min_dist)
        return;

    // include (i, j) in current path
    visited[i][j] = 1;

    // Recurse for all safe adjacent neighbours
    for (int k = 0; k < 4; k++)
    {
        if (isValid(i + rowNum[k], j + colNum[k]) &&
            isSafe(mat, visited, i + rowNum[k], j + colNum[k]))
        {
            findShortestPathUtil(mat, visited, i + rowNum[k],
                           j + colNum[k], min_dist, dist + 1);
        }
    }

    // Backtrack
    visited[i][j] = 0;
}

// A wrapper function over findshortestPathUtil()
void findShortestPath(int mat[R][C])
{
    // stores minimum cost of shortest path so far
    int min_dist = INT_MAX;

    // create a boolean matrix to store info about
    // cells already visited in current route
    int visited[R][C];

    // mark adjacent cells of landmines as unsafe
    markUnsafeCells(mat);

    // start from first column and take minimum
    for (int i = 0; i < R; i++)
    {
        // if path is safe from current cell
        if (mat[i][0] == 1)
        {
            // initialize visited to false
            memset(visited, 0, sizeof visited);

            // find shortest route from (i, 0) to any
            // cell of last column (x, C - 1) where
            // 0 <= x < R
            findShortestPathUtil(mat, visited, i, 0,
                                 min_dist, 0);

            // if min distance is already found
            if(min_dist == C - 1)
                break;
        }
    }

    // if destination can be reached
    if (min_dist != INT_MAX)
        cout << "Length of shortest safe route is "
             << min_dist;

    else // if the destination is not reachable
        cout << "Destination not reachable from "
             << "given source";
}

// Driver code
int main()
{
    // input matrix with landmines shown with number 0
    int mat[R][C] =
    {
        { 1, 1, 1, 1, 1, 1, 1, 1, 1, 1 },
        { 1, 0, 1, 1, 1, 1, 1, 1, 1, 1 },
        { 1, 1, 1, 0, 1, 1, 1, 1, 1, 1 },
        { 1, 1, 1, 1, 0, 1, 1, 1, 1, 1 },
        { 1, 1, 1, 1, 1, 1, 1, 1, 1, 1 },
        { 1, 1, 1, 1, 1, 0, 1, 1, 1, 1 },
        { 1, 0, 1, 1, 1, 1, 1, 1, 0, 1 },
        { 1, 1, 1, 1, 1, 1, 1, 1, 1, 1 },
        { 1, 1, 1, 1, 1, 1, 1, 1, 1, 1 },
        { 0, 1, 1, 1, 1, 0, 1, 1, 1, 1 },
        { 1, 1, 1, 1, 1, 1, 1, 1, 1, 1 },
        { 1, 1, 1, 0, 1, 1, 1, 1, 1, 1 }
    };

    // find shortest path
    findShortestPath(mat);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find shortest safe Route
// in the matrix with landmines
import java.util.Arrays;

class GFG{

static final int R = 12;
static final int C = 10;

// These arrays are used to get row and column
// numbers of 4 neighbours of a given cell
static int rowNum[] = { -1, 0, 0, 1 };
static int colNum[] = { 0, -1, 1, 0 };

static int min_dist;

// A function to check if a given cell (x, y)
// can be visited or not
static boolean isSafe(int[][] mat, boolean[][] visited,
                      int x, int y)
{
    if (mat[x][y] == 0 || visited[x][y])
        return false;

    return true;
}

// A function to check if a given cell (x, y) is
// a valid cell or not
static boolean isValid(int x, int y)
{
    if (x < R && y < C && x >= 0 && y >= 0)
        return true;

    return false;
}

// A function to mark all adjacent cells of
// landmines as unsafe. Landmines are shown with
// number 0
static void markUnsafeCells(int[][] mat)
{
    for(int i = 0; i < R; i++)
    {
        for(int j = 0; j < C; j++)
        {

            // If a landmines is found
            if (mat[i][j] == 0)
            {

                // Mark all adjacent cells
                for(int k = 0; k < 4; k++)
                    if (isValid(i + rowNum[k], j + colNum[k]))
                        mat[i + rowNum[k]][j + colNum[k]] = -1;
            }
        }
    }

    // Mark all found adjacent cells as unsafe
    for(int i = 0; i < R; i++)
    {
        for(int j = 0; j < C; j++)
        {
            if (mat[i][j] == -1)
                mat[i][j] = 0;
        }
    }

    // Uncomment below lines to print the path
    /*
     * for (int i = 0; i < R; i++) {
     * for (int j = 0; j < C; j++) { cout <<
     * std::setw(3) << mat[i][j]; } cout << endl; }
     */
}

// Function to find shortest safe Route in the
// matrix with landmines
// mat[][] - binary input matrix with safe cells marked as 1
// visited[][] - store info about cells already visited in
// current route
// (i, j) are coordinates of the current cell
// min_dist --> stores minimum cost of shortest path so far
// dist --> stores current path cost
static void findShortestPathUtil(int[][] mat,
                                 boolean[][] visited,
                                 int i, int j, int dist)
{

    // If destination is reached
    if (j == C - 1)
    {

        // Update shortest path found so far
        min_dist = Math.min(dist, min_dist);
        return;
    }

    // If current path cost exceeds minimum so far
    if (dist > min_dist)
        return;

    // include (i, j) in current path
    visited[i][j] = true;

    // Recurse for all safe adjacent neighbours
    for(int k = 0; k < 4; k++)
    {
        if (isValid(i + rowNum[k], j + colNum[k]) &&
            isSafe(mat, visited, i + rowNum[k],
                                 j + colNum[k]))
        {
            findShortestPathUtil(mat, visited, i + rowNum[k],
                             j + colNum[k], dist + 1);
        }
    }

    // Backtrack
    visited[i][j] = false;
}

// A wrapper function over findshortestPathUtil()
static void findShortestPath(int[][] mat)
{

    // Stores minimum cost of shortest path so far
    min_dist = Integer.MAX_VALUE;

    // Create a boolean matrix to store info about
    // cells already visited in current route
    boolean[][] visited = new boolean[R][C];

    // Mark adjacent cells of landmines as unsafe
    markUnsafeCells(mat);

    // Start from first column and take minimum
    for(int i = 0; i < R; i++)
    {

        // If path is safe from current cell
        if (mat[i][0] == 1)
        {

            // Initialize visited to false
            for(int k = 0; k < R; k++)
            {
                Arrays.fill(visited[k], false);
            }

            // Find shortest route from (i, 0) to any
            // cell of last column (x, C - 1) where
            // 0 <= x < R
            findShortestPathUtil(mat, visited, i, 0, 0);

            // If min distance is already found
            if (min_dist == C - 1)
                break;
        }
    }

    // If destination can be reached
    if (min_dist != Integer.MAX_VALUE)
        System.out.println("Length of shortest " +
                           "safe route is " + min_dist);

    else

        // If the destination is not reachable
        System.out.println("Destination not " +
                           "reachable from given source");
}

// Driver code
public static void main(String[] args)
{

    // Input matrix with landmines shown with number 0
    int[][] mat = {
        { 1, 1, 1, 1, 1, 1, 1, 1, 1, 1 },
        { 1, 0, 1, 1, 1, 1, 1, 1, 1, 1 },
        { 1, 1, 1, 0, 1, 1, 1, 1, 1, 1 },
        { 1, 1, 1, 1, 0, 1, 1, 1, 1, 1 },
        { 1, 1, 1, 1, 1, 1, 1, 1, 1, 1 },
        { 1, 1, 1, 1, 1, 0, 1, 1, 1, 1 },
        { 1, 0, 1, 1, 1, 1, 1, 1, 0, 1 },
        { 1, 1, 1, 1, 1, 1, 1, 1, 1, 1 },
        { 1, 1, 1, 1, 1, 1, 1, 1, 1, 1 },
        { 0, 1, 1, 1, 1, 0, 1, 1, 1, 1 },
        { 1, 1, 1, 1, 1, 1, 1, 1, 1, 1 },
        { 1, 1, 1, 0, 1, 1, 1, 1, 1, 1 } };

    // Find shortest path
    findShortestPath(mat);
}
}

// This code is contributed by sanjeev2552
```

## 蟒蛇 3

```
# Python3 program to find shortest safe Route
# in the matrix with landmines
import sys

R = 12
C = 10

# These arrays are used to get row and column
# numbers of 4 neighbours of a given cell
rowNum = [ -1, 0, 0, 1 ]
colNum = [ 0, -1, 1, 0 ]

min_dist = sys.maxsize

# A function to check if a given cell (x, y)
# can be visited or not
def isSafe(mat, visited, x, y):

    if (mat[x][y] == 0 or visited[x][y]):
        return False

    return True

# A function to check if a given cell (x, y) is
# a valid cell or not
def isValid(x, y):

    if (x < R and y < C and x >= 0 and y >= 0):
        return True

    return False

# A function to mark all adjacent cells of
# landmines as unsafe. Landmines are shown with
# number 0
def markUnsafeCells(mat):

    for i in range(R):
        for j in range(C):
            # If a landmines is found
            if (mat[i][j] == 0):
                # Mark all adjacent cells
                for k in range(4):
                    if (isValid(i + rowNum[k], j + colNum[k])):
                        mat[i + rowNum[k]][j + colNum[k]] = -1

    # Mark all found adjacent cells as unsafe
    for i in range(R):
        for j in range(C):
            if (mat[i][j] == -1):
                mat[i][j] = 0

    """ Uncomment below lines to print the path
    /*
     * for (int i = 0; i < R; i++) {
     * for (int j = 0; j < C; j++) { cout <<
     * std::setw(3) << mat[i][j]; } cout << endl; }
     *"""

# Function to find shortest safe Route in the
# matrix with landmines
# mat[][] - binary input matrix with safe cells marked as 1
# visited[][] - store info about cells already visited in
# current route
# (i, j) are coordinates of the current cell
# min_dist --> stores minimum cost of shortest path so far
# dist --> stores current path cost
def findShortestPathUtil(mat, visited, i, j, dist):

    global min_dist

    # If destination is reached
    if (j == C - 1):
        # Update shortest path found so far
        min_dist = min(dist, min_dist)
        return

    # If current path cost exceeds minimum so far
    if (dist > min_dist):
        return

    # include (i, j) in current path
    visited[i][j] = True

    # Recurse for all safe adjacent neighbours
    for k in range(4):
        if (isValid(i + rowNum[k], j + colNum[k]) and isSafe(mat, visited, i + rowNum[k], j + colNum[k])):
            findShortestPathUtil(mat, visited, i + rowNum[k], j + colNum[k], dist + 1)

    # Backtrack
    visited[i][j] = False

# A wrapper function over findshortestPathUtil()
def findShortestPath(mat):

    global min_dist

    # Stores minimum cost of shortest path so far
    min_dist = sys.maxsize

    # Create a boolean matrix to store info about
    # cells already visited in current route
    visited = [[False for i in range(C)] for j in range(R)]

    # Mark adjacent cells of landmines as unsafe
    markUnsafeCells(mat)

    # Start from first column and take minimum
    for i in range(R):
        # If path is safe from current cell
        if (mat[i][0] == 1):
            # Find shortest route from (i, 0) to any
            # cell of last column (x, C - 1) where
            # 0 <= x < R
            findShortestPathUtil(mat, visited, i, 0, 0)

            # If min distance is already found
            if (min_dist == C - 1):
                break

    # If destination can be reached
    if (min_dist != sys.maxsize):
        print("Length of shortest safe route is", min_dist)
    else:
        # If the destination is not reachable
        print("Destination not reachable from given source")

mat = [
        [ 1, 1, 1, 1, 1, 1, 1, 1, 1, 1 ],
        [ 1, 0, 1, 1, 1, 1, 1, 1, 1, 1 ],
        [ 1, 1, 1, 0, 1, 1, 1, 1, 1, 1 ],
        [ 1, 1, 1, 1, 0, 1, 1, 1, 1, 1 ],
        [ 1, 1, 1, 1, 1, 1, 1, 1, 1, 1 ],
        [ 1, 1, 1, 1, 1, 0, 1, 1, 1, 1 ],
        [ 1, 0, 1, 1, 1, 1, 1, 1, 0, 1 ],
        [ 1, 1, 1, 1, 1, 1, 1, 1, 1, 1 ],
        [ 1, 1, 1, 1, 1, 1, 1, 1, 1, 1 ],
        [ 0, 1, 1, 1, 1, 0, 1, 1, 1, 1 ],
        [ 1, 1, 1, 1, 1, 1, 1, 1, 1, 1 ],
        [ 1, 1, 1, 0, 1, 1, 1, 1, 1, 1 ] ]

# Find shortest path
findShortestPath(mat)

# This code is contributed by mukesh07.
```

## C#

```
// C# program to find shortest safe Route
// in the matrix with landmines
using System;
using System.Collections.Generic;
class GFG {

    static int R = 12;
    static int C = 10;

    // These arrays are used to get row and column
    // numbers of 4 neighbours of a given cell
    static int[] rowNum = { -1, 0, 0, 1 };
    static int[] colNum = { 0, -1, 1, 0 };

    static int min_dist;

    // A function to check if a given cell (x, y)
    // can be visited or not
    static bool isSafe(int[,] mat, bool[,] visited, int x, int y)
    {
        if (mat[x,y] == 0 || visited[x,y])
            return false;

        return true;
    }

    // A function to check if a given cell (x, y) is
    // a valid cell or not
    static bool isValid(int x, int y)
    {
        if (x < R && y < C && x >= 0 && y >= 0)
            return true;

        return false;
    }

    // A function to mark all adjacent cells of
    // landmines as unsafe. Landmines are shown with
    // number 0
    static void markUnsafeCells(int[,] mat)
    {
        for(int i = 0; i < R; i++)
        {
            for(int j = 0; j < C; j++)
            {

                // If a landmines is found
                if (mat[i,j] == 0)
                {

                    // Mark all adjacent cells
                    for(int k = 0; k < 4; k++)
                        if (isValid(i + rowNum[k], j + colNum[k]))
                            mat[i + rowNum[k],j + colNum[k]] = -1;
                }
            }
        }

        // Mark all found adjacent cells as unsafe
        for(int i = 0; i < R; i++)
        {
            for(int j = 0; j < C; j++)
            {
                if (mat[i,j] == -1)
                    mat[i,j] = 0;
            }
        }

        // Uncomment below lines to print the path
        /*
         * for (int i = 0; i < R; i++) {
         * for (int j = 0; j < C; j++) { cout <<
         * std::setw(3) << mat[i][j]; } cout << endl; }
         */
    }

    // Function to find shortest safe Route in the
    // matrix with landmines
    // mat[][] - binary input matrix with safe cells marked as 1
    // visited[][] - store info about cells already visited in
    // current route
    // (i, j) are coordinates of the current cell
    // min_dist --> stores minimum cost of shortest path so far
    // dist --> stores current path cost
    static void findShortestPathUtil(int[,] mat,
                                     bool[,] visited,
                                     int i, int j, int dist)
    {

        // If destination is reached
        if (j == C - 1)
        {

            // Update shortest path found so far
            min_dist = Math.Min(dist, min_dist);
            return;
        }

        // If current path cost exceeds minimum so far
        if (dist > min_dist)
            return;

        // include (i, j) in current path
        visited[i,j] = true;

        // Recurse for all safe adjacent neighbours
        for(int k = 0; k < 4; k++)
        {
            if (isValid(i + rowNum[k], j + colNum[k]) &&
                isSafe(mat, visited, i + rowNum[k], j + colNum[k]))
            {
                findShortestPathUtil(mat, visited, i + rowNum[k], j + colNum[k], dist + 1);
            }
        }

        // Backtrack
        visited[i,j] = false;
    }

    // A wrapper function over findshortestPathUtil()
    static void findShortestPath(int[,] mat)
    {

        // Stores minimum cost of shortest path so far
        min_dist = Int32.MaxValue;

        // Create a boolean matrix to store info about
        // cells already visited in current route
        bool[,] visited = new bool[R,C];

        // Mark adjacent cells of landmines as unsafe
        markUnsafeCells(mat);

        // Start from first column and take minimum
        for(int i = 0; i < R; i++)
        {

            // If path is safe from current cell
            if (mat[i,0] == 1)
            {
                // Find shortest route from (i, 0) to any
                // cell of last column (x, C - 1) where
                // 0 <= x < R
                findShortestPathUtil(mat, visited, i, 0, 0);

                // If min distance is already found
                if (min_dist == C - 1)
                    break;
            }
        }

        // If destination can be reached
        if (min_dist != Int32.MaxValue)
            Console.WriteLine("Length of shortest " +
                               "safe route is " + min_dist);

        else

            // If the destination is not reachable
            Console.WriteLine("Destination not " +
                               "reachable from given source");
    }

  static void Main()
  {

    // Input matrix with landmines shown with number 0
    int[,] mat = {
        { 1, 1, 1, 1, 1, 1, 1, 1, 1, 1 },
        { 1, 0, 1, 1, 1, 1, 1, 1, 1, 1 },
        { 1, 1, 1, 0, 1, 1, 1, 1, 1, 1 },
        { 1, 1, 1, 1, 0, 1, 1, 1, 1, 1 },
        { 1, 1, 1, 1, 1, 1, 1, 1, 1, 1 },
        { 1, 1, 1, 1, 1, 0, 1, 1, 1, 1 },
        { 1, 0, 1, 1, 1, 1, 1, 1, 0, 1 },
        { 1, 1, 1, 1, 1, 1, 1, 1, 1, 1 },
        { 1, 1, 1, 1, 1, 1, 1, 1, 1, 1 },
        { 0, 1, 1, 1, 1, 0, 1, 1, 1, 1 },
        { 1, 1, 1, 1, 1, 1, 1, 1, 1, 1 },
        { 1, 1, 1, 0, 1, 1, 1, 1, 1, 1 } };

    // Find shortest path
    findShortestPath(mat);
  }
}

// This code is contributed by rameshtravel07.
```

## java 描述语言

```
<script>
    // Javascript program to find shortest safe Route
    // in the matrix with landmines

    let R = 12;
    let C = 10;

    // These arrays are used to get row and column
    // numbers of 4 neighbours of a given cell
    let rowNum = [ -1, 0, 0, 1 ];
    let colNum = [ 0, -1, 1, 0 ];

    let min_dist;

    // A function to check if a given cell (x, y)
    // can be visited or not
    function isSafe(mat, visited, x, y)
    {
        if (mat[x][y] == 0 || visited[x][y])
            return false;

        return true;
    }

    // A function to check if a given cell (x, y) is
    // a valid cell or not
    function isValid(x, y)
    {
        if (x < R && y < C && x >= 0 && y >= 0)
            return true;

        return false;
    }

    // A function to mark all adjacent cells of
    // landmines as unsafe. Landmines are shown with
    // number 0
    function markUnsafeCells(mat)
    {
        for(let i = 0; i < R; i++)
        {
            for(let j = 0; j < C; j++)
            {

                // If a landmines is found
                if (mat[i][j] == 0)
                {

                    // Mark all adjacent cells
                    for(let k = 0; k < 4; k++)
                        if (isValid(i + rowNum[k], j + colNum[k]))
                            mat[i + rowNum[k]][j + colNum[k]] = -1;
                }
            }
        }

        // Mark all found adjacent cells as unsafe
        for(let i = 0; i < R; i++)
        {
            for(let j = 0; j < C; j++)
            {
                if (mat[i][j] == -1)
                    mat[i][j] = 0;
            }
        }

        // Uncomment below lines to print the path
        /*
         * for (int i = 0; i < R; i++) {
         * for (int j = 0; j < C; j++) { cout <<
         * std::setw(3) << mat[i][j]; } cout << endl; }
         */
    }

    // Function to find shortest safe Route in the
    // matrix with landmines
    // mat[][] - binary input matrix with safe cells marked as 1
    // visited[][] - store info about cells already visited in
    // current route
    // (i, j) are coordinates of the current cell
    // min_dist --> stores minimum cost of shortest path so far
    // dist --> stores current path cost
    function findShortestPathUtil(mat, visited, i, j, dist)
    {

        // If destination is reached
        if (j == C - 1)
        {

            // Update shortest path found so far
            min_dist = Math.min(dist, min_dist);
            return;
        }

        // If current path cost exceeds minimum so far
        if (dist > min_dist)
            return;

        // include (i, j) in current path
        visited[i][j] = true;

        // Recurse for all safe adjacent neighbours
        for(let k = 0; k < 4; k++)
        {
            if (isValid(i + rowNum[k], j + colNum[k]) &&
                isSafe(mat, visited, i + rowNum[k],
                                     j + colNum[k]))
            {
                findShortestPathUtil(mat, visited, i + rowNum[k],
                                 j + colNum[k], dist + 1);
            }
        }

        // Backtrack
        visited[i][j] = false;
    }

    // A wrapper function over findshortestPathUtil()
    function findShortestPath(mat)
    {

        // Stores minimum cost of shortest path so far
        min_dist = Number.MAX_VALUE;

        // Create a boolean matrix to store info about
        // cells already visited in current route
        let visited = new Array(R);

        for(let i = 0; i < R; i++)
        {
            visited[i] = new Array(C);
            for(let j = 0; j < C; j++)
            {
                visited[i][j] = false;
            }
        }

        // Mark adjacent cells of landmines as unsafe
        markUnsafeCells(mat);

        // Start from first column and take minimum
        for(let i = 0; i < R; i++)
        {
            // If path is safe from current cell
            if (mat[i][0] == 1)
            {

                // Find shortest route from (i, 0) to any
                // cell of last column (x, C - 1) where
                // 0 <= x < R
                findShortestPathUtil(mat, visited, i, 0, 0);

                // If min distance is already found
                if (min_dist == C - 1)
                    break;
            }
        }

        // If destination can be reached
        if (min_dist != Number.MAX_VALUE)
            document.write("Length of shortest " +
                               "safe route is " + min_dist + "</br>");

        else

            // If the destination is not reachable
            document.write("Destination not " +
                               "reachable from given source" + "</br>");
    }

    // Input matrix with landmines shown with number 0
    let mat = [
        [ 1, 1, 1, 1, 1, 1, 1, 1, 1, 1 ],
        [ 1, 0, 1, 1, 1, 1, 1, 1, 1, 1 ],
        [ 1, 1, 1, 0, 1, 1, 1, 1, 1, 1 ],
        [ 1, 1, 1, 1, 0, 1, 1, 1, 1, 1 ],
        [ 1, 1, 1, 1, 1, 1, 1, 1, 1, 1 ],
        [ 1, 1, 1, 1, 1, 0, 1, 1, 1, 1 ],
        [ 1, 0, 1, 1, 1, 1, 1, 1, 0, 1 ],
        [ 1, 1, 1, 1, 1, 1, 1, 1, 1, 1 ],
        [ 1, 1, 1, 1, 1, 1, 1, 1, 1, 1 ],
        [ 0, 1, 1, 1, 1, 0, 1, 1, 1, 1 ],
        [ 1, 1, 1, 1, 1, 1, 1, 1, 1, 1 ],
        [ 1, 1, 1, 0, 1, 1, 1, 1, 1, 1 ] ];

    // Find shortest path
    findShortestPath(mat);

// This code is contributed by decode2207.
</script>
```

**输出:**

```
Length of shortest safe route is 13
```

**另一种方法:**借助广度优先搜索可以多项式时间求解。将距离为 0 的队列中值为 1 的单元格入队。随着 BFS 进程的进行，计算从第一列到每个单元的最短路径。最后对于最后一列的可达单元格，输出最小距离。

C++中的实现如下:

## C++

```
// C++ program to find shortest safe Route in
// the matrix with landmines
#include <bits/stdc++.h>
using namespace std;

#define R 12
#define C 10

struct Key{
    int x,y;
    Key(int i,int j){ x=i;y=j;};
};

// These arrays are used to get row and column
// numbers of 4 neighbours of a given cell
int rowNum[] = { -1, 0, 0, 1 };
int colNum[] = { 0, -1, 1, 0 };

// A function to check if a given cell (x, y) is
// a valid cell or not
bool isValid(int x, int y)
{
    if (x < R && y < C && x >= 0 && y >= 0)
        return true;

    return false;
}

// A function to mark all adjacent cells of
// landmines as unsafe. Landmines are shown with
// number 0
void findShortestPath(int mat[R][C]){
    int i,j;

    for (i = 0; i < R; i++)
    {
        for (j = 0; j < C; j++)
        {
            // if a landmines is found
            if (mat[i][j] == 0)
            {
            // mark all adjacent cells
            for (int k = 0; k < 4; k++)
                if (isValid(i + rowNum[k], j + colNum[k]))
                    mat[i + rowNum[k]][j + colNum[k]] = -1;
            }
        }
    }
// mark all found adjacent cells as unsafe
    for (i = 0; i < R; i++)
    {
        for (j = 0; j < C; j++)
        {
            if (mat[i][j] == -1)
                mat[i][j] = 0;
        }
    }

    int dist[R][C];

    for(i=0;i<R;i++){
        for(j=0;j<C;j++)
            dist[i][j] = -1;
    }
    queue<Key> q;

    for(i=0;i<R;i++){
        if(mat[i][0] == 1){
            q.push(Key(i,0));
            dist[i][0] = 0;
        }
    }

    while(!q.empty()){
        Key k = q.front();
        q.pop();

        int d = dist[k.x][k.y];

        int x = k.x;
        int y = k.y;

        for (int k = 0; k < 4; k++) {
            int xp = x + rowNum[k];
            int yp = y + colNum[k];
            if(isValid(xp,yp) && dist[xp][yp] == -1 && mat[xp][yp] == 1){
                dist[xp][yp] = d+1;
                q.push(Key(xp,yp));
            }
        }
    }
    // stores minimum cost of shortest path so far
    int ans = INT_MAX;
    // start from first column and take minimum
    for(i=0;i<R;i++){
        if(mat[i][C-1] == 1 && dist[i][C-1] != -1){
            ans = min(ans,dist[i][C-1]);
        }
    }

    // if destination can be reached
    if(ans == INT_MAX)
        cout << "NOT POSSIBLE\n";

    else// if the destination is not reachable
        cout << "Length of shortest safe route is " << ans << endl;
}

// Driver code
int main(){

    // input matrix with landmines shown with number 0
    int mat[R][C] =
    {
        { 1, 1, 1, 1, 1, 1, 1, 1, 1, 1 },
        { 1, 0, 1, 1, 1, 1, 1, 1, 1, 1 },
        { 1, 1, 1, 0, 1, 1, 1, 1, 1, 1 },
        { 1, 1, 1, 1, 0, 1, 1, 1, 1, 1 },
        { 1, 1, 1, 1, 1, 1, 1, 1, 1, 1 },
        { 1, 1, 1, 1, 1, 0, 1, 1, 1, 1 },
        { 1, 0, 1, 1, 1, 1, 1, 1, 0, 1 },
        { 1, 1, 1, 1, 1, 1, 1, 1, 1, 1 },
        { 1, 1, 1, 1, 1, 1, 1, 1, 1, 1 },
        { 0, 1, 1, 1, 1, 0, 1, 1, 1, 1 },
        { 1, 1, 1, 1, 1, 1, 1, 1, 1, 1 },
        { 1, 1, 1, 0, 1, 1, 1, 1, 1, 1 }
    };

    // find shortest path
    findShortestPath(mat);
}
```

**输出:**

```
Length of shortest safe route is 13
```

本文由**阿迪蒂亚·戈尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。