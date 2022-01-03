# 无向图

中的欧拉路径

> 原文： [https://www.geeksforgeeks.org/eulerian-path-undirected-graph/](https://www.geeksforgeeks.org/eulerian-path-undirected-graph/)

给定一个无向图的邻接矩阵表示。 查找图表中是否有[欧拉路径](https://www.geeksforgeeks.org/mathematics-euler-hamiltonian-paths/)。 如果没有路径，请打印“无解决方案”。 如果有任何路径，请打印路径。

**范例**：

```
Input : [[0, 1, 0, 0, 1],
         [1, 0, 1, 1, 0],
         [0, 1, 0, 1, 0],
         [0, 1, 1, 0, 0],
         [1, 0, 0, 0, 0]]

Output : 5 -> 1 -> 2 -> 4 -> 3 -> 2

Input : [[0, 1, 0, 1, 1],
         [1, 0, 1, 0, 1],
         [0, 1, 0, 1, 1],
         [1, 1, 1, 0, 0],
         [1, 0, 1, 0, 0]]
Output : "No Solution"

```

此问题的基本情况是，如果边数为奇数（即奇数度）的顶点数大于 2，则不存在欧拉路径。

如果它有解决方案，并且所有节点的边数均为偶数，则可以从任何节点开始路径。

如果它具有解，并且恰好两个顶点的边数为奇数，则我们必须从这两个顶点之一开始路径。

不会出现一个顶点具有奇数个边的情况，因为总共有偶数个边。

**查找路径的过程**：

1.  首先，取一个空栈和一个空路径。

2.  如果所有顶点的边数均为偶数，则从其中任何一个开始。 如果两个顶点的边数为奇数，则从其中一个开始。 将可变电流设置到此起始顶点。

3.  如果当前顶点具有至少一个相邻节点，则首先发现该节点，然后通过回溯来发现当前节点。 为此，将当前节点添加到堆栈中，移除当前节点和邻居节点之间的边，将当前节点设置为当前节点。

4.  如果当前节点没有任何邻居，则将其添加到路径，然后弹出堆栈将当前设置为弹出顶点。

5.  重复过程 3 和 4，直到堆栈为空并且当前节点没有任何邻居为止。

![](img/5bed0a958460d6915ee75c47f2629d71.png)

在过程路径变量之后，保持欧拉路径。

## C++

```cpp

// Efficient C++ program to
// find out Eulerian path
#include <bits/stdc++.h>
using namespace std;

// Function to find out the path
// It takes the adjacency matrix 
// representation of the graph as input
void findpath(int graph[][5], int n)
{
    vector<int> numofadj;

    // Find out number of edges each vertex has
    for (int i = 0; i < n; i++)
        numofadj.push_back(accumulate(graph[i], 
                                      graph[i] + 5, 0));

    // Find out how many vertex has odd number edges
    int startpoint = 0, numofodd = 0;
    for (int i = n - 1; i >= 0; i--)
    {
        if (numofadj[i] % 2 == 1)
        {
            numofodd++;
            startpoint = i;
        }
    }

    // If number of vertex with odd number of edges
    // is greater than two return "No Solution".
    if (numofodd > 2) 
    {
        cout << "No Solution" << endl;
        return;
    }

    // If there is a path find the path
    // Initialize empty stack and path
    // take the starting current as discussed
    stack<int> stack;
    vector<int> path;
    int cur = startpoint;

    // Loop will run until there is element in the stack
    // or current edge has some neighbour.
    while (!stack.empty() or 
            accumulate(graph[cur], 
                       graph[cur] + 5, 0) != 0)
    {
        // If current node has not any neighbour
        // add it to path and pop stack
        // set new current to the popped element
        if (accumulate(graph[cur],
                       graph[cur] + 5, 0) == 0)
        {
            path.push_back(cur);
            cur = stack.top();
            stack.pop();
        }

        // If the current vertex has at least one
        // neighbour add the current vertex to stack,
        // remove the edge between them and set the
        // current to its neighbour.
        else
        {
            for (int i = 0; i < n; i++)
            {
                if (graph[cur][i] == 1) 
                {
                    stack.push(cur);
                    graph[cur][i] = 0;
                    graph[i][cur] = 0;
                    cur = i;
                    break;
                }
            }
        }
    }

    // print the path
    for (auto ele : path) cout << ele << " -> ";
    cout << cur << endl;
}

// Driver Code
int main() 
{
    // Test case 1
    int graph1[][5] = {{0, 1, 0, 0, 1},
                       {1, 0, 1, 1, 0},
                       {0, 1, 0, 1, 0},
                       {0, 1, 1, 0, 0},
                       {1, 0, 0, 0, 0}};
    int n = sizeof(graph1) / sizeof(graph1[0]);
    findpath(graph1, n);

    // Test case 2
    int graph2[][5] = {{0, 1, 0, 1, 1},
                       {1, 0, 1, 0, 1},
                       {0, 1, 0, 1, 1},
                       {1, 1, 1, 0, 0},
                       {1, 0, 1, 0, 0}};
    n = sizeof(graph1) / sizeof(graph1[0]);
    findpath(graph2, n);

    // Test case 3
    int graph3[][5] = {{0, 1, 0, 0, 1},
                       {1, 0, 1, 1, 1},
                       {0, 1, 0, 1, 0},
                       {0, 1, 1, 0, 1},
                       {1, 1, 0, 1, 0}};
    n = sizeof(graph1) / sizeof(graph1[0]);
    findpath(graph3, n);
}

// This code is contributed by
// sanjeev2552

```

## Java

```java

// Efficient Java program to 
// find out Eulerian path 
import java.util.*;

class GFG 
{

    // Function to find out the path
    // It takes the adjacency matrix
    // representation of the graph as input
    static void findpath(int[][] graph, int n)
    {
        Vector<Integer> numofadj = new Vector<>();

        // Find out number of edges each vertex has
        for (int i = 0; i < n; i++)
            numofadj.add(accumulate(graph[i], 0));

        // Find out how many vertex has odd number edges
        int startPoint = 0, numofodd = 0;
        for (int i = n - 1; i >= 0; i--)
        {
            if (numofadj.elementAt(i) % 2 == 1) 
            {
                numofodd++;
                startPoint = i;
            }
        }

        // If number of vertex with odd number of edges
        // is greater than two return "No Solution".
        if (numofodd > 2)
        {
            System.out.println("No Solution");
            return;
        }

        // If there is a path find the path
        // Initialize empty stack and path
        // take the starting current as discussed
        Stack<Integer> stack = new Stack<>();
        Vector<Integer> path = new Vector<>();
        int cur = startPoint;

        // Loop will run until there is element in the stack
        // or current edge has some neighbour.
        while (!stack.isEmpty() || accumulate(graph[cur], 0) != 0)
        {

            // If current node has not any neighbour
            // add it to path and pop stack
            // set new current to the popped element
            if (accumulate(graph[cur], 0) == 0)
            {
                path.add(cur);
                cur = stack.pop();

                // If the current vertex has at least one
                // neighbour add the current vertex to stack,
                // remove the edge between them and set the
                // current to its neighbour.
            } 
            else
            {
                for (int i = 0; i < n; i++)
                {
                    if (graph[cur][i] == 1) 
                    {
                        stack.add(cur);
                        graph[cur][i] = 0;
                        graph[i][cur] = 0;
                        cur = i;
                        break;
                    }
                }
            }
        }

        // print the path
        for (int ele : path)
            System.out.print(ele + " -> ");
        System.out.println(cur);
    }

    static int accumulate(int[] arr, int sum)
    {
        for (int i : arr)
            sum += i;
        return sum;
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Test case 1
        int[][] graph1 = { { 0, 1, 0, 0, 1 },
                        { 1, 0, 1, 1, 0 },
                        { 0, 1, 0, 1, 0 },
                        { 0, 1, 1, 0, 0 },
                        { 1, 0, 0, 0, 0 } };
        int n = graph1.length;
        findpath(graph1, n);

        // Test case 2
        int[][] graph2 = { { 0, 1, 0, 1, 1 },
                        { 1, 0, 1, 0, 1 },
                        { 0, 1, 0, 1, 1 },
                        { 1, 1, 1, 0, 0 },
                        { 1, 0, 1, 0, 0 } };
        n = graph2.length;
        findpath(graph2, n);

        // Test case 3
        int[][] graph3 = { { 0, 1, 0, 0, 1 },
                        { 1, 0, 1, 1, 1 },
                        { 0, 1, 0, 1, 0 },
                        { 0, 1, 1, 0, 1 },
                        { 1, 1, 0, 1, 0 } };
        n = graph3.length;
        findpath(graph3, n);
    }
}

// This code is contributed by
// sanjeev2552

```

## C#

```cs

// Efficient C# program to 
// find out Eulerian path 
using System;
using System.Collections.Generic;
class GFG{

// Function to find out the path
// It takes the adjacency matrix
// representation of the graph 
// as input
static void findpath(int[,] graph, 
                     int n)
{
  List<int> numofadj = 
            new List<int>();

  // Find out number of edges 
  // each vertex has
  for (int i = 0; i < n; i++)
    numofadj.Add(accumulate(graph, 
                            i, 0));

  // Find out how many vertex has 
  // odd number edges
  int startPoint = 0, numofodd = 0;
  for (int i = n - 1; i >= 0; i--)
  {
    if (numofadj[i] % 2 == 1) 
    {
      numofodd++;
      startPoint = i;
    }
  }

  // If number of vertex with odd 
  // number of edges is greater than 
  // two return "No Solution".
  if (numofodd > 2)
  {
    Console.WriteLine("No Solution");
    return;
  }

  // If there is a path find the path
  // Initialize empty stack and path
  // take the starting current as 
  // discussed
  Stack<int> stack = new Stack<int>();
  List<int> path = new List<int>();
  int cur = startPoint;

  // Loop will run until there is element 
  // in the stack or current edge has some 
  // neighbour.
  while (stack.Count != 0 || 
         accumulate(graph, cur, 0) != 0)
  {

    // If current node has not any 
    // neighbour add it to path and 
    // pop stack set new current to 
    // the popped element
    if (accumulate(graph,cur, 0) == 0)
    {
      path.Add(cur);
      cur = stack.Pop();

      // If the current vertex has at 
      // least one neighbour add the 
      // current vertex to stack, remove 
      // the edge between them and set the
      // current to its neighbour.
    } 
    else
    {
      for (int i = 0; i < n; i++)
      {
        if (graph[cur, i] == 1) 
        {
          stack.Push(cur);
          graph[cur, i] = 0;
          graph[i, cur] = 0;
          cur = i;
          break;
        }
      }
    }
  }

  // print the path
  foreach (int ele in path)
    Console.Write(ele + " -> ");
  Console.WriteLine(cur);
}

static int accumulate(int[,] matrix, 
                      int row, int sum)
{    
  int []arr = GetRow(matrix, 
                     row);

 foreach (int i in arr)
   sum += i;
 return sum;
}

public static int[] GetRow(int[,] matrix, 
                           int row)
{
  var rowLength = matrix.GetLength(1);
  var rowVector = new int[rowLength];

  for (var i = 0; i < rowLength; i++)
    rowVector[i] = matrix[row, i];

  return rowVector;
}

// Driver Code
public static void Main(String[] args)
{
  // Test case 1
  int[,] graph1 = {{0, 1, 0, 0, 1},
                   {1, 0, 1, 1, 0},
                   {0, 1, 0, 1, 0},
                   {0, 1, 1, 0, 0},
                   {1, 0, 0, 0, 0}};
  int n = graph1.GetLength(0);
  findpath(graph1, n);

  // Test case 2
  int[,] graph2 = {{0, 1, 0, 1, 1},
                   {1, 0, 1, 0, 1},
                   {0, 1, 0, 1, 1},
                   {1, 1, 1, 0, 0},
                   {1, 0, 1, 0, 0}};
  n = graph2.GetLength(0);
  findpath(graph2, n);

  // Test case 3
  int[,] graph3 = {{0, 1, 0, 0, 1},
                   {1, 0, 1, 1, 1},
                   {0, 1, 0, 1, 0},
                   {0, 1, 1, 0, 1},
                   {1, 1, 0, 1, 0}};
  n = graph3.GetLength(0);
  findpath(graph3, n);
}
}

// This code is contributed by Rajput-Ji

```

**输出**：

```
4 -> 0 -> 1 -> 3 -> 2 -> 1
No Solution
4 -> 3 -> 2 -> 1 -> 4 -> 0 -> 1 -> 3

```

**时间复杂度**：

该算法的运行时复杂度为 O（E）。 该算法也可用于查找欧拉回路。 如果路径的第一个和最后一个顶点相同，则它将是欧拉回路。



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。