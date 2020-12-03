# 检查所有连通组件的长度是否为斐波那契数

> 原文： [https://www.geeksforgeeks.org/check-if-the-length-of-all-connected-components-is-a-fibonacci-number/](https://www.geeksforgeeks.org/check-if-the-length-of-all-connected-components-is-a-fibonacci-number/)

给定具有`V`顶点和`E`边的无向图，任务是找到图的所有连接部分，并检查它们的每个长度是否都是**斐波那契数**。

例如，考虑下图。

![](img/04b31f134d4b95d9099a2af641344cf3.png)

如上所述，连通组件的长度是 2、3 和 2，它们是斐波那契数。

**示例**：[

> **输入**：E = 4，V = 7
> 
> ![](img/9255bcb43473debac85556f66c0f8245.png)
> 
> **输出**：是
> **输入**：E = 6，V = 10
> 
> ![](img/beabc5855ca715c86b194a754a8f3b8e.png)
> 
> **输出**：否
> **说明**：连通组件{1}，{2、3、4、5}，{6、7、8}，{9 的长度 ，10}分别为 1，`4`，3、2。

**方法**：

预计算斐波纳契数并将其存储在 HashSet 中。 如本文章[中所述，使用 DFS 方法遍历顶点并生成 Connected 组件。 检查所有长度是否都存在于预先计算的斐波那契数的 HashSet 中。

以下是上述方法的实现：](https://www.geeksforgeeks.org/connected-components-in-an-undirected-graph/)

## C++

```cpp

// C++ program to check if the length of 
// all connected components are a 
// Fibonacci or not
#include <bits/stdc++.h>
using namespace std;

// Function to traverse graph using 
// DFS algorithm and track the
// connected components
void depthFirst(int v, vector<int> graph[],
                vector<bool>& visited, int& ans)
{
    // Mark the current vertex as visited
    visited[v] = true;

    // Variable ans to keep count of 
    // connected components
    ans++;
    for (auto i : graph[v]) {
        if (visited[i] == false) {
            depthFirst(i, graph, visited, ans);
        }
    }
}

// Function to check and print if the
// length of all connected components
// are a Fibonacci or not
void countConnectedFibonacci(vector<int> graph[], 
                                int V, int E)
{
    // Hash Container (Set) to store 
    // the Fibonacci sequence
    unordered_set<int> fibonacci;
    fibonacci.insert(0);
    fibonacci.insert(1);
    // Pre-computation of Fibonacci sequence
    long long a = 0,b = 1;
    for (int i = 2; i < 1001; i++) {
        fibonacci.insert(a + b);
        a = a+b;
        swap(a,b);
    }

    // Initializing boolean visited array 
    // to mark visited vertices
    vector<bool> visited(10001, false);

    // Following loop invokes DFS algorithm
    for (int i = 1; i <= V; i++) {
        if (visited[i] == false) {
            // ans variable stores the 
            // length of respective 
            // connected components
            int ans = 0;

            // DFS algorithm
            depthFirst(i, graph, visited, ans);
            if(fibonacci.find(ans) == fibonacci.end())
            {
                cout << "No"<<endl;
                return;
            }
        }
    }

    cout<<"Yes"<<endl;
}

// Driver code
int main()
{
    // Initializing graph in the form of adjacency list
    vector<int> graph[1001];

    // Defining the number of edges and vertices
    int E = 4,V = 7;

    // Constructing the undirected graph
    graph[1].push_back(2);
    graph[2].push_back(5);
    graph[3].push_back(4);
    graph[4].push_back(3);
    graph[3].push_back(6);
    graph[6].push_back(3);
    graph[8].push_back(7);
    graph[7].push_back(8);

    countConnectedFibonacci(graph, V, E);
    return 0;
}

```

## Java

```java

// Java program to check if the length of 
// all connected components are a 
// Fibonacci or not

import java.util.*;

class GFG{

// Function to traverse graph using 
// DFS algorithm and track the
// connected components
static void depthFirst(int v, Vector<Integer> graph[],
                boolean []visited, int ans)
{
    // Mark the current vertex as visited
    visited[v] = true;

    // Variable ans to keep count of 
    // connected components
    ans++;
    for (int i : graph[v]) {
        if (visited[i] == false) {
            depthFirst(i, graph, visited, ans);
        }
    }
}

// Function to check and print if the
// length of all connected components
// are a Fibonacci or not
static void countConnectedFibonacci(Vector<Integer> graph[], 
                                int V, int E)
{
    // Hash Container (Set) to store 
    // the Fibonacci sequence
    HashSet<Integer> fibonacci = new HashSet<Integer>();
    fibonacci.add(0);
    fibonacci.add(1);
    // Pre-computation of Fibonacci sequence
    int a = 0,b = 1;
    for (int i = 2; i < 1001; i++) {
        fibonacci.add(a + b);
        a = a + b;
        a = a + b;
        b = a - b;
        a = a - b;
    }

    // Initializing boolean visited array 
    // to mark visited vertices
    boolean []visited = new boolean[10001];

    // Following loop invokes DFS algorithm
    for (int i = 1; i <= V; i++) {
        if (visited[i] == false) {
            // ans variable stores the 
            // length of respective 
            // connected components
            int ans = 0;

            // DFS algorithm
            depthFirst(i, graph, visited, ans);
            if(!fibonacci.contains(ans))
            {
                System.out.println("No");
                return;
            }
        }
    }

    System.out.println("Yes");
}

// Driver code
public static void main(String[] args)
{
    // Initializing graph in the form of adjacency list
    Vector<Integer> []graph = new Vector[1001];
    for(int i = 0; i < graph.length; i++)
        graph[i] = new Vector<Integer>();

    // Defining the number of edges and vertices
    int E = 4,V = 7;

    // Constructing the undirected graph
    graph[1].add(2);
    graph[2].add(5);
    graph[3].add(4);
    graph[4].add(3);
    graph[3].add(6);
    graph[6].add(3);
    graph[8].add(7);
    graph[7].add(8);

    countConnectedFibonacci(graph, V, E);
}
}

// This code is contributed by 29AjayKumar

```

## C#

```cs

// C# program to check if the length of 
// all connected components are a 
// Fibonacci or not
using System;
using System.Collections.Generic;

class GFG{

// Function to traverse graph using 
// DFS algorithm and track the
// connected components
static void depthFirst(int v, List<int> []graph,
                         bool []visited, int ans)
{

    // Mark the current vertex as visited
    visited[v] = true;

    // Variable ans to keep count of 
    // connected components
    ans++;
    foreach(int i in graph[v]) 
    {
        if (visited[i] == false)
        {
            depthFirst(i, graph, visited, ans);
        }
    }
}

// Function to check and print if the
// length of all connected components
// are a Fibonacci or not
static void countConnectedFibonacci(List<int> []graph, 
                                    int V, int E)
{

    // Hash Container (Set) to store 
    // the Fibonacci sequence
    HashSet<int> fibonacci = new HashSet<int>();
    fibonacci.Add(0);
    fibonacci.Add(1);

    // Pre-computation of Fibonacci sequence
    int a = 0,b = 1;
    for(int i = 2; i < 1001; i++)
    {
        fibonacci.Add(a + b);
        a = a + b;
        a = a + b;
        b = a - b;
        a = a - b;
    }

    // Initializing bool visited array 
    // to mark visited vertices
    bool []visited = new bool[10001];

    // Following loop invokes DFS algorithm
    for(int i = 1; i <= V; i++)
    {
        if (visited[i] == false) 
        {

            // ans variable stores the 
            // length of respective 
            // connected components
            int ans = 0;

            // DFS algorithm
            depthFirst(i, graph, visited, ans);

            if(!fibonacci.Contains(ans))
            {
                Console.WriteLine("No");
                return;
            }
        }
    }
    Console.WriteLine("Yes");
}

// Driver code
public static void Main(String[] args)
{

    // Initializing graph in the 
    // form of adjacency list
    List<int> []graph = new List<int>[1001];
    for(int i = 0; i < graph.Length; i++)
        graph[i] = new List<int>();

    // Defining the number of edges and vertices
    int E = 4,V = 7;

    // Constructing the undirected graph
    graph[1].Add(2);
    graph[2].Add(5);
    graph[3].Add(4);
    graph[4].Add(3);
    graph[3].Add(6);
    graph[6].Add(3);
    graph[8].Add(7);
    graph[7].Add(8);

    countConnectedFibonacci(graph, V, E);
}
}

// This code is contributed by amal kumar choubey 

```

**Output:** 

```
Yes

```

**复杂度分析**：

程序的整体复杂度主要由三个因素决定，即深度优先遍历，从 Fibonacci 容器中识别元素以及对 Fibonacci 进行预计算 顺序。 DFS 遍历的时间复杂度为 **O（E + V）**，其中 E 和 V 是图形的边和顶点。 需要花费 **`O(1)`**时间复杂度来检查 HashSet 中是否存在特定长度。 初始预计算的时间复杂度为`O(N)`，其中 N 是斐波那契数列所存储的数字。

时间复杂度： *`O(N)`*。

**有效方法**：

该方法基本上避免了斐波那契预计算，并使用简单的公式来检查各个长度是否为斐波那契数。 检测 N 是否为斐波那契数的公式是找到 **5N <sup>2</sup> + 4** 和 **5N <sup>2</sup> – 4** 的值，以及 检查它们是否是**完美正方形**。 所述制剂是由 I Gessel 配制的，可以从[这个](http://www.maths.surrey.ac.uk/hosted-sites/R.Knott/Fibonacci/fibFormula.html#section5)链接中引用。 该程序的其余部分具有与上述类似的方法，即通过 DFS 遍历计算连通组件。

以下是上述方法的实现：

## C++

```cpp

// C++ program to check if the length of 
// all connected components are a 
// Fibonacci or not
#include <bits/stdc++.h>
using namespace std;

// Function to traverse graph using 
// DFS algorithm and track the
// connected components
void depthFirst(int v, vector<int> graph[],
                vector<bool>& visited, int& ans)
{
    // Mark the current vertex as visited
    visited[v] = true;

    // Variable ans to keep count of 
    // connected components
    ans++;
    for (auto i : graph[v]) {
        if (visited[i] == false) {
            depthFirst(i, graph, visited, ans);
        }
    }
}

// Function to check and print if the
// length of all connected components
// are a Fibonacci or not
void countConnectedFibonacci(vector<int> graph[], 
                                int V, int E)
{

    // Initializing boolean visited array 
    // to mark visited vertices
    vector<bool> visited(10001, false);

    // Following loop invokes DFS algorithm
    for (int i = 1; i <= V; i++) {
        if (visited[i] == false) {
            // ans variable stores the 
            // length of respective 
            // connected components
            int ans = 0;

            // DFS algorithm
            depthFirst(i, graph, visited, ans);

            double x1 = sqrt(5*ans*ans + 4);
            int x2 = sqrt(5 * ans * ans + 4);

            double y1 = sqrt(5*ans*ans - 4);
            int y2 = sqrt(5 * ans * ans - 4);

            if(!(x1 - x2) || !(y1 - y2))
                continue;
            else
            {
                cout << "No"<<endl;
                return;
            }
        }
    }

    cout<<"Yes"<<endl;
}

// Driver code
int main()
{
    // Initializing graph in the form of adjacency list
    vector<int> graph[1001];

    // Defining the number of edges and vertices
    int E = 4,V = 7;

    // Constructing the undirected graph
    graph[1].push_back(2);
    graph[2].push_back(1);
    graph[2].push_back(5);
    graph[5].push_back(2);
    graph[3].push_back(4);
    graph[4].push_back(3);
    graph[3].push_back(6);
    graph[6].push_back(3);
    graph[8].push_back(7);
    graph[7].push_back(8);

    countConnectedFibonacci(graph, V, E);
    return 0;
}

```

## Java

```java

// Java program to check if the length of 
// all connected components are a 
// Fibonacci or not
import java.util.*;
class GFG{

// Function to traverse graph using 
// DFS algorithm and track the
// connected components
static void depthFirst(int v, Vector<Integer> graph[],
                    Vector<Boolean> visited, int ans)
{
    // Mark the current vertex as visited
    visited.add(v, true);

    // Variable ans to keep count of 
    // connected components
    ans++;
    for (int i : graph[v]) 
    {
        if (visited.get(i) == false)
        {
            depthFirst(i, graph, visited, ans);
        }
    }
}

// Function to check and print if the
// length of all connected components
// are a Fibonacci or not
static void countConnectedFibonacci(Vector<Integer> graph[], 
                                    int V, int E)
{

    // Initializing boolean visited array 
    // to mark visited vertices
    Vector<Boolean> visited = new Vector<>(10001);
    for(int i = 0; i < 10001; i++)
        visited.add(i, false);

    // Following loop invokes DFS algorithm
    for (int i = 1; i < V; i++) 
    {
        if (visited.get(i) == false)
        {
            // ans variable stores the 
            // length of respective 
            // connected components
            int ans = 0;

            // DFS algorithm
            depthFirst(i, graph, visited, ans);

            double x1 = Math.sqrt(5 * ans * ans + 4);
            int x2 = (int)Math.sqrt(5 * ans * ans + 4);

            double y1 = Math.sqrt(5 * ans * ans - 4);
            int y2 = (int)Math.sqrt(5 * ans * ans - 4);

            if((x1 - x2) != 0 || (y1 - y2) != 0)
                continue;
            else
            {
                System.out.println("No");
                return;
            }
        }
    }
    System.out.println("Yes");
}

// Driver code
public static void main(String[] args)
{
    // Initializing graph in the form of adjacency list
    @SuppressWarnings("unchecked")
    Vector<Integer> []graph = new Vector[1001];
    for(int i = 0; i < 1001; i++)
        graph[i] = new Vector<Integer>();

    // Defining the number of edges and vertices
    int E = 4,V = 7;

    // Constructing the undirected graph
    graph[1].add(2);
    graph[2].add(1);
    graph[2].add(5);
    graph[5].add(2);
    graph[3].add(4);
    graph[4].add(3);
    graph[3].add(6);
    graph[6].add(3);
    graph[8].add(7);
    graph[7].add(8);

    countConnectedFibonacci(graph, V, E);
}
}

// This code is contributed by Rohit_ranjan

```

## C#

```cs

// C# program to check if the 
// length of all connected 
// components are a Fibonacci 
// or not
using System;
using System.Collections;
class GFG{

// Function to traverse graph using 
// DFS algorithm and track the
// connected components
static void depthFirst(int v, ArrayList []graph,
                       ArrayList visited, int ans)
{
  // Mark the current vertex 
  // as visited
  visited[v] = true;

  // Variable ans to keep count of 
  // connected components
  ans++;

  foreach(int i in graph[v]) 
  {
    if ((bool)visited[i] == false)
    {
      depthFirst(i, graph, visited, ans);
    }
  }
}

// Function to check and print if the
// length of all connected components
// are a Fibonacci or not
static void countConnectedFibonacci(ArrayList []graph, 
                                    int V, int E)
{
  // Initializing boolean visited array 
  // to mark visited vertices
  ArrayList visited = new ArrayList();
  for(int i = 0; i < 10001; i++)
    visited.Add(false);

  // Following loop invokes 
  // DFS algorithm
  for (int i = 1; i < V; i++) 
  {
    if ((bool)visited[i] == false)
    {
      // ans variable stores the 
      // length of respective 
      // connected components
      int ans = 0;

      // DFS algorithm
      depthFirst(i, graph, visited, ans);

      double x1 = Math.Sqrt(5 * ans * ans + 4);
      int x2 = (int)Math.Sqrt(5 * ans * ans + 4);

      double y1 = Math.Sqrt(5 * ans * ans - 4);
      int y2 = (int)Math.Sqrt(5 * ans * ans - 4);

      if((x1 - x2) != 0 || (y1 - y2) != 0)
        continue;
      else
      {
        Console.Write("No");
        return;
      }
    }
  }
  Console.Write("Yes");
}

// Driver code
public static void Main(string[] args)
{
  // Initializing graph in the 
  // form of adjacency list
  ArrayList []graph = 
              new ArrayList[1001];

  for(int i = 0; i < 1001; i++)
    graph[i] = new ArrayList();

  // Defining the number of 
  // edges and vertices
  int E = 4,
      V = 7;

  // Constructing the 
  // undirected graph
  graph[1].Add(2);
  graph[2].Add(1);
  graph[2].Add(5);
  graph[5].Add(2);
  graph[3].Add(4);
  graph[4].Add(3);
  graph[3].Add(6);
  graph[6].Add(3);
  graph[8].Add(7);
  graph[7].Add(8);

  countConnectedFibonacci(graph, V, E);
}
}

// This code is contributed by rutvik_56

```

**Output:** 

```
Yes

```

**复杂度分析**：

时间复杂度：`O(V + E)`

此方法避免了较早的预先计算，并使用数学公式来检测各个长度是否为斐波那契数。 因此，可以在恒定时间 **`O(1)`**和恒定空间中实现计算，因为它避免了使用任何 HashSet 来存储斐波那契数。 因此，仅通过 DFS 遍历即可确定此方法中程序的整体复杂性。 因此，复杂度为 **O（E + V）**，其中 E 和 V 是无向图的边和顶点数。

![competitive-programming-img](img/5211864e7e7a28eeeb039fa5d6073a24.png)

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。