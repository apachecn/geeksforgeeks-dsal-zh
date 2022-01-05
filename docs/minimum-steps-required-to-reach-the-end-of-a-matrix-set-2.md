# 到达矩阵末端所需的最小步数|第 2 组

> 原文:[https://www . geesforgeks . org/到达矩阵集末尾所需的最少步骤-2/](https://www.geeksforgeeks.org/minimum-steps-required-to-reach-the-end-of-a-matrix-set-2/)

给定一个由正整数组成的 2d 矩阵 **mat[][]** ，任务是找到到达矩阵末端所需的最小步数。如果我们在牢房 **(i，j)** 我们可以去牢房 **(i，j + arr[i][j])** 或 **(i + arr[i][j]，j)** 。我们不能出界。如果没有路径，则打印 **-1** 。

**示例:**

> **输入:** mat[][] = {
> {2，1，2}，
> {1，1，1}，
> {1，1，1}}
> **输出:** 2
> 路径将为{0，0} - > {0，2} - > {2，2}
> 因此，我们分两步到达那里。
> **输入:** mat[][] = {
> {1，1，1}，
> {1，1，1}，
> {1，1，1}}
> **输出:** 4

**方法:**我们已经在[这篇](https://www.geeksforgeeks.org/find-minimum-steps-required-to-reach-the-end-of-a-matrix-set-1/)文章中讨论了这个问题的基于动态规划的方法。这个问题也可以使用[广度优先搜索(BFS)](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/) 解决。
算法如下:

*   将(0，0)推入队列。
*   遍历(0，0)，即推送队列中它可以访问的所有单元格。
*   重复上述步骤，即如果队列中的所有元素以前没有被访问/遍历过，则再次单独遍历它们。
*   重复，直到我们没有到达细胞(N-1，N-1)。
*   这个遍历的深度将给出到达终点所需的最小步数。

记住在遍历完一个单元格后，将其标记为已访问。为此，我们将使用 2D 布尔数组。

BFS 为什么工作？

*   整个场景可以被认为相当于一个有向图，其中每个单元最多连接到另外两个单元({i，j+arr[i][j])和{i+arr[i][j]，j})。
*   这个图没有加权。在这种情况下，BFS 可以找到最短的路径。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
#define n 3
using namespace std;

// Function to return the minimum steps
// required to reach the end of the matrix
int minSteps(int arr[][n])
{
    // Array to determine whether
    // a cell has been visited before
    bool v[n][n] = { 0 };

    // Queue for bfs
    queue<pair<int, int> > q;

    // Initializing queue
    q.push({ 0, 0 });

    // To store the depth of search
    int depth = 0;

    // BFS algorithm
    while (q.size() != 0) {

        // Current queue size
        int x = q.size();
        while (x--) {

            // Top-most element of queue
            pair<int, int> y = q.front();

            // To store index of cell
            // for simplicity
            int i = y.first, j = y.second;
            q.pop();

            // Base case
            if (v[i][j])
                continue;

            // If we reach (n-1, n-1)
            if (i == n - 1 && j == n - 1)
                return depth;

            // Marking the cell visited
            v[i][j] = 1;

            // Pushing the adjacent cells in the
            // queue that can be visited
            // from the current cell
            if (i + arr[i][j] < n)
                q.push({ i + arr[i][j], j });
            if (j + arr[i][j] < n)
                q.push({ i, j + arr[i][j] });
        }
        depth++;
    }

    return -1;
}

// Driver code
int main()
{
    int arr[n][n] = { { 1, 1, 1 },
                      { 1, 1, 1 },
                      { 1, 1, 1 } };

    cout << minSteps(arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

static int n= 3 ;
static class Pair
{
    int first , second;
    Pair(int a, int b)
    {
        first = a;
        second = b;
    }
}

// Function to return the minimum steps
// required to reach the end of the matrix
static int minSteps(int arr[][])
{
    // Array to determine whether
    // a cell has been visited before
    boolean v[][] = new boolean[n][n];

    // Queue for bfs
    Queue<Pair> q = new LinkedList<Pair>();

    // Initializing queue
    q.add(new Pair( 0, 0 ));

    // To store the depth of search
    int depth = 0;

    // BFS algorithm
    while (q.size() != 0)
    {

        // Current queue size
        int x = q.size();
        while (x-->0)
        {

            // Top-most element of queue
            Pair y = q.peek();

            // To store index of cell
            // for simplicity
            int i = y.first, j = y.second;
            q.remove();

            // Base case
            if (v[i][j])
                continue;

            // If we reach (n-1, n-1)
            if (i == n - 1 && j == n - 1)
                return depth;

            // Marking the cell visited
            v[i][j] = true;

            // Pushing the adjacent cells in the
            // queue that can be visited
            // from the current cell
            if (i + arr[i][j] < n)
                q.add(new Pair( i + arr[i][j], j ));
            if (j + arr[i][j] < n)
                q.add(new Pair( i, j + arr[i][j] ));
        }
        depth++;
    }
    return -1;
}

// Driver code
public static void main(String args[])
{
    int arr[][] = { { 1, 1, 1 },
                    { 1, 1, 1 },
                    { 1, 1, 1 } };

    System.out.println(minSteps(arr));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python 3 implementation of the approach
n = 3

# Function to return the minimum steps
# required to reach the end of the matrix
def minSteps(arr):

    # Array to determine whether
    # a cell has been visited before
    v = [[0 for i in range(n)] for j in range(n)]

    # Queue for bfs
    q = [[0,0]]

    # To store the depth of search
    depth = 0

    # BFS algorithm
    while (len(q) != 0):

        # Current queue size
        x = len(q)
        while (x > 0):

            # Top-most element of queue
            y = q[0]

            # To store index of cell
            # for simplicity
            i = y[0]
            j = y[1]
            q.remove(q[0])

            x -= 1

            # Base case
            if (v[i][j]):
                continue

            # If we reach (n-1, n-1)
            if (i == n - 1 and j == n - 1):
                return depth

            # Marking the cell visited
            v[i][j] = 1

            # Pushing the adjacent cells in the
            # queue that can be visited
            # from the current cell
            if (i + arr[i][j] < n):
                q.append([i + arr[i][j], j])
            if (j + arr[i][j] < n):
                q.append([i, j + arr[i][j]])

        depth += 1

    return -1

# Driver code
if __name__ == '__main__':
    arr = [[1, 1, 1],
            [1, 1, 1],
            [1, 1, 1]]

    print(minSteps(arr))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

static int n= 3 ;
public class Pair
{
    public int first , second;
    public Pair(int a, int b)
    {
        first = a;
        second = b;
    }
}

// Function to return the minimum steps
// required to reach the end of the matrix
static int minSteps(int [,]arr)
{
    // Array to determine whether
    // a cell has been visited before
    Boolean [,]v = new Boolean[n,n];

    // Queue for bfs
    Queue<Pair> q = new Queue<Pair>();

    // Initializing queue
    q.Enqueue(new Pair( 0, 0 ));

    // To store the depth of search
    int depth = 0;

    // BFS algorithm
    while (q.Count != 0)
    {

        // Current queue size
        int x = q.Count;
        while (x-->0)
        {

            // Top-most element of queue
            Pair y = q.Peek();

            // To store index of cell
            // for simplicity
            int i = y.first, j = y.second;
            q.Dequeue();

            // Base case
            if (v[i,j])
                continue;

            // If we reach (n-1, n-1)
            if (i == n - 1 && j == n - 1)
                return depth;

            // Marking the cell visited
            v[i,j] = true;

            // Pushing the adjacent cells in the
            // queue that can be visited
            // from the current cell
            if (i + arr[i,j] < n)
                q.Enqueue(new Pair( i + arr[i,j], j ));
            if (j + arr[i,j] < n)
                q.Enqueue(new Pair( i, j + arr[i,j] ));
        }
        depth++;
    }
    return -1;
}

// Driver code
public static void Main()
{
    int [,]arr = { { 1, 1, 1 },
                    { 1, 1, 1 },
                    { 1, 1, 1 } };

    Console.WriteLine(minSteps(arr));
}
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the approach
var n =  3;

// Function to return the minimum steps
// required to reach the end of the matrix
function minSteps(arr)
{
    // Array to determine whether
    // a cell has been visited before
    var v = Array.from(Array(n), ()=> Array(n).fill(0));

    // Queue for bfs
    var q = [];

    // Initializing queue
    q.push([0, 0 ]);

    // To store the depth of search
    var depth = 0;

    // BFS algorithm
    while (q.length != 0) {

        // Current queue size
        var x = q.length;
        while (x--) {

            // Top-most element of queue
            var y = q[0];

            // To store index of cell
            // for simplicity
            var i = y[0], j = y[1];
            q.shift();

            // Base case
            if (v[i][j])
                continue;

            // If we reach (n-1, n-1)
            if (i == n - 1 && j == n - 1)
                return depth;

            // Marking the cell visited
            v[i][j] = 1;

            // Pushing the adjacent cells in the
            // queue that can be visited
            // from the current cell
            if (i + arr[i][j] < n)
                q.push([ i + arr[i][j], j ]);
            if (j + arr[i][j] < n)
                q.push([i, j + arr[i][j] ]);
        }
        depth++;
    }

    return -1;
}

// Driver code
var arr = [ [ 1, 1, 1 ],
                  [ 1, 1, 1 ],
                  [ 1, 1, 1 ] ];
document.write( minSteps(arr));

</script>
```

**Output:** 

```
4
```

**时间复杂度:** O(n <sup>2</sup> )