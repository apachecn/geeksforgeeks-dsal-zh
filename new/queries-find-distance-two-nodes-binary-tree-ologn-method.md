# 查询以查找二叉树的两个节点之间的距离-O（logn）方法

> 原文：[https://www.geeksforgeeks.org/queries-find-distance-two-nodes-binary-tree-ologn-method/](https://www.geeksforgeeks.org/queries-find-distance-two-nodes-binary-tree-ologn-method/)

给定一个二叉树，任务是找到一棵二叉树中两个键之间的距离，没有给出父指针。 两个节点之间的距离是要遍历才能到达另一个节点的最小边数。

这个问题已经在[先前的文章](https://www.geeksforgeeks.org/find-distance-between-two-nodes-of-a-binary-tree/)中进行了讨论，但是它使用**二叉树的三个遍历**，一个遍历用于查找两个节点的最低公共祖先（LCA）（let A 和 B），然后进行两次遍历以查找 LCA 与 A 之间的距离以及 LCA 与 B 之间的时间复杂度为 O（n）。 在这篇文章中，将讨论一种方法，该方法需要 **O（log（n））**时间来找到两个节点的 LCA。

![](img/e98cf3d60cdbfebbe7118d29e43d5fed.png)

两个节点之间的距离可以根据最低的共同祖先获得。 以下是公式。

```
Dist(n1, n2) = Dist(root, n1) + Dist(root, n2) - 2*Dist(root, lca) 
'n1' and 'n2' are the two given keys
'root' is root of given Binary Tree.
'lca' is lowest common ancestor of n1 and n2
Dist(n1, n2) is the distance between n1 and n2.

```

上面的公式也可以写成：

```
Dist(n1, n2) = Level[n1] + Level[n2] - 2*Level[lca] 

```

此问题可以分解为：

1.  查找每个节点的级别

2.  寻找二叉树的欧拉之旅

3.  LCA 的构建段树，

这些步骤说明如下：

> 1.  通过应用[级别顺序遍历](https://www.geeksforgeeks.org/print-levels-nodes-binary-tree/)来找到每个节点的级别。
> 2.  通过将[二叉树](https://www.geeksforgeeks.org/euler-tour-binary-tree/)的 Euler 游标存储在数组中，并借助每个节点的级别和 Euler 游程来计算另外两个数组，从而在 O（logn）中找到二叉树中两个节点的 LCA。
>     这些步骤如下所示：
>     （I）首先，找到二叉树的 Euler Tour。
>     
> 
> ![](img/2708b1df3a48f61766a2991e20a9827a.png)
> 
> 欧拉二叉树示例
> 
> 1.  （II）然后，将每个节点的级别存储在不同阵列中的 Euler 阵列中。
>     
> 
> ![](img/46c3681a944153e098ee85c4a7d527ff.png)
> 
> 1.  （III）然后，将二叉树所有节点的第一个匹配项存储在 Euler 数组中。 H 存储来自 Euler 数组的节点的索引，因此可以最小化查找最小值的查询范围，并且可以通过进一步优化查询时间来最小化它们的查找范围。
>     
> 
> ![](img/df28d4f97f3049a97ec62a66b102db30.png)
> 
> 1.  然后 ***在 L 数组*** 上构建段树，并从 H 数组中获取低值和高值，这将使我们得出两个节点（A 和 B）的首次出现。 然后，*我们查询段树以找到范围内 X 的最小值*（ **H [A]至 H [B]** ）。 然后**我们使用值 X 的索引作为 Euler 数组的索引，以获得** ***LCA*** ，即 Euler [index（X）]。
>     设 A = 8 且 B =5。
>     （I）H [8] = 1 且 H [5] = 2
>     （II）查询段树，得到 L 数组中的最小值 当 X = 0，index = 7 时在 1 和 2 之间。
> 2.  最后，我们应用上面讨论的距离公式来获得两个节点之间的距离。

## C++

```cpp

// C++ program to find distance between
// two nodes for multiple queries
#include <bits/stdc++.h>
#define MAX 100001
using namespace std;

/* A tree node structure */
struct Node {
    int data;
    struct Node* left;
    struct Node* right;
};

/* Utility function to create a new Binary Tree node */
struct Node* newNode(int data)
{
    struct Node* temp = new struct Node;
    temp->data = data;
    temp->left = temp->right = NULL;
    return temp;
}

// Array to store level of each node
int level[MAX];

// Utility Function to store level of all nodes
void FindLevels(struct Node* root)
{
    if (!root)
        return;

    // queue to hold tree node with level
    queue<pair<struct Node*, int> > q;

    // let root node be at level 0
    q.push({ root, 0 });

    pair<struct Node*, int> p;

    // Do level Order Traversal of tree
    while (!q.empty()) {
        p = q.front();
        q.pop();

        // Node p.first is on level p.second
        level[p.first->data] = p.second;

        // If left child exits, put it in queue
        // with current_level +1
        if (p.first->left)
            q.push({ p.first->left, p.second + 1 });

        // If right child exists, put it in queue
        // with current_level +1
        if (p.first->right)
            q.push({ p.first->right, p.second + 1 });
    }
}

// Stores Euler Tour
int Euler[MAX];

// index in Euler array
int idx = 0;

// Find Euler Tour
void eulerTree(struct Node* root)
{

    // store current node's data
    Euler[++idx] = root->data;

    // If left node exists
    if (root->left) {

        // traverse left subtree
        eulerTree(root->left);

        // store parent node's data
        Euler[++idx] = root->data;
    }

    // If right node exists
    if (root->right) {
        // traverse right subtree
        eulerTree(root->right);

        // store parent node's data
        Euler[++idx] = root->data;
    }
}

// checks for visited nodes
int vis[MAX];

// Stores level of Euler Tour
int L[MAX];

// Stores indices of first occurrence
// of nodes in Euler tour
int H[MAX];

// Preprocessing Euler Tour for finding LCA
void preprocessEuler(int size)
{
    for (int i = 1; i <= size; i++) {
        L[i] = level[Euler[i]];

        // If node is not visited before
        if (vis[Euler[i]] == 0) {
            // Add to first occurrence
            H[Euler[i]] = i;

            // Mark it visited
            vis[Euler[i]] = 1;
        }
    }
}

// Stores values and positions
pair<int, int> seg[4 * MAX];

// Utility function to find minimum of
// pair type values
pair<int, int> min(pair<int, int> a,
                   pair<int, int> b)
{
    if (a.first <= b.first)
        return a;
    else
        return b;
}

// Utility function to build segment tree
pair<int, int> buildSegTree(int low, int high, int pos)
{
    if (low == high) {
        seg[pos].first = L[low];
        seg[pos].second = low;
        return seg[pos];
    }
    int mid = low + (high - low) / 2;
    buildSegTree(low, mid, 2 * pos);
    buildSegTree(mid + 1, high, 2 * pos + 1);

    seg[pos] = min(seg[2 * pos], seg[2 * pos + 1]);
}

// Utility function to find LCA
pair<int, int> LCA(int qlow, int qhigh, int low,
                   int high, int pos)
{
    if (qlow <= low && qhigh >= high)
        return seg[pos];

    if (qlow > high || qhigh < low)
        return { INT_MAX, 0 };

    int mid = low + (high - low) / 2;

    return min(LCA(qlow, qhigh, low, mid, 2 * pos),
               LCA(qlow, qhigh, mid + 1, high, 2 * pos + 1));
}

// Function to return distance between
// two nodes n1 and n2
int findDistance(int n1, int n2, int size)
{
    // Maintain original Values
    int prevn1 = n1, prevn2 = n2;

    // Get First Occurrence of n1
    n1 = H[n1];

    // Get First Occurrence of n2
    n2 = H[n2];

    // Swap if low > high
    if (n2 < n1)
        swap(n1, n2);

    // Get position of minimum value
    int lca = LCA(n1, n2, 1, size, 1).second;

    // Extract value out of Euler tour
    lca = Euler[lca];

    // return calculated distance
    return level[prevn1] + level[prevn2] - 2 * level[lca];
}

void preProcessing(Node* root, int N)
{
    // Build Tree
    eulerTree(root);

    // Store Levels
    FindLevels(root);

    // Find L and H array
    preprocessEuler(2 * N - 1);

    // Build segment Tree
    buildSegTree(1, 2 * N - 1, 1);
}

/* Driver function to test above functions */
int main()
{
    int N = 8; // Number of nodes

    /* Constructing tree given in the above figure */
    Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->left = newNode(6);
    root->right->right = newNode(7);
    root->right->left->right = newNode(8);

    // Function to do all preprocessing
    preProcessing(root, N);

    cout << "Dist(4, 5) = " << 
      findDistance(4, 5, 2 * N - 1) << "\n";
    cout << "Dist(4, 6) = " << 
      findDistance(4, 6, 2 * N - 1) << "\n";
    cout << "Dist(3, 4) = " << 
      findDistance(3, 4, 2 * N - 1) << "\n";
    cout << "Dist(2, 4) = " << 
      findDistance(2, 4, 2 * N - 1) << "\n";
    cout << "Dist(8, 5) = " << 
      findDistance(8, 5, 2 * N - 1) << "\n";

    return 0;
}

```

## Java

```java

// Java program to find distance between 
// two nodes for multiple queries
import java.io.*;
import java.util.*;

class GFG
{
    static int MAX = 100001;

    /* A tree node structure */
    static class Node 
    {
        int data;
        Node left, right;

        Node(int data) 
        {
            this.data = data;
            this.left = this.right = null;
        }
    }

    static class Pair<T, V> 
    {
        T first;
        V second;

        Pair() {
        }

        Pair(T first, V second)
        {
            this.first = first;
            this.second = second;
        }
    }

    // Array to store level of each node
    static int[] level = new int[MAX];

    // Utility Function to store level of all nodes
    static void findLevels(Node root)
    {
        if (root == null)
            return;

        // queue to hold tree node with level
        Queue<Pair<Node, Integer>> q = new LinkedList<>();

        // let root node be at level 0
        q.add(new Pair<Node, Integer>(root, 0));

        Pair<Node, Integer> p = new Pair<Node, Integer>();

        // Do level Order Traversal of tree
        while (!q.isEmpty()) 
        {
            p = q.poll();

            // Node p.first is on level p.second
            level[p.first.data] = p.second;

            // If left child exits, put it in queue
            // with current_level +1
            if (p.first.left != null)
                q.add(new Pair<Node, 
                      Integer>(p.first.left, 
                                  p.second + 1));

            // If right child exists, put it in queue
            // with current_level +1
            if (p.first.right != null)
                q.add(new Pair<Node, 
                      Integer>(p.first.right,
                                p.second + 1));
        }
    }

    // Stores Euler Tour
    static int[] Euler = new int[MAX];

    // index in Euler array
    static int idx = 0;

    // Find Euler Tour
    static void eulerTree(Node root)
    {

        // store current node's data
        Euler[++idx] = root.data;

        // If left node exists
        if (root.left != null)
        {

            // traverse left subtree
            eulerTree(root.left);

            // store parent node's data
            Euler[++idx] = root.data;
        }

        // If right node exists
        if (root.right != null) 
        {
            // traverse right subtree
            eulerTree(root.right);

            // store parent node's data
            Euler[++idx] = root.data;
        }
    }

    // checks for visited nodes
    static int[] vis = new int[MAX];

    // Stores level of Euler Tour
    static int[] L = new int[MAX];

    // Stores indices of first occurrence
    // of nodes in Euler tour
    static int[] H = new int[MAX];

    // Preprocessing Euler Tour for finding LCA
    static void preprocessEuler(int size)
    {
        for (int i = 1; i <= size; i++)
        {
            L[i] = level[Euler[i]];

            // If node is not visited before
            if (vis[Euler[i]] == 0)
            {

                // Add to first occurrence
                H[Euler[i]] = i;

                // Mark it visited
                vis[Euler[i]] = 1;
            }
        }
    }

    // Stores values and positions
    @SuppressWarnings("unchecked")
    static Pair<Integer, Integer>[] seg = 
    (Pair<Integer, Integer>[]) new Pair[4 * MAX];

    // Utility function to find minimum of
    // pair type values
    static Pair<Integer, Integer> 
                       min(Pair<Integer, Integer> a, 
                           Pair<Integer, Integer> b)
    {
        if (a.first <= b.first)
            return a;
        return b;
    }

    // Utility function to build segment tree
    static Pair<Integer, Integer> buildSegTree(int low, 
                                    int high, int pos) 
    {
        if (low == high)
        {
            seg[pos].first = L[low];
            seg[pos].second = low;
            return seg[pos];
        }
        int mid = low + (high - low) / 2;
        buildSegTree(low, mid, 2 * pos);
        buildSegTree(mid + 1, high, 2 * pos + 1);

        seg[pos] = min(seg[2 * pos], seg[2 * pos + 1]);

        return seg[pos];
    }

    // Utility function to find LCA
    static Pair<Integer, Integer> LCA(int qlow, int qhigh, 
                                int low, int high, int pos)
    {
        if (qlow <= low && qhigh >= high)
            return seg[pos];

        if (qlow > high || qhigh < low)
            return new Pair<Integer, Integer>
                                  (Integer.MAX_VALUE, 0);

        int mid = low + (high - low) / 2;

        return min(LCA(qlow, qhigh, low, mid, 2 * pos), 
           LCA(qlow, qhigh, mid + 1, high, 2 * pos + 1));
    }

    // Function to return distance between
    // two nodes n1 and n2
    static int findDistance(int n1, int n2, int size)
    {

        // Maintain original Values
        int prevn1 = n1, prevn2 = n2;

        // Get First Occurrence of n1
        n1 = H[n1];

        // Get First Occurrence of n2
        n2 = H[n2];

        // Swap if low > high
        if (n2 < n1) 
        {
            int temp = n1;
            n1 = n2;
            n2 = temp;
        }

        // Get position of minimum value
        int lca = LCA(n1, n2, 1, size, 1).second;

        // Extract value out of Euler tour
        lca = Euler[lca];

        // return calculated distance
        return level[prevn1] + level[prevn2] - 
                                  2 * level[lca];
    }

    static void preProcessing(Node root, int N) 
    {
        for (int i = 0; i < 4 * MAX; i++) 
        {
            seg[i] = new Pair<>();
        }

        // Build Tree
        eulerTree(root);

        // Store Levels
        findLevels(root);

        // Find L and H array
        preprocessEuler(2 * N - 1);

        // Build segment Tree
        buildSegTree(1, 2 * N - 1, 1);
    }

    // Driver Code
    public static void main(String[] args) 
    {

        // Number of nodes
        int N = 8;

        /* Constructing tree given in the above figure */
        Node root = new Node(1);
        root.left = new Node(2);
        root.right = new Node(3);
        root.left.left = new Node(4);
        root.left.right = new Node(5);
        root.right.left = new Node(6);
        root.right.right = new Node(7);
        root.right.left.right = new Node(8);

        // Function to do all preprocessing
        preProcessing(root, N);

        System.out.println("Dist(4, 5) = " + 
                        findDistance(4, 5, 2 * N - 1));
        System.out.println("Dist(4, 6) = " + 
                        findDistance(4, 6, 2 * N - 1));
        System.out.println("Dist(3, 4) = " + 
                        findDistance(3, 4, 2 * N - 1));
        System.out.println("Dist(2, 4) = " + 
                        findDistance(2, 4, 2 * N - 1));
        System.out.println("Dist(8, 5) = " + 
                        findDistance(8, 5, 2 * N - 1));
    }
}

// This code is contributed by
// sanjeev2552

```

## Python3

```py

# Python3 program to find distance between

> 原文：[https://www.geeksforgeeks.org/queries-find-distance-two-nodes-binary-tree-ologn-method/](https://www.geeksforgeeks.org/queries-find-distance-two-nodes-binary-tree-ologn-method/)
# two nodes for multiple queries

> 原文：[https://www.geeksforgeeks.org/queries-find-distance-two-nodes-binary-tree-ologn-method/](https://www.geeksforgeeks.org/queries-find-distance-two-nodes-binary-tree-ologn-method/)

from collections import deque
from sys import maxsize as INT_MAX

MAX = 100001

# A tree node structure

> 原文：[https://www.geeksforgeeks.org/queries-find-distance-two-nodes-binary-tree-ologn-method/](https://www.geeksforgeeks.org/queries-find-distance-two-nodes-binary-tree-ologn-method/)
class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Array to store level of each node

> 原文：[https://www.geeksforgeeks.org/queries-find-distance-two-nodes-binary-tree-ologn-method/](https://www.geeksforgeeks.org/queries-find-distance-two-nodes-binary-tree-ologn-method/)
level = [0] * MAX

# Utility Function to store level of all nodes

> 原文：[https://www.geeksforgeeks.org/queries-find-distance-two-nodes-binary-tree-ologn-method/](https://www.geeksforgeeks.org/queries-find-distance-two-nodes-binary-tree-ologn-method/)
def findLevels(root: Node):
    global level

    if root is None:
        return

    # queue to hold tree node with level
    q = deque()

    # let root node be at level 0
    q.append((root, 0))

    # Do level Order Traversal of tree
    while q:
        p = q[0]
        q.popleft()

        # Node p.first is on level p.second
        level[p[0].data] = p[1]

        # If left child exits, put it in queue
        # with current_level +1
        if p[0].left:
            q.append((p[0].left, p[1] + 1))

        # If right child exists, put it in queue
        # with current_level +1
        if p[0].right:
            q.append((p[0].right, p[1] + 1))

# Stores Euler Tour

> 原文：[https://www.geeksforgeeks.org/queries-find-distance-two-nodes-binary-tree-ologn-method/](https://www.geeksforgeeks.org/queries-find-distance-two-nodes-binary-tree-ologn-method/)
Euler = [0] * MAX

# index in Euler array

> 原文：[https://www.geeksforgeeks.org/queries-find-distance-two-nodes-binary-tree-ologn-method/](https://www.geeksforgeeks.org/queries-find-distance-two-nodes-binary-tree-ologn-method/)
idx = 0

# Find Euler Tour

> 原文：[https://www.geeksforgeeks.org/queries-find-distance-two-nodes-binary-tree-ologn-method/](https://www.geeksforgeeks.org/queries-find-distance-two-nodes-binary-tree-ologn-method/)
def eulerTree(root: Node):
    global Euler, idx
    idx += 1

    # store current node's data
    Euler[idx] = root.data

    # If left node exists
    if root.left:

        # traverse left subtree
        eulerTree(root.left)
        idx += 1

        # store parent node's data
        Euler[idx] = root.data

    # If right node exists
    if root.right:

        # traverse right subtree
        eulerTree(root.right)
        idx += 1

        # store parent node's data
        Euler[idx] = root.data

# checks for visited nodes

> 原文：[https://www.geeksforgeeks.org/queries-find-distance-two-nodes-binary-tree-ologn-method/](https://www.geeksforgeeks.org/queries-find-distance-two-nodes-binary-tree-ologn-method/)
vis = [0] * MAX

# Stores level of Euler Tour

> 原文：[https://www.geeksforgeeks.org/queries-find-distance-two-nodes-binary-tree-ologn-method/](https://www.geeksforgeeks.org/queries-find-distance-two-nodes-binary-tree-ologn-method/)
L = [0] * MAX

# Stores indices of the first occurrence

> 原文：[https://www.geeksforgeeks.org/queries-find-distance-two-nodes-binary-tree-ologn-method/](https://www.geeksforgeeks.org/queries-find-distance-two-nodes-binary-tree-ologn-method/)
# of nodes in Euler tour

> 原文：[https://www.geeksforgeeks.org/queries-find-distance-two-nodes-binary-tree-ologn-method/](https://www.geeksforgeeks.org/queries-find-distance-two-nodes-binary-tree-ologn-method/)
H = [0] * MAX

# Preprocessing Euler Tour for finding LCA

> 原文：[https://www.geeksforgeeks.org/queries-find-distance-two-nodes-binary-tree-ologn-method/](https://www.geeksforgeeks.org/queries-find-distance-two-nodes-binary-tree-ologn-method/)
def preprocessEuler(size: int):
    global L, H, vis
    for i in range(1, size + 1):
        L[i] = level[Euler[i]]

        # If node is not visited before
        if vis[Euler[i]] == 0:

            # Add to first occurrence
            H[Euler[i]] = i

            # Mark it visited
            vis[Euler[i]] = 1

# Stores values and positions

> 原文：[https://www.geeksforgeeks.org/queries-find-distance-two-nodes-binary-tree-ologn-method/](https://www.geeksforgeeks.org/queries-find-distance-two-nodes-binary-tree-ologn-method/)
seg = [0] * (4 * MAX)
for i in range(4 * MAX):
    seg[i] = [0, 0]

# Utility function to find minimum of

> 原文：[https://www.geeksforgeeks.org/queries-find-distance-two-nodes-binary-tree-ologn-method/](https://www.geeksforgeeks.org/queries-find-distance-two-nodes-binary-tree-ologn-method/)
# pair type values

> 原文：[https://www.geeksforgeeks.org/queries-find-distance-two-nodes-binary-tree-ologn-method/](https://www.geeksforgeeks.org/queries-find-distance-two-nodes-binary-tree-ologn-method/)
def minPair(a: list, b: list) -> list:
    if a[0] <= b[0]:
        return a
    else:
        return b

# Utility function to build segment tree

> 原文：[https://www.geeksforgeeks.org/queries-find-distance-two-nodes-binary-tree-ologn-method/](https://www.geeksforgeeks.org/queries-find-distance-two-nodes-binary-tree-ologn-method/)
def buildSegTree(low: int, high: int, 
                       pos: int) -> list:
    if low == high:
        seg[pos][0] = L[low]
        seg[pos][1] = low
        return seg[pos]

    mid = low + (high - low) // 2
    buildSegTree(low, mid, 2 * pos)
    buildSegTree(mid + 1, high, 2 * pos + 1)

    seg[pos] = min(seg[2 * pos], seg[2 * pos + 1])

# Utility function to find LCA

> 原文：[https://www.geeksforgeeks.org/queries-find-distance-two-nodes-binary-tree-ologn-method/](https://www.geeksforgeeks.org/queries-find-distance-two-nodes-binary-tree-ologn-method/)
def LCA(qlow: int, qhigh: int, low: int, 
                     high: int, pos: int) -> list:
    if qlow <= low and qhigh >= high:
        return seg[pos]

    if qlow > high or qhigh < low:
        return [INT_MAX, 0]

    mid = low + (high - low) // 2

    return minPair(LCA(qlow, qhigh, low, mid, 2 * pos),
          LCA(qlow, qhigh, mid + 1, high, 2 * pos + 1))

# Function to return distance between

> 原文：[https://www.geeksforgeeks.org/queries-find-distance-two-nodes-binary-tree-ologn-method/](https://www.geeksforgeeks.org/queries-find-distance-two-nodes-binary-tree-ologn-method/)
# two nodes n1 and n2

> 原文：[https://www.geeksforgeeks.org/queries-find-distance-two-nodes-binary-tree-ologn-method/](https://www.geeksforgeeks.org/queries-find-distance-two-nodes-binary-tree-ologn-method/)
def findDistance(n1: int, n2: int, size: int) -> int:

    # Maintain original Values
    prevn1 = n1
    prevn2 = n2

    # Get First Occurrence of n1
    n1 = H[n1]

    # Get First Occurrence of n2
    n2 = H[n2]

    # Swap if low>high
    if n2 < n1:
        n1, n2 = n2, n1

    # Get position of minimum value
    lca = LCA(n1, n2, 1, size, 1)[1]

    # Extract value out of Euler tour
    lca = Euler[lca]

    # return calculated distance
    return level[prevn1] + level[prevn2] -
                                2 * level[lca]

def preProcessing(root: Node, N: int):

    # Build Tree
    eulerTree(root)

    # Store Levels
    findLevels(root)

    # Find L and H array
    preprocessEuler(2 * N - 1)

    # Build sparse table
    buildSegTree(1, 2 * N - 1, 1)

# Driver Code

> 原文：[https://www.geeksforgeeks.org/queries-find-distance-two-nodes-binary-tree-ologn-method/](https://www.geeksforgeeks.org/queries-find-distance-two-nodes-binary-tree-ologn-method/)
if __name__ == "__main__":

    # Number of nodes
    N = 8

    # Constructing tree given in the above figure
    root = Node(1)
    root.left = Node(2)
    root.right = Node(3)
    root.left.left = Node(4)
    root.left.right = Node(5)
    root.right.left = Node(6)
    root.right.right = Node(7)
    root.right.left.right = Node(8)

    # Function to do all preprocessing
    preProcessing(root, N)

    print("Dist(4, 5) =", 
          findDistance(4, 5, 2 * N - 1))
    print("Dist(4, 6) =", 
          findDistance(4, 6, 2 * N - 1))
    print("Dist(3, 4) =", 
          findDistance(3, 4, 2 * N - 1))
    print("Dist(2, 4) =", 
          findDistance(2, 4, 2 * N - 1))
    print("Dist(8, 5) =", 
          findDistance(8, 5, 2 * N - 1))

# This code is contributed by

> 原文：[https://www.geeksforgeeks.org/queries-find-distance-two-nodes-binary-tree-ologn-method/](https://www.geeksforgeeks.org/queries-find-distance-two-nodes-binary-tree-ologn-method/)
# sanjeev2552

> 原文：[https://www.geeksforgeeks.org/queries-find-distance-two-nodes-binary-tree-ologn-method/](https://www.geeksforgeeks.org/queries-find-distance-two-nodes-binary-tree-ologn-method/)

```

## C#

```cs

// C# program to find distance between 
// two nodes for multiple queries
using System;
using System.Collections.Generic;

class GFG
{
    static int MAX = 100001;

    /* A tree node structure */
    public class Node 
    {
        public int data;
        public Node left, right;

        public Node(int data) 
        {
            this.data = data;
            this.left = this.right = null;
        }
    }

    class Pair<T, V> 
    {
        public T first;
        public V second;

        public Pair() {
        }

        public Pair(T first, V second)
        {
            this.first = first;
            this.second = second;
        }
    }

    // Array to store level of each node
    static int[] level = new int[MAX];

    // Utility Function to store level of all nodes
    static void findLevels(Node root)
    {
        if (root == null)
            return;

        // queue to hold tree node with level
        List<Pair<Node, int>> q = 
        new List<Pair<Node, int>>();

        // let root node be at level 0
        q.Add(new Pair<Node, int>(root, 0));

        Pair<Node, int> p = new Pair<Node, int>();

        // Do level Order Traversal of tree
        while (q.Count != 0) 
        {
            p = q[0];
            q.RemoveAt(0);

            // Node p.first is on level p.second
            level[p.first.data] = p.second;

            // If left child exits, put it in queue
            // with current_level +1
            if (p.first.left != null)
                q.Add(new Pair<Node, int>
                      (p.first.left, p.second + 1));

            // If right child exists, put it in queue
            // with current_level +1
            if (p.first.right != null)
                q.Add(new Pair<Node, int>
                      (p.first.right, p.second + 1));
        }
    }

    // Stores Euler Tour
    static int[] Euler = new int[MAX];

    // index in Euler array
    static int idx = 0;

    // Find Euler Tour
    static void eulerTree(Node root)
    {

        // store current node's data
        Euler[++idx] = root.data;

        // If left node exists
        if (root.left != null)
        {

            // traverse left subtree
            eulerTree(root.left);

            // store parent node's data
            Euler[++idx] = root.data;
        }

        // If right node exists
        if (root.right != null) 
        {
            // traverse right subtree
            eulerTree(root.right);

            // store parent node's data
            Euler[++idx] = root.data;
        }
    }

    // checks for visited nodes
    static int[] vis = new int[MAX];

    // Stores level of Euler Tour
    static int[] L = new int[MAX];

    // Stores indices of first occurrence
    // of nodes in Euler tour
    static int[] H = new int[MAX];

    // Preprocessing Euler Tour for finding LCA
    static void preprocessEuler(int size)
    {
        for (int i = 1; i <= size; i++)
        {
            L[i] = level[Euler[i]];

            // If node is not visited before
            if (vis[Euler[i]] == 0)
            {

                // Add to first occurrence
                H[Euler[i]] = i;

                // Mark it visited
                vis[Euler[i]] = 1;
            }
        }
    }

    // Stores values and positions
    static Pair<int, int>[] seg = new
                          Pair<int, int>[4 * MAX];

    // Utility function to find minimum of
    // pair type values
    static Pair<int, int> min(Pair<int, int> a, 
                                    Pair<int, int> b)
    {
        if (a.first <= b.first)
            return a;
        return b;
    }

    // Utility function to build segment tree
    static Pair<int, int> buildSegTree(int low, 
                                    int high, int pos) 
    {
        if (low == high)
        {
            seg[pos].first = L[low];
            seg[pos].second = low;
            return seg[pos];
        }
        int mid = low + (high - low) / 2;
        buildSegTree(low, mid, 2 * pos);
        buildSegTree(mid + 1, high, 2 * pos + 1);

        seg[pos] = min(seg[2 * pos], seg[2 * pos + 1]);

        return seg[pos];
    }

    // Utility function to find LCA
    static Pair<int, int> LCA(int qlow, int qhigh, 
                    int low, int high, int pos)
    {
        if (qlow <= low && qhigh >= high)
            return seg[pos];

        if (qlow > high || qhigh < low)
            return new Pair<int, int>(int.MaxValue, 0);

        int mid = low + (high - low) / 2;

        return min(LCA(qlow, qhigh, low, mid, 2 * pos), 
                LCA(qlow, qhigh, mid + 1, 
                                 high, 2 * pos + 1));
    }

    // Function to return distance between
    // two nodes n1 and n2
    static int findDistance(int n1, int n2, int size)
    {

        // Maintain original Values
        int prevn1 = n1, prevn2 = n2;

        // Get First Occurrence of n1
        n1 = H[n1];

        // Get First Occurrence of n2
        n2 = H[n2];

        // Swap if low > high
        if (n2 < n1) 
        {
            int temp = n1;
            n1 = n2;
            n2 = temp;
        }

        // Get position of minimum value
        int lca = LCA(n1, n2, 1, size, 1).second;

        // Extract value out of Euler tour
        lca = Euler[lca];

        // return calculated distance
        return level[prevn1] + level[prevn2] - 
                                2 * level[lca];
    }

    static void preProcessing(Node root, int N) 
    {
        for (int i = 0; i < 4 * MAX; i++) 
        {
            seg[i] = new Pair<int,int>();
        }

        // Build Tree
        eulerTree(root);

        // Store Levels
        findLevels(root);

        // Find L and H array
        preprocessEuler(2 * N - 1);

        // Build segment Tree
        buildSegTree(1, 2 * N - 1, 1);
    }

    // Driver Code
    public static void Main(String[] args) 
    {

        // Number of nodes
        int N = 8;

        /* Constructing tree given in the above figure */
        Node root = new Node(1);
        root.left = new Node(2);
        root.right = new Node(3);
        root.left.left = new Node(4);
        root.left.right = new Node(5);
        root.right.left = new Node(6);
        root.right.right = new Node(7);
        root.right.left.right = new Node(8);

        // Function to do all preprocessing
        preProcessing(root, N);

        Console.WriteLine("Dist(4, 5) = " + 
                       findDistance(4, 5, 2 * N - 1));
        Console.WriteLine("Dist(4, 6) = " + 
                       findDistance(4, 6, 2 * N - 1));
        Console.WriteLine("Dist(3, 4) = " + 
                       findDistance(3, 4, 2 * N - 1));
        Console.WriteLine("Dist(2, 4) = " + 
                       findDistance(2, 4, 2 * N - 1));
        Console.WriteLine("Dist(8, 5) = " + 
                       findDistance(8, 5, 2 * N - 1));
    }
}

// This code is contributed by Rajput-Ji

```

**输出**：

```
Dist(4, 5) = 2
Dist(4, 6) = 4
Dist(3, 4) = 3
Dist(2, 4) = 1
Dist(8, 5) = 5

```

**时间复杂度**：O（Log N）

**空间复杂度**：O（N）

[查询以查找二叉树的两个节点之间的距离– O（ 1）方法](https://www.geeksforgeeks.org/queries-find-distance-two-nodes-binary-tree/)

[![competitive-programming-img](img/5211864e7e7a28eeeb039fa5d6073a24.png)](https://practice.geeksforgeeks.org/courses/competitive-programming-live?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_cp)

* * *

* * *



