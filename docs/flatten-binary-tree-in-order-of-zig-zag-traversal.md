# 按照之字形遍历的顺序展平二叉树

> 原文:[https://www . geeksforgeeks . org/扁平化-二叉树-按之字形顺序遍历/](https://www.geeksforgeeks.org/flatten-binary-tree-in-order-of-zig-zag-traversal/)

给定一棵二叉树，任务是按照树的[之字形遍历](https://www.geeksforgeeks.org/zigzag-tree-traversal/)的顺序将其展平。在展平的二叉树中，所有节点的左节点必须为空。
**例:**

```
Input: 
          1 
        /   \ 
       5     2 
      / \   / \ 
     6   4 9   3 
Output: 1 2 5 6 4 9 3

Input:
      1
       \
        2
         \
          3
           \
            4
             \
              5
Output: 1 2 3 4 5
```

**方法:**我们将通过模拟二叉树的 ZigZag 遍历来解决这个问题。
算法:

1.  创建两个栈，“c_lev”和“n_lev”，并存储当前和下一级二叉树的节点。
2.  创建一个变量“prev”，并通过父节点初始化它。
3.  在 c_lev 堆栈中推动父对象的左右子对象。
4.  应用 ZigZag 遍历。假设“curr”是“c_lev”中最重要的元素。然后，
    *   如果“curr”为空，则继续。
    *   否则按适当的顺序在堆栈“n_lev”上按 curr->left 和 curr->right。如果我们执行的是从左到右的遍历，那么 curr->left 被首先推，否则 curr->right 被首先推。
    *   set prev = curr。

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Node of the binary tree
struct node {
    int data;
    node* left;
    node* right;
    node(int data)
    {
        this->data = data;
        left = NULL;
        right = NULL;
    }
};

// Function to flatten Binary tree
void flatten(node* parent)
{
    // Queue to store node
    // for BFS
    stack<node *> c_lev, n_lev;

    c_lev.push(parent->left);
    c_lev.push(parent->right);

    bool lev = 1;
    node* prev = parent;

    // Code for BFS
    while (c_lev.size()) {

        // Size of queue
        while (c_lev.size()) {

            // Front most node in
            // queue
            node* curr = c_lev.top();
            c_lev.pop();

            // Base case
            if (curr == NULL)
                continue;
            prev->right = curr;
            prev->left = NULL;
            prev = curr;

            // Pushing new elements
            // in queue
            if (!lev)
                n_lev.push(curr->left);
            n_lev.push(curr->right);
            if (lev)
                n_lev.push(curr->left);
        }
        lev = (!lev);
        c_lev = n_lev;
        while (n_lev.size())
            n_lev.pop();
    }

    prev->left = NULL;
    prev->right = NULL;
}

// Function to print flattened
// binary tree
void print(node* parent)
{
    node* curr = parent;
    while (curr != NULL)
        cout << curr->data << " ", curr = curr->right;
}

// Driver code
int main()
{
    node* root = new node(1);
    root->left = new node(5);
    root->right = new node(2);
    root->left->left = new node(6);
    root->left->right = new node(4);
    root->right->left = new node(9);
    root->right->right = new node(3);

    // Calling required functions
    flatten(root);

    print(root);

    return 0;
}
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Node of the binary tree
class node {

    constructor(data)
    {
        this.data = data;
        this.left = null;
        this.right = null;
    }
};

// Function to flatten Binary tree
function flatten()
{
    // Queue to store node
    // for BFS
    var c_lev = [], n_lev = [];

    c_lev.push(parent.left);
    c_lev.push(parent.right);

    var lev = 1;
    var prev = parent;

    // Code for BFS
    while (c_lev.length!=0) {

        // Size of queue
        while (c_lev.length!=0) {

            // Front most node in
            // queue
            var curr = c_lev[c_lev.length-1];
            c_lev.pop();

            // Base case
            if (curr == null)
                continue;

            prev.right = curr;
            prev.left = null;
            prev = curr;

            // Pushing new elements
            // in queue
            if (!lev)
                n_lev.push(curr.left);
            n_lev.push(curr.right);
            if (lev)
                n_lev.push(curr.left);
        }

        lev = lev==0?1:0;
        c_lev = n_lev;
        n_lev = [];
    }

    prev.left = null;
    prev.right = null;
}

// Function to print flattened
// binary tree
function print()
{
    var curr = parent;
    while (curr != null)
    {
        document.write(curr.data + " ");
        curr = curr.right;
    }     
}

// Driver code
var parent = new node(1);
parent.left = new node(5);
parent.right = new node(2);
parent.left.left = new node(6);
parent.left.right = new node(4);
parent.right.left = new node(9);
parent.right.right = new node(3);
// Calling required functions
flatten();
print();

// This code is contributed by rrrtnx.
</script>
```

**Output:** 

```
1 2 5 6 4 9 3
```

**时间复杂度:**O(N)
T3】空间复杂度: O(N)其中 N 是二叉树的大小。