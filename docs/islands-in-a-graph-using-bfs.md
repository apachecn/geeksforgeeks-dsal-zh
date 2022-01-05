# 使用 BFS 的图形中的岛屿

> 原文:[https://www.geeksforgeeks.org/islands-in-a-graph-using-bfs/](https://www.geeksforgeeks.org/islands-in-a-graph-using-bfs/)

给定一个布尔 2D 矩阵，求岛的个数。一组相连的 1 形成一个岛。例如，下面的矩阵包含 5 个岛

**示例:**

```
Input : mat[][] = {{1, 1, 0, 0, 0},
                   {0, 1, 0, 0, 1},
                   {1, 0, 0, 1, 1},
                   {0, 0, 0, 0, 0},
                   {1, 0, 1, 0, 1} 
Output : 5
```

***什么是岛？***
一组相连的 1 形成一个岛。例如，下面的矩阵包含 5 个岛

```
                        {1,  1, 0, 0, 0},
                        {0, 1, 0, 0, 1},
                        {1, 0, 0, 1, 1},
                        {0, 0, 0, 0, 0},
                        {1, 0, 1, 0, 1}
```

这是标准问题的变体:[连接组件](https://www.geeksforgeeks.org/connected-components-in-an-undirected-graph/)。无向图的连通分支是这样一个子图，其中每两个顶点通过一条路径相互连接，并且不连接到子图之外的任何其他顶点。

例如，下图显示了三个相连的组件。

![](img/6f4d30e79bc2c91466c6c30130582262.png)

所有顶点相互连接的图只有一个连通分支，由整个图组成。只有一个连通分支的图叫做强连通图。
我们已经讨论了岛屿的 [DFS 解决方案](https://www.geeksforgeeks.org/find-number-of-islands/)已经讨论过了。这个问题也可以通过在每个组件上应用 BFS()来解决。在每个 BFS()调用中，都会访问一个组件或子图。我们将在下一个未访问的部分致电 BFS。对 BFS()的呼叫数给出了连接的组件数。BFS 也可以用。

2D 矩阵中的一个单元可以连接到 8 个邻居。因此，与标准 BFS()不同，我们只处理 8 个相邻顶点。我们跟踪被访问的 1，这样它们就不会再被访问。

## C++

```
// A BFS based solution to count number of
// islands in a graph.
#include <bits/stdc++.h>
using namespace std;

// R x C matrix
#define R 5
#define C 5

// A function to check if a given cell
// (u, v) can be included in DFS
bool isSafe(int mat[R][C], int i, int j,
            bool vis[R][C])
{
    return (i >= 0) && (i < R) &&
           (j >= 0) && (j < C) &&
           (mat[i][j] && !vis[i][j]);
}

void BFS(int mat[R][C], bool vis[R][C],
         int si, int sj)
{

    // These arrays are used to get row and
    // column numbers of 8 neighbours of
    // a given cell
    int row[] = { -1, -1, -1, 0, 0, 1, 1, 1 };
    int col[] = { -1, 0, 1, -1, 1, -1, 0, 1 };

    // Simple BFS first step, we enqueue
    // source and mark it as visited
    queue<pair<int, int> > q;
    q.push(make_pair(si, sj));
    vis[si][sj] = true;

    // Next step of BFS. We take out
    // items one by one from queue and
    // enqueue their univisited adjacent
    while (!q.empty()) {

        int i = q.front().first;
        int j = q.front().second;
        q.pop();

        // Go through all 8 adjacent
        for (int k = 0; k < 8; k++) {
            if (isSafe(mat, i + row[k],
                       j + col[k], vis)) {
             vis[i + row[k]][j + col[k]] = true;
             q.push(make_pair(i + row[k], j + col[k]));
            }
        }
    }
}

// This function returns number islands (connected
// components) in a graph. It simply works as
// BFS for disconnected graph and returns count
// of BFS calls.
int countIslands(int mat[R][C])
{
    // Mark all cells as not visited
    bool vis[R][C];
    memset(vis, 0, sizeof(vis));

    // Call BFS for every unvisited vertex
    // Whenever we see an univisted vertex,
    // we increment res (number of islands)
    // also.
    int res = 0;
    for (int i = 0; i < R; i++) {
        for (int j = 0; j < C; j++) {
            if (mat[i][j] && !vis[i][j]) {
                BFS(mat, vis, i, j);
                res++;
            }
        }
    }

    return res;
}

// main function
int main()
{
    int mat[][C] = { { 1, 1, 0, 0, 0 },
                     { 0, 1, 0, 0, 1 },
                     { 1, 0, 0, 1, 1 },
                     { 0, 0, 0, 0, 0 },
                     { 1, 0, 1, 0, 1 } };

    cout << countIslands(mat);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A BFS based solution to count number of
// islands in a graph.
import java.util.*;

class GFG
{

// R x C matrix
static final int R = 5;
static final int C = 5 ;
static class pair
{
    int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// A function to check if a given cell
// (u, v) can be included in DFS
static boolean isSafe(int mat[][], int i, int j,
                       boolean vis[][])
{
    return (i >= 0) && (i < R) &&
        (j >= 0) && (j < C) &&
        (mat[i][j]==1 && !vis[i][j]);
}

static void BFS(int mat[][], boolean vis[][],
                int si, int sj)
{

    // These arrays are used to get row and
    // column numbers of 8 neighbours of
    // a given cell
    int row[] = { -1, -1, -1, 0, 0, 1, 1, 1 };
    int col[] = { -1, 0, 1, -1, 1, -1, 0, 1 };

    // Simple BFS first step, we enqueue
    // source and mark it as visited
    Queue<pair> q = new LinkedList<pair>();
    q.add(new pair(si, sj));
    vis[si][sj] = true;

    // Next step of BFS. We take out
    // items one by one from queue and
    // enqueue their univisited adjacent
    while (!q.isEmpty())
    {

        int i = q.peek().first;
        int j = q.peek().second;
        q.remove();

        // Go through all 8 adjacent
        for (int k = 0; k < 8; k++)
        {
            if (isSafe(mat, i + row[k],
                    j + col[k], vis))
            {
                vis[i + row[k]][j + col[k]] = true;
                q.add(new pair(i + row[k], j + col[k]));
            }
        }
    }
}

// This function returns number islands (connected
// components) in a graph. It simply works as
// BFS for disconnected graph and returns count
// of BFS calls.
static int countIslands(int mat[][])
{
    // Mark all cells as not visited
    boolean [][]vis = new boolean[R][C];

    // Call BFS for every unvisited vertex
    // Whenever we see an univisted vertex,
    // we increment res (number of islands)
    // also.
    int res = 0;
    for (int i = 0; i < R; i++)
    {
        for (int j = 0; j < C; j++)
        {
            if (mat[i][j]==1 && !vis[i][j])
            {
                BFS(mat, vis, i, j);
                res++;
            }
        }
    }
    return res;
}

// Driver code
public static void main(String[] args)
{
    int mat[][] = { { 1, 1, 0, 0, 0 },
                    { 0, 1, 0, 0, 1 },
                    { 1, 0, 0, 1, 1 },
                    { 0, 0, 0, 0, 0 },
                    { 1, 0, 1, 0, 1 } };

    System.out.print(countIslands(mat));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# A BFS based solution to count number of
# islands in a graph.
from collections import deque

# A function to check if a given cell
# (u, v) can be included in DFS
def isSafe(mat, i, j, vis):

    return ((i >= 0) and (i < 5) and 
            (j >= 0) and (j < 5) and
          (mat[i][j] and (not vis[i][j])))

def BFS(mat, vis, si, sj):

    # These arrays are used to get row and
    # column numbers of 8 neighbours of
    # a given cell
    row = [-1, -1, -1, 0, 0, 1, 1, 1]
    col = [-1, 0, 1, -1, 1, -1, 0, 1]

    # Simple BFS first step, we enqueue
    # source and mark it as visited
    q = deque()
    q.append([si, sj])
    vis[si][sj] = True

    # Next step of BFS. We take out
    # items one by one from queue and
    # enqueue their univisited adjacent
    while (len(q) > 0):
        temp = q.popleft()

        i = temp[0]
        j = temp[1]

        # Go through all 8 adjacent
        for k in range(8):
            if (isSafe(mat, i + row[k], j + col[k], vis)):
                vis[i + row[k]][j + col[k]] = True
                q.append([i + row[k], j + col[k]])

# This function returns number islands (connected
# components) in a graph. It simply works as
# BFS for disconnected graph and returns count
# of BFS calls.
def countIslands(mat):

    # Mark all cells as not visited
    vis = [[False for i in range(5)]
                  for i in range(5)]
    # memset(vis, 0, sizeof(vis));

    # 5all BFS for every unvisited vertex
    # Whenever we see an univisted vertex,
    # we increment res (number of islands)
    # also.
    res = 0

    for i in range(5):
        for j in range(5):
            if (mat[i][j] and not vis[i][j]):
                BFS(mat, vis, i, j)
                res += 1

    return res

# Driver code
if __name__ == '__main__':

    mat = [ [ 1, 1, 0, 0, 0 ],
            [ 0, 1, 0, 0, 1 ],
            [ 1, 0, 0, 1, 1 ],
            [ 0, 0, 0, 0, 0 ],
            [ 1, 0, 1, 0, 1 ]]

    print (countIslands(mat))

# This code is contributed by mohit kumar 29
```

## C#

```
// A BFS based solution to count number of
// islands in a graph.
using System;
using System.Collections.Generic;

class GFG
{

// R x C matrix
static readonly int R = 5;
static readonly int C = 5 ;
class pair
{
    public int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// A function to check if a given cell
// (u, v) can be included in DFS
static bool isSafe(int [,]mat, int i, int j,
                    bool [,]vis)
{
    return (i >= 0) && (i < R) &&
        (j >= 0) && (j < C) &&
        (mat[i, j]==1 && !vis[i, j]);
}

static void BFS(int [,]mat, bool [,]vis,
                int si, int sj)
{

    // These arrays are used to get row and
    // column numbers of 8 neighbours of
    // a given cell
    int []row = { -1, -1, -1, 0, 0, 1, 1, 1 };
    int []col = { -1, 0, 1, -1, 1, -1, 0, 1 };

    // Simple BFS first step, we enqueue
    // source and mark it as visited
    List<pair> q = new List<pair>();
    q.Add(new pair(si, sj));
    vis[si, sj] = true;

    // Next step of BFS. We take out
    // items one by one from queue and
    // enqueue their univisited adjacent
    while (q.Count != 0)
    {
        int i = q[0].first;
        int j = q[0].second;
        q.RemoveAt(0);

        // Go through all 8 adjacent
        for (int k = 0; k < 8; k++)
        {
            if (isSafe(mat, i + row[k],
                    j + col[k], vis))
            {
                vis[i + row[k], j + col[k]] = true;
                q.Add(new pair(i + row[k], j + col[k]));
            }
        }
    }
}

// This function returns number islands (connected
// components) in a graph. It simply works as
// BFS for disconnected graph and returns count
// of BFS calls.
static int countIslands(int [,]mat)
{
    // Mark all cells as not visited
    bool [,]vis = new bool[R, C];

    // Call BFS for every unvisited vertex
    // Whenever we see an univisted vertex,
    // we increment res (number of islands)
    // also.
    int res = 0;
    for (int i = 0; i < R; i++)
    {
        for (int j = 0; j < C; j++)
        {
            if (mat[i, j]==1 && !vis[i, j])
            {
                BFS(mat, vis, i, j);
                res++;
            }
        }
    }
    return res;
}

// Driver code
public static void Main(String[] args)
{
    int [,]mat = { { 1, 1, 0, 0, 0 },
                    { 0, 1, 0, 0, 1 },
                    { 1, 0, 0, 1, 1 },
                    { 0, 0, 0, 0, 0 },
                    { 1, 0, 1, 0, 1 } };

    Console.Write(countIslands(mat));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// A BFS based solution to count number of
// islands in a graph.

// R x C matrix
let R = 5;
let C = 5 ;

// A function to check if a given cell
// (u, v) can be included in DFS
function isSafe(mat,i,j,vis)
{
    return (i >= 0) && (i < R) &&
        (j >= 0) && (j < C) &&
        (mat[i][j] == 1 && !vis[i][j]);
}

function BFS(mat, vis, si, sj)
{

    // These arrays are used to get row and
    // column numbers of 8 neighbours of
    // a given cell
       let row = [ -1, -1, -1, 0, 0, 1, 1, 1 ];
    let col = [ -1, 0, 1, -1, 1, -1, 0, 1 ];

    // Simple BFS first step, we enqueue
    // source and mark it as visited
    let q = [];
    q.push([si, sj]);
    vis[si][sj] = true;

    // Next step of BFS. We take out
    // items one by one from queue and
    // enqueue their univisited adjacent
    while (q.length != 0)
    {

        let i = q[0][0];
        let j = q[0][1];
        q.shift();

        // Go through all 8 adjacent
        for (let k = 0; k < 8; k++)
        {
            if (isSafe(mat, i + row[k],
                    j + col[k], vis))
            {
                vis[i + row[k]][j + col[k]] = true;
                q.push([i + row[k], j + col[k]]);
            }
        }
    }
}

// This function returns number islands (connected
// components) in a graph. It simply works as
// BFS for disconnected graph and returns count
// of BFS calls.
function countIslands(mat)
{

    // Mark all cells as not visited
    let vis = new Array(R);
    for(let i = 0; i < R; i++)
    {
        vis[i] = new Array(C);
        for(let j = 0; j < C; j++)
        {
            vis[i][j] = false;
        }
    }

    // Call BFS for every unvisited vertex
    // Whenever we see an univisted vertex,
    // we increment res (number of islands)
    // also.
    let res = 0;
    for (let i = 0; i < R; i++)
    {
        for (let j = 0; j < C; j++)
        {
            if (mat[i][j] == 1 && !vis[i][j])
            {
                BFS(mat, vis, i, j);
                res++;
            }
        }
    }
    return res;
}

// Driver code
let mat = [[ 1, 1, 0, 0, 0 ],
                    [ 0, 1, 0, 0, 1 ],
                    [ 1, 0, 0, 1, 1 ],
                    [ 0, 0, 0, 0, 0 ],
                    [ 1, 0, 1, 0, 1 ] ];

document.write(countIslands(mat));

// This code is contributed by patel2127.
</script>
```

**Output:** 

```
5
```

时间复杂度:O(ROW * COL)，其中 ROW 是行数，COL 是矩阵中的列数。