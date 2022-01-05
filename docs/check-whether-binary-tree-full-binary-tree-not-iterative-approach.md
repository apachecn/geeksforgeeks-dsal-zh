# 检查二叉树是否是完全二叉树|迭代方法

> 原文:[https://www . geesforgeks . org/check-when-二叉树-full-二叉树-非迭代-方法/](https://www.geeksforgeeks.org/check-whether-binary-tree-full-binary-tree-not-iterative-approach/)

给定一个包含 **n 个**节点的二叉树。问题是检查给定的二叉树是否是完全二叉树。完全二叉树被定义为所有节点都有零个或两个子节点的二叉树。相反，完全二叉树中没有节点，只有一个子节点。
**例:**

```
Input : 
           1
         /   \
        2     3
       / \  
      4   5
Output : Yes

Input :
           1
         /   \
        2     3
       /  
      4   
Output :No
```

**方法:**在[之前的帖子](https://www.geeksforgeeks.org/check-whether-binary-tree-full-binary-tree-not/)中已经讨论了递归解决方案。在这篇文章中，采用了迭代的方法。使用队列执行树的[迭代级别顺序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)。对于遇到的每个**节点**，按照下面给出的步骤操作:

1.  如果(节点->左==空&&节点->右==空)，则它是叶节点。丢弃它并开始处理队列中的下一个节点。
2.  如果(节点->左==空||节点->右==空)，则表示只有**节点**的子节点存在。返回 false，因为二叉树不是完整的二叉树。
3.  否则，将**节点**的左右子节点推到队列中。

如果队列中的所有节点都得到了处理而没有返回 false，那么返回 true，因为二叉树是一个完整的二叉树。

## C++

```
// C++ implementation to check whether a binary
// tree is a full binary tree or not
#include <bits/stdc++.h>
using namespace std;

// structure of a node of binary tree
struct Node {
    int data;
    Node *left, *right;
};

// function to get a new node
Node* getNode(int data)
{
    // allocate space
    Node* newNode = (Node*)malloc(sizeof(Node));

    // put in the data
    newNode->data = data;
    newNode->left = newNode->right = NULL;
    return newNode;
}

// function to check whether a binary tree
// is a full binary tree or not
bool isFullBinaryTree(Node* root)
{
    // if tree is empty
    if (!root)
        return true;

    // queue used for level order traversal
    queue<Node*> q;

    // push 'root' to 'q'
    q.push(root);

    // traverse all the nodes of the binary tree
    // level by level until queue is empty
    while (!q.empty()) {
        // get the pointer to 'node' at front
        // of queue
        Node* node = q.front();
        q.pop();

        // if it is a leaf node then continue
        if (node->left == NULL && node->right == NULL)
            continue;

        // if either of the child is not null and the
        // other one is null, then binary tree is not
        // a full binary tee
        if (node->left == NULL || node->right == NULL)
            return false;

        // push left and right childs of 'node'
        // on to the queue 'q'
        q.push(node->left);
        q.push(node->right);
    }

    // binary tree is a full binary tee
    return true;
}

// Driver program to test above
int main()
{
    Node* root = getNode(1);
    root->left = getNode(2);
    root->right = getNode(3);
    root->left->left = getNode(4);
    root->left->right = getNode(5);

    if (isFullBinaryTree(root))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check whether a binary
// tree is a full binary tree or not
import java.util.*;
class GfG {

// structure of a node of binary tree
static class Node {
    int data;
    Node left, right;
}

// function to get a new node
static Node getNode(int data)
{
    // allocate space
    Node newNode = new Node();

    // put in the data
    newNode.data = data;
    newNode.left = null;
    newNode.right = null;
    return newNode;
}

// function to check whether a binary tree
// is a full binary tree or not
static boolean isFullBinaryTree(Node root)
{
    // if tree is empty
    if (root == null)
        return true;

    // queue used for level order traversal
    Queue<Node> q = new LinkedList<Node> ();

    // push 'root' to 'q'
    q.add(root);

    // traverse all the nodes of the binary tree
    // level by level until queue is empty
    while (!q.isEmpty()) {
        // get the pointer to 'node' at front
        // of queue
        Node node = q.peek();
        q.remove();

        // if it is a leaf node then continue
        if (node.left == null && node.right == null)
            continue;

        // if either of the child is not null and the
        // other one is null, then binary tree is not
        // a full binary tee
        if (node.left == null || node.right == null)
            return false;

        // push left and right childs of 'node'
        // on to the queue 'q'
        q.add(node.left);
        q.add(node.right);
    }

    // binary tree is a full binary tee
    return true;
}

// Driver program to test above
public static void main(String[] args)
{
    Node root = getNode(1);
    root.left = getNode(2);
    root.right = getNode(3);
    root.left.left = getNode(4);
    root.left.right = getNode(5);

    if (isFullBinaryTree(root))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}
```

## 蟒蛇 3

```
# Python3 program to find deepest
# left leaf Binary search Tree

# Helper function that allocates a 
# new node with the given data and
# None left and right pairs.                                    
class getNode:

    # Constructor to create a new node
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# function to check whether a binary 
# tree is a full binary tree or not
def isFullBinaryTree( root) :

    # if tree is empty
    if (not root) :
        return True

    # queue used for level order
    # traversal
    q = []

    # append 'root' to 'q'
    q.append(root)

    # traverse all the nodes of the
    # binary tree level by level
    # until queue is empty
    while (not len(q)):

        # get the pointer to 'node'
        # at front of queue
        node = q[0]
        q.pop(0)

        # if it is a leaf node then continue
        if (node.left == None and
            node.right == None):
            continue

        # if either of the child is not None 
        # and the other one is None, then
        # binary tree is not a full binary tee
        if (node.left == None or
            node.right == None):
            return False

        # append left and right childs
        # of 'node' on to the queue 'q'
        q.append(node.left)
        q.append(node.right)

    # binary tree is a full binary tee
    return True

# Driver Code
if __name__ == '__main__':
    root = getNode(1)
    root.left = getNode(2)
    root.right = getNode(3)
    root.left.left = getNode(4)
    root.left.right = getNode(5)

    if (isFullBinaryTree(root)) :
        print("Yes" )
    else:
        print("No")

# This code is contributed by
# Shubham Singh(SHUBHAMSINGH10)
```

## C#

```
// C# implementation to check whether a binary
// tree is a full binary tree or not
using System;
using System.Collections.Generic;

class GfG
{

// structure of a node of binary tree
public class Node
{
    public int data;
    public Node left, right;
}

// function to get a new node
static Node getNode(int data)
{
    // allocate space
    Node newNode = new Node();

    // put in the data
    newNode.data = data;
    newNode.left = null;
    newNode.right = null;
    return newNode;
}

// function to check whether a binary tree
// is a full binary tree or not
static bool isFullBinaryTree(Node root)
{
    // if tree is empty
    if (root == null)
        return true;

    // queue used for level order traversal
    Queue<Node> q = new Queue<Node> ();

    // push 'root' to 'q'
    q.Enqueue(root);

    // traverse all the nodes of the binary tree
    // level by level until queue is empty
    while (q.Count!=0) {
        // get the pointer to 'node' at front
        // of queue
        Node node = q.Peek();
        q.Dequeue();

        // if it is a leaf node then continue
        if (node.left == null && node.right == null)
            continue;

        // if either of the child is not null and the
        // other one is null, then binary tree is not
        // a full binary tee
        if (node.left == null || node.right == null)
            return false;

        // push left and right childs of 'node'
        // on to the queue 'q'
        q.Enqueue(node.left);
        q.Enqueue(node.right);
    }

    // binary tree is a full binary tee
    return true;
}

// Driver code
public static void Main(String[] args)
{
    Node root = getNode(1);
    root.left = getNode(2);
    root.right = getNode(3);
    root.left.left = getNode(4);
    root.left.right = getNode(5);

    if (isFullBinaryTree(root))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

    // JavaScript implementation to check whether a binary
    // tree is a full binary tree or not

    // A Binary Tree Node
    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    // function to get a new node
    function getNode(data)
    {
        // allocate space
        let newNode = new Node(data);
        return newNode;
    }

    // function to check whether a binary tree
    // is a full binary tree or not
    function isFullBinaryTree(root)
    {
        // if tree is empty
        if (root == null)
            return true;

        // queue used for level order traversal
        let q = [];

        // push 'root' to 'q'
        q.push(root);

        // traverse all the nodes of the binary tree
        // level by level until queue is empty
        while (q.length > 0) {
            // get the pointer to 'node' at front
            // of queue
            let node = q[0];
            q.shift();

            // if it is a leaf node then continue
            if (node.left == null && node.right == null)
                continue;

            // if either of the child is not null and the
            // other one is null, then binary tree is not
            // a full binary tee
            if (node.left == null || node.right == null)
                return false;

            // push left and right childs of 'node'
            // on to the queue 'q'
            q.push(node.left);
            q.push(node.right);
        }

        // binary tree is a full binary tee
        return true;
    }

    let root = getNode(1);
    root.left = getNode(2);
    root.right = getNode(3);
    root.left.left = getNode(4);
    root.left.right = getNode(5);

    if (isFullBinaryTree(root))
        document.write("Yes");
    else
        document.write("No");

</script>
```

**输出:**

```
Yes
```

**时间复杂度:** O(n)。
**辅助空间:** O(最大值)，其中**最大值**是特定级别的最大节点数。