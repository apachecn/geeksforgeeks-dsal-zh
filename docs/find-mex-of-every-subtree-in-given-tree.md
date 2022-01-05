# 找到给定树中每个子树的 MEX

> 原文:[https://www . geesforgeks . org/find-MEX-of-even-subtree-in-given-tree/](https://www.geeksforgeeks.org/find-mex-of-every-subtree-in-given-tree/)

给定一个由从 **0** 到**N–1**编号的 **N** 节点组成的[类属树](https://www.geeksforgeeks.org/generic-treesn-array-trees/)，其根在节点 **0** 和数组 **val[]** ，使得每个节点的值由 **val[i]** 表示，每个节点的任务是找到其子树的 **MEX** 的值。

> 节点 **V** 的 **MEX** 值定义为扎根于**节点 V** 的树中**最小缺失正数**。

**示例:**

> **输入:** N = 6，边= {{0，1}，{1，2}，{0，3}，{3，4}，{3，5}}，val[] = {4，3，5，1，0，2 }
> T3】输出:【6，0，0，3，1，0】
> **解释:**
> 0(4)
> /\
> 1(3)3(1)
> //
> 
> 在:
> **节点 0:** 的子树中，范围[0，5]中的所有值都存在，因此不存在的最小非负值是 6。
> **节点 1:** 节点 1 的子树中不存在的最小非负值为 0。
> **节点 2:** 不存在的节点 2 的子树中不存在的最小非负值为 0。
> **节点 3:** 范围[0，2]中的所有值都存在，因此节点 3 的子树中不存在的最小非负值是 3。
> **节点 4:** 节点 4 的子树中不存在的最小非负值为 1。
> **节点 5:** 节点 5 的子树中不存在的最小非负值为 0。

**方法:**给定的问题可以通过在给定的树上使用 [DFS 遍历并执行](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)[二分搜索法](https://www.geeksforgeeks.org/binary-search/)来找到每个节点子树中缺失的最小正整数来解决。按照以下步骤解决问题:

*   初始化一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)，比如说**sol【】**来存储每个节点的 MEX。
*   从节点 **0** 执行 [DFS 遍历](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)，并执行以下步骤:
    *   为向量中的每个节点存储 DFS 期间的所有节点。
    *   按照递归调用中每个节点的排序顺序合并两个向量。
    *   将排序列表上的[二分搜索法](https://www.geeksforgeeks.org/binary-search/)应用于[找到排序数组](https://www.geeksforgeeks.org/find-the-first-missing-number/)中不存在的最小非负整数值，并将当前子树的 **MEX** 的值存储在数组 **sol[]** 中。
*   完成上述步骤后，打印存储在数组**sol【】**中的值作为结果。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Stores the edges of the tree
vector<vector<int> > edges;

// Function to add edges
void add_edge(int x, int y)
{
    edges.push_back({ x, y });
}

// Function to merge two sorted vectors
vector<int> merge(vector<int>& a,
                  vector<int>& b)
{
    // To store the result
    vector<int> res;

    int i = 0, j = 0;
    int n = a.size(), m = b.size();

    // Iterating both vectors
    while (i < n && j < m) {
        if (a[i] < b[j])
            res.push_back(a[i++]);
        else if (b[j] < a[i])
            res.push_back(b[j++]);
    }

    // Pushing remaining elements of
    // vector a
    while (i < n)
        res.push_back(a[i++]);

    // Pushing remaining elements of
    // vector b
    while (j < m)
        res.push_back(b[j++]);

    return res;
}

// Function to perform the DFS Traversal
// that returns the subtree of node
// in sorted manner
vector<int> help(vector<int> tree[], int x,
                 int p, vector<int>& c,
                 vector<int>& sol)
{
    vector<int> res;
    res.push_back(c[x]);

    // Iterate the childrens
    for (auto i : tree[x]) {

        // All values of subtree
        // i in sorted manner
        if (i != p) {
            vector<int> tmp
                = help(tree, i, x, c, sol);
            res = merge(res, tmp);
        }
    }

    int l = 0, r = res.size() - 1;
    int ans = res.size();

    // Binary search to find MEX
    while (l <= r) {
        // Find the mid
        int mid = (l + r) / 2;

        // Update the ranges
        if (res[mid] > mid)
            r = mid - 1;
        else {
            ans = mid + 1;
            l = mid + 1;
        }
    }
    if (res[0] != 0)
        ans = 0;

    // Update the MEX for the current
    // tree node
    sol[x] = ans;

    return res;
}

// Function to find MEX of each
// subtree of tree
void solve(int A, vector<int> C)
{
    int n = A;
    vector<int> tree[n + 1];
    for (auto i : edges) {
        tree[i[0]].push_back(i[1]);
        tree[i[1]].push_back(i[0]);
    }
    vector<int> sol(n, 0);

    // Function Call
    help(tree, 0, -1, C, sol);

    // Printe the ans for each nodes
    for (auto i : sol)
        cout << i << " ";
}

// Driver Code
int main()
{
    int N = 6;
    add_edge(0, 1);
    add_edge(1, 2);
    add_edge(0, 3);
    add_edge(3, 4);
    add_edge(3, 5);

    vector<int> val = { 4, 3, 5, 1, 0, 2 };
    solve(N, val);

    return 0;
}
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Stores the edges of the tree
let edges = [];

// Function to add edges
function add_edge(x, y) {
  edges.push([x, y]);
}

// Function to merge two sorted vectors
function merge(a, b) {
  // To store the result
  let res = [];

  let i = 0,
    j = 0;
  let n = a.length,
    m = b.length;

  // Iterating both vectors
  while (i < n && j < m) {
    if (a[i] < b[j]) res.push(a[i++]);
    else if (b[j] < a[i]) res.push(b[j++]);
  }

  // Pushing remaining elements of
  // vector a
  while (i < n) res.push(a[i++]);

  // Pushing remaining elements of
  // vector b
  while (j < m) res.push(b[j++]);

  return res;
}

// Function to perform the DFS Traversal
// that returns the subtree of node
// in sorted manner
function help(tree, x, p, c, sol) {
  let res = [];
  res.push(c[x]);

  // Iterate the childrens
  for (let i of tree[x]) {
    // All values of subtree
    // i in sorted manner
    if (i != p) {
      let tmp = help(tree, i, x, c, sol);
      res = merge(res, tmp);
    }
  }

  let l = 0,
    r = res.length - 1;
  let ans = res.length;

  // Binary search to find MEX
  while (l <= r) {
    // Find the mid
    let mid = Math.floor((l + r) / 2);

    // Update the ranges
    if (res[mid] > mid) r = mid - 1;
    else {
      ans = mid + 1;
      l = mid + 1;
    }
  }
  if (res[0] != 0) ans = 0;

  // Update the MEX for the current
  // tree node
  sol[x] = ans;

  return res;
}

// Function to find MEX of each
// subtree of tree
function solve(A, C) {
  let n = A;
  let tree = new Array(n + 1).fill(0).map(() => []);
  for (let i of edges) {
    tree[i[0]].push(i[1]);
    tree[i[1]].push(i[0]);
  }
  let sol = new Array(n).fill(0);

  // Function Call
  help(tree, 0, -1, C, sol);

  // Printe the ans for each nodes
  for (let i of sol) document.write(i + " ");
}

// Driver Code

let N = 6;
add_edge(0, 1);
add_edge(1, 2);
add_edge(0, 3);
add_edge(3, 4);
add_edge(3, 5);

let val = [4, 3, 5, 1, 0, 2];
solve(N, val);

// This code is contributed by _saurabh_jaiswal.
</script>
```

**Output:** 

```
6 0 0 3 1 0
```

***时间复杂度:**O(N *(N+log N))*
***辅助空间:** O(N)*