# 不使用数组将 BST 转换为最小堆

> 原文:[https://www . geesforgeks . org/in-place-convert-BST-in-a-min-heap/](https://www.geeksforgeeks.org/in-place-convert-bst-into-a-min-heap/)

给定一个二叉查找树，在 O(n)时间内将其转换为包含相同元素的最小堆。就地进行。

```
Input: Binary Search Tree
        8
     /    \
    4      12
  /  \     /  \
 2    6   10  14

Output - Min Heap
       2
     /    \
   4        6
 /  \     /   \
8    10  12   14
[Or any other tree that follows Min Heap
 properties and has same keys]
```

如果我们被允许使用额外的空间，我们可以执行有序的树遍历，并将关键字存储在一个辅助数组中。当我们在 BST 上进行有序遍历时，数组将被排序。最后，我们从排序的数组中构造一个完整的二叉树。我们从排序数组中取下一个最小元素，从左到右逐级构造二叉树。构建的二叉树将是一个最小堆。此解决方案在 O(n)时间内有效，但不在原位。
**如何做到到位？**
想法是先把二叉查找树转换成排序链表。我们可以通过以更有序的方式遍历 BST 来做到这一点。我们在当前链表的开头添加节点，并使用指针对指针更新链表的头部。由于我们在开头插入，为了保持排序顺序，我们首先在左子树之前遍历右子树。即进行反向有序遍历。
最后我们通过适当设置左右指针将排序后的链表转换成最小堆。我们可以通过使用队列对部分构建的最小堆树进行级别顺序遍历并同时遍历链表来做到这一点。在每一步中，我们从队列中取出父节点，将链表的下两个节点作为父节点的子节点，并将下两个节点排队。当链表被排序时，保持最小堆属性。
以下是上述思路的实现–

## C++

```
// Program to convert a BST into a Min-Heap
// in O(n) time and in-place
#include <bits/stdc++.h>
using namespace std;

// Node for BST/Min-Heap
struct Node
{
    int data;
    Node *left, *right;
};

// Utility function for allocating node for BST
Node* newNode(int data)
{
    Node* node = new Node;
    node->data = data;
    node->left = node->right = NULL;
    return node;
}

// Utility function to print Min-heap level by level
void printLevelOrder(Node *root)
{
    // Base Case
    if (root == NULL)  return;

    // Create an empty queue for level order traversal
    queue<Node *> q;
    q.push(root);

    while (!q.empty())
    {
        int nodeCount = q.size();
        while (nodeCount > 0)
        {
            Node *node = q.front();
            cout << node->data << " ";
            q.pop();
            if (node->left)
                q.push(node->left);
            if (node->right)
                q.push(node->right);
            nodeCount--;
        }
        cout << endl;
    }
}

// A simple recursive function to convert a given
// Binary Search tree to Sorted Linked List
// root     --> Root of Binary Search Tree
// head_ref --> Pointer to head node of created
//              linked list
void BSTToSortedLL(Node* root, Node** head_ref)
{
    // Base cases
    if(root == NULL)
        return;

    // Recursively convert right subtree
    BSTToSortedLL(root->right, head_ref);

    // insert root into linked list
    root->right = *head_ref;

    // Change left pointer of previous head
    // to point to NULL
    if (*head_ref != NULL)
        (*head_ref)->left = NULL;

    // Change head of linked list
    *head_ref = root;

    // Recursively convert left subtree
    BSTToSortedLL(root->left, head_ref);
}

// Function to convert a sorted Linked
// List to Min-Heap.
// root --> Root of Min-Heap
// head --> Pointer to head node of sorted
//              linked list
void SortedLLToMinHeap(Node* &root, Node* head)
{
    // Base Case
    if (head == NULL)
        return;

    // queue to store the parent nodes
    queue<Node *> q;

    // The first node is always the root node
    root = head;

    // advance the pointer to the next node
    head = head->right;

    // set right child to NULL
    root->right = NULL;

    // add first node to the queue
    q.push(root);

    // run until the end of linked list is reached
    while (head)
    {
        // Take the parent node from the q and remove it from q
        Node* parent = q.front();
        q.pop();

        // Take next two nodes from the linked list and
        // Add them as children of the current parent node
        // Also in push them into the queue so that
        // they will be parents to the future nodes
        Node *leftChild = head;
        head = head->right;        // advance linked list to next node
        leftChild->right = NULL; // set its right child to NULL
        q.push(leftChild);

        // Assign the left child of parent
        parent->left = leftChild;

        if (head)
        {
            Node *rightChild = head;
            head = head->right; // advance linked list to next node
            rightChild->right = NULL; // set its right child to NULL
            q.push(rightChild);

            // Assign the right child of parent
            parent->right = rightChild;
        }
    }
}

// Function to convert BST into a Min-Heap
// without using any extra space
Node* BSTToMinHeap(Node* &root)
{
    // head of Linked List
    Node *head = NULL;

    // Convert a given BST to Sorted Linked List
    BSTToSortedLL(root, &head);

    // set root as NULL
    root = NULL;

    // Convert Sorted Linked List to Min-Heap
    SortedLLToMinHeap(root, head);
}

// Driver code
int main()
{
    /* Constructing below tree
                8
              /   \
             4     12
           /  \   /  \
          2    6 10   14
     */

    Node* root = newNode(8);
    root->left = newNode(4);
    root->right = newNode(12);
    root->right->left = newNode(10);
    root->right->right = newNode(14);
    root->left->left = newNode(2);
    root->left->right = newNode(6);

    BSTToMinHeap(root);

    /* Output - Min Heap
                2
              /   \
             4     6
           /  \   /  \
          8   10 12   14
     */

    printLevelOrder(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to convert a BST into a Min-Heap
// in O(n) time and in-place
import java.util.*;

class GFG
{

// Node for BST/Min-Heap
static class Node
{
    int data;
    Node left, right;
};

// Utility function for allocating node for BST
static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = node.right = null;
    return node;
}

// Utility function to print Min-heap level by level
static void printLevelOrder(Node root)
{
    // Base Case
    if (root == null) return;

    // Create an empty queue for level order traversal
    Queue<Node> q = new LinkedList<>();
    q.add(root);

    while (q.size() > 0)
    {
        int nodeCount = q.size();
        while (nodeCount > 0)
        {
            Node node = q.peek();
            System.out.print( node.data + " ");
            q.remove();
            if (node.left != null)
                q.add(node.left);
            if (node.right != null)
                q.add(node.right);
            nodeCount--;
        }
        System.out.println();
    }
}

// A simple recursive function to convert a given
// Binary Search tree to Sorted Linked List
// root     -. Root of Binary Search Tree
// head_ref -. Pointer to head node of created
//             linked list
static Node BSTToSortedLL(Node root, Node head_ref)
{
    // Base cases
    if(root == null)
        return head_ref;

    // Recursively convert right subtree
    head_ref = BSTToSortedLL(root.right, head_ref);

    // insert root into linked list
    root.right = head_ref;

    // Change left pointer of previous head
    // to point to null
    if (head_ref != null)
        (head_ref).left = null;

    // Change head of linked list
    head_ref = root;

    // Recursively convert left subtree
    head_ref = BSTToSortedLL(root.left, head_ref);
    return head_ref;
}

// Function to convert a sorted Linked
// List to Min-Heap.
// root -. Root of Min-Heap
// head -. Pointer to head node of sorted
//             linked list
static Node SortedLLToMinHeap(Node root, Node head)
{
    // Base Case
    if (head == null)
        return null;

    // queue to store the parent nodes
    Queue<Node > q = new LinkedList<>();

    // The first node is always the root node
    root = head;

    // advance the pointer to the next node
    head = head.right;

    // set right child to null
    root.right = null;

    // add first node to the queue
    q.add(root);

    // run until the end of linked list is reached
    while (head != null)
    {
        // Take the parent node from the q and remove it from q
        Node parent = q.peek();
        q.remove();

        // Take next two nodes from the linked list and
        // Add them as children of the current parent node
        // Also in add them into the queue so that
        // they will be parents to the future nodes
        Node leftChild = head;
        head = head.right;     // advance linked list to next node
        leftChild.right = null; // set its right child to null
        q.add(leftChild);

        // Assign the left child of parent
        parent.left = leftChild;

        if (head != null)
        {
            Node rightChild = head;
            head = head.right; // advance linked list to next node
            rightChild.right = null; // set its right child to null
            q.add(rightChild);

            // Assign the right child of parent
            parent.right = rightChild;
        }
    }
    return root;
}

// Function to convert BST into a Min-Heap
// without using any extra space
static Node BSTToMinHeap(Node root)
{
    // head of Linked List
    Node head = null;

    // Convert a given BST to Sorted Linked List
    head = BSTToSortedLL(root, head);

    // set root as null
    root = null;

    // Convert Sorted Linked List to Min-Heap
    root = SortedLLToMinHeap(root, head);
    return root;
}

// Driver code
public static void main(String args[])
{
    /* Constructing below tree
                8
            / \
            4     12
        / \ / \
        2 6 10 14
    */

    Node root = newNode(8);
    root.left = newNode(4);
    root.right = newNode(12);
    root.right.left = newNode(10);
    root.right.right = newNode(14);
    root.left.left = newNode(2);
    root.left.right = newNode(6);

    root = BSTToMinHeap(root);

    /* Output - Min Heap
                2
            / \
            4     6
        / \ / \
        8 10 12 14
    */

    printLevelOrder(root);
}
}

// This code is contributed by andrew1234
```

## 蟒蛇 3

```
# Python3 prgroam to contrcut all unique
# BSTs for keys from 1 to n

# Binary Tree Node
""" A utility function to create a
new BST node """
class newNode:

    # Construct to create a newNode
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Utility function to print Min-heap
# level by level
def printLevelOrder(root):

    # Base Case
    if (root == None):
        return

    # Create an empty queue for level
    # order traversal
    q = []
    q.append(root)

    while (len(q)):
        nodeCount = len(q)
        while (nodeCount > 0) :

            node = q[0]
            print(node.data, end = " " )
            q.pop(0)
            if (node.left) :
                q.append(node.left)
            if (node.right) :
                q.append(node.right)
            nodeCount -= 1
        print()

# A simple recursive function to convert a
# given Binary Search tree to Sorted Linked
# List root     -. Root of Binary Search Tree
def BSTToSortedLL(root, head_ref):

    # Base cases
    if(root == None) :
        return

    # Recursively convert right subtree
    BSTToSortedLL(root.right, head_ref)

    # insert root into linked list
    root.right = head_ref[0]

    # Change left pointer of previous
    # head to point to None
    if (head_ref[0] != None):
        (head_ref[0]).left = None

    # Change head of linked list
    head_ref[0] = root

    # Recursively convert left subtree
    BSTToSortedLL(root.left, head_ref)

# Function to convert a sorted Linked
# List to Min-Heap.
# root -. root[0] of Min-Heap
# head -. Pointer to head node of
#          sorted linked list
def SortedLLToMinHeap( root, head) :

    # Base Case
    if (head == None) :
        return

    # queue to store the parent nodes
    q = []

    # The first node is always the
    # root node
    root[0] = head[0]

    # advance the pointer to the next node
    head[0] = head[0].right

    # set right child to None
    root[0].right = None

    # add first node to the queue
    q.append(root[0])

    # run until the end of linked list
    # is reached
    while (head[0] != None) :

        # Take the parent node from the q
        # and remove it from q
        parent = q[0]
        q.pop(0)

        # Take next two nodes from the linked
        # list and Add them as children of the
        # current parent node. Also in push them
        # into the queue so that they will be
        # parents to the future nodes
        leftChild = head[0]
        head[0] = head[0].right     # advance linked list to next node
        leftChild.right = None # set its right child to None
        q.append(leftChild)

        # Assign the left child of parent
        parent.left = leftChild

        if (head) :
            rightChild = head[0]
            head[0] = head[0].right # advance linked list to next node
            rightChild.right = None # set its right child to None
            q.append(rightChild)

            # Assign the right child of parent
            parent.right = rightChild

# Function to convert BST into a Min-Heap
# without using any extra space
def BSTToMinHeap(root):

    # head of Linked List
    head = [None]

    # Convert a given BST to Sorted Linked List
    BSTToSortedLL(root, head)

    # set root as None
    root = [None]

    # Convert Sorted Linked List to Min-Heap
    SortedLLToMinHeap(root, head)
    return root

# Driver Code
if __name__ == '__main__':

    """ Constructing below tree
                8
            / \
            4     12
        / \ / \
        2 6 10 14
    """
    root = newNode(8)
    root.left = newNode(4)
    root.right = newNode(12)
    root.right.left = newNode(10)
    root.right.right = newNode(14)
    root.left.left = newNode(2)
    root.left.right = newNode(6)

    root = BSTToMinHeap(root)

    """ Output - Min Heap
                2
            / \
            4     6
        / \ / \
        8 10 12 14
    """
    printLevelOrder(*root)

# This code is contributed by
# Shubham Singh(SHUBHAMSINGH10)
```

## C#

```
// C# Program to convert a BST into a Min-Heap
// in O(n) time and in-place
using System;
using System.Collections.Generic;
public class GFG
{

  // Node for BST/Min-Heap
  public
    class Node
    {
      public
        int data;
      public
        Node left, right;
    };

  // Utility function for allocating node for BST
  static Node newNode(int data)
  {
    Node node = new Node();
    node.data = data;
    node.left = node.right = null;
    return node;
  }

  // Utility function to print Min-heap level by level
  static void printLevelOrder(Node root)
  {

    // Base Case
    if (root == null) return;

    // Create an empty queue for level order traversal
    Queue<Node> q = new Queue<Node>();
    q.Enqueue(root);

    while (q.Count > 0)
    {
      int nodeCount = q.Count;
      while (nodeCount > 0)
      {
        Node node = q.Peek();
        Console.Write( node.data + " ");
        q.Dequeue();
        if (node.left != null)
          q.Enqueue(node.left);
        if (node.right != null)
          q.Enqueue(node.right);
        nodeCount--;
      }
      Console.WriteLine();
    }
  }

  // A simple recursive function to convert a given
  // Binary Search tree to Sorted Linked List
  // root     -. Root of Binary Search Tree
  // head_ref -. Pointer to head node of created
  //             linked list
  static Node BSTToSortedLL(Node root, Node head_ref)
  {

    // Base cases
    if(root == null)
      return head_ref;

    // Recursively convert right subtree
    head_ref = BSTToSortedLL(root.right, head_ref);

    // insert root into linked list
    root.right = head_ref;

    // Change left pointer of previous head
    // to point to null
    if (head_ref != null)
      (head_ref).left = null;

    // Change head of linked list
    head_ref = root;

    // Recursively convert left subtree
    head_ref = BSTToSortedLL(root.left, head_ref);
    return head_ref;
  }

  // Function to convert a sorted Linked
  // List to Min-Heap.
  // root -. Root of Min-Heap
  // head -. Pointer to head node of sorted
  //             linked list
  static Node SortedLLToMinHeap(Node root, Node head)
  {
    // Base Case
    if (head == null)
      return null;

    // queue to store the parent nodes
    Queue<Node > q = new Queue<Node>();

    // The first node is always the root node
    root = head;

    // advance the pointer to the next node
    head = head.right;

    // set right child to null
    root.right = null;

    // add first node to the queue
    q.Enqueue(root);

    // run until the end of linked list is reached
    while (head != null)
    {

      // Take the parent node from the q and remove it from q
      Node parent = q.Peek();
      q.Dequeue();

      // Take next two nodes from the linked list and
      // Add them as children of the current parent node
      // Also in add them into the queue so that
      // they will be parents to the future nodes
      Node leftChild = head;
      head = head.right;     // advance linked list to next node
      leftChild.right = null; // set its right child to null
      q.Enqueue(leftChild);

      // Assign the left child of parent
      parent.left = leftChild;
      if (head != null)
      {
        Node rightChild = head;
        head = head.right; // advance linked list to next node
        rightChild.right = null; // set its right child to null
        q.Enqueue(rightChild);

        // Assign the right child of parent
        parent.right = rightChild;
      }
    }
    return root;
  }

  // Function to convert BST into a Min-Heap
  // without using any extra space
  static Node BSTToMinHeap(Node root)
  {

    // head of Linked List
    Node head = null;

    // Convert a given BST to Sorted Linked List
    head = BSTToSortedLL(root, head);

    // set root as null
    root = null;

    // Convert Sorted Linked List to Min-Heap
    root = SortedLLToMinHeap(root, head);
    return root;
  }

  // Driver code
  public static void Main(String []args)
  {

    /* Constructing below tree
                8
            / \
            4     12
        / \ / \
        2 6 10 14
    */

    Node root = newNode(8);
    root.left = newNode(4);
    root.right = newNode(12);
    root.right.left = newNode(10);
    root.right.right = newNode(14);
    root.left.left = newNode(2);
    root.left.right = newNode(6);

    root = BSTToMinHeap(root);

    /* Output - Min Heap
                2
            / \
            4     6
        / \ / \
        8 10 12 14
    */
    printLevelOrder(root);
  }
}

// This code is contributed by aashish1995
```

## java 描述语言

```
<script>

// Javascript Program to convert a BST into a Min-Heap
// in O(n) time and in-place
// Node for BST/Min-Heap
class Node
{
    constructor()
    {
        this.data = 0;
        this.left = null;
        this.right = null;
    }
};

// Utility function for allocating node for BST
function newNode(data)
{
  var node = new Node();
  node.data = data;
  node.left = node.right = null;
  return node;
}
// Utility function to print Min-heap level by level
function printLevelOrder(root)
{
  // Base Case
  if (root == null) return;
  // Create an empty queue for level order traversal
  var q = [];
  q.push(root);
  while (q.length > 0)
  {
    var nodeCount = q.length;
    while (nodeCount > 0)
    {
      var node = q[0];
      document.write( node.data + " ");
      q.shift();
      if (node.left != null)
        q.push(node.left);
      if (node.right != null)
        q.push(node.right);
      nodeCount--;
    }
    document.write("<br>");
  }
}
// A simple recursive function to convert a given
// Binary Search tree to Sorted Linked List
// root     -. Root of Binary Search Tree
// head_ref -. Pointer to head node of created
//             linked list
function BSTToSortedLL(root, head_ref)
{
  // Base cases
  if(root == null)
    return head_ref;
  // Recursively convert right subtree
  head_ref = BSTToSortedLL(root.right, head_ref);
  // insert root into linked list
  root.right = head_ref;
  // Change left pointer of previous head
  // to point to null
  if (head_ref != null)
    (head_ref).left = null;
  // Change head of linked list
  head_ref = root;
  // Recursively convert left subtree
  head_ref = BSTToSortedLL(root.left, head_ref);
  return head_ref;
}
// Function to convert a sorted Linked
// List to Min-Heap.
// root -. Root of Min-Heap
// head -. Pointer to head node of sorted
//             linked list
function SortedLLToMinHeap( root, head)
{
  // Base Case
  if (head == null)
    return null;
  // queue to store the parent nodes
  var q = [];
  // The first node is always the root node
  root = head;
  // advance the pointer to the next node
  head = head.right;
  // set right child to null
  root.right = null;
  // add first node to the queue
  q.push(root);
  // run until the end of linked list is reached
  while (head != null)
  {
    // Take the parent node from the q and remove it from q
    var parent = q[0];
    q.shift();
    // Take next two nodes from the linked list and
    // Add them as children of the current parent node
    // Also in add them into the queue so that
    // they will be parents to the future nodes
    var leftChild = head;
    head = head.right;     // advance linked list to next node
    leftChild.right = null; // set its right child to null
    q.push(leftChild);
    // Assign the left child of parent
    parent.left = leftChild;
    if (head != null)
    {
      var rightChild = head;
      head = head.right; // advance linked list to next node
      rightChild.right = null; // set its right child to null
      q.push(rightChild);
      // Assign the right child of parent
      parent.right = rightChild;
    }
  }
  return root;
}
// Function to convert BST into a Min-Heap
// without using any extra space
function BSTToMinHeap(root)
{
  // head of Linked List
  var head = null;
  // Convert a given BST to Sorted Linked List
  head = BSTToSortedLL(root, head);
  // set root as null
  root = null;
  // Convert Sorted Linked List to Min-Heap
  root = SortedLLToMinHeap(root, head);
  return root;
}
// Driver code
/* Constructing below tree
            8
        / \
        4     12
    / \ / \
    2 6 10 14
*/
var root = newNode(8);
root.left = newNode(4);
root.right = newNode(12);
root.right.left = newNode(10);
root.right.right = newNode(14);
root.left.left = newNode(2);
root.left.right = newNode(6);
root = BSTToMinHeap(root);
/* Output - Min Heap
            2
        / \
        4     6
    / \ / \
    8 10 12 14
*/
printLevelOrder(root);

</script>
```

**输出:**

```
2 
4 6 
8 10 12 14 
```

本文由**阿迪蒂亚·戈尔**供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如发现任何不正确的地方，请写评论，或者您想分享更多关于上述话题的信息