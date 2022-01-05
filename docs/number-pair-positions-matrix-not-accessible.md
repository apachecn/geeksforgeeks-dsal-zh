# 矩阵中不可访问的位置对的数量

> 原文:[https://www . geesforgeks . org/number-pair-positions-matrix-不可访问/](https://www.geeksforgeeks.org/number-pair-positions-matrix-not-accessible/)

给定正整数 **N** 。考虑一个 **N X N** 的矩阵。除了(x1，y1)、(x2，y2)形式的给定对单元外，任何其他单元都不可访问，即在(x2，y2)到(x1，y1)之间存在路径(可访问)。任务是找到对(a1，b1)、(a2，b2)的计数，使得单元格(a2，b2)不能从(a1，b1)访问。
**例:**

```
Input : N = 2
Allowed path 1: (1, 1) (1, 2)
Allowed path 2: (1, 2) (2, 2)
Output : 6
Cell (2, 1) is not accessible from any cell
and no cell is accessible from it.
```

![](img/06885ce895f04d9ead73e006c97854aa.png)

```
(1, 1) - (2, 1)
(1, 2) - (2, 1)
(2, 2) - (2, 1)
(2, 1) - (1, 1)
(2, 1) - (1, 2)
(2, 1) - (2, 2)
```

将每个单元视为一个节点，编号从 1 到 N*N。每个单元(x，y)可以使用(x–1)* N+y 映射到数字。现在，将每个给定的允许路径视为节点之间的边。这将形成连接组件的不相交集合。现在，使用[深度优先遍历](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/)或[广度优先遍历](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/)，我们可以很容易地找到连接组件的节点数量或大小，比如 x。现在，不可访问路径的数量是 x *(N * N–x)。这样，我们可以为每个连接的路径找到不可访问的路径。
以下是本办法的实施情况:

## C++

```
// C++ program to count number of pair of positions
// in matrix which are not accessible
#include<bits/stdc++.h>
using namespace std;

// Counts number of vertices connected in a component
// containing x. Stores the count in k.
void dfs(vector<int> graph[], bool visited[],
                               int x, int *k)
{
    for (int i = 0; i < graph[x].size(); i++)
    {
        if (!visited[graph[x][i]])
        {
            // Incrementing the number of node in
            // a connected component.
            (*k)++;

            visited[graph[x][i]] = true;
            dfs(graph, visited, graph[x][i], k);
        }
    }
}

// Return the number of count of non-accessible cells.
int countNonAccessible(vector<int> graph[], int N)
{
    bool visited[N*N + N];
    memset(visited, false, sizeof(visited));

    int ans = 0;
    for (int i = 1; i <= N*N; i++)
    {
        if (!visited[i])
        {
            visited[i] = true;

            // Initialize count of connected
            // vertices found by DFS starting
            // from i.
            int k = 1;
            dfs(graph, visited, i, &k);

            // Update result
            ans += k * (N*N - k);
        }
    }
    return ans;
}

// Inserting the edge between edge.
void insertpath(vector<int> graph[], int N, int x1,
                             int y1, int x2, int y2)
{
    // Mapping the cell coordinate into node number.
    int a = (x1 - 1) * N + y1;
    int b = (x2 - 1) * N + y2;

    // Inserting the edge.
    graph[a].push_back(b);
    graph[b].push_back(a);
}

// Driven Program
int main()
{
    int N = 2;

    vector<int> graph[N*N + 1];

    insertpath(graph, N, 1, 1, 1, 2);
    insertpath(graph, N, 1, 2, 2, 2);

    cout << countNonAccessible(graph, N) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of
// pair of positions in matrix
// which are not accessible
import java.util.*;
class GFG
{

static int k;

// Counts number of vertices connected
// in a component containing x.
// Stores the count in k.
static void dfs(Vector<Integer> graph[],
                boolean visited[], int x)
{
    for (int i = 0; i < graph[x].size(); i++)
    {
        if (!visited[graph[x].get(i)])
        {
            // Incrementing the number of node in
            // a connected component.
            (k)++;

            visited[graph[x].get(i)] = true;
            dfs(graph, visited, graph[x].get(i));
        }
    }
}

// Return the number of count of non-accessible cells.
static int countNonAccessible(Vector<Integer> graph[], int N)
{
    boolean []visited = new boolean[N * N + N];

    int ans = 0;
    for (int i = 1; i <= N * N; i++)
    {
        if (!visited[i])
        {
            visited[i] = true;

            // Initialize count of connected
            // vertices found by DFS starting
            // from i.
            int k = 1;
            dfs(graph, visited, i);

            // Update result
            ans += k * (N * N - k);
        }
    }
    return ans;
}

// Inserting the edge between edge.
static void insertpath(Vector<Integer> graph[],
                       int N, int x1, int y1,
                       int x2, int y2)
{
    // Mapping the cell coordinate into node number.
    int a = (x1 - 1) * N + y1;
    int b = (x2 - 1) * N + y2;

    // Inserting the edge.
    graph[a].add(b);
    graph[b].add(a);
}

// Driver Code
public static void main(String args[])
{
    int N = 2;

    Vector[] graph = new Vector[N * N + 1];
    for (int i = 1; i <= N * N; i++)
        graph[i] = new Vector<Integer>();
    insertpath(graph, N, 1, 1, 1, 2);
    insertpath(graph, N, 1, 2, 2, 2);

    System.out.println(countNonAccessible(graph, N));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to count number of pair of
# positions in matrix which are not accessible

# Counts number of vertices connected in a
# component containing x. Stores the count in k.
def dfs(graph,visited, x, k):
    for i in range(len(graph[x])):
        if (not visited[graph[x][i]]):

            # Incrementing the number of node 
            # in a connected component.
            k[0] += 1

            visited[graph[x][i]] = True
            dfs(graph, visited, graph[x][i], k)

# Return the number of count of
# non-accessible cells.
def countNonAccessible(graph, N):
    visited = [False] * (N * N + N)

    ans = 0
    for i in range(1, N * N + 1):
        if (not visited[i]):
            visited[i] = True

            # Initialize count of connected
            # vertices found by DFS starting
            # from i.
            k = [1]
            dfs(graph, visited, i, k)

            # Update result
            ans += k[0] * (N * N - k[0])
    return ans

# Inserting the edge between edge.
def insertpath(graph, N, x1, y1, x2, y2):

    # Mapping the cell coordinate
    # into node number.
    a = (x1 - 1) * N + y1
    b = (x2 - 1) * N + y2

    # Inserting the edge.
    graph[a].append(b)
    graph[b].append(a)

# Driver Code
if __name__ == '__main__':

    N = 2

    graph = [[] for i in range(N*N + 1)]

    insertpath(graph, N, 1, 1, 1, 2)
    insertpath(graph, N, 1, 2, 2, 2)

    print(countNonAccessible(graph, N))

# This code is contributed by PranchalK
```

## C#

```
// C# program to count number of
// pair of positions in matrix
// which are not accessible
using System;
using System.Collections.Generic;

class GFG
{
static int k;

// Counts number of vertices connected
// in a component containing x.
// Stores the count in k.
static void dfs(List<int> []graph,
                bool []visited, int x)
{
    for (int i = 0; i < graph[x].Count; i++)
    {
        if (!visited[graph[x][i]])
        {
            // Incrementing the number of node in
            // a connected component.
            (k)++;

            visited[graph[x][i]] = true;
            dfs(graph, visited, graph[x][i]);
        }
    }
}

// Return the number of count
// of non-accessible cells.
static int countNonAccessible(List<int> []graph,
                                   int N)
{
    bool []visited = new bool[N * N + N];

    int ans = 0;
    for (int i = 1; i <= N * N; i++)
    {
        if (!visited[i])
        {
            visited[i] = true;

            // Initialize count of connected
            // vertices found by DFS starting
            // from i.
            int k = 1;
            dfs(graph, visited, i);

            // Update result
            ans += k * (N * N - k);
        }
    }
    return ans;
}

// Inserting the edge between edge.
static void insertpath(List<int> []graph,
                            int N, int x1, int y1,
                            int x2, int y2)
{
    // Mapping the cell coordinate into node number.
    int a = (x1 - 1) * N + y1;
    int b = (x2 - 1) * N + y2;

    // Inserting the edge.
    graph[a].Add(b);
    graph[b].Add(a);
}

// Driver Code
public static void Main(String []args)
{
    int N = 2;

    List<int>[] graph = new List<int>[N * N + 1];
    for (int i = 1; i <= N * N; i++)
        graph[i] = new List<int>();
    insertpath(graph, N, 1, 1, 1, 2);
    insertpath(graph, N, 1, 2, 2, 2);

    Console.WriteLine(countNonAccessible(graph, N));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript program to count number of
// pair of positions in matrix
// which are not accessible

let k;

// Counts number of vertices connected
// in a component containing x.
// Stores the count in k.
function dfs(graph,visited,x)
{
    for (let i = 0; i < graph[x].length; i++)
    {
        if (!visited[graph[x][i]])
        {
            // Incrementing the number of node in
            // a connected component.
            (k)++;

            visited[graph[x][i]] = true;
            dfs(graph, visited, graph[x][i]);
        }
    }
}

// Return the number of count of non-accessible cells.
function countNonAccessible(graph,N)
{
    let visited = new Array(N * N + N);

    let ans = 0;
    for (let i = 1; i <= N * N; i++)
    {
        if (!visited[i])
        {
            visited[i] = true;

            // Initialize count of connected
            // vertices found by DFS starting
            // from i.
            let k = 1;
            dfs(graph, visited, i);

            // Update result
            ans += k * (N * N - k);
        }
    }
    return ans;
}

// Inserting the edge between edge.
function insertpath(graph,N,x1,y1,x2,y2)
{
    // Mapping the cell coordinate into node number.
    let a = (x1 - 1) * N + y1;
    let b = (x2 - 1) * N + y2;

    // Inserting the edge.
    graph[a].push(b);
    graph[b].push(a);
}

// Driver Code
let N = 2;

let graph = new Array(N * N + 1);
for (let i = 1; i <= N * N; i++)
    graph[i] = [];
insertpath(graph, N, 1, 1, 1, 2);
insertpath(graph, N, 1, 2, 2, 2);

document.write(countNonAccessible(graph, N));

// This code is contributed by rag2127

</script>
```

**输出:**

```
6
```

**时间复杂度:** O(N * N)。
本文由 **Anuj Chauhan** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。