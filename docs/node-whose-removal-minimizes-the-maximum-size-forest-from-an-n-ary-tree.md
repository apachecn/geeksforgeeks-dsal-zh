# 从 N 元树中移除最小化最大森林大小的节点

> 原文:[https://www . geeksforgeeks . org/node-其移除使 n 元树中的最大大小森林最小化/](https://www.geeksforgeeks.org/node-whose-removal-minimizes-the-maximum-size-forest-from-an-n-ary-tree/)

给定一个 [n 元树](https://www.geeksforgeeks.org/generic-treesn-array-trees/) **T** ，任务是找到一个节点，该节点的移除最小化了生成的所有森林([连接组件](https://www.geeksforgeeks.org/strongly-connected-components/))的最大大小。

**示例:**

> **输入:**
> 1
> /| \
> 2 3 4
> /\
> 5 6
> **输出:** 1
> **说明:**
> 有 6 个节点可以移除形成森林:
> 移除(1):最大森林大小为 3
> 移除(2):最大森林大小为 3
> 移除(3):最大森林大小为 5
> 移除(4):最大森林大小为 5
> 
> **输入:**
> 1
> / \
> 2 3
> **输出:** 1
> **说明:**
> 有三个节点可以移除形成森林:
> 移除(1):最大森林大小为 1
> 移除(2):最大森林大小为 1
> 移除(3):最大森林大小为 1
> 因此，移除节点 1 或 2 或 3 会将最大森林大小最小化为 1。

**逼近**:思路是[使用](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)[深度优先搜索遍历](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)遍历树，对于树的每个节点，统计其子树中的节点数。从给定的树中移除任何节点都会导致两种不同类型的森林:

*   [由包括其左右子树在内的子树构成的连接组件](https://www.geeksforgeeks.org/connected-components-in-an-undirected-graph/)。
*   由包含其父节点的子树形成的连接组件

因此，请按照以下步骤解决问题:

*   使用 **DFS** 遍历树。
*   对于每个节点，递归计算其子树中的节点数。通过计算给定树中的节点总数与其子树中的节点总数之差，计算包含其父级的连接组件中的节点数。
*   保持更新为任何节点获得的连接组件的最大大小的最小值。
*   最后，打印所连接组件的最大尺寸最小值对应的节点。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

int mini = 105, ans, n;
vector<vector<int> > g(100);
int size[100];

// Function to create the graph
void create_graph()
{
    g[1].push_back(2);
    g[2].push_back(1);
    g[1].push_back(3);
    g[3].push_back(1);
    g[1].push_back(4);
    g[4].push_back(1);
    g[2].push_back(5);
    g[5].push_back(2);
    g[2].push_back(6);
    g[6].push_back(2);
}

// Function to traverse the graph
// and find the minimum of maximum
// size forest after removing a node
void dfs(int node, int parent)
{
    size[node] = 1;
    int mx = 0;

    // Traversing every child subtree
    // except the parent node
    for (int y : g[node]) {
        if (y == parent)
            continue;

        // Traverse all subtrees
        dfs(y, node);

        size[node] += size[y];

        // Update the maximum
        // size of forests
        mx = max(mx, size[y]);
    }

    // Update the minimum of maximum
    // size of forests obtained
    mx = max(mx, n - size[node]);

    // Condition to find the minimum
    // of maximum size forest
    if (mx < mini) {
        mini = mx;

        // Update and store the
        // corresponding node
        ans = node;
    }
}

// Driver Code
int main()
{
    n = 6;

    create_graph();

    dfs(1, -1);

    cout << ans << "\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG{

static int mini = 105, ans, n;
static Vector<Integer> []g = new Vector[100];
static int []size = new int[100];

// Function to create the graph
static void create_graph()
{
  g[1].add(2);
  g[2].add(1);
  g[1].add(3);
  g[3].add(1);
  g[1].add(4);
  g[4].add(1);
  g[2].add(5);
  g[5].add(2);
  g[2].add(6);
  g[6].add(2);
}

// Function to traverse the graph
// and find the minimum of maximum
// size forest after removing a node
static void dfs(int node, int parent)
{
  size[node] = 1;
  int mx = 0;

  // Traversing every child subtree
  // except the parent node
  for (int y : g[node])
  {
    if (y == parent)
      continue;

    // Traverse all subtrees
    dfs(y, node);

    size[node] += size[y];

    // Update the maximum
    // size of forests
    mx = Math.max(mx, size[y]);
  }

  // Update the minimum of maximum
  // size of forests obtained
  mx = Math.max(mx, n - size[node]);

  // Condition to find the minimum
  // of maximum size forest
  if (mx < mini)
  {
    mini = mx;

    // Update and store the
    // corresponding node
    ans = node;
  }
}

// Driver Code
public static void main(String[] args)
{
  n = 6;

  for (int i = 0; i < g.length; i++)
    g[i] = new Vector<Integer>();

  create_graph();
  dfs(1, -1);
  System.out.print(ans + "\n");
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
mini = 105;
ans = 0;
n = 0;
g = [];
size = [0] * 100;

# Function to create the graph
def create_graph():

    g[1].append(2);
    g[2].append(1);
    g[1].append(3);
    g[3].append(1);
    g[1].append(4);
    g[4].append(1);
    g[2].append(5);
    g[5].append(2);
    g[2].append(6);
    g[6].append(2);

# Function to traverse the graph
# and find the minimum of maximum
# size forest after removing a Node
def dfs(Node, parent):

    size[Node] = 1;
    mx = 0;
    global mini
    global ans

    # Traversing every child subtree
    # except the parent Node
    for y in g[Node]:
        if (y == parent):
            continue;

        # Traverse all subtrees
        dfs(y, Node);

        size[Node] += size[y];

        # Update the maximum
        # size of forests
        mx = max(mx, size[y]);

    # Update the minimum of maximum
    # size of forests obtained
    mx = max(mx, n - size[Node]);

    # Condition to find the minimum
    # of maximum size forest
    if (mx < mini):
        mini = mx;

        # Update and store the
        # corresponding Node
        ans = Node;

# Driver Code
if __name__ == '__main__':

    n = 6;
    for i in range(100):
        g.append([])
    create_graph();
    dfs(1, -1);
    print(ans);

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;
class GFG{

static int mini = 105, ans, n;
static List<int> []g = new List<int>[100];
static int []size = new int[100];

// Function to create the graph
static void create_graph()
{
  g[1].Add(2);
  g[2].Add(1);
  g[1].Add(3);
  g[3].Add(1);
  g[1].Add(4);
  g[4].Add(1);
  g[2].Add(5);
  g[5].Add(2);
  g[2].Add(6);
  g[6].Add(2);
}

// Function to traverse the graph
// and find the minimum of maximum
// size forest after removing a node
static void dfs(int node, int parent)
{
  size[node] = 1;
  int mx = 0;

  // Traversing every child subtree
  // except the parent node
  foreach (int y in g[node])
  {
    if (y == parent)
      continue;

    // Traverse all subtrees
    dfs(y, node);

    size[node] += size[y];

    // Update the maximum
    // size of forests
    mx = Math.Max(mx, size[y]);
  }

  // Update the minimum of maximum
  // size of forests obtained
  mx = Math.Max(mx, n - size[node]);

  // Condition to find the minimum
  // of maximum size forest
  if (mx < mini)
  {
    mini = mx;

    // Update and store the
    // corresponding node
    ans = node;
  }
}

// Driver Code
public static void Main(String[] args)
{
  n = 6;
  for (int i = 0; i < g.Length; i++)
    g[i] = new List<int>();

  create_graph();
  dfs(1, -1);
  Console.Write(ans + "\n");
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

var mini = 105, ans, n;
var g = Array.from(Array(100), ()=> new Array());
var size = Array(100).fill(0);

// Function to create the graph
function create_graph()
{
    g[1].push(2);
    g[2].push(1);
    g[1].push(3);
    g[3].push(1);
    g[1].push(4);
    g[4].push(1);
    g[2].push(5);
    g[5].push(2);
    g[2].push(6);
    g[6].push(2);
}

// Function to traverse the graph
// and find the minimum of Math.maximum
// size forest after removing a node
function dfs(node, parent)
{
    size[node] = 1;
    var mx = 0;

    // Traversing every child subtree
    // except the parent node
    g[node].forEach(y => {

        if (y != parent)
        {

        // Traverse all subtrees
        dfs(y, node);

        size[node] += size[y];

        // Update the Math.maximum
        // size of forests
        mx = Math.max(mx, size[y]);
        }
    });

    // Update the minimum of Math.maximum
    // size of forests obtained
    mx = Math.max(mx, n - size[node]);

    // Condition to find the minimum
    // of Math.maximum size forest
    if (mx < mini) {
        mini = mx;

        // Update and store the
        // corresponding node
        ans = node;
    }
}

// Driver Code

n = 6;
create_graph();
dfs(1, -1);
document.write( ans );

</script>
```

**Output**

```
2
```

***时间复杂度:** O(N)，其中 N 为节点数。*
***辅助空间:** O(N)*