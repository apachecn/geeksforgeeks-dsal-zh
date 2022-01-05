# 贝尔曼福特算法(简单实现)

> 原文:[https://www . geesforgeks . org/bellman-Ford-algorithm-simple-implementation/](https://www.geeksforgeeks.org/bellman-ford-algorithm-simple-implementation/)

我们已经介绍了贝尔曼·福特，并在此讨论了实施。
*输入:*图形和一个源顶点 *src*
输出:从 *src* 到所有顶点的最短距离。如果存在负重量循环，则不计算最短距离，而是报告负重量循环。
**1)** 此步骤将从源到所有顶点的距离初始化为无穷大，到源本身的距离初始化为 0。创建一个大小为|V|的数组 dist[]，除了 dist[src]以外，所有值都为无穷大，其中 src 是源顶点。
**2)** 此步骤计算最短距离。执行以下|V|-1 次，其中|V|是给定图中的顶点数。
….. **a)** 对每个边缘 u-v
………………如果 dist[v] > dist[u] +边缘 uv 的权重，则更新 dist[v]
……………………。dist[v] = dist[u] +边缘 uv 的权重
**3)** 此步骤报告图形中是否存在负权重循环。对每个边 u-v
……如果 dist[v] > dist[u] +边 uv 的权重，那么“图形包含负权重循环”
步骤 3 的思想是，如果图形不包含负权重循环，步骤 2 保证最短距离。如果我们再次遍历所有边，得到任意顶点的较短路径，那么就有一个负权重循环
**例**
让我们用下面的例图来理解算法。图片来自[这个](http://www.cs.arizona.edu/classes/cs445/spring07/ShortestPath2.prn.pdf)源。
让给定的源顶点为 0。将所有距离初始化为无穷大，到源本身的距离除外。图中顶点总数为 5，因此*所有边必须处理 4 次。*

![Example Graph](img/566868a605baa6b2dadb4d9184a7c629.png)

让所有边按以下顺序处理:(B，E)，(D，B)，(B，D)，(A，B)，(A，C)，(D，C)，(B，C)，(E，D)。第一次处理所有边时，我们得到以下距离。中的第一行显示初始距离。第二行显示处理边(B，E)、(D，B)、(B，D)和(A，B)时的距离。第三行显示处理(A，C)时的距离。第四行显示处理(D，C)、(B，C)和(E，D)的时间。

![](img/27e4581ddb941b8bdb551d8ffb84321e.png)

第一次迭代保证给出所有最短路径，其长度最多为 1 条边。第二次处理所有边时，我们得到以下距离(最后一行显示最终值)。

![](img/c5fc23a47dc1ccc7a2de578ec1d30ee5.png)

第二次迭代保证给出所有最短路径，其长度最多为 2 条边。该算法将所有边再处理 2 次。距离在第二次迭代后被最小化，所以第三次和第四次迭代不会更新距离。

## C++

```
// A C++ program for Bellman-Ford's single source
// shortest path algorithm.
#include <bits/stdc++.h>
using namespace std;

// The main function that finds shortest
// distances from src to all other vertices
// using Bellman-Ford algorithm. The function
// also detects negative weight cycle
// The row graph[i] represents i-th edge with
// three values u, v and w.
void BellmanFord(int graph[][3], int V, int E,
                 int src)
{
    // Initialize distance of all vertices as infinite.
    int dis[V];
    for (int i = 0; i < V; i++)
        dis[i] = INT_MAX;

    // initialize distance of source as 0
    dis[src] = 0;

    // Relax all edges |V| - 1 times. A simple
    // shortest path from src to any other
    // vertex can have at-most |V| - 1 edges
    for (int i = 0; i < V - 1; i++) {

        for (int j = 0; j < E; j++) {
            if (dis[graph[j][0]] != INT_MAX && dis[graph[j][0]] + graph[j][2] <
                               dis[graph[j][1]])
                dis[graph[j][1]] =
                  dis[graph[j][0]] + graph[j][2];
        }
    }

    // check for negative-weight cycles.
    // The above step guarantees shortest
    // distances if graph doesn't contain
    // negative weight cycle.  If we get a
    // shorter path, then there is a cycle.
    for (int i = 0; i < E; i++) {
        int x = graph[i][0];
        int y = graph[i][1];
        int weight = graph[i][2];
        if (dis[x] != INT_MAX &&
                   dis[x] + weight < dis[y])
            cout << "Graph contains negative"
                    " weight cycle"
                 << endl;
    }

    cout << "Vertex Distance from Source" << endl;
    for (int i = 0; i < V; i++)
        cout << i << "\t\t" << dis[i] << endl;
}

// Driver program to test above functions
int main()
{
    int V = 5; // Number of vertices in graph
    int E = 8; // Number of edges in graph

    // Every edge has three values (u, v, w) where
    // the edge is from vertex u to v. And weight
    // of the edge is w.
    int graph[][3] = { { 0, 1, -1 }, { 0, 2, 4 },
                       { 1, 2, 3 }, { 1, 3, 2 },
                       { 1, 4, 2 }, { 3, 2, 5 },
                       { 3, 1, 1 }, { 4, 3, -3 } };

    BellmanFord(graph, V, E, 0);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java program for Bellman-Ford's single source
// shortest path algorithm.

class GFG
{

// The main function that finds shortest
// distances from src to all other vertices
// using Bellman-Ford algorithm. The function
// also detects negative weight cycle
// The row graph[i] represents i-th edge with
// three values u, v and w.
static void BellmanFord(int graph[][], int V, int E,
                int src)
{
    // Initialize distance of all vertices as infinite.
    int []dis = new int[V];
    for (int i = 0; i < V; i++)
        dis[i] = Integer.MAX_VALUE;

    // initialize distance of source as 0
    dis[src] = 0;

    // Relax all edges |V| - 1 times. A simple
    // shortest path from src to any other
    // vertex can have at-most |V| - 1 edges
    for (int i = 0; i < V - 1; i++)
    {

        for (int j = 0; j < E; j++)
        {
            if (dis[graph[j][0]] != Integer.MAX_VALUE && dis[graph[j][0]] + graph[j][2] <
                            dis[graph[j][1]])
                dis[graph[j][1]] =
                dis[graph[j][0]] + graph[j][2];
        }
    }

    // check for negative-weight cycles.
    // The above step guarantees shortest
    // distances if graph doesn't contain
    // negative weight cycle. If we get a
    // shorter path, then there is a cycle.
    for (int i = 0; i < E; i++)
    {
        int x = graph[i][0];
        int y = graph[i][1];
        int weight = graph[i][2];
        if (dis[x] != Integer.MAX_VALUE &&
                dis[x] + weight < dis[y])
            System.out.println("Graph contains negative"
                    +" weight cycle");
    }

    System.out.println("Vertex Distance from Source");
    for (int i = 0; i < V; i++)
        System.out.println(i + "\t\t" + dis[i]);
}

// Driver code
public static void main(String[] args)
{
    int V = 5; // Number of vertices in graph
    int E = 8; // Number of edges in graph

    // Every edge has three values (u, v, w) where
    // the edge is from vertex u to v. And weight
    // of the edge is w.
    int graph[][] = { { 0, 1, -1 }, { 0, 2, 4 },
                    { 1, 2, 3 }, { 1, 3, 2 },
                    { 1, 4, 2 }, { 3, 2, 5 },
                    { 3, 1, 1 }, { 4, 3, -3 } };

    BellmanFord(graph, V, E, 0);
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for Bellman-Ford's
# single source shortest path algorithm.
from sys import maxsize

# The main function that finds shortest
# distances from src to all other vertices
# using Bellman-Ford algorithm. The function
# also detects negative weight cycle
# The row graph[i] represents i-th edge with
# three values u, v and w.
def BellmanFord(graph, V, E, src):

    # Initialize distance of all vertices as infinite.
    dis = [maxsize] * V

    # initialize distance of source as 0
    dis[src] = 0

    # Relax all edges |V| - 1 times. A simple
    # shortest path from src to any other
    # vertex can have at-most |V| - 1 edges
    for i in range(V - 1):
        for j in range(E):
            if dis[graph[j][0]] + \
                   graph[j][2] < dis[graph[j][1]]:
                dis[graph[j][1]] = dis[graph[j][0]] + \
                                       graph[j][2]

    # check for negative-weight cycles.
    # The above step guarantees shortest
    # distances if graph doesn't contain
    # negative weight cycle. If we get a
    # shorter path, then there is a cycle.
    for i in range(E):
        x = graph[i][0]
        y = graph[i][1]
        weight = graph[i][2]
        if dis[x] != maxsize and dis[x] + \
                        weight < dis[y]:
            print("Graph contains negative weight cycle")

    print("Vertex Distance from Source")
    for i in range(V):
        print("%d\t\t%d" % (i, dis[i]))

# Driver Code
if __name__ == "__main__":
    V = 5 # Number of vertices in graph
    E = 8 # Number of edges in graph

    # Every edge has three values (u, v, w) where
    # the edge is from vertex u to v. And weight
    # of the edge is w.
    graph = [[0, 1, -1], [0, 2, 4], [1, 2, 3],
             [1, 3, 2], [1, 4, 2], [3, 2, 5],
             [3, 1, 1], [4, 3, -3]]
    BellmanFord(graph, V, E, 0)

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program for Bellman-Ford's single source
// shortest path algorithm.
using System;

class GFG
{

// The main function that finds shortest
// distances from src to all other vertices
// using Bellman-Ford algorithm. The function
// also detects negative weight cycle
// The row graph[i] represents i-th edge with
// three values u, v and w.
static void BellmanFord(int [,]graph, int V,
                        int E, int src)
{
    // Initialize distance of all vertices as infinite.
    int []dis = new int[V];
    for (int i = 0; i < V; i++)
        dis[i] = int.MaxValue;

    // initialize distance of source as 0
    dis[src] = 0;

    // Relax all edges |V| - 1 times. A simple
    // shortest path from src to any other
    // vertex can have at-most |V| - 1 edges
    for (int i = 0; i < V - 1; i++)
    {
        for (int j = 0; j < E; j++)
        {
            if (dis[graph[j, 0]] = int.MaxValue && dis[graph[j, 0]] + graph[j, 2] <
                dis[graph[j, 1]])
                dis[graph[j, 1]] =
                dis[graph[j, 0]] + graph[j, 2];
        }
    }

    // check for negative-weight cycles.
    // The above step guarantees shortest
    // distances if graph doesn't contain
    // negative weight cycle. If we get a
    // shorter path, then there is a cycle.
    for (int i = 0; i < E; i++)
    {
        int x = graph[i, 0];
        int y = graph[i, 1];
        int weight = graph[i, 2];
        if (dis[x] != int.MaxValue &&
                dis[x] + weight < dis[y])
            Console.WriteLine("Graph contains negative" +
                                        " weight cycle");
    }

    Console.WriteLine("Vertex Distance from Source");
    for (int i = 0; i < V; i++)
        Console.WriteLine(i + "\t\t" + dis[i]);
}

// Driver code
public static void Main(String[] args)
{
    int V = 5; // Number of vertices in graph
    int E = 8; // Number of edges in graph

    // Every edge has three values (u, v, w) where
    // the edge is from vertex u to v. And weight
    // of the edge is w.
    int [,]graph = {{ 0, 1, -1 }, { 0, 2, 4 },
                    { 1, 2, 3 }, { 1, 3, 2 },
                    { 1, 4, 2 }, { 3, 2, 5 },
                    { 3, 1, 1 }, { 4, 3, -3 }};

    BellmanFord(graph, V, E, 0);
}
}

// This code is contributed by Princi Singh
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A PHP program for Bellman-Ford's single
// source shortest path algorithm.

// The main function that finds shortest
// distances from src to all other vertices
// using Bellman-Ford algorithm. The function
// also detects negative weight cycle
// The row graph[i] represents i-th edge with
// three values u, v and w.
function BellmanFord($graph, $V, $E, $src)
{
    // Initialize distance of all vertices as infinite.
    $dis = array();
    for ($i = 0; $i < $V; $i++)
        $dis[$i] = PHP_INT_MAX;

    // initialize distance of source as 0
    $dis[$src] = 0;

    // Relax all edges |V| - 1 times. A simple
    // shortest path from src to any other
    // vertex can have at-most |V| - 1 edges
    for ($i = 0; $i < $V - 1; $i++)
    {
        for ($j = 0; $j < $E; $j++)
        {
            if ($dis[$graph[$j][0]] != PHP_INT_MAX && $dis[$graph[$j][0]] + $graph[$j][2] <
                                 $dis[$graph[$j][1]])
                $dis[$graph[$j][1]] = $dis[$graph[$j][0]] +    
                                           $graph[$j][2];
        }
    }

    // check for negative-weight cycles.
    // The above step guarantees shortest
    // distances if graph doesn't contain
    // negative weight cycle. If we get a
    // shorter path, then there is a cycle.
    for ($i = 0; $i < $E; $i++)
    {
        $x = $graph[$i][0];
        $y = $graph[$i][1];
        $weight = $graph[$i][2];
        if ($dis[$x] != PHP_INT_MAX &&
            $dis[$x] + $weight < $dis[$y])
            echo "Graph contains negative weight cycle \n";
    }

    echo "Vertex Distance from Source \n";
    for ($i = 0; $i < $V; $i++)
        echo $i, "\t\t", $dis[$i], "\n";
}

// Driver Code
$V = 5; // Number of vertices in graph
$E = 8; // Number of edges in graph

// Every edge has three values (u, v, w) where
// the edge is from vertex u to v. And weight
// of the edge is w.
$graph = array( array( 0, 1, -1 ), array( 0, 2, 4 ),
                array( 1, 2, 3 ), array( 1, 3, 2 ),
                array( 1, 4, 2 ), array( 3, 2, 5),
                array( 3, 1, 1), array( 4, 3, -3 ) );

BellmanFord($graph, $V, $E, 0);

// This code is contributed by AnkitRai01
?>
```

## java 描述语言

```
<script>

// Javascript program for Bellman-Ford's single source
// shortest path algorithm.

// The main function that finds shortest
// distances from src to all other vertices
// using Bellman-Ford algorithm. The function
// also detects negative weight cycle
// The row graph[i] represents i-th edge with
// three values u, v and w.
function BellmanFord(graph, V, E, src)
{
    // Initialize distance of all vertices as infinite.
    var dis = Array(V).fill(1000000000);

    // initialize distance of source as 0
    dis[src] = 0;

    // Relax all edges |V| - 1 times. A simple
    // shortest path from src to any other
    // vertex can have at-most |V| - 1 edges
    for (var i = 0; i < V - 1; i++)
    {
        for (var j = 0; j < E; j++)
        {
            if ((dis[graph[j][0]] + graph[j][2]) < dis[graph[j][1]])
                dis[graph[j][1]] = dis[graph[j][0]] + graph[j][2];
        }
    }

    // check for negative-weight cycles.
    // The above step guarantees shortest
    // distances if graph doesn't contain
    // negative weight cycle. If we get a
    // shorter path, then there is a cycle.
    for (var i = 0; i < E; i++)
    {
        var x = graph[i][0];
        var y = graph[i][1];
        var weight = graph[i][2];
        if ((dis[x] != 1000000000) &&
                (dis[x] + weight < dis[y]))
            document.write("Graph contains negative" +
                                        " weight cycle<br>");
    }

    document.write("Vertex Distance from Source<br>");
    for (var i = 0; i < V; i++)
        document.write(i + "   " + dis[i] + "<br>");
}

// Driver code
var V = 5; // Number of vertices in graph
var E = 8; // Number of edges in graph

// Every edge has three values (u, v, w) where
// the edge is from vertex u to v. And weight
// of the edge is w.
var graph = [[ 0, 1, -1 ], [ 0, 2, 4 ],
                [ 1, 2, 3 ], [ 1, 3, 2 ],
                [ 1, 4, 2 ], [ 3, 2, 5 ],
                [ 3, 1, 1 ], [ 4, 3, -3 ]];
BellmanFord(graph, V, E, 0);

// This code is contributed by importantly.
</script>
```

**Output:** 

```
Vertex Distance from Source
0        0
1        -1
2        2
3        -2
4        1
```

**时间复杂度:** O(VE)
这个实现由[**prateekupt10**](https://auth.geeksforgeeks.org/user/PrateekGupta10)
提出