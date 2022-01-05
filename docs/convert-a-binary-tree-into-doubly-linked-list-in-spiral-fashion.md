# 以螺旋方式将二叉树转换为双链表

> 原文:[https://www . geeksforgeeks . org/convert-a-二叉树-in-double-link-list-in-spiral-fashion/](https://www.geeksforgeeks.org/convert-a-binary-tree-into-doubly-linked-list-in-spiral-fashion/)

给定一棵二叉树，将其转换为双链表，其中节点以螺旋状表示。二叉树节点的左指针应该作为创建的 DLL 的前一个节点，右指针应该作为下一个节点。
解决方案不应该为 DLL 节点分配额外的内存。它应该使用二叉树节点来创建动态链接库，即只允许改变指针

![](img/21c1d16743f62fc7b9b165f0a1af8fd2.png)

例如，对于左侧的树，双链表可以是，
**1**2 3**7 6 5 4**8 9 10 11 13 14 或
1**3 2**4 5 6 7**14 13 11 10 9 8**。
**我们强烈建议您尽量减少浏览器，先自己试试这个。**
我们可以通过在 O(n)个时间和 O(n)个额外空间中进行螺旋顺序遍历来做到这一点。其思想是使用可以在两端(前端或后端)扩展或收缩的 deque(双端队列)。我们做一些类似于级别顺序遍历的事情，但是为了保持螺旋顺序，对于每个奇数级别，我们将节点从前面出列，并将其左右子节点插入到 deque 数据结构的后面。对于每个偶数级别，我们从后面将节点出列，并在 deque 的前面插入它的左右子节点。我们还维护一个堆栈来存储二叉树节点。每当我们从 deque 弹出节点时，我们都会将该节点推入堆栈。稍后，我们从堆栈中弹出所有节点，并将节点推送到列表的开头。如果我们维护一个总是指向 DLL 最后一个节点的尾指针，并在最后的 O(1)时间插入节点，我们可以避免使用堆栈。
以下是上述思路的实施

## C++

```
/* c++ program to convert Binary Tree into Doubly
   Linked List where the nodes are represented
   spirally. */
#include <bits/stdc++.h>
using namespace std;

// A Binary Tree Node
struct Node
{
    int data;
    struct Node *left, *right;
};

/* Given a reference to the head of a list and a node,
inserts the node on the front of the list. */
void push(Node** head_ref, Node* node)
{
    // Make right of given node as head and left as
    // NULL
    node->right = (*head_ref);
    node->left = NULL;

    // change left of head node to given node
    if ((*head_ref) !=  NULL)
        (*head_ref)->left = node ;

    // move the head to point to the given node
    (*head_ref) = node;
}

// Function to prints contents of DLL
void printList(Node *node)
{
    while (node != NULL)
    {
        cout << node->data << " ";
        node = node->right;
    }
}

/* Function to print corner node at each level */
void spiralLevelOrder(Node *root)
{
    // Base Case
    if (root == NULL)
        return;

    // Create an empty deque for doing spiral
    // level order traversal and enqueue root
    deque<Node*> q;
    q.push_front(root);

    // create a stack to store Binary Tree nodes
    // to insert into DLL later
    stack<Node*> stk;

    int level = 0;
    while (!q.empty())
    {
        // nodeCount indicates number of Nodes
        // at current level.
        int nodeCount = q.size();

        // Dequeue all Nodes of current level and
        // Enqueue all Nodes of next level
        if (level&1)    //odd level
        {
            while (nodeCount > 0)
            {
                // dequeue node from front & push it to
                // stack
                Node *node = q.front();
                q.pop_front();
                stk.push(node);

                // insert its left and right children
                // in the back of the deque
                if (node->left != NULL)
                    q.push_back(node->left);
                if (node->right != NULL)
                    q.push_back(node->right);

                nodeCount--;
            }
        }
        else      //even level
        {
            while (nodeCount > 0)
            {
                // dequeue node from the back & push it
                // to stack
                Node *node = q.back();
                q.pop_back();
                stk.push(node);

                // inserts its right and left children
                // in the front of the deque
                if (node->right != NULL)
                    q.push_front(node->right);
                if (node->left != NULL)
                    q.push_front(node->left);
                nodeCount--;
            }
        }
        level++;
    }

    // head pointer for DLL
    Node* head = NULL;

    // pop all nodes from stack and
    // push them in the beginning of the list
    while (!stk.empty())
    {
        push(&head, stk.top());
        stk.pop();
    }

    cout << "Created DLL is:\n";
    printList(head);
}

// Utility function to create a new tree Node
Node* newNode(int data)
{
    Node *temp = new Node;
    temp->data = data;
    temp->left = temp->right = NULL;

    return temp;
}

// Driver program to test above functions
int main()
{
    // Let us create binary tree shown in above diagram
    Node *root =  newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    root->right->left = newNode(6);
    root->right->right = newNode(7);

    root->left->left->left  = newNode(8);
    root->left->left->right  = newNode(9);
    root->left->right->left  = newNode(10);
    root->left->right->right  = newNode(11);
    //root->right->left->left  = newNode(12);
    root->right->left->right  = newNode(13);
    root->right->right->left  = newNode(14);
    //root->right->right->right  = newNode(15);

    spiralLevelOrder(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Java program to convert Binary Tree into Doubly Linked List
   where the nodes are represented spirally */

import java.util.*;

// A binary tree node
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
    Node head;

    /* Given a reference to a node,
       inserts the node on the front of the list. */
    void push(Node node)
    {
        // Make right of given node as head and left as
        // NULL
        node.right = head;
        node.left = null;

        // change left of head node to given node
        if (head != null)
            head.left = node;

        // move the head to point to the given node
        head = node;
    }

    // Function to prints contents of DLL
    void printList(Node node)
    {
        while (node != null)
        {
            System.out.print(node.data + " ");
            node = node.right;
        }
    }

    /* Function to print corner node at each level */
    void spiralLevelOrder(Node root)
    {
        // Base Case
        if (root == null)
            return;

        // Create an empty deque for doing spiral
        // level order traversal and enqueue root
        Deque<Node> q = new LinkedList<Node>();
        q.addFirst(root);

        // create a stack to store Binary Tree nodes
        // to insert into DLL later
        Stack<Node> stk = new Stack<Node>();

        int level = 0;
        while (!q.isEmpty())
        {
            // nodeCount indicates number of Nodes
            // at current level.
            int nodeCount = q.size();

            // Dequeue all Nodes of current level and
            // Enqueue all Nodes of next level
            if ((level & 1) %2 != 0) //odd level
            {
                while (nodeCount > 0)
                {
                    // dequeue node from front & push it to
                    // stack
                    Node node = q.peekFirst();
                    q.pollFirst();
                    stk.push(node);

                    // insert its left and right children
                    // in the back of the deque
                    if (node.left != null)
                        q.addLast(node.left);
                    if (node.right != null)
                        q.addLast(node.right);

                    nodeCount--;
                }
            }
            else //even level
            {
                while (nodeCount > 0)
                {
                    // dequeue node from the back & push it
                    // to stack
                    Node node = q.peekLast();
                    q.pollLast();
                    stk.push(node);

                    // inserts its right and left children
                    // in the front of the deque
                    if (node.right != null)
                        q.addFirst(node.right);
                    if (node.left != null)
                        q.addFirst(node.left);
                    nodeCount--;
                }
            }
            level++;
        }

        // pop all nodes from stack and
        // push them in the beginning of the list
        while (!stk.empty())
        {
            push(stk.peek());
            stk.pop();
        }

        System.out.println("Created DLL is : ");
        printList(head);
    }

    // Driver program to test above functions
    public static void main(String[] args)
    {
        // Let us create binary tree as shown in above diagram
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
        // tree.root.right.left.left = new Node(12);
        tree.root.right.left.right = new Node(13);
        tree.root.right.right.left = new Node(14);
        // tree.root.right.right.right = new Node(15);

        tree.spiralLevelOrder(tree.root);
    }
}

// This code has been contributed by Mayank Jaiswal(mayank_24)
```

## 蟒蛇 3

```
# Python3 program to convert Binary Tree
# into Doubly Linked List where the nodes
# are represented spirally.

# Binary tree node
class newNode:

    # Constructor to create a newNode
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

""" Given a reference to the head of a list
    and a node, inserts the node on the front
    of the list. """
def push(head_ref, node):

    # Make right of given node as
    # head and left as None
    node.right = (head_ref)
    node.left = None

    # change left of head node to
    # given node
    if ((head_ref) != None):
        (head_ref).left = node

    # move the head to point to
    # the given node
    (head_ref) = node

# Function to prints contents of DLL
def printList(node):
    i = 0
    while (i < len(node)):

        print(node[i].data, end = " ")
        i += 1

""" Function to prcorner node at each level """
def spiralLevelOrder(root):

    # Base Case
    if (root == None):
        return

    # Create an empty deque for doing spiral
    # level order traversal and enqueue root
    q = []
    q.append(root)

    # create a stack to store Binary
    # Tree nodes to insert into DLL later
    stk = []

    level = 0
    while (len(q)):

        # nodeCount indicates number of
        # Nodes at current level.
        nodeCount = len(q)

        # Dequeue all Nodes of current level
        # and Enqueue all Nodes of next level
        if (level&1): # odd level
            while (nodeCount > 0):

                # dequeue node from front &
                # push it to stack
                node = q[0]
                q.pop(0)
                stk.append(node)

                # insert its left and right children
                # in the back of the deque
                if (node.left != None):
                    q.append(node.left)
                if (node.right != None):
                    q.append(node.right)

                nodeCount -= 1

        else:     # even level

            while (nodeCount > 0):

                # dequeue node from the back &
                # push it to stack
                node = q[-1]
                q.pop(-1)
                stk.append(node)

                # inserts its right and left
                # children in the front of
                # the deque
                if (node.right != None):
                    q.insert(0, node.right)
                if (node.left != None):
                    q.insert(0, node.left)
                nodeCount -= 1
        level += 1

    # head pointer for DLL
    head = []

    # pop all nodes from stack and push
    # them in the beginning of the list
    while (len(stk)):

        head.append(stk[0])
        stk.pop(0)

    print("Created DLL is:")
    printList(head)

# Driver Code
if __name__ == '__main__':

    """Let us create Binary Tree as
    shown in above example """

    root = newNode(1)
    root.left = newNode(2)
    root.right = newNode(3)
    root.left.left = newNode(4)
    root.left.right = newNode(5)
    root.right.left = newNode(6)
    root.right.right = newNode(7)

    root.left.left.left = newNode(8)
    root.left.left.right = newNode(9)
    root.left.right.left = newNode(10)
    root.left.right.right = newNode(11)
    #root.right.left.left = newNode(12)
    root.right.left.right = newNode(13)
    root.right.right.left = newNode(14)
    #root.right.right.right = newNode(15)

    spiralLevelOrder(root)

# This code is contributed
# by SHUBHAMSINGH10
```

## C#

```
/* C# program to convert Binary Tree into Doubly Linked List
where the nodes are represented spirally */
using System;
using System.Collections.Generic;

// A binary tree node
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

public class BinaryTree
{
    Node root;
    Node head;

    /* Given a reference to a node,
    inserts the node on the front of the list. */
    void push(Node node)
    {
        // Make right of given node as head and left as
        // NULL
        node.right = head;
        node.left = null;

        // change left of head node to given node
        if (head != null)
            head.left = node;

        // move the head to point to the given node
        head = node;
    }

    // Function to prints contents of DLL
    void printList(Node node)
    {
        while (node != null)
        {
            Console.Write(node.data + " ");
            node = node.right;
        }
    }

    /* Function to print corner node at each level */
    void spiralLevelOrder(Node root)
    {
        // Base Case
        if (root == null)
            return;

        // Create an empty deque for doing spiral
        // level order traversal and enqueue root
        LinkedList<Node> q = new LinkedList<Node>();
        q.AddFirst(root);

        // create a stack to store Binary Tree nodes
        // to insert into DLL later
        Stack<Node> stk = new Stack<Node>();

        int level = 0;
        while (q.Count != 0)
        {
            // nodeCount indicates number of Nodes
            // at current level.
            int nodeCount = q.Count;

            // Dequeue all Nodes of current level and
            // Enqueue all Nodes of next level
            if ((level & 1) % 2 != 0) //odd level
            {
                while (nodeCount > 0)
                {
                    // dequeue node from front & push it to
                    // stack
                    Node node = q.First.Value;
                    q.RemoveFirst();
                    stk.Push(node);

                    // insert its left and right children
                    // in the back of the deque
                    if (node.left != null)
                        q.AddLast(node.left);
                    if (node.right != null)
                        q.AddLast(node.right);

                    nodeCount--;
                }
            }
            else //even level
            {
                while (nodeCount > 0)
                {
                    // dequeue node from the back & push it
                    // to stack
                    Node node = q.Last.Value;
                    q.RemoveLast();
                    stk.Push(node);

                    // inserts its right and left children
                    // in the front of the deque
                    if (node.right != null)
                        q.AddFirst(node.right);
                    if (node.left != null)
                        q.AddFirst(node.left);
                    nodeCount--;
                }
            }
            level++;
        }

        // pop all nodes from stack and
        // push them in the beginning of the list
        while (stk.Count != 0)
        {
            push(stk.Peek());
            stk.Pop();
        }

        Console.WriteLine("Created DLL is : ");
        printList(head);
    }

    // Driver program to test above functions
    public static void Main(String[] args)
    {
        // Let us create binary tree as shown in above diagram
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
        // tree.root.right.left.left = new Node(12);
        tree.root.right.left.right = new Node(13);
        tree.root.right.right.left = new Node(14);
        // tree.root.right.right.right = new Node(15);

        tree.spiralLevelOrder(tree.root);
    }
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

/* Javascript program to convert Binary Tree into Doubly Linked List
where the nodes are represented spirally */

// A binary tree node
class Node
{
  constructor(data)
  {
      this.data = data;
      this.left = null;
      this.right = null;
  }
}

var root = null;
var head = null;
/* Given a reference to a node,
inserts the node on the front of the list. */
function push(node)
{
    // Make right of given node as head and left as
    // NULL
    node.right = head;
    node.left = null;
    // change left of head node to given node
    if (head != null)
        head.left = node;

    // move the head to point to the given node
    head = node;
}
// Function to prints contents of DLL
function printList(node)
{
    while (node != null)
    {
        document.write(node.data + " ");
        node = node.right;
    }
}
/* Function to print corner node at each level */
function spiralLevelOrder(root)
{
    // Base Case
    if (root == null)
        return;
    // Create an empty deque for doing spiral
    // level order traversal and enqueue root
    var q = [];
    q.unshift(root);
    // create a stack to store Binary Tree nodes
    // to insert into DLL later
    var stk = [];
    var level = 0;
    while (q.length != 0)
    {
        // nodeCount indicates number of Nodes
        // at current level.
        var nodeCount = q.length;
        // Dequeue all Nodes of current level and
        // Enqueue all Nodes of next level
        if ((level & 1) % 2 != 0) //odd level
        {
            while (nodeCount > 0)
            {
                // dequeue node from front & push it to
                // stack
                var node = q[0];
                q.shift();
                stk.push(node);
                // insert its left and right children
                // in the back of the deque
                if (node.left != null)
                    q.push(node.left);
                if (node.right != null)
                    q.push(node.right);
                nodeCount--;
            }
        }
        else //even level
        {
            while (nodeCount > 0)
            {
                // dequeue node from the back & push it
                // to stack
                var node = q[q.length-1];
                q.pop();
                stk.push(node);
                // inserts its right and left children
                // in the front of the deque
                if (node.right != null)
                    q.unshift(node.right);
                if (node.left != null)
                    q.unshift(node.left);
                nodeCount--;
            }
        }
        level++;
    }
    // pop all nodes from stack and
    // push them in the beginning of the list
    while (stk.length != 0)
    {
        push(stk[stk.length-1]);
        stk.pop();
    }
    document.write("Created DLL is :<br>");
    printList(head);
}

// Driver program to test above functions
// Let us create binary tree as shown in above diagram
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
// tree.root.right.left.left = new Node(12);
root.right.left.right = new Node(13);
root.right.right.left = new Node(14);
// tree.root.right.right.right = new Node(15);
spiralLevelOrder(root);

// This code is contributed by itsok.

</script>
```

**输出:**

```
Created DLL is:
1 2 3 7 6 5 4 8 9 10 11 13 14 
```

本文由**阿迪蒂亚·戈尔**供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如发现任何不正确的地方，请写评论，或者您想分享更多关于上述话题的信息