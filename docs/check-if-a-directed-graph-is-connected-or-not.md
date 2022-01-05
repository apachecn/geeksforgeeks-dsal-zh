# 检查有向图是否连通

> 原文:[https://www . geesforgeks . org/check-a-directed-graph-on-or-not/](https://www.geeksforgeeks.org/check-if-a-directed-graph-is-connected-or-not/)

给定一个有向图。任务是检查给定的图是否连通。
**例:**

> **输入:**
> 
> ![](img/9f40cbced6916586b54fa357894d36e9.png)
> 
> **输出:**是
> T3】输入:T5】
> 
> ![](img/943f908a0a737defec80d9abccfdc31f.png)
> 
> **输出:**否

**进场:**

1.  取两个 bool 数组 **vis1** 和 **vis2** 大小 **N** (图的节点数)，在所有索引中保留 false。
2.  从图 G 的一个随机顶点 **v** 开始，运行一个 DFS(G，v)。
3.  将所有访问过的顶点 **v** 设为**vis1【v】= true**。
4.  现在反转所有边的方向。
5.  在步骤 2 中选择的顶点开始 DFS。
6.  将所有访问过的顶点 **v** 设为**vis2【v】= true**。
7.  如果任一顶点 **v** 有 **vis1[v] =假**和 **vis2[v] =假**，则该图不连通。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define N 100000

// To keep correct and reverse direction
vector<int> gr1[N], gr2[N];

bool vis1[N], vis2[N];

// Function to add edges
void Add_edge(int u, int v)
{
    gr1[u].push_back(v);
    gr2[v].push_back(u);
}

// DFS function
void dfs1(int x)
{
    vis1[x] = true;

    for (auto i : gr1[x])
        if (!vis1[i])
            dfs1(i);
}

// DFS function
void dfs2(int x)
{
    vis2[x] = true;

    for (auto i : gr2[x])
        if (!vis2[i])
            dfs2(i);
}

bool Is_Connected(int n)
{
    // Call for correct direction
    memset(vis1, false, sizeof vis1);
    dfs1(1);

    // Call for reverse direction
    memset(vis2, false, sizeof vis2);
    dfs2(1);

    for (int i = 1; i <= n; i++) {

        // If any vertex it not visited in any direction
        // Then graph is not connected
        if (!vis1[i] and !vis2[i])
            return false;
    }

    // If graph is connected
    return true;
}

// Driver code
int main()
{
    int n = 4;

    // Add edges
    Add_edge(1, 2);
    Add_edge(1, 3);
    Add_edge(2, 3);
    Add_edge(3, 4);

    // Function call
    if (Is_Connected(n))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{
    static int N = 100000;

    // To keep correct and reverse direction
    @SuppressWarnings("unchecked")
    static Vector<Integer>[] gr1 = new Vector[N];
    @SuppressWarnings("unchecked")
    static Vector<Integer>[] gr2 = new Vector[N];

    static boolean[] vis1 = new boolean[N];
    static boolean[] vis2 = new boolean[N];

    static {
        for (int i = 0; i < N; i++)
        {
            gr1[i] = new Vector<>();
            gr2[i] = new Vector<>();
        }
    }

    // Function to add edges
    static void Add_edge(int u, int v)
    {
        gr1[u].add(v);
        gr2[v].add(u);
    }

    // DFS function
    static void dfs1(int x)
    {
        vis1[x] = true;
        for (int i : gr1[x])
            if (!vis1[i])
                dfs1(i);
    }

    // DFS function
    static void dfs2(int x)
    {
        vis2[x] = true;
        for (int i : gr2[x])
            if (!vis2[i])
                dfs2(i);
    }

    static boolean Is_connected(int n)
    {

        // Call for correct direction
        Arrays.fill(vis1, false);
        dfs1(1);

        // Call for reverse direction
        Arrays.fill(vis2, false);
        dfs2(1);

        for (int i = 1; i <= n; i++)
        {

            // If any vertex it not visited in any direction
            // Then graph is not connected
            if (!vis1[i] && !vis2[i])
                return false;
        }

        // If graph is connected
        return true;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 4;

        // Add edges
        Add_edge(1, 2);
        Add_edge(1, 3);
        Add_edge(2, 3);
        Add_edge(3, 4);

        // Function call
        if (Is_connected(n))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of the approach
N = 100000

# To keep correct and reverse direction
gr1 = {}; gr2 = {};

vis1 = [0] * N; vis2 = [0] * N;

# Function to add edges
def Add_edge(u, v) :

    if u not in gr1 :
        gr1[u] = [];

    if v not in gr2 :
        gr2[v] = [];

    gr1[u].append(v);
    gr2[v].append(u);

# DFS function
def dfs1(x) :
    vis1[x] = True;
    if x not in gr1 :
        gr1[x] = {};

    for i in gr1[x] :
        if (not vis1[i]) :
            dfs1(i)

# DFS function
def dfs2(x) :

    vis2[x] = True;

    if x not in gr2 :
        gr2[x] = {};

    for i in gr2[x] :
        if (not vis2[i]) :
            dfs2(i);

def Is_Connected(n) :

    global vis1;
    global vis2;

    # Call for correct direction
    vis1 = [False] * len(vis1);
    dfs1(1);

    # Call for reverse direction
    vis2 = [False] * len(vis2);
    dfs2(1);

    for i in range(1, n + 1) :

        # If any vertex it not visited in any direction
        # Then graph is not connected
        if (not vis1[i] and not vis2[i]) :
            return False;

    # If graph is connected
    return True;

# Driver code
if __name__ == "__main__" :

    n = 4;

    # Add edges
    Add_edge(1, 2);
    Add_edge(1, 3);
    Add_edge(2, 3);
    Add_edge(3, 4);

    # Function call
    if (Is_Connected(n)) :
        print("Yes");
    else :
        print("No");

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{
    static int N = 100000;

    // To keep correct and reverse direction
    static List<int>[] gr1 = new List<int>[N];

    static List<int>[] gr2 = new List<int>[N];

    static bool[] vis1 = new bool[N];
    static bool[] vis2 = new bool[N];

    // Function to add edges
    static void Add_edge(int u, int v)
    {
        gr1[u].Add(v);
        gr2[v].Add(u);
    }

    // DFS function
    static void dfs1(int x)
    {
        vis1[x] = true;
        foreach (int i in gr1[x])
            if (!vis1[i])
                dfs1(i);
    }

    // DFS function
    static void dfs2(int x)
    {
        vis2[x] = true;
        foreach (int i in gr2[x])
            if (!vis2[i])
                dfs2(i);
    }

    static bool Is_connected(int n)
    {

        // Call for correct direction
        for (int i = 0; i < n; i++)
            vis1[i] = false;
        dfs1(1);

        // Call for reverse direction
        for (int i = 0; i < n; i++)
            vis2[i] = false;
        dfs2(1);

        for (int i = 1; i <= n; i++)
        {

            // If any vertex it not visited in any direction
            // Then graph is not connected
            if (!vis1[i] && !vis2[i])
                return false;
        }

        // If graph is connected
        return true;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int n = 4;
        for (int i = 0; i < N; i++)
        {
            gr1[i] = new List<int>();
            gr2[i] = new List<int>();
        }

        // Add edges
        Add_edge(1, 2);
        Add_edge(1, 3);
        Add_edge(2, 3);
        Add_edge(3, 4);

        // Function call
        if (Is_connected(n))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    let N = 100000;

    // To keep correct and reverse direction
    let gr1 = [];
    let gr2 = [];
    for(let i = 0; i < N; i++)
    {
        gr1.push([]);
        gr2.push([]);
    }

    let vis1 = new Array(N);
    let vis2 = new Array(N);
    vis1.fill(false);
    vis2.fill(false);

    // Function to add edges
    function Add_edge(u, v)
    {
        gr1[u].push(v);
        gr2[v].push(u);
    }

    // DFS function
    function dfs1(x)
    {
        vis1[x] = true;
        for(let i = 0; i < gr1[x].length; i++)
        {
            if (!vis1[gr1[x][i]])
            {
                dfs1(gr1[x][i]);
            }
        }
    }

    // DFS function
    function dfs2(x)
    {
        vis2[x] = true;
        for(let i = 0; i < gr2[x].length; i++)
        {
            if (!vis2[gr2[x][i]])
            {
                dfs2(gr2[x][i]);
            }
        }
    }

    function Is_connected(n)
    {

        // Call for correct direction
        for (let i = 0; i < n; i++)
            vis1[i] = false;
        dfs1(1);

        // Call for reverse direction
        for (let i = 0; i < n; i++)
            vis2[i] = false;
        dfs2(1);

        for (let i = 1; i <= n; i++)
        {

            // If any vertex it not visited in any direction
            // Then graph is not connected
            if (!vis1[i] && !vis2[i])
                return false;
        }

        // If graph is connected
        return true;
    }

    let n = 4;
    for (let i = 0; i < N; i++)
    {
      gr1[i] = [];
      gr2[i] = [];
    }

    // Add edges
    Add_edge(1, 2);
    Add_edge(1, 3);
    Add_edge(2, 3);
    Add_edge(3, 4);

    // Function call
    if (Is_connected(n))
      document.write("Yes");
    else
      document.write("No");

    // This code is contributed by divyesh072019.
</script>
```

**Output:** 

```
Yes
```