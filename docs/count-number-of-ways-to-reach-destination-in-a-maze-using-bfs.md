# 使用 BFS 计算迷宫中到达目的地的路数

> 原文:[https://www . geesforgeks . org/count-到达迷宫中目的地的路数-使用-bfs/](https://www.geeksforgeeks.org/count-number-of-ways-to-reach-destination-in-a-maze-using-bfs/)

给定一个有障碍物的迷宫，计算从最上面最左边的单元格到达最右边最下面的单元格的路径数。给定迷宫中的一个单元如果是阻塞或死胡同，则值为-1，否则为 0。
从给定的单元格开始，我们只允许移动到单元格(i+1，j)和(I，j+1)。

**示例:**

> **输入:** mat[][] = {
> {1，0，0，1}，
> {1，1，1，1}，
> {1，0，1，1}}
> **输出:** 2
> 
> **输入:** mat[][] = {
> {1，1，1，1}，
> {1，0，1，1}，
> {0，1，1，1}，
> {1，1，1，1}}
> **输出:** 4

**方法:**想法是使用[队列](https://www.geeksforgeeks.org/queue-data-structure/)并应用 [bfs](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) 并使用变量**计数**来存储可能路径的数量。制作一对行和列，并将(0，0)插入队列。现在继续从队列中弹出对，如果弹出的值是矩阵的末尾，则递增**计数**，否则检查下一列是否能给出有效的移动或下一行是否能给出有效的移动，并根据这一点，将相应的行、列对插入队列。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

#define m 4
#define n 3

// Function to return the number of valid
// paths in the given maze
int Maze(int matrix[n][m])
{
    queue<pair<int, int> > q;

    // Insert the starting point i.e.
    // (0, 0) in the queue
    q.push(make_pair(0, 0));

    // To store the count of possible paths
    int count = 0;

    while (!q.empty()) {
        pair<int, int> p = q.front();
        q.pop();

        // Increment the count of paths since
        // it is the destination
        if (p.first == n - 1 && p.second == m - 1)
            count++;

        // If moving to the next row is a valid move
        if (p.first + 1 < n
            && matrix[p.first + 1][p.second] == 1) {
            q.push(make_pair(p.first + 1, p.second));
        }

        // If moving to the next column is a valid move
        if (p.second + 1 < m
            && matrix[p.first][p.second + 1] == 1) {
            q.push(make_pair(p.first, p.second + 1));
        }
    }

    return count;
}

// Driver code
int main()
{
    // Matrix to represent maze
    int matrix[n][m] = { { 1, 0, 0, 1 },
                         { 1, 1, 1, 1 },
                         { 1, 0, 1, 1 } };

    cout << Maze(matrix);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
class GFG
{
static int m = 4;
static int n = 3;
static class pair
{
    int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to return the number of valid
// paths in the given maze
static int Maze(int matrix[][])
{
    Queue<pair> q = new LinkedList<>();

    // Insert the starting point i.e.
    // (0, 0) in the queue
    q.add(new pair(0, 0));

    // To store the count of possible paths
    int count = 0;

    while (!q.isEmpty())
    {
        pair p = q.peek();
        q.remove();

        // Increment the count of paths since
        // it is the destination
        if (p.first == n - 1 && p.second == m - 1)
            count++;

        // If moving to the next row is a valid move
        if (p.first + 1 < n &&
            matrix[p.first + 1][p.second] == 1)
        {
            q.add(new pair(p.first + 1, p.second));
        }

        // If moving to the next column is a valid move
        if (p.second + 1 < m &&
            matrix[p.first][p.second + 1] == 1)
        {
            q.add(new pair(p.first, p.second + 1));
        }
    }
    return count;
}

// Driver code
public static void main(String[] args)
{
    // Matrix to represent maze
    int matrix[][] = {{ 1, 0, 0, 1 },
                      { 1, 1, 1, 1 },
                      { 1, 0, 1, 1 }};

    System.out.println(Maze(matrix));
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from collections import deque
m = 4
n = 3

# Function to return the number of valid
# paths in the given maze
def Maze(matrix):
    q = deque()

    # Insert the starting poi.e.
    # (0, 0) in the queue
    q.append((0, 0))

    # To store the count of possible paths
    count = 0

    while (len(q) > 0):
        p = q.popleft()

        # Increment the count of paths since
        # it is the destination
        if (p[0] == n - 1 and p[1] == m - 1):
            count += 1

        # If moving to the next row is a valid move
        if (p[0] + 1 < n and
            matrix[p[0] + 1][p[1]] == 1):
            q.append((p[0] + 1, p[1]))

        # If moving to the next column is a valid move
        if (p[1] + 1 < m and
            matrix[p[0]][p[1] + 1] == 1):
            q.append((p[0], p[1] + 1))

    return count

# Driver code

# Matrix to represent maze
matrix = [ [ 1, 0, 0, 1 ],
           [ 1, 1, 1, 1 ],
           [ 1, 0, 1, 1 ] ]

print(Maze(matrix))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{
static int m = 4;
static int n = 3;
class pair
{
    public int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to return the number of valid
// paths in the given maze
static int Maze(int [,]matrix)
{
    Queue<pair> q = new Queue<pair>();

    // Insert the starting point i.e.
    // (0, 0) in the queue
    q.Enqueue(new pair(0, 0));

    // To store the count of possible paths
    int count = 0;

    while (q.Count != 0)
    {
        pair p = q.Peek();
        q.Dequeue();

        // Increment the count of paths since
        // it is the destination
        if (p.first == n - 1 && p.second == m - 1)
            count++;

        // If moving to the next row is a valid move
        if (p.first + 1 < n &&
            matrix[p.first + 1, p.second] == 1)
        {
            q.Enqueue(new pair(p.first + 1, p.second));
        }

        // If moving to the next column is a valid move
        if (p.second + 1 < m &&
            matrix[p.first, p.second + 1] == 1)
        {
            q.Enqueue(new pair(p.first, p.second + 1));
        }
    }
    return count;
}

// Driver code
public static void Main(String[] args)
{
    // Matrix to represent maze
    int [,]matrix = {{ 1, 0, 0, 1 },
                     { 1, 1, 1, 1 },
                     { 1, 0, 1, 1 }};

    Console.WriteLine(Maze(matrix));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript implementation of the approach
var m = 4;
var n = 3;

// Function to return the number of valid
// paths in the given maze
function Maze(matrix)
{
    var q = [];

    // Insert the starting point i.e.
    // (0, 0) in the queue
    q.push([0, 0]);

    // To store the count of possible paths
    var count = 0;

    while (q.length != 0)
    {
        var p = q[0];
        q.shift();

        // Increment the count of paths since
        // it is the destination
        if (p[0] == n - 1 && p[1] == m - 1)
            count++;

        // If moving to the next row is a valid move
        if (p[0] + 1 < n &&
            matrix[p[0] + 1][p[1]] == 1)
        {
            q.push([p[0] + 1, p[1]]);
        }

        // If moving to the next column is a valid move
        if (p[1] + 1 < m &&
            matrix[p[0]][p[1] + 1] == 1)
        {
            q.push([p[0], p[1] + 1]);
        }
    }
    return count;
}

// Driver code

// Matrix to represent maze
var matrix = [ [ 1, 0, 0, 1 ],
               [ 1, 1, 1, 1 ],
               [ 1, 0, 1, 1 ] ];

document.write( Maze(matrix));

// This code is contributed by rutvik_56

</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(N * M)。
**辅助空间** : O(N * M)。