# 从每个连接的组件中选择节点的方法数量

> 原文:[https://www . geeksforgeeks . org/从每个连接的组件中选择节点的方式数/](https://www.geeksforgeeks.org/number-of-ways-to-select-a-node-from-each-connected-component/)

给定一个有 **N** 个节点和 **M** 条边的图。任务是找到从给定图的每个连接组件中选择节点的方法数量。
**例:**

> **输入:**
> 
> ![](img/2d48dcc28c566342e1e748cc4174f8db.png)
> 
> **输出:** 3
> (1，4)、(2，4)、(3，4)是可能的方式。
> **输入:**
> 
> ![](img/27fca39eeadeb691de5b87e103e51061.png)
> 
> **输出:** 6
> (1、4、5)、(2、4、5)、(3、4、5)、(1、4、6)、(2、4、6)、(3、4、6)都是可能的方式。

**方法:**每个连接组件中的节点数的乘积就是所需答案。运行一个简单的 [dfs](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/) 来查找每个连接组件中的节点数。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define N 100005

int n, m, temp;
vector<int> gr[N];
int vis[N];

// Function to add edges in the graph
void Add_edges(int x, int y)
{
    gr[x].push_back(y);
    gr[y].push_back(x);
}

// Function for DFS
void dfs(int ch)
{
    // Mark node as visited
    vis[ch] = 1;

    // Count number of nodes in a component
    temp++;
    for (auto i : gr[ch])
        if (!vis[i])
            dfs(i);
}

// Function to return the required number of ways
int NumberOfWays()
{

    // To store the required answer
    int ans = 1;

    memset(vis, 0, sizeof vis);
    for (int i = 1; i <= n; i++) {

        // If current node hasn't been visited yet
        if (!vis[i]) {
            temp = 0;
            dfs(i);

            // Multiply it with the answer
            ans *= temp;
        }
    }

    return ans;
}

// Driver code
int main()
{
    n = 4, m = 2;

    // Add edges
    Add_edges(1, 2);
    Add_edges(1, 3);

    cout << NumberOfWays();

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

static final int N = 100005;

static int n, m, temp;
static Vector<Integer> []gr = new Vector[N];
static int []vis = new int[N];

// Function to add edges in the graph
static void Add_edges(int x, int y)
{
    gr[x].add(y);
    gr[y].add(x);
}

// Function for DFS
static void dfs(int ch)
{
    // Mark node as visited
    vis[ch] = 1;

    // Count number of nodes in a component
    temp++;
    for (int i : gr[ch])
        if (vis[i] == 0)
            dfs(i);
}

// Function to return the required number of ways
static int NumberOfWays()
{

    // To store the required answer
    int ans = 1;
    Arrays.fill(vis, 0);

    for (int i = 1; i <= n; i++)
    {

        // If current node hasn't been visited yet
        if (vis[i] == 0)
        {
            temp = 0;
            dfs(i);

            // Multiply it with the answer
            ans *= temp;
        }
    }

    return ans;
}

// Driver code
public static void main(String[] args)
{
    n = 4;
    m = 2;
    for (int i = 0; i < N; i++)
        gr[i] = new Vector<Integer>();

    // Add edges
    Add_edges(1, 2);
    Add_edges(1, 3);

    System.out.print(NumberOfWays());
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to add edges in the graph
def Add_edges(x, y):

    gr[x].append(y)
    gr[y].append(x)

# Function for DFS
def dfs(ch):

    # Mark node as visited
    vis[ch] = 1
    global temp

    # Count number of nodes
    # in a component
    temp += 1
    for i in gr[ch]:
        if not vis[i]:
            dfs(i)

# Function to return the required
# number of ways
def NumberOfWays():

    # To store the required answer
    ans = 1
    global temp

    for i in range(1, n + 1):

        # If current node hasn't been
        # visited yet
        if not vis[i]:
            temp = 0
            dfs(i)

            # Multiply it with the answer
            ans *= temp

    return ans

# Driver code
if __name__ == "__main__":

    n, m, temp = 4, 2, 0
    N = 100005

    gr = [[] for i in range(N)]
    vis = [None] * N

    # Add edges
    Add_edges(1, 2)
    Add_edges(1, 3)

    print(NumberOfWays())

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

static readonly int N = 100005;

static int n, m, temp;
static List<int> []gr = new List<int>[N];
static int []vis = new int[N];

// Function to add edges in the graph
static void Add_edges(int x, int y)
{
    gr[x].Add(y);
    gr[y].Add(x);
}

// Function for DFS
static void dfs(int ch)
{
    // Mark node as visited
    vis[ch] = 1;

    // Count number of nodes in a component
    temp++;
    foreach (int i in gr[ch])
        if (vis[i] == 0)
            dfs(i);
}

// Function to return the required number of ways
static int NumberOfWays()
{

    // To store the required answer
    int ans = 1;
    for(int i= 0; i < N; i++)
        vis[i] = 0;

    for (int i = 1; i <= n; i++)
    {

        // If current node hasn't been visited yet
        if (vis[i] == 0)
        {
            temp = 0;
            dfs(i);

            // Multiply it with the answer
            ans *= temp;
        }
    }

    return ans;
}

// Driver code
public static void Main(String[] args)
{
    n = 4;
    m = 2;
    for (int i = 0; i < N; i++)
        gr[i] = new List<int>();

    // Add edges
    Add_edges(1, 2);
    Add_edges(1, 3);

    Console.Write(NumberOfWays());
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

let N = 100005;

let n, m, temp;

let gr = new Array(N);
let vis = new Array(N);

// Function to add edges in the graph
function Add_edges(x,y)
{
    gr[x].push(y);
    gr[y].push(x);
}

// Function for DFS
function dfs(ch)
{
    // Mark node as visited
    vis[ch] = 1;

    // Count number of nodes in a component
    temp++;
    for (let i of gr[ch])
        if (vis[i] == 0)
            dfs(i);
}

// Function to return the required number of ways
function NumberOfWays()
{
    // To store the required answer
    let ans = 1;
    for(let i=0;i<vis.length;i++)
        vis[i]=0;

    for (let i = 1; i <= n; i++)
    {

        // If current node hasn't been visited yet
        if (vis[i] == 0)
        {
            temp = 0;
            dfs(i);

            // Multiply it with the answer
            ans *= temp;
        }
    }

    return ans;
}

// Driver code
n = 4;
m = 2;
for (let i = 0; i < N; i++)
    gr[i] = [];

// Add edges
Add_edges(1, 2);
Add_edges(1, 3);

document.write(NumberOfWays());

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
3
```