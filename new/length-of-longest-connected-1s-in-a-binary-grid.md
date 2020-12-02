# 二进制网格中最长连接的 1 的长度

> 原文： [https://www.geeksforgeeks.org/length-of-longest-connected-1s-in-a-binary-grid/](https://www.geeksforgeeks.org/length-of-longest-connected-1s-in-a-binary-grid/)

给定大小为 **N * M** 的网格仅由 **0** 和 **1** 组成，任务是找到最长连接的 **1s** 的长度。 在给定的网格中。 我们只能从网格的任何当前单元格向左，向右，向上或向下移动。

**示例：**

> **输入：** N = 3，M = 3，grid [] [] = {{0，0，0}，{0，1，0}，{0，0，0}}
> **输出：** 1
> **说明：**
> 最长的路径是 1，因为从矩阵的（1，1）位置不能有任何移动。
> 
> **输入：** N = 6，M = 7，grid [] [] = {{0，0，0，0，0，0，0}，{0，1，0，1，0， 0，0}，{0，1，0，1，0，0，0}，{0，1，0，1，0，1，0}，{0，1，1，1，1，1， 0}，{0，0，0，0，0，0，0}}}
> **输出：** 9
> **说明：**
> 最长的路线是 9 从（1，1）->（2，1）->（3，1）->（4，1）->（4，2）->（4 ，3）->（4，4）->（4，5）->（3，5）。

**方法：**的想法是在当前单元格值为 **1** 的网格上进行 [DFS 遍历](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)，然后递归调用当前单元格的所有四个方向 值是 **1** ，并更新了连接的 **1** 的最大长度。

下面是上述方法的实现：

## C ++

```

// C++ program for the above approach

#include <bits/stdc++.h>
#define row 6
#define col 7
using namespace std;

int vis[row + 1][col + 1], id;
int diameter = 0, length = 0;

// Keeps a track of directions
// that is up, down, left, right
int dx[] = { -1, 1, 0, 0 };
int dy[] = { 0, 0, -1, 1 };

// Function to perform the dfs traversal
void dfs(int a, int b, int lis[][col],
         int& x, int& y)
{

    // Mark the current node as visited
    vis[a][b] = id;

    // Increment length from this node
    length++;

    // Update the diameter length
    if (length > diameter) {
        x = a;
        y = b;
        diameter = length;
    }
    for (int j = 0; j < 4; j++) {

        // Move to next cell in x-direction
        int cx = a + dx[j];

        // Move to next cell in y-direction
        int cy = b + dy[j];

        // Check if cell is invalid
        // then continue
        if (cx < 0 || cy < 0 || cx >= row
            || cy >= col || lis[cx][cy] == 0
            || vis[cx][cy]) {
            continue;
        }

        // Perform DFS on new cell
        dfs(cx, cy, lis, x, y);
    }

    vis[a][b] = 0;

    // Decrement the length
    length--;
}

// Function to find the maximum length of
// connected 1s in the given grid
void findMaximumLength(int lis[][col])
{

    int x, y;

    // Increment the id
    id++;
    length = 0;
    diameter = 0;

    // Traverse the grid[]
    for (int i = 0; i < row; i++) {

        for (int j = 0; j < col; j++) {

            if (lis[i][j] != 0) {

                // Find start point of
                // start dfs call
                dfs(i, j, lis, x, y);
                i = row;
                break;
            }
        }
    }

    id++;
    length = 0;
    diameter = 0;

    // DFS Traversal from cell (x, y)
    dfs(x, y, lis, x, y);

    // Print the maximum length
    cout << diameter;
}

// Driver Code
int main()
{
    // Given grid[][]
    int grid[][col] = { { 0, 0, 0, 0, 0, 0, 0 },
                        { 0, 1, 0, 1, 0, 0, 0 },
                        { 0, 1, 0, 1, 0, 0, 0 },
                        { 0, 1, 0, 1, 0, 1, 0 },
                        { 0, 1, 1, 1, 1, 1, 0 },
                        { 0, 0, 0, 1, 0, 0, 0 } };

    // Function Call
    findMaximumLength(grid);

    return 0;
}

```

