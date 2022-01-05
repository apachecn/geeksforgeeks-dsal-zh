# 找到从左下角到右上角的最大成本路径

> 原文:[https://www . geesforgeks . org/find-最大成本-路径-从左下角到右上角/](https://www.geeksforgeeks.org/find-the-maximum-cost-path-from-the-bottom-left-corner-to-the-top-right-corner/)

给定一个二维网格，其中每个单元包含整数成本，该成本表示遍历该单元的成本。任务是找到从左下角到右上角的最大成本路径。
**注意:**只使用上、右移

**示例:**

```
Input : mat[][] = {{20, -10, 0}, 
                   {1, 5, 10}, 
                   {1, 2, 3}}
Output : 18
(2, 0) ==> (2, 1) ==> (1, 1) ==> (1, 2) ==> (0, 2)  
cost for this path is (1+2+5+10+0) = 18

Input : mat[][] = {{1, -2, -3}, 
                   {1, 15, 10},
                   {1, -2, 3}}
Output : 24
```

**先决条件:** [允许向左、向右、向下和向上移动的最小成本路径](https://www.geeksforgeeks.org/minimum-cost-path-left-right-bottom-moves-allowed/)
**方法:**想法是使用[队列](https://www.geeksforgeeks.org/queue-data-structure/)维护一个单独的数组来存储所有单元的最大成本。对于每个单元，检查到达该单元的当前成本是否大于之前的成本。如果以前的成本最小，则用当前成本更新单元格。

下面是上述方法的实现:

## C++

```
// C++ program to find maximum cost to reach
// top right corner from bottom left corner
#include <bits/stdc++.h>
using namespace std;

#define ROW 3
#define COL 3

// To store matrix cell coordinates
struct Point
{
    int x;
    int y;
};

// Check whether given cell (row, col)
// is a valid cell or not.
bool isValid(Point p)
{
    // Return true if row number and column number
    // is in range
    return (p.x >=0) && (p.y <COL);
}

// Function to find maximum cost to reach
// top right corner from bottom left corner
int find_max_cost(int mat[][COL])
{
    int max_val[ROW][COL];
    memset(max_val, 0, sizeof max_val);
        max_val[ROW-1][0] = mat[ROW-1][0];

    // Starting point   
    Point src = {ROW-1,0};

    // Create a queue for traversal
    queue<Point> q;

    q.push(src); // Enqueue source cell

    // Do a BFS starting from source cell
    // on the allowed direction
    while (!q.empty())
    {
        Point curr = q.front();
        q.pop();

        // Find up point
        Point up = {curr.x-1, curr.y};

        // if adjacent cell is valid, enqueue it.
        if (isValid(up))
        {
            max_val[up.x][up.y] = max(max_val[up.x][up.y],
                 mat[up.x][up.y] + max_val[curr.x][curr.y]);
            q.push(up);
        }

        // Find right point   
        Point right = {curr.x, curr.y+1};

        if(isValid(right))
        {
            max_val[right.x][right.y] = max(max_val[right.x][right.y],
                mat[right.x][right.y] + max_val[curr.x][curr.y]);
            q.push(right);
        }

    }

    // Return the required answer
    return max_val[0][COL-1];
}

// Driver code
int main()
{
    int mat[ROW][COL] = { {20, -10, 0},
                          {1, 5, 10},
                          {1, 2, 3},};

    std::cout<<"Given matrix is "<<endl;

    for(int i = 0 ; i<ROW;++i)
    {
        for(int j =0; j<COL; ++j)
            std::cout<<mat[i][j]<<" ";

        std::cout<<endl;
    }

    std::cout<<"Maximum cost is " << find_max_cost(mat);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum cost to reach
// top right corner from bottom left corner
import java.util.*;
class GFG
{
static int ROW = 3;
static int COL = 3;

// To store matrix cell coordinates
static class Point
{
    int x;
    int y;

    public Point(int x, int y)
    {
        this.x = x;
        this.y = y;
    }
}

// Check whether given cell (row, col)
// is a valid cell or not.
static boolean isValid(Point p)
{
    // Return true if row number and column number
    // is in range
    return (p.x >= 0) && (p.y < COL);
}

// Function to find maximum cost to reach
// top right corner from bottom left corner
static int find_max_cost(int mat[][])
{
    int [][]max_val = new int[ROW][COL];
    max_val[ROW - 1][0] = mat[ROW - 1][0];

    // Starting point
    Point src = new Point(ROW - 1, 0);

    // Create a queue for traversal
    Queue<Point> q = new LinkedList<>();

    q.add(src); // Enqueue source cell

    // Do a BFS starting from source cell
    // on the allowed direction
    while (!q.isEmpty())
    {
        Point curr = q.peek();
        q.remove();

        // Find up point
        Point up = new Point(curr.x - 1, curr.y);

        // if adjacent cell is valid, enqueue it.
        if (isValid(up))
        {
            max_val[up.x][up.y] = Math.max(max_val[up.x][up.y],
                mat[up.x][up.y] + max_val[curr.x][curr.y]);
            q.add(up);
        }

        // Find right point
        Point right = new Point(curr.x, curr.y + 1);

        if(isValid(right))
        {
            max_val[right.x][right.y] = Math.max(max_val[right.x][right.y],
                mat[right.x][right.y] + max_val[curr.x][curr.y]);
            q.add(right);
        }
    }

    // Return the required answer
    return max_val[0][COL - 1];
}

// Driver code
public static void main(String[] args)
{
    int mat[][] = {{20, -10, 0},
                   {1, 5, 10},
                   {1, 2, 3}};

    System.out.println("Given matrix is ");

    for(int i = 0 ; i < ROW; ++i)
    {
        for(int j = 0; j < COL; ++j)
            System.out.print(mat[i][j] + " ");

        System.out.println();
    }

    System.out.print("Maximum cost is " +
                     find_max_cost(mat));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to find maximum cost to reach
# top right corner from bottom left corner
from collections import deque as queue

ROW = 3
COL = 3

# Check whether given cell (row, col)
# is a valid cell or not.
def isValid(p):

    # Return true if row number and column number
    # is in range
    return (p[0] >= 0) and (p[1] < COL)

# Function to find maximum cost to reach
# top right corner from bottom left corner
def find_max_cost(mat):
    max_val = [[0 for i in range(COL)] for i in range(ROW)]

    max_val[ROW - 1][0] = mat[ROW - 1][0]

    # Starting po
    src = [ROW - 1, 0]

    # Create a queue for traversal
    q = queue()

    q.appendleft(src) # Enqueue source cell

    # Do a BFS starting from source cell
    # on the allowed direction
    while (len(q) > 0):
        curr = q.pop()

        # Find up point
        up = [curr[0] - 1, curr[1]]

        # if adjacent cell is valid, enqueue it.
        if (isValid(up)):
            max_val[up[0]][up[1]] = max(max_val[up[0]][up[1]],mat[up[0]][up[1]] + max_val[curr[0]][curr[1]])
            q.appendleft(up)

        # Find right po
        right = [curr[0], curr[1] + 1]

        if(isValid(right)):
            max_val[right[0]][right[1]] = max(max_val[right[0]][right[1]],mat[right[0]][right[1]] + max_val[curr[0]][curr[1]])
            q.appendleft(right)

    # Return the required answer
    return max_val[0][COL - 1]

# Driver code
mat = [[20, -10, 0],
    [1, 5, 10],
    [1, 2, 3]]

print("Given matrix is ")

for i in range(ROW):
    for j in range(COL):
        print(mat[i][j],end=" ")
    print()

print("Maximum cost is ", find_max_cost(mat))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to find maximum cost to reach
// top right corner from bottom left corner
using System;
using System.Collections.Generic;

class GFG
{

static int ROW = 3;
static int COL = 3;

// To store matrix cell coordinates
public class Point
{
    public int x;
    public int y;

    public Point(int x, int y)
    {
        this.x = x;
        this.y = y;
    }
}

// Check whether given cell (row, col)
// is a valid cell or not.
static Boolean isValid(Point p)
{
    // Return true if row number and
    // column number is in range
    return (p.x >= 0) && (p.y < COL);
}

// Function to find maximum cost to reach
// top right corner from bottom left corner
static int find_max_cost(int [,]mat)
{
    int [,]max_val = new int[ROW,COL];
    max_val[ROW - 1, 0] = mat[ROW - 1, 0];

    // Starting point
    Point src = new Point(ROW - 1, 0);

    // Create a queue for traversal
    Queue<Point> q = new Queue<Point>();

    q.Enqueue(src); // Enqueue source cell

    // Do a BFS starting from source cell
    // on the allowed direction
    while (q.Count != 0)
    {
        Point curr = q.Peek();
        q.Dequeue();

        // Find up point
        Point up = new Point(curr.x - 1, curr.y);

        // if adjacent cell is valid, enqueue it.
        if (isValid(up))
        {
            max_val[up.x, up.y] = Math.Max(max_val[up.x, up.y],
                mat[up.x, up.y] + max_val[curr.x, curr.y]);
            q.Enqueue(up);
        }

        // Find right point
        Point right = new Point(curr.x,
                                curr.y + 1);

        if(isValid(right))
        {
            max_val[right.x, right.y] = Math.Max(max_val[right.x, right.y],
                mat[right.x, right.y] + max_val[curr.x, curr.y]);
            q.Enqueue(right);
        }
    }

    // Return the required answer
    return max_val[0, COL - 1];
}

// Driver code
public static void Main(String[] args)
{
    int [,]mat = {{20, -10, 0},
                  {1, 5, 10},
                  {1, 2, 3}};

    Console.WriteLine("Given matrix is ");

    for(int i = 0 ; i < ROW; ++i)
    {
        for(int j = 0; j < COL; ++j)
            Console.Write(mat[i, j] + " ");

        Console.WriteLine();
    }

    Console.Write("Maximum cost is " +
                  find_max_cost(mat));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript program to find maximum cost to reach
// top right corner from bottom left corner
let ROW = 3;
let COL = 3;

// To store matrix cell coordinates
class Point
{
    constructor(x, y)
    {
        this.x = x;
        this.y = y;
    }
}

// Check whether given cell (row, col)
// is a valid cell or not.
function isValid(p)
{

    // Return true if row number and column
    // number is in range
    return (p.x >= 0) && (p.y < COL);
}

// Function to find maximum cost to reach
// top right corner from bottom left corner
function find_max_cost(mat)
{
    let max_val = new Array(ROW);
    for(let i = 0; i < ROW; i++)
    {
        max_val[i] = new Array(COL);
        for(let j = 0; j < COL; j++)
        {
            max_val[i][j] = 0;
        }
    }
    max_val[ROW - 1][0] = mat[ROW - 1][0];

    // Starting point
    let src = new Point(ROW - 1, 0);

    // Create a queue for traversal
    let q = [];

    // Enqueue source cell
    q.push(src);

    // Do a BFS starting from source cell
    // on the allowed direction
    while (q.length != 0)
    {
        let curr = q.shift();

        // Find up point
        let up = new Point(curr.x - 1, curr.y);

        // If adjacent cell is valid, enqueue it.
        if (isValid(up))
        {
            max_val[up.x][up.y] = Math.max(max_val[up.x][up.y],
                mat[up.x][up.y] + max_val[curr.x][curr.y]);
            q.push(up);
        }

        // Find right point
        let right = new Point(curr.x, curr.y + 1);

        if(isValid(right))
        {
            max_val[right.x][right.y] = Math.max(max_val[right.x][right.y],
                mat[right.x][right.y] + max_val[curr.x][curr.y]);
            q.push(right);
        }
    }

    // Return the required answer
    return max_val[0][COL - 1];
}

// Driver code
let mat = [ [ 20, -10, 0 ],
            [ 1, 5, 10 ],
            [ 1, 2, 3 ] ];

document.write("Given matrix is <br>");

for(let i = 0; i < ROW; ++i)
{
    for(let j = 0; j < COL; ++j)
        document.write(mat[i][j] + " ");

    document.write("<br>");
}

document.write("Maximum cost is " +
               find_max_cost(mat));

// This code is contributed by patel2127

</script>
```

**Output:** 

```
Given matrix is 
20 -10 0 
1 5 10 
1 2 3 
Maximum cost is 18
```

**时间复杂度:**O(ROW * COL)
T3】辅助空间: O(ROW * COL)