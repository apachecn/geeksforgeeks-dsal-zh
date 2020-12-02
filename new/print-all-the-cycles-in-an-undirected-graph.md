# 在无向图中打印所有循环

> 原文： [https://www.geeksforgeeks.org/print-all-the-cycles-in-an-undirected-graph/](https://www.geeksforgeeks.org/print-all-the-cycles-in-an-undirected-graph/)

给定一个无向图，请打印在其中形成循环的所有顶点。
**前提条件**：[使用颜色](https://www.geeksforgeeks.org/detect-cycle-direct-graph-using-colors/)，
在有向图中检测循环。

![](img/2a7a28e0e1677574cb31e8c7408c7af0.png)

在上图中，循环已用深绿色标记。 上面的输出将是

> **第一周期**：3 5 4 6
> **第二周期**：11 12 13

**方法**：使用[图形着色方法](https://www.geeksforgeeks.org/detect-cycle-direct-graph-using-colors/)，用唯一编号标记不同循环的所有顶点。 图形遍历完成后，将所有相似的标记数字推入邻接表，并相应地打印邻接表。 下面给出的是算法：

*   将边插入邻接表。
*   调用 DFS 函数，该函数使用着色方法标记顶点。
*   每当有部分访问的顶点时，都将**回溯**直到到达当前顶点，并用周期号标记所有这些顶点。 标记所有顶点后，增加循环数。
*   Dfs 完成后，迭代边缘，并将相同的标记数字边缘推到另一个邻接列表。
*   迭代另一个邻接表并明智地打印顶点循环数。

下面是上述方法的实现：

## C++

```cpp

// C++ program to print all the cycles
// in an undirected graph
#include <bits/stdc++.h>
using namespace std;
const int N = 100000;

// variables to be used
// in both functions
vector<int> graph[N];
vector<int> cycles[N];

// Function to mark the vertex with
// different colors for different cycles
void dfs_cycle(int u, int p, int color[],
               int mark[], int par[], int& cyclenumber)
{

    // already (completely) visited vertex.
    if (color[u] == 2) {
        return;
    }

    // seen vertex, but was not completely visited -> cycle detected.
    // backtrack based on parents to find the complete cycle.
    if (color[u] == 1) {

        cyclenumber++;
        int cur = p;
        mark[cur] = cyclenumber;

        // backtrack the vertex which are
        // in the current cycle thats found
        while (cur != u) {
            cur = par[cur];
            mark[cur] = cyclenumber;
        }
        return;
    }
    par[u] = p;

    // partially visited.
    color[u] = 1;

    // simple dfs on graph
    for (int v : graph[u]) {

        // if it has not been visited previously
        if (v == par[u]) {
            continue;
        }
        dfs_cycle(v, u, color, mark, par, cyclenumber);
    }

    // completely visited.
    color[u] = 2;
}

// add the edges to the graph
void addEdge(int u, int v)
{
    graph[u].push_back(v);
    graph[v].push_back(u);
}

// Function to print the cycles
void printCycles(int edges, int mark[], int& cyclenumber)
{

    // push the edges that into the
    // cycle adjacency list
    for (int i = 1; i <= edges; i++) {
        if (mark[i] != 0)
            cycles[mark[i]].push_back(i);
    }

    // print all the vertex with same cycle
    for (int i = 1; i <= cyclenumber; i++) {
        // Print the i-th cycle
        cout << "Cycle Number " << i << ": ";
        for (int x : cycles[i])
            cout << x << " ";
        cout << endl;
    }
}

// Driver Code
int main()
{

    // add edges
    addEdge(1, 2);
    addEdge(2, 3);
    addEdge(3, 4);
    addEdge(4, 6);
    addEdge(4, 7);
    addEdge(5, 6);
    addEdge(3, 5);
    addEdge(7, 8);
    addEdge(6, 10);
    addEdge(5, 9);
    addEdge(10, 11);
    addEdge(11, 12);
    addEdge(11, 13);
    addEdge(12, 13);

    // arrays required to color the
    // graph, store the parent of node
    int color[N];
    int par[N];

    // mark with unique numbers
    int mark[N];

    // store the numbers of cycle
    int cyclenumber = 0;
    int edges = 13;

    // call DFS to mark the cycles
    dfs_cycle(1, 0, color, mark, par, cyclenumber);

    // function to print the cycles
    printCycles(edges, mark, cyclenumber);
}

```

## Java

```java

// Java program to print all the cycles 
// in an undirected graph 
import java.util.*;

class GFG 
{

    static final int N = 100000;

    // variables to be used
    // in both functions
    @SuppressWarnings("unchecked")
    static Vector<Integer>[] graph = new Vector[N];
    @SuppressWarnings("unchecked")
    static Vector<Integer>[] cycles = new Vector[N];
    static int cyclenumber;

    // Function to mark the vertex with
    // different colors for different cycles
    static void dfs_cycle(int u, int p, int[] color, 
                       int[] mark, int[] par)
    {

        // already (completely) visited vertex.
        if (color[u] == 2)
        {
            return;
        }

        // seen vertex, but was not completely visited -> cycle detected.
        // backtrack based on parents to find the complete cycle.
        if (color[u] == 1)
        {

            cyclenumber++;
            int cur = p;
            mark[cur] = cyclenumber;

            // backtrack the vertex which are
            // in the current cycle thats found
            while (cur != u)
            {
                cur = par[cur];
                mark[cur] = cyclenumber;
            }
            return;
        }
        par[u] = p;

        // partially visited.
        color[u] = 1;

        // simple dfs on graph
        for (int v : graph[u])
        {

            // if it has not been visited previously
            if (v == par[u])
            {
                continue;
            }
            dfs_cycle(v, u, color, mark, par);
        }

        // completely visited.
        color[u] = 2;
    }

    // add the edges to the graph
    static void addEdge(int u, int v) 
    {
        graph[u].add(v);
        graph[v].add(u);
    }

    // Function to print the cycles
    static void printCycles(int edges, int mark[])
    {

        // push the edges that into the
        // cycle adjacency list
        for (int i = 1; i <= edges; i++)
        {
            if (mark[i] != 0)
                cycles[mark[i]].add(i);
        }

        // print all the vertex with same cycle
        for (int i = 1; i <= cyclenumber; i++)
        {
            // Print the i-th cycle
            System.out.printf("Cycle Number %d: ", i);
            for (int x : cycles[i])
                System.out.printf("%d ", x);
            System.out.println();
        }
    }

    // Driver Code
    public static void main(String[] args)
    {

        for (int i = 0; i < N; i++)
        {
            graph[i] = new Vector<>();
            cycles[i] = new Vector<>();
        }

        // add edges
        addEdge(1, 2);
        addEdge(2, 3);
        addEdge(3, 4);
        addEdge(4, 6);
        addEdge(4, 7);
        addEdge(5, 6);
        addEdge(3, 5);
        addEdge(7, 8);
        addEdge(6, 10);
        addEdge(5, 9);
        addEdge(10, 11);
        addEdge(11, 12);
        addEdge(11, 13);
        addEdge(12, 13);

        // arrays required to color the
        // graph, store the parent of node
        int[] color = new int[N];
        int[] par = new int[N];

        // mark with unique numbers
        int[] mark = new int[N];

        // store the numbers of cycle
        cyclenumber = 0;
        int edges = 13;

        // call DFS to mark the cycles
        dfs_cycle(1, 0, color, mark, par);

        // function to print the cycles
        printCycles(edges, mark);
    }
}

// This code is contributed by
// sanjeev2552

```

## Python3

```

# Python3 program to print all the cycles
# in an undirected graph
N = 100000

# variables to be used
# in both functions
graph = [[] for i in range(N)]
cycles = [[] for i in range(N)]

# Function to mark the vertex with
# different colors for different cycles
def dfs_cycle(u, p, color: list,
              mark: list, par: list):
    global cyclenumber

    # already (completely) visited vertex.
    if color[u] == 2:
        return

    # seen vertex, but was not 
    # completely visited -> cycle detected.
    # backtrack based on parents to
    # find the complete cycle.
    if color[u] == 1:
        cyclenumber += 1
        cur = p
        mark[cur] = cyclenumber

        # backtrack the vertex which are
        # in the current cycle thats found
        while cur != u:
            cur = par[cur]
            mark[cur] = cyclenumber

        return

    par[u] = p

    # partially visited.
    color[u] = 1

    # simple dfs on graph
    for v in graph[u]:

        # if it has not been visited previously
        if v == par[u]:
            continue
        dfs_cycle(v, u, color, mark, par)

    # completely visited.
    color[u] = 2

# add the edges to the graph
def addEdge(u, v):
    graph[u].append(v)
    graph[v].append(u)

# Function to print the cycles
def printCycles(edges, mark: list):

    # push the edges that into the
    # cycle adjacency list
    for i in range(1, edges + 1):
        if mark[i] != 0:
            cycles[mark[i]].append(i)

    # print all the vertex with same cycle
    for i in range(1, cyclenumber + 1):

        # Print the i-th cycle
        print("Cycle Number %d:" % i, end = " ")
        for x in cycles[i]:
            print(x, end = " ")
        print()

# Driver Code
if __name__ == "__main__":

    # add edges
    addEdge(1, 2)
    addEdge(2, 3)
    addEdge(3, 4)
    addEdge(4, 6)
    addEdge(4, 7)
    addEdge(5, 6)
    addEdge(3, 5)
    addEdge(7, 8)
    addEdge(6, 10)
    addEdge(5, 9)
    addEdge(10, 11)
    addEdge(11, 12)
    addEdge(11, 13)
    addEdge(12, 13)

    # arrays required to color the
    # graph, store the parent of node
    color = [0] * N
    par = [0] * N

    # mark with unique numbers
    mark = [0] * N

    # store the numbers of cycle
    cyclenumber = 0
    edges = 13

    # call DFS to mark the cycles
    dfs_cycle(1, 0, color, mark, par)

    # function to print the cycles
    printCycles(edges, mark)

# This code is contributed by
# sanjeev2552

```

## C#

```cs

// C# program to print all
// the cycles in an undirected 
// graph 
using System;
using System.Collections.Generic;
class GFG{

static readonly int N = 100000;

// variables to be used
// in both functions
static List<int>[] graph = 
       new List<int>[N];
static List<int>[] cycles = 
       new List<int>[N];
static int cyclenumber;

// Function to mark the vertex with
// different colors for different cycles
static void dfs_cycle(int u, int p, 
                      int[] color, 
                      int[] mark, 
                      int[] par)
{
  // already (completely)
  // visited vertex.
  if (color[u] == 2)
  {
    return;
  }

  // seen vertex, but was not 
  // completely visited -> cycle 
  // detected. backtrack based on 
  // parents to find the complete
  // cycle.
  if (color[u] == 1)
  {
    cyclenumber++;
    int cur = p;
    mark[cur] = cyclenumber;

    // backtrack the vertex which 
    // are in the current cycle 
    // thats found
    while (cur != u)
    {
      cur = par[cur];
      mark[cur] = cyclenumber;
    }
    return;
  }
  par[u] = p;

  // partially visited.
  color[u] = 1;

  // simple dfs on graph
  foreach (int v in graph[u])
  {
    // if it has not been 
    // visited previously
    if (v == par[u])
    {
      continue;
    }
    dfs_cycle(v, u, color, 
              mark, par);
  }

  // completely visited.
  color[u] = 2;
}

// add the edges to the 
// graph
static void addEdge(int u, 
                    int v) 
{
  graph[u].Add(v);
  graph[v].Add(u);
}

// Function to print the cycles
static void printCycles(int edges,
                        int []mark)
{
  // push the edges that into the
  // cycle adjacency list
  for (int i = 1; i <= edges; i++)
  {
    if (mark[i] != 0)
      cycles[mark[i]].Add(i);
  }

  // print all the vertex with 
  // same cycle
  for (int i = 1; 
           i <= cyclenumber; i++)
  {
    // Print the i-th cycle
    Console.Write("Cycle Number " + i + ":");
    foreach (int x in cycles[i])
      Console.Write(" " + x);
    Console.WriteLine();
  }
}

// Driver Code
public static void Main(String[] args)
{
  for (int i = 0; i < N; i++)
  {
    graph[i] = new List<int>();
    cycles[i] = new List<int>();
  }

  // add edges
  addEdge(1, 2);
  addEdge(2, 3);
  addEdge(3, 4);
  addEdge(4, 6);
  addEdge(4, 7);
  addEdge(5, 6);
  addEdge(3, 5);
  addEdge(7, 8);
  addEdge(6, 10);
  addEdge(5, 9);
  addEdge(10, 11);
  addEdge(11, 12);
  addEdge(11, 13);
  addEdge(12, 13);

  // arrays required to color 
  // the graph, store the parent 
  // of node
  int[] color = new int[N];
  int[] par = new int[N];

  // mark with unique numbers
  int[] mark = new int[N];

  // store the numbers of cycle
  cyclenumber = 0;
  int edges = 13;

  // call DFS to mark 
  // the cycles
  dfs_cycle(1, 0, color,
            mark, par);

  // function to print the cycles
  printCycles(edges, mark);
}
}

// This code is contributed by Amit Katiyar

```

**输出**：

```
Cycle Number 1: 3 4 5 6 
Cycle Number 2: 11 12 13 

```

**时间复杂度**：O（N + M），其中 N 是顶点数，M 是边数。
**辅助空间**：O（N + M）



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。