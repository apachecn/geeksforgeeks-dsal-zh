# 计算迷宫中到达目的地的路数

> 原文:[https://www . geesforgeks . org/count-迷宫中到达目的地的路数/](https://www.geeksforgeeks.org/count-number-of-ways-to-reach-destination-in-a-maze/)

给定一个由 0 和-1 单元格组成的迷宫，任务是找到从(0，0)到(n-1，m-1)的所有路径，并且每条路径都应该穿过至少一个包含-1 的单元格。从一个给定的单元格，我们只能移动到单元格(i+1，j)和(I，j+1)。
这个问题是[这里](https://www.geeksforgeeks.org/count-number-ways-reach-destination-maze/)公布的问题的变种。
**示例:**

> **输入:**迷宫[][] = {
> {0，0，0，0}，
> {0，-1，0，0}，
> {-1，0，0，0}，
> {0，0，0，0}}
> **输出:** 16

**方法:**寻找通过至少一个标记单元(包含-1 的单元)的所有路径。如果我们找到不经过任何标记单元的路径以及从(0，0)到(n-1，m-1)的所有可能路径，那么我们可以找到经过至少一个标记单元的所有路径。
**通过至少一个标记单元格的路径数=(路径总数–不通过任何标记单元格的路径数)**
我们将使用本文中提到的方法来查找不通过任何标记单元格的路径总数，从源到目的地的路径总数将为(m+n–2)！/(n–1)！*(m–1)！其中 m 和 n 是行数和列数。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define R 4
#define C 4

// Function to return the count of possible paths
// in a maze[R][C] from (0, 0) to (R-1, C-1) that
// do not pass through any of the marked cells
int countPaths(int maze[][C])
{
    // If the initial cell is blocked, there is no
    // way of moving anywhere
    if (maze[0][0] == -1)
        return 0;

    // Initializing the leftmost column
    for (int i = 0; i < R; i++) {
        if (maze[i][0] == 0)
            maze[i][0] = 1;

        // If we encounter a blocked cell in leftmost
        // row, there is no way of visiting any cell
        // directly below it.
        else
            break;
    }

    // Similarly initialize the topmost row
    for (int i = 1; i < C; i++) {
        if (maze[0][i] == 0)
            maze[0][i] = 1;

        // If we encounter a blocked cell in bottommost
        // row, there is no way of visiting any cell
        // directly below it.
        else
            break;
    }

    // The only difference is that if a cell is -1,
    // simply ignore it else recursively compute
    // count value maze[i][j]
    for (int i = 1; i < R; i++) {
        for (int j = 1; j < C; j++) {
            // If blockage is found, ignore this cell
            if (maze[i][j] == -1)
                continue;

            // If we can reach maze[i][j] from maze[i-1][j]
            // then increment count.
            if (maze[i - 1][j] > 0)
                maze[i][j] = (maze[i][j] + maze[i - 1][j]);

            // If we can reach maze[i][j] from maze[i][j-1]
            // then increment count.
            if (maze[i][j - 1] > 0)
                maze[i][j] = (maze[i][j] + maze[i][j - 1]);
        }
    }

    // If the final cell is blocked, output 0, otherwise
    // the answer
    return (maze[R - 1][C - 1] > 0) ? maze[R - 1][C - 1] : 0;
}
// Function to return the count of all possible
// paths from (0, 0) to (n - 1, m - 1)
int numberOfPaths(int m, int n)
{
    // We have to calculate m+n-2 C n-1 here
    // which will be (m+n-2)! / (n-1)! (m-1)!
    int path = 1;
    for (int i = n; i < (m + n - 1); i++) {
        path *= i;
        path /= (i - n + 1);
    }
    return path;
}

// Function to return the total count of paths
// from (0, 0) to (n - 1, m - 1) that pass
// through at least one of the marked cells
int solve(int maze[][C])
{

    // Total count of paths - Total paths that do not
    // pass through any of the marked cell
    int ans = numberOfPaths(R, C) - countPaths(maze);

    // return answer
    return ans;
}

// Driver code
int main()
{
    int maze[R][C] = { { 0, 0, 0, 0 },
                       { 0, -1, 0, 0 },
                       { -1, 0, 0, 0 },
                       { 0, 0, 0, 0 } };

    cout << solve(maze);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{
static int R = 4;
static int C = 4;

// Function to return the count of possible paths
// in a maze[R][C] from (0, 0) to (R-1, C-1) that
// do not pass through any of the marked cells
static int countPaths(int maze[][])
{

    // If the initial cell is blocked,
    // there is no way of moving anywhere
    if (maze[0][0] == -1)
        return 0;

    // Initializing the leftmost column
    for (int i = 0; i < R; i++)
    {
        if (maze[i][0] == 0)
            maze[i][0] = 1;

        // If we encounter a blocked cell in leftmost
        // row, there is no way of visiting any cell
        // directly below it.
        else
            break;
    }

    // Similarly initialize the topmost row
    for (int i = 1; i < C; i++)
    {
        if (maze[0][i] == 0)
            maze[0][i] = 1;

        // If we encounter a blocked cell in bottommost
        // row, there is no way of visiting any cell
        // directly below it.
        else
            break;
    }

    // The only difference is that if a cell is -1,
    // simply ignore it else recursively compute
    // count value maze[i][j]
    for (int i = 1; i < R; i++)
    {
        for (int j = 1; j < C; j++)
        {

            // If blockage is found, ignore this cell
            if (maze[i][j] == -1)
                continue;

            // If we can reach maze[i][j] from
            //  maze[i-1][j] then increment count.
            if (maze[i - 1][j] > 0)
                maze[i][j] = (maze[i][j] +
                              maze[i - 1][j]);

            // If we can reach maze[i][j] from
            // maze[i][j-1] then increment count.
            if (maze[i][j - 1] > 0)
                maze[i][j] = (maze[i][j] +
                              maze[i][j - 1]);
        }
    }

    // If the final cell is blocked,
    // output 0, otherwise the answer
    return (maze[R - 1][C - 1] > 0) ?
                 maze[R - 1][C - 1] : 0;
}

// Function to return the count of all possible
// paths from (0, 0) to (n - 1, m - 1)
static int numberOfPaths(int m, int n)
{
    // We have to calculate m+n-2 C n-1 here
    // which will be (m+n-2)! / (n-1)! (m-1)!
    int path = 1;
    for (int i = n; i < (m + n - 1); i++)
    {
        path *= i;
        path /= (i - n + 1);
    }
    return path;
}

// Function to return the total count of paths
// from (0, 0) to (n - 1, m - 1) that pass
// through at least one of the marked cells
static int solve(int maze[][])
{

    // Total count of paths - Total paths that do not
    // pass through any of the marked cell
    int ans = numberOfPaths(R, C) - countPaths(maze);

    // return answer
    return ans;
}

// Driver code
public static void main (String[] args)
{
    int maze[][] = { { 0, 0, 0, 0 },
                     { 0, -1, 0, 0 },
                     { -1, 0, 0, 0 },
                     { 0, 0, 0, 0 } };

    System.out.println(solve(maze));
}
}

// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python3 implementation of the approach
R = 4
C = 4

# Function to return the count of
# possible paths in a maze[R][C]
# from (0, 0) to (R-1, C-1) that
# do not pass through any of
# the marked cells
def countPaths(maze):

    # If the initial cell is blocked,
    # there is no way of moving anywhere
    if (maze[0][0] == -1):
        return 0

    # Initializing the leftmost column
    for i in range(R):
        if (maze[i][0] == 0):
            maze[i][0] = 1

        # If we encounter a blocked cell
        # in leftmost row, there is no way of
        # visiting any cell directly below it.
        else:
            break

    # Similarly initialize the topmost row
    for i in range(1, C):
        if (maze[0][i] == 0):
            maze[0][i] = 1

        # If we encounter a blocked cell in
        # bottommost row, there is no way of
        # visiting any cell directly below it.
        else:
            break

    # The only difference is that if
    # a cell is -1, simply ignore it
    # else recursively compute
    # count value maze[i][j]
    for i in range(1, R):
        for j in range(1, C):

            # If blockage is found,
            # ignore this cell
            if (maze[i][j] == -1):
                continue

            # If we can reach maze[i][j] from
            # maze[i-1][j] then increment count.
            if (maze[i - 1][j] > 0):
                maze[i][j] = (maze[i][j] +
                              maze[i - 1][j])

            # If we can reach maze[i][j] from
            # maze[i][j-1] then increment count.
            if (maze[i][j - 1] > 0):
                maze[i][j] = (maze[i][j] +
                              maze[i][j - 1])

    # If the final cell is blocked,
    # output 0, otherwise the answer
    if (maze[R - 1][C - 1] > 0):
        return maze[R - 1][C - 1]
    else:
        return 0

# Function to return the count of
# all possible paths from
# (0, 0) to (n - 1, m - 1)
def numberOfPaths(m, n):

    # We have to calculate m+n-2 C n-1 here
    # which will be (m+n-2)! / (n-1)! (m-1)!
    path = 1
    for i in range(n, m + n - 1):

        path *= i
        path //= (i - n + 1)

    return path

# Function to return the total count
# of paths from (0, 0) to (n - 1, m - 1)
# that pass through at least one
# of the marked cells
def solve(maze):

    # Total count of paths - Total paths
    # that do not pass through any of
    # the marked cell
    ans = (numberOfPaths(R, C) -
           countPaths(maze))

    # return answer
    return ans

# Driver code
maze = [[ 0, 0, 0, 0 ],
        [ 0, -1, 0, 0 ],
        [ -1, 0, 0, 0 ],
        [ 0, 0, 0, 0 ]]

print(solve(maze))

# This code is contributed
# by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;
class GFG
{
static int R = 4;
static int C = 4;

// Function to return the count of possible paths
// in a maze[R][C] from (0, 0) to (R-1, C-1) that
// do not pass through any of the marked cells
static int countPaths(int [,]maze)
{

    // If the initial cell is blocked,
    // there is no way of moving anywhere
    if (maze[0, 0] == -1)
        return 0;

    // Initializing the leftmost column
    for (int i = 0; i < R; i++)
    {
        if (maze[i, 0] == 0)
            maze[i, 0] = 1;

        // If we encounter a blocked cell in leftmost
        // row, there is no way of visiting any cell
        // directly below it.
        else
            break;
    }

    // Similarly initialize the topmost row
    for (int i = 1; i < C; i++)
    {
        if (maze[0, i] == 0)
            maze[0, i] = 1;

        // If we encounter a blocked cell in
        // bottommost row, there is no way of
        // visiting any cell directly below it.
        else
            break;
    }

    // The only difference is that if a cell is -1,
    // simply ignore it else recursively compute
    // count value maze[i][j]
    for (int i = 1; i < R; i++)
    {
        for (int j = 1; j < C; j++)
        {

            // If blockage is found, ignore this cell
            if (maze[i, j] == -1)
                continue;

            // If we can reach maze[i][j] from
            // maze[i-1][j] then increment count.
            if (maze[i - 1, j] > 0)
                maze[i, j] = (maze[i, j] +
                              maze[i - 1, j]);

            // If we can reach maze[i][j] from
            // maze[i][j-1] then increment count.
            if (maze[i, j - 1] > 0)
                maze[i, j] = (maze[i, j] +
                              maze[i, j - 1]);
        }
    }

    // If the final cell is blocked,
    // output 0, otherwise the answer
    return (maze[R - 1, C - 1] > 0) ?
            maze[R - 1, C - 1] : 0;
}

// Function to return the count of all possible
// paths from (0, 0) to (n - 1, m - 1)
static int numberOfPaths(int m, int n)
{
    // We have to calculate m+n-2 C n-1 here
    // which will be (m+n-2)! / (n-1)! (m-1)!
    int path = 1;
    for (int i = n; i < (m + n - 1); i++)
    {
        path *= i;
        path /= (i - n + 1);
    }
    return path;
}

// Function to return the total count of paths
// from (0, 0) to (n - 1, m - 1) that pass
// through at least one of the marked cells
static int solve(int [,]maze)
{

    // Total count of paths - Total paths that do not
    // pass through any of the marked cell
    int ans = numberOfPaths(R, C) -
              countPaths(maze);

    // return answer
    return ans;
}

// Driver code
public static void Main ()
{
    int [,]maze = {{ 0, 0, 0, 0 },
                   { 0, -1, 0, 0 },
                   { -1, 0, 0, 0 },
                   { 0, 0, 0, 0 }};

    Console.Write(solve(maze));
}
}

// This code is contributed by anuj_67..
```

## java 描述语言

```
<script>

// Javascript implementation of the approach
var R = 4
var C = 4

// Function to return the count of possible paths
// in a maze[R][C] from (0, 0) to (R-1, C-1) that
// do not pass through any of the marked cells
function countPaths(maze)
{
    // If the initial cell is blocked, there is no
    // way of moving anywhere
    if (maze[0][0] == -1)
        return 0;

    // Initializing the leftmost column
    for (var i = 0; i < R; i++) {
        if (maze[i][0] == 0)
            maze[i][0] = 1;

        // If we encounter a blocked cell in leftmost
        // row, there is no way of visiting any cell
        // directly below it.
        else
            break;
    }

    // Similarly initialize the topmost row
    for (var i = 1; i < C; i++) {
        if (maze[0][i] == 0)
            maze[0][i] = 1;

        // If we encounter a blocked cell in bottommost
        // row, there is no way of visiting any cell
        // directly below it.
        else
            break;
    }

    // The only difference is that if a cell is -1,
    // simply ignore it else recursively compute
    // count value maze[i][j]
    for (var i = 1; i < R; i++) {
        for (var j = 1; j < C; j++) {
            // If blockage is found, ignore this cell
            if (maze[i][j] == -1)
                continue;

            // If we can reach maze[i][j] from maze[i-1][j]
            // then increment count.
            if (maze[i - 1][j] > 0)
                maze[i][j] = (maze[i][j] + maze[i - 1][j]);

            // If we can reach maze[i][j] from maze[i][j-1]
            // then increment count.
            if (maze[i][j - 1] > 0)
                maze[i][j] = (maze[i][j] + maze[i][j - 1]);
        }
    }

    // If the final cell is blocked, output 0, otherwise
    // the answer
    return (maze[R - 1][C - 1] > 0) ? maze[R - 1][C - 1] : 0;
}
// Function to return the count of all possible
// paths from (0, 0) to (n - 1, m - 1)
function numberOfPaths(m, n)
{
    // We have to calculate m+n-2 C n-1 here
    // which will be (m+n-2)! / (n-1)! (m-1)!
    var path = 1;
    for (var i = n; i < (m + n - 1); i++) {
        path *= i;
        path /= (i - n + 1);
    }
    return path;
}

// Function to return the total count of paths
// from (0, 0) to (n - 1, m - 1) that pass
// through at least one of the marked cells
function solve(maze)
{

    // Total count of paths - Total paths that do not
    // pass through any of the marked cell
    var ans = numberOfPaths(R, C) - countPaths(maze);

    // return answer
    return ans;
}

// Driver code
var maze = [ [ 0, 0, 0, 0 ],
                   [ 0, -1, 0, 0 ],
                   [ -1, 0, 0, 0 ],
                   [ 0, 0, 0, 0 ] ];
document.write( solve(maze));

// This code is contributed by rrrtnx.
</script>   
```

**Output:** 

```
16
```

**时间复杂度:**O(R * C)
T3】辅助空间: O(R*C)