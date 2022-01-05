# 有向加权图中正好有 k 条边的最短路径|集合 2

> 原文:[https://www . geeksforgeeks . org/有向加权图集中有 k 条边的最短路径集-2/](https://www.geeksforgeeks.org/shortest-path-with-exactly-k-edges-in-a-directed-and-weighted-graph-set-2/)

给定一个有向加权图和其中的两个顶点 **S** 和 **D** ，任务是找到从 **S** 到 **D** 的最短路径，路径上正好有 **K** 条边。如果不存在这样的路径，请打印-1。

**示例:**

> **输入:** N = 3，K = 2，ed = { { {，2}，5}，{{2，3}，3}，{{3，1}，4}}，S = 1，D = 3
> **输出:** 8
> **解释:**有两条边的最短路径会是 1- > 2- > 3
> 
> **输入:** N = 3，K = 4，ed = { { {，2}，5}，{{2，3}，3}，{{3，1}，4}}，S = 1，D = 3
> **输出:** -1
> **解释:**从节点 1 到 3 不存在边长为 4 的路径
> 
> **输入:** N = 3，K = 5，ed = { { {，2}，5}，{{2，3}，3}，{{3，1}，4}}，S = 1，D = 3
> **输出:** 20
> **解释:**最短路径将为 1->2->3->1->2->3。

**方法:**一个 **O(V^3*K)** 方法对于这个问题已经在[前一篇文章中讨论过了。](https://www.geeksforgeeks.org/shortest-path-exactly-k-edges-directed-weighted-graph/)本文讨论了一种解决这个问题的方法 **O(E*K)** 。

想法是用[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)来解决这个问题。

让 dp[X][J]是从节点 **S** 到节点 **X** 的最短路径，总共正好使用 **J** 条边。利用这一点，dp[X][J+1]可以计算为:

```
dp[X][J+1] = min(arr[Y][J]+weight[{Y, X}])
for all Y which has an edge from Y to X.
```

问题的结果可以通过以下步骤计算:

1.  初始化一个数组，dis[]的初始值为“inf ”,除了 dis[S]为 0。
2.  对于 I 等于 1–K，运行一个循环
    *   初始化一个数组，dis1[]，初始值为“inf”。
    *   对于图中的每条边，
        dis 1[edge . second]= min(dis 1[edge . second]，dis[edge . first]+权重(edge))
3.  如果 dist[d]在无穷大，返回-1，否则返回 dist[d]。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
#define inf 100000000
using namespace std;

// Function to find the smallest path
// with exactly K edges
double smPath(int s, int d,
              vector<pair<pair<int, int>, int> > ed,
              int n, int k)
{
    // Array to store dp
    int dis[n + 1];

    // Initialising the array
    for (int i = 0; i <= n; i++)
        dis[i] = inf;
    dis[s] = 0;

    // Loop to solve DP
    for (int i = 0; i < k; i++) {

        // Initialising next state
        int dis1[n + 1];
        for (int j = 0; j <= n; j++)
            dis1[j] = inf;

        // Recurrence relation
        for (auto it : ed)
            dis1[it.first.second] = min(dis1[it.first.second],
                                        dis[it.first.first]
                                            + it.second);
        for (int i = 0; i <= n; i++)
            dis[i] = dis1[i];
    }

    // Returning final answer
    if (dis[d] == inf)
        return -1;
    else
        return dis[d];
}

// Driver code
int main()
{

    int n = 4;
    vector<pair<pair<int, int>, int> > ed;

    // Input edges
    ed = { { { 0, 1 }, 10 },
           { { 0, 2 }, 3 },
           { { 0, 3 }, 2 },
           { { 1, 3 }, 7 },
           { { 2, 3 }, 7 } };

    // Source and Destination
    int s = 0, d = 3;

    // Number of edges in path
    int k = 2;

    // Calling the function
    cout << smPath(s, d, ed, n, k);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.ArrayList;
import java.util.Arrays;

class GFG{

static class Pair<K, V>
{
    K first;
    V second;

    public Pair(K first, V second)
    {
        this.first = first;
        this.second = second;
    }
}

static int inf = 100000000;

// Function to find the smallest path
// with exactly K edges
static int smPath(int s, int d,
                  ArrayList<Pair<Pair<Integer, Integer>, Integer>> ed,
                  int n, int k)
{

    // Array to store dp
    int[] dis = new int[n + 1];

    // Initialising the array
    Arrays.fill(dis, inf);
    dis[s] = 0;

    // Loop to solve DP
    for(int i = 0; i < k; i++)
    {

        // Initialising next state
        int[] dis1 = new int[n + 1];
        Arrays.fill(dis1, inf);

        // Recurrence relation
        for(Pair<Pair<Integer, Integer>, Integer> it : ed)
            dis1[it.first.second] = Math.min(dis1[it.first.second],
                                             dis[it.first.first] +
                                                 it.second);
        for(int j = 0; j <= n; j++)
            dis[j] = dis1[j];
    }

    // Returning final answer
    if (dis[d] == inf)
        return -1;
    else
        return dis[d];
}

// Driver code
public static void main(String[] args)
{
    int n = 4;

    // Input edges
    ArrayList<Pair<Pair<Integer, Integer>, Integer>> ed = new ArrayList<>(
            Arrays.asList(
                    new Pair<Pair<Integer, Integer>, Integer>(
                        new Pair<Integer, Integer>(0, 1), 10),
                    new Pair<Pair<Integer, Integer>, Integer>(
                        new Pair<Integer, Integer>(0, 2), 3),
                    new Pair<Pair<Integer, Integer>, Integer>(
                        new Pair<Integer, Integer>(0, 3), 2),
                    new Pair<Pair<Integer, Integer>, Integer>(
                        new Pair<Integer, Integer>(1, 3), 7),
                    new Pair<Pair<Integer, Integer>, Integer>(
                        new Pair<Integer, Integer>(2, 3), 7)
            )
    );

    // Source and Destination
    int s = 0, d = 3;

    // Number of edges in path
    int k = 2;

    // Calling the function
    System.out.println(smPath(s, d, ed, n, k));
}
}

// This code is contributed by sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of the above approach
inf = 100000000

# Function to find the smallest path
# with exactly K edges
def smPath(s, d, ed, n, k):

    # Array to store dp
    dis = [inf] * (n + 1)
    dis[s] = 0

    # Loop to solve DP
    for i in range(k):

        # Initialising next state
        dis1 = [inf] * (n + 1)

        # Recurrence relation
        for it in ed:
            dis1[it[1]] = min(dis1[it[1]],
                            dis[it[0]]+ it[2])
        for i in range(n + 1):
            dis[i] = dis1[i]

    # Returning final answer
    if (dis[d] == inf):
        return -1
    else:
        return dis[d]

# Driver code
if __name__ == '__main__':

    n = 4

    # Input edges
    ed = [ [0, 1 ,10],
           [ 0, 2 ,3],
           [ 0, 3 ,2],
           [ 1, 3 ,7],
           [ 2, 3 ,7] ]

    # Source and Destination
    s = 0
    d = 3

    # Number of edges in path
    k = 2

    # Calling the function
    print(smPath(s, d, ed, n, k))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the above approach
using System;
using System.Linq;
using System.Collections.Generic;

public class GFG{

static int inf = 100000000;

// Function to find the smallest path
// with exactly K edges
public static int smPath(int s, int d,
                  List<KeyValuePair<KeyValuePair<int, int>, int>> ed,
                  int n, int k)
{

    // Array to store dp
    // Initialising the array
    int []dis = Enumerable.Repeat(inf, n+1).ToArray();
    dis[s] = 0;

    // Loop to solve DP
    for(int i = 0; i < k; i++)
    {

        // Initialising next state
        int []dis1 = Enumerable.Repeat(inf, n+1).ToArray();

        // Recurrence relation
        foreach(KeyValuePair<KeyValuePair<int, int>, int> it in ed)
            dis1[it.Key.Value] = Math.Min(dis1[it.Key.Value],
                                             dis[it.Key.Key] +
                                                 it.Value);
        for(int j = 0; j <= n; j++)
            dis[j] = dis1[j];
    }

    // Returning final answer
    if (dis[d] == inf)
        return -1;
    else
        return dis[d];
}

// Driver code
public static void Main(string[] args)
{
    int n = 4;

    // Input edges
    List<KeyValuePair<KeyValuePair<int, int>, int>> ed = new List<KeyValuePair<KeyValuePair<int, int>, int>>(){
                    new KeyValuePair<KeyValuePair<int, int>, int>(
                        new KeyValuePair<int, int>(0, 1), 10),
                    new KeyValuePair<KeyValuePair<int, int>, int>(
                        new KeyValuePair<int, int>(0, 2), 3),
                    new KeyValuePair<KeyValuePair<int, int>, int>(
                        new KeyValuePair<int, int>(0, 3), 2),
                    new KeyValuePair<KeyValuePair<int, int>, int>(
                        new KeyValuePair<int, int>(1, 3), 7),
                    new KeyValuePair<KeyValuePair<int, int>, int>(
                        new KeyValuePair<int, int>(2, 3), 7)
    };

    // Source and Destination
    int s = 0, d = 3;

    // Number of edges in path
    int k = 2;

    // Calling the function
    Console.Write(smPath(s, d, ed, n, k));
}
}

// This code is contributed by rrrtnx.
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach

let inf = 100000000;

// Function to find the smallest path
// with exactly K edges
function smPath(s,d,ed,n,k)
{
    // Array to store dp
    let dis = new Array(n + 1);

    // Initialising the array
    for(let i=0;i<(n+1);i++)
    {
        dis[i]=inf;
    }

    dis[s] = 0;

    // Loop to solve DP
    for(let i = 0; i < k; i++)
    {

        // Initialising next state
        let dis1 = new Array(n + 1);
        for(let i=0;i<(n+1);i++)
        {
            dis1[i]=inf;
        }

        // Recurrence relation
        for(let it=0;it< ed.length;it++)
            dis1[ed[it][1]] = Math.min(dis1[ed[it][1]],
                                             dis[ed[it][0]] +
                                                 ed[it][2]);
        document.write()
        for(let j = 0; j <= n; j++)
            dis[j] = dis1[j];
    }

    // Returning final answer
    if (dis[d] == inf)
        return -1;
    else
        return dis[d];
}

// Driver code
let n = 4;

 // Input edges
let ed = [ [0, 1 ,10],
           [ 0, 2 ,3],
           [ 0, 3 ,2],
           [ 1, 3 ,7],
           [ 2, 3 ,7] ];
// Source and Destination
let s = 0, d = 3;

// Number of edges in path
let k = 2;

// Calling the function
document.write(smPath(s, d, ed, n, k));

// This code is contributed by patel2127
</script>
```

**Output:** 

```
10
```

**时间复杂度:**O(E * K)
T3】空间复杂度: O(N)