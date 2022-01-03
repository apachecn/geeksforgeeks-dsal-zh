# 查找无向图是否包含给定大小的独立集

> 原文： [https://www.geeksforgeeks.org/find-if-an-undirected-graph-contains-an-independent-set-of-a-given-size/](https://www.geeksforgeeks.org/find-if-an-undirected-graph-contains-an-independent-set-of-a-given-size/)

给定一个无向图，请检查它是否包含大小为`k`的独立集合。 如果存在独立的尺寸`k`集，则打印“是”。 否则打印“否”。

**独立集**：图形中的独立集是一组不彼此直接连接的顶点。

**示例 1**：

```
Input : K = 4,
        graph = [[1, 1, 0, 0, 0],
                 [1, 1, 1, 1, 1],
                 [0, 1, 1, 0, 0],
                 [0, 1, 0, 1, 0],
                 [0, 1, 0, 0, 1]]
Output : Yes 

```

![](img/9abac79a9d59b9ef5cd442a6df44b7f9.png)

上图包含一组独立的大小 4（顶点 1、2、3、4 彼此不直接连接）。 因此，输出为“是”。

**示例 2**：

```
Input : K = 4,
        graph = [[1, 1, 0, 0, 0],
                 [1, 1, 1, 1, 1],
                 [0, 1, 1, 0, 0],
                 [0, 1, 0, 1, 1],
                 [0, 1, 0, 1, 1]]
Output : No

```

![](img/6825fd4a8fff962198d653b847a4f4cb.png)

上面的图形没有包含独立的大小 4 集。因此，输出为“否”。

**方法**：

*   用布尔值*假*值初始化变量 **sol** 。

*   从给定图中找出大小为`K`的所有可能的顶点集。

*   如果找到独立的大小`k`集，则将 **sol** 的值更改为 True 并返回。

*   否则，继续检查其他可能的设置。

*   最后，如果 **sol** 为 True，则打印“是”，否则打印“否”。

下面是上述方法的实现：

## C++ 14

```

// C++ code to check if a given graph
// contains an independent set of size k
#include <bits/stdc++.h>
using namespace std;

// Function prototype
bool check(int[][5], vector<int> &, int);

// Function to construct a set of given size k
bool func(int graph[][5], vector<int> &arr, 
          int k, int index, bool sol[])
{
    // Check if the selected set is independent or not.
    // Change the value of sol to True and return
    // if it is independent
    if (k == 0)
    {
        if (check(graph, arr, arr.size()))
        {
            sol[0] = true;
            return true;
        }
    }
    else
    {
        // Set of size k can be formed even if we don't
        // include the vertex at current index.
        if (index >= k)
        {
            vector<int> newvec(arr.begin(), arr.end());
            newvec.push_back(index);
            return (func(graph, newvec, k - 1, 
                                index - 1, sol) or
                    func(graph, arr, k, index - 1, sol));
        }

        // Set of size k cannot be formed if we don't
        // include the vertex at current index.
        else
        {
            arr.push_back(index);
            return func(graph, arr, k - 1, 
                          index - 1, sol);
        }
    }
}

// Function to check if the given set is
// independent or not
// arr --> set of size k (contains the
// index of included vertex)
bool check(int graph[][5], vector<int> &arr, int n)
{
    // Check if each vertex is connected to any other
    // vertex in the set or not
    for (int i = 0; i < n; i++)
        for (int j = i + 1; j < n; j++)
            if (graph[arr[i]][arr[j]] == 1)
                return false;
    return true;
}

// Driver Code
int main()
{
    int graph[][5] = {{1, 1, 0, 0, 0},
                      {1, 1, 1, 1, 1},
                      {0, 1, 1, 0, 0},
                      {0, 1, 0, 1, 0},
                      {0, 1, 0, 0, 1}};
    int k = 4;
    vector<int> arr; // Empty set
    bool sol[] = {false};
    int n = sizeof(graph) / 
            sizeof(graph[0]);
    func(graph, arr, k, n - 1, sol);

    if (sol[0])
        cout << "Yes" << endl;
    else
        cout << "No" << endl;
    return 0;
}

// This code is contributed by
// sanjeev2552

```

## Java

```java

// Java code to check if a 
// given graph contains an 
// independent set of size k
import java.util.*;
class GFG{

static  Vector<Integer> arr = 
        new Vector<>();

// Function to cona set of 
// given size k
static boolean func(int graph[][], 
                    int k, int index, 
                    boolean sol[])
{
  // Check if the selected set is 
  // independent or not. Change the 
  // value of sol to True and return
  // if it is independent
  if (k == 0)
  {
    if (check(graph, 
              arr.size()))
    {
      sol[0] = true;
      return true;
    }
  }
  else
  {
    // Set of size k can be
    // formed even if we don't 
    // include the vertex at 
    // current index.
    if (index >= k)
    {
      Vector<Integer> newvec = 
             new Vector<>();
      newvec.add(index);
      return (func(graph, k - 1, 
                   index - 1, sol) ||
              func(graph, k, 
                   index - 1, sol));
    }

    // Set of size k cannot be 
    // formed if we don't include 
    // the vertex at current index.
    else
    {
      arr.add(index);
      return func(graph, k - 1, 
                  index - 1, sol);
    }
  }
  return true;
}

// Function to check if the 
// given set is independent 
// or not arr -. set of size 
// k (contains the index of 
// included vertex)
static boolean check(int graph[][], 
                     int n)
{
  // Check if each vertex is 
  // connected to any other
  // vertex in the set or not
  for (int i = 0; i < n; i++)
    for (int j = i + 1; j < n; j++)
      if (graph[arr.get(i)][arr.get(j)] == 1)
        return false;
  return true;
}

// Driver Code
public static void main(String[] args)
{
  int graph[][] = {{1, 1, 0, 0, 0},
                   {1, 1, 1, 1, 1},
                   {0, 1, 1, 0, 0},
                   {0, 1, 0, 1, 0},
                   {0, 1, 0, 0, 1}};
  int k = 4;
  boolean []sol = new boolean[1];
  int n = graph.length;
  func(graph, k, n - 1, sol);

  if (sol[0])
    System.out.print("Yes" + "\n");
  else
    System.out.print("No" + "\n");
}
}

// This code is contributed by Amit Katiyar

```

## Python

```py

# Python3 code to check if a given graph
# contains an independent set of size k

# Function to construct a set of given size k
def func(graph, arr, k, index, sol):

    # Check if the selected set is independent or not. 
    # Change the value of sol to True and return 
    # if it is independent
    if k == 0:
        if check(graph, arr) == True:
            sol[0] = True
            return

    else:
        # Set of size k can be formed even if we don't 
        # include the vertex at current index.
        if index >= k:
            return (func(graph, arr[:] + [index], k-1, index-1, sol) or
                    func(graph, arr[:], k, index-1, sol))

        # Set of size k cannot be formed if we don't
        # include the vertex at current index.
        else:
            return func(graph, arr[:] + [index], k-1, index-1, sol)

# Function to check if the given set is 
# independent or not
# arr --> set of size k (contains the
# index of included vertex)
def check(graph, arr):

    # Check if each vertex is connected to any other
    # vertex in the set or not
    for i in range(len(arr)):
        for j in range(i + 1, len(arr)):

            if graph[arr[i]][arr[j]] == 1:
                return False

    return True

# Driver Code    
graph = [[1, 1, 0, 0, 0],
         [1, 1, 1, 1, 1],
         [0, 1, 1, 0, 0],
         [0, 1, 0, 1, 0],
         [0, 1, 0, 0, 1]]

k = 4
arr = []     # Empty set 
sol = [False]

func(graph, arr[:], k, len(graph)-1, sol)

if sol[0] == True:
    print("Yes")
else:
    print("No")

```

## C#

```cs

// C# code to check if a 
// given graph contains an 
// independent set of size k
using System;
using System.Collections.Generic;

class GFG{

static List<int> arr = new List<int>();

// Function to cona set of 
// given size k
static bool func(int [,]graph, 
                 int k, int index, 
                 bool []sol)
{

  // Check if the selected set is 
  // independent or not. Change the 
  // value of sol to True and return
  // if it is independent
  if (k == 0)
  {
    if (check(graph, 
              arr.Count))
    {
      sol[0] = true;
      return true;
    }
  }
  else
  {

    // Set of size k can be
    // formed even if we don't 
    // include the vertex at 
    // current index.
    if (index >= k)
    {
      List<int> newvec = new List<int>();
      newvec.Add(index);

      return (func(graph, k - 1, 
                       index - 1, sol) ||
              func(graph, k, 
                   index - 1, sol));
    }

    // Set of size k cannot be 
    // formed if we don't include 
    // the vertex at current index.
    else
    {
      arr.Add(index);

      return func(graph, k - 1, 
                     index - 1, sol);
    }
  }
  return true;
}

// Function to check if the 
// given set is independent 
// or not arr -. set of size 
// k (contains the index of 
// included vertex)
static bool check(int [,]graph, int n)
{

  // Check if each vertex is 
  // connected to any other
  // vertex in the set or not
  for(int i = 0; i < n; i++)
    for(int j = i + 1; j < n; j++)
      if (graph[arr[i],arr[j]] == 1)
        return false;

  return true;
}

// Driver Code
public static void Main(String[] args)
{
  int [,]graph = { { 1, 1, 0, 0, 0 },
                   { 1, 1, 1, 1, 1 },
                   { 0, 1, 1, 0, 0 },
                   { 0, 1, 0, 1, 0 },
                   { 0, 1, 0, 0, 1 } };
  int k = 4;
  bool []sol = new bool[1];
  int n = graph.GetLength(0);

  func(graph, k, n - 1, sol);

  if (sol[0])
    Console.Write("Yes" + "\n");
  else
    Console.Write("No" + "\n");
}
}

// This code is contributed by Amit Katiyar

```

**Output:** 

```
Yes

```

**时间复杂度**：

![O({V\choose k} * k^2)     ](img/f6c47eebf05a940ea631bf9327f85a65.png "Rendered by QuickLaTeX.com")

其中`V`是图形中的顶点数，`k`是给定的集合大小。



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。