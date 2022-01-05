# Sudo 放置【1.4】| BST 遍历

> 原文:[https://www . geesforgeks . org/sudo-placement 1-4-BST-traversation/](https://www.geeksforgeeks.org/sudo-placement1-4-bst-traversal/)

给定要插入二叉查找树的 N 个元素。任务是构造一个只有插入操作的二叉查找树，最后打印出后序遍历中的元素。BST 是根据元素的到达顺序构造的。

**例:**

```
Input: N elements =  {8, 5, 10, 3, 4, 9, 7}
Output: 4 3 7 5 9 10 8

For the above input, the BST is: 
               8
             /    \
          5         10
        /   \      /
       3     7    9
       \
        4
The post-order traversal of the above BST is 4 3 7 5 9 10 8

```

**方法:**解决这个问题的方法是在 BST 中使用[插入](https://www.geeksforgeeks.org/binary-search-tree-set-1-search-and-insertion/)的方法构建 BST。插入所有节点后，打印树的[后序遍历](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)。

下面是上述方法的实现:

## c++

```
// C++ program to insert nodes
// and print the postorder traversal
#include <bits/stdc++.h>
using namespace std;

// structure to store the BST
struct Node {
    int data;
    Node* left = NULL;
    Node* right = NULL;
};

// locates the memory space
Node* newNode(int key)
{
    Node* temp = new Node;
    temp->data = key;
    temp->left = NULL;
    temp->right = NULL;
    return temp;
}

// inserts node in the BST
Node* insertNode(Node* head, int key)
{
    // if first node
    if (head == NULL)
        head = newNode(key);
    else {
        // move to left
        if (key < head->data)
            head->left = insertNode(head->left, key);
        // move to right
        else
            head->right = insertNode(head->right, key);
    }
    return head;
}

// print the postorder traversal
void posOrder(Node* head)
{
    // leaf node is null
    if (head == NULL)
        return;

    // left
    posOrder(head->left);

    // right
    posOrder(head->right);

    // data
    cout << head->data << " ";
}

// Driver Code
int main()
{

    Node* root = NULL;
    root = insertNode(root, 8);
    root = insertNode(root, 5);
    root = insertNode(root, 10);
    root = insertNode(root, 3);
    root = insertNode(root, 4);
    root = insertNode(root, 9);
    root = insertNode(root, 7);

    // prints the postorder traversal of
    // the tree
    posOrder(root);
    cout << endl;
}
```

## Java

```
// Java program to insert nodes
// and print the postorder traversal
class GFG {

    // structure to store the BST
    static class Node {
        int data;
        Node left = null;
        Node right = null;
    };

    // locates the memory space
    static Node newNode(int key)
    {
        Node temp = new Node();
        temp.data = key;
        temp.left = null;
        temp.right = null;
        return temp;
    }

    // inserts node in the BST
    static Node insertNode(Node head, int key)
    {
        // if first node
        if (head == null)
            head = newNode(key);
        else {
            // move to left
            if (key < head.data)
                head.left = insertNode(head.left, key);
            // move to right
            else
                head.right = insertNode(head.right, key);
        }
        return head;
    }

    // print the postorder traversal
    static void posOrder(Node head)
    {
        // leaf node is null
        if (head == null)
            return;

        // left
        posOrder(head.left);

        // right
        posOrder(head.right);

        // data
        System.out.print(head.data + " ");
    }

    // Driver Code
    public static void main(String[] args)
    {
        Node root = new Node();
        root = insertNode(root, 8);
        root = insertNode(root, 5);
        root = insertNode(root, 10);
        root = insertNode(root, 3);
        root = insertNode(root, 4);
        root = insertNode(root, 9);
        root = insertNode(root, 7);

        // prints the postorder traversal of
        // the tree
        posOrder(root);
        System.out.println("");
    }
}

// This code has been contributed by 29AjayKumar
```

## python 3

```
# Python program to insert nodes
# and print the postorder traversal
import math

# structure to store the BST
class Node:
    def __init__(self,data):
        self.data = data
        self.left = None
        self.right=None

# locates the memory space
def newNode(key):
    temp = Node(key)
    temp.data = key
    temp.left = None
    temp.right = None
    return temp

# inserts node in the BST
def insertNode(head, key):

    # if first node
    if (head == None):
        head = newNode(key)
    else :

        # move to left
        if (key < head.data):
            head.left = insertNode(head.left, key)

        # move to right
        else:
            head.right = insertNode(head.right, key)

    return head

# print the postorder traversal
def posOrder(head):

    # leaf node is None
    if (head == None):
        return

    # left
    posOrder(head.left)

    # right
    posOrder(head.right)

    # data
    print(head.data,end = " ")

# Driver Code
if __name__=='__main__':
    root = None
    root = insertNode(root, 8)
    root = insertNode(root, 5)
    root = insertNode(root, 10)
    root = insertNode(root, 3)
    root = insertNode(root, 4)
    root = insertNode(root, 9)
    root = insertNode(root, 7)

    # prints the postorder traversal of
    # the tree
    posOrder(root)

# This code is contributed by Srathore
```

## c#

```
// C# program to insert nodes
// and print the postorder traversal
using System;

class GFG {

    // structure to store the BST
    public class Node {
        public int data;
        public Node left = null;
        public Node right = null;
    };

    // locates the memory space
    static Node newNode(int key)
    {
        Node temp = new Node();
        temp.data = key;
        temp.left = null;
        temp.right = null;
        return temp;
    }

    // inserts node in the BST
    static Node insertNode(Node head, int key)
    {
        // if first node
        if (head == null)
            head = newNode(key);
        else {
            // move to left
            if (key < head.data)
                head.left = insertNode(head.left, key);
            // move to right
            else
                head.right = insertNode(head.right, key);
        }
        return head;
    }

    // print the postorder traversal
    static void posOrder(Node head)
    {
        // leaf node is null
        if (head == null)
            return;

        // left
        posOrder(head.left);

        // right
        posOrder(head.right);

        // data
        Console.Write(head.data + " ");
    }

    // Driver Code
    public static void Main(String[] args)
    {
        Node root = new Node();
        root = insertNode(root, 8);
        root = insertNode(root, 5);
        root = insertNode(root, 10);
        root = insertNode(root, 3);
        root = insertNode(root, 4);
        root = insertNode(root, 9);
        root = insertNode(root, 7);

        // prints the postorder traversal of
        // the tree
        posOrder(root);
        Console.WriteLine("");
    }
}

// This code contributed by Rajput-Ji
```

T21

## Javascript

```
<script>

// Javascript program to insert nodes
// and print the postorder traversal

// Structure to store the BST
class Node
{
    constructor()
    {
        this.data = 0;
        this.left = null;
        this.right = null;
    }
};

// Locates the memory space
function newNode(key)
{
    var temp = new Node();
    temp.data = key;
    temp.left = null;
    temp.right = null;
    return temp;
}

// Inserts node in the BST
function insertNode(head, key)
{

    // If first node
    if (head == null)
        head = newNode(key);
    else
    {

        // Move to left
        if (key < head.data)
            head.left = insertNode(head.left, key);

        // Move to right
        else
            head.right = insertNode(head.right, key);
    }
    return head;
}

// Print the postorder traversal
function posOrder(head)
{

    // Leaf node is null
    if (head == null)
        return;

    // Left
    posOrder(head.left);

    // Right
    posOrder(head.right);

    // Data
    document.write(head.data + " ");
}

// Driver Code
var root = null;
root = insertNode(root, 8);
root = insertNode(root, 5);
root = insertNode(root, 10);
root = insertNode(root, 3);
root = insertNode(root, 4);
root = insertNode(root, 9);
root = insertNode(root, 7);

// Prints the postorder traversal of
// the tree
posOrder(root);

document.write("<br>");

// This code is contributed by rutvik_56

</script>
```

**输出:**

```
4 3 7 5 9 10 8
```