# 预排序的莫里斯遍历

> 原文:[https://www . geesforgeks . org/Morris-traversation-for-preorder/](https://www.geeksforgeeks.org/morris-traversal-for-preorder/)

使用莫里斯遍历，我们可以遍历树而不使用堆栈和递归。前序的算法几乎类似于中序的莫里斯遍历。

**1。**..**如果**左子为空，打印当前节点数据。移到右边的孩子。
……。**否则**，使前一个节点的右子节点指向当前节点。出现两种情况:
……**a)**前一个节点的右子节点已经指向当前节点。将右子级设置为空。移动到当前节点的右子节点。
……**b)**右边的孩子为空。将其设置为当前节点。打印当前节点的数据并移动到当前节点的左子节点。
**2。**..迭代，直到当前节点不为空。

下面是上述算法的实现。

## C++

```
// C++ program for Morris Preorder traversal
#include <bits/stdc++.h>
using namespace std;

class node
{
    public:
    int data;
    node *left, *right;
};

/* Helper function that allocates a new node with the
given data and NULL left and right pointers. */
node* newNode(int data)
{
    node* temp = new node();
    temp->data = data;
    temp->left = temp->right = NULL;
    return temp;
}

// Preorder traversal without recursion and without stack
void morrisTraversalPreorder(node* root)
{
    while (root)
    {
        // If left child is null, print the current node data. Move to
        // right child.
        if (root->left == NULL)
        {
            cout<<root->data<<" ";
            root = root->right;
        }
        else
        {
            // Find inorder predecessor
            node* current = root->left;
            while (current->right && current->right != root)
                current = current->right;

            // If the right child of inorder predecessor already points to
            // this node
            if (current->right == root)
            {
                current->right = NULL;
                root = root->right;
            }

            // If right child doesn't point to this node, then print this
            // node and make right child point to this node
            else
            {
                cout<<root->data<<" ";
                current->right = root;
                root = root->left;
            }
        }
    }
}

// Function for Standard preorder traversal
void preorder(node* root)
{
    if (root)
    {
        cout<<root->data<<" ";
        preorder(root->left);
        preorder(root->right);
    }
}

/* Driver program to test above functions*/
int main()
{
    node* root = NULL;

    root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);

    root->left->left = newNode(4);
    root->left->right = newNode(5);

    root->right->left = newNode(6);
    root->right->right = newNode(7);

    root->left->left->left = newNode(8);
    root->left->left->right = newNode(9);

    root->left->right->left = newNode(10);
    root->left->right->right = newNode(11);

    morrisTraversalPreorder(root);

    cout<<endl;
    preorder(root);

    return 0;
}

//This code is contributed by rathbhupendra
```

## C

```
// C program for Morris Preorder traversal
#include <stdio.h>
#include <stdlib.h>

struct node
{
    int data;
    struct node *left, *right;
};

/* Helper function that allocates a new node with the
   given data and NULL left and right pointers. */
struct node* newNode(int data)
{
    struct node* temp = (struct node*) malloc(sizeof(struct node));
    temp->data = data;
    temp->left = temp->right = NULL;
    return temp;
}

// Preorder traversal without recursion and without stack
void morrisTraversalPreorder(struct node* root)
{
    while (root)
    {
        // If left child is null, print the current node data. Move to
        // right child.
        if (root->left == NULL)
        {
            printf( "%d ", root->data );
            root = root->right;
        }
        else
        {
            // Find inorder predecessor
            struct node* current = root->left;
            while (current->right && current->right != root)
                current = current->right;

            // If the right child of inorder predecessor already points to
            // this node
            if (current->right == root)
            {
                current->right = NULL;
                root = root->right;
            }

            // If right child doesn't point to this node, then print this
            // node and make right child point to this node
            else
            {
                printf("%d ", root->data);
                current->right = root;
                root = root->left;
            }
        }
    }
}

// Function for Standard preorder traversal
void preorder(struct node* root)
{
    if (root)
    {
        printf( "%d ", root->data);
        preorder(root->left);
        preorder(root->right);
    }
}

/* Driver program to test above functions*/
int main()
{
    struct node* root = NULL;

    root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);

    root->left->left = newNode(4);
    root->left->right = newNode(5);

    root->right->left = newNode(6);
    root->right->right = newNode(7);

    root->left->left->left = newNode(8);
    root->left->left->right = newNode(9);

    root->left->right->left = newNode(10);
    root->left->right->right = newNode(11);

    morrisTraversalPreorder(root);

    printf("\n");
    preorder(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement Morris preorder traversal

// A binary tree node
class Node {

    int data;
    Node left, right;

    Node(int item) {
        data = item;
        left = right = null;
    }
}

class BinaryTree {

    Node root;

    void morrisTraversalPreorder()
    {
        morrisTraversalPreorder(root);
    }

    // Preorder traversal without recursion and without stack
    void morrisTraversalPreorder(Node node) {
        while (node != null) {

            // If left child is null, print the current node data. Move to
            // right child.
            if (node.left == null) {
                System.out.print(node.data + " ");
                node = node.right;
            } else {

                // Find inorder predecessor
                Node current = node.left;
                while (current.right != null && current.right != node) {
                    current = current.right;
                }

                // If the right child of inorder predecessor
                // already points to this node
                if (current.right == node) {
                    current.right = null;
                    node = node.right;
                }

                // If right child doesn't point to this node, then print
                // this node and make right child point to this node
                else {
                    System.out.print(node.data + " ");
                    current.right = node;
                    node = node.left;
                }
            }
        }
    }

    void preorder()
    {
        preorder(root);
    }

    // Function for Standard preorder traversal
    void preorder(Node node) {
        if (node != null) {
            System.out.print(node.data + " ");
            preorder(node.left);
            preorder(node.right);
        }
    }

    // Driver programs to test above functions
    public static void main(String args[]) {
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
        tree.morrisTraversalPreorder();
        System.out.println("");
        tree.preorder();

    }
}

// this code has been contributed by Mayank Jaiswal
```

