# 查询矩阵中连接的非空单元格的计数并更新

> 原文:[https://www . geeksforgeeks . org/query-to-find-count-of-connected-non-empty-cells-in-a-matrix-with-updates/](https://www.geeksforgeeks.org/queries-to-find-the-count-of-connected-non-empty-cells-in-a-matrix-with-updates/)

给定一个由 **N** 行和 **M** 列组成的布尔矩阵 **mat[][]** ，最初用 **0** 的(空单元格)填充，一个整数 **K** 并查询{X，Y}类型的 **Q[][]** ，任务是替换 **mat[X][Y] = 1** (非空单元格)，并计算给定矩阵中连接的非空单元格的数量。
**示例:**

> **输入:** N = 3，M = 3，K = 4，Q[][] = {{0，0}，{1，1}，{1，0}，{1，2}}
> **输出:**1 2 1
> 1**解释:**T8】最初，mat[][] = {{0，0，0}，{0，0，0}，{0，0，0}}
> 查询 1: mat[][] = {{1，0，0}} Count = 2
> 查询 1: mat[][] = {{1，0，0}，{1，1，0}，{0，0，0}}，Count = 1
> 查询 1: mat[][] = {{1，0，0}，{1，1，1}，{0，0，0}}，Count = 1
> **输入:** N = 2，M = 2，K = 2，Q[][] = {{0，0}，{0，1 } }【0

**方法:**
问题可以使用[不相交集合数据结构](https://www.geeksforgeeks.org/disjoint-set-data-structures/)来解决。按照以下步骤解决问题:

*   因为最初矩阵中没有 **1** ，所以**计数= 0** 。
*   通过执行线性映射**索引= X * M + Y** ，将二维问题转化为经典的[联合查找](https://www.geeksforgeeks.org/union-find-algorithm-set-2-union-by-rank/)，其中 **M** 为列长。
*   在每个查询中设置一个**索引**后，增加**计数**。
*   如果 4 个相邻单元格中有一个非空单元格:
    *   对当前**索引**和**相邻单元格**执行并集操作(连接两套)。
    *   递减**计数**为两台机组连接。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Count of connected cells
int ctr = 0;

// Function to return the representative
// of the Set to which x belongs
int find(vector<int>& parent, int x)
{

    // If x is parent of itself
    if (parent[x] == x)

        // x is representative
        // of the Set
        return x;

    // Otherwise
    parent[x] = find(parent, parent[x]);

    // Path Compression
    return parent[x];
}

// Unites the set that includes
// x and the set that includes y
void setUnion(vector<int>& parent,
              vector<int>& rank, int x, int y)
{
    // Find the representatives(or the
    // root nodes) for x an y
    int parentx = find(parent, x);
    int parenty = find(parent, y);

    // If both are in the same set
    if (parenty == parentx)
        return;

    // Decrement count
    ctr--;

    // If x's rank is less than y's rank
    if (rank[parentx] < rank[parenty]) {
        parent[parentx] = parenty;
    }

    // Otherwise
    else if (rank[parentx] > rank[parenty]) {
        parent[parenty] = parentx;
    }
    else {

        // Then move x under y (doesn't matter
        // which one goes where)
        parent[parentx] = parenty;

        // And increment the result tree's
        // rank by 1
        rank[parenty]++;
    }
}

// Function to count the number of
// connected cells in the matrix
vector<int> solve(int n, int m,
                  vector<pair<int, int> >& query)
{

    // Store result for queries
    vector<int> result(query.size());

    // Store representative of
    // each element
    vector<int> parent(n * m);

    // Initially, all elements
    // are in their own set
    for (int i = 0; i < n * m; i++)
        parent[i] = i;

    // Stores the rank(depth) of each node
    vector<int> rank(n * m, 1);

    vector<bool> grid(n * m, 0);

    for (int i = 0; i < query.size(); i++) {

        int x = query[i].first;
        int y = query[i].second;

        // If the grid[x*m + y] is already
        // set, store the result
        if (grid[m * x + y] == 1) {
            result[i] = ctr;
            continue;
        }

        // Set grid[x*m + y] to 1
        grid[m * x + y] = 1;

        // Increment count.
        ctr++;

        // Check for all adjacent cells
        // to do a Union with neighbour's
        // set if neighbour is also 1
        if (x > 0 and grid[m * (x - 1) + y] == 1)
            setUnion(parent, rank,
                     m * x + y, m * (x - 1) + y);

        if (y > 0 and grid[m * (x) + y - 1] == 1)
            setUnion(parent, rank,
                     m * x + y, m * (x) + y - 1);

        if (x < n - 1 and grid[m * (x + 1) + y] == 1)
            setUnion(parent, rank,
                     m * x + y, m * (x + 1) + y);

        if (y < m - 1 and grid[m * (x) + y + 1] == 1)
            setUnion(parent, rank,
                     m * x + y, m * (x) + y + 1);

        // Store result.
        result[i] = ctr;
    }
    return result;
}

// Driver Code
int main()
{
    int N = 3, M = 3, K = 4;

    vector<pair<int, int> > query
        = { { 0, 0 },
            { 1, 1 },
            { 1, 0 },
            { 1, 2 } };
    vector<int> result = solve(N, M, query);

    for (int i = 0; i < K; i++)
        cout << result[i] << " ";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Count of connected cells
static int ctr = 0;

// Function to return the representative
// of the Set to which x belongs
static int find(int []parent, int x)
{

    // If x is parent of itself
    if (parent[x] == x)

        // x is representative
        // of the Set
        return x;

    // Otherwise
    parent[x] = find(parent, parent[x]);

    // Path Compression
    return parent[x];
}

// Unites the set that includes
// x and the set that includes y
static void setUnion(int[] parent,
                     int[] rank, int x, int y)
{

    // Find the representatives(or the
    // root nodes) for x an y
    int parentx = find(parent, x);
    int parenty = find(parent, y);

    // If both are in the same set
    if (parenty == parentx)
        return;

    // Decrement count
    ctr--;

    // If x's rank is less than y's rank
    if (rank[parentx] < rank[parenty])
    {
        parent[parentx] = parenty;
    }

    // Otherwise
    else if (rank[parentx] > rank[parenty])
    {
        parent[parenty] = parentx;
    }
    else
    {

        // Then move x under y (doesn't matter
        // which one goes where)
        parent[parentx] = parenty;

        // And increment the result tree's
        // rank by 1
        rank[parenty]++;
    }
}

// Function to count the number of
// connected cells in the matrix
static int [] solve(int n, int m,
                    int [][]query)
{

    // Store result for queries
    int []result = new int[query.length];

    // Store representative of
    // each element
    int []parent = new int[n * m];

    // Initially, all elements
    // are in their own set
    for(int i = 0; i < n * m; i++)
        parent[i] = i;

    // Stores the rank(depth) of each node
    int []rank = new int[n * m];
    Arrays.fill(rank, 1);

    boolean []grid = new boolean[n * m];

    for(int i = 0; i < query.length; i++)
    {
        int x = query[i][0];
        int y = query[i][1];

        // If the grid[x*m + y] is already
        // set, store the result
        if (grid[m * x + y] == true)
        {
            result[i] = ctr;
            continue;
        }

        // Set grid[x*m + y] to 1
        grid[m * x + y] = true;

        // Increment count.
        ctr++;

        // Check for all adjacent cells
        // to do a Union with neighbour's
        // set if neighbour is also 1
        if (x > 0 && grid[m * (x - 1) + y] == true)
            setUnion(parent, rank,
                     m * x + y, m * (x - 1) + y);

        if (y > 0 && grid[m * (x) + y - 1] == true)
            setUnion(parent, rank,
                     m * x + y, m * (x) + y - 1);

        if (x < n - 1 && grid[m * (x + 1) + y] == true)
            setUnion(parent, rank,
                     m * x + y, m * (x + 1) + y);

        if (y < m - 1 && grid[m * (x) + y + 1] == true)
            setUnion(parent, rank,
                     m * x + y, m * (x) + y + 1);

        // Store result.
        result[i] = ctr;
    }
    return result;
}

// Driver Code
public static void main(String[] args)
{
    int N = 3, M = 3, K = 4;

    int [][]query = { { 0, 0 },
                      { 1, 1 },
                      { 1, 0 },
                      { 1, 2 } };
    int[] result = solve(N, M, query);

    for(int i = 0; i < K; i++)
        System.out.print(result[i] + " ");
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python 3 program to implement
# the above approach

# Count of connected cells
ctr = 0

# Function to return the
# representative of the Set
# to which x belongs
def find(parent, x):

    # If x is parent of itself
    if (parent[x] == x):

        # x is representative
        # of the Set
        return x

    # Otherwise
    parent[x] = find(parent,
                     parent[x])

    # Path Compression
    return parent[x]

# Unites the set that
# includes x and the
# set that includes y
def setUnion(parent,
             rank, x, y):

    global ctr

    # Find the representatives
    # (or the root nodes) for x an y
    parentx = find(parent, x)
    parenty = find(parent, y)

    # If both are in the same set
    if (parenty == parentx):
        return

    # Decrement count
    ctr -= 1

    # If x's rank is less than y's rank
    if (rank[parentx] < rank[parenty]):
        parent[parentx] = parenty

    # Otherwise
    elif (rank[parentx] > rank[parenty]):
        parent[parenty] = parentx

    else:

        # Then move x under y
        # (doesn't matter which
        # one goes where)
        parent[parentx] = parenty

        # And increment the result
        # tree's rank by 1
        rank[parenty] += 1

# Function to count the number of
# connected cells in the matrix
def solve(n, m, query):

    global ctr

    # Store result for queries
    result = [0] * len(query)

    # Store representative of
    # each element
    parent = [0] * (n * m)

    # Initially, all elements
    # are in their own set
    for i in range (n * m):
        parent[i] = i

    # Stores the rank(depth)
    # of each node
    rank = [1] * (n * m)

    grid = [0] * (n * m)

    for  i in range (len( query)):
        x = query[i][0]
        y = query[i][1]

        # If the grid[x*m + y] is already
        # set, store the result
        if (grid[m * x + y] == 1):
            result[i] = ctr
            continue

        # Set grid[x*m + y] to 1
        grid[m * x + y] = 1

        # Increment count.
        ctr += 1

        # Check for all adjacent cells
        # to do a Union with neighbour's
        # set if neighbour is also 1
        if (x > 0 and
            grid[m * (x - 1) + y] == 1):
            setUnion(parent, rank,
                     m * x + y,
                     m * (x - 1) + y)

        if (y > 0 and
            grid[m * (x) + y - 1] == 1):
            setUnion(parent, rank,
                     m * x + y,
                     m * (x) + y - 1)

        if (x < n - 1 and
            grid[m * (x + 1) + y] == 1):
            setUnion(parent, rank,
                     m * x + y,
                     m * (x + 1) + y)

        if (y < m - 1 and
            grid[m * (x) + y + 1] == 1):
            setUnion(parent, rank,
                     m * x + y,
                     m * (x) + y + 1)

        # Store result.
        result[i] = ctr
    return result

# Driver Code
if __name__ == "__main__":

    N = 3
    M = 3
    K = 4
    query = [[0, 0],
             [1, 1],
             [1, 0],
             [1, 2]]
    result = solve(N, M, query)
    for i in range (K):
        print (result[i], end = " ")

# This code is contributed by Chitranayal
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

// Count of connected cells
static int ctr = 0;

// Function to return the representative
// of the Set to which x belongs
static int find(int []parent, int x)
{

    // If x is parent of itself
    if (parent[x] == x)

        // x is representative
        // of the Set
        return x;

    // Otherwise
    parent[x] = find(parent, parent[x]);

    // Path Compression
    return parent[x];
}

// Unites the set that includes
// x and the set that includes y
static void setUnion(int[] parent,
                     int[] rank,
                     int x, int y)
{

    // Find the representatives(or the
    // root nodes) for x an y
    int parentx = find(parent, x);
    int parenty = find(parent, y);

    // If both are in the same set
    if (parenty == parentx)
        return;

    // Decrement count
    ctr--;

    // If x's rank is less than y's rank
    if (rank[parentx] < rank[parenty])
    {
        parent[parentx] = parenty;
    }

    // Otherwise
    else if (rank[parentx] > rank[parenty])
    {
        parent[parenty] = parentx;
    }
    else
    {

        // Then move x under y (doesn't matter
        // which one goes where)
        parent[parentx] = parenty;

        // And increment the result tree's
        // rank by 1
        rank[parenty]++;
    }
}

// Function to count the number of
// connected cells in the matrix
static int [] solve(int n, int m,
                    int [,]query)
{

    // Store result for queries
    int []result = new int[query.Length];

    // Store representative of
    // each element
    int []parent = new int[n * m];

    // Initially, all elements
    // are in their own set
    for(int i = 0; i < n * m; i++)
        parent[i] = i;

    // Stores the rank(depth) of each node
    int []rank = new int[n * m];
    for(int i = 0; i < rank.Length; i++)
        rank[i] = 1;
    bool []grid = new bool[n * m];

    for(int i = 0; i < query.GetLength(0); i++)
    {
        int x = query[i, 0];
        int y = query[i, 1];

        // If the grid[x*m + y] is already
        // set, store the result
        if (grid[m * x + y] == true)
        {
            result[i] = ctr;
            continue;
        }

        // Set grid[x*m + y] to 1
        grid[m * x + y] = true;

        // Increment count.
        ctr++;

        // Check for all adjacent cells
        // to do a Union with neighbour's
        // set if neighbour is also 1
        if (x > 0 && grid[m * (x - 1) + y] == true)
            setUnion(parent, rank,
                     m * x + y, m * (x - 1) + y);

        if (y > 0 && grid[m * (x) + y - 1] == true)
            setUnion(parent, rank,
                     m * x + y, m * (x) + y - 1);

        if (x < n - 1 && grid[m * (x + 1) + y] == true)
            setUnion(parent, rank,
                     m * x + y, m * (x + 1) + y);

        if (y < m - 1 && grid[m * (x) + y + 1] == true)
            setUnion(parent, rank,
                     m * x + y, m * (x) + y + 1);

        // Store result.
        result[i] = ctr;
    }
    return result;
}

// Driver Code
public static void Main(String[] args)
{
    int N = 3, M = 3, K = 4;

    int [,]query = {{ 0, 0 }, { 1, 1 },
                    { 1, 0 }, { 1, 2 }};
    int[] result = solve(N, M, query);

    for(int i = 0; i < K; i++)
        Console.Write(result[i] + " ");
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Count of connected cells
let ctr = 0;

// Function to return the representative
// of the Set to which x belongs
function find(parent,x)
{
    // If x is parent of itself
    if (parent[x] == x)

        // x is representative
        // of the Set
        return x;

    // Otherwise
    parent[x] = find(parent, parent[x]);

    // Path Compression
    return parent[x];
}

// Unites the set that includes
// x and the set that includes y
function setUnion(parent,rank,x,y)
{
    // Find the representatives(or the
    // root nodes) for x an y
    let parentx = find(parent, x);
    let parenty = find(parent, y);

    // If both are in the same set
    if (parenty == parentx)
        return;

    // Decrement count
    ctr--;

    // If x's rank is less than y's rank
    if (rank[parentx] < rank[parenty])
    {
        parent[parentx] = parenty;
    }

    // Otherwise
    else if (rank[parentx] > rank[parenty])
    {
        parent[parenty] = parentx;
    }
    else
    {

        // Then move x under y (doesn't matter
        // which one goes where)
        parent[parentx] = parenty;

        // And increment the result tree's
        // rank by 1
        rank[parenty]++;
    }
}

// Function to count the number of
// connected cells in the matrix
function solve(n,m,query)
{
    // Store result for queries
    let result = new Array(query.length);

    // Store representative of
    // each element
    let parent = new Array(n * m);

    // Initially, all elements
    // are in their own set
    for(let i = 0; i < n * m; i++)
        parent[i] = i;

    // Stores the rank(depth) of each node
    let rank = new Array(n * m);

    let grid = new Array(n * m);

    for(let i=0;i<(n*m);i++)
    {
        rank[i]=0;
        grid[i]=false;
    }

    for(let i = 0; i < query.length; i++)
    {
        let x = query[i][0];
        let y = query[i][1];

        // If the grid[x*m + y] is already
        // set, store the result
        if (grid[m * x + y] == true)
        {
            result[i] = ctr;
            continue;
        }

        // Set grid[x*m + y] to 1
        grid[m * x + y] = true;

        // Increment count.
        ctr++;

        // Check for all adjacent cells
        // to do a Union with neighbour's
        // set if neighbour is also 1
        if (x > 0 && grid[m * (x - 1) + y] == true)
            setUnion(parent, rank,
                     m * x + y, m * (x - 1) + y);

        if (y > 0 && grid[m * (x) + y - 1] == true)
            setUnion(parent, rank,
                     m * x + y, m * (x) + y - 1);

        if (x < n - 1 && grid[m * (x + 1) + y] == true)
            setUnion(parent, rank,
                     m * x + y, m * (x + 1) + y);

        if (y < m - 1 && grid[m * (x) + y + 1] == true)
            setUnion(parent, rank,
                     m * x + y, m * (x) + y + 1);

        // Store result.
        result[i] = ctr;
    }
    return result;
}

// Driver Code
let N = 3, M = 3, K = 4;
let query = [[ 0, 0 ],
                      [ 1, 1 ],
                      [ 1, 0 ],
                      [ 1, 2 ]];

let result = solve(N, M, query);
for(let i = 0; i < K; i++)
    document.write(result[i] + " ");

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
1 2 1 1
```

***时间复杂度:**O(N * M * sizeof(Q))*
***辅助空间:** O(N*M)*