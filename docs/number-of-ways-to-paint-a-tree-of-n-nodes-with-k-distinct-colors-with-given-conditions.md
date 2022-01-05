# 在给定条件下用 K 种不同颜色绘制 N 个节点的树的方法数量

> 原文:[https://www . geeksforgeeks . org/给定条件下用 k 种不同颜色绘制 n 节点树的方法数/](https://www.geeksforgeeks.org/number-of-ways-to-paint-a-tree-of-n-nodes-with-k-distinct-colors-with-given-conditions/)

给定一棵有 N 个节点和一个数字 K 的树。用 K 种可用颜色中的一种绘制树的每个节点。
计算并返回绘制树的方式数，使得距离为 1 或 2 的任意两个节点以不同的颜色绘制。
**示例:**输入的第一行包含两个整数 N 和 k。
下一行包含一对数组。每对(x，y)表示 x 和 y 之间的一条无向边

> **输入** : N = 3 K = 3
> 树= { (2，1)，(3，2) }
> **输出:** 6
> 我们有三种颜色，说红蓝绿。我们可以用以下方法画画。
> 
> <figure class="table">
> 
> | 节点 1 | 附注 2 | 节点 3 |
> | 红色 | 蓝色 | 格林（姓氏）；绿色的 |
> | 红色 | 格林（姓氏）；绿色的 | 蓝色 |
> | 蓝色 | 红色 | 格林（姓氏）；绿色的 |
> | 蓝色 | 格林（姓氏）；绿色的 | 红色 |
> | 格林（姓氏）；绿色的 | 红色 | 蓝色 |
> | 格林（姓氏）；绿色的 | 蓝色 | 红色 |
> 
> 因此 6 是答案。
> **输入:** N = 5 K = 6
> 树= { (1，2)，(5，1)，(3，1)，(4，2) }
> **输出:** 48
> 
> </figure>

**方法:**
让我们在节点 1 处对树进行根处理，然后从根向下移动到叶子开始绘制。对于根，我们可以用 k 种可用的颜色来绘制它。如果根有 x 个子，我们可以用 **<sup>k-1</sup> P <sub>x</sub>** 的方式来画，那就是
(k-1)！/(k-1-x)！。因为每个孩子都必须使用不同的颜色，它们都应该不同于根所用的颜色。
现在对于剩余的节点，我们一次绘制一个特定节点 v 的所有子节点。他们的颜色必须与 v 和 v 的父亲所用的颜色截然不同。所以如果 v 有 x 个儿子，我们可以用**<sup>k-2</sup>P<sub>x</sub>**的方式
画出来，下面是上面的做法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ Implementation of above approach
#include <bits/stdc++.h>
using namespace std;
const int maxx = 1e5;
vector<int> tree[maxx];
int degree_of_node[maxx], parent_of_node[maxx],
    child_of_node[maxx], flag = -1;

// Function to calculate number of children
// of every node in a tree with root 1
void dfs(int current, int parent)
{
    parent_of_node[current] = parent;
    for (int& child : tree[current]) {

        // If current and parent are same we have
        // already visited it, so no need to visit again
        if (child == parent)
            return;
        dfs(child, current);
    }

    // If the current node is a leaf node
    if (degree_of_node[current] == 1 && current != 1) {

        // For leaf nodes there will be no child.
        child_of_node[current] = 0;
        return;
    }

    // Gives the total child of current node
    int total_child = 0;
    for (auto& child : tree[current]) {
        if (child == parent)
            return;
        else
            ++total_child;
    }
    child_of_node[current] = total_child;
    return;
}

// Function to calculate permutations ( nPr )
int find_nPr(int N, int R)
{
    if (R > N) {
        flag = 0;
        return 0;
    }
    int total = 1;
    for (int i = N - R + 1; i <= N; ++i) {
        total = total * i;
    }
    return total;
}

// Function to calculate the number of ways
// to paint the tree according to given conditions
int NoOfWays(int Nodes, int colors)
{

    // Do dfs to find parent and child of a node,
    // we root the tree at node 1.
    dfs(1, -1);

    // Now start iterating for all nodes of
    // the tree and count the number of ways to
    // paint its children and node itself
    int ways = 0;
    for (int i = 1; i <= Nodes; ++i) {

        // If the current node is root node, then
        // we have total of K ways to paint it and
        // (k-1)P(x) to paint its child
        if (i == 1) {
            ways = ways + colors *
                   find_nPr(colors - 1, child_of_node[1]);
        }
        else {

            // For other remaining nodes which are not
            // leaf nodes we have (k-2)P(x) to paint
            // its children, we will not take into
            // consideration of current node
            // since we already painted it.
            if (degree_of_node[i] == 1) {
                continue;
            }
            else {
                ways = ways *
                find_nPr(colors - 2, child_of_node[i]);
            }
        }
    }
    return ways;
}

// Function to build the tree
void MakeTree()
{

    tree[2].push_back(1);
    tree[1].push_back(2);
    tree[3].push_back(2);
    tree[2].push_back(3);
    degree_of_node[2]++;
    degree_of_node[1]++;
    degree_of_node[3]++;
    degree_of_node[2]++;
}

// Driver Code
int main()
{
    int N = 3, K = 3;
    MakeTree();
    int Count = NoOfWays(N, K);
    cout << Count << "\n";
    return 0;
}
```

**Output:** 

```
6
```

**时间复杂度** : O(N)