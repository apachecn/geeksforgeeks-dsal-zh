# 完美二叉树特定级别顺序遍历|集合 2

> 原文:[https://www . geesforgeks . org/perfect-二叉树-特定级别-顺序-遍历-集合-2/](https://www.geeksforgeeks.org/perfect-binary-tree-specific-level-order-traversal-set-2/)

在[集合 1](https://www.geeksforgeeks.org/perfect-binary-tree-specific-level-order-traversal/) 中使用特定级别顺序遍历的完美二叉树。早期的遍历是从上到下。在这篇文章中，讨论了自下而上的遍历(在[亚马逊采访|第 120 集–第 1 轮](https://www.geeksforgeeks.org/amazon-interview-set-120-campus-internship/)中询问)。

![image(4)](img/ab9fda089880b51dc36ca0cace7ce5a7.png)

16 31 17 30 18 29 19 28 20 27 21 26 22 25 23 248 15 9 14 10 13 11 124 7 5 62 31
任务是按级别顺序打印节点，但节点应该从左到右交替排列，并自下而上排列

```
5th level: 16(left), 31(right), 17(left), 30(right), … are printed.

4th level: 8(left), 15(right), 9(left), 14(right), … are printed.
 v
3rd level: 4(left), 7(right), 5(left), 6(right) are printed.

1st and 2nd levels are trivial. 
```

**进场 1**
标准的关卡顺序遍历思路在这里略有变化。

1.  我们将一次处理两个节点，而不是一次处理一个节点。
2.  对于出列的节点，我们按照以下方式将节点的左右子节点推入堆栈——第二个节点的左子节点、第一个节点的右子节点、第二个节点的右子节点和第一个节点的左子节点。
3.  当将子节点推入队列时，入队顺序将是:第一个节点的右子节点、第二个节点的左子节点、第一个节点的左子节点和第二个节点的右子节点。另外，当我们处理两个队列节点时。
4.  最后从堆栈中弹出所有节点并打印它们。

## C++

```
/* C++ program for special order traversal */
#include <bits/stdc++.h>
using namespace std;

/* A binary tree node has data, pointer to left child
and a pointer to right child */
struct Node
{
    int data;
    Node *left, *right;
};

/* Helper function that allocates a new node with the
given data and NULL left and right pointers. */
Node* newNode(int data)
{
    Node* node = new Node;
    node->data = data;
    node->right = node->left = NULL;
    return node;
}

void printSpecificLevelOrderUtil(Node* root, stack<Node*> &s)
{
    if (root == NULL)
        return;

    // Create a queue and enqueue left and right
    // children of root
    queue<Node*> q;

    q.push(root->left);
    q.push(root->right);

    // We process two nodes at a time, so we
    // need two variables to store two front
    // items of queue
    Node *first = NULL, *second = NULL;

    // traversal loop
    while (!q.empty())
    {
        // Pop two items from queue
        first = q.front();
        q.pop();
        second = q.front();
        q.pop();

        // Push first and second node's children
        // in reverse order
        s.push(second->left);
        s.push(first->right);
        s.push(second->right);
        s.push(first->left);

        // If first and second have grandchildren,
        // enqueue them in specific order
        if (first->left->left != NULL)
        {
            q.push(first->right);
            q.push(second->left);
            q.push(first->left);
            q.push(second->right);
        }
    }
}

/* Given a perfect binary tree, print its nodes in
specific level order */
void printSpecificLevelOrder(Node* root)
{
    //create a stack and push root
    stack<Node*> s;

    //Push level 1 and level 2 nodes in stack
    s.push(root);

    // Since it is perfect Binary Tree, right is
    // not checked
    if (root->left != NULL)
    {
        s.push(root->right);
        s.push(root->left);
    }

    // Do anything more if there are nodes at next
    // level in given perfect Binary Tree
    if (root->left->left != NULL)
        printSpecificLevelOrderUtil(root, s);

    // Finally pop all Nodes from stack and prints
    // them.
    while (!s.empty())
    {
        cout << s.top()->data << " ";
        s.pop();
    }
}

/* Driver program to test above functions*/
int main()
{
    // Perfect Binary Tree of Height 4
    Node* root = newNode(1);

    root->left = newNode(2);
    root->right = newNode(3);

    /* root->left->left  = newNode(4);
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
    */
    cout << "Specific Level Order traversal of binary "
         "tree is \n";
    printSpecificLevelOrder(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for special order traversal

import java.util.*;

/* A binary tree node has data, pointer to left child
   and a pointer to right child */
class Node
{
    int data;
    Node left, right;

    public Node(int data)
    {
        this.data = data;
        left = right = null;
    }
}

class BinaryTree
{
    Node root;

    void printSpecificLevelOrderUtil(Node root, Stack<Node> s)
    {
        if (root == null)
            return;

        // Create a queue and enqueue left and right
        // children of root
        Queue<Node> q = new LinkedList<Node>();

        q.add(root.left);
        q.add(root.right);

        // We process two nodes at a time, so we
        // need two variables to store two front
        // items of queue
        Node first = null, second = null;

        // traversal loop
        while (!q.isEmpty())
        {
            // Pop two items from queue
            first = q.peek();
            q.poll();
            second = q.peek();
            q.poll();

            // Push first and second node's children
            // in reverse order
            s.push(second.left);
            s.push(first.right);
            s.push(second.right);
            s.push(first.left);

            // If first and second have grandchildren,
            // enqueue them in specific order
            if (first.left.left != null)
            {
                q.add(first.right);
                q.add(second.left);
                q.add(first.left);
                q.add(second.right);
            }
        }
    }

    /* Given a perfect binary tree, print its nodes in
       specific level order */
    void printSpecificLevelOrder(Node root)
    {
        //create a stack and push root
        Stack<Node> s = new Stack<Node>();

        //Push level 1 and level 2 nodes in stack
        s.push(root);

        // Since it is perfect Binary Tree, right is
        // not checked
        if (root.left != null)
        {
            s.push(root.right);
            s.push(root.left);
        }

        // Do anything more if there are nodes at next
        // level in given perfect Binary Tree
        if (root.left.left != null)
            printSpecificLevelOrderUtil(root, s);

        // Finally pop all Nodes from stack and prints
        // them.
        while (!s.empty())
        {
            System.out.print(s.peek().data + " ");
            s.pop();
        }
    }

    // Driver program to test the above functions
    public static void main(String[] args)
    {
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(1);
        tree.root.left = new Node(2);
        tree.root.right = new Node(3);

        /*  tree.root.left.left  = new Node(4);
        tree.root.left.right = new Node(5);
        tree.root.right.left  = new Node(6);
        tree.root.right.right = new Node(7);

        tree.root.left.left.left  = new Node(8);
        tree.root.left.left.right  = new Node(9);
        tree.root.left.right.left  = new Node(10);
        tree.root.left.right.right  = new Node(11);
        tree.root.right.left.left  = new Node(12);
        tree.root.right.left.right  = new Node(13);
        tree.root.right.right.left  = new Node(14);
        tree.root.right.right.right  = new Node(15);

        tree.root.left.left.left.left  = new Node(16);
        tree.root.left.left.left.right  = new Node(17);
        tree.root.left.left.right.left  = new Node(18);
        tree.root.left.left.right.right  = new Node(19);
        tree.root.left.right.left.left  = new Node(20);
        tree.root.left.right.left.right  = new Node(21);
        tree.root.left.right.right.left  = new Node(22);
        tree.root.left.right.right.right  = new Node(23);
        tree.root.right.left.left.left  = new Node(24);
        tree.root.right.left.left.right  = new Node(25);
        tree.root.right.left.right.left  = new Node(26);
        tree.root.right.left.right.right  = new Node(27);
        tree.root.right.right.left.left  = new Node(28);
        tree.root.right.right.left.right  = new Node(29);
        tree.root.right.right.right.left  = new Node(30);
        tree.root.right.right.right.right  = new Node(31);
         */
        System.out.println("Specific Level Order Traversal "
                + "of Binary Tree is ");
        tree.printSpecificLevelOrder(tree.root);
    }
}

// This code has been contributed by Mayank Jaiswal(mayank_24)
```

## 蟒蛇 3

```
# Python program for special order traversal

# A binary tree node
class Node:

    # Create queue and enqueue left
    # and right child of root
    s = []
    q = []

    # Variable to traverse the reversed array
    elements = 0

    # A constructor for making a new node
    def __init__(self, key):
        self.data = key
        self.left = None
        self.right = None

    # Given a perfect binary tree print
    # its node in specific order
    def printSpecificLevelOrder(self, root):
        self.s.append(root)

        # Pop the element from the list
        prnt = self.s.pop(0)
        self.q.append(prnt.data)
        if prnt.right:
            self.s.append(root.right)
        if prnt.left:
            self.s.append(root.left)

        # Traversal loop
        while(len(self.s) > 0):

            # Pop two items from queue
            first = self.s.pop(0)
            self.q.append(first.data)
            second = self.s.pop(0)
            self.q.append(second.data)

            # Since it is perfect Binary tree,
            # one of the node is needed to be checked
            if first.left and second.right and first.right and second.left:

                # If first and second have grandchildren,
                # enqueue them in reverse order
                self.s.append(first.left)
                self.s.append(second.right)
                self.s.append(first.right)
                self.s.append(second.left)

        # Give a perfect binary tree print
        # its node in reverse order
        for elements in reversed(self.q):
            print(elements, end=" ")

# Driver Code
root = Node(1)

root.left = Node(2)
root.right = Node(3)

'''
root.left.left = Node(4)
root.left.right = Node(5)
root.right.left = Node(6)
root.right.right = Node(7)

root.left.left.left = Node(8)
root.left.left.right = Node(9)
root.left.right.left = Node(10)
root.left.right.right = Node(11)
root.right.left.left = Node(12)
root.right.left.right = Node(13)
root.right.right.left = Node(14)
root.right.right.right = Node(15)

root.left.left.left.left = Node(16)
root.left.left.left.right = Node(17)
root.left.left.right.left = Node(18)
root.left.left.right.right = Node(19)
root.left.right.left.left = Node(20)
root.left.right.left.right = Node(21)
root.left.right.right.left = Node(22)
root.left.right.right.right = Node(23)
root.right.left.left.left = Node(24)
root.right.left.left.right = Node(25)
root.right.left.right.left = Node(26)
root.right.left.right.right = Node(27)
root.right.right.left.left = Node(28)
root.right.right.left.right = Node(29)
root.right.right.right.left = Node(30)
root.right.right.right.right = Node(31)
'''
print("Specific Level Order traversal of "
                         "binary tree is")
root.printSpecificLevelOrder(root)

# This code is contributed by 'Vaibhav Kumar 12'
```

## C#

```
// C# program for special order traversal
using System;
using System.Collections.Generic;

/* A binary tree node has data,
pointer to left child and a
pointer to right child */
public class Node
{
    public int data;
    public Node left, right;

    public Node(int data)
    {
        this.data = data;
        left = right = null;
    }
}

class GFG
{
public Node root;

public virtual void printSpecificLevelOrderUtil(Node root,
                                                Stack<Node> s)
{
    if (root == null)
    {
        return;
    }

    // Create a queue and enqueue left
    // and right children of root
    LinkedList<Node> q = new LinkedList<Node>();

    q.AddLast(root.left);
    q.AddLast(root.right);

    // We process two nodes at a time, so we
    // need two variables to store two front
    // items of queue
    Node first = null, second = null;

    // traversal loop
    while (q.Count > 0)
    {
        // Pop two items from queue
        first = q.First.Value;
        q.RemoveFirst();
        second = q.First.Value;
        q.RemoveFirst();

        // Push first and second node's
        // children in reverse order
        s.Push(second.left);
        s.Push(first.right);
        s.Push(second.right);
        s.Push(first.left);

        // If first and second have grandchildren,
        // enqueue them in specific order
        if (first.left.left != null)
        {
            q.AddLast(first.right);
            q.AddLast(second.left);
            q.AddLast(first.left);
            q.AddLast(second.right);
        }
    }
}

/* Given a perfect binary tree,
print its nodes in specific
level order */
public virtual void printSpecificLevelOrder(Node root)
{
    // create a stack and push root
    Stack<Node> s = new Stack<Node>();

    // Push level 1 and level 2
    // nodes in stack
    s.Push(root);

    // Since it is perfect Binary Tree,
    // right is not checked
    if (root.left != null)
    {
        s.Push(root.right);
        s.Push(root.left);
    }

    // Do anything more if there are
    // nodes at next level in given
    // perfect Binary Tree
    if (root.left.left != null)
    {
        printSpecificLevelOrderUtil(root, s);
    }

    // Finally pop all Nodes from
    // stack and prints them.
    while (s.Count > 0)
    {
        Console.Write(s.Peek().data + " ");
        s.Pop();
    }
}

// Driver Code
public static void Main(string[] args)
{
    GFG tree = new GFG();
    tree.root = new Node(1);
    tree.root.left = new Node(2);
    tree.root.right = new Node(3);

    /* tree.root.left.left = new Node(4);
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
    */
    Console.WriteLine("Specific Level Order Traversal " +
                                   "of Binary Tree is ");
    tree.printSpecificLevelOrder(tree.root);
}
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

    // JavaScript program for special order traversal

    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    let root;

    function printSpecificLevelOrderUtil(root, s)
    {
        if (root == null)
            return;

        // Create a queue and enqueue left and right
        // children of root
        let q = [];

        q.push(root.left);
        q.push(root.right);

        // We process two nodes at a time, so we
        // need two variables to store two front
        // items of queue
        let first = null, second = null;

        // traversal loop
        while (q.length > 0)
        {
            // Pop two items from queue
            first = q[0];
            q.shift();
            second = q[0];
            q.shift();

            // Push first and second node's children
            // in reverse order
            s.push(second.left);
            s.push(first.right);
            s.push(second.right);
            s.push(first.left);

            // If first and second have grandchildren,
            // enqueue them in specific order
            if (first.left.left != null)
            {
                q.push(first.right);
                q.push(second.left);
                q.push(first.left);
                q.push(second.right);
            }
        }
    }

    /* Given a perfect binary tree, print its nodes in
       specific level order */
    function printSpecificLevelOrder(root)
    {
        //create a stack and push root
        let s = [];

        //Push level 1 and level 2 nodes in stack
        s.push(root);

        // Since it is perfect Binary Tree, right is
        // not checked
        if (root.left != null)
        {
            s.push(root.right);
            s.push(root.left);
        }

        // Do anything more if there are nodes at next
        // level in given perfect Binary Tree
        if (root.left.left != null)
            printSpecificLevelOrderUtil(root, s);

        // Finally pop all Nodes from stack and prints
        // them.
        while (s.length > 0)
        {
            document.write(s[s.length - 1].data + " ");
            s.pop();
        }
    }

    root = new Node(1);
    root.left = new Node(2);
    root.right = new Node(3);

    document.write("Specific Level Order Traversal "
                + "of Binary Tree is " + "</br>");
        printSpecificLevelOrder(root);

</script>
```

**输出:**

```
Specific Level Order traversal of binary tree is 
2 3 1 
```

**方法 2:** (使用矢量)

1.  我们将从上到下遍历每一层，并将每一层从上到下推至堆栈

2.  这样，我们终于可以向下到向上打印的级别，

3.  我们在向量中有一个水平，所以我们可以以任何定义的方式打印它，

## C++

```
/* C++ program for special order traversal */
#include<bits/stdc++.h>
using namespace std;

/* A binary tree node has data, pointer to left child
and a pointer to right child */
class Node
{
    public:
        int data;
        Node* left;
        Node* right;

        /* Helper function that allocates a new node with the
        given data and NULL left and right pointers. */
        Node(int value)
        {
            data = value;
            left = NULL;
            right = NULL;
        }
};

/* Given a perfect binary tree, print its nodes in
specific level order */
void specific_level_order_traversal(Node* root)
{
    //for level order traversal
    queue <Node*> q;
    // stack to print reverse
    stack < vector <int> > s;

    q.push(root);
    int sz;

    while(!q.empty())
    {
        vector <int> v;    //vector to store the level
        sz = q.size();    //considering size of the level

        for(int i=0;i<sz;++i)
        {
            Node* temp = q.front();
            q.pop();

            //push data of the node of a particular level to vector
            v.push_back(temp->data);

            if(temp->left!=NULL)
            q.push(temp->left);

            if(temp->right!=NULL)
                q.push(temp->right);
        }

        //push vector containing a level in stack
        s.push(v);
    }

    //print the stack
    while(!s.empty())
    {
        // Finally pop all Nodes from stack and prints
        // them.
        vector <int> v = s.top();
        s.pop();
        for(int i=0,j=v.size()-1;i<j;++i)
            {
                cout<<v[i]<<" "<<v[j]<<" ";
                j--;
            }
    }

    //finally print root;
    cout<<root->data;

}

// Driver code
int main()
{
    Node *root = new Node(1);

    root->left = new Node(2);
    root->right = new Node(3);

/*    root->left->left = new Node(4);
    root->left->right = new Node(5);
    root->right->left = new Node(6);
    root->right->right = new Node(7);

    root->left->left->left = new Node(8);
    root->left->left->right = new Node(9);
    root->left->right->left = new Node(10);
    root->left->right->right = new Node(11);
    root->right->left->left = new Node(12);
    root->right->left->right = new Node(13);
    root->right->right->left = new Node(14);
    root->right->right->right = new Node(15);

    root->left->left->left->left = new Node(16);
    root->left->left->left->right = new Node(17);
    root->left->left->right->left = new Node(18);
    root->left->left->right->right = new Node(19);
    root->left->right->left->left = new Node(20);
    root->left->right->left->right = new Node(21);
    root->left->right->right->left = new Node(22);
    root->left->right->right->right = new Node(23);
    root->right->left->left->left = new Node(24);
    root->right->left->left->right = new Node(25);
    root->right->left->right->left = new Node(26);
    root->right->left->right->right = new Node(27);
    root->right->right->left->left = new Node(28);
    root->right->right->left->right = new Node(29);
    root->right->right->right->left = new Node(30);
    root->right->right->right->right = new Node(31);*/
    cout << "Specific Level Order traversal of binary "
        "tree is \n";
    specific_level_order_traversal(root);
    return 0;
}
// This code is contributed by Rachit Yadav.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for special order traversal
import java.util.*;

class GFG
{

/* A binary tree node has data,
pointer to left child and
a pointer to right child */
static class Node
{
    int data;
    Node left;
    Node right;

    /* Helper function that allocates 
    a new node with the given data and
    null left and right pointers. */
    Node(int value)
    {
        data = value;
        left = null;
        right = null;
    }
};

/* Given a perfect binary tree,
print its nodes in specific level order */
static void specific_level_order_traversal(Node root)
{
    // for level order traversal
    Queue <Node> q= new LinkedList<>();

    // Stack to print reverse
    Stack <Vector<Integer>> s = new Stack<Vector<Integer>>();

    q.add(root);
    int sz;

    while(q.size() > 0)
    {
        // vector to store the level
        Vector<Integer> v = new Vector<Integer>();
        sz = q.size(); // considering size of the level

        for(int i = 0; i < sz; ++i)
        {
            Node temp = q.peek();
            q.remove();

            // push data of the node of a
            // particular level to vector
            v.add(temp.data);

            if(temp.left != null)
            q.add(temp.left);

            if(temp.right != null)
                q.add(temp.right);
        }

        // push vector containing a level in Stack
        s.push(v);
    }

    // print the Stack
    while(s.size() > 0)
    {
        // Finally pop all Nodes from Stack
        // and prints them.
        Vector <Integer> v = s.peek();
        s.pop();
        for(int i = 0, j = v.size() - 1; i < j; ++i)
            {
                System.out.print(v.get(i) + " " +
                                 v.get(j) + " ");
                j--;
            }
    }

    // finally print root;
    System.out.println(root.data);

}

// Driver code
public static void main(String args[])
{
    Node root = new Node(1);

    root.left = new Node(2);
    root.right = new Node(3);

 /* root.left.left = new Node(4);
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
    root.right.right.right.right = new Node(31);*/
    System.out.println("Specific Level Order traversal" +
                                   " of binary tree is");
    specific_level_order_traversal(root);
}
}

// This code is contributed by Arnab Kundu
```

## 计算机编程语言

```
# Python program for special order traversal

# Linked List node
class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Given a perfect binary tree,
# print its nodes in specific level order
def specific_level_order_traversal(root) :

    # for level order traversal
    q = []

    # Stack to print reverse
    s = []

    q.append(root)
    sz = 0

    while(len(q) > 0) :

        # vector to store the level
        v = []
        sz = len(q) # considering size of the level
        i = 0
        while( i < sz) :

            temp = q[0]
            q.pop(0)

            # push data of the node of a
            # particular level to vector
            v.append(temp.data)

            if(temp.left != None) :
                q.append(temp.left)

            if(temp.right != None) :
                q.append(temp.right)

            i = i + 1

        # push vector containing a level in Stack
        s.append(v)

    # print the Stack
    while(len(s) > 0) :

        # Finally pop all Nodes from Stack
        # and prints them.
        v = s[-1]
        s.pop()
        i = 0
        j = len(v) - 1
        while( i < j) :
            print(v[i] , " " , v[j] ,end= " ")
            j = j - 1
            i = i + 1

    # finally print root
    print(root.data)

# Driver code

root = Node(1)

root.left = Node(2)
root.right = Node(3)

print("Specific Level Order traversal of binary tree is")
specific_level_order_traversal(root)

# This code is contributed by Arnab Kundu
```

## C#

```
// C# program for special order traversal
using System;
using System.Collections.Generic;

class GFG
{

/* A binary tree node has data,
pointer to left child and
a pointer to right child */
public class Node
{
    public int data;
    public Node left;
    public Node right;

    /* Helper function that allocates
    a new node with the given data and
    null left and right pointers. */
    public Node(int value)
    {
        data = value;
        left = null;
        right = null;
    }
};

/* Given a perfect binary tree,
print its nodes in specific
level order */
static void specific_level_order_traversal(Node root)
{
    // for level order traversal
    Queue <Node> q = new Queue <Node>();

    // Stack to print reverse
    Stack <List<int>> s = new Stack<List<int>>();

    q.Enqueue(root);
    int sz;

    while(q.Count > 0)
    {
        // vector to store the level
        List<int> v = new List<int>();

        // considering size of the level
        sz = q.Count;

        for(int i = 0; i < sz; ++i)
        {
            Node temp = q.Peek();
            q.Dequeue();

            // push data of the node of a
            // particular level to vector
            v.Add(temp.data);

            if(temp.left != null)
            q.Enqueue(temp.left);

            if(temp.right != null)
                q.Enqueue(temp.right);
        }

        // push vector containing a level in Stack
        s.Push(v);
    }

    // print the Stack
    while(s.Count > 0)
    {
        // Finally pop all Nodes from Stack
        // and prints them.
        List<int> v = s.Peek();
        s.Pop();
        for(int i = 0,
                j = v.Count - 1; i < j; ++i)
        {
            Console.Write(v[i] + " " +
                          v[j] + " ");
            j--;
        }
    }

    // finally print root;
    Console.WriteLine(root.data);
}

// Driver code
public static void Main(String []args)
{
    Node root = new Node(1);

    root.left = new Node(2);
    root.right = new Node(3);

 /* root.left.left = new Node(4);
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
    root.right.right.right.right = new Node(31);*/
    Console.WriteLine("Specific Level Order traversal" +
                                  " of binary tree is");
    specific_level_order_traversal(root);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program for special order traversal

/* A binary tree node has data,
pointer to left child and
a pointer to right child */
class Node
{
    /* Helper function that allocates
    a new node with the given data and
    null left and right pointers. */
    constructor(value)
    {
      this.data = value;
      this.left = null;
      this.right = null;
    }
};

/* Given a perfect binary tree,
print its nodes in specific
level order */
function specific_level_order_traversal(root)
{
    // for level order traversal
    var q = [];

    // Stack to print reverse
    var s = [];

    q.push(root);
    var sz;

    while(q.length > 0)
    {
        // vector to store the level
        var v = [];

        // considering size of the level
        sz = q.length;

        for(var i = 0; i < sz; ++i)
        {
            var temp = q[0];
            q.shift();

            // push data of the node of a
            // particular level to vector
            v.push(temp.data);

            if(temp.left != null)
            q.push(temp.left);

            if(temp.right != null)
                q.push(temp.right);
        }

        // push vector containing a level in Stack
        s.push(v);
    }

    // print the Stack
    while(s.length > 0)
    {
        // Finally pop all Nodes from Stack
        // and prints them.
        var v = s[s.length-1];
        s.pop();
        for(var i = 0,
                j = v.length - 1; i < j; ++i)
        {
            document.write(v[i] + " " +
                          v[j] + " ");
            j--;
        }
    }

    // finally print root;
    document.write(root.data);
}

// Driver code
var root = new Node(1);
root.left = new Node(2);
root.right = new Node(3);
/* root.left.left = new Node(4);
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
root.right.right.right.right = new Node(31);*/
document.write("Specific Level Order traversal" +
                              " of binary tree is<br>");
specific_level_order_traversal(root);

// This code is contributed by itsok.
</script>
```

**输出:**

```
Specific Level Order traversal of binary tree is 
2 3 1 
```

https://www.youtube.com/watch?v=zjDznRE4v

-8

本文由**阿迪蒂亚·戈尔**供稿。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息