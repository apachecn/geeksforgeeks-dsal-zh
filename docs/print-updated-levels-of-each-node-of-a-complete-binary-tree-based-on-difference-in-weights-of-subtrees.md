# 根据子树权重的差异打印完整二叉树每个节点的更新级别

> 原文:[https://www . geesforgeks . org/print-updated-基于子树权重差的完整二叉树每个节点的级别/](https://www.geeksforgeeks.org/print-updated-levels-of-each-node-of-a-complete-binary-tree-based-on-difference-in-weights-of-subtrees/)

给定一个完整的二叉树，其 **N** **级**编号为**【0，(N–1)】**从根到最低级别按递减顺序排列，其**权重**编号为**【1，2】<sup>N</sup>–1】**从根到最后一个叶节点按递增顺序排列，每个节点的任务是根据以下条件调整其左右子树中存在的所有节点的级别值:

*   通过权重的不同来增加较轻子树的所有节点的级别。
*   通过权重的不同来降低较重子树的所有节点的级别。

**示例:**

> **输入:**
> 
> ```
>           1
>         /   \
>        2     3
> ```
> 
> **输出:** 0 0 -2
> **说明:**
> 节点{1，2，3}的初始级别分别为{0，-1，-1}。
> 根节点保持不变。
> 左子树的权重为 2，右子树的权重为 3。
> 所以，左边的子树上升(3–2)= 1 级到 0 级。
> 右边的子树下降 1 级到-2。
> **输入:**
> 
> ```
>              1
>            /   \
>           2     3
>          / \   / \
>         4   5 6   7
> ```
> 
> **输出:** 0 4 -6 4 2 -6 -8
> **说明:**
> 节点{1，2，3，4，5，6，7}的初始级别分别为{0，-1，-1，-2，-2，-2，-2}。
> 根节点保持不变。
> 左子树{2，4，5}的权重为 11。
> 右子树{3，6，7}的权重为 16。
> 因此，左子树中的所有节点向上移动 5，而右子树中的节点向下移动 5。
> 因此，每个节点的新级别是:
> 节点 2: -1 + 5 = 4
> 节点 3:-1–5 =-6
> 节点 4，5: -2 + 5 = 3
> 节点 6，7:-2–5 =-7
> 现在，节点 4，5 进一步基于它们的权重差(5 -4 ) = 1。
> 节点 4: 3 + 1 = 4
> 节点 5:3–1 = 2
> 同样，节点 6、7 也得到调整。
> 节点 6: -7 + 1 = -6
> 节点 7:-7–1 =-8
> 因此，所有节点的最终调整级别为 0 4 -6 4 2 -6 -8。

**方法:**为了解决这个问题，我们为每个节点计算左 **(w_left)** 和右 **(w_right)** [子树](https://www.geeksforgeeks.org/sub-tree-nodes-tree-using-dfs/)的权重，并存储它们的差值 **K** 。一旦计算出来，我们递归地将其较轻子树的所有节点的**级**的值增加 **K** ，并将其较重子树的值从它们各自的当前值减少 **K** 。一旦对所有节点进行了计算，我们将显示每个节点的**级别**的最终值。
以下代码是上述方法的实现:

## C++

```
// C++ Program to print updated levels
// of each node of a Complete Binary Tree
// based on difference in weights of subtrees

#include <bits/stdc++.h>
using namespace std;

// Node for the given binary tree
struct node {

    int weight;

    // stores the weight of node
    int level;

    // stores the level of node
    struct node* left;
    struct node* right;

    node(int w, int l)
    {
        this->weight = w;
        this->level = l;
        left = right = NULL;
    }
};

// Utility function to insert a node
// in a tree rooted at root
struct node* insert(struct node* root,
 int n_weight,
int n_level, queue<node*>& q)
{

    struct node* n
= new node(n_weight, n_level);

    // if the tree is empty till now
    // make node n the root
    if (root == NULL)
        root = n;

    // If the frontmost node of
    // queue has no left child
    // make node n its left child
    // the frontmost node still
    // remains in the queue because
    // its right child is null yet
    else if (q.front()->left == NULL) {
        q.front()->left = n;
    }

    // Make node n the right child of
    // the frontmost node and remove
    // the front node from queue
    else {
        q.front()->right = n;
        q.pop();
    }
    // push the node n into queue
    q.push(n);

    return root;
}

// Function to create a complete binary tree
struct node* createTree(vector<int> weights,
vector<int> levels)
{

    // initialise the root node of tree
    struct node* root = NULL;

    // initialise a queue of nodes
    queue<node*> q;

    int n = weights.size();
    for (int i = 0; i < n; i++) {

        /*
        keep inserting nodes with weight values
        from the weights vector and level values
        from the levels vector
        */
        root = insert(root, weights[i],
        levels[i], q);
    }
    return root;
}

// Function to print final levels of nodes
void printNodeLevels(struct node* root)
{

    if (root == NULL)
        return;

    queue<node*> q;
    q.push(root);

    while (!q.empty()) {

        cout << q.front()->level << " ";

        if (q.front()->left != NULL)
            q.push(q.front()->left);
        if (q.front()->right != NULL)
            q.push(q.front()->right);
        q.pop();
    }
    cout << endl;
}

// Function to find the weight of subtree
int findWeight(struct node* root)
{
    // If the root node is null
    // then weight of subtree will be 0
    if (root == NULL)
        return 0;

    return root->weight +
        findWeight(root->left)
        + findWeight(root->right);
}

// Function to compute new level
// of the nodes based on the
// difference of weight K
void changeLevels(struct node* root, int k)
{

    if (root == NULL)
        return;

    // Change the level of root node
    root->level = root->level + k;

    // Recursively change the level of
    // left and right subtree
    changeLevels(root->left, k);
    changeLevels(root->right, k);
}

// Function to calculate weight of
// the left and the right subtrees and
// adjust levels based on their difference
void adjustLevels(struct node* root)
{

    // No adjustment required
    // when root is null
    if (root == NULL)
        return;

    // Find weights of left
    // and right subtrees
    int w_left = findWeight(root->left);
    int w_right = findWeight(root->right);

    // find the difference between the
    // weights of left and right subtree
    int w_diff = w_left - w_right;

    // Change the levels of nodes
    // according to weight difference at root
    changeLevels(root->left, -w_diff);
    changeLevels(root->right, w_diff);

    // Recursively adjust the levels
    // for left and right subtrees
    adjustLevels(root->left);
    adjustLevels(root->right);
}

// Driver code
int main()
{
    // Number of levels
    int N = 3;

    // Number of nodes
    int nodes = pow(2, N) - 1;

    vector<int> weights;
    // Vector to store weights of tree nodes
    for (int i = 1; i <= nodes; i++) {
        weights.push_back(i);
    }

    vector<int> levels;
    // Vector to store levels of every nodes
    for (int i = 0; i < N; i++) {

        // 2^i nodes are present at ith level
        for (int j = 0; j < pow(2, i); j++) {

            // value of level becomes negative
            // while going down the root
            levels.push_back(-1 * i);
        }
    }

    // Create tree with the
// given weights and levels
    struct node* root
= createTree(weights, levels);

    // Adjust the levels
    adjustLevels(root);

    // Display the final levels
    printNodeLevels(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to print updated levels
// of each node of a Complete Binary Tree
// based on difference in weights of subtrees
import java.util.ArrayList;
import java.util.LinkedList;
import java.util.Queue;

class GFG {

    // Node for the given binary tree
    static class node {

        int weight;

        // stores the weight of node
        int level;

        // stores the level of node
        node left;
        node right;
        public node(int w, int l)
        {
            this.weight = w;
            this.level = l;
            left = right = null;
        }
    }

    // Utility function to insert a node
    // in a tree rooted at root
    static node insert(node root, int n_weight, int n_level, Queue<node> q)
    {
        node n = new node(n_weight, n_level);

        // if the tree is empty till now
        // make node n the root
        if (root == null)
            root = n;

        // If the frontmost node of
        // queue has no left child
        // make node n its left child
        // the frontmost node still
        // remains in the queue because
        // its right child isnull yet
        else if (q.peek().left == null)
        {
            q.peek().left = n;
        }

        // Make node n the right child of
        // the frontmost node and remove
        // the front node from queue
        else
        {
            q.peek().right = n;
            q.poll();
        }

        // push the node n into queue
        q.add(n);

        return root;
    }

    // Function to create a complete binary tree
    static node createTree(ArrayList<Integer> weights,
                           ArrayList<Integer> levels)
    {

        // initialise the root node of tree
        node root = null;

        // initialise a queue of nodes
        Queue<node> q = new LinkedList<>();
        int n = weights.size();
        for (int i = 0; i < n; i++)
        {

            /*
             * keep inserting nodes with weight values
             * from the weights vector and level
             * values from the levels vector
             */
            root = insert(root, weights.get(i), levels.get(i), q);
        }
        return root;
    }

    // Function to print final levels of nodes
    static void printNodeLevels(node root)
    {

        if (root == null)
            return;

        Queue<node> q = new LinkedList<>();
        q.add(root);

        while (!q.isEmpty()) {
            System.out.print(q.peek().level + " ");

            if (q.peek().left != null)
                q.add(q.peek().left);
            if (q.peek().right != null)
                q.add(q.peek().right);
            q.poll();
        }
        System.out.println();
    }

    // Function to find the weight of subtree
    static int findWeight(node root)
    {

        // If the root node isnull
        // then weight of subtree will be 0
        if (root == null)
            return 0;

        return root.weight + findWeight(root.left) + findWeight(root.right);
    }

    // Function to compute new level
    // of the nodes based on the
    // difference of weight K
    static void changeLevels(node root, int k)
    {
        if (root == null)
            return;

        // Change the level of root node
        root.level = root.level + k;

        // Recursively change the level of
        // left and right subtree
        changeLevels(root.left, k);
        changeLevels(root.right, k);
    }

    // Function to calculate weight of
    // the left and the right subtrees and
    // adjust levels based on their difference
    static void adjustLevels(node root)
    {

        // No adjustment required
        // when root isnull
        if (root == null)
            return;

        // Find weights of left
        // and right subtrees
        int w_left = findWeight(root.left);
        int w_right = findWeight(root.right);

        // find the difference between the
        // weights of left and right subtree
        int w_diff = w_left - w_right;

        // Change the levels of nodes
        // according to weight difference at root
        changeLevels(root.left, -w_diff);
        changeLevels(root.right, w_diff);

        // Recursively adjust the levels
        // for left and right subtrees
        adjustLevels(root.left);
        adjustLevels(root.right);
    }

    // Driver code
    public static void main(String[] args)
    {

        // Number of levels
        int N = 3;

        // Number of nodes
        int nodes = (int) Math.pow(2, N) - 1;

        // Vector to store weights of tree nodes
        ArrayList<Integer> weights = new ArrayList<>();
        for (int i = 1; i <= nodes; i++) {
            weights.add(i);
        }

        // Vector to store levels of every nodes
        ArrayList<Integer> levels = new ArrayList<>();
        for (int i = 0; i < N; i++) {

            // 2^i nodes are present at ith level
            for (int j = 0; j < (int) Math.pow(2, i); j++) {

                // value of level becomes negative
                // while going down the root
                levels.add(-1 * i);
            }
        }

        // Create tree with the
        // given weights and levels
        node root = createTree(weights, levels);

        // Adjust the levels
        adjustLevels(root);

        // Display the final levels
        printNodeLevels(root);

    }
}

// This code is contributed by sanjeev2552
```

## 蟒蛇 3

```
# Python3 Program to print
# updated levels of each
# node of a Complete Binary
# Tree based on difference
# in weights of subtrees
import math

# Node for the given binary
# tree
class node:

    def __init__(self, w, l):

        self.weight = w
        self.level = l
        self.left = None
        self.right = None

# Utility function to insert
# a node in a tree rooted at
# root
def insert(root, n_weight,
           n_level, q):

    n = node(n_weight,
             n_level);

    # if the tree is empty
    # till now make node n
    # the root
    if (root == None):
        root = n;

    # If the frontmost node of
    # queue has no left child
    # make node n its left child
    # the frontmost node still
    # remains in the queue because
    # its right child is null yet
    elif (q[0].left == None):
        q[0].left = n;

    # Make node n the right
    # child of the frontmost
    # node and remove the
    # front node from queue
    else:
        q[0].right = n;
        q.pop(0);

    # push the node n
    # into queue
    q.append(n);

    return root;

# Function to create a
# complete binary tree
def createTree(weights,
               levels):

    # initialise the root
    # node of tree
    root = None;

    # initialise a queue
    # of nodes
    q = []

    n = len(weights)

    for i in range(n):
        '''
        keep inserting nodes with
        weight values from the weights
        vector and level values from
        the levels vector
        '''       
        root = insert(root, weights[i],
                      levels[i], q);

    return root;

# Function to print final
# levels of nodes
def printNodeLevels(root):

    if (root == None):
        return;

    q = []
    q.append(root);

    while (len(q) != 0):       
        print(q[0].level,
              end = ' ')
        if (q[0].left != None):
            q.append(q[0].left);
        if (q[0].right != None):
            q.append(q[0].right);
        q.pop(0);
    print()

# Function to find the weight
# of subtree
def findWeight(root):

    # If the root node is
    # null then weight of
    # subtree will be 0
    if (root == None):
        return 0;

    return (root.weight +
            findWeight(root.left) +
            findWeight(root.right));

# Function to compute new level
# of the nodes based on the
# difference of weight K
def changeLevels(root, k):

    if (root == None):
        return;

    # Change the level of
    # root node
    root.level = root.level + k;

    # Recursively change the
    # level of left and right
    # subtree
    changeLevels(root.left, k);
    changeLevels(root.right, k);

# Function to calculate weight
# of the left and the right
# subtrees and adjust levels
# based on their difference
def adjustLevels(root):

    # No adjustment required
    # when root is null
    if (root == None):
        return;

    # Find weights of left
    # and right subtrees
    w_left = findWeight(root.left);
    w_right = findWeight(root.right);

    # find the difference between
    # the weights of left and
    # right subtree
    w_diff = w_left - w_right;

    # Change the levels of nodes
    # according to weight difference
    # at root
    changeLevels(root.left,
                 -w_diff);
    changeLevels(root.right,
                 w_diff);

    # Recursively adjust the levels
    # for left and right subtrees
    adjustLevels(root.left);
    adjustLevels(root.right);

# Driver code
if __name__=="__main__":

    # Number of levels
    N = 3;

    # Number of nodes
    nodes = int(math.pow(2, N)) - 1;

    weights = []

    # Vector to store weights
    # of tree nodes
    for i in range(1, nodes + 1):   
        weights.append(i);   

    levels = []

    # Vector to store levels
    # of every nodes
    for i in range(N):

        # 2^i nodes are present
        # at ith level
        for j in range(pow(2, i)):

            # value of level becomes
            # negative while going
            # down the root
            levels.append(-1 * i);               

    # Create tree with the
    # given weights and levels
    root = createTree(weights,
                      levels);

    # Adjust the levels
    adjustLevels(root);

    # Display the final levels
    printNodeLevels(root);

# This code is contributed by Rutvik_56
```

## C#

```
// C# Program to print updated levels
// of each node of a Complete Binary Tree
// based on difference in weights of subtrees
using System;
using System.Collections.Generic;
class GFG {

    // Node for the given binary tree
    class node {

        public int weight, level;
        public node left, right;

        public node(int w, int l)
        {
            this.weight = w;
            this.level = l;
            left = right = null;
        }
    }

    // Utility function to insert a node
    // in a tree rooted at root
    static node insert(node root, int n_weight, int n_level, List<node> q)
    {
        node n = new node(n_weight, n_level);

        // if the tree is empty till now
        // make node n the root
        if (root == null)
            root = n;

        // If the frontmost node of
        // queue has no left child
        // make node n its left child
        // the frontmost node still
        // remains in the queue because
        // its right child isnull yet
        else if (q[0].left == null)
        {
            q[0].left = n;
        }

        // Make node n the right child of
        // the frontmost node and remove
        // the front node from queue
        else
        {
            q[0].right = n;
            q.RemoveAt(0);
        }

        // push the node n into queue
        q.Add(n);

        return root;
    }

    // Function to create a complete binary tree
    static node createTree(List<int> weights, List<int> levels)
    {

        // initialise the root node of tree
        node root = null;

        // initialise a queue of nodes
        List<node> q = new List<node>();
        int n = weights.Count;
        for (int i = 0; i < n; i++)
        {

            /*
             * keep inserting nodes with weight values
             * from the weights vector and level
             * values from the levels vector
             */
            root = insert(root, weights[i], levels[i], q);
        }
        return root;
    }

    // Function to print final levels of nodes
    static void printNodeLevels(node root)
    {

        if (root == null)
            return;

        List<node> q = new List<node>();
        q.Add(root);

        while (q.Count > 0) {
            Console.Write(q[0].level + " ");

            if (q[0].left != null)
                q.Add(q[0].left);
            if (q[0].right != null)
                q.Add(q[0].right);
            q.RemoveAt(0);
        }
        Console.WriteLine();
    }

    // Function to find the weight of subtree
    static int findWeight(node root)
    {

        // If the root node isnull
        // then weight of subtree will be 0
        if (root == null)
            return 0;

        return root.weight + findWeight(root.left) + findWeight(root.right);
    }

    // Function to compute new level
    // of the nodes based on the
    // difference of weight K
    static void changeLevels(node root, int k)
    {
        if (root == null)
            return;

        // Change the level of root node
        root.level = root.level + k;

        // Recursively change the level of
        // left and right subtree
        changeLevels(root.left, k);
        changeLevels(root.right, k);
    }

    // Function to calculate weight of
    // the left and the right subtrees and
    // adjust levels based on their difference
    static void adjustLevels(node root)
    {

        // No adjustment required
        // when root isnull
        if (root == null)
            return;

        // Find weights of left
        // and right subtrees
        int w_left = findWeight(root.left);
        int w_right = findWeight(root.right);

        // find the difference between the
        // weights of left and right subtree
        int w_diff = w_left - w_right;

        // Change the levels of nodes
        // according to weight difference at root
        changeLevels(root.left, -w_diff);
        changeLevels(root.right, w_diff);

        // Recursively adjust the levels
        // for left and right subtrees
        adjustLevels(root.left);
        adjustLevels(root.right);
    }

  static void Main() {
    // Number of levels
    int N = 3;

    // Number of nodes
    int nodes = (int) Math.Pow(2, N) - 1;

    // Vector to store weights of tree nodes
    List<int> weights = new List<int>();
    for (int i = 1; i <= nodes; i++) {
        weights.Add(i);
    }

    // Vector to store levels of every nodes
    List<int> levels = new List<int>();
    for (int i = 0; i < N; i++) {

        // 2^i nodes are present at ith level
        for (int j = 0; j < (int) Math.Pow(2, i); j++) {

            // value of level becomes negative
            // while going down the root
            levels.Add(-1 * i);
        }
    }

    // Create tree with the
    // given weights and levels
    node root = createTree(weights, levels);

    // Adjust the levels
    adjustLevels(root);

    // Display the final levels
    printNodeLevels(root);
  }
}

// This code is contributed by suresh07.
```

## java 描述语言

```
<script>

    // JavaScript Program to print updated levels
    // of each node of a Complete Binary Tree
    // based on difference in weights of subtrees

    // Node for the given binary tree
    class node {
        constructor(w, l) {
           this.left = null;
           this.right = null;
           this.weight = w;
           this.level = l;
        }
    }

    // Utility function to insert a node
    // in a tree rooted at root
    function insert(root, n_weight, n_level, q)
    {
        let n = new node(n_weight, n_level);

        // if the tree is empty till now
        // make node n the root
        if (root == null)
            root = n;

        // If the frontmost node of
        // queue has no left child
        // make node n its left child
        // the frontmost node still
        // remains in the queue because
        // its right child isnull yet
        else if (q[0].left == null)
        {
            q[0].left = n;
        }

        // Make node n the right child of
        // the frontmost node and remove
        // the front node from queue
        else
        {
            q[0].right = n;
            q.shift();
        }

        // push the node n into queue
        q.push(n);

        return root;
    }

    // Function to create a complete binary tree
    function createTree(weights, levels)
    {

        // initialise the root node of tree
        let root = null;

        // initialise a queue of nodes
        let q = [];
        let n = weights.length;
        for (let i = 0; i < n; i++)
        {

            /*
             * keep inserting nodes with weight values
             * from the weights vector and level
             * values from the levels vector
             */
            root = insert(root, weights[i], levels[i], q);
        }
        return root;
    }

    // Function to print final levels of nodes
    function printNodeLevels(root)
    {

        if (root == null)
            return;

        let q = [];
        q.push(root);

        while (q.length > 0) {
            document.write(q[0].level + " ");

            if (q[0].left != null)
                q.push(q[0].left);
            if (q[0].right != null)
                q.push(q[0].right);
            q.shift();
        }
        document.write("</br>");
    }

    // Function to find the weight of subtree
    function findWeight(root)
    {

        // If the root node isnull
        // then weight of subtree will be 0
        if (root == null)
            return 0;

        return root.weight + findWeight(root.left) +
        findWeight(root.right);
    }

    // Function to compute new level
    // of the nodes based on the
    // difference of weight K
    function changeLevels(root, k)
    {
        if (root == null)
            return;

        // Change the level of root node
        root.level = root.level + k;

        // Recursively change the level of
        // left and right subtree
        changeLevels(root.left, k);
        changeLevels(root.right, k);
    }

    // Function to calculate weight of
    // the left and the right subtrees and
    // adjust levels based on their difference
    function adjustLevels(root)
    {

        // No adjustment required
        // when root isnull
        if (root == null)
            return;

        // Find weights of left
        // and right subtrees
        let w_left = findWeight(root.left);
        let w_right = findWeight(root.right);

        // find the difference between the
        // weights of left and right subtree
        let w_diff = w_left - w_right;

        // Change the levels of nodes
        // according to weight difference at root
        changeLevels(root.left, -w_diff);
        changeLevels(root.right, w_diff);

        // Recursively adjust the levels
        // for left and right subtrees
        adjustLevels(root.left);
        adjustLevels(root.right);
    }

    // Number of levels
    let N = 3;

    // Number of nodes
    let nodes = Math.pow(2, N) - 1;

    // Vector to store weights of tree nodes
    let weights = [];
    for (let i = 1; i <= nodes; i++) {
      weights.push(i);
    }

    // Vector to store levels of every nodes
    let levels = [];
    for (let i = 0; i < N; i++) {

      // 2^i nodes are present at ith level
      for (let j = 0; j < Math.pow(2, i); j++) {

        // value of level becomes negative
        // while going down the root
        levels.push(-1 * i);
      }
    }

    // Create tree with the
    // given weights and levels
    let root = createTree(weights, levels);

    // Adjust the levels
    adjustLevels(root);

    // Display the final levels
    printNodeLevels(root);

</script>
```

**Output:** 

```
0 4 -6 4 2 -6 -8
```

**时间复杂度:** O(N)，其中 N 为树中节点总数。
**辅助空间:** O(N)