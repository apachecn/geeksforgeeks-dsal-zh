# 双色树中色差最小的子树

> 原文:[https://www . geesforgeks . org/sub-tree-mini-color-difference-2-color-tree/](https://www.geeksforgeeks.org/sub-tree-minimum-color-difference-2-coloured-tree/)

一棵树有 N 个节点和 N-1 条边，它的节点有两种不同的颜色。
找到色差最小的子树，即 abs(1 色节点–2 色节点)最小。
**例:**

```
Input : 
Edges : 1 2
        1 3
        2 4
        3 5
Colours : 1 1 2 2 1 [1-based indexing where 
                    index denotes the node]
Output : 2
Explanation : The sub-tree {1-2} and {1-2-3-5}
have color difference of 2\. Sub-tree {1-2} has two
1-colour nodes and zero 2-colour nodes. So, color 
difference is 2\. Sub-tree {1-2-3-5} has three 1-colour
nodes and one 2-colour nodes. So color diff = 2.
```

**方法 1 :** 从树的每个节点检查每个可能的子树，就可以解决这个问题。这将花费指数时间，因为我们将检查每个节点的子树。
**方法二:(高效)**如果我们观察，我们在解一部分树好几次。这会产生反复出现的子问题。我们可以使用 [**动态编程**](https://www.geeksforgeeks.org/dynamic-programming/) 的方法，在一次遍历中获得最小的色差。为了使事情更简单，我们可以将颜色值设为 1 和-1。现在，如果我们有一个两个颜色节点相等的子树，我们的颜色总和将为 0。为了得到最小差，我们应该有最大负和或最大正和。

*   **情况 1** 当我们需要有一个最大和的子树时:我们取一个节点，如果它的值> 0，即和(父)+=最大(0，和(子))
*   **情况 2** 当我们需要有一个最小和(或最大负和)的子树时:我们取一个节点如果它的值<为 0，即和(父)+= min(0，和(子))

为了得到最小和，我们可以交换节点的颜色，即-1 变成 1，反之亦然。
下面是实现:

## C++

```
// CPP code to find the sub-tree with minimum color
// difference in a 2-coloured tree
#include <bits/stdc++.h>
using namespace std;

// Tree traversal to compute minimum difference
void dfs(int node, int parent, vector<int> tree[],
                    int colour[], int answer[])
{
    // Initial min difference is the color of node
    answer[node] = colour[node];

    // Traversing its children
    for (auto u : tree[node]) {

        // Not traversing the parent
        if (u == parent)
            continue;

        dfs(u, node, tree, colour, answer);

        // If the child is adding positively to
        // difference, we include it in the answer
        // Otherwise, we leave the sub-tree and
        // include 0 (nothing) in the answer
        answer[node] += max(answer[u], 0);
    }
}

int maxDiff(vector<int> tree[], int colour[], int N)
{
       int answer[N + 1];
       memset(answer, 0, sizeof(answer));

    // DFS for colour difference : 1colour - 2colour
    dfs(1, 0, tree, colour, answer);

    // Minimum colour difference is maximum answer value
    int high = 0;
    for (int i = 1; i <= N; i++) {
        high = max(high, answer[i]);

        // Clearing the current value
        // to check for colour2 as well
        answer[i] = 0;
    }

    // Interchanging the colours
    for (int i = 1; i <= N; i++) {
        if (colour[i] == -1)
            colour[i] = 1;
        else
            colour[i] = -1;
    }

    // DFS for colour difference : 2colour - 1colour
    dfs(1, 0, tree, colour, answer);

    // Checking if colour2 makes the minimum colour
    // difference
    for (int i = 1; i < N; i++)
        high = max(high, answer[i]);

    return high;
}

// Driver code
int main()
{
    // Nodes
    int N = 5;

    // Adjacency list representation
    vector<int> tree[N + 1];

    // Edges
    tree[1].push_back(2);
    tree[2].push_back(1);

    tree[1].push_back(3);
    tree[3].push_back(1);

    tree[2].push_back(4);
    tree[4].push_back(2);

    tree[3].push_back(5);
    tree[5].push_back(3);

    // Index represent the colour of that node
    // There is no Node 0, so we start from
    // index 1 to N
    int colour[] = { 0, 1, 1, -1, -1, 1 };

    // Printing the result
    cout << maxDiff(tree,  colour,  N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find the sub-tree
// with minimum color difference
// in a 2-coloured tree
import java.util.*;
class GFG
{

// Tree traversal to compute minimum difference
static void dfs(int node, int parent,
                Vector<Integer> tree[], 
                int colour[], int answer[])
{
    // Initial min difference is
    // the color of node
    answer[node] = colour[node];

    // Traversing its children
    for (Integer u : tree[node])
    {

        // Not traversing the parent
        if (u == parent)
            continue;

        dfs(u, node, tree, colour, answer);

        // If the child is adding positively to
        // difference, we include it in the answer
        // Otherwise, we leave the sub-tree and
        // include 0 (nothing) in the answer
        answer[node] += Math.max(answer[u], 0);
    }
}

static int maxDiff(Vector<Integer> tree[],
                   int colour[], int N)
{
    int []answer = new int[N + 1];

    // DFS for colour difference : 1colour - 2colour
    dfs(1, 0, tree, colour, answer);

    // Minimum colour difference is
    // maximum answer value
    int high = 0;
    for (int i = 1; i <= N; i++)
    {
        high = Math.max(high, answer[i]);

        // Clearing the current value
        // to check for colour2 as well
        answer[i] = 0;
    }

    // Interchanging the colours
    for (int i = 1; i <= N; i++)
    {
        if (colour[i] == -1)
            colour[i] = 1;
        else
            colour[i] = -1;
    }

    // DFS for colour difference : 2colour - 1colour
    dfs(1, 0, tree, colour, answer);

    // Checking if colour2 makes the
    // minimum colour difference
    for (int i = 1; i < N; i++)
        high = Math.max(high, answer[i]);

    return high;
}

// Driver code
public static void main(String []args)
{

    // Nodes
    int N = 5;

    // Adjacency list representation
    Vector<Integer> tree[] = new Vector[N + 1];
    for(int i = 0; i < N + 1; i++)
        tree[i] = new Vector<Integer>();

    // Edges
    tree[1].add(2);
    tree[2].add(1);

    tree[1].add(3);
    tree[3].add(1);

    tree[2].add(4);
    tree[4].add(2);

    tree[3].add(5);
    tree[5].add(3);

    // Index represent the colour of that node
    // There is no Node 0, so we start from
    // index 1 to N
    int colour[] = { 0, 1, 1, -1, -1, 1 };

    // Printing the result
    System.out.println(maxDiff(tree, colour, N));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 code to find the sub-tree
# with minimum color difference
# in a 2-coloured tree

# Tree traversal to compute minimum difference
def dfs(node, parent, tree, colour, answer):
    # Initial min difference is
    # the color of node
    answer[node] = colour[node]

    # Traversing its children
    for u in tree[node]:

        # Not traversing the parent
        if (u == parent):
            continue

        dfs(u, node, tree, colour, answer)

        # If the child is Adding positively to
        # difference, we include it in the answer
        # Otherwise, we leave the sub-tree and
        # include 0 (nothing) in the answer
        answer[node] += max(answer[u], 0)

def maxDiff(tree, colour, N):
    answer = [0 for _ in range(N+1)]

    # DFS for colour difference : 1colour - 2colour
    dfs(1, 0, tree, colour, answer)

    # Minimum colour difference is
    # maximum answer value
    high = 0
    for i in range(1, N+1):
        high = max(high, answer[i])

        # Clearing the current value
        # to check for colour2 as well
        answer[i] = 0

    # Interchanging the colours
    for i in range(1, N+1):
        if colour[i] == -1:
            colour[i] = 1
        else:
            colour[i] = -1

    # DFS for colour difference : 2colour - 1colour
    dfs(1, 0, tree, colour, answer)

    # Checking if colour2 makes the
    # minimum colour difference
    for i in range(1, N):
        high = max(high, answer[i])

    return high

# Driver code
# Nodes
N = 5

# Adjacency list representation
tree = [list() for _ in range(N+1)]

# Edges
tree[1].append(2)
tree[2].append(1)
tree[1].append(3)
tree[3].append(1)
tree[2].append(4)
tree[4].append(2)
tree[3].append(5)
tree[5].append(3)

# Index represent the colour of that node
# There is no Node 0, so we start from
# index 1 to N
colour = [0, 1, 1, -1, -1, 1]

# Printing the result
print(maxDiff(tree, colour, N))

# This code is contributed by nitibi9839.
```

## C#

```
// C# code to find the sub-tree
// with minimum color difference
// in a 2-coloured tree
using System;
using System.Collections.Generic;

class GFG
{

// Tree traversal to compute minimum difference
static void dfs(int node, int parent,
                List<int> []tree,
                int []colour, int []answer)
{
    // Initial min difference is
    // the color of node
    answer[node] = colour[node];

    // Traversing its children
    foreach (int u in tree[node])
    {

        // Not traversing the parent
        if (u == parent)
            continue;

        dfs(u, node, tree, colour, answer);

        // If the child is Adding positively to
        // difference, we include it in the answer
        // Otherwise, we leave the sub-tree and
        // include 0 (nothing) in the answer
        answer[node] += Math.Max(answer[u], 0);
    }
}

static int maxDiff(List<int> []tree,
                         int []colour, int N)
{
    int []answer = new int[N + 1];

    // DFS for colour difference : 1colour - 2colour
    dfs(1, 0, tree, colour, answer);

    // Minimum colour difference is
    // maximum answer value
    int high = 0;
    for (int i = 1; i <= N; i++)
    {
        high = Math.Max(high, answer[i]);

        // Clearing the current value
        // to check for colour2 as well
        answer[i] = 0;
    }

    // Interchanging the colours
    for (int i = 1; i <= N; i++)
    {
        if (colour[i] == -1)
            colour[i] = 1;
        else
            colour[i] = -1;
    }

    // DFS for colour difference : 2colour - 1colour
    dfs(1, 0, tree, colour, answer);

    // Checking if colour2 makes the
    // minimum colour difference
    for (int i = 1; i < N; i++)
        high = Math.Max(high, answer[i]);

    return high;
}

// Driver code
public static void Main(String []args)
{

    // Nodes
    int N = 5;

    // Adjacency list representation
    List<int> []tree = new List<int>[N + 1];
    for(int i = 0; i < N + 1; i++)
        tree[i] = new List<int>();

    // Edges
    tree[1].Add(2);
    tree[2].Add(1);

    tree[1].Add(3);
    tree[3].Add(1);

    tree[2].Add(4);
    tree[4].Add(2);

    tree[3].Add(5);
    tree[5].Add(3);

    // Index represent the colour of that node
    // There is no Node 0, so we start from
    // index 1 to N
    int []colour = { 0, 1, 1, -1, -1, 1 };

    // Printing the result
    Console.WriteLine(maxDiff(tree, colour, N));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript code to find the sub-tree
// with minimum color difference
// in a 2-coloured tree

// Tree traversal to compute minimum difference
function dfs(node, parent, tree, colour, answer)
{
    // Initial min difference is
    // the color of node
    answer[node] = colour[node];

    // Traversing its children
    for(var u of tree[node])
    {

        // Not traversing the parent
        if (u == parent)
            continue;

        dfs(u, node, tree, colour, answer);

        // If the child is Adding positively to
        // difference, we include it in the answer
        // Otherwise, we leave the sub-tree and
        // include 0 (nothing) in the answer
        answer[node] += Math.max(answer[u], 0);
    }
}

function maxDiff(tree, colour, N)
{
    var answer = Array(N+1).fill(0);

    // DFS for colour difference : 1colour - 2colour
    dfs(1, 0, tree, colour, answer);

    // Minimum colour difference is
    // maximum answer value
    var high = 0;
    for (var i = 1; i <= N; i++)
    {
        high = Math.max(high, answer[i]);

        // Clearing the current value
        // to check for colour2 as well
        answer[i] = 0;
    }

    // Interchanging the colours
    for (var i = 1; i <= N; i++)
    {
        if (colour[i] == -1)
            colour[i] = 1;
        else
            colour[i] = -1;
    }

    // DFS for colour difference : 2colour - 1colour
    dfs(1, 0, tree, colour, answer);

    // Checking if colour2 makes the
    // minimum colour difference
    for (var i = 1; i < N; i++)
        high = Math.max(high, answer[i]);

    return high;
}

// Driver code
// Nodes
var N = 5;
// Adjacency list representation
var tree = Array.from(Array(N+1), ()=>Array());

// Edges
tree[1].push(2);
tree[2].push(1);
tree[1].push(3);
tree[3].push(1);
tree[2].push(4);
tree[4].push(2);
tree[3].push(5);
tree[5].push(3);
// Index represent the colour of that node
// There is no Node 0, so we start from
// index 1 to N
var colour = [0, 1, 1, -1, -1, 1];
// Printing the result
document.write(maxDiff(tree, colour, N));

</script>
```

**输出:**

```
2
```

本文由 [**罗希特·塔普利亚尔**](https://www.hackerrank.com/rohit_thapliyal) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。