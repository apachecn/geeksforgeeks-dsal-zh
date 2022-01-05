# 打印二叉树中给定节点的表兄弟|单次遍历

> 原文:[https://www . geesforgeks . org/print-给定二叉树中节点的表亲-单次遍历/](https://www.geeksforgeeks.org/print-cousins-of-a-given-node-in-binary-tree-single-traversal/)

给定一个二叉树和一个节点，打印给定节点的所有表兄弟。请注意，不应打印兄弟姐妹。

**示例:**

```
Input : root of below tree 
             1
           /   \
          2     3
        /   \  /  \
       4    5  6   7
       and pointer to a node say 5.

Output : 6, 7
```

请注意，这与[给出的问题相同，打印二叉树](https://www.geeksforgeeks.org/print-cousins-of-a-given-node-in-binary-tree/)中给定节点的表亲，该二叉树由两个递归遍历组成。在这篇文章中，讨论了一种单层遍历方法。
想法是进行树的级别顺序遍历，因为节点的表亲和兄弟可以在其级别顺序遍历中找到。运行遍历，直到没有找到包含该节点的级别，如果找到，打印给定的级别。

**如何打印表亲节点而不是兄弟节点，如何获取队列中该级别的节点？**在等级顺序中，当对于父节点，如果父- >左== Node_to_find，或者父- >右== Node_to_find，那么这个父节点的子节点一定不能被推入队列(因为一个是节点，另一个是它的兄弟节点)。推送队列中同一级别的剩余节点，然后退出循环。当前队列的节点将位于下一个级别(被搜索节点的级别，节点及其同级除外)。现在，打印队列。

下面是上述算法的实现。

## C++

```
// C++ program to print cousins of a node
#include <iostream>
#include <queue>
using namespace std;

// A Binary Tree Node
struct Node {
    int data;
    Node *left, *right;
};

// A utility function to create a new Binary
// Tree Node
Node* newNode(int item)
{
    Node* temp = new Node;
    temp->data = item;
    temp->left = temp->right = NULL;
    return temp;
}

// function to print cousins of the node
void printCousins(Node* root, Node* node_to_find)
{
    // if the given node is the root itself,
    // then no nodes would be printed
    if (root == node_to_find) {
        cout << "Cousin Nodes : None" << endl;
        return;
    }

    queue<Node*> q;
    bool found = false;
    int size_;
    Node* p;
    q.push(root);

    // the following loop runs until found is
    // not true, or q is not empty.
    // if found has become true => we have found
    // the level in which the node is present
    // and the present queue will contain all the
    // cousins of that node
    while (!q.empty() && !found) {

        size_ = q.size();
        while (size_) {
            p = q.front();
            q.pop();

            // if current node's left or right child
            // is the same as the node to find,
            // then make found = true, and don't push
            // any of them into the queue, as
            // we don't have to print the siblings
            if ((p->left == node_to_find ||
                p->right == node_to_find)) {
                found = true;
            }
            else {
                if (p->left)
                    q.push(p->left);
                if (p->right)
                    q.push(p->right);
            }

            size_--;
        }
    }

    // if found == true then the queue will contain the
    // cousins of the given node
    if (found) {
        cout << "Cousin Nodes : ";
        size_ = q.size();

        // size_ will be 0 when the node was at the
        // level just below the root node.
        if (size_ == 0)
            cout << "None";
        for (int i = 0; i < size_; i++) {
            p = q.front();
            q.pop();
            cout << p->data << " ";
        }
    }
    else {
        cout << "Node not found";
    }
    cout << endl;
    return;
}

// Driver Program to test above function
int main()
{
    Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->left->right->right = newNode(15);
    root->right->left = newNode(6);
    root->right->right = newNode(7);
    root->right->left->right = newNode(8);

    Node* x = newNode(43);

    printCousins(root, x);
    printCousins(root, root);
    printCousins(root, root->right);
    printCousins(root, root->left);
    printCousins(root, root->left->right);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print
// cousins of a node
import java.io.*;
import java.util.*;
import java.lang.*;

// A Binary Tree Node
class Node
{
    int data;
    Node left, right;
    Node(int key)
    {
        data = key;
        left = right = null;
    }
}

class GFG
{

// function to print
// cousins of the node
static void printCousins(Node root,
                         Node node_to_find)
{
    // if the given node
    // is the root itself,
    // then no nodes would
    // be printed
    if (root == node_to_find)
    {
        System.out.print("Cousin Nodes :" +
                           " None" + "\n");
        return;
    }

    Queue<Node> q = new LinkedList<Node>();
    boolean found = false;
    int size_ = 0;
    Node p = null;
    q.add(root);

    // the following loop runs
    // until found is not true,
    // or q is not empty. if
    // found has become true => we
    // have found the level in
    // which the node is present
    // and the present queue will
    // contain all the cousins of
    // that node
    while (q.isEmpty() == false &&
                 found == false)
    {

        size_ = q.size();
        while (size_ -- > 0)
        {
            p = q.peek();
            q.remove();

            // if current node's left
            // or right child is the
            // same as the node to find,
            // then make found = true,
            // and don't push any of them
            // into the queue, as we don't
            // have to print the siblings
            if ((p.left == node_to_find ||
                 p.right == node_to_find))
            {
                found = true;
            }
            else
            {
                if (p.left != null)
                    q.add(p.left);
                if (p.right!= null)
                    q.add(p.right);
            }

        }
    }

    // if found == true then the
    // queue will contain the
    // cousins of the given node
    if (found == true)
    {
        System.out.print("Cousin Nodes : ");
        size_ = q.size();

        // size_ will be 0 when
        // the node was at the
        // level just below the
        // root node.
        if (size_ == 0)
            System.out.print("None");

        for (int i = 0; i < size_; i++)
        {
            p = q.peek();
            q.poll();

            System.out.print(p.data + " ");
        }
    }
    else
    {
        System.out.print("Node not found");
    }

    System.out.println("");
    return;
}

// Driver code
public static void main(String[] args)
{
    Node root = new Node(1);
    root.left = new Node(2);
    root.right = new Node(3);
    root.left.left = new Node(4);
    root.left.right = new Node(5);
    root.left.right.right = new Node(15);
    root.right.left = new Node(6);
    root.right.right = new Node(7);
    root.right.left.right = new Node(8);

    Node x = new Node(43);

    printCousins(root, x);
    printCousins(root, root);
    printCousins(root, root.right);
    printCousins(root, root.left);
    printCousins(root, root.left.right);
}
}
```

## 蟒蛇 3

```
# Python3 program to print cousins of a node

# A Binary Tree Node
class Node:

    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# A utility function to create a new Binary
# Tree Node
def newNode(item):

    temp = Node(item)
    return temp

# function to print cousins of the node
def printCousins(root, node_to_find):

    # if the given node is the root itself,
    # then no nodes would be printed
    if (root == node_to_find):
        print("Cousin Nodes : None")
        return;

    q = []
    found = False;
    size_ = 0
    p = None
    q.append(root);

    # the following loop runs until found is
    # not true, or q is not empty.
    # if found has become true => we have found
    # the level in which the node is present
    # and the present queue will contain all the
    # cousins of that node
    while (len(q) != 0 and not found):

        size_ = len(q)

        while (size_ != 0):

            p = q[0]
            q.pop(0);

            # if current node's left or right child
            # is the same as the node to find,
            # then make found = true, and don't append
            # any of them into the queue, as
            # we don't have to print the siblings
            if ((p.left == node_to_find or p.right == node_to_find)):
                found = True;
            else:
                if (p.left):
                    q.append(p.left);
                if (p.right):
                    q.append(p.right);

            size_-=1

    # if found == true then the queue will contain the
    # cousins of the given node
    if (found):
        print("Cousin Nodes : ", end='')
        size_ = len(q)

        # size_ will be 0 when the node was at the
        # level just below the root node.
        if (size_ == 0):
            print("None", end='')

        for i in range(0, size_):

            p = q[0]
            q.pop(0);
            print(p.data, end=' ')

    else:
        print("Node not found", end='')

    print()
    return;

# Driver Program to test above function
if __name__=='__main__':

    root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);
    root.left.right.right = newNode(15);
    root.right.left = newNode(6);
    root.right.right = newNode(7);
    root.right.left.right = newNode(8);

    x = newNode(43);

    printCousins(root, x);
    printCousins(root, root);
    printCousins(root, root.right);
    printCousins(root, root.left);
    printCousins(root, root.left.right);

# This code is contributed by rutvik_56
```

## C#

```
// C# program to print
// cousins of a node
using System;
using System.Collections.Generic;

// A Binary Tree Node
public class Node
{
    public int data;
    public Node left, right;
    public Node(int key)
    {
        data = key;
        left = right = null;
    }
}

public class GFG
{

// function to print
// cousins of the node
static void printCousins(Node root,
                         Node node_to_find)
{
    // if the given node
    // is the root itself,
    // then no nodes would
    // be printed
    if (root == node_to_find)
    {
        Console.Write("Cousin Nodes :" +
                           " None" + "\n");
        return;
    }

    Queue<Node> q = new Queue<Node>();
    bool found = false;
    int size_ = 0;
    Node p = null;
    q.Enqueue(root);

    // the following loop runs
    // until found is not true,
    // or q is not empty. if
    // found has become true => we
    // have found the level in
    // which the node is present
    // and the present queue will
    // contain all the cousins of
    // that node
    while (q.Count!=0 &&
                 found == false)
    {

        size_ = q.Count;
        while (size_ -- > 0)
        {
            p = q.Peek();
            q.Dequeue();

            // if current node's left
            // or right child is the
            // same as the node to find,
            // then make found = true,
            // and don't push any of them
            // into the queue, as we don't
            // have to print the siblings
            if ((p.left == node_to_find ||
                 p.right == node_to_find))
            {
                found = true;
            }
            else
            {
                if (p.left != null)
                    q.Enqueue(p.left);
                if (p.right!= null)
                    q.Enqueue(p.right);
            }

        }
    }

    // if found == true then the
    // queue will contain the
    // cousins of the given node
    if (found == true)
    {
        Console.Write("Cousin Nodes : ");
        size_ = q.Count;

        // size_ will be 0 when
        // the node was at the
        // level just below the
        // root node.
        if (size_ == 0)
            Console.Write("None");

        for (int i = 0; i < size_; i++)
        {
            p = q.Peek();
            q.Dequeue();

            Console.Write(p.data + " ");
        }
    }
    else
    {
        Console.Write("Node not found");
    }

    Console.WriteLine("");
    return;
}

// Driver code
public static void Main(String[] args)
{
    Node root = new Node(1);
    root.left = new Node(2);
    root.right = new Node(3);
    root.left.left = new Node(4);
    root.left.right = new Node(5);
    root.left.right.right = new Node(15);
    root.right.left = new Node(6);
    root.right.right = new Node(7);
    root.right.left.right = new Node(8);

    Node x = new Node(43);

    printCousins(root, x);
    printCousins(root, root);
    printCousins(root, root.right);
    printCousins(root, root.left);
    printCousins(root, root.left.right);
}
}

// This code is contributed Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to print
// cousins of a node

// A Binary Tree Node
class Node
{
    constructor(key)
    {
        this.data = key;
        this.left = null;
        this.right = null;
    }
}

// Function to print
// cousins of the node
function printCousins(root, node_to_find)
{

    // If the given node
    // is the root itself,
    // then no nodes would
    // be printed
    if (root == node_to_find)
    {
        document.write("Cousin Nodes :" +
                       " None" + "<br>");
        return;
    }

    var q = [];
    var found = false;
    var size_ = 0;
    var p = null;
    q.push(root);

    // The following loop runs
    // until found is not true,
    // or q is not empty. if
    // found has become true => we
    // have found the level in
    // which the node is present
    // and the present queue will
    // contain all the cousins of
    // that node
    while (q.length != 0 &&
           found == false)
    {
        size_ = q.length;

        while (size_ -- > 0)
        {
            p = q[0];
            q.shift();

            // If current node's left
            // or right child is the
            // same as the node to find,
            // then make found = true,
            // and don't push any of them
            // into the queue, as we don't
            // have to print the siblings
            if ((p.left == node_to_find ||
                p.right == node_to_find))
            {
                found = true;
            }
            else
            {
                if (p.left != null)
                    q.push(p.left);
                if (p.right!= null)
                    q.push(p.right);
            }

        }
    }

    // If found == true then the
    // queue will contain the
    // cousins of the given node
    if (found == true)
    {
        document.write("Cousin Nodes : ");
        size_ = q.length;

        // size_ will be 0 when
        // the node was at the
        // level just below the
        // root node.
        if (size_ == 0)
            document.write("None");

        for(var i = 0; i < size_; i++)
        {
            p = q[0];
            q.shift();

            document.write(p.data + " ");
        }
    }
    else
    {
        document.write("Node not found");
    }

    document.write("<br>");
    return;
}

// Driver code
var root = new Node(1);
root.left = new Node(2);
root.right = new Node(3);
root.left.left = new Node(4);
root.left.right = new Node(5);
root.left.right.right = new Node(15);
root.right.left = new Node(6);
root.right.right = new Node(7);
root.right.left.right = new Node(8);

var x = new Node(43);

printCousins(root, x);
printCousins(root, root);
printCousins(root, root.right);
printCousins(root, root.left);
printCousins(root, root.left.right);

// This code is contributed by famously

</script>
```

**Output:** 

```
Node not found
Cousin Nodes : None
Cousin Nodes : None
Cousin Nodes : None
Cousin Nodes : 6 7
```

**时间复杂度:**这是单级顺序遍历，因此时间复杂度= O(n)，辅助空间= O(n)(参见[本](https://www.geeksforgeeks.org/bfs-vs-dfs-binary-tree/))。