## 爪哇

```

// Java program for the above approach
import java.util.*;

class GFG{

static final int row = 6;
static final int col = 7; 
static int [][]vis = new int[row + 1][col + 1];
static int id;
static int diameter = 0, length = 0;
static int x = 0, y = 0;

// Keeps a track of directions
// that is up, down, left, right
static int dx[] = { -1, 1, 0, 0 };
static int dy[] = { 0, 0, -1, 1 };

// Function to perform the dfs traversal
static void dfs(int a, int b, int lis[][])
{

    // Mark the current node as visited
    vis[a][b] = id;

    // Increment length from this node
    length++;

    // Update the diameter length
    if (length > diameter)
    {
        x = a;
        y = b;
        diameter = length;
    }

    for(int j = 0; j < 4; j++) 
    {

       // Move to next cell in x-direction
       int cx = a + dx[j];

       // Move to next cell in y-direction
       int cy = b + dy[j];

       // Check if cell is invalid
       // then continue
       if (cx < 0 || cy < 0 || 
           cx >= row || cy >= col || 
           lis[cx][cy] == 0 || vis[cx][cy] > 0) 
       {
           continue;
       }

       // Perform DFS on new cell
       dfs(cx, cy, lis);
    }

    vis[a][b] = 0;

    // Decrement the length
    length--;
}

// Function to find the maximum length of
// connected 1s in the given grid
static void findMaximumLength(int lis[][])
{

    // Increment the id
    id++;
    length = 0;
    diameter = 0;

    // Traverse the grid[]
    for(int i = 0; i < row; i++) 
    {
       for(int j = 0; j < col; j++)
       {
          if (lis[i][j] != 0)
          {

              // Find start point of
              // start dfs call
              dfs(i, j, lis);
              i = row;
              break;
          }
       }
    }

    id++;
    length = 0;
    diameter = 0;

    // DFS Traversal from cell (x, y)
    dfs(x, y, lis);

    // Print the maximum length
    System.out.print(diameter);
}

// Driver Code
public static void main(String[] args)
{

    // Given grid[][]
    int grid[][] = { { 0, 0, 0, 0, 0, 0, 0 },
                     { 0, 1, 0, 1, 0, 0, 0 },
                     { 0, 1, 0, 1, 0, 0, 0 },
                     { 0, 1, 0, 1, 0, 1, 0 },
                     { 0, 1, 1, 1, 1, 1, 0 },
                     { 0, 0, 0, 1, 0, 0, 0 } };

    // Function Call
    findMaximumLength(grid);
}
}

// This code is contributed by amal kumar choubey

```

## Python3

```

# Python3 program for the above approach
row = 6
col = 7

vis = [[0 for i in range(col + 1)]
          for j in range(row + 1)] 
id = 0
diameter = 0
length = 0

# Keeps a track of directions
# that is up, down, left, right
dx = [ -1, 1, 0, 0 ]
dy = [ 0, 0, -1, 1 ]

# Function to perform the dfs traversal
def dfs(a, b, lis, x, y):

    global id, length, diameter

    # Mark the current node as visited
    vis[a][b] = id

    # Increment length from this node
    length += 1

    # Update the diameter length
    if (length > diameter):
        x = a
        y = b
        diameter = length

    for j in range(4):

        # Move to next cell in x-direction
        cx = a + dx[j]

        # Move to next cell in y-direction
        cy = b + dy[j]

        # Check if cell is invalid
        # then continue
        if (cx < 0 or cy < 0 or
            cx >= row or cy >= col or
            lis[cx][cy] == 0 or vis[cx][cy]):
            continue

        # Perform DFS on new cell
        dfs(cx, cy, lis, x, y)

    vis[a][b] = 0

    # Decrement the length
    length -= 1

    return x, y

# Function to find the maximum length of
# connected 1s in the given grid
def findMaximumLength(lis):

    global id, length, diameter

    x = 0
    y = 0

    # Increment the id
    id += 1

    length = 0
    diameter = 0

    # Traverse the grid[]
    for i in range(row):
        for j in range(col):
            if (lis[i][j] != 0):

                # Find start point of
                # start dfs call
                x, y = dfs(i, j, lis, x, y)
                i = row
                break

    id += 1
    length = 0
    diameter = 0

    # DFS Traversal from cell (x, y)
    x, y = dfs(x, y, lis, x, y)

    # Print the maximum length
    print(diameter)

# Driver Code
if __name__=="__main__":

    # Given grid[][]
    grid = [ [ 0, 0, 0, 0, 0, 0, 0 ],
             [ 0, 1, 0, 1, 0, 0, 0 ],
             [ 0, 1, 0, 1, 0, 0, 0 ],
             [ 0, 1, 0, 1, 0, 1, 0 ],
             [ 0, 1, 1, 1, 1, 1, 0 ],
             [ 0, 0, 0, 1, 0, 0, 0 ] ]

    # Function Call
    findMaximumLength(grid)

# This code is contributed by rutvik_56

```

