# 找到与 X 的和具有最小设置位的节点

> 原文:[https://www . geeksforgeeks . org/find-the-node-with-x-sum-with-x-with-minimum-set-bits/](https://www.geeksforgeeks.org/find-the-node-whose-sum-with-x-has-minimum-set-bits/)

给定一棵树，所有节点的权重和一个整数 **x** ，任务是找到一个节点 **i** ，使得**权重[i] + x** 给出最小的设置位，如果两个或多个节点在加上 **x** 时具有相同的设置位计数，则找到具有最小值的节点。

**示例:**

> **输入:**
> 
> ![](img/107072b5f698ad7b63297c5c333d9375.png)
> 
> x = 15
> **输出:** 1
> 节点 1:设置位(5 + 15) = 2
> 节点 2:设置位(10 + 15) = 3
> 节点 3:设置位(11 + 15) = 3
> 节点 4:设置位(8 + 15) = 4
> 节点 5:设置位(6 + 15) = 3

**方法:**在树上执行 [dfs](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) ，并跟踪其与**的和 x** 具有最小设置位的节点。如果两个或两个以上的节点具有相同数量的设置位，则选择具有最小数量的节点。

下面是上述方法的实现:

## C++

```
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

## Java 语言(一种计算机语言，尤用于创建网站)

```
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

## 蟒蛇 3

```
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

```
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

## java 描述语言

```
<script>

// Javascript implementation of the approach
let minimum = Number.MAX_VALUE;
let x;
let ans = Number.MAX_VALUE;

let graph = new Array(100);
let weight = new Array(100);
for(let i = 0; i < 100; i++)
{
    graph[i] = [];
    weight[i] = 0;
}

// Function to perform dfs to find
// the minimum set bits value
function dfs(node, parent)
{

    // If current set bits value is smaller than
    // the current minimum
    let a = (weight[node] + x).toString(2).split('').filter(
            y => y == '1').length;
    if (minimum > a)
    {
        minimum = a;
        ans = node;
    }

    // If count is equal to the minimum
    // then choose the node with minimum value
    else if (minimum == a)
        ans = Math.min(ans, node);

    for(let to = 0; to < graph[node].length; to++)
    {
        if (graph[node][to] == parent)
            continue

        dfs(graph[node][to], node);
    }
}

// Driver code
x = 15;

// Weights of the node
weight[1] = 5;
weight[2] = 10;
weight[3] = 11;
weight[4] = 8;
weight[5] = 6;

// Edges of the tree
graph[1].push(2);
graph[2].push(3);
graph[2].push(4);
graph[1].push(5);

dfs(1, 1);

document.write(ans);

// This code is contributed by Dharanendra L V.

</script>
```

**Output:** 

```
1
```

**复杂度分析:**

*   **时间复杂度:** O(N)。
    在 dfs 中，树的每个节点都被处理一次，因此如果树中总共有 N 个节点，由于 dfs 而导致的复杂性是 O(N)。此外，为了处理每个节点，使用了 builtin_popcount()函数，该函数的复杂度为 O(c)，其中 c 是常数，由于该复杂度是常数，因此它不会影响总的时间复杂度。因此，时间复杂度为 O(N)。
*   **辅助空间:** O(1)。
    不需要任何额外的空间，所以空间复杂度不变。