# 数组中循环元素的个数，我们可以根据数值

进行跳转

> 原文:[https://www . geeksforgeeks . org/数组中循环元素的数量我们可以根据值跳转/](https://www.geeksforgeeks.org/number-of-cyclic-elements-in-an-array-where-we-can-jump-according-to-value/)

给定 n 个整数的数组 arr[]。对于每个值 arr[i]，考虑到循环中的数组元素，我们可以顺时针移动到 arr[I]+1
。我们需要计算数组中的循环元素。如果从一个元素开始，移动到 arr[i] + 1，则该元素是循环的。

示例:

```
Input : arr[] = {1, 1, 1, 1}
Output : 4
All 4 elements are cyclic elements.
1 -> 3 -> 1
2 -> 4 -> 2
3 -> 1 -> 3
4 -> 2 -> 4

Input : arr[] = {3, 0, 0, 0}
Output : 1
There is one cyclic point 1,
1 -> 1
The path covered starting from 2 is
2 -> 3 -> 4 -> 1 -> 1.

The path covered starting from 3 is
2 -> 3 -> 4 -> 1 -> 1.

The path covered starting from 4 is
4 -> 1 -> 1
```

一**简单的解决方法**就是逐个检查所有元素。我们遵循从每个元素 arr[i]开始的简单路径，我们转到 arr[i] + 1。如果我们回到 arr[i]之外的被访问元素，我们不计算 arr[i]。该解决方案的时间复杂度为 0(n<sup>2</sup>

一个**高效的解决方案**基于以下步骤。
1)使用数组索引作为节点创建有向图。我们添加一条从 I 到节点的边(arr[i] + 1)%n.
2)一旦创建了一个图，我们就使用 Kosaraju 的算法
找到所有[强连接的组件 3)我们最终返回单个强连接组件中节点计数的总和。](https://www.geeksforgeeks.org/strongly-connected-components/)

## C++

```
// C++ program to count cyclic points
// in an array using Kosaraju's Algorithm
#include <bits/stdc++.h>
using namespace std;

// Most of the code is taken from below link
// https://www.geeksforgeeks.org/strongly-connected-components/
class Graph {
    int V;
    list<int>* adj;
    void fillOrder(int v, bool visited[],
                      stack<int>& Stack);
    int DFSUtil(int v, bool visited[]);

public:
    Graph(int V);
    void addEdge(int v, int w);
    int countSCCNodes();
    Graph getTranspose();
};

Graph::Graph(int V)
{
    this->V = V;
    adj = new list<int>[V];
}

// Counts number of nodes reachable
// from v
int Graph::DFSUtil(int v, bool visited[])
{
    visited[v] = true;
    int ans = 1;
    list<int>::iterator i;
    for (i = adj[v].begin(); i != adj[v].end(); ++i)
        if (!visited[*i])
           ans += DFSUtil(*i, visited);
    return ans;
}

Graph Graph::getTranspose()
{
    Graph g(V);
    for (int v = 0; v < V; v++) {
        list<int>::iterator i;
        for (i = adj[v].begin(); i != adj[v].end(); ++i)
            g.adj[*i].push_back(v);
    }
    return g;
}

void Graph::addEdge(int v, int w)
{
    adj[v].push_back(w);
}

void Graph::fillOrder(int v, bool visited[],
                           stack<int>& Stack)
{
    visited[v] = true;
    list<int>::iterator i;
    for (i = adj[v].begin(); i != adj[v].end(); ++i)
        if (!visited[*i])
            fillOrder(*i, visited, Stack);
    Stack.push(v);
}

// This function mainly returns total count of
// nodes in individual SCCs using Kosaraju's
// algorithm.
int Graph::countSCCNodes()
{
    int res = 0;
    stack<int> Stack;
    bool* visited = new bool[V];
    for (int i = 0; i < V; i++)
        visited[i] = false;
    for (int i = 0; i < V; i++)
        if (visited[i] == false)
            fillOrder(i, visited, Stack);
    Graph gr = getTranspose();
    for (int i = 0; i < V; i++)
        visited[i] = false;
    while (Stack.empty() == false) {
        int v = Stack.top();
        Stack.pop();
        if (visited[v] == false) {
            int ans = gr.DFSUtil(v, visited);
            if (ans > 1)
                res += ans;
        }
    }
    return res;
}

// Returns count of cyclic elements in arr[]
int countCyclic(int arr[], int n)
{
    int  res = 0;

    // Create a graph of array elements
    Graph g(n + 1);

    for (int i = 1; i <= n; i++) {
        int x = arr[i-1];

        // If i + arr[i-1] jumps beyond last
        // element, we take mod considering
        // cyclic array
        int v = (x + i) % n + 1;

        // If there is a self loop, we
        // increment count of cyclic points.
        if (i == v)
            res++;

        g.addEdge(i, v);
    }

    // Add nodes of strongly connected components
    // of size more than 1.
    res += g.countSCCNodes();

    return res;
}

// Driver code
int main()
{
    int arr[] = {1, 1, 1, 1};
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << countCyclic(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Python3 program to count cyclic points
// in an array using Kosaraju's Algorithm

// Counts number of nodes reachable
// from v
import java.io.*;
import java.util.*;
class GFG
{
  static boolean[] visited = new boolean[100];
  static Stack<Integer> stack = new Stack<Integer>();
  static ArrayList<ArrayList<Integer>> adj =
    new ArrayList<ArrayList<Integer>>();

  static int DFSUtil(int v)
  {
    visited[v] = true;
    int ans = 1;
    for(int i: adj.get(v))
    {
      if(!visited[i])
      {
        ans += DFSUtil(i);
      }
    }
    return ans;
  }
  static void getTranspose()
  {

    for(int v = 0; v < 5; v++)
    {
      for(int i : adj.get(v))
      {
        adj.get(i).add(v);
      }
    }
  }
  static void addEdge(int v, int w)
  {
    adj.get(v).add(w);
  }
  static void fillOrder(int v)
  {
    visited[v] = true;
    for(int i: adj.get(v))
    {
      if(!visited[i])
      {
        fillOrder(i);
      }
    }
    stack.add(v);
  }

  // This function mainly returns total count of
  // nodes in individual SCCs using Kosaraju's
  // algorithm.
  static int countSCCNodes()
  {
    int res = 0;

    // stack<int> Stack;
    // bool* visited = new bool[V];
    for(int i = 0; i < 5; i++)
    {
      if(visited[i] == false)
      {
        fillOrder(i);
      }
    }
    getTranspose();
    for(int i = 0; i < 5; i++)
    {
      visited[i] = false;
    }
    while(stack.size() > 0)
    {
      int v = stack.get(stack.size() - 1);
      stack.remove(stack.size() - 1);
      if (visited[v] == false)
      {
        int ans = DFSUtil(v);
        if (ans > 1)
        {
          res += ans;
        }
      }
    }
    return res;
  }

  // Returns count of cyclic elements in arr[]
  static int countCyclic(int[] arr, int n)
  {
    int res = 0;

    // Create a graph of array elements
    for(int i = 1; i < n + 1; i++)
    {
      int x = arr[i - 1];

      // If i + arr[i-1] jumps beyond last
      // element, we take mod considering
      // cyclic array
      int v = (x + i) % n + 1;

      // If there is a self loop, we
      // increment count of cyclic points.
      if (i == v)
        res++;
      addEdge(i, v);
    }

    // Add nodes of strongly connected components
    // of size more than 1.
    res += countSCCNodes();
    return res;
  }

  // Driver code
  public static void main (String[] args)
  {
    int arr[] = {1, 1, 1, 1};
    int n = arr.length;
    for(int i = 0; i < 100; i++)
    {
      adj.add(new ArrayList<Integer>());

    }
    System.out.println(countCyclic(arr, n));
  }
}

// This code is contributed by avanitrachhadiya2155
```

## 蟒蛇 3

```
# Python3 program to count cyclic points
# in an array using Kosaraju's Algorithm

# Counts number of nodes reachable
# from v
def DFSUtil(v):

    global visited, adj

    visited[v] = True
    ans = 1

    for i in adj[v]:
        if (not visited[i]):
           ans += DFSUtil(i)

    return ans

def getTranspose():

    global visited, adj

    for v in range(5):
        for i in adj[v]:
            adj[i].append(v)

def addEdge(v, w):

    global visited, adj
    adj[v].append(w)

def fillOrder(v):

    global Stack, adj, visited
    visited[v] = True

    for i in adj[v]:
        if (not visited[i]):
            fillOrder(i)

    Stack.append(v)

# This function mainly returns total count of
# nodes in individual SCCs using Kosaraju's
# algorithm.
def countSCCNodes():

    global adj, visited, S
    res = 0

    #stack<int> Stack;
    #bool* visited = new bool[V];
    for i in range(5):
        if (visited[i] == False):
            fillOrder(i)

    getTranspose()
    for i in range(5):
        visited[i] = False

    while (len(Stack) > 0):
        v = Stack[-1]
        del Stack[-1]

        if (visited[v] == False):
            ans = DFSUtil(v)
            if (ans > 1):
                res += ans

    return res

# Returns count of cyclic elements in arr[]
def countCyclic(arr, n):

    global adj
    res = 0

    # Create a graph of array elements
    for i in range(1, n + 1):
        x = arr[i - 1]

        # If i + arr[i-1] jumps beyond last
        # element, we take mod considering
        # cyclic array
        v = (x + i) % n + 1

        # If there is a self loop, we
        # increment count of cyclic points.
        if (i == v):
            res += 1

        addEdge(i, v)

    # Add nodes of strongly connected components
    # of size more than 1.
    res += countSCCNodes()

    return res

# Driver code
if __name__ == '__main__':

    adj = [[] for i in range(100)]
    visited = [False for i in range(100)]
    arr = [ 1, 1, 1, 1 ]
    Stack = []
    n = len(arr)

    print(countCyclic(arr, n))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to count cyclic points
// in an array using Kosaraju's Algorithm

// Counts number of nodes reachable
// from v
using System;
using System.Collections.Generic;
public class GFG
{

  static bool[] visited = new bool[100];
  static List<int> stack = new List<int>();
  static List<List<int>> adj = new List<List<int>>();
  static int DFSUtil(int v)
  {
    visited[v] = true;
    int ans = 1;
    foreach(int i in adj[v])
    {
      if(!visited[i])
      {
        ans += DFSUtil(i);
      }
    }
    return ans;
  }
  static void getTranspose()
  {
    for(int v = 0; v < 5; v++)
    {
      foreach(int i in adj[v])
      {
        adj[i].Add(v);
      }
    }
  }
  static void addEdge(int v, int w)
  {
    adj[v].Add(w);
  }
  static void fillOrder(int v)
  {
    visited[v] = true;
    foreach(int i in adj[v])
    {
      if(!visited[i])
      {
        fillOrder(i);
      }
    }
    stack.Add(v);
  }

  // This function mainly returns total count of
  // nodes in individual SCCs using Kosaraju's
  // algorithm.
  static int countSCCNodes()
  {
    int res = 0;

    // stack<int> Stack;
    // bool* visited = new bool[V];
    for(int i = 0; i < 5; i++)
    {
      if(visited[i] == false)
      {
        fillOrder(i);
      }
    }
    getTranspose();
    for(int i = 0; i < 5; i++)
    {
      visited[i] = false;
    }
    while(stack.Count > 0)
    {
      int v=stack[stack.Count - 1];
      stack.Remove(stack.Count - 1);
      if (visited[v] == false)
      {
        int ans = DFSUtil(v);
        if (ans > 1)
        {
          res += ans;
        }
      }
    }
    return res;
  }

  // Returns count of cyclic elements in arr[]
  static int countCyclic(int[] arr, int n)
  {
    int res = 0;

    // Create a graph of array elements
    for(int i = 1; i < n + 1; i++)
    {
      int x = arr[i - 1];

      // If i + arr[i-1] jumps beyond last
      // element, we take mod considering
      //cyclic array
      int v = (x + i) % n + 1;   

      // If there is a self loop, we
      // increment count of cyclic points.
      if (i == v)
        res++;
      addEdge(i, v);
    }

    // Add nodes of strongly connected components
    // of size more than 1.
    res += countSCCNodes();
    return res;
  }

  // Driver code
  static public void Main ()
  {
    int[] arr = {1, 1, 1, 1};
    int n = arr.Length;
    for(int i = 0; i < 100; i++)
    {
      adj.Add(new List<int>());
    }
    Console.WriteLine(countCyclic(arr, n));
  }
}

// This code is contributed by rag2127
```

## java 描述语言

```
<script>
// Javascript program to count cyclic points
// in an array using Kosaraju's Algorithm

// Counts number of nodes reachable
// from v

    let visited = new Array(100);
    for(let i=0;i<100;i++)
    {
        visited[i]=false;
    }
    let stack = [];
    let adj=[];

function DFSUtil(v)
{
    visited[v] = true;
    let ans = 1;
    for(let i=0;i<adj[v].length;i++)
    {
      if(!visited[adj[v][i]])
      {
        ans += DFSUtil(adj[v][i]);
      }
    }
    return ans;
}

function getTranspose()
{
    for(let v = 0; v < 5; v++)
    {
      for(let i=0;i<adj[v].length;i++)
      {
        adj[adj[v][i]].push(v);
      }
    }
}

function addEdge(v,w)
{
    adj[v].push(w);
}

function fillOrder(v)
{
    visited[v] = true;
    for(let i=0;i<adj[v].length;i++)
    {
      if(!visited[adj[v][i]])
      {
        fillOrder(adj[v][i]);
      }
    }
    stack.push(v);
}

// This function mainly returns total count of
  // nodes in individual SCCs using Kosaraju's
  // algorithm.
function countSCCNodes()
{
let res = 0;

    // stack<int> Stack;
    // bool* visited = new bool[V];
    for(let i = 0; i < 5; i++)
    {
      if(visited[i] == false)
      {
        fillOrder(i);
      }
    }
    getTranspose();
    for(let i = 0; i < 5; i++)
    {
      visited[i] = false;
    }
    while(stack.length > 0)
    {
      let v = stack[stack.length - 1];
      stack.pop();
      if (visited[v] == false)
      {
        let ans = DFSUtil(v);
        if (ans > 1)
        {
          res += ans;
        }
      }
    }
    return res;
}

// Returns count of cyclic elements in arr[]
function countCyclic(arr,n)
{
    let res = 0;

    // Create a graph of array elements
    for(let i = 1; i < n + 1; i++)
    {
      let x = arr[i - 1];

      // If i + arr[i-1] jumps beyond last
      // element, we take mod considering
      // cyclic array
      let v = (x + i) % n + 1;

      // If there is a self loop, we
      // increment count of cyclic points.
      if (i == v)
        res++;
      addEdge(i, v);
    }

    // Add nodes of strongly connected components
    // of size more than 1.
    res += countSCCNodes();
    return res;
}

// Driver code
let arr=[1, 1, 1, 1];
let n = arr.length;
for(let i = 0; i < 100; i++)
{
    adj.push([]);

}
document.write(countCyclic(arr, n));

// This code is contributed by unknown2108
</script>
```

**输出:**

```
4
```

时间复杂度:O(n)
辅助空间:O(n)注意只有 O(n)条边。

本文由 [**莫哈克·阿格沃尔**](https://auth.geeksforgeeks.org/profile.php?user=agrawalmohak99&list=practice) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。