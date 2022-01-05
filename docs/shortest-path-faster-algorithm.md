# 最短路径快速算法

> 原文:[https://www . geesforgeks . org/最短路径-更快-算法/](https://www.geeksforgeeks.org/shortest-path-faster-algorithm/)

**先决条件:** [贝尔曼-福特算法](https://www.geeksforgeeks.org/bellman-ford-algorithm-dp-23/)
给定一个具有 **V** 顶点、 **E** 边和一个源顶点 **S** 的**有向加权图**。任务是找到从源顶点到给定图中所有其他顶点的最短路径。
**例:**

> **输入:** V = 5，S = 1，arr = {{1，2，1}、{2，3，7}、{2，4，-2}、{1，3，8}、{1，4，9}、{3，4，3}、{2，5，3}、{4，5，-3}}
> **输出:**
> 1，0
> 2，1
> 3，8
> 4，-1
> 5，-4【T100】
> **输入:** V = 5，S = 1，arr = {{1，2，-1}、{1，3，4}、{2，3，3}、{2，4，2}、{2，5，2}、{4，3，5}、{4，2，1}、{5，4，3}}
> **输出:**
> 1，0
> 2，-1
> 3，2
> 4

**方法:**最短路径快速算法基于[贝尔曼-福特](https://www.geeksforgeeks.org/bellman-ford-algorithm-dp-23/)算法，其中每个顶点都用于放松其相邻的顶点，但是在 SPF 算法中，保持一个顶点队列，并且只有当该顶点放松时，才将该顶点添加到队列中。重复这个过程，直到没有顶点可以放松。
可以执行以下步骤来计算结果:

1.  创建一个数组 **d[]** 来存储所有顶点到源顶点的最短距离。除了 d[S] = 0(其中 **S** 是源顶点)之外，将该数组初始化为无穷大。
2.  创建一个[队列](http://www.geeksforgeeks.org/queue-data-structure/) **Q** 并在其中推送起始源顶点。
    *   当队列不为空时，对图中的每条边(u，v)执行以下操作
        *   如果 d[v] > d[u] +边的权重(u，v)
        *   d[v] = d[u] +边的权重(u，v)
        *   如果顶点 v 不在队列中，则将顶点 v 推入队列。

**注意:**术语**松弛**意味着更新连接到顶点 **v** 的所有顶点的成本，如果这些成本通过包括经由顶点 **v** 的路径而得到改善的话。从最短路径的估计和螺旋拉伸弹簧的长度之间的类比可以更好地理解这一点，螺旋拉伸弹簧不是为压缩而设计的。最初，最短路径的成本被高估了，就像一个伸展的弹簧。随着更短路径的发现，估计成本降低，弹簧放松。最终，找到了最短的路径，如果有的话，弹簧被放松到其静止长度。
以下是上述方法的实施:

## C++

```
// C++ implementation of SPFA

#include <bits/stdc++.h>
using namespace std;

// Graph is stored as vector of vector of pairs
// first element of pair store vertex
// second element of pair store weight
vector<vector<pair<int, int> >> graph;

// Function to add edges in the graph
// connecting a pair of vertex(frm) and weight
// to another vertex(to) in graph
void addEdge(int frm, int to, int weight)
{

    graph[frm].push_back({ to, weight });
}

// Function to print shortest distance from source
void print_distance(int d[], int V)
{
    cout << "Vertex \t\t Distance"
         << " from source" << endl;

    for (int i = 1; i <= V; i++) {
        cout << i << "             " << d[i] << '\n';
    }
}

// Function to compute the SPF algorithm
void shortestPathFaster(int S, int V)
{
    // Create array d to store shortest distance
    int d[V + 1];

    // Boolean array to check if vertex
    // is present in queue or not
    bool inQueue[V + 1] = { false };

    // Initialize the distance from source to
    // other vertex as INT_MAX(infinite)
    for (int i = 0; i <= V; i++) {
        d[i] = INT_MAX;
    }
    d[S] = 0;

    queue<int> q;
    q.push(S);
    inQueue[S] = true;

    while (!q.empty()) {

        // Take the front vertex from Queue
        int u = q.front();
        q.pop();
        inQueue[u] = false;

        // Relaxing all the adjacent edges of
        // vertex taken from the Queue
        for (int i = 0; i < graph[u].size(); i++) {

            int v = graph[u][i].first;
            int weight = graph[u][i].second;

            if (d[v] > d[u] + weight) {
                d[v] = d[u] + weight;

                // Check if vertex v is in Queue or not
                // if not then push it into the Queue
                if (!inQueue[v]) {
                    q.push(v);
                    inQueue[v] = true;
                }
            }
        }
    }

    // Print the result
    print_distance(d, V);
}

// Driver code
int main()
{
    int V = 5;
    int S = 1;

      graph = vector<vector<pair<int,int>>> (V+1);
    // Connect vertex a to b with weight w
    // addEdge(a, b, w)

    addEdge(1, 2, 1);
    addEdge(2, 3, 7);
    addEdge(2, 4, -2);
    addEdge(1, 3, 8);
    addEdge(1, 4, 9);
    addEdge(3, 4, 3);
    addEdge(2, 5, 3);
    addEdge(4, 5, -3);

    // Calling shortestPathFaster function
    shortestPathFaster(S, V);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of SPFA
import java.util.*;

class GFG
{
    static class pair
    {
        int first, second;
        public pair(int first, int second)
        {
            this.first = first;
            this.second = second;
        }
    }

// Graph is stored as vector of vector of pairs
// first element of pair store vertex
// second element of pair store weight
static Vector<pair > []graph = new Vector[100000];

// Function to add edges in the graph
// connecting a pair of vertex(frm) and weight
// to another vertex(to) in graph
static void addEdge(int frm, int to, int weight)
{

    graph[frm].add(new pair( to, weight ));
}

// Function to print shortest distance from source
static void print_distance(int d[], int V)
{
    System.out.print("Vertex \t\t Distance"
        + " from source" +"\n");

    for (int i = 1; i <= V; i++)
    {
        System.out.printf("%d \t\t %d\n", i, d[i]);
    }
}

// Function to compute the SPF algorithm
static void shortestPathFaster(int S, int V)
{
    // Create array d to store shortest distance
    int []d = new int[V + 1];

    // Boolean array to check if vertex
    // is present in queue or not
    boolean []inQueue = new boolean[V + 1];

    // Initialize the distance from source to
    // other vertex as Integer.MAX_VALUE(infinite)
    for (int i = 0; i <= V; i++)
    {
        d[i] = Integer.MAX_VALUE;
    }
    d[S] = 0;

    Queue<Integer> q = new LinkedList<>();
    q.add(S);
    inQueue[S] = true;

    while (!q.isEmpty())
    {

        // Take the front vertex from Queue
        int u = q.peek();
        q.remove();
        inQueue[u] = false;

        // Relaxing all the adjacent edges of
        // vertex taken from the Queue
        for (int i = 0; i < graph[u].size(); i++)
        {

            int v = graph[u].get(i).first;
            int weight = graph[u].get(i).second;

            if (d[v] > d[u] + weight)
            {
                d[v] = d[u] + weight;

                // Check if vertex v is in Queue or not
                // if not then push it into the Queue
                if (!inQueue[v])
                {
                    q.add(v);
                    inQueue[v] = true;
                }
            }
        }
    }

    // Print the result
    print_distance(d, V);
}

// Driver code
public static void main(String[] args)
{
    int V = 5;
    int S = 1;
    for (int i = 0; i < graph.length; i++)
    {
        graph[i] = new Vector<pair>();
    }

    // Connect vertex a to b with weight w
    // addEdge(a, b, w)
    addEdge(1, 2, 1);
    addEdge(2, 3, 7);
    addEdge(2, 4, -2);
    addEdge(1, 3, 8);
    addEdge(1, 4, 9);
    addEdge(3, 4, 3);
    addEdge(2, 5, 3);
    addEdge(4, 5, -3);

    // Calling shortestPathFaster function
    shortestPathFaster(S, V);
}
}

// This code is contributed by 29AjayKumar
```

## C#

```
// C# implementation of SPFA
using System;
using System.Collections.Generic;

class GFG
{
    class pair
    {
        public int first, second;
        public pair(int first, int second)
        {
            this.first = first;
            this.second = second;
        }
    }

// Graph is stored as vector of vector of pairs
// first element of pair store vertex
// second element of pair store weight
static List<pair> []graph = new List<pair>[100000];

// Function to add edges in the graph
// connecting a pair of vertex(frm) and weight
// to another vertex(to) in graph
static void addEdge(int frm, int to, int weight)
{

    graph[frm].Add(new pair( to, weight ));
}

// Function to print shortest distance from source
static void print_distance(int []d, int V)
{
    Console.Write("Vertex \t\t Distance"
        + " from source" +"\n");

    for (int i = 1; i <= V; i++)
    {
        Console.Write("{0} \t\t {1}\n", i, d[i]);
    }
}

// Function to compute the SPF algorithm
static void shortestPathFaster(int S, int V)
{
    // Create array d to store shortest distance
    int []d = new int[V + 1];

    // Boolean array to check if vertex
    // is present in queue or not
    bool []inQueue = new bool[V + 1];

    // Initialize the distance from source to
    // other vertex as int.MaxValue(infinite)
    for (int i = 0; i <= V; i++)
    {
        d[i] = int.MaxValue;
    }
    d[S] = 0;

    Queue<int> q = new Queue<int>();
    q.Enqueue(S);
    inQueue[S] = true;

    while (q.Count!=0)
    {

        // Take the front vertex from Queue
        int u = q.Peek();
        q.Dequeue();
        inQueue[u] = false;

        // Relaxing all the adjacent edges of
        // vertex taken from the Queue
        for (int i = 0; i < graph[u].Count; i++)
        {

            int v = graph[u][i].first;
            int weight = graph[u][i].second;

            if (d[v] > d[u] + weight)
            {
                d[v] = d[u] + weight;

                // Check if vertex v is in Queue or not
                // if not then push it into the Queue
                if (!inQueue[v])
                {
                    q.Enqueue(v);
                    inQueue[v] = true;
                }
            }
        }
    }

    // Print the result
    print_distance(d, V);
}

// Driver code
public static void Main(String[] args)
{
    int V = 5;
    int S = 1;
    for (int i = 0; i < graph.Length; i++)
    {
        graph[i] = new List<pair>();
    }

    // Connect vertex a to b with weight w
    // addEdge(a, b, w)
    addEdge(1, 2, 1);
    addEdge(2, 3, 7);
    addEdge(2, 4, -2);
    addEdge(1, 3, 8);
    addEdge(1, 4, 9);
    addEdge(3, 4, 3);
    addEdge(2, 5, 3);
    addEdge(4, 5, -3);

    // Calling shortestPathFaster function
    shortestPathFaster(S, V);
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of SPFA
from collections import deque

# Graph is stored as vector of vector of pairs
# first element of pair store vertex
# second element of pair store weight
graph = [[] for _ in range(100000)]

# Function to add edges in the graph
# connecting a pair of vertex(frm) and weight
# to another vertex(to) in graph
def addEdge(frm, to, weight):

    graph[frm].append([to, weight])

# Function to prshortest distance from source
def print_distance(d, V):
    print("Vertex","\t","Distance from source")

    for i in range(1, V + 1):
        print(i,"\t",d[i])

# Function to compute the SPF algorithm
def shortestPathFaster(S, V):

    # Create array d to store shortest distance
    d = [10**9]*(V + 1)

    # Boolean array to check if vertex
    # is present in queue or not
    inQueue = [False]*(V + 1)

    d[S] = 0

    q = deque()
    q.append(S)
    inQueue[S] = True

    while (len(q) > 0):

        # Take the front vertex from Queue
        u = q.popleft()
        inQueue[u] = False

        # Relaxing all the adjacent edges of
        # vertex taken from the Queue
        for i in range(len(graph[u])):

            v = graph[u][i][0]
            weight = graph[u][i][1]

            if (d[v] > d[u] + weight):
                d[v] = d[u] + weight

                # Check if vertex v is in Queue or not
                # if not then append it into the Queue
                if (inQueue[v] == False):
                    q.append(v)
                    inQueue[v] = True

    # Print the result
    print_distance(d, V)

# Driver code
if __name__ == '__main__':
    V = 5
    S = 1

    # Connect vertex a to b with weight w
    # addEdge(a, b, w)

    addEdge(1, 2, 1)
    addEdge(2, 3, 7)
    addEdge(2, 4, -2)
    addEdge(1, 3, 8)
    addEdge(1, 4, 9)
    addEdge(3, 4, 3)
    addEdge(2, 5, 3)
    addEdge(4, 5, -3)

    # Calling shortestPathFaster function
    shortestPathFaster(S, V)

# This code is contributed by mohit kumar 29
```

## java 描述语言

```
<script>

// JavaScript implementation of SPFA

 // Graph is stored as vector of vector of pairs
// first element of pair store vertex
// second element of pair store weight
    let graph=new Array(100000);

    // Function to add edges in the graph
// connecting a pair of vertex(frm) and weight
// to another vertex(to) in graph
    function addEdge(frm,to,weight)
    {
        graph[frm].push([to, weight ]);
    }

    // Function to print shortest distance from source
    function print_distance(d,V)
    {
        document.write(
   "Vertex", " ", "Distance" + " from source" +"<br>"
        );

    for (let i = 1; i <= V; i++)
    {
        document.write( i+"     "+
        d[i]+"<br>");
    }
    }

    // Function to compute the SPF algorithm
    function shortestPathFaster(S,V)
    {
        // Create array d to store shortest distance
    let d = new Array(V + 1);

    // Boolean array to check if vertex
    // is present in queue or not
    let inQueue = new Array(V + 1);

    // Initialize the distance from source to
    // other vertex as Integer.MAX_VALUE(infinite)
    for (let i = 0; i <= V; i++)
    {
        d[i] = Number.MAX_VALUE;
    }
    d[S] = 0;

    let q = [];
    q.push(S);
    inQueue[S] = true;

    while (q.length!=0)
    {

        // Take the front vertex from Queue
        let u = q[0];
        q.shift();
        inQueue[u] = false;

        // Relaxing all the adjacent edges of
        // vertex taken from the Queue
        for (let i = 0; i < graph[u].length; i++)
        {

            let v = graph[u][i][0];
            let weight = graph[u][i][1];

            if (d[v] > d[u] + weight)
            {
                d[v] = d[u] + weight;

                // Check if vertex v is in Queue or not
                // if not then push it into the Queue
                if (!inQueue[v])
                {
                    q.push(v);
                    inQueue[v] = true;
                }
            }
        }
    }

    // Print the result
    print_distance(d, V);
    }

    // Driver code
    let V = 5;
    let S = 1;
    for (let i = 0; i < graph.length; i++)
    {
        graph[i] = [];
    }

    // Connect vertex a to b with weight w
    // addEdge(a, b, w)
    addEdge(1, 2, 1);
    addEdge(2, 3, 7);
    addEdge(2, 4, -2);
    addEdge(1, 3, 8);
    addEdge(1, 4, 9);
    addEdge(3, 4, 3);
    addEdge(2, 5, 3);
    addEdge(4, 5, -3);

    // Calling shortestPathFaster function
    shortestPathFaster(S, V);

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
Vertex    Distance from source
1          0
2          1
3          8
4          -1
5          -4
```

**时间复杂度:**
**平均时间复杂度:** O(|E|)
**最差案例时间复杂度** : O(|V|。|E|)
**注:**平均运行时上界尚未证明。
**参考文献:** [最短路径快速算法](https://en.wikipedia.org/wiki/Shortest_Path_Faster_Algorithm)