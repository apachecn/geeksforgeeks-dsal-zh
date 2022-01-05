# 从二元矩阵的源单元到目的单元的最短路径，通过仅由 1 组成的单元

> 原文:[https://www . geesforgeks . org/从源单元到目标单元的最短路径-二进制矩阵单元-通过仅由-1s 组成的单元/](https://www.geeksforgeeks.org/shortest-path-from-a-source-cell-to-a-destination-cell-of-a-binary-matrix-through-cells-consisting-only-of-1s/)

给定尺寸为 **N * M** 的[二进制矩阵](https://www.geeksforgeeks.org/program-to-check-if-a-matrix-is-binary-matrix-or-not/)**mat【】【】**和分别表示**源**和**目的**单元的整数对 **src** 和 **dest** ，任务是通过仅由 **1** s 组成的单元找到从给定源单元到目的单元的最短移动顺序。允许的移动是向左移动单元 ****右** ( **R** )、**上** ( **U** )、**下** ( **D** ) ( *如果存在*)。 如果不存在这样的路径，则打印**-1”**。否则，打印移动顺序。**

****示例:****

> ****输入:**mat[][]= {'0 '，' 0 '，' 0 '，' 0 '，' 0'}，{'0 '，' 1 '，' 1 '，' 0'}，{'0 '，' 1 '，' 0 '，' 1 '，' 1'}，{ ' 0 '，' 0 '，' 0 '，' 0 '，' 0'}}，src = {1，2}，dest = {2，4 }
> T3】输出: LDDRRRU 【T5 1) - > (2，1) - > (3，1) - > (3，2) - > (3，3) - > (3，4) - > (2，4)
> start->Left->Down->Down->Right->Right->Right->Up
> 因此，合成路径为 **LDDRRRRU** 。**
> 
> ****输入:**mat[]= { {‘0’，【1】、【0】、【1】、【0】、【1】、【1】、【1】、【1】、【1】、【1】、【1】、【0】、【0】、【0】、}、【src = { 0.3 }、
> 输出:ddld**

****方法:**给定问题可以通过对从给定源单元到目的单元的给定矩阵执行 [BFS 遍历](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/)来解决。
按照以下步骤解决给定问题:**

*   **初始化在给定矩阵上执行 [BFS 遍历](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/)所需的[队列](https://www.geeksforgeeks.org/queue-data-structure/)。**
*   **初始化一个布尔矩阵，比如**访问了【N】【M】**，用来检查给定的单元格是否被访问。最初，将所有指数设置为**假**。**
*   **初始化另一个矩阵，比如**距离【N】【M】**，用来存储从源节点到每个小区的最短距离。初始化为 **-1** 。**
*   **初始化一个字符串**路径将**移动为**“**，以存储从**源**到**目的单元格**的路径。**
*   **[将源节点推入队列](https://www.geeksforgeeks.org/queuepush-and-queuepop-in-cpp-stl/)，距离为 **0** 。**
*   **迭代直到[队列不为空](https://www.geeksforgeeks.org/queueempty-queuesize-c-stl/)并执行以下步骤:

    *   [弹出队列的前节点](https://www.geeksforgeeks.org/queuepush-and-queuepop-in-cpp-stl/)，说**当前节点**。
    *   检查弹出的节点是否为目的节点。如果发现为真，则使用[回溯](https://www.geeksforgeeks.org/backtracking-algorithms/)找到从目标单元格到源单元格的路径。
    *   否则，以**距离**为**(前一距离+ 1)** 插入当前弹出节点的所有未访问的相邻单元格。将**距离【当前码. x】【当前码. y】**的值更新为**(当前距离+ 1)** 。** 
*   **完成上述步骤后，如果存在从给定源到目标单元格的路径，则打印存储在**路径移动**中的路径作为结果。否则，打印**-1”**。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

#define ROW 4
#define COL 4

// Stores the coordinates
// of the matrix cell
struct Point {
    int x, y;
};

// Stores coordinates of
// a cell and its distance
struct Node {
    Point pt;
    int dist;
};

// Check if the given cell is valid or not
bool isValid(int row, int col)
{
    return (row >= 0) && (col >= 0)
           && (row < ROW) && (col < COL);
}

// Stores the moves of the directions of adjacent cells
int dRow[] = { -1, 0, 0, 1 };
int dCol[] = { 0, -1, 1, 0 };

// Function to find the shortest path from the
// source to destination in the given  matrix
void pathMoves(char mat[][COL],
               Point src, Point dest)
{
    // Stores the distance for each
    // cell from the source cell
    int d[ROW][COL];
    memset(d, -1, sizeof d);

    // Distance of source cell is 0
    d[src.x][src.y] = 0;

    // Initialize a visited array
    bool visited[ROW][COL];
    memset(visited, false, sizeof visited);

    // Mark source cell as visited
    visited[src.x][src.y] = true;

    // Create a queue for BFS
    queue<Node> q;

    // Distance of source cell is 0
    Node s = { src, 0 };

    // Enqueue source cell
    q.push(s);

    // Keeps track of whether
    // destination is reached or not
    bool ok = false;

    // Iterate until queue is not empty
    while (!q.empty()) {

        // Deque front of the queue
        Node curr = q.front();
        Point pt = curr.pt;

        // If the destination cell is
        // reached, then find the path
        if (pt.x == dest.x
            && pt.y == dest.y) {

            int xx = pt.x, yy = pt.y;
            int dist = curr.dist;

            // Assign the distance of
            // destination to the
            // distance matrix
            d[pt.x][pt.y] = dist;

            // Stores the smallest path
            string pathmoves = "";

            // Iterate until source is reached
            while (xx != src.x
                   || yy != src.y) {

                // Append D
                if (xx > 0 && d[xx - 1][yy] == dist - 1) {
                    pathmoves += 'D';
                    xx--;
                }

                // Append U
                if (xx < ROW - 1
                    && d[xx + 1][yy]
                           == dist - 1) {
                    pathmoves += 'U';
                    xx++;
                }

                // Append R
                if (yy > 0 && d[xx][yy - 1] == dist - 1) {
                    pathmoves += 'R';
                    yy--;
                }

                // Append L
                if (yy < COL - 1
                    && d[xx][yy + 1]
                           == dist - 1) {
                    pathmoves += 'L';
                    yy++;
                }
                dist--;
            }

            // Reverse the backtracked path
            reverse(pathmoves.begin(),
                    pathmoves.end());

            cout << pathmoves;
            ok = true;
            break;
        }

        // Pop the start of queue
        q.pop();

        // Explore all adjacent directions
        for (int i = 0; i < 4; i++) {
            int row = pt.x + dRow[i];
            int col = pt.y + dCol[i];

            // If the current cell is valid
            // cell and can be traversed
            if (isValid(row, col)
                && (mat[row][col] == '1'
                    || mat[row][col] == 's'
                    || mat[row][col] == 'd')
                && !visited[row][col]) {

                // Mark the adjacent cells as visited
                visited[row][col] = true;

                // Enqueue the adjacent cells
                Node adjCell
                    = { { row, col }, curr.dist + 1 };
                q.push(adjCell);

                // Update the distance
                // of the adjacent cells
                d[row][col] = curr.dist + 1;
            }
        }
    }

    // If the destination
    // is not reachable
    if (!ok)
        cout << -1;
}

// Driver Code
int main()
{
    char mat[ROW][COL] = { { '0', '1', '0', '1' },
                           { '1', '0', '1', '1' },
                           { '0', '1', '1', '1' },
                           { '1', '1', '1', '0' } };
    Point src = { 0, 3 };
    Point dest = { 3, 0 };

    pathMoves(mat, src, dest);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

static int ROW;
static int COL;

// Stores the coordinates
// of the matrix cell
static class Point
{
    int x, y;
    Point(int x, int y)
    {
        this.x = x;
        this.y = y;
    }
}

// Stores coordinates of
// a cell and its distance
static class Node
{
    Point pt;
    int dist;

    Node(Point p, int dist)
    {
        this.pt = p;
        this.dist = dist;
    }
}

// Check if the given cell is valid or not
static boolean isValid(int row, int col)
{
    return (row >= 0) && (col >= 0) &&
           (row < ROW) && (col < COL);
}

// Stores the moves of the directions
// of adjacent cells
static int dRow[] = { -1, 0, 0, 1 };
static int dCol[] = { 0, -1, 1, 0 };

// Function to find the shortest path from the
// source to destination in the given  matrix
static void pathMoves(char mat[][], Point src,
                      Point dest)
{

    // Stores the distance for each
    // cell from the source cell
    int d[][] = new int[ROW][COL];
    for(int dd[] : d)
        Arrays.fill(dd, -1);

    // Distance of source cell is 0
    d[src.x][src.y] = 0;

    // Initialize a visited array
    boolean visited[][] = new boolean[ROW][COL];

    // Mark source cell as visited
    visited[src.x][src.y] = true;

    // Create a queue for BFS
    ArrayDeque<Node> q = new ArrayDeque<>();

    // Distance of source cell is 0
    Node s = new Node(src, 0);

    // Enqueue source cell
    q.addLast(s);

    // Keeps track of whether
    // destination is reached or not
    boolean ok = false;

    // Iterate until queue is not empty
    while (!q.isEmpty())
    {

        // Deque front of the queue
        Node curr = q.removeFirst();
        Point pt = curr.pt;

        // If the destination cell is
        // reached, then find the path
        if (pt.x == dest.x && pt.y == dest.y)
        {
            int xx = pt.x, yy = pt.y;
            int dist = curr.dist;

            // Assign the distance of
            // destination to the
            // distance matrix
            d[pt.x][pt.y] = dist;

            // Stores the smallest path
            String pathmoves = "";

            // Iterate until source is reached
            while (xx != src.x || yy != src.y)
            {

                // Append D
                if (xx > 0 &&
                    d[xx - 1][yy] == dist - 1)
                {
                    pathmoves += 'D';
                    xx--;
                }

                // Append U
                if (xx < ROW - 1 &&
                    d[xx + 1][yy] == dist - 1)
                {
                    pathmoves += 'U';
                    xx++;
                }

                // Append R
                if (yy > 0 &&
                    d[xx][yy - 1] == dist - 1)
                {
                    pathmoves += 'R';
                    yy--;
                }

                // Append L
                if (yy < COL - 1 &&
                    d[xx][yy + 1] == dist - 1)
                {
                    pathmoves += 'L';
                    yy++;
                }
                dist--;
            }

            // Print reverse the backtracked path
            for(int i = pathmoves.length() - 1;
                    i >= 0; --i)
                System.out.print(pathmoves.charAt(i));

            ok = true;
            break;
        }

        // Pop the start of queue
        if (!q.isEmpty())
            q.removeFirst();

        // Explore all adjacent directions
        for(int i = 0; i < 4; i++)
        {
            int row = pt.x + dRow[i];
            int col = pt.y + dCol[i];

            // If the current cell is valid
            // cell and can be traversed
            if (isValid(row, col) &&
               (mat[row][col] == '1' ||
                mat[row][col] == 's' ||
                mat[row][col] == 'd') &&
                !visited[row][col])
            {

                // Mark the adjacent cells as visited
                visited[row][col] = true;

                // Enqueue the adjacent cells
                Node adjCell = new Node(
                    new Point(row, col), curr.dist + 1);
                q.addLast(adjCell);

                // Update the distance
                // of the adjacent cells
                d[row][col] = curr.dist + 1;
            }
        }
    }

    // If the destination
    // is not reachable
    if (!ok)
        System.out.println(-1);
}

// Driver Code
public static void main(String[] args)
{
    char mat[][] = { { '0', '1', '0', '1' },
                     { '1', '0', '1', '1' },
                     { '0', '1', '1', '1' },
                     { '1', '1', '1', '0' } };

    ROW = mat.length;
    COL = mat[0].length;

    Point src = new Point(0, 3);
    Point dest = new Point(3, 0);

    pathMoves(mat, src, dest);
}
}

// This code is contributed by Kingash
```

## **蟒蛇 3**

```
# Python3 program for the above approach
from collections import deque

# Stores the coordinates
# of the matrix cell
class Point:
    def __init__(self, xx, yy):
        self.x = xx
        self.y = yy

# Stores coordinates of
# a cell and its distance
class Node:
    def __init__(self, P, d):
        self.pt = P
        self.dist = d

# Check if the given cell is valid or not
def isValid(row, col):
    return (row >= 0) and (col >= 0) and (row < 4) and (col < 4)

# Stores the moves of the directions of adjacent cells
dRow = [-1, 0, 0, 1]
dCol = [0, -1, 1, 0]

# Function to find the shortest path from the
# source to destination in the given  matrix
def pathMoves(mat, src, dest):

    # Stores the distance for each
    # cell from the source cell
    d = [[ -1 for i in range(4)] for i in range(4)]

    # Distance of source cell is 0
    d[src.x][src.y] = 0

    # Initialize a visited array
    visited = [[ False for i in range(4)] for i in range(4)]
    # memset(visited, false, sizeof visited)

    # Mark source cell as visited
    visited[src.x][src.y] = True

    # Create a queue for BFS
    q = deque()

    # Distance of source cell is 0
    s = Node(src, 0)

    # Enqueue source cell
    q.append(s)

    # Keeps track of whether
    # destination is reached or not
    ok = False

    # Iterate until queue is not empty
    while (len(q)>0):

        # Deque front of the queue
        curr = q.popleft()
        pt = curr.pt

        # If the destination cell is
        # reached, then find the path
        if (pt.x == dest.x and pt.y == dest.y):
            xx, yy = pt.x, pt.y
            dist = curr.dist

            # Assign the distance of
            # destination to the
            # distance matrix
            d[pt.x][pt.y] = dist

            # Stores the smallest path
            pathmoves = ""

            # Iterate until source is reached
            while (xx != src.x or yy != src.y):

                # Append D
                if (xx > 0 and d[xx - 1][yy] == dist - 1):
                    pathmoves += 'D'
                    xx -= 1

                # Append U
                if (xx < 4 - 1 and d[xx + 1][yy] == dist - 1):
                    pathmoves += 'U'
                    xx += 1

                # Append R
                if (yy > 0 and d[xx][yy - 1] == dist - 1):
                    pathmoves += 'R'
                    yy -= 1

                # Append L
                if (yy < 4 - 1 and d[xx][yy + 1] == dist - 1):
                    pathmoves += 'L'
                    yy += 1
                dist -= 1

            # Reverse the backtracked path
            pathmoves =  pathmoves[::-1]

            print(pathmoves, end = "")
            ok = True
            break

        # Pop the start of queue
        # q.pop()

        # Explore all adjacent directions
        for i in range(4):
            row = pt.x + dRow[i]
            col = pt.y + dCol[i]

            # If the current cell is valid
            # cell and can be traversed
            if (isValid(row, col) and (mat[row][col] == '1' or mat[row][col] == 's' or mat[row][col] == 'd') and (not visited[row][col])):

                # Mark the adjacent cells as visited
                visited[row][col] = True

                # Enqueue the adjacent cells
                adjCell = Node( Point(row, col), curr.dist + 1)
                q.append(adjCell)

                # Update the distance
                # of the adjacent cells
                d[row][col] = curr.dist + 1

    # If the destination
    # is not reachable
    if (not ok):
        print(-1)

# Driver Code
if __name__ == '__main__':
    mat =[ ['0', '1', '0', '1'],
          [ '1', '0', '1', '1'],
          [ '0', '1', '1', '1'],
          [ '1', '1', '1', '0']]

    src = Point(0, 3)
    dest = Point(3, 0)

    pathMoves(mat, src, dest)

# This code is contributed by mohit kumar 29.
```

## **C#**

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

static int ROW;
static int COL;

// Stores the coordinates
// of the matrix cell
class Point
{
    public int x, y;
};

static Point newPoint(int x, int y)
{
    Point temp = new Point();
    temp.x = x;
    temp.y = y;
    return temp;
}

// Stores coordinates of
// a cell and its distance
class Node
{
    public Point pt;
    public int dist;
};

static Node newNode(Point p, int dist)
{
    Node temp = new Node();
    temp.pt = p;
    temp.dist = dist;
    return temp;
}

// Check if the given cell is valid or not
static bool isValid(int row, int col)
{
    return (row >= 0) && (col >= 0) &&
          (row < ROW) && (col < COL);
}

// Stores the moves of the directions
// of adjacent cells
static int []dRow = { -1, 0, 0, 1 };
static int []dCol = { 0, -1, 1, 0 };

// Function to find the shortest path from the
// source to destination in the given  matrix
static void pathMoves(char [,]mat, Point src,
                      Point dest)
{

    // Stores the distance for each
    // cell from the source cell
    int [,]d = new int[ROW, COL];
    for(int i = 0; i < ROW; i++)
    {
        for(int j = 0; j < COL; j++)
            d[i, j] = -1;
    }

    // Distance of source cell is 0
    d[src.x, src.y] = 0;

    // Initialize a visited array
    bool [,]visited = new bool[ROW, COL];

    // Mark source cell as visited
    visited[src.x, src.y] = true;

    // Create a queue for BFS
    Queue<Node> q = new Queue<Node>();

    // Distance of source cell is 0
    Node s = newNode(src, 0);

    // Enqueue source cell
    q.Enqueue(s);

    // Keeps track of whether
    // destination is reached or not
    bool ok = false;

    // Iterate until queue is not empty
    while (q.Count > 0)
    {

        // Deque front of the queue
        Node curr = q.Peek();
        q.Dequeue();
        Point pt = curr.pt;

        // If the destination cell is
        // reached, then find the path
        if (pt.x == dest.x && pt.y == dest.y)
        {
            int xx = pt.x, yy = pt.y;
            int dist = curr.dist;

            // Assign the distance of
            // destination to the
            // distance matrix
            d[pt.x,pt.y] = dist;

            // Stores the smallest path
            string pathmoves = "";

            // Iterate until source is reached
            while (xx != src.x || yy != src.y)
            {

                // Append D
                if (xx > 0 &&
                  d[xx - 1, yy] == dist - 1)
                {
                    pathmoves += 'D';
                    xx--;
                }

                // Append U
                if (xx < ROW - 1 &&
                    d[xx + 1, yy] == dist - 1)
                {
                    pathmoves += 'U';
                    xx++;
                }

                // Append R
                if (yy > 0 &&
                    d[xx, yy - 1] == dist - 1)
                {
                    pathmoves += 'R';
                    yy--;
                }

                // Append L
                if (yy < COL - 1 &&
                    d[xx, yy + 1] == dist - 1)
                {
                    pathmoves += 'L';
                    yy++;
                }
                dist--;
            }

            // Print reverse the backtracked path
            for(int i = pathmoves.Length - 1;
                    i >= 0; --i)
                Console.Write(pathmoves[i]);

            ok = true;
            break;
        }

        // Pop the start of queue
        if (q.Count > 0)
        {
            q.Peek();
            q.Dequeue();
        }

        // Explore all adjacent directions
        for(int i = 0; i < 4; i++)
        {
            int row = pt.x + dRow[i];
            int col = pt.y + dCol[i];

            // If the current cell is valid
            // cell and can be traversed
            if (isValid(row, col) &&
                   (mat[row, col] == '1' ||
                    mat[row, col] == 's' ||
                    mat[row, col] == 'd') &&
               !visited[row, col])
            {

                // Mark the adjacent cells as visited
                visited[row,col] = true;

                // Enqueue the adjacent cells
                Node adjCell = newNode(newPoint(row, col),
                                       curr.dist + 1);
                q.Enqueue(adjCell);

                // Update the distance
                // of the adjacent cells
                d[row, col] = curr.dist + 1;
            }
        }
    }

    // If the destination
    // is not reachable
    if (ok == false)
        Console.Write(-1);
}

// Driver Code
public static void Main()
{
    char [,]mat = { { '0', '1', '0', '1' },
                    { '1', '0', '1', '1' },
                    { '0', '1', '1', '1' },
                    { '1', '1', '1', '0' } };

    ROW = mat.GetLength(0);
    COL = mat.GetLength(0);

    Point src = newPoint(0, 3);
    Point dest = newPoint(3, 0);

    pathMoves(mat, src, dest);
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## **java 描述语言**

```
<script>

// Javascript program for the above approach

var ROW = 0;
var COL = 0;

// Stores the coordinates
// of the matrix cell
class Point
{
    constructor()
    {
        this.x = 0;
        this.y = 0;
    }
};

function newPoint(x, y)
{
    var temp = new Point();
    temp.x = x;
    temp.y = y;
    return temp;
}

// Stores coordinates of
// a cell and its distance
class Node
{
    constructor()
    {
        this.pt = null;
        this.dist = 0;
    }
};

function newNode(p, dist)
{
    var temp = new Node();
    temp.pt = p;
    temp.dist = dist;
    return temp;
}

// Check if the given cell is valid or not
function isValid(row, col)
{
    return (row >= 0) && (col >= 0) &&
          (row < ROW) && (col < COL);
}

// Stores the moves of the directions
// of adjacent cells
var dRow = [-1, 0, 0, 1];
var dCol = [0, -1, 1, 0];

// Function to find the shortest path from the
// source to destination in the given  matrix
function pathMoves(mat, src, dest)
{

    // Stores the distance for each
    // cell from the source cell
    var d = Array.from(Array(ROW), ()=>Array(COL));
    for(var i = 0; i < ROW; i++)
    {
        for(var j = 0; j < COL; j++)
            d[i][j] = -1;
    }

    // Distance of source cell is 0
    d[src.x][src.y] = 0;

    // Initialize a visited array
    var visited = Array.from(Array(ROW), ()=>Array(COL));

    // Mark source cell as visited
    visited[src.x][src.y] = true;

    // Create a queue for BFS
    var q = [];

    // Distance of source cell is 0
    var s = newNode(src, 0);

    // push source cell
    q.push(s);

    // Keeps track of whether
    // destination is reached or not
    var ok = false;

    // Iterate until queue is not empty
    while (q.length > 0)
    {

        // Deque front of the queue
        var curr = q[0];
        q.shift();
        var pt = curr.pt;

        // If the destination cell is
        // reached, then find the path
        if (pt.x == dest.x && pt.y == dest.y)
        {
            var xx = pt.x, yy = pt.y;
            var dist = curr.dist;

            // Assign the distance of
            // destination to the
            // distance matrix
            d[pt.x][pt.y] = dist;

            // Stores the smallest path
            var pathmoves = "";

            // Iterate until source is reached
            while (xx != src.x || yy != src.y)
            {

                // Append D
                if (xx > 0 &&
                  d[xx - 1][yy] == dist - 1)
                {
                    pathmoves += 'D';
                    xx--;
                }

                // Append U
                if (xx < ROW - 1 &&
                    d[xx + 1][yy] == dist - 1)
                {
                    pathmoves += 'U';
                    xx++;
                }

                // Append R
                if (yy > 0 &&
                    d[xx][yy - 1] == dist - 1)
                {
                    pathmoves += 'R';
                    yy--;
                }

                // Append L
                if (yy < COL - 1 &&
                    d[xx][yy + 1] == dist - 1)
                {
                    pathmoves += 'L';
                    yy++;
                }
                dist--;
            }

            // Print reverse the backtracked path
            for(var i = pathmoves.length - 1;
                    i >= 0; --i)
                document.write(pathmoves[i]);

            ok = true;
            break;
        }

        // Pop the start of queue
        if (q.length > 0)
        {
            q.shift();
        }

        // Explore all adjacent directions
        for(var i = 0; i < 4; i++)
        {
            var row = pt.x + dRow[i];
            var col = pt.y + dCol[i];

            // If the current cell is valid
            // cell and can be traversed
            if (isValid(row, col) &&
                   (mat[row][col] == '1' ||
                    mat[row][col] == 's' ||
                    mat[row][col] == 'd') &&
               !visited[row][col])
            {

                // Mark the adjacent cells as visited
                visited[row][col] = true;

                // Enqueue the adjacent cells
                var adjCell = newNode(newPoint(row, col),
                                       curr.dist + 1);
                q.push(adjCell);

                // Update the distance
                // of the adjacent cells
                d[row][col] = curr.dist + 1;
            }
        }
    }

    // If the destination
    // is not reachable
    if (ok == false)
        document.write(-1);
}

// Driver Code
var mat = [ [ '0', '1', '0', '1' ],
                [ '1', '0', '1', '1' ],
                [ '0', '1', '1', '1' ],
                [ '1', '1', '1', '0' ] ];
ROW = mat.length;
COL = mat[0].length;
var src = newPoint(0, 3);
var dest = newPoint(3, 0);
pathMoves(mat, src, dest);

// This code is contributed by rutvik_56.
</script>
```

****Output:** 

```
DLDLDL
```** 

*****时间复杂度:** O(N*M)*
***辅助空间:** O(N*M)***