# 无向图中所有直接连接到给定节点的节点中的第 k 个最大节点

> 原文:[https://www . geesforgeks . org/kth-所有直接连接节点中最大的节点到给定的无向图中的节点/](https://www.geeksforgeeks.org/kth-largest-node-among-all-directly-connected-nodes-to-the-given-node-in-an-undirected-graph/)

给定两个数组 **u** 和 **v** ，表示一个图，使得存在从**u【I】**到**v【I】**(0≤v【I】，u【I】<N)的无向边，并且每个节点具有某个值**val【I】**(0≤I<N)。对于每个节点，如果直接连接到它的节点根据它们的值按降序排序(如果值相等，则按它们的索引按升序排序)，则在 **k <sup>th</sup>** 位置打印该节点的编号。如果总节点为 **< k** ，则打印 **-1** 。

**示例:**

> **输入:** u[] = {0，0，1}，v[] = {2，1，2}，val[] = {2，4，3}，k = 2
> **输出:**
> 2
> 0
> 0
> 对于 0 节点，与其直接相连的节点分别为值为 4 和 3 的 1 和 2
> ，因此第二大值的节点为 2。
> 对于 1 个节点，与其直接相连的节点分别为 0 和 2
> 值分别为 2 和 3，因此第二大值的节点为 0。
> 对于 2 节点，与其直接相连的节点分别为 0 和 1
> 值为 2 和 4，因此第二大值的节点为 0。
> 
> **输入:**u[]= { 0.2 }、v[]= { 2.1 }、val[] = {2，4，3}、k = 2
> **输出:**
> –1
> -1
> 0

**方法:**想法是将直接连接到一个节点的节点连同它们的值一起存储在一个向量中，并按递增的顺序对它们进行排序，具有 **n** 个直接连接节点的节点的第 k 个最大值将是从最后一个节点开始的第**(n–k)**个节点。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to print Kth node for each node
void findKthNode(int u[], int v[], int n, int val[], int V, int k)
{

    // Vector to store nodes directly
    // connected to ith node along with
    // their values
    vector<pair<int, int> > g[V];

    // Add edges to the vector along with
    // the values of the node
    for (int i = 0; i < n; i++) {
        g[u[i]].push_back(make_pair(val[v[i]], v[i]));
        g[v[i]].push_back(make_pair(val[u[i]], u[i]));
    }

    // Sort neighbors of every node
    // and find the Kth node
    for (int i = 0; i < V; i++) {
        if (g[i].size() > 0)
            sort(g[i].begin(), g[i].end());

        // Get the kth node
        if (k <= g[i].size())
            printf("%d\n", g[i][g[i].size() - k].second);

        // If total nodes are < k
        else
            printf("-1\n");
    }

    return;
}

// Driver code
int main()
{
    int V = 3;
    int val[] = { 2, 4, 3 };
    int u[] = { 0, 0, 1 };
    int v[] = { 2, 1, 2 };

    int n = sizeof(u) / sizeof(int);
    int k = 2;

    findKthNode(u, v, n, val, V, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// pair class
static class pair
{
    int first,second;
    pair(int a,int b)
    {
        first = a;
        second = b;
    }
}

// Function to print Kth node for each node
static void findKthNode(int u[], int v[], int n,
                        int val[], int V, int k)
{

    // Vector to store nodes directly
    // connected to ith node along with
    // their values
    Vector<Vector<pair >> g = new Vector<Vector<pair>>();

    for(int i = 0; i < V; i++)
    g.add(new Vector<pair>());

    // Add edges to the Vector along with
    // the values of the node
    for (int i = 0; i < n; i++)
    {
        g.get(u[i]).add(new pair(val[v[i]], v[i]));
        g.get(v[i]).add(new pair(val[u[i]], u[i]));
    }

    // Sort neighbors of every node
    // and find the Kth node
    for (int i = 0; i < V; i++)
    {
        if (g.get(i).size() > 0)
            Collections.sort(g.get(i),new Comparator<pair>()
        {
            public int compare(pair p1, pair p2)
            {
                return p1.first - p2.first;
            }
        });

        // Get the kth node
        if (k <= g.get(i).size())
            System.out.printf("%d\n", g.get(i).get(g.get(i).size() - k).second);

        // If total nodes are < k
        else
            System.out.printf("-1\n");
    }

    return;
}

// Driver code
public static void main(String args[])
{
    int V = 3;
    int val[] = { 2, 4, 3 };
    int u[] = { 0, 0, 1 };
    int v[] = { 2, 1, 2 };

    int n = u.length;
    int k = 2;

    findKthNode(u, v, n, val, V, k);
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to print Kth node for each node
def findKthNode(u, v, n, val, V, k):

    # Vector to store nodes directly connected
    # to ith node along with their values
    g = [[] for i in range(V)]

    # Add edges to the vector along
    # with the values of the node
    for i in range(0, n): 
        g[u[i]].append((val[v[i]], v[i]))
        g[v[i]].append((val[u[i]], u[i]))

    # Sort neighbors of every node
    # and find the Kth node
    for i in range(0, V):
        if len(g[i]) > 0:
            g[i].sort()

        # Get the kth node
        if k <= len(g[i]):
            print(g[i][-k][1])

        # If total nodes are < k
        else:
            print("-1")

    return

# Driver code
if __name__ == "__main__":

    V = 3
    val = [2, 4, 3] 
    u = [0, 0, 1]
    v = [2, 1, 2] 
    n, k = len(u), 2

    findKthNode(u, v, n, val, V, k)

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections;
using System.Collections.Generic;

class GFG
{

// pair class
class pair
{
    public int first,second;
    public pair(int a,int b)
    {
        first = a;
        second = b;
    }
}

class sortHelper : IComparer
{
   int IComparer.Compare(object a, object b)
   {
      pair first = (pair)a;
      pair second = (pair)b;

      return first.first - second.first;
   }
}

// Function to print Kth node for each node
static void findKthNode(int []u, int []v, int n,
                        int []val, int V, int k)
{

    // Vector to store nodes directly
    // connected to ith node along with
    // their values
    ArrayList g = new ArrayList();    
    for(int i = 0; i < V; i++)
        g.Add(new ArrayList());

    // Add edges to the Vector along with
    // the values of the node
    for (int i = 0; i < n; i++)
    {
        ((ArrayList)g[u[i]]).Add(new pair(val[v[i]], v[i]));
        ((ArrayList)g[v[i]]).Add(new pair(val[u[i]], u[i]));
    }

    // Sort neighbors of every node
    // and find the Kth node
    for (int i = 0; i < V; i++)
    {
        if (((ArrayList)g[i]).Count > 0)
        {
            ArrayList tmp = (ArrayList)g[i];
            tmp.Sort(new sortHelper());
            g[i] = tmp;           
        }

        // Get the kth node
        if (k <= ((ArrayList)g[i]).Count)
            Console.Write(((pair)((ArrayList)g[i])[((ArrayList)g[i]).Count - k]).second+"\n");

        // If total nodes are < k
        else
            Console.Write("-1\n");
    }
    return;
}

// Driver code
public static void Main(string []args)
{
    int V = 3;
    int []val = { 2, 4, 3 };
    int []u = { 0, 0, 1 };
    int []v = { 2, 1, 2 };
    int n = u.Length;
    int k = 2;
    findKthNode(u, v, n, val, V, k);
}
}

// This code is contributed by Pratham76
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to print Kth node for each node
function findKthNode(u, v, n, val, V, k)
{

    // Vector to store nodes directly
    // connected to ith node along with
    // their values
    var g = Array.from(Array(V), () => Array());

    // Add edges to the vector along with
    // the values of the node
    for(var i = 0; i < n; i++)
    {
        g[u[i]].push([val[v[i]], v[i]]);
        g[v[i]].push([val[u[i]], u[i]]);
    }

    // Sort neighbors of every node
    // and find the Kth node
    for(var i = 0; i < V; i++)
    {
        if (g[i].length > 0)
            g[i].sort();

        // Get the kth node
        if (k <= g[i].length)
            document.write(
                g[i][g[i].length - k][1] + "<br>");

        // If total nodes are < k
        else
            document.write("-1<br>");
    }
    return;
}

// Driver code
var V = 3;
var val = [ 2, 4, 3 ];
var u = [ 0, 0, 1 ];
var v = [ 2, 1, 2 ];
var n = u.length;
var k = 2;

findKthNode(u, v, n, val, V, k);

// This code is contributed by rutvik_56

</script>
```

**Output:** 

```
2
0
0
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)