# 矩阵所有相连的非空单元格的大小

> 原文:[https://www . geeksforgeeks . org/所有连接的非空矩阵单元的大小/](https://www.geeksforgeeks.org/size-of-all-connected-non-empty-cells-of-a-matrix/)

给定一个二进制矩阵 **mat[][]** ，任务是找出所有可能的非空连通单元的大小。

> 空单元由 **0** 表示，而非空单元由 **1** 表示。
> 如果两个电池在水平或垂直方向上相邻，即**mat[I][j]= mat[I][j–1]**或 **mat[i][j] = mat[i][j + 1]** 或**mat[I][j]= mat[I–1][j]**或 **mat[i][j] = mat[i + 1][j]** ，则称它们是相连的。

**示例:**

> **输入:** mat[][] = {{1，1，0，0，0，0}，{0，1，0，0，1}，{1，0，0，1，1}，{0，0，0，0，0，0，0}，{1，0，1，0，0，1}}
> **输出:** 3 3 1 1 1 1
> **解释:**
> {mat[0][0]，mat[0][1]，mat[1][1]}，{ mat
> 
>  ****输入:** mat[][] = {{1，1，0，0，0，0}，{1，1，0，1，1}，{1，0，0，1，1}，{0，0，0，0，0，0}，{0，0，1，1，1，1，1}}
> **输出:** 5 4 3**

****进场:**
思路是在矩阵上使用 [BFS](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/) 和[递归](https://www.geeksforgeeks.org/recursion/)。
按照以下步骤操作:**

*   **初始化一个[队列数据结构](https://www.geeksforgeeks.org/queue-data-structure/)并插入一个单元( **mat[i][j] = 1** )。**
*   **对插入的像元执行 **BFS** ，并遍历其相邻的像元。**
*   **检查边界条件，检查当前元素是否为 **1** ，然后翻转到 **0** 。**
*   **标记已访问的单元格，并更新已连接的非空单元格的大小。**
*   **最后，打印获得的所有连接尺寸。**

**下面是上述方法的实现:**

## **C++14**

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find size of all the
// islands from the given matrix
int BFS(vector<vector<int> >& mat,
        int row, int col)
{
    int area = 0;

    // Initialize a queue for
    // the BFS traversal
    queue<pair<int, int> > Q;
    Q.push({ row, col });

    // Iterate until the
    // queue is empty
    while (!Q.empty()) {

        // Top element of queue
        auto it = Q.front();

        // Pop the element
        Q.pop();

        int r = it.first, c = it.second;

        // Check for boundaries
        if (r < 0 || c < 0 || r > 4 || c > 4)
            continue;

        // Check if current element is 0
        if (mat[r] == 0)
            continue;

        // Check if current element is 1
        if (mat[r] == 1) {

            // Mark the cell visited
            mat[r] = 0;

            // Incrementing the size
            area++;
        }

        // Traverse all neighbors
        Q.push({ r + 1, c });
        Q.push({ r - 1, c });
        Q.push({ r, c + 1 });
        Q.push({ r, c - 1 });
    }

    // Return the answer
    return area;
}

// Function to print size of each connections
void sizeOfConnections(vector<vector<int> > mat)
{

    // Stores the size of each
    // connected non-empty
    vector<int> result;

    for (int row = 0; row < 5; ++row) {
        for (int col = 0; col < 5; ++col) {

            // Check if the cell is
            // non-empty
            if (mat[row][col] == 1) {

                // Function call
                int area = BFS(mat, row, col);
                result.push_back(area);
            }
        }
    }

    // Print the answer
    for (int val : result)
        cout << val << " ";
}

// Driver Code
int main()
{

    vector<vector<int> > mat
        = { { 1, 1, 0, 0, 0 },
            { 1, 1, 0, 1, 1 },
            { 1, 0, 0, 1, 1 },
            { 1, 0, 0, 0, 0 },
            { 0, 0, 1, 1, 1 } };

    sizeOfConnections(mat);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program to implement
// the above approach
import java.util.*;
import java.lang.*;

class GFG{

static class pair
{
    int first, second;
    pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to find size of all the
// islands from the given matrix
static int BFS(int[][] mat,
               int row, int col)
{
    int area = 0;

    // Initialize a queue for
    // the BFS traversal
    Queue<pair> Q = new LinkedList<>();
    Q.add(new pair(row, col));

    // Iterate until the
    // queue is empty
    while (!Q.isEmpty())
    {

        // Top element of queue
        pair it = Q.peek();

        // Pop the element
        Q.poll();

        int r = it.first, c = it.second;

        // Check for boundaries
        if (r < 0 || c < 0 ||
            r > 4 || c > 4)
            continue;

        // Check if current element is 0
        if (mat[r] == 0)
            continue;

        // Check if current element is 1
        if (mat[r] == 1)
        {

            // Mark the cell visited
            mat[r] = 0;

            // Incrementing the size
            area++;
        }

        // Traverse all neighbors
        Q.add(new pair(r + 1, c));
        Q.add(new pair(r - 1, c));
        Q.add(new pair(r, c + 1));
        Q.add(new pair(r, c - 1));
    }

    // Return the answer
    return area;
}

// Function to print size of each connections
static void sizeOfConnections(int[][] mat)
{

    // Stores the size of each
    // connected non-empty
    ArrayList<Integer> result = new ArrayList<>();

    for(int row = 0; row < 5; ++row)
    {
        for(int col = 0; col < 5; ++col)
        {

            // Check if the cell is
            // non-empty
            if (mat[row][col] == 1)
            {

                // Function call
                int area = BFS(mat, row, col);
                result.add(area);
            }
        }
    }

    // Print the answer
    for(int val : result)
       System.out.print(val + " ");
}

// Driver code
public static void main (String[] args)
{
    int[][] mat = { { 1, 1, 0, 0, 0 },
                    { 1, 1, 0, 1, 1 },
                    { 1, 0, 0, 1, 1 },
                    { 1, 0, 0, 0, 0 },
                    { 0, 0, 1, 1, 1 } };

    sizeOfConnections(mat);
}
}

// This code is contributed by offbeat
```

## **蟒蛇 3**

```
# Python3 program to implement
# the above approach
from collections import deque

# Function to find size of all the
# islands from the given matrix
def BFS(mat, row, col):

    area = 0

    # Initialize a queue for
    # the BFS traversal
    Q = deque()
    Q.append([row, col])

    # Iterate until the
    # queue is empty
    while (len(Q) > 0):

        # Top element of queue
        it = Q.popleft()

        # Pop the element
        # Q.pop();
        r, c = it[0], it[1]

        # Check for boundaries
        if (r < 0 or c < 0 or r > 4 or c > 4):
            continue

        # Check if current element is 0
        if (mat[r] == 0):
            continue

        # Check if current element is 1
        if (mat[r] == 1):

            # Mark the cell visited
            mat[r] = 0

            # Incrementing the size
            area += 1

        # Traverse all neighbors
        Q.append([r + 1, c])
        Q.append([r - 1, c])
        Q.append([r, c + 1])
        Q.append([r, c - 1])

    # Return the answer
    return area

# Function to prsize of each connections
def sizeOfConnections(mat):

    # Stores the size of each
    # connected non-empty
    result = []

    for row in range(5):
        for col in range(5):

            # Check if the cell is
            # non-empty
            if (mat[row][col] == 1):

                # Function call
                area = BFS(mat, row, col);
                result.append(area)

    # Print the answer
    for val in result:
        print(val, end = " ")

# Driver Code
if __name__ == '__main__':

    mat = [ [ 1, 1, 0, 0, 0 ],
            [ 1, 1, 0, 1, 1 ],
            [ 1, 0, 0, 1, 1 ],
            [ 1, 0, 0, 0, 0 ],
            [ 0, 0, 1, 1, 1 ] ]

    sizeOfConnections(mat)

# This code is contributed by mohit kumar 29
```

## **C#**

```
// C# program to implement
// the above approach
using System;
using System.Collections;
using System.Collections.Generic;

class GFG{

class pair
{
    public int first, second;

    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to find size of all the
// islands from the given matrix
static int BFS(int[, ] mat, int row, int col)
{
    int area = 0;

    // Initialize a queue for
    // the BFS traversal
    Queue<pair> Q = new Queue<pair>();
    Q.Enqueue(new pair(row, col));

    // Iterate until the
    // queue is empty
    while (Q.Count != 0)
    {

        // Top element of queue
        pair it = Q.Peek();

        // Pop the element
        Q.Dequeue();

        int r = it.first, c = it.second;

        // Check for boundaries
        if (r < 0 || c < 0 || r > 4 || c > 4)
            continue;

        // Check if current element is 0
        if (mat[r, c] == 0)
            continue;

        // Check if current element is 1
        if (mat[r, c] == 1)
        {

            // Mark the cell visited
            mat[r, c] = 0;

            // Incrementing the size
            area++;
        }

        // Traverse all neighbors
        Q.Enqueue(new pair(r + 1, c));
        Q.Enqueue(new pair(r - 1, c));
        Q.Enqueue(new pair(r, c + 1));
        Q.Enqueue(new pair(r, c - 1));
    }

    // Return the answer
    return area;
}

// Function to print size of each connections
static void sizeOfConnections(int[,] mat)
{

    // Stores the size of each
    // connected non-empty
    ArrayList result = new ArrayList();

    for(int row = 0; row < 5; ++row)
    {
        for(int col = 0; col < 5; ++col)
        {

            // Check if the cell is
            // non-empty
            if (mat[row, col] == 1)
            {

                // Function call
                int area = BFS(mat, row, col);
                result.Add(area);
            }
        }
    }

    // Print the answer
    foreach(int val in result)
        Console.Write(val + " ");
}

// Driver code
public static void Main(string[] args)
{
    int[, ] mat = { { 1, 1, 0, 0, 0 },
                    { 1, 1, 0, 1, 1 },
                    { 1, 0, 0, 1, 1 },
                    { 1, 0, 0, 0, 0 },
                    { 0, 0, 1, 1, 1 } };

    sizeOfConnections(mat);
}
}

// This code is contributed by grand_master
```

## **java 描述语言**

```
<script>

// Javascript program to implement
// the above approach

class pair
{
    constructor(first, second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to find size of all the
// islands from the given matrix
function BFS(mat, row, col)
{
    var area = 0;

    // Initialize a queue for
    // the BFS traversal
    var Q = [];
    Q.push(new pair(row, col));

    // Iterate until the
    // queue is empty
    while (Q.length != 0)
    {

        // Top element of queue
        var it = Q[0];

        // Pop the element
        Q.shift();

        var r = it.first, c = it.second;

        // Check for boundaries
        if (r < 0 || c < 0 || r > 4 || c > 4)
            continue;

        // Check if current element is 0
        if (mat[r][ c] == 0)
            continue;

        // Check if current element is 1
        if (mat[r] == 1)
        {

            // Mark the cell visited
            mat[r] = 0;

            // Incrementing the size
            area++;
        }

        // Traverse all neighbors
        Q.push(new pair(r + 1, c));
        Q.push(new pair(r - 1, c));
        Q.push(new pair(r, c + 1));
        Q.push(new pair(r, c - 1));
    }

    // Return the answer
    return area;
}

// Function to print size of each connections
function sizeOfConnections(mat)
{

    // Stores the size of each
    // connected non-empty
    var result = [];

    for(var row = 0; row < 5; ++row)
    {
        for(var col = 0; col < 5; ++col)
        {

            // Check if the cell is
            // non-empty
            if (mat[row][col] == 1)
            {

                // Function call
                var area = BFS(mat, row, col);
                result.push(area);
            }
        }
    }

    // Print the answer
    for(var val of result)
        document.write(val + " ");
}

// Driver code
var mat = [ [ 1, 1, 0, 0, 0 ],
                [ 1, 1, 0, 1, 1 ],
                [ 1, 0, 0, 1, 1 ],
                [ 1, 0, 0, 0, 0 ],
                [ 0, 0, 1, 1, 1 ] ];
sizeOfConnections(mat);

</script>
```

****Output:** 

```
6 4 3
```** 

*****时间复杂度:** O(行* col)*
***辅助空间:** O(行* col)***