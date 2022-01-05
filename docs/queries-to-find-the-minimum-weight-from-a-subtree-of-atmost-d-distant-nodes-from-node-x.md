# 从节点 X 的距离为 D 的节点的子树中寻找最小权重的查询

> 原文:[https://www . geesforgeks . org/query-to-find-最小权重-从 Atmos-d-distance-nodes-from-x/](https://www.geeksforgeeks.org/queries-to-find-the-minimum-weight-from-a-subtree-of-atmost-d-distant-nodes-from-node-x/)

给定一个以 **1** 为根的 **N 元树**，一个由分配给每个节点的权重组成的数组 **val[]** ，以及一个由形式为 **{X，D}** 的查询组成的矩阵 **Q[][]** ，每个查询的任务是找到分配给与节点 **X** 相距 **D** 的节点的所有权重的最小值。

**示例:**

> **输入:**q[]= { { 1，2}，{2，1}}，val[] = {1，2，3，3，5}
> 
> ```
>            1
>           / \
>          4   5
>         /
>        3
>       /
>      2
> 
> ```
> 
> **输出:**
> 1
> 3
> T5】解释:
> 查询 1: X = 1，D = 2
> 距离节点 1 距离为 2 的节点 atmost 为{1，3，4，5}，分配给这些节点的权重分别为{1，3，3，5}。
> 因此，分配的最小重量为 1。
> 查询 2: X = 2，D = 1
> 距离节点 2 距离为 1 的节点大气为{2，3}，分配给这些节点的权重分别为{2，3}。
> 因此，分配的最小权重为 2。
> 
> **输入:**q[]= { { 1，2}}，val[] = {1，2，4}
> 
> ```
>             1
>            / \
>           2   3
> 
> ```
> 
> **输出:** 1

**天真方法:**
求解每个查询最简单的方法是迭代树，找到距离节点 **X** 最远的所有节点 **D** ，找到分配给这些节点的所有权重的**最小值**。
***时间复杂度:** O(Q * N)
**辅助空间:** O(1)*

**高效方法:**
要优化上述方法，请按照以下步骤操作:

*   实现树的[欧拉游](https://www.geeksforgeeks.org/euler-tour-tree/)，给树的每个节点分配一个索引。
*   现在，在每个索引处，将**深度**和与节点相关联的值存储在一个数组中。
*   在数组上建立[合并排序树](https://www.geeksforgeeks.org/merge-sort-tree-for-range-order-statistics/)，[根据节点深度排序](https://www.geeksforgeeks.org/merge-sort/)范围。
*   对于每个查询，已知 X 的子树的所有节点位于 in[X]和 out[X]数组之间，其中 in 和 out 是节点执行 [DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 的索引。
*   在这个范围内，找到距离最大为 **D** 的最小加权节点。构建**合并排序树**，按照**深度** 的*递增顺序合并两个范围，在**合并排序树**的每个节点的值中找到**前缀最小值**。*

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

const int INF = 1e9 + 9;

/// Function to perform DFs
void dfs(int a, int par, int dep,
         vector<vector<int> >& v,
         vector<int>& depth, vector<int>& in,
         vector<int>& out,
         vector<pair<int, int> >& inv,
         vector<int>& val, int& tim)
{

    // Assign depth
    depth[a] = dep;

    // Assign in-time
    in[a] = ++tim;

    // Store depth and value to
    // construct Merge Sort Tree
    inv[tim] = make_pair(depth[a], val[a]);
    for (int i : v[a]) {

        // Skip the parent
        if (i == par)
            continue;

        dfs(i, a, dep + 1, v, depth, in,
            out, inv, val, tim);
    }

    // Assign out-time
    out[a] = tim;
}

// Function to build the Merge Sort Tree
void build(int node, int l, int r,
           vector<vector<pair<int,
                              int> > >& segtree,
           vector<pair<int, int> >& inv)
{

    // If the current node is
    // a leaf node
    if (l == r) {

        segtree[node].push_back(inv[l]);
        return;
    }

    int mid = (l + r) >> 1;

    // Recursively build left and right subtree
    build(2 * node + 1, l, mid, segtree, inv);
    build(2 * node + 2, mid + 1, r, segtree, inv);

    // Merge left and right node
    // of merge sort tree
    merge(segtree[2 * node + 1].begin(),
          segtree[2 * node + 1].end(),
          segtree[2 * node + 2].begin(),
          segtree[2 * node + 2].end(),
          back_inserter(segtree[node]));

    int mn = INF;

    for (auto& i : segtree[node]) {

        // Compute the prefix minimum
        mn = min(mn, i.second);
        i.second = mn;
    }
}

// Function to solve each query
int query(int x, int y, int dep, int node,
          int l, int r,
          vector<vector<pair<int,
                             int> > >& segtree)
{
    // Check for no overlap
    if (l > y || r < x || x > y)
        return INF;

    // Condition for complete overlap
    if (x <= l && r <= y) {

        // Find the node with
        // depth greater than d;
        auto it
            = upper_bound(segtree[node].begin(),
                          segtree[node].end(),
                          make_pair(dep, INF));

        if (it == segtree[node].begin())

            // Return if the first depth
            // is greater than d
            return INF;

        // Decrement the pointer;
        it--;

        // Return prefix minimum
        return it->second;
    }
    int mid = (l + r) >> 1;
    int a = query(x, y, dep, 2 * node + 1,
                  l, mid, segtree);

    int b = query(x, y, dep, 2 * node + 2,
                  mid + 1, r, segtree);

    return min(a, b);
}

// Function to compute the queries
void answerQueries(vector<pair<int, int> > queries,
                   vector<vector<int> >& v,
                   vector<int> val, int n)
{
    // Stores the time
    int tim = 0;

    // Stores the in and out time
    vector<int> in(n + 10), out(n + 10);

    // Stores depth
    vector<int> depth(n + 10);

    vector<pair<int, int> > inv(n + 10);
    dfs(1, 0, 0, v, depth, in, out, inv, val, tim);

    // Merge sort tree to store
    // depth of each node
    vector<vector<pair<int,
                       int> > >
        segtree(4 * n + 10);

    // Construct the merge sort tree
    build(0, 1, tim, segtree, inv);

    for (auto& i : queries) {

        int x = i.first;
        int dep = depth[x] + i.second;

        // Find the minimum value in subtree of x
        // and subtree of x lies from in[x]
        // to out[x] in merge sort tree
        int minVal = query(in[x], out[x], dep, 0,
                           1, tim, segtree);
        cout << minVal << endl;
    }
}

// Driver Code
int main()
{

    /*
                    1
                   /  \
                 4     5
                /
               3
              /
            2
    */
    int n = 5;

    // Stores the graph
    vector<vector<int> > v(n + 1);

    // Stores the weights
    vector<int> val(n + 1);

    // Assign edges
    v[1].push_back(4);
    v[4].push_back(1);
    v[1].push_back(5);
    v[5].push_back(1);
    v[4].push_back(3);
    v[3].push_back(4);
    v[3].push_back(2);
    v[2].push_back(3);

    // Assign weights
    val[1] = 1;
    val[2] = 3;
    val[3] = 2;
    val[4] = 3;
    val[5] = 5;

    // Stores the queries
    vector<pair<int, int> > queries = { { 1, 2 },
                                        { 2, 1 } };

    answerQueries(queries, v, val, n);
    return 0;
}
```

**Output:**

```
1
3

```

***时间复杂度:**O(N * log(N)+Q * log(N))*
***辅助空间:** O(N * log N)*