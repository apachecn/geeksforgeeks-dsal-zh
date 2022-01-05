# Prim 的最小生成树(MST) |贪婪算法-5

> 原文:[https://www . geesforgeks . org/prims-最小生成树-mst-greedy-algo-5/](https://www.geeksforgeeks.org/prims-minimum-spanning-tree-mst-greedy-algo-5/)

我们已经讨论了最小生成树的算法。和克鲁斯卡尔的算法一样，普里姆的算法也是[贪婪算法](https://www.geeksforgeeks.org/archives/18528)。它从一个空的生成树开始。这个想法是保持两组顶点。第一个集合包含已经包含在 MST 中的顶点，另一个集合包含尚未包含的顶点。在每一步中，它都会考虑连接这两个集合的所有边，并从这些边中挑选权重最小的边。拾取边后，它会将边的另一个端点移动到包含 MST 的集合中。
连接图中两组顶点的一组边在图论中称为[割](http://en.wikipedia.org/wiki/Cut_%28graph_theory%29)。*所以，在 Prim 算法的每一步，我们找到一个割(两个集合的割，一个包含已经包含在 MST 中的顶点，另一个包含剩余的顶点)，从割中挑选最小权重边，并将这个顶点包含到 MST 集合(包含已经包含的顶点的集合)。*

***Prim 的算法是如何工作的？***Prim 算法背后的思想很简单，一棵生成树意味着所有顶点都必须连通。因此两个不相交的顶点子集(如上所述)必须连接起来，以形成一个*生成*树。并且它们必须与最小权边连接，使其成为*最小*生成树。

***算法***
**1)** 创建一个集合 *mstSet* 来跟踪已经包含在 MST 中的顶点。
**2)** 为输入图形中的所有顶点分配一个键值。将所有键值初始化为 INFINITE。为第一个顶点指定键值为 0，以便首先拾取它。
**3)** 而 mstSet 不包括所有顶点
…。 **a)** 拾取一个顶点 *u* ，该顶点不在 *mstSet* 中，且具有最小关键值。
…。 **b)** 包括 *u* 到 mstSet。
…。 **c)** 更新 *u* 所有相邻顶点的键值。要更新键值，迭代所有相邻的顶点。对于每一个相邻的顶点 *v* ，如果边 *u-v* 的权重小于上一个 *v* 的键值，将键值更新为*u-v*T40】的权重，使用键值的思路是从[切](http://en.wikipedia.org/wiki/Cut_(graph_theory))中拾取最小权重的边。键值仅用于尚未包含在 MST 中的顶点，这些顶点的键值指示将它们连接到包含在 MST 中的顶点集的最小权重边。

让我们用下面的例子来理解:

[![Prim’s Minimum Spanning Tree](img/f4164d3a1cad2c61fbd1ef4aab72ab7a.png)](https://www.geeksforgeeks.org/wp-content/uploads/Fig-11.jpg)

集合 *mstSet* 最初为空，分配给顶点的键为{0，INF，INF，INF，INF，INF，INF，INF，INF}，其中 INF 表示无限。现在选择具有最小键值的顶点。顶点 0 被拾取，包括在 *mstSet* 中。所以 *mstSet* 变成了{0}。包含到 *mstSet* 后，更新相邻顶点的键值。0 的相邻顶点是 1 和 7。1 和 7 的键值更新为 4 和 8。下面的子图显示了顶点及其键值，只显示了键值有限的顶点。MST 中包含的顶点以绿色显示。

[![Prim’s Minimum Spanning Tree Algorithm 1](img/1dc515cdf61e19cfa8c73ea1ac12135d.png)](https://www.geeksforgeeks.org/wp-content/uploads/MST1.jpg)

拾取具有最小键值且尚未包含在 MST 中的顶点(不在 mstSET 中)。顶点 1 被拾取并添加到 mstSet。所以 mstSet 现在变成了{0，1}。更新相邻顶点的键值 1。顶点 2 的键值变成 8。

[![Prim’s Minimum Spanning Tree Algorithm 2](img/282f826cb599f98cbd4d7de3b68eaeb0.png)](https://www.geeksforgeeks.org/wp-content/uploads/MST2.jpg)

拾取具有最小键值且尚未包含在 MST 中的顶点(不在 mstSET 中)。我们可以选择顶点 7 或顶点 2，让顶点 7 被选择。所以 mstSet 现在变成了{0，1，7}。更新 7 的相邻顶点的键值。顶点 6 和 8 的键值变得有限(分别为 1 和 7)。

[![Prim’s Minimum Spanning Tree Algorithm 3](img/5b0180de55a947f0707e79ee89c09562.png)](https://www.geeksforgeeks.org/wp-content/uploads/MST3.jpg)

拾取具有最小键值且尚未包含在 MST 中的顶点(不在 mstSET 中)。顶点 6 被拾取。所以 mstSet 现在变成了{0，1，7，6}。更新 6 的相邻顶点的键值。顶点 5 和 8 的键值被更新。

[![Prim’s Minimum Spanning Tree Algorithm 4](img/324459e8bbafe5f5a6cffbd058ccf36d.png)](https://www.geeksforgeeks.org/wp-content/uploads/MST4.jpg)

我们重复以上步骤，直到 *mstSet* 包括给定图的所有顶点。最后，我们得到了下图。

[![Prim’s Minimum Spanning Tree Algorithm 5](img/ae64c938f36beae884d9dbc4af34383f.png)](https://www.geeksforgeeks.org/wp-content/uploads/MST5.jpg)

***如何实现上述算法？***
我们用一个布尔数组 mstSet[]来表示包含在 MST 中的顶点集。如果值 mstSet[v]为真，则顶点 v 包含在 MST 中，否则不包含。数组键[]用于存储所有顶点的键值。另一个数组 parent[]用于存储 MST 中父节点的索引。父数组是输出数组，用于显示构造的 MST。

## C++

```
// A C++ program for Prim's Minimum
// Spanning Tree (MST) algorithm. The program is
// for adjacency matrix representation of the graph
#include <bits/stdc++.h>
using namespace std;

// Number of vertices in the graph
#define V 5

// A utility function to find the vertex with
// minimum key value, from the set of vertices
// not yet included in MST
int minKey(int key[], bool mstSet[])
{
    // Initialize min value
    int min = INT_MAX, min_index;

    for (int v = 0; v < V; v++)
        if (mstSet[v] == false && key[v] < min)
            min = key[v], min_index = v;

    return min_index;
}

// A utility function to print the
// constructed MST stored in parent[]
void printMST(int parent[], int graph[V][V])
{
    cout<<"Edge \tWeight\n";
    for (int i = 1; i < V; i++)
        cout<<parent[i]<<" - "<<i<<" \t"<<graph[i][parent[i]]<<" \n";
}

// Function to construct and print MST for
// a graph represented using adjacency
// matrix representation
void primMST(int graph[V][V])
{
    // Array to store constructed MST
    int parent[V];

    // Key values used to pick minimum weight edge in cut
    int key[V];

    // To represent set of vertices included in MST
    bool mstSet[V];

    // Initialize all keys as INFINITE
    for (int i = 0; i < V; i++)
        key[i] = INT_MAX, mstSet[i] = false;

    // Always include first 1st vertex in MST.
    // Make key 0 so that this vertex is picked as first vertex.
    key[0] = 0;
    parent[0] = -1; // First node is always root of MST

    // The MST will have V vertices
    for (int count = 0; count < V - 1; count++)
    {
        // Pick the minimum key vertex from the
        // set of vertices not yet included in MST
        int u = minKey(key, mstSet);

        // Add the picked vertex to the MST Set
        mstSet[u] = true;

        // Update key value and parent index of
        // the adjacent vertices of the picked vertex.
        // Consider only those vertices which are not
        // yet included in MST
        for (int v = 0; v < V; v++)

            // graph[u][v] is non zero only for adjacent vertices of m
            // mstSet[v] is false for vertices not yet included in MST
            // Update the key only if graph[u][v] is smaller than key[v]
            if (graph[u][v] && mstSet[v] == false && graph[u][v] < key[v])
                parent[v] = u, key[v] = graph[u][v];
    }

    // print the constructed MST
    printMST(parent, graph);
}

// Driver code
int main()
{
    /* Let us create the following graph
        2 3
    (0)--(1)--(2)
    | / \ |
    6| 8/ \5 |7
    | / \ |
    (3)-------(4)
            9     */
    int graph[V][V] = { { 0, 2, 0, 6, 0 },
                        { 2, 0, 3, 8, 5 },
                        { 0, 3, 0, 0, 7 },
                        { 6, 8, 0, 0, 9 },
                        { 0, 5, 7, 9, 0 } };

    // Print the solution
    primMST(graph);

    return 0;
}

// This code is contributed by rathbhupendra
```

## C

```
// A C program for Prim's Minimum
// Spanning Tree (MST) algorithm. The program is
// for adjacency matrix representation of the graph
#include <limits.h>
#include <stdbool.h>
#include <stdio.h>
// Number of vertices in the graph
#define V 5

// A utility function to find the vertex with
// minimum key value, from the set of vertices
// not yet included in MST
int minKey(int key[], bool mstSet[])
{
    // Initialize min value
    int min = INT_MAX, min_index;

    for (int v = 0; v < V; v++)
        if (mstSet[v] == false && key[v] < min)
            min = key[v], min_index = v;

    return min_index;
}

// A utility function to print the
// constructed MST stored in parent[]
int printMST(int parent[], int graph[V][V])
{
    printf("Edge \tWeight\n");
    for (int i = 1; i < V; i++)
        printf("%d - %d \t%d \n", parent[i], i, graph[i][parent[i]]);
}

// Function to construct and print MST for
// a graph represented using adjacency
// matrix representation
void primMST(int graph[V][V])
{
    // Array to store constructed MST
    int parent[V];
    // Key values used to pick minimum weight edge in cut
    int key[V];
    // To represent set of vertices included in MST
    bool mstSet[V];

    // Initialize all keys as INFINITE
    for (int i = 0; i < V; i++)
        key[i] = INT_MAX, mstSet[i] = false;

    // Always include first 1st vertex in MST.
    // Make key 0 so that this vertex is picked as first vertex.
    key[0] = 0;
    parent[0] = -1; // First node is always root of MST

    // The MST will have V vertices
    for (int count = 0; count < V - 1; count++) {
        // Pick the minimum key vertex from the
        // set of vertices not yet included in MST
        int u = minKey(key, mstSet);

        // Add the picked vertex to the MST Set
        mstSet[u] = true;

        // Update key value and parent index of
        // the adjacent vertices of the picked vertex.
        // Consider only those vertices which are not
        // yet included in MST
        for (int v = 0; v < V; v++)

            // graph[u][v] is non zero only for adjacent vertices of m
            // mstSet[v] is false for vertices not yet included in MST
            // Update the key only if graph[u][v] is smaller than key[v]
            if (graph[u][v] && mstSet[v] == false && graph[u][v] < key[v])
                parent[v] = u, key[v] = graph[u][v];
    }

    // print the constructed MST
    printMST(parent, graph);
}

// driver program to test above function
int main()
{
    /* Let us create the following graph
        2 3
    (0)--(1)--(2)
    | / \ |
    6| 8/ \5 |7
    | /     \ |
    (3)-------(4)
            9         */
    int graph[V][V] = { { 0, 2, 0, 6, 0 },
                        { 2, 0, 3, 8, 5 },
                        { 0, 3, 0, 0, 7 },
                        { 6, 8, 0, 0, 9 },
                        { 0, 5, 7, 9, 0 } };

    // Print the solution
    primMST(graph);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java program for Prim's Minimum Spanning Tree (MST) algorithm.
// The program is for adjacency matrix representation of the graph

import java.util.*;
import java.lang.*;
import java.io.*;

class MST {
    // Number of vertices in the graph
    private static final int V = 5;

    // A utility function to find the vertex with minimum key
    // value, from the set of vertices not yet included in MST
    int minKey(int key[], Boolean mstSet[])
    {
        // Initialize min value
        int min = Integer.MAX_VALUE, min_index = -1;

        for (int v = 0; v < V; v++)
            if (mstSet[v] == false && key[v] < min) {
                min = key[v];
                min_index = v;
            }

        return min_index;
    }

    // A utility function to print the constructed MST stored in
    // parent[]
    void printMST(int parent[], int graph[][])
    {
        System.out.println("Edge \tWeight");
        for (int i = 1; i < V; i++)
            System.out.println(parent[i] + " - " + i + "\t" + graph[i][parent[i]]);
    }

    // Function to construct and print MST for a graph represented
    // using adjacency matrix representation
    void primMST(int graph[][])
    {
        // Array to store constructed MST
        int parent[] = new int[V];

        // Key values used to pick minimum weight edge in cut
        int key[] = new int[V];

        // To represent set of vertices included in MST
        Boolean mstSet[] = new Boolean[V];

        // Initialize all keys as INFINITE
        for (int i = 0; i < V; i++) {
            key[i] = Integer.MAX_VALUE;
            mstSet[i] = false;
        }

        // Always include first 1st vertex in MST.
        key[0] = 0; // Make key 0 so that this vertex is
        // picked as first vertex
        parent[0] = -1; // First node is always root of MST

        // The MST will have V vertices
        for (int count = 0; count < V - 1; count++) {
            // Pick thd minimum key vertex from the set of vertices
            // not yet included in MST
            int u = minKey(key, mstSet);

            // Add the picked vertex to the MST Set
            mstSet[u] = true;

            // Update key value and parent index of the adjacent
            // vertices of the picked vertex. Consider only those
            // vertices which are not yet included in MST
            for (int v = 0; v < V; v++)

                // graph[u][v] is non zero only for adjacent vertices of m
                // mstSet[v] is false for vertices not yet included in MST
                // Update the key only if graph[u][v] is smaller than key[v]
                if (graph[u][v] != 0 && mstSet[v] == false && graph[u][v] < key[v]) {
                    parent[v] = u;
                    key[v] = graph[u][v];
                }
        }

        // print the constructed MST
        printMST(parent, graph);
    }

    public static void main(String[] args)
    {
        /* Let us create the following graph
        2 3
        (0)--(1)--(2)
        | / \ |
        6| 8/ \5 |7
        | /     \ |
        (3)-------(4)
            9         */
        MST t = new MST();
        int graph[][] = new int[][] { { 0, 2, 0, 6, 0 },
                                      { 2, 0, 3, 8, 5 },
                                      { 0, 3, 0, 0, 7 },
                                      { 6, 8, 0, 0, 9 },
                                      { 0, 5, 7, 9, 0 } };

        // Print the solution
        t.primMST(graph);
    }
}
// This code is contributed by Aakash Hasija
```

## 计算机编程语言

```
# A Python program for Prim's Minimum Spanning Tree (MST) algorithm.
# The program is for adjacency matrix representation of the graph

import sys # Library for INT_MAX

class Graph():

    def __init__(self, vertices):
        self.V = vertices
        self.graph = [[0 for column in range(vertices)]
                    for row in range(vertices)]

    # A utility function to print the constructed MST stored in parent[]
    def printMST(self, parent):
        print "Edge \tWeight"
        for i in range(1, self.V):
            print parent[i], "-", i, "\t", self.graph[i][ parent[i] ]

    # A utility function to find the vertex with
    # minimum distance value, from the set of vertices
    # not yet included in shortest path tree
    def minKey(self, key, mstSet):

        # Initialize min value
        min = sys.maxsize

        for v in range(self.V):
            if key[v] < min and mstSet[v] == False:
                min = key[v]
                min_index = v

        return min_index

    # Function to construct and print MST for a graph
    # represented using adjacency matrix representation
    def primMST(self):

        # Key values used to pick minimum weight edge in cut
        key = [sys.maxsize] * self.V
        parent = [None] * self.V # Array to store constructed MST
        # Make key 0 so that this vertex is picked as first vertex
        key[0] = 0
        mstSet = [False] * self.V

        parent[0] = -1 # First node is always the root of

        for cout in range(self.V):

            # Pick the minimum distance vertex from
            # the set of vertices not yet processed.
            # u is always equal to src in first iteration
            u = self.minKey(key, mstSet)

            # Put the minimum distance vertex in
            # the shortest path tree
            mstSet[u] = True

            # Update dist value of the adjacent vertices
            # of the picked vertex only if the current
            # distance is greater than new distance and
            # the vertex in not in the shortest path tree
            for v in range(self.V):

                # graph[u][v] is non zero only for adjacent vertices of m
                # mstSet[v] is false for vertices not yet included in MST
                # Update the key only if graph[u][v] is smaller than key[v]
                if self.graph[u][v] > 0 and mstSet[v] == False and key[v] > self.graph[u][v]:
                        key[v] = self.graph[u][v]
                        parent[v] = u

        self.printMST(parent)

g = Graph(5)
g.graph = [ [0, 2, 0, 6, 0],
            [2, 0, 3, 8, 5],
            [0, 3, 0, 0, 7],
            [6, 8, 0, 0, 9],
            [0, 5, 7, 9, 0]]

g.primMST();

# Contributed by Divyanshu Mehta
```

## C#

```
// A C# program for Prim's Minimum
// Spanning Tree (MST) algorithm.
// The program is for adjacency
// matrix representation of the graph
using System;
class MST {

    // Number of vertices in the graph
    static int V = 5;

    // A utility function to find
    // the vertex with minimum key
    // value, from the set of vertices
    // not yet included in MST
    static int minKey(int[] key, bool[] mstSet)
    {

        // Initialize min value
        int min = int.MaxValue, min_index = -1;

        for (int v = 0; v < V; v++)
            if (mstSet[v] == false && key[v] < min) {
                min = key[v];
                min_index = v;
            }

        return min_index;
    }

    // A utility function to print
    // the constructed MST stored in
    // parent[]
    static void printMST(int[] parent, int[, ] graph)
    {
        Console.WriteLine("Edge \tWeight");
        for (int i = 1; i < V; i++)
            Console.WriteLine(parent[i] + " - " + i + "\t" + graph[i, parent[i]]);
    }

    // Function to construct and
    // print MST for a graph represented
    // using adjacency matrix representation
    static void primMST(int[, ] graph)
    {

        // Array to store constructed MST
        int[] parent = new int[V];

        // Key values used to pick
        // minimum weight edge in cut
        int[] key = new int[V];

        // To represent set of vertices
        // included in MST
        bool[] mstSet = new bool[V];

        // Initialize all keys
        // as INFINITE
        for (int i = 0; i < V; i++) {
            key[i] = int.MaxValue;
            mstSet[i] = false;
        }

        // Always include first 1st vertex in MST.
        // Make key 0 so that this vertex is
        // picked as first vertex
        // First node is always root of MST
        key[0] = 0;
        parent[0] = -1;

        // The MST will have V vertices
        for (int count = 0; count < V - 1; count++) {

            // Pick thd minimum key vertex
            // from the set of vertices
            // not yet included in MST
            int u = minKey(key, mstSet);

            // Add the picked vertex
            // to the MST Set
            mstSet[u] = true;

            // Update key value and parent
            // index of the adjacent vertices
            // of the picked vertex. Consider
            // only those vertices which are
            // not yet included in MST
            for (int v = 0; v < V; v++)

                // graph[u][v] is non zero only
                // for adjacent vertices of m
                // mstSet[v] is false for vertices
                // not yet included in MST Update
                // the key only if graph[u][v] is
                // smaller than key[v]
                if (graph[u, v] != 0 && mstSet[v] == false
                    && graph[u, v] < key[v]) {
                    parent[v] = u;
                    key[v] = graph[u, v];
                }
        }

        // print the constructed MST
        printMST(parent, graph);
    }

    // Driver Code
    public static void Main()
    {

        /* Let us create the following graph
        2 3
        (0)--(1)--(2)
        | / \ |
        6| 8/ \5 |7
        | / \ |
        (3)-------(4)
            9 */

        int[, ] graph = new int[, ] { { 0, 2, 0, 6, 0 },
                                      { 2, 0, 3, 8, 5 },
                                      { 0, 3, 0, 0, 7 },
                                      { 6, 8, 0, 0, 9 },
                                      { 0, 5, 7, 9, 0 } };

        // Print the solution
        primMST(graph);
    }
}

// This code is contributed by anuj_67.
```

## java 描述语言

```
<script>

// Number of vertices in the graph
let V = 5;

// A utility function to find the vertex with
// minimum key value, from the set of vertices
// not yet included in MST
function minKey(key, mstSet)
{
    // Initialize min value
    let min = Number.MAX_VALUE, min_index;

    for (let v = 0; v < V; v++)
        if (mstSet[v] == false && key[v] < min)
            min = key[v], min_index = v;

    return min_index;
}

// A utility function to print the
// constructed MST stored in parent[]
function printMST(parent, graph)
{
    document.write("Edge      Weight" + "<br>");
    for (let i = 1; i < V; i++)
        document.write(parent[i] + "   -  " + i + "     " + graph[i][parent[i]] + "<br>");
}

// Function to construct and print MST for
// a graph represented using adjacency
// matrix representation
function primMST(graph)
{
    // Array to store constructed MST
    let parent = [];

    // Key values used to pick minimum weight edge in cut
    let key = [];

    // To represent set of vertices included in MST
    let mstSet = [];

    // Initialize all keys as INFINITE
    for (let i = 0; i < V; i++)
        key[i] = Number.MAX_VALUE, mstSet[i] = false;

    // Always include first 1st vertex in MST.
    // Make key 0 so that this vertex is picked as first vertex.
    key[0] = 0;
    parent[0] = -1; // First node is always root of MST

    // The MST will have V vertices
    for (let count = 0; count < V - 1; count++)
    {
        // Pick the minimum key vertex from the
        // set of vertices not yet included in MST
        let u = minKey(key, mstSet);

        // Add the picked vertex to the MST Set
        mstSet[u] = true;

        // Update key value and parent index of
        // the adjacent vertices of the picked vertex.
        // Consider only those vertices which are not
        // yet included in MST
        for (let v = 0; v < V; v++)

            // graph[u][v] is non zero only for adjacent vertices of m
            // mstSet[v] is false for vertices not yet included in MST
            // Update the key only if graph[u][v] is smaller than key[v]
            if (graph[u][v] && mstSet[v] == false && graph[u][v] < key[v])
                parent[v] = u, key[v] = graph[u][v];
    }

    // print the constructed MST
    printMST(parent, graph);
}

// Driver code

/* Let us create the following graph
    2 3
    (0)--(1)--(2)
    | / \ |
    6| 8/ \5 |7
    | / \ |
    (3)-------(4)
    9     */

let graph = [ [ 0, 2, 0, 6, 0 ],
[ 2, 0, 3, 8, 5 ],
[ 0, 3, 0, 0, 7 ],
[ 6, 8, 0, 0, 9 ],
[ 0, 5, 7, 9, 0 ] ];

// Print the solution
primMST(graph);

// This code is contributed by Dharanendra L V.
</script>
```

**输出:**

```
Edge   Weight
0 - 1    2
1 - 2    3
0 - 3    6
1 - 4    5
```

上述程序的时间复杂度是 O(V^2).如果输入的[图用邻接表](https://www.geeksforgeeks.org/archives/27134)表示，那么 Prim 算法的时间复杂度可以借助二进制堆降低到 O(E log V)。更多详细信息，请参见 [Prim 的邻接表表示法](https://www.geeksforgeeks.org/greedy-algorithms-set-5-prims-mst-for-adjacency-list-representation/)。

？list = plqm7 alhxfysghrb9iq-jxdhLUriW-V6wr
如果发现有不正确的地方，或者想分享更多关于上面讨论的话题的信息，请写评论。