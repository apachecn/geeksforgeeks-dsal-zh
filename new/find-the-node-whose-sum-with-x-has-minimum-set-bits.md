# 查找与 X 的总和具有最小设置位的节点

> 原文： [https://www.geeksforgeeks.org/find-the-node-whose-sum-with-x-has-minimum-set-bits/](https://www.geeksforgeeks.org/find-the-node-whose-sum-with-x-has-minimum-set-bits/)

给定一棵树，以及所有节点的权重和整数`x`，任务是找到一个节点`i`，使得 **weight [i] + x** 给出最小的设置位，如果两个或多个节点在添加`x`时具有相同的设置位计数，则找到一个最小值。

**范例**：

> **输入**：
> 
> ![](img/107072b5f698ad7b63297c5c333d9375.png)
> 
> x = 15
> **输出**：1
> 节点 1：setbits（5 + 15）= 2
> 节点 2：setbits（10 + 15）= 3
> 节点 3：setbits （11 + 15）= 3
> 节点 4：setbits（8 + 15）= 4
> 节点 5：setbits（6 + 15）= 3

**方法**：在树上执行 [dfs](http://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) ，并跟踪其与`x`的总和具有最小设置位的节点。 如果两个或更多节点的设置位数相等，则选择数量最少的一个。

以下是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

int minimum = INT_MAX, x, ans = INT_MAX;

vector<int> graph[100];
vector<int> weight(100);

// Function to perform dfs to find
// the minimum set bits value
void dfs(int node, int parent)
{
    // If current set bits value is smaller than
    // the current minimum
    int a = __builtin_popcount(weight[node] + x);
    if (minimum > a) {
        minimum = a;
        ans = node;
    }

    // If count is equal to the minimum
    // then choose the node with minimum value
    else if (minimum == a)
        ans = min(ans, node);

    for (int to : graph[node]) {
        if (to == parent)
            continue;
        dfs(to, node);
    }
}

// Driver code
int main()
{
    x = 15;

    // Weights of the node
    weight[1] = 5;
    weight[2] = 10;
    weight[3] = 11;
    weight[4] = 8;
    weight[5] = 6;

    // Edges of the tree
    graph[1].push_back(2);
    graph[2].push_back(3);
    graph[2].push_back(4);
    graph[1].push_back(5);

    dfs(1, 1);

    cout << ans;

    return 0;
}

```

## Java

```java

// Java implementation of the approach
import java.util.*;
class GFG{

static int minimum = Integer.MAX_VALUE, 
           x, ans = Integer.MAX_VALUE;

static Vector<Integer> []graph = 
              new Vector[100];
static int []weight = new int[100];

// Function to perform dfs 
// to find the minimum set 
// bits value
static void dfs(int node, 
                int parent)
{
  // If current set bits value 
  // is smaller than the current 
  // minimum
  int a = Integer.bitCount(weight[node] + x);
  if (minimum > a) 
  {
    minimum = a;
    ans = node;
  }

  // If count is equal to the 
  // minimum then choose the 
  // node with minimum value
  else if (minimum == a)
    ans = Math.min(ans, node);

  for (int to : graph[node]) 
  {
    if (to == parent)
      continue;
    dfs(to, node);
  }
}

// Driver code
public static void main(String[] args)
{
  x = 15;
  for (int i = 0; i < graph.length; i++)
    graph[i] = new Vector<Integer>();

  // Weights of the node
  weight[1] = 5;
  weight[2] = 10;
  weight[3] = 11;
  weight[4] = 8;
  weight[5] = 6;

  // Edges of the tree
  graph[1].add(2);
  graph[2].add(3);
  graph[2].add(4);
  graph[1].add(5);

  dfs(1, 1);

  System.out.print(ans);
}
}

// This code is contributed by gauravrajput1

```

## Python

```py

# Python3 implementation of the approach
from sys import maxsize

minimum, x, ans = maxsize, None, maxsize

graph = [[] for i in range(100)]
weight = [0] * 100

# Function to perform dfs to find
# the minimum set bits value
def dfs(node, parent):
    global x, ans, graph, weight, minimum

    # If current set bits value is greater than
    # the current minimum
    a = bin(weight[node] + x).count('1')

    if minimum > a:
        minimum = a
        ans = node

    # If count is equal to the minimum
    # then choose the node with minimum value
    elif minimum == a:
        ans = min(ans, node)

    for to in graph[node]:
        if to == parent:
            continue
        dfs(to, node)

# Driver Code
if __name__ == "__main__":

    x = 15

    # Weights of the node
    weight[1] = 5
    weight[2] = 10
    weight[3] = 11
    weight[4] = 8
    weight[5] = 6

    # Edges of the tree
    graph[1].append(2)
    graph[2].append(3)
    graph[2].append(4)
    graph[1].append(5)

    dfs(1, 1)

    print(ans)

# This code is contributed by
# sanjeev2552

```

## C#

```cs

// C# implementation of the approach 
using System; 
using System.Collections; 
using System.Collections.Generic; 
using System.Text; 

class GFG{

static int minimum = int.MaxValue, x, 
               ans = int.MaxValue;

static ArrayList[] graph = new ArrayList[100]; 
static int[] weight = new int[100]; 

static int PopCount(int n) 
{ 
    int count = 0;

    while (n > 0)
    { 
        count += n & 1; 
        n >>= 1; 
    } 
    return count; 
} 

// Function to perform dfs to find
// the minimum set bits value
static void dfs(int node, int parent)
{

    // If current set bits value is smaller 
    // than the current minimum
    int a = PopCount(weight[node] + x);
    if (minimum > a) 
    {
        minimum = a;
        ans = node;
    }

    // If count is equal to the minimum
    // then choose the node with minimum value
    else if (minimum == a)
        ans = Math.Min(ans, node);

    foreach(int to in graph[node])
    {
        if (to == parent)
            continue;

        dfs(to, node);
    }
}

// Driver Code
public static void Main(string[] args)
{
    x = 15;

    for(int i = 0; i < 100; i++) 
        graph[i] = new ArrayList();

    // Weights of the node
    weight[1] = 5;
    weight[2] = 10;
    weight[3] = 11;
    weight[4] = 8;
    weight[5] = 6;

    // Edges of the tree
    graph[1].Add(2);
    graph[2].Add(3);
    graph[2].Add(4);
    graph[1].Add(5);

    dfs(1, 1);

    Console.Write(ans); 
}
}

// This code is contributed by rutvik_56

```

**Output:** 

```
1

```

**复杂度分析**：

*   **时间复杂度**：`O(N)`。

    在 dfs 中，树的每个节点都处理一次，因此，如果树中总共有 N 个节点，则由于 dfs 而导致的复杂度为`O(N)`。 另外，为了处理每个节点，使用了 Builtin_popcount（）函数，该函数的复杂度为 O（c），其中 c 为常数，并且由于该常数为常数，因此不会影响整体时间复杂度。 因此，时间复杂度为`O(N)`。

*   **辅助空间**：`O(1)`。

    不需要任何额外的空间，因此空间复杂度是恒定的。



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。