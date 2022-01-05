# 卡普最小平均(或平均)重量循环算法

> 原文:[https://www . geeksforgeeks . org/karps-最小-平均-平均-重量-周期-算法/](https://www.geeksforgeeks.org/karps-minimum-mean-average-weight-cycle-algorithm/)

给定一个具有非负边权重的有向[强连通图](https://www.geeksforgeeks.org/strongly-connected-components/)。我们将一个循环的平均权重定义为该循环的所有边权重之和除以边数。我们的任务是在图的所有有向循环中找到最小平均权重。
**例:**

```
Input : Below Graph
```

![karps_mean_value](img/2750dbeb9fc99a13aaa2fa286fa0f264.png)

```
Output : 1.66667
```

高效寻找最小加权平均值循环的方法

```
Step 1: Choose first vertex as source.

Step 2: Compute the shortest path to all other vertices 
        on a path consisting of k edges 0 <= k <= V 
        where V is number of vertices.
        This is a simple dp problem which can be computed 
        by the recursive solution
        dp[k][v] = min(dp[k][v], dp[k-1][u] + weight(u,v)
        where v is the destination and the edge(u,v) should
        belong to E

Step 3: For each vertex calculate max(dp[n][v]-dp[k][v])/(n-k) 
         where 0<=k<=n-1

Step 4: The minimum of the values calculated above is the 
        required answer.
```

以上步骤求最小平均重量的证明，请参考这里的问题 9.2 [的解答。](https://courses.csail.mit.edu/6.046/fall01/handouts/ps9sol.pdf)

## C++

```
// C++ program to find minimum average
// weight of a cycle in connected and
// directed graph.
#include<bits/stdc++.h>
using namespace std;

const int V = 4;

// a struct to represent edges
struct edge
{
    int from, weight;
};

// vector to store edges
vector <edge> edges[V];

void addedge(int u,int v,int w)
{
    edges[v].push_back({u, w});
}

// calculates the shortest path
void shortestpath(int dp[][V])
{
    // initializing all distances as -1
    for (int i=0; i<=V; i++)
        for (int j=0; j<V; j++)
            dp[i][j] = -1;

    // shortest distance from first vertex
    // to in tself consisting of 0 edges
    dp[0][0] = 0;

    // filling up the dp table
    for (int i=1; i<=V; i++)
    {
        for (int j=0; j<V; j++)
        {
            for (int k=0; k<edges[j].size(); k++)
            {
                if (dp[i-1][edges[j][k].from] != -1)
                {
                    int curr_wt = dp[i-1][edges[j][k].from] +
                                  edges[j][k].weight;
                    if (dp[i][j] == -1)
                        dp[i][j] = curr_wt;
                    else
                       dp[i][j] = min(dp[i][j], curr_wt);
                }
            }
        }
    }
}

// Returns minimum value of average weight of a
// cycle in graph.
double minAvgWeight()
{
    int dp[V+1][V];
    shortestpath(dp);

    // array to store the avg values
    double avg[V];
    for (int i=0; i<V; i++)
        avg[i] = -1;

    // Compute average values for all vertices using
    // weights of shortest paths store in dp.
    for (int i=0; i<V; i++)
    {
        if (dp[V][i] != -1)
        {
            for (int j=0; j<V; j++)
                if (dp[j][i] != -1)
                    avg[i] = max(avg[i],
                ((double)dp[V][i]-dp[j][i])/(V-j));
        }
    }

    // Find minimum value in avg[]
    double result = avg[0];
    for (int i=0; i<V; i++)
        if (avg[i] != -1 && avg[i] < result)
            result = avg[i];

    return result;
}

// Driver function
int main()
{
    addedge(0, 1, 1);
    addedge(0, 2, 10);
    addedge(1, 2, 3);
    addedge(2, 3, 2);
    addedge(3, 1, 0);
    addedge(3, 0, 8);

    cout << minAvgWeight();

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum average
// weight of a cycle in connected and
// directed graph.
import java.io.*;
import java.util.*;

class GFG
{
static int V = 4;

// a struct to represent edges
static class Edge
{
    int from, weight;

    Edge(int from, int weight)
    {
        this.from = from;
        this.weight = weight;
    }
}

// vector to store edges
//@SuppressWarnings("unchecked")
static Vector<Edge>[] edges = new Vector[V];
static
{
    for (int i = 0; i < V; i++)
        edges[i] = new Vector<>();
}

static void addedge(int u, int v, int w)
{
    edges[v].add(new Edge(u, w));
}

// calculates the shortest path
static void shortestpath(int[][] dp)
{
    // initializing all distances as -1
    for (int i = 0; i <= V; i++)
        for (int j = 0; j < V; j++)
            dp[i][j] = -1;

    // shortest distance from first vertex
    // to in tself consisting of 0 edges
    dp[0][0] = 0;

    // filling up the dp table
    for (int i = 1; i <= V; i++)
    {
        for (int j = 0; j < V; j++)
        {
            for (int k = 0; k < edges[j].size(); k++)
            {
                if (dp[i - 1][edges[j].elementAt(k).from] != -1)
                {
                    int curr_wt = dp[i - 1][edges[j].elementAt(k).from] +
                                            edges[j].elementAt(k).weight;
                    if (dp[i][j] == -1)
                        dp[i][j] = curr_wt;
                    else
                        dp[i][j] = Math.min(dp[i][j], curr_wt);
                }
            }
        }
    }
}

// Returns minimum value of average weight
// of a cycle in graph.
static double minAvgWeight()
{
    int[][] dp = new int[V + 1][V];
    shortestpath(dp);

    // array to store the avg values
    double[] avg = new double[V];
    for (int i = 0; i < V; i++)
        avg[i] = -1;

    // Compute average values for all vertices using
    // weights of shortest paths store in dp.
    for (int i = 0; i < V; i++)
    {
        if (dp[V][i] != -1)
        {
            for (int j = 0; j < V; j++)
                if (dp[j][i] != -1)
                    avg[i] = Math.max(avg[i],
                                    ((double) dp[V][i] -
                                              dp[j][i]) / (V - j));
        }
    }

    // Find minimum value in avg[]
    double result = avg[0];
    for (int i = 0; i < V; i++)
        if (avg[i] != -1 && avg[i] < result)
            result = avg[i];

    return result;
}

// Driver Code
public static void main(String[] args)
{
    addedge(0, 1, 1);
    addedge(0, 2, 10);
    addedge(1, 2, 3);
    addedge(2, 3, 2);
    addedge(3, 1, 0);
    addedge(3, 0, 8);

    System.out.printf("%.5f", minAvgWeight());
}
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 program to find minimum
# average weight of a cycle in
# connected and directed graph.

# a struct to represent edges
class edge:
    def __init__(self, u, w):
        self.From = u
        self.weight = w

def addedge(u, v, w):
    edges[v].append(edge(u, w))

# calculates the shortest path
def shortestpath(dp):

    # initializing all distances as -1
    for i in range(V + 1):
        for j in range(V):
            dp[i][j] = -1

    # shortest distance From first vertex
    # to in tself consisting of 0 edges
    dp[0][0] = 0

    # filling up the dp table
    for i in range(1, V + 1):
        for j in range(V):
            for k in range(len(edges[j])):
                if (dp[i - 1][edges[j][k].From] != -1):
                    curr_wt = (dp[i - 1][edges[j][k].From] +
                                         edges[j][k].weight)
                    if (dp[i][j] == -1):
                        dp[i][j] = curr_wt
                    else:
                        dp[i][j] = min(dp[i][j], curr_wt)

# Returns minimum value of average
# weight of a cycle in graph.
def minAvgWeight():
    dp = [[None] * V for i in range(V + 1)]
    shortestpath(dp)

    # array to store the avg values
    avg = [-1] * V

    # Compute average values for all
    # vertices using weights of
    # shortest paths store in dp.
    for i in range(V):
        if (dp[V][i] != -1):
            for j in range(V):
                if (dp[j][i] != -1):
                    avg[i] = max(avg[i], (dp[V][i] -
                                          dp[j][i]) / (V - j))

    # Find minimum value in avg[]
    result = avg[0]
    for i in range(V):
        if (avg[i] != -1 and avg[i] < result):
            result = avg[i]

    return result

# Driver Code
V = 4

# vector to store edges
edges = [[] for i in range(V)]

addedge(0, 1, 1)
addedge(0, 2, 10)
addedge(1, 2, 3)
addedge(2, 3, 2)
addedge(3, 1, 0)
addedge(3, 0, 8)

print(minAvgWeight())

# This code is contributed by Pranchalk
```

## C#

```
// C# program to find minimum
// average weight of a cycle
// in connected and directed graph.
using System;
using System.Collections.Generic;
class GFG{

static int V = 4;

// a struct to represent
// edges
public class Edge
{
  public int from, weight;
  public Edge(int from,
              int weight)
  {
    this.from = from;
    this.weight = weight;
  }
}

// vector to store edges 
static List<Edge>[] edges =
            new List<Edge>[V]; 

static void addedge(int u,
                    int v, int w)
{
  edges[v].Add(new Edge(u, w));
}

// calculates the shortest path
static void shortestpath(int[,] dp)
{
  // initializing all distances
  // as -1
  for (int i = 0; i <= V; i++)
    for (int j = 0; j < V; j++)
      dp[i, j] = -1;

  // shortest distance from
  // first vertex to in tself
  // consisting of 0 edges
  dp[0, 0] = 0;

  // filling up the dp table
  for (int i = 1; i <= V; i++)
  {
    for (int j = 0; j < V; j++)
    {
      for (int k = 0;
               k < edges[j].Count; k++)
      {
        if (dp[i - 1,
               edges[j][k].from] != -1)
        {
          int curr_wt = dp[i - 1,
                           edges[j][k].from] +
                           edges[j][k].weight;
          if (dp[i, j] == -1)
            dp[i, j] = curr_wt;
          else
            dp[i, j] = Math.Min(dp[i, j],
                                curr_wt);
        }
      }
    }
  }
}

// Returns minimum value of
// average weight of a cycle
// in graph.
static double minAvgWeight()
{
  int[,] dp = new int[V + 1, V];
  shortestpath(dp);

  // array to store the
  // avg values
  double[] avg = new double[V];

  for (int i = 0; i < V; i++)
    avg[i] = -1;

  // Compute average values for
  // all vertices using weights
  // of shortest paths store in dp.
  for (int i = 0; i < V; i++)
  {
    if (dp[V, i] != -1)
    {
      for (int j = 0; j < V; j++)
        if (dp[j, i] != -1)
          avg[i] = Math.Max(avg[i],
                           ((double) dp[V, i] -
                             dp[j, i]) /
                             (V - j));
    }
  }

  // Find minimum value in avg[]
  double result = avg[0];

  for (int i = 0; i < V; i++)
    if (avg[i] != -1 &&
        avg[i] < result)
      result = avg[i];

  return result;
}

// Driver Code
public static void Main(String[] args)
{
  for (int i = 0; i < V; i++)
    edges[i] = new List<Edge>();

  addedge(0, 1, 1);
  addedge(0, 2, 10);
  addedge(1, 2, 3);
  addedge(2, 3, 2);
  addedge(3, 1, 0);
  addedge(3, 0, 8);

  Console.Write("{0:F5}",
                minAvgWeight());
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// JavaScript program to find minimum
// average weight of a cycle
// in connected and directed graph.

var V = 4;

// a struct to represent
// edges
class Edge
{
    constructor(from, weight)
    {
        this.from = from;
        this.weight = weight;
    }
}

// vector to store edges 
var edges = Array.from(Array(V), ()=>Array());

function addedge(u, v, w)
{
  edges[v].push(new Edge(u, w));
}

// calculates the shortest path
function shortestpath(dp)
{
  // initializing all distances
  // as -1
  for (var i = 0; i <= V; i++)
    for (var j = 0; j < V; j++)
      dp[i][j] = -1;

  // shortest distance from
  // first vertex to in tself
  // consisting of 0 edges
  dp[0][0] = 0;

  // filling up the dp table
  for (var i = 1; i <= V; i++)
  {
    for (var j = 0; j < V; j++)
    {
      for (var k = 0;
               k < edges[j].length; k++)
      {
        if (dp[i - 1][
               edges[j][k].from] != -1)
        {
          var curr_wt = dp[i - 1][
                           edges[j][k].from] +
                           edges[j][k].weight;
          if (dp[i][j] == -1)
            dp[i][j] = curr_wt;
          else
            dp[i][j] = Math.min(dp[i][j],
                                curr_wt);
        }
      }
    }
  }
}

// Returns minimum value of
// average weight of a cycle
// in graph.
function minAvgWeight()
{
  var dp = Array.from(Array(V+1), ()=>Array(V).fill(0))
  shortestpath(dp);

  // array to store the
  // avg values
  var avg = Array(V).fill(0);

  for (var i = 0; i < V; i++)
    avg[i] = -1;

  // Compute average values for
  // all vertices using weights
  // of shortest paths store in dp.
  for (var i = 0; i < V; i++)
  {
    if (dp[V][i] != -1)
    {
      for (var j = 0; j < V; j++)
        if (dp[j][i] != -1)
          avg[i] = Math.max(avg[i],
                           ( dp[V][i] -
                             dp[j][i]) /
                             (V - j));
    }
  }

  // Find minimum value in avg[]
  var result = avg[0];

  for (var i = 0; i < V; i++)
    if (avg[i] != -1 &&
        avg[i] < result)
      result = avg[i];

  return result;
}

// Driver Code
addedge(0, 1, 1);
addedge(0, 2, 10);
addedge(1, 2, 3);
addedge(2, 3, 2);
addedge(3, 1, 0);
addedge(3, 0, 8);
document.write(minAvgWeight().toFixed(5));

</script>
```

**输出:**

```
1.66667
```

这里没有循环的图将返回值为-1。
**参考:**
[https://courses . csail . MIT . edu/6.046/fall 01/讲义/ps9 sol . pdf](https://courses.csail.mit.edu/6.046/fall01/handouts/ps9sol.pdf)
[https://www . hackereath . com/practice/notes/Karp-最小均方加权循环/](https://www.hackerearth.com/practice/notes/karp-minimum-mean-weighted-cycle/)
算法导论第三版第 681 页作者:Thomas H. Cormen，Charles E. Leiserson，罗纳德·L·李维斯特和 Clifford Stein
本文由【如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。