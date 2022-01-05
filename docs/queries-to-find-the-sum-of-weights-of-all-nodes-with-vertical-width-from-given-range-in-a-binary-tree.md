# 查询二叉树中给定范围内所有垂直宽度节点的权重之和

> 原文:[https://www . geeksforgeeks . org/query-to-find-从二叉树中给定范围找到垂直宽度的所有节点的权重之和/](https://www.geeksforgeeks.org/queries-to-find-the-sum-of-weights-of-all-nodes-with-vertical-width-from-given-range-in-a-binary-tree/)

给定由值在范围**【0，N–1】**内的 **N** 节点组成的[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，根为 **0** ，大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)wt【】，其中**wt【I】**是**I<sup>th</sup>T19】节点和 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)T25 的权重 每个查询的任务是找出[垂直宽度](https://www.geeksforgeeks.org/width-binary-tree-set-1/)在**【L，R】**范围内的所有节点的权重之和。**

**示例:**

> **输入:** N = 4，wt[] = {1，2，3，4}，Q[][] = {{0，1}，{1，1}}
> 
> 0(1)
> /\
> 3(4)1(2)
> /
> 2(3)
> **输出:**
> 6
> 10
> **解释:**
> **对于查询 1:** 范围为[0，1]
> 
> 1.  宽度位置为 0: 0，2 的节点。因此，节点的总和是 1 + 3 = 4。
> 2.  宽度位置 1: 1 处的节点。因此，节点的总和为 2。
> 
> 因此，所有节点的权重之和= 4 + 2 = 6。
> 
> **查询 2:** 范围为[-1，1]
> 
> 1.  宽度位置-1 的节点是 3。因此，节点的总和为 4。
> 2.  宽度位置为 0: 0，2 的节点。因此，节点的总和是 1 + 3 = 4。
> 3.  宽度位置 1: 1 处的节点。因此，节点的总和为 2。
> 
> 因此，所有节点的权重之和= 4 + 4 + 2 = 10。
> 
> **输入:** N= 8，wt[] = {8，6，4，5，1，2，9，1}，Q[][]= {-1，1}，{-2，-1}，{0，3}}
> 
> 1
> /\
> 3 2
> /\ \
> 5 6 4
> /\
> 7 0
> T7】输出:T9】25
> 7
> 29

**天真方法:**解决给定问题的最简单方法是[对每个查询执行树](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)遍历，然后打印位于给定范围内的所有节点的权重总和**【L，R】**。

***时间复杂度:** O(N*Q)*
***辅助空间:** O(1)*

**高效方法:**上述方法也可以通过预先计算每个宽度位置的权重之和并将其存储在[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/) **M** 中，然后找到新创建数组的[前缀之和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)来进行优化，从而在恒定时间内处理查询。按照以下步骤解决问题:

