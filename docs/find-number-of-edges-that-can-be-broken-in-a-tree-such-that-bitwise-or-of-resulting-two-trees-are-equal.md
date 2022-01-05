# 找出一棵树中可以断开的边的数量，使得生成的两棵树的位或相等

> 原文:[https://www . geeksforgeeks . org/find-可在树中断开的边数-这样得到的两个树的按位或等于/](https://www.geeksforgeeks.org/find-number-of-edges-that-can-be-broken-in-a-tree-such-that-bitwise-or-of-resulting-two-trees-are-equal/)

给定一棵树，它有 n 个节点，每个节点都有一个编号。我们可以打破树的任何边缘，这将导致形成两个新的树。我们必须计算边的数量，使得在断开该边后形成的两个树中存在的节点的按位“或”相等。每个节点的值≤ 10 <sup>6</sup> 。
**例:**

```
Input: values[]={2, 3, 32, 43, 8}
         1
        / \
       2   3
      /     \
     4       5
Output: 1
If we break the edge between 2 and 4 then the Bitwise OR 
of both the resulting tree will be 43.

Input: values[]={1, 3, 2, 3}
        1
      / | \
     2  3  4
Output: 2
The edge between 1 and 2 can be broken,the Bitwise OR 
of the resulting two trees will be 3.
Similarly, the edge between 1 and 4 can also be broken.
```

**方法:**这个问题可以用简单的 [DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 解决。由于节点的值≤ 10 <sup>6</sup> ，因此可以用 22 个二进制位来表示。节点值的按位“或”也可以用 22 位二进制表示。方法是找出在一个子树的所有值中每个位被设置的次数。对于每个边，我们将检查对于从 0 到 21 的每个位，具有该特定位的数字在两个结果树中都是零，或者在两个结果树中都大于零，并且如果满足所有位的条件，则在结果中计数该边。
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include<bits/stdc++.h>
using namespace std;

    int m[1000],x[22];

    // Array to store the number of times each bit
    // is set in all the values of a subtree
    int a[1000][22];

    vector<vector<int>> g;
    int ans = 0;

    // Function to perform simple DFS
    void dfs(int u, int p)
    {
        for (int i=0;i<g[u].size();i++) {
            int v = g[u][i];
            if (v != p) {
                dfs(v, u);

                // Finding the number of times each bit is set
                // in all the values of a subtree rooted at v
                for (int i = 0; i < 22; i++)
                    a[u][i] += a[v][i];
            }
        }

        // Checking for each bit whether the numbers
        // with that particular bit as set are
        // either zero in both the resulting trees or
        // greater than zero in both the resulting trees
        int pp = 0;
        for (int i = 0; i < 22; i++) {
            if (!((a[u][i] > 0 && x[i] - a[u][i] > 0)
                || (a[u][i] == 0 && x[i] == 0))) {
                pp = 1;
                break;
            }
        }
        if (pp == 0)
            ans++;
    }

    // Driver code
    int main()
    {

        // Number of nodes
        int n = 4;

        // ArrayList to store the tree
        g.resize(n+1);

        // Array to store the value of nodes
        m[1] = 1;
        m[2] = 3;
        m[3] = 2;
        m[4] = 3;

        // Array to store the number of times each bit
        // is set in all the values in complete tree

        for (int i = 1; i <= n; i++) {
            int y = m[i];
            int k = 0;

            // Finding the set bits in the value of node i
            while (y != 0) {
                int p = y % 2;
                if (p == 1) {
                    x[k]++;
                    a[i][k]++;
                }
                y = y / 2;
                k++;
            }
        }

        // push_back edges
        g[1].push_back(2);
        g[2].push_back(1);
        g[1].push_back(3);
        g[3].push_back(1);
        g[1].push_back(4);
        g[4].push_back(1);
        dfs(1, 0);
        cout<<(ans);
}
//contributed by Arnab Kundu
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
public class GFG {
    static int m[], a[][], x[];
    static ArrayList<Integer> g[];
    static int ans = 0;

    // Function to perform simple DFS
    static void dfs(int u, int p)
    {
        for (int v : g[u]) {
            if (v != p) {
                dfs(v, u);

                // Finding the number of times each bit is set
                // in all the values of a subtree rooted at v
                for (int i = 0; i < 22; i++)
                    a[u][i] += a[v][i];
            }
        }

        // Checking for each bit whether the numbers
        // with that particular bit as set are
        // either zero in both the resulting trees or
        // greater than zero in both the resulting trees
        int pp = 0;
        for (int i = 0; i < 22; i++) {
            if (!((a[u][i] > 0 && x[i] - a[u][i] > 0)
                  || (a[u][i] == 0 && x[i] == 0))) {
                pp = 1;
                break;
            }
        }
        if (pp == 0)
            ans++;
    }

    // Driver code
    public static void main(String args[])
    {

        // Number of nodes
        int n = 4;

        // ArrayList to store the tree
        g = new ArrayList[n + 1];

        // Array to store the value of nodes
        m = new int[n + 1];
        m[1] = 1;
        m[2] = 3;
        m[3] = 2;
        m[4] = 3;

        // Array to store the number of times each bit
        // is set in all the values of a subtree
        a = new int[n + 1][22];

        // Array to store the number of times each bit
        // is set in all the values in complete tree
        x = new int[22];
        for (int i = 1; i <= n; i++) {
            g[i] = new ArrayList<>();
            int y = m[i];
            int k = 0;

            // Finding the set bits in the value of node i
            while (y != 0) {
                int p = y % 2;
                if (p == 1) {
                    x[k]++;
                    a[i][k]++;
                }
                y = y / 2;
                k++;
            }
        }

        // Add edges
        g[1].add(2);
        g[2].add(1);
        g[1].add(3);
        g[3].add(1);
        g[1].add(4);
        g[4].add(1);
        dfs(1, 0);
        System.out.println(ans);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach
m, x = [0] * 1000, [0] * 22

# Array to store the number of times each bit
# is set in all the values of a subtree
a = [[0 for i in range(22)]
        for j in range(1000)]
ans = 0

# Function to perform simple DFS
def dfs(u, p):

    global ans
    for i in range(0, len(g[u])):
        v = g[u][i]
        if v != p:
            dfs(v, u)

            # Finding the number of times
            # each bit is set in all the
            # values of a subtree rooted at v
            for i in range(0, 22):
                a[u][i] += a[v][i]

    # Checking for each bit whether the numbers
    # with that particular bit as set are
    # either zero in both the resulting trees or
    # greater than zero in both the resulting trees
    pp = 0
    for i in range(0, 22):
        if (not((a[u][i] > 0 and
                 x[i] - a[u][i] > 0)
            or (a[u][i] == 0 and x[i] == 0))):
            pp = 1
            break

    if pp == 0:
        ans += 1

# Driver code
if __name__ == "__main__":

    # Number of nodes
    n = 4

    # ArrayList to store the tree
    g = [[] for i in range(n+1)]

    # Array to store the value of nodes
    m[1] = 1
    m[2] = 3
    m[3] = 2
    m[4] = 3

    # Array to store the number of times
    # each bit is set in all the values
    # in complete tree
    for i in range(1, n+1):
        y, k = m[i], 0

        # Finding the set bits in the
        # value of node i
        while y != 0:
            p = y % 2
            if p == 1:
                x[k] += 1
                a[i][k] += 1

            y = y // 2
            k += 1

    # append edges
    g[1].append(2)
    g[2].append(1)
    g[1].append(3)
    g[3].append(1)
    g[1].append(4)
    g[4].append(1)
    dfs(1, 0)
    print(ans)

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{
    static int []m;
    static int [,]a;
    static int []x;
    static List<int> []g;
    static int ans = 0;

    // Function to perform simple DFS
    static void dfs(int u, int p)
    {
        foreach (int v in g[u])
        {
            if (v != p)
            {
                dfs(v, u);

                // Finding the number of times each bit is set
                // in all the values of a subtree rooted at v
                for (int i = 0; i < 22; i++)
                    a[u,i] += a[v,i];
            }
        }

        // Checking for each bit whether the numbers
        // with that particular bit as set are
        // either zero in both the resulting trees or
        // greater than zero in both the resulting trees
        int pp = 0;
        for (int i = 0; i < 22; i++)
        {
            if (!((a[u,i] > 0 && x[i] - a[u,i] > 0)
                || (a[u,i] == 0 && x[i] == 0)))
            {
                pp = 1;
                break;
            }
        }
        if (pp == 0)
            ans++;
    }

    // Driver code
    public static void Main(String []args)
    {

        // Number of nodes
        int n = 4;

        // ArrayList to store the tree
        g = new List<int>[n + 1];

        // Array to store the value of nodes
        m = new int[n + 1];
        m[1] = 1;
        m[2] = 3;
        m[3] = 2;
        m[4] = 3;

        // Array to store the number of times each bit
        // is set in all the values of a subtree
        a = new int[n + 1,22];

        // Array to store the number of times each bit
        // is set in all the values in complete tree
        x = new int[22];
        for (int i = 1; i <= n; i++)
        {
            g[i] = new List<int>();
            int y = m[i];
            int k = 0;

            // Finding the set bits in the value of node i
            while (y != 0)
            {
                int p = y % 2;
                if (p == 1)
                {
                    x[k]++;
                    a[i,k]++;
                }
                y = y / 2;
                k++;
            }
        }

        // Add edges
        g[1].Add(2);
        g[2].Add(1);
        g[1].Add(3);
        g[3].Add(1);
        g[1].Add(4);
        g[4].Add(1);
        dfs(1, 0);
        Console.WriteLine(ans);
    }
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach
var m = [];
var a = [];
var x = [];
var g = [];
var ans = 0;

// Function to perform simple DFS
function dfs(u, p)
{
    for(var v of g[u])
    {
        if (v != p)
        {
            dfs(v, u);
            // Finding the number of times each bit is set
            // in all the values of a subtree rooted at v
            for (var i = 0; i < 22; i++)
                a[u][i] += a[v][i];
        }
    }
    // Checking for each bit whether the numbers
    // with that particular bit as set are
    // either zero in both the resulting trees or
    // greater than zero in both the resulting trees
    var pp = 0;
    for (var i = 0; i < 22; i++)
    {
        if (!((a[u][i] > 0 && x[i] - a[u][i] > 0)
            || (a[u][i] == 0 && x[i] == 0)))
        {
            pp = 1;
            break;
        }
    }
    if (pp == 0)
        ans++;
}
// Driver code
// Number of nodes
var n = 4;
// ArrayList to store the tree
g = Array.from(Array(n+1), ()=>Array().fill(0));
// Array to store the value of nodes
m = Array(n+1);
m[1] = 1;
m[2] = 3;
m[3] = 2;
m[4] = 3;
// Array to store the number of times each bit
// is set in all the values of a subtree
a = Array.from(Array(n+1), ()=>Array(22).fill(0));
// Array to store the number of times each bit
// is set in all the values in complete tree
x = Array(22).fill(0);
for (var i = 1; i <= n; i++)
{
    g[i] = [];
    var y = m[i];
    var k = 0;
    // Finding the set bits in the value of node i
    while (y != 0)
    {
        var p = y % 2;
        if (p == 1)
        {
            x[k]++;
            a[i][k]++;
        }
        y = parseInt(y / 2);
        k++;
    }
}
// push edges
g[1].push(2);
g[2].push(1);
g[1].push(3);
g[3].push(1);
g[1].push(4);
g[4].push(1);
dfs(1, 0);
document.write(ans);

</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(N * log(MAX))，其中 N 为节点数，MAX 为树中节点的最大值。

**辅助空间:** O(N)