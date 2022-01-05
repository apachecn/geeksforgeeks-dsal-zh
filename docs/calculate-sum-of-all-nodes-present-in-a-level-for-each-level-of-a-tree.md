# 计算树的每一级中存在的所有节点的总和

> 原文:[https://www . geeksforgeeks . org/计算树的每一级中所有节点的总和/](https://www.geeksforgeeks.org/calculate-sum-of-all-nodes-present-in-a-level-for-each-level-of-a-tree/)

给定由 **N** 节点(*以 0* 为根)组成的[类属树](https://www.geeksforgeeks.org/generic-treesn-array-trees/)，其中每个节点都与一个值相关联，该树的每个级别的任务是找到该树级别上存在的所有节点值的总和。

**示例:**

> **输入:** node_number = { 1，2，3，4，5，6，7，8，9，10 }，node_values = { 2，3，4，4，7，6，2，3，9，1 }
> 
> [![](img/909a1c04e02efb05f7e7340542a1a532.png)](https://media.geeksforgeeks.org/wp-content/uploads/pariwiseswapnodes.png)
> 
> **输出:**
> 0 级之和= 2
> 1 级之和= 7
> 2 级之和= 14
> 3 级之和= 18
> **说明:**
> 
> *   级别 0 = {1}上值为 2 的节点
> *   级别 1 = {2，3}上的节点，它们各自的值为{3，4}。总和= 7。
> *   级别 2 = {4，5，8}上的节点分别具有值{4，7，3}。总和= 14。
> *   级别 3 上的节点= {6，7，9，10}分别具有值{6，2，9，1}。总和= 18
> 
> **输入:**节点号= { 1 }，节点值= { 10 }
> 输出:0 级之和= 10

**方法:**按照以下步骤解决问题:

1.  [使用](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/) [DFS](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/) 或 [BFS](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/) 遍历树
2.  使用[这个](https://www.geeksforgeeks.org/level-node-tree-source-node-using-bfs/)方法存储这个节点的级别。
3.  然后，将节点值添加到数组中节点的相应级别，比如 **sum[ ]。**
4.  打印数组 **sum[]** ，显示每一层所有节点的总和。

下面是上述方法的实现:

## C++

```
// C++ implementation of
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to add edges to the tree
void add_edge(int a, int b,
              vector<vector<int> >& tree)
{
    // 0-based indexing
    a--, b--;

    tree[a].push_back(b);
    tree[b].push_back(a);
}

// Function to print sum of
// nodes on all levels of a tree
void dfs(int u, int level, int par,
         int node_values[], vector<vector<int> >& tree,
         map<int, int>& sum, int& depth)
{
    // update max depth of tree
    depth = max(depth, level);

    // Add value of current node
    // to its corresponding level
    sum[level] += node_values[u];

    for (int child : tree[u]) {

        if (child == par)
            continue;

        // Recursive traverse child nodes
        dfs(child, level + 1, u, node_values,
            tree, sum, depth);
    }
}

// Function to calculate sum of
// nodes of each level of the Tree
void getSum(int node_values[],
            vector<vector<int> >& tree)
{
    // Depth of the tree
    int depth = 0;

    // Stores sum at each level
    map<int, int> sum;

    dfs(0, 0,
        -1, node_values,
        tree, sum, depth);

    // Print final sum
    for (int i = 0; i <= depth; i++) {
        cout << "Sum of level " << i
             << " = " << sum[i] << endl;
    }
}

// Driver Code
int32_t main()
{

    // Create a tree structure
    int N = 10;

    vector<vector<int> > tree(N);
    add_edge(1, 2, tree);
    add_edge(1, 3, tree);
    add_edge(2, 4, tree);
    add_edge(3, 5, tree);
    add_edge(3, 8, tree);
    add_edge(5, 6, tree);
    add_edge(5, 7, tree);
    add_edge(8, 9, tree);
    add_edge(8, 10, tree);

    int node_values[]
        = { 2, 3, 4, 4, 7,
            6, 2, 3, 9, 1 };

    // Function call to get the sum
    // of nodes of different level
    getSum(node_values, tree);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// the above approach
import java.io.*;
import java.util.*;

class GFG{

static Map<Integer, Integer> sum = new HashMap<>();
static int depth = 0;

// Function to add edges to the tree
static void add_edge(int a, int b,
                     ArrayList<ArrayList<Integer>> tree)
{

    // 0-based indexing
    a--;
    b--;

    tree.get(a).add(b);
    tree.get(b).add(a);
}

// Function to print sum of
// Nodes on all levels of a tree
static void dfs(int u, int level, int par,
                int []node_values,
                ArrayList<ArrayList<Integer>> tree)
{

    // Update max depth of tree
    depth = Math.max(depth, level);

    // Add value of current node
    // to its corresponding level
    if (sum.containsKey(level))
    {
        sum.put(level, sum.get(level) +
                       node_values[u]);
    }
    else
        sum.put(level,node_values[u]);

    for(int child : tree.get(u))
    {
        if (child == par)
            continue;

        // Recursive traverse child nodes
        dfs(child, level + 1, u, node_values,
            tree);
    }
}

// Function to calculate sum of
// nodes of each level of the Tree
static void getSum(int []node_values,
                   ArrayList<ArrayList<Integer>> tree)
{

    dfs(0, 0, -1, node_values, tree);

    // Print final sum
    for(int i = 0; i <= depth; i++)
    {
        System.out.println("Sum of level " + (int) i +
                                     " = " + sum.get(i));
    }
}

// Driver Code
public static void main (String[] args)
{

    // Create a tree structure
    int N = 10;

    ArrayList<ArrayList<Integer>> tree = new ArrayList<ArrayList<Integer>>();
    for(int i = 0; i < N; i++)
       tree.add(new ArrayList<Integer>());

    add_edge(1, 2, tree);
    add_edge(1, 3, tree);
    add_edge(2, 4, tree);
    add_edge(3, 5, tree);
    add_edge(3, 8, tree);
    add_edge(5, 6, tree);
    add_edge(5, 7, tree);
    add_edge(8, 9, tree);
    add_edge(8, 10, tree);

    int []node_values = { 2, 3, 4, 4, 7,
                          6, 2, 3, 9, 1 };

    // Function call to get the sum
    // of nodes of different level
    getSum(node_values, tree);
}
}

// This code is contributed by avanitrachhadiya2155
```

## 蟒蛇 3

```
# Python3 implementation of
# the above approach

# Function to add edges to the tree
def add_edge(a, b):
    global tree

    # 0-based indexing
    a, b = a - 1, b - 1
    tree[a].append(b)
    tree[b].append(a)

# Function to prsum of
# nodes on all levels of a tree
def dfs(u, level, par, node_values):
    global sum, tree, depth

    # update max depth of tree
    depth = max(depth, level)

    # Add value of current node
    # to its corresponding level
    sum[level] = sum.get(level, 0) + node_values[u]
    for child in tree[u]:
        if (child == par):
            continue

        # Recursive traverse child nodes
        dfs(child, level + 1, u, node_values)

# Function to calculate sum of
# nodes of each level of the Tree
def getSum(node_values):
    global sum, depth, tree

    # Depth of the tree
    # depth = 0

    # Stores sum at each level
    # map<int, int> sum
    dfs(0, 0, -1, node_values)

    # Prfinal sum
    for i in range(depth + 1):
        print("Sum of level", i, "=", sum[i])

# Driver Code
if __name__ == '__main__':

    # Create a tree structure
    N = 10
    tree = [[] for i in range(N+1)]
    sum = {}
    depth = 0
    add_edge(1, 2)
    add_edge(1, 3)
    add_edge(2, 4)
    add_edge(3, 5)
    add_edge(3, 8)
    add_edge(5, 6)
    add_edge(5, 7)
    add_edge(8, 9)
    add_edge(8, 10)
    node_values = [2, 3, 4, 4, 7, 6, 2, 3, 9, 1]

    # Function call to get the sum
    # of nodes of different level
    getSum(node_values)

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# implementation of
// the above approach
using System;
using System.Collections.Generic;
class GFG
{

static Dictionary<int, int> sum = new Dictionary<int,int>();
  static int depth = 0;

// Function to add edges to the tree
static void add_edge(int a, int b, List<List<int>> tree)
{

    // 0-based indexing
    a--;
    b--;

    tree[a].Add(b);
    tree[b].Add(a);
}

// Function to print sum of
// Nodes on all levels of a tree
static void dfs(int u, int level, int par,
         int []node_values, List<List<int>> tree
         )
{

    // update max depth of tree
    depth = Math.Max(depth, level);

    // Add value of current node
    // to its corresponding level
    if(sum.ContainsKey(level))
      sum[level] += node_values[u];
    else
      sum[level] = node_values[u];

    foreach (int child in tree[u]) {

        if (child == par)
            continue;

        // Recursive traverse child nodes
        dfs(child, level + 1, u, node_values,
            tree);
    }
}

// Function to calculate sum of
// nodes of each level of the Tree
static void getSum(int []node_values, List<List<int>> tree)
{

    dfs(0, 0, -1, node_values, tree);

    // Print final sum
    for (int i = 0; i <= depth; i++) {
        Console.WriteLine("Sum of level " + (int) i + " = "+ sum[i]);
    }
}

// Driver Code
public static void Main()
{

    // Create a tree structure
    int N = 10;

    List<List<int> > tree = new List<List<int>>();
    for(int i = 0; i < N; i++)
       tree.Add(new List<int>());
    add_edge(1, 2, tree);
    add_edge(1, 3, tree);
    add_edge(2, 4, tree);
    add_edge(3, 5, tree);
    add_edge(3, 8, tree);
    add_edge(5, 6, tree);
    add_edge(5, 7, tree);
    add_edge(8, 9, tree);
    add_edge(8, 10, tree);

    int []node_values = {2, 3, 4, 4, 7,6, 2, 3, 9, 1};

    // Function call to get the sum
    // of nodes of different level
    getSum(node_values, tree);
}
}

// This code is contributed by bgangwar59.
```

## java 描述语言

```
<script>

// Javascript implementation of
// the above approach
var sum = new Map();
var depth = 0;

// Function to add edges to the tree
function add_edge(a, b, tree)
{

    // 0-based indexing
    a--;
    b--;

    tree[a].push(b);
    tree[b].push(a);
}

// Function to print sum of
// Nodes on all levels of a tree
function dfs(u, level, par, node_values, tree)
{

    // Update max depth of tree
    depth = Math.max(depth, level);

    // Push value of current node
    // to its corresponding level
    if (sum.has(level))
        sum.set(level, sum.get(level) +
                       node_values[u]);
    else
        sum.set(level, node_values[u])

    for(var child of tree[u])
    {
        if (child == par)
            continue;

        // Recursive traverse child nodes
        dfs(child, level + 1, u, node_values,
            tree);
    }
}

// Function to calculate sum of
// nodes of each level of the Tree
function getSum(node_values, tree)
{
    dfs(0, 0, -1, node_values, tree);

    // Print final sum
    for(var i = 0; i <= depth; i++)
    {
        document.write("Sum of level " + i +
                       " = "+ sum.get(i) + "<br>");
    }
}

// Driver Code

// Create a tree structure
var N = 10;
var tree = [];
for(var i = 0; i < N; i++)
   tree.push([]);

add_edge(1, 2, tree);
add_edge(1, 3, tree);
add_edge(2, 4, tree);
add_edge(3, 5, tree);
add_edge(3, 8, tree);
add_edge(5, 6, tree);
add_edge(5, 7, tree);
add_edge(8, 9, tree);
add_edge(8, 10, tree);
var node_values = [ 2, 3, 4, 4, 7,6, 2, 3, 9, 1 ];

// Function call to get the sum
// of nodes of different level
getSum(node_values, tree);

// This code is contributed by rrrtnx

</script>
```

**Output:** 

```
Sum of level 0 = 2
Sum of level 1 = 7
Sum of level 2 = 14
Sum of level 3 = 18
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)