*   [对给定的树](https://www.geeksforgeeks.org/dfs-traversal-of-a-tree-using-recursion/)执行 DFS 遍历，更新所有宽度位置的总和，并通过执行以下操作将其存储在[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/) **M** 中:
    *   最初，根的位置**位置**是 **0** 。
    *   在每个[递归调用](https://www.geeksforgeeks.org/recursion/)中，通过更新 **M[pos] = M[pos] + wt[node]** 来更新 **M** 中节点的权重。
    *   通过将**位置**递减 **1** ，递归调用到其左子级。
    *   通过将**位置**递增 **1** ，递归调用到它的右子级。
*   [遍历地图](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/) **M** 并将每个**键值对**的**值**更新为之前出现的值的总和。
*   现在，[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **查询[]** ，对于每个查询**【L，R】**，打印**(M[R]–M[L–1])**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Structure of a node
struct Node {
    int data;
    Node* left;
    Node* right;
};

// Function to create new node
Node* newNode(int d)
{
    Node* n = new Node;
    n->data = d;
    n->left = NULL;
    n->right = NULL;
    return n;
}

// Function to pre-compute the sum of
// weights at each width position
void findwt(Node* root, int wt[],
            map<int, int>& um,
            int width = 0)
{
    // Base Case
    if (root == NULL) {
        return;
    }

    // Update the current width
    // position weight
    um[width] += wt[root->data];

    // Recursive Call to its left
    findwt(root->left, wt, um,
           width - 1);

    // Recursive Call to its right
    findwt(root->right, wt, um,
           width + 1);
}

// Function to find the sum of the
// weights of nodes whose vertical
// widths lies over the range [L, R]
// for Q queries
void solveQueries(int wt[], Node* root,
                  vector<vector<int> > queries)
{
    // Stores the weight sum
    // of each width position
    map<int, int> um;

    // Function Call to fill um
    findwt(root, wt, um);

    // Stores the sum of all previous
    // nodes, while traversing Map
    int x = 0;

    // Traverse the Map um
    for (auto it = um.begin();
         it != um.end(); it++) {
        x += it->second;
        um[it->first] = x;
    }

    // Iterate over all queries
    for (int i = 0;
         i < queries.size(); i++) {

        int l = queries[i][0];
        int r = queries[i][1];

        // Print the result for the
        // current query [l, r]
        cout << um[r] - um[l - 1]
             << "\n";
    }
}

// Driver Code
int main()
{
    int N = 8;

    // Given Tree
    Node* root = newNode(1);
    root->left = newNode(3);
    root->left->left = newNode(5);
    root->left->right = newNode(6);
    root->right = newNode(2);
    root->right->right = newNode(4);
    root->right->right->left = newNode(7);
    root->right->right->right = newNode(0);
    int wt[] = { 8, 6, 4, 5, 1, 2, 9, 1 };
    vector<vector<int> > queries{ { -1, 1 },
                                  { -2, -1 },
                                  { 0, 3 } };

    solveQueries(wt, root, queries);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Structure of a node
static class Node
{
    int data;
    Node left;
    Node right;
}

// Function to create new node
static Node newNode(int d)
{
    Node n = new Node();
    n.data = d;
    n.left = null;
    n.right = null;
    return n;
}

// Function to pre-compute the sum of
// weights at each width position
static void findwt(Node root, int wt[],
                   TreeMap<Integer, Integer> um,
                   int width)
{

    // Base Case
    if (root == null)
    {
        return;
    }

    // Update the current width
    // position weight
    if (um.containsKey(width))
    {
        um.put(width, um.get(width) +
               wt[root.data]);
    }
    else
    {
        um.put(width, wt[root.data]);
    }

    // Recursive Call to its left
    findwt(root.left, wt, um,
           width - 1);

    // Recursive Call to its right
    findwt(root.right, wt, um,
           width + 1);
}

// Function to find the sum of the
// weights of nodes whose vertical
// widths lies over the range [L, R]
// for Q queries
static void solveQueries(int wt[], Node root,
                         int[][] queries)
{

    // Stores the weight sum
    // of each width position
    TreeMap<Integer,
            Integer> um = new TreeMap<Integer,
                                      Integer>();

    // Function Call to fill um
    findwt(root, wt, um, 0);

    // Stores the sum of all previous
    // nodes, while traversing Map
    int x = 0;

    // Traverse the Map um
      for(Map.Entry<Integer, Integer> it : um.entrySet())
      {
        x += it.getValue();
          um.put(it.getKey(), x);
    }

    // Iterate over all queries
    for(int i = 0; i < queries.length; i++)
    {
        int l = queries[i][0];
        int r = queries[i][1];

        // Print the result for the
        // current query [l, r]
          int ans = 0;
          if (um.containsKey(r))
          {
              ans = um.get(r);
        }

          if (um.containsKey(l - 1))
          {
              ans -= um.get(l - 1);
        }
        System.out.println(ans);
    }
}

// Driver Code
public static void main(String[] args)
{
    int N = 8;

    // Given Tree
    Node root = newNode(1);
    root.left = newNode(3);
    root.left.left = newNode(5);
    root.left.right = newNode(6);
    root.right = newNode(2);
    root.right.right = newNode(4);
    root.right.right.left = newNode(7);
    root.right.right.right = newNode(0);

    int wt[] = { 8, 6, 4, 5, 1, 2, 9, 1 };
    int queries[][] = { { -1, 1 },
                        { -2, -1 },
                        { 0, 3 } };

    solveQueries(wt, root, queries);
}
}

// This code is contributed by Dharanendra L V.
```

**Output:** 

```
25
7
29
```

***时间复杂度:**O(N * log N+Q)*
T5**辅助空间:** O(N)