## 蟒蛇 3

```
# Python program for Morris Preorder traversal

# A binary tree Node
class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Preorder traversal without
# recursion and without stack
def MorrisTraversal(root):
    curr = root

    while curr:
        # If left child is null, print the
        # current node data. And, update
        # the current pointer to right child.
        if curr.left is None:
            print(curr.data, end= " ")
            curr = curr.right

        else:
            # Find the inorder predecessor
            prev = curr.left

            while prev.right is not None and prev.right is not curr:
                prev = prev.right

            # If the right child of inorder
            # predecessor already points to
            # the current node, update the
            # current with it's right child
            if prev.right is curr:
                prev.right = None
                curr = curr.right

            # else If right child doesn't point
            # to the current node, then print this
            # node's data and update the right child
            # pointer with the current node and update
            # the current with it's left child
            else:
                print (curr.data, end=" ")
                prev.right = curr
                curr = curr.left

# Function for Standard preorder traversal
def preorfer(root):
    if root :
        print(root.data, end = " ")
        preorfer(root.left)
        preorfer(root.right)

# Driver program to test
root = Node(1)
root.left = Node(2)
root.right = Node(3)

root.left.left = Node(4)
root.left.right = Node(5)

root.right.left= Node(6)
root.right.right = Node(7)

root.left.left.left = Node(8)
root.left.left.right = Node(9)

root.left.right.left = Node(10)
root.left.right.right = Node(11)

MorrisTraversal(root)
print("\n")
preorfer(root)

# This code is contributed by 'Aartee'
```

## C#

```
// C# program to implement Morris
// preorder traversal
using System;

// A binary tree node
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

public virtual void morrisTraversalPreorder()
{
    morrisTraversalPreorder(root);
}

// Preorder traversal without
// recursion and without stack
public virtual void morrisTraversalPreorder(Node node)
{
    while (node != null)
    {

        // If left child is null, print the
        // current node data. Move to right child.
        if (node.left == null)
        {
            Console.Write(node.data + " ");
            node = node.right;
        }
        else
        {

            // Find inorder predecessor
            Node current = node.left;
            while (current.right != null &&
                   current.right != node)
            {
                current = current.right;
            }

            // If the right child of inorder predecessor
            // already points to this node
            if (current.right == node)
            {
                current.right = null;
                node = node.right;
            }

            // If right child doesn't point to
            // this node, then print this node
            // and make right child point to this node
            else
            {
                Console.Write(node.data + " ");
                current.right = node;
                node = node.left;
            }
        }
    }
}

public virtual void preorder()
{
    preorder(root);
}

// Function for Standard preorder traversal
public virtual void preorder(Node node)
{
    if (node != null)
    {
        Console.Write(node.data + " ");
        preorder(node.left);
        preorder(node.right);
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
    tree.morrisTraversalPreorder();
    Console.WriteLine("");
    tree.preorder();
}
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

// Javascript program to implement Morris
// preorder traversal

// A binary tree node
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

// Preorder traversal without
// recursion and without stack
function morrisTraversalPreorder(node)
{
    while (node != null)
    {

        // If left child is null, print the
        // current node data. Move to right child.
        if (node.left == null)
        {
            document.write(node.data + " ");
            node = node.right;
        }
        else
        {

            // Find inorder predecessor
            var current = node.left;
            while (current.right != null &&
                   current.right != node)
            {
                current = current.right;
            }

            // If the right child of inorder predecessor
            // already points to this node
            if (current.right == node)
            {
                current.right = null;
                node = node.right;
            }

            // If right child doesn't point to
            // this node, then print this node
            // and make right child point to this node
            else
            {
                document.write(node.data + " ");
                current.right = node;
                node = node.left;
            }
        }
    }
}

// Function for Standard preorder traversal
function preorder(node)
{
    if (node != null)
    {
        document.write(node.data + " ");
        preorder(node.left);
        preorder(node.right);
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
morrisTraversalPreorder(root);
document.write("<br>");
preorder(root);

</script>
```

**输出:**

```
1 2 4 8 9 5 10 11 3 6 7
1 2 4 8 9 5 10 11 3 6 7
```

**限制:**
Morris 遍历在过程中修改树。它在向下移动时建立正确的链接，在向上移动时重置正确的链接。因此，如果不允许写操作，则无法应用该算法。

本文由 [**【阿施·巴恩瓦尔】**](https://www.facebook.com/barnwal.aashish) 编辑，GeeksforGeeks 团队审核。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。