## C＃

```

// C# program for the above approach
using System;

class GFG{

static readonly int row = 6;
static readonly int col = 7; 
static int [,]vis = new int[row + 1, col + 1];
static int id;
static int diameter = 0, length = 0;
static int x = 0, y = 0;

// Keeps a track of directions
// that is up, down, left, right
static int []dx = { -1, 1, 0, 0 };
static int []dy = { 0, 0, -1, 1 };

// Function to perform the dfs traversal
static void dfs(int a, int b, int [,]lis)
{

    // Mark the current node as visited
    vis[a, b] = id;

    // Increment length from this node
    length++;

    // Update the diameter length
    if (length > diameter)
    {
        x = a;
        y = b;
        diameter = length;
    }

    for(int j = 0; j < 4; j++) 
    {

        // Move to next cell in x-direction
        int cx = a + dx[j];

        // Move to next cell in y-direction
        int cy = b + dy[j];

        // Check if cell is invalid
        // then continue
        if (cx < 0 || cy < 0 || 
            cx >= row || cy >= col || 
            lis[cx, cy] == 0 || vis[cx, cy] > 0) 
        {
            continue;
        }

        // Perform DFS on new cell
        dfs(cx, cy, lis);
    }
    vis[a, b] = 0;

    // Decrement the length
    length--;
}

// Function to find the maximum length of
// connected 1s in the given grid
static void findMaximumLength(int [,]lis)
{

    // Increment the id
    id++;
    length = 0;
    diameter = 0;

    // Traverse the grid[]
    for(int i = 0; i < row; i++) 
    {
        for(int j = 0; j < col; j++)
        {
            if (lis[i, j] != 0)
            {

                // Find start point of
                // start dfs call
                dfs(i, j, lis);
                i = row;
                break;
            }
        }
    }

    id++;
    length = 0;
    diameter = 0;

    // DFS Traversal from cell (x, y)
    dfs(x, y, lis);

    // Print the maximum length
    Console.Write(diameter);
}

// Driver Code
public static void Main(String[] args)
{

    // Given grid[,]
    int [,]grid = { { 0, 0, 0, 0, 0, 0, 0 },
                    { 0, 1, 0, 1, 0, 0, 0 },
                    { 0, 1, 0, 1, 0, 0, 0 },
                    { 0, 1, 0, 1, 0, 1, 0 },
                    { 0, 1, 1, 1, 1, 1, 0 },
                    { 0, 0, 0, 1, 0, 0, 0 } };

    // Function Call
    findMaximumLength(grid);
}
}

// This code is contributed by amal kumar choubey

```

**Output:** 

```
9

```

**时间复杂度：** *O（行+列）*

[![competitive-programming-img](img/5211864e7e7a28eeeb039fa5d6073a24.png)](https://practice.geeksforgeeks.org/courses/competitive-programming-live?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_cp)

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。