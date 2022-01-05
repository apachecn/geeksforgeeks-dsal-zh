# 2D 数组上的广度优先遍历(BFS)

> 原文:[https://www . geesforgeks . org/width-first-遍历-bfs-on-a-2d-array/](https://www.geeksforgeeks.org/breadth-first-traversal-bfs-on-a-2d-array/)

给定一个由整数组成的大小为 **M x N** 的矩阵，任务是使用[广度优先搜索](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/)遍历来打印矩阵元素。

**示例:**

> **输入:**网格[][] = {{1，2，3，4}，{5，6，7，8}，{9，10，11，12}，{13，14，15，16}}
> **输出:**1 2 5 3 6 4 7 10 13 8 11 14 12 15 16
> 
> **输入:**网格[][]= {-1，0，0，1}，{-1，-1，-2，-1}，{-1，-1，-1，-1}，{0，0，0，0 } }
> T3】输出:-1 0-1 0-1 0-1 1 1-2-1 0-1 0-1 0-1 0 0 0

**方法:**按照以下步骤解决问题:

1.  初始化方向[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **卓尔[] = {-1，0，1，0}** 和 **dCol[] = {0，1，0，-1}** 以及[对](https://www.geeksforgeeks.org/pair-in-cpp-stl/)的[队列](https://www.geeksforgeeks.org/queue-data-structure/)，以存储矩阵单元的索引。
2.  从第一个单元格开始 [BFS 遍历](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/)，即 **(0，0)** ，然后[将该单元格的索引排入](https://www.geeksforgeeks.org/queuepush-and-queuepop-in-cpp-stl/)[队列](https://www.geeksforgeeks.org/queue-data-structure/)。
3.  初始化一个布尔[数组](https://www.geeksforgeeks.org/array-data-structure/)来标记矩阵的访问单元。将单元格 **(0，0)** 标记为已访问。
4.  声明一个函数 **isValid()** 来检查单元格坐标是否有效，即是否位于给定矩阵的边界内，是否未被访问。
5.  当[队列不为空时](https://www.geeksforgeeks.org/queueempty-queuesize-c-stl/)进行迭代，并执行以下操作:
    *   [将位于队列](https://www.geeksforgeeks.org/queuepush-and-queuepop-in-cpp-stl/)前面[的单元格出列](https://www.geeksforgeeks.org/queuefront-queueback-c-stl/)并打印。
    *   移动到未被访问的相邻单元格。
    *   将他们标记为已访问，并将其排入队列。

**注意:**方向向量用于以给定的顺序遍历给定单元的相邻单元。例如 **(x，y)** 是一个需要遍历其相邻单元格**(x–1，y)，(x，y + 1)，(x + 1，y)，(x，y–1)**的单元格，则可以使用方向向量 **(-1，0)，(0，1)，(1，0)，(0，-1)** 按照上、左、下、右的顺序进行。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

#define ROW 4
#define COL 4

// Direction vectors
int dRow[] = { -1, 0, 1, 0 };
int dCol[] = { 0, 1, 0, -1 };

// Function to check if a cell
// is be visited or not
bool isValid(bool vis[][COL],
             int row, int col)
{
    // If cell lies out of bounds
    if (row < 0 || col < 0
        || row >= ROW || col >= COL)
        return false;

    // If cell is already visited
    if (vis[row][col])
        return false;

    // Otherwise
    return true;
}

// Function to perform the BFS traversal
void BFS(int grid[][COL], bool vis[][COL],
         int row, int col)
{
    // Stores indices of the matrix cells
    queue<pair<int, int> > q;

    // Mark the starting cell as visited
    // and push it into the queue
    q.push({ row, col });
    vis[row][col] = true;

    // Iterate while the queue
    // is not empty
    while (!q.empty()) {

        pair<int, int> cell = q.front();
        int x = cell.first;
        int y = cell.second;

        cout << grid[x][y] << " ";

        q.pop();

        // Go to the adjacent cells
        for (int i = 0; i < 4; i++) {

            int adjx = x + dRow[i];
            int adjy = y + dCol[i];

            if (isValid(vis, adjx, adjy)) {
                q.push({ adjx, adjy });
                vis[adjx][adjy] = true;
            }
        }
    }
}

// Driver Code
int main()
{
    // Given input matrix
    int grid[ROW][COL] = { { 1, 2, 3, 4 },
                           { 5, 6, 7, 8 },
                           { 9, 10, 11, 12 },
                           { 13, 14, 15, 16 } };

    // Declare the visited array
    bool vis[ROW][COL];
    memset(vis, false, sizeof vis);

    BFS(grid, vis, 0, 0);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

static class pair
{
    int first, second;

    public pair(int first, int second) 
    {
        this.first = first;
        this.second = second;
    }   
}

static final int ROW = 4;
static final int COL = 4;

// Direction vectors
static int dRow[] = { -1, 0, 1, 0 };
static int dCol[] = { 0, 1, 0, -1 };

// Function to check if a cell
// is be visited or not
static boolean isValid(boolean vis[][],
                       int row, int col)
{

    // If cell lies out of bounds
    if (row < 0 || col < 0 ||
        row >= ROW || col >= COL)
        return false;

    // If cell is already visited
    if (vis[row][col])
        return false;

    // Otherwise
    return true;
}

// Function to perform the BFS traversal
static void BFS(int grid[][], boolean vis[][],
                int row, int col)
{

    // Stores indices of the matrix cells
    Queue<pair > q = new LinkedList<>();

    // Mark the starting cell as visited
    // and push it into the queue
    q.add(new pair(row, col));
    vis[row][col] = true;

    // Iterate while the queue
    // is not empty
    while (!q.isEmpty())
    {
        pair cell = q.peek();
        int x = cell.first;
        int y = cell.second;

        System.out.print(grid[x][y] + " ");

        q.remove();

        // Go to the adjacent cells
        for(int i = 0; i < 4; i++)
        {
            int adjx = x + dRow[i];
            int adjy = y + dCol[i];

            if (isValid(vis, adjx, adjy))
            {
                q.add(new pair(adjx, adjy));
                vis[adjx][adjy] = true;
            }
        }
    }
}

// Driver Code
public static void main(String[] args)
{

    // Given input matrix
    int grid[][] = { { 1, 2, 3, 4 },
                     { 5, 6, 7, 8 },
                     { 9, 10, 11, 12 },
                     { 13, 14, 15, 16 } };

    // Declare the visited array
    boolean [][]vis = new boolean[ROW][COL];

    BFS(grid, vis, 0, 0);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach
from collections import deque as queue

# Direction vectors
dRow = [ -1, 0, 1, 0]
dCol = [ 0, 1, 0, -1]

# Function to check if a cell
# is be visited or not
def isValid(vis, row, col):

    # If cell lies out of bounds
    if (row < 0 or col < 0 or row >= 4 or col >= 4):
        return False

    # If cell is already visited
    if (vis[row][col]):
        return False

    # Otherwise
    return True

# Function to perform the BFS traversal
def BFS(grid, vis, row, col):

    # Stores indices of the matrix cells
    q = queue()

    # Mark the starting cell as visited
    # and push it into the queue
    q.append(( row, col ))
    vis[row][col] = True

    # Iterate while the queue
    # is not empty
    while (len(q) > 0):
        cell = q.popleft()
        x = cell[0]
        y = cell[1]
        print(grid[x][y], end = " ")

        #q.pop()

        # Go to the adjacent cells
        for i in range(4):
            adjx = x + dRow[i]
            adjy = y + dCol[i]
            if (isValid(vis, adjx, adjy)):
                q.append((adjx, adjy))
                vis[adjx][adjy] = True

# Driver Code
if __name__ == '__main__':

    # Given input matrix
    grid= [ [ 1, 2, 3, 4 ],
           [ 5, 6, 7, 8 ],
           [ 9, 10, 11, 12 ],
           [ 13, 14, 15, 16 ] ]

    # Declare the visited array
    vis = [[ False for i in range(4)] for i in range(4)]
    # vis, False, sizeof vis)

    BFS(grid, vis, 0, 0)

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
public class GFG
{

  class pair
  {
    public int first, second;

    public pair(int first, int second) 
    {
      this.first = first;
      this.second = second;
    }   
  }
  static readonly int ROW = 4;
  static readonly int COL = 4;

  // Direction vectors
  static int []dRow = { -1, 0, 1, 0 };
  static int []dCol = { 0, 1, 0, -1 };

  // Function to check if a cell
  // is be visited or not
  static bool isValid(bool [,]vis,
                      int row, int col)
  {

    // If cell lies out of bounds
    if (row < 0 || col < 0 ||
        row >= ROW || col >= COL)
      return false;

    // If cell is already visited
    if (vis[row,col])
      return false;

    // Otherwise
    return true;
  }

  // Function to perform the BFS traversal
  static void BFS(int [,]grid, bool [,]vis,
                  int row, int col)
  {

    // Stores indices of the matrix cells
    Queue<pair> q = new Queue<pair>();

    // Mark the starting cell as visited
    // and push it into the queue
    q.Enqueue(new pair(row, col));
    vis[row,col] = true;

    // Iterate while the queue
    // is not empty
    while (q.Count!=0)
    {
      pair cell = q.Peek();
      int x = cell.first;
      int y = cell.second;
      Console.Write(grid[x,y] + " ");
      q.Dequeue();

      // Go to the adjacent cells
      for(int i = 0; i < 4; i++)
      {
        int adjx = x + dRow[i];
        int adjy = y + dCol[i];
        if (isValid(vis, adjx, adjy))
        {
          q.Enqueue(new pair(adjx, adjy));
          vis[adjx,adjy] = true;
        }
      }
    }
  }

  // Driver Code
  public static void Main(String[] args)
  {

    // Given input matrix
    int [,]grid = { { 1, 2, 3, 4 },
                   { 5, 6, 7, 8 },
                   { 9, 10, 11, 12 },
                   { 13, 14, 15, 16 } };

    // Declare the visited array
    bool [,]vis = new bool[ROW,COL];
    BFS(grid, vis, 0, 0);
  }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program for the above approach

var ROW = 4;
var COL = 4;

// Direction vectors
var dRow = [-1, 0, 1, 0 ];
var dCol = [0, 1, 0, -1 ];

// Function to check if a cell
// is be visited or not
function isValid(vis, row, col)
{
    // If cell lies out of bounds
    if (row < 0 || col < 0
        || row >= ROW || col >= COL)
        return false;

    // If cell is already visited
    if (vis[row][col])
        return false;

    // Otherwise
    return true;
}

// Function to perform the BFS traversal
function BFS( grid, vis,row, col)
{
    // Stores indices of the matrix cells
    var q = [];

    // Mark the starting cell as visited
    // and push it into the queue
    q.push([row, col ]);
    vis[row][col] = true;

    // Iterate while the queue
    // is not empty
    while (q.length!=0) {

        var cell = q[0];
        var x = cell[0];
        var y = cell[1];

        document.write( grid[x][y] + " ");

        q.shift();

        // Go to the adjacent cells
        for (var i = 0; i < 4; i++) {

            var adjx = x + dRow[i];
            var adjy = y + dCol[i];

            if (isValid(vis, adjx, adjy)) {
                q.push([adjx, adjy ]);
                vis[adjx][adjy] = true;
            }
        }
    }
}

// Driver Code
// Given input matrix
var grid = [[1, 2, 3, 4 ],
                       [5, 6, 7, 8 ],
                       [9, 10, 11, 12 ],
                       [13, 14, 15, 16 ] ];
// Declare the visited array
var vis = Array.from(Array(ROW), ()=> Array(COL).fill(false));
BFS(grid, vis, 0, 0);

</script>
```

**Output:** 

```
1 2 5 3 6 9 4 7 10 13 8 11 14 12 15 16
```

***时间复杂度:** O(N * M)*
***辅助空间:** O(N * M)*