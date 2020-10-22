# 二进制迷宫中的最短路径

> 原文： [https://www.geeksforgeeks.org/shortest-path-in-a-binary-maze/](https://www.geeksforgeeks.org/shortest-path-in-a-binary-maze/)

给定一个`MxN`矩阵，其中每个元素可以为 0 或 1。我们需要找到给定源单元格到目标单元格之间的最短路径。 如果路径的值为 1，则只能在单元格外部创建路径。

预期时间复杂度为`O(MN)`。

例如：

```
Input:
mat[ROW][COL]  = {{1, 0, 1, 1, 1, 1, 0, 1, 1, 1 },
                  {1, 0, 1, 0, 1, 1, 1, 0, 1, 1 },
                  {1, 1, 1, 0, 1, 1, 0, 1, 0, 1 },
                  {0, 0, 0, 0, 1, 0, 0, 0, 0, 1 },
                  {1, 1, 1, 0, 1, 1, 1, 0, 1, 0 },
                  {1, 0, 1, 1, 1, 1, 0, 1, 0, 0 },
                  {1, 0, 0, 0, 0, 0, 0, 0, 0, 1 },
                  {1, 0, 1, 1, 1, 1, 0, 1, 1, 1 },
                  {1, 1, 0, 0, 0, 0, 1, 0, 0, 1 }};
Source = {0, 0};
Destination = {3, 4};

Output:
Shortest Path is 11 
```



这个想法的灵感来自 [Lee 算法](https://en.wikipedia.org/wiki/Lee_algorithm)，并使用了 BFS。

1.  我们从源单元开始，并调用 BFS 过程。

2.  我们维护一个队列来存储矩阵的坐标，并使用源单元格对其进行初始化。

3.  我们还维护一个布尔数组，该数组的大小与输入矩阵的大小相同，并将其所有元素初始化为`false`。

    1.  我们循环直到队列不为空。

    2.  从队列中取出前端单元。

    3.  如果到达目标坐标，则返回。

    4.  对于其四个相邻单元格中的每个单元格，如果值为 1 并且尚未访问它们，我们将其排队在队列中，并将它们标记为已访问。

**请注意**， [BFS](http://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) 在这里可以正常使用，因为它不会一次考虑单个路径。 它考虑了从源头开始的所有路径，并同时在所有这些路径中向前移动了一个单元，这确保了第一次访问目的地时，它是最短的路径。

以下是该想法的实现–

## C++

```cpp
// C++ program to find the shortest path between
// a given source cell to a destination cell.
#include <bits/stdc++.h>
using namespace std;
#define ROW 9
#define COL 10
 
//To store matrix cell cordinates
struct Point
{
    int x;
    int y;
};
 
// A Data Structure for queue used in BFS
struct queueNode
{
    Point pt;  // The cordinates of a cell
    int dist;  // cell's distance of from the source
};
 
// check whether given cell (row, col) is a valid
// cell or not.
bool isValid(int row, int col)
{
    // return true if row number and column number
    // is in range
    return (row >= 0) && (row < ROW) &&
           (col >= 0) && (col < COL);
}
 
// These arrays are used to get row and column
// numbers of 4 neighbours of a given cell
int rowNum[] = {-1, 0, 0, 1};
int colNum[] = {0, -1, 1, 0};
 
// function to find the shortest path between
// a given source cell to a destination cell.
int BFS(int mat[][COL], Point src, Point dest)
{
    // check source and destination cell
    // of the matrix have value 1
    if (!mat[src.x][src.y] || !mat[dest.x][dest.y])
        return -1;
 
    bool visited[ROW][COL];
    memset(visited, false, sizeof visited);
     
    // Mark the source cell as visited
    visited[src.x][src.y] = true;
 
    // Create a queue for BFS
    queue<queueNode> q;
     
    // Distance of source cell is 0
    queueNode s = {src, 0};
    q.push(s);  // Enqueue source cell
 
    // Do a BFS starting from source cell
    while (!q.empty())
    {
        queueNode curr = q.front();
        Point pt = curr.pt;
 
        // If we have reached the destination cell,
        // we are done
        if (pt.x == dest.x && pt.y == dest.y)
            return curr.dist;
 
        // Otherwise dequeue the front 
        // cell in the queue
        // and enqueue its adjacent cells
        q.pop();
 
        for (int i = 0; i < 4; i++)
        {
            int row = pt.x + rowNum[i];
            int col = pt.y + colNum[i];
             
            // if adjacent cell is valid, has path and
            // not visited yet, enqueue it.
            if (isValid(row, col) && mat[row][col] && 
               !visited[row][col])
            {
                // mark cell as visited and enqueue it
                visited[row][col] = true;
                queueNode Adjcell = { {row, col},
                                      curr.dist + 1 };
                q.push(Adjcell);
            }
        }
    }
 
    // Return -1 if destination cannot be reached
    return -1;
}
 
// Driver program to test above function
int main()
{
    int mat[ROW][COL] =
    {
        { 1, 0, 1, 1, 1, 1, 0, 1, 1, 1 },
        { 1, 0, 1, 0, 1, 1, 1, 0, 1, 1 },
        { 1, 1, 1, 0, 1, 1, 0, 1, 0, 1 },
        { 0, 0, 0, 0, 1, 0, 0, 0, 0, 1 },
        { 1, 1, 1, 0, 1, 1, 1, 0, 1, 0 },
        { 1, 0, 1, 1, 1, 1, 0, 1, 0, 0 },
        { 1, 0, 0, 0, 0, 0, 0, 0, 0, 1 },
        { 1, 0, 1, 1, 1, 1, 0, 1, 1, 1 },
        { 1, 1, 0, 0, 0, 0, 1, 0, 0, 1 }
    };
 
    Point source = {0, 0};
    Point dest = {3, 4};
 
    int dist = BFS(mat, source, dest);
 
    if (dist != -1)
        cout << "Shortest Path is " << dist ;
    else
        cout << "Shortest Path doesn't exist";
 
    return 0;
}
```

## Java

```java
// Java program to find the shortest 
// path between a given source cell 
// to a destination cell.
import java.util.*;
 
class GFG 
{
static int ROW = 9;
static int COL = 10;
 
// To store matrix cell cordinates
static class Point
{
    int x;
    int y;
 
    public Point(int x, int y)
    {
        this.x = x;
        this.y = y;
    }
};
 
// A Data Structure for queue used in BFS
static class queueNode
{
    Point pt; // The cordinates of a cell
    int dist; // cell's distance of from the source
 
    public queueNode(Point pt, int dist)
    {
        this.pt = pt;
        this.dist = dist;
    }
};
 
// check whether given cell (row, col) 
// is a valid cell or not.
static boolean isValid(int row, int col)
{
    // return true if row number and 
    // column number is in range
    return (row >= 0) && (row < ROW) &&
           (col >= 0) && (col < COL);
}
 
// These arrays are used to get row and column
// numbers of 4 neighbours of a given cell
static int rowNum[] = {-1, 0, 0, 1};
static int colNum[] = {0, -1, 1, 0};
 
// function to find the shortest path between
// a given source cell to a destination cell.
static int BFS(int mat[][], Point src,
                            Point dest)
{
    // check source and destination cell
    // of the matrix have value 1
    if (mat[src.x][src.y] != 1 || 
        mat[dest.x][dest.y] != 1)
        return -1;
 
    boolean [][]visited = new boolean[ROW][COL];
     
    // Mark the source cell as visited
    visited[src.x][src.y] = true;
 
    // Create a queue for BFS
    Queue<queueNode> q = new LinkedList<>();
     
    // Distance of source cell is 0
    queueNode s = new queueNode(src, 0);
    q.add(s); // Enqueue source cell
 
    // Do a BFS starting from source cell
    while (!q.isEmpty())
    {
        queueNode curr = q.peek();
        Point pt = curr.pt;
 
        // If we have reached the destination cell,
        // we are done
        if (pt.x == dest.x && pt.y == dest.y)
            return curr.dist;
 
        // Otherwise dequeue the front cell 
        // in the queue and enqueue
        // its adjacent cells
        q.remove();
 
        for (int i = 0; i < 4; i++)
        {
            int row = pt.x + rowNum[i];
            int col = pt.y + colNum[i];
             
            // if adjacent cell is valid, has path 
            // and not visited yet, enqueue it.
            if (isValid(row, col) && 
                    mat[row][col] == 1 && 
                    !visited[row][col])
            {
                // mark cell as visited and enqueue it
                visited[row][col] = true;
                queueNode Adjcell = new queueNode
                             (new Point(row, col),
                                   curr.dist + 1 );
                q.add(Adjcell);
            }
        }
    }
 
    // Return -1 if destination cannot be reached
    return -1;
}
 
// Driver Code
public static void main(String[] args) 
{
    int mat[][] = {{ 1, 0, 1, 1, 1, 1, 0, 1, 1, 1 },
                   { 1, 0, 1, 0, 1, 1, 1, 0, 1, 1 },
                   { 1, 1, 1, 0, 1, 1, 0, 1, 0, 1 },
                   { 0, 0, 0, 0, 1, 0, 0, 0, 0, 1 },
                   { 1, 1, 1, 0, 1, 1, 1, 0, 1, 0 },
                   { 1, 0, 1, 1, 1, 1, 0, 1, 0, 0 },
                   { 1, 0, 0, 0, 0, 0, 0, 0, 0, 1 },
                   { 1, 0, 1, 1, 1, 1, 0, 1, 1, 1 },
                   { 1, 1, 0, 0, 0, 0, 1, 0, 0, 1 }};
 
    Point source = new Point(0, 0);
    Point dest = new Point(3, 4);
 
    int dist = BFS(mat, source, dest);
 
    if (dist != -1)
        System.out.println("Shortest Path is " + dist);
    else
        System.out.println("Shortest Path doesn't exist");
    }
}
 
// This code is contributed by PrinciRaj1992
```

## Python

```py
# Python program to find the shortest
# path between a given source cell 
# to a destination cell.
 
from collections import deque
ROW = 9
COL = 10
 
# To store matrix cell cordinates
class Point:
    def __init__(self,x: int, y: int):
        self.x = x
        self.y = y
 
# A data structure for queue used in BFS
class queueNode:
    def __init__(self,pt: Point, dist: int):
        self.pt = pt  # The cordinates of the cell
        self.dist = dist  # Cell's distance from the source
 
# Check whether given cell(row,col)
# is a valid cell or not
def isValid(row: int, col: int):
    return (row >= 0) and (row < ROW) and
                   (col >= 0) and (col < COL)
 
# These arrays are used to get row and column 
# numbers of 4 neighbours of a given cell 
rowNum = [-1, 0, 0, 1]
colNum = [0, -1, 1, 0]
 
# Function to find the shortest path between 
# a given source cell to a destination cell. 
def BFS(mat, src: Point, dest: Point):
     
    # check source and destination cell 
    # of the matrix have value 1 
    if mat[src.x][src.y]!=1 or mat[dest.x][dest.y]!=1:
        return -1
     
    visited = [[False for i in range(COL)] 
                       for j in range(ROW)]
     
    # Mark the source cell as visited 
    visited[src.x][src.y] = True
     
    # Create a queue for BFS 
    q = deque()
     
    # Distance of source cell is 0
    s = queueNode(src,0)
    q.append(s) #  Enqueue source cell
     
    # Do a BFS starting from source cell 
    while q:
 
        curr = q.popleft() # Dequeue the front cell
         
        # If we have reached the destination cell, 
        # we are done 
        pt = curr.pt
        if pt.x == dest.x and pt.y == dest.y:
            return curr.dist
         
        # Otherwise enqueue its adjacent cells 
        for i in range(4):
            row = pt.x + rowNum[i]
            col = pt.y + colNum[i]
             
            # if adjacent cell is valid, has path  
            # and not visited yet, enqueue it.
            if (isValid(row,col) and
               mat[row][col] == 1 and
                not visited[row][col]):
                visited[row][col] = True
                Adjcell = queueNode(Point(row,col),
                                    curr.dist+1)
                q.append(Adjcell)
     
    # Return -1 if destination cannot be reached 
    return -1
 
# Driver code
def main():
    mat = [[ 1, 0, 1, 1, 1, 1, 0, 1, 1, 1 ],
           [ 1, 0, 1, 0, 1, 1, 1, 0, 1, 1 ], 
           [ 1, 1, 1, 0, 1, 1, 0, 1, 0, 1 ], 
           [ 0, 0, 0, 0, 1, 0, 0, 0, 0, 1 ], 
           [ 1, 1, 1, 0, 1, 1, 1, 0, 1, 0 ], 
           [ 1, 0, 1, 1, 1, 1, 0, 1, 0, 0 ], 
           [ 1, 0, 0, 0, 0, 0, 0, 0, 0, 1 ], 
           [ 1, 0, 1, 1, 1, 1, 0, 1, 1, 1 ], 
           [ 1, 1, 0, 0, 0, 0, 1, 0, 0, 1 ]]
    source = Point(0,0)
    dest = Point(3,4)
     
    dist = BFS(mat,source,dest)
     
    if dist!=-1:
        print("Shortest Path is",dist)
    else:
        print("Shortest Path doesn't exist")
main()
 
# This code is contributed by stutipathak31jan
```

## C#

```cs
// C# program to find the shortest 
// path between a given source cell 
// to a destination cell.
using System;
using System.Collections.Generic;
 
class GFG 
{
static int ROW = 9;
static int COL = 10;
 
// To store matrix cell cordinates
public class Point
{
    public int x;
    public int y;
 
    public Point(int x, int y)
    {
        this.x = x;
        this.y = y;
    }
};
 
// A Data Structure for queue used in BFS
public class queueNode
{
    // The cordinates of a cell
    public Point pt; 
     
    // cell's distance of from the source
    public int dist; 
 
    public queueNode(Point pt, int dist)
    {
        this.pt = pt;
        this.dist = dist;
    }
};
 
// check whether given cell (row, col) 
// is a valid cell or not.
static bool isValid(int row, int col)
{
    // return true if row number and 
    // column number is in range
    return (row >= 0) && (row < ROW) &&
           (col >= 0) && (col < COL);
}
 
// These arrays are used to get row and column
// numbers of 4 neighbours of a given cell
static int []rowNum = {-1, 0, 0, 1};
static int []colNum = {0, -1, 1, 0};
 
// function to find the shortest path between
// a given source cell to a destination cell.
static int BFS(int [,]mat, Point src,
                           Point dest)
{
    // check source and destination cell
    // of the matrix have value 1
    if (mat[src.x, src.y] != 1 || 
        mat[dest.x, dest.y] != 1)
        return -1;
 
    bool [,]visited = new bool[ROW, COL];
     
    // Mark the source cell as visited
    visited[src.x, src.y] = true;
 
    // Create a queue for BFS
    Queue<queueNode> q = new Queue<queueNode>();
     
    // Distance of source cell is 0
    queueNode s = new queueNode(src, 0);
    q.Enqueue(s); // Enqueue source cell
 
    // Do a BFS starting from source cell
    while (q.Count != 0)
    {
        queueNode curr = q.Peek();
        Point pt = curr.pt;
 
        // If we have reached the destination cell,
        // we are done
        if (pt.x == dest.x && pt.y == dest.y)
            return curr.dist;
 
        // Otherwise dequeue the front cell 
        // in the queue and enqueue
        // its adjacent cells
        q.Dequeue();
 
        for (int i = 0; i < 4; i++)
        {
            int row = pt.x + rowNum[i];
            int col = pt.y + colNum[i];
             
            // if adjacent cell is valid, has path 
            // and not visited yet, enqueue it.
            if (isValid(row, col) && 
                    mat[row, col] == 1 && 
               !visited[row, col])
            {
                // mark cell as visited and enqueue it
                visited[row, col] = true;
                queueNode Adjcell = new queueNode
                           (new Point(row, col),
                                curr.dist + 1 );
                q.Enqueue(Adjcell);
            }
        }
    }
 
    // Return -1 if destination cannot be reached
    return -1;
}
 
// Driver Code
public static void Main(String[] args) 
{
    int [,]mat = {{ 1, 0, 1, 1, 1, 1, 0, 1, 1, 1 },
                  { 1, 0, 1, 0, 1, 1, 1, 0, 1, 1 },
                   { 1, 1, 1, 0, 1, 1, 0, 1, 0, 1 },
                  { 0, 0, 0, 0, 1, 0, 0, 0, 0, 1 },
                  { 1, 1, 1, 0, 1, 1, 1, 0, 1, 0 },
                  { 1, 0, 1, 1, 1, 1, 0, 1, 0, 0 },
                  { 1, 0, 0, 0, 0, 0, 0, 0, 0, 1 },
                  { 1, 0, 1, 1, 1, 1, 0, 1, 1, 1 },
                  { 1, 1, 0, 0, 0, 0, 1, 0, 0, 1 }};
 
    Point source = new Point(0, 0);
    Point dest = new Point(3, 4);
 
    int dist = BFS(mat, source, dest);
 
    if (dist != -1)
        Console.WriteLine("Shortest Path is " + dist);
    else
        Console.WriteLine("Shortest Path doesn't exist");
    }
}
 
// This code is contributed by PrinciRaj1992
```

输出：

```
Shortest Path is 11
```

