# 完美二叉树特定级别顺序遍历

> 原文:[https://www . geesforgeks . org/perfect-二叉树-特定级别-顺序-遍历/](https://www.geeksforgeeks.org/perfect-binary-tree-specific-level-order-traversal/)

给定一个[完美二叉树](http://xlinux.nist.gov/dads//HTML/perfectBinaryTree.html)如下:
(点击图片获得清晰视图)

![image(4)](img/ab9fda089880b51dc36ca0cace7ce5a7.png)

以下列特定方式打印节点的级别顺序:

```
  1 2 3 4 7 5 6 8 15 9 14 10 13 11 12 16 31 17 30 18 29 19 28 20 27 21 26  22 25 23 24
```

即按级别顺序打印节点，但是节点应该交替地从左侧和右侧开始。这里 1 <sup>st</sup> 和 2 <sup>nd</sup> 等级都是微不足道的。
同时打印 3 <sup>rd</sup> 级别:4(左)、7(右)、5(左)、6(右)。
而第 4 <sup>级</sup>级:8(左)、15(右)、9(左)、14(右)、..被打印出来。
而第 5<sup>级:16(左)、31(右)、17(左)、30(右)，..被打印出来。</sup>

**强烈建议尽量减少浏览器，先自己试试这个。**
在标准[级顺序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)中，我们将根入队到队列 1 <sup>st</sup> 中，然后我们将一个节点从队列中出列，处理(打印)它，将其子节点入队到队列中。我们一直这样做，直到队列空了。

**方法 1:**
我们也可以在这里进行标准的级序遍历，但是不是直接打印节点，而是将当前级的节点存储在一个临时数组或者列表 1 <sup>st</sup> 中，然后从交替的两端(左右)取节点并打印节点。继续对所有级别重复此操作。
这种方法比标准遍历占用更多内存。

**进场 2:**
标准的关卡顺序遍历思路在这里会略有改变。我们将一次处理两个节点，而不是一次处理一个节点。将子节点推入队列时，入队顺序为:1 <sup>st</sup> 节点的左子节点，2 <sup>nd</sup> 节点的右子节点，1 <sup>st</sup> 节点的右子节点，2 <sup>nd</sup> 节点的左子节点。

## C++

```
/* C++ program for special order traversal */
#include <iostream>
#include <queue>
using namespace std;

/* A binary tree node has data, pointer to left child
   and a pointer to right child */
struct Node
{
    int data;
    Node *left;
    Node *right;
};

/* Helper function that allocates a new node with the
   given data and NULL left and right pointers. */
Node *newNode(int data)
{
    Node *node = new Node;
    node->data = data;
    node->right = node->left = NULL;
    return node;
}

/* Given a perfect binary tree, print its nodes in specific
   level order */
void printSpecificLevelOrder(Node *root)
{
    if (root == NULL)
        return;

    // Let us print root and next level first
    cout << root->data;

    // / Since it is perfect Binary Tree, right is not checked
    if (root->left != NULL)
      cout << " " << root->left->data << " " << root->right->data;

    // Do anything more if there are nodes at next level in
    // given perfect Binary Tree
    if (root->left->left == NULL)
        return;

    // Create a queue and enqueue left and right children of root
    queue <Node *> q;
    q.push(root->left);
    q.push(root->right);

    // We process two nodes at a time, so we need two variables
    // to store two front items of queue
    Node *first = NULL, *second = NULL;

    // traversal loop
    while (!q.empty())
    {
       // Pop two items from queue
       first = q.front();
       q.pop();
       second = q.front();
       q.pop();

       // Print children of first and second in reverse order
       cout << " " << first->left->data << " " << second->right->data;
       cout << " " << first->right->data << " " << second->left->data;

       // If first and second have grandchildren, enqueue them
       // in reverse order
       if (first->left->left != NULL)
       {
           q.push(first->left);
           q.push(second->right);
           q.push(first->right);
           q.push(second->left);
       }
    }
}

/* Driver program to test above functions*/
int main()
{
    //Perfect Binary Tree of Height 4
    Node *root = newNode(1);

    root->left        = newNode(2);
    root->right       = newNode(3);

    root->left->left  = newNode(4);
    root->left->right = newNode(5);
    root->right->left  = newNode(6);
    root->right->right = newNode(7);

    root->left->left->left  = newNode(8);
    root->left->left->right  = newNode(9);
    root->left->right->left  = newNode(10);
    root->left->right->right  = newNode(11);
    root->right->left->left  = newNode(12);
    root->right->left->right  = newNode(13);
    root->right->right->left  = newNode(14);
    root->right->right->right  = newNode(15);

    root->left->left->left->left  = newNode(16);
    root->left->left->left->right  = newNode(17);
    root->left->left->right->left  = newNode(18);
    root->left->left->right->right  = newNode(19);
    root->left->right->left->left  = newNode(20);
    root->left->right->left->right  = newNode(21);
    root->left->right->right->left  = newNode(22);
    root->left->right->right->right  = newNode(23);
    root->right->left->left->left  = newNode(24);
    root->right->left->left->right  = newNode(25);
    root->right->left->right->left  = newNode(26);
    root->right->left->right->right  = newNode(27);
    root->right->right->left->left  = newNode(28);
    root->right->right->left->right  = newNode(29);
    root->right->right->right->left  = newNode(30);
    root->right->right->right->right  = newNode(31);

    cout << "Specific Level Order traversal of binary tree is \n";
    printSpecificLevelOrder(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for special level order traversal

import java.util.LinkedList;
import java.util.Queue;

/* Class containing left and right child of current
   node and key value*/
class Node
{
    int data;
    Node left, right;

    public Node(int item)
    {
        data = item;
        left = right = null;
    }
}

class BinaryTree
{
    Node root;

    /* Given a perfect binary tree, print its nodes in specific
       level order */
    void printSpecificLevelOrder(Node node)
    {
        if (node == null)
            return;

        // Let us print root and next level first
        System.out.print(node.data);

        //  Since it is perfect Binary Tree, right is not checked
        if (node.left != null)
            System.out.print(" " + node.left.data + " " + node.right.data);

        // Do anything more if there are nodes at next level in
        // given perfect Binary Tree
        if (node.left.left == null)
            return;

        // Create a queue and enqueue left and right children of root
        Queue<Node> q = new LinkedList<Node>();
        q.add(node.left);
        q.add(node.right);

        // We process two nodes at a time, so we need two variables
        // to store two front items of queue
        Node first = null, second = null;

        // traversal loop
        while (!q.isEmpty())
        {
            // Pop two items from queue
            first = q.peek();
            q.remove();
            second = q.peek();
            q.remove();

            // Print children of first and second in reverse order
            System.out.print(" " + first.left.data + " " +second.right.data);
            System.out.print(" " + first.right.data + " " +second.left.data);

            // If first and second have grandchildren, enqueue them
            // in reverse order
            if (first.left.left != null)
            {
                q.add(first.left);
                q.add(second.right);
                q.add(first.right);
                q.add(second.left);
            }
        }
    }

    // Driver program to test for above functions
    public static void main(String args[])
    {
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(1);
        tree.root.left = new Node(2);
        tree.root.right = new Node(3);

        tree.root.left.left = new Node(4);
        tree.root.left.right = new Node(5);
        tree.root.right.left = new Node(6);
        tree.root.right.right = new Node(7);

        tree.root.left.left.left = new Node(8);
        tree.root.left.left.right = new Node(9);
        tree.root.left.right.left = new Node(10);
        tree.root.left.right.right = new Node(11);
        tree.root.right.left.left = new Node(12);
        tree.root.right.left.right = new Node(13);
        tree.root.right.right.left = new Node(14);
        tree.root.right.right.right = new Node(15);

        tree.root.left.left.left.left = new Node(16);
        tree.root.left.left.left.right = new Node(17);
        tree.root.left.left.right.left = new Node(18);
        tree.root.left.left.right.right = new Node(19);
        tree.root.left.right.left.left = new Node(20);
        tree.root.left.right.left.right = new Node(21);
        tree.root.left.right.right.left = new Node(22);
        tree.root.left.right.right.right = new Node(23);
        tree.root.right.left.left.left = new Node(24);
        tree.root.right.left.left.right = new Node(25);
        tree.root.right.left.right.left = new Node(26);
        tree.root.right.left.right.right = new Node(27);
        tree.root.right.right.left.left = new Node(28);
        tree.root.right.right.left.right = new Node(29);
        tree.root.right.right.right.left = new Node(30);
        tree.root.right.right.right.right = new Node(31);

        System.out.println("Specific Level Order traversal of binary"
                                                            +"tree is ");
        tree.printSpecificLevelOrder(tree.root);
    }
}

// This code has been contributed by Mayank Jaiswal
```

## 计算机编程语言

```
# Python program for special order traversal

# A binary tree node
class Node:
    # A constructor for making a new node
    def __init__(self, key):
        self.data = key
        self.left = None
        self.right = None

# Given a perfect binary tree print its node in
# specific order
def printSpecificLevelOrder(root):
    if root is None:
        return

    # Let us print root and next level first
    print root.data,

    # Since it is perfect Binary tree,
    # one of the node is needed to be checked
    if root.left is not None :
        print root.left.data,
        print root.right.data,

    # Do anything more if there are nodes at next level
    # in given perfect Binary Tree
    if root.left.left is None:
        return

    # Create a queue and enqueue left and right
    # children of root
    q = []
    q.append(root.left)
    q.append(root.right)

    # We process two nodes at a time, so we need
    # two variables to store two front items of queue
    first = None
    second = None

    # Traversal loop
    while(len(q) > 0):

        # Pop two items from queue
        first = q.pop(0)
        second = q.pop(0)

        # Print children of first and second in reverse order
        print first.left.data,
        print second.right.data,
        print first.right.data,
        print second.left.data,

        # If first and second have grandchildren,
        # enqueue them in reverse order
        if first.left.left is not None:
            q.append(first.left)
            q.append(second.right)
            q.append(first.right)
            q.append(second.left)

# Driver program to test above function

# Perfect Binary Tree of Height 4
root = Node(1)

root.left= Node(2)
root.right   = Node(3)

root.left.left  = Node(4)
root.left.right = Node(5)
root.right.left  = Node(6)
root.right.right = Node(7)

root.left.left.left  = Node(8)
root.left.left.right  = Node(9)
root.left.right.left  = Node(10)
root.left.right.right  = Node(11)
root.right.left.left  = Node(12)
root.right.left.right  = Node(13)
root.right.right.left  = Node(14)
root.right.right.right  = Node(15)

root.left.left.left.left  = Node(16)
root.left.left.left.right  = Node(17)
root.left.left.right.left  = Node(18)
root.left.left.right.right  = Node(19)
root.left.right.left.left  = Node(20)
root.left.right.left.right  = Node(21)
root.left.right.right.left  = Node(22)
root.left.right.right.right  = Node(23)
root.right.left.left.left  = Node(24)
root.right.left.left.right  = Node(25)
root.right.left.right.left  = Node(26)
root.right.left.right.right  = Node(27)
root.right.right.left.left  = Node(28)
root.right.right.left.right  = Node(29)
root.right.right.right.left  = Node(30)
root.right.right.right.right  = Node(31)

print "Specific Level Order traversal of binary tree is"
printSpecificLevelOrder(root);

# This code is contributed by Nikhil Kumar Singh(nickzuck_007)
```

## C#

```
// C# program for special level
// order traversal
using System;
using System.Collections.Generic;

/* Class containing left and right
child of current node and key value*/
public class Node
{
    public int data;
    public Node left, right;

    public Node(int item)
    {
        data = item;
        left = right = null;
    }
}

class GFG
{
public Node root;

/* Given a perfect binary tree,
print its nodes in specific
level order */
public virtual void printSpecificLevelOrder(Node node)
{
    if (node == null)
    {
        return;
    }

    // Let us print root and next level first
    Console.Write(node.data);

    // Since it is perfect Binary Tree,
    // right is not checked
    if (node.left != null)
    {
        Console.Write(" " + node.left.data +
                      " " + node.right.data);
    }

    // Do anything more if there
    // are nodes at next level in
    // given perfect Binary Tree
    if (node.left.left == null)
    {
        return;
    }

    // Create a queue and enqueue left
    // and right children of root
    LinkedList<Node> q = new LinkedList<Node>();
    q.AddLast(node.left);
    q.AddLast(node.right);

    // We process two nodes at a time,
    // so we need two variables to
    // store two front items of queue
    Node first = null, second = null;

    // traversal loop
    while (q.Count > 0)
    {
        // Pop two items from queue
        first = q.First.Value;
        q.RemoveFirst();
        second = q.First.Value;
        q.RemoveFirst();

        // Print children of first and
        // second in reverse order
        Console.Write(" " + first.left.data +
                      " " + second.right.data);
        Console.Write(" " + first.right.data +
                      " " + second.left.data);

        // If first and second have grandchildren,
        // enqueue them in reverse order
        if (first.left.left != null)
        {
            q.AddLast(first.left);
            q.AddLast(second.right);
            q.AddLast(first.right);
            q.AddLast(second.left);
        }
    }
}

// Driver Code
public static void Main(string[] args)
{
    GFG tree = new GFG();
    tree.root = new Node(1);
    tree.root.left = new Node(2);
    tree.root.right = new Node(3);

    tree.root.left.left = new Node(4);
    tree.root.left.right = new Node(5);
    tree.root.right.left = new Node(6);
    tree.root.right.right = new Node(7);

    tree.root.left.left.left = new Node(8);
    tree.root.left.left.right = new Node(9);
    tree.root.left.right.left = new Node(10);
    tree.root.left.right.right = new Node(11);
    tree.root.right.left.left = new Node(12);
    tree.root.right.left.right = new Node(13);
    tree.root.right.right.left = new Node(14);
    tree.root.right.right.right = new Node(15);

    tree.root.left.left.left.left = new Node(16);
    tree.root.left.left.left.right = new Node(17);
    tree.root.left.left.right.left = new Node(18);
    tree.root.left.left.right.right = new Node(19);
    tree.root.left.right.left.left = new Node(20);
    tree.root.left.right.left.right = new Node(21);
    tree.root.left.right.right.left = new Node(22);
    tree.root.left.right.right.right = new Node(23);
    tree.root.right.left.left.left = new Node(24);
    tree.root.right.left.left.right = new Node(25);
    tree.root.right.left.right.left = new Node(26);
    tree.root.right.left.right.right = new Node(27);
    tree.root.right.right.left.left = new Node(28);
    tree.root.right.right.left.right = new Node(29);
    tree.root.right.right.right.left = new Node(30);
    tree.root.right.right.right.right = new Node(31);

    Console.WriteLine("Specific Level Order " +
                      "traversal of binary" + "tree is ");
    tree.printSpecificLevelOrder(tree.root);
}
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

// JavaScript program for special level
// order traversal

/* Class containing left and right
child of current node and key value*/
class Node
{
  constructor(item)
  {
    this.data = item;
    this.left = null;
    this.right = null;
  }
}

var root = null;

/* Given a perfect binary tree,
print its nodes in specific
level order */
function printSpecificLevelOrder(node)
{
    if (node == null)
    {
        return;
    }

    // Let us print root and next level first
    document.write(node.data);

    // Since it is perfect Binary Tree,
    // right is not checked
    if (node.left != null)
    {
        document.write(" " + node.left.data +
                      " " + node.right.data);
    }

    // Do anything more if there
    // are nodes at next level in
    // given perfect Binary Tree
    if (node.left.left == null)
    {
        return;
    }

    // Create a queue and enqueue left
    // and right children of root
    var q = [];
    q.push(node.left);
    q.push(node.right);

    // We process two nodes at a time,
    // so we need two variables to
    // store two front items of queue
    var first = null, second = null;

    // traversal loop
    while (q.length > 0)
    {
        // Pop two items from queue
        first = q[0];
        q.shift();
        second = q[0];
        q.shift();

        // Print children of first and
        // second in reverse order
        document.write(" " + first.left.data +
                      " " + second.right.data);
        document.write(" " + first.right.data +
                      " " + second.left.data);

        // If first and second have grandchildren,
        // enqueue them in reverse order
        if (first.left.left != null)
        {
            q.push(first.left);
            q.push(second.right);
            q.push(first.right);
            q.push(second.left);
        }
    }
}

// Driver Code
root = new Node(1);
root.left = new Node(2);
root.right = new Node(3);
root.left.left = new Node(4);
root.left.right = new Node(5);
root.right.left = new Node(6);
root.right.right = new Node(7);
root.left.left.left = new Node(8);
root.left.left.right = new Node(9);
root.left.right.left = new Node(10);
root.left.right.right = new Node(11);
root.right.left.left = new Node(12);
root.right.left.right = new Node(13);
root.right.right.left = new Node(14);
root.right.right.right = new Node(15);
root.left.left.left.left = new Node(16);
root.left.left.left.right = new Node(17);
root.left.left.right.left = new Node(18);
root.left.left.right.right = new Node(19);
root.left.right.left.left = new Node(20);
root.left.right.left.right = new Node(21);
root.left.right.right.left = new Node(22);
root.left.right.right.right = new Node(23);
root.right.left.left.left = new Node(24);
root.right.left.left.right = new Node(25);
root.right.left.right.left = new Node(26);
root.right.left.right.right = new Node(27);
root.right.right.left.left = new Node(28);
root.right.right.left.right = new Node(29);
root.right.right.right.left = new Node(30);
root.right.right.right.right = new Node(31);
document.write("Specific Level Order " +
                  "traversal of binary" + "tree is <br>");
printSpecificLevelOrder(root);

</script>
```

**输出:**

```
Specific Level Order traversal of binary tree is
1 2 3 4 7 5 6 8 15 9 14 10 13 11 12 16 31 17 30 18 29 19 28 20 27 21 26 22 25 23 24
```

**后续问题:**

1.  上面的代码从上到下打印特定的级别顺序。你将如何进行从底部到顶部的特定级别顺序遍历([亚马逊采访|第 120 集–第 1 轮最后一个问题](https://www.geeksforgeeks.org/amazon-interview-set-120-campus-internship/))
2.  如果树不是完美的，而是完整的。
3.  如果树既不完美，也不完整。它可以是任何一般的二叉树。

本文由**阿努拉格·辛格**供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。