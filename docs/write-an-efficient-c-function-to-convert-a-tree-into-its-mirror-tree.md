# 将二叉树转换为其镜像树

> 原文:[https://www . geesforgeks . org/write-a-efficient-c-function-to-convert-a-tree-a-to-it-mirror-tree/](https://www.geeksforgeeks.org/write-an-efficient-c-function-to-convert-a-tree-into-its-mirror-tree/)

树的镜像:二叉树 T 的镜像是另一个二叉树 M(T)，所有非叶节点的左右子节点互换。

![MirrorTree1](img/1d400b3adab5b9fbd195ed41164fa688.png)

上图树木互为镜像

**方法 1(递归)**

算法–镜像(树):

```
(1)  Call Mirror for left-subtree    i.e., Mirror(left-subtree)
(2)  Call Mirror for right-subtree  i.e., Mirror(right-subtree)
(3)  Swap left and right subtrees.
          temp = left-subtree
          left-subtree = right-subtree
          right-subtree = temp
```

## C++

```
// C++ program to convert a binary tree
// to its mirror
#include<bits/stdc++.h>
using namespace std;

/* A binary tree node has data, pointer
to left child and a pointer to right child */
struct Node
{
    int data;
    struct Node* left;
    struct Node* right;
};

/* Helper function that allocates a new node with
the given data and NULL left and right pointers. */
struct Node* newNode(int data)
{
    struct Node* node = (struct Node*)
                         malloc(sizeof(struct Node));
    node->data = data;
    node->left = NULL;
    node->right = NULL;

    return(node);
}

/* Change a tree so that the roles of the left and
    right pointers are swapped at every node.

So the tree...
    4
    / \
    2 5
    / \
1 3

is changed to...
    4
    / \
    5 2
        / \
    3 1
*/
void mirror(struct Node* node)
{
    if (node == NULL)
        return;
    else
    {
        struct Node* temp;

        /* do the subtrees */
        mirror(node->left);
        mirror(node->right);

        /* swap the pointers in this node */
        temp     = node->left;
        node->left = node->right;
        node->right = temp;
    }
}

/* Helper function to print
Inorder traversal.*/
void inOrder(struct Node* node)
{
    if (node == NULL)
        return;

    inOrder(node->left);
    cout << node->data << " ";
    inOrder(node->right);
}

// Driver Code
int main()
{
    struct Node *root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);

    /* Print inorder traversal of the input tree */
    cout << "Inorder traversal of the constructed"
         << " tree is" << endl;
    inOrder(root);

    /* Convert tree to its mirror */
    mirror(root);

    /* Print inorder traversal of the mirror tree */
    cout << "\nInorder traversal of the mirror tree"
         << " is \n";
    inOrder(root);

    return 0;
}

// This code is contributed by Akanksha Rai
```

## C

```
// C program to convert a binary tree
// to its mirror
#include<stdio.h>
#include<stdlib.h>

/* A binary tree node has data, pointer
   to left child and a pointer to right child */
struct Node
{
    int data;
    struct Node* left;
    struct Node* right;
};

/* Helper function that allocates a new node with the
   given data and NULL left and right pointers. */
struct Node* newNode(int data)

{
  struct Node* node = (struct Node*)
                       malloc(sizeof(struct Node));
  node->data = data;
  node->left = NULL;
  node->right = NULL;

  return(node);
}

/* Change a tree so that the roles of the  left and
    right pointers are swapped at every node.

 So the tree...
       4
      / \
     2   5
    / \
   1   3

 is changed to...
       4
      / \
     5   2
        / \
       3   1
*/
void mirror(struct Node* node)
{
  if (node==NULL)
    return; 
  else
  {
    struct Node* temp;

    /* do the subtrees */
    mirror(node->left);
    mirror(node->right);

    /* swap the pointers in this node */
    temp        = node->left;
    node->left  = node->right;
    node->right = temp;
  }
}

/* Helper function to print Inorder traversal.*/
void inOrder(struct Node* node)
{
  if (node == NULL)
    return;

  inOrder(node->left);
  printf("%d ", node->data);
  inOrder(node->right);
} 

/* Driver program to test mirror() */
int main()
{
  struct Node *root = newNode(1);
  root->left        = newNode(2);
  root->right       = newNode(3);
  root->left->left  = newNode(4);
  root->left->right = newNode(5);

  /* Print inorder traversal of the input tree */
  printf("Inorder traversal of the constructed"
           " tree is \n");
  inOrder(root);

  /* Convert tree to its mirror */
  mirror(root);

  /* Print inorder traversal of the mirror tree */
  printf("\nInorder traversal of the mirror tree"
         " is \n"); 
  inOrder(root);

  return 0; 
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to convert binary tree into its mirror

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

    void mirror()
    {
        root = mirror(root);
    }

    Node mirror(Node node)
    {
        if (node == null)
            return node;

        /* do the subtrees */
        Node left = mirror(node.left);
        Node right = mirror(node.right);

        /* swap the left and right pointers */
        node.left = right;
        node.right = left;

        return node;
    }

    void inOrder()
    {
        inOrder(root);
    }

    /* Helper function to test mirror(). Given a binary
       search tree, print out its data elements in
       increasing sorted order.*/
    void inOrder(Node node)
    {
        if (node == null)
            return;

        inOrder(node.left);
        System.out.print(node.data + " ");

        inOrder(node.right);
    }

    /* testing for example nodes */
    public static void main(String args[])
    {
        /* creating a binary tree and entering the nodes */
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(1);
        tree.root.left = new Node(2);
        tree.root.right = new Node(3);
        tree.root.left.left = new Node(4);
        tree.root.left.right = new Node(5);

        /* print inorder traversal of the input tree */
        System.out.println("Inorder traversal of input tree is :");
        tree.inOrder();
        System.out.println("");

        /* convert tree to its mirror */
        tree.mirror();

        /* print inorder traversal of the minor tree */
        System.out.println("Inorder traversal of binary tree is : ");
        tree.inOrder();

    }
}
```

## 蟒蛇 3

```
# Python3 program to convert a binary
# tree to its mirror

# Utility function to create a new
# tree node
class newNode:
    def __init__(self,data):
        self.data = data
        self.left = self.right = None

""" Change a tree so that the roles of the
    left and right pointers are swapped at
    every node.

So the tree...
        4
        / \
    2 5
    / \
    1 3

is changed to...
    4
    / \
    5 2
    / \
    3 1
"""
def mirror(node):

    if (node == None):
        return
    else:

        temp = node

        """ do the subtrees """
        mirror(node.left)
        mirror(node.right)

        """ swap the pointers in this node """
        temp = node.left
        node.left = node.right
        node.right = temp

""" Helper function to print Inorder traversal."""
def inOrder(node) :

    if (node == None):
        return

    inOrder(node.left)
    print(node.data, end = " ")
    inOrder(node.right)

# Driver code
if __name__ =="__main__":

    root = newNode(1)
    root.left = newNode(2)
    root.right = newNode(3)
    root.left.left = newNode(4)
    root.left.right = newNode(5)

    """ Print inorder traversal of
        the input tree """
    print("Inorder traversal of the",
               "constructed tree is")
    inOrder(root)

    """ Convert tree to its mirror """
    mirror(root)

    """ Print inorder traversal of
        the mirror tree """
    print("\nInorder traversal of",
              "the mirror treeis ")
    inOrder(root)

# This code is contributed by
# Shubham Singh(SHUBHAMSINGH10)
```

## C#

```
// C# program to convert binary
// tree into its mirror
using System;

// Class containing left and right
// child of current node and key value
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

public virtual void mirror()
{
    root = mirror(root);
}

public virtual Node mirror(Node node)
{
    if (node == null)
    {
        return node;
    }

    /* do the subtrees */
    Node left = mirror(node.left);
    Node right = mirror(node.right);

    /* swap the left and right pointers */
    node.left = right;
    node.right = left;

    return node;
}

public virtual void inOrder()
{
    inOrder(root);
}

/* Helper function to test mirror().
Given a binary search tree, print out its
data elements in increasing sorted order.*/
public virtual void inOrder(Node node)
{
    if (node == null)
    {
        return;
    }

    inOrder(node.left);
    Console.Write(node.data + " ");

    inOrder(node.right);
}

/* testing for example nodes */
public static void Main(string[] args)
{
    /* creating a binary tree and
    entering the nodes */
    GFG tree = new GFG();
    tree.root = new Node(1);
    tree.root.left = new Node(2);
    tree.root.right = new Node(3);
    tree.root.left.left = new Node(4);
    tree.root.left.right = new Node(5);

    /* print inorder traversal of the input tree */
    Console.WriteLine("Inorder traversal " +
                      "of input tree is :");
    tree.inOrder();
    Console.WriteLine("");

    /* convert tree to its mirror */
    tree.mirror();

    /* print inorder traversal of the minor tree */
    Console.WriteLine("Inorder traversal " +
                    "of binary tree is : ");
    tree.inOrder();
}
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

// JavaScript program to convert
// binary tree into its mirror

/* Class containing left and right child of current
   node and key value*/

class Node
{
    constructor(item)
    {
        this.data=item;
        this.left=this.right=null;
    }
}

    let root;

    function mirror(node)
    {
        if (node == null)
            return node;

        /* do the subtrees */
        let left = mirror(node.left);
        let right = mirror(node.right);

        /* swap the left and right pointers */
        node.left = right;
        node.right = left;

        return node;
    }

    /* Helper function to test mirror(). Given a binary
       search tree, print out its data elements in
       increasing sorted order.*/
    function inOrder(node)
    {
        if (node == null)
            return;

        inOrder(node.left);
        document.write(node.data + " ");

        inOrder(node.right);
    }

    /* testing for example nodes */
    /* creating a binary tree and entering the nodes */

        root = new Node(1);
        root.left = new Node(2);
        root.right = new Node(3);
        root.left.left = new Node(4);
        root.left.right = new Node(5);

        /* print inorder traversal of the input tree */
        document.write("Inorder traversal of input tree is :<br>");
        inOrder(root);
        document.write("<br>");

        /* convert tree to its mirror */
        mirror(root);

        /* print inorder traversal of the minor tree */
        document.write(
        "Inorder traversal of binary tree is : <br>"
        );
        inOrder(root);

// This code is contributed by rag2127

</script>
```

**输出:**

```
Inorder traversal of the constructed tree is 
4 2 5 1 3 
Inorder traversal of the mirror tree is 
3 1 5 2 4 
```

**时间&空间复杂度:**最坏的情况时间复杂度是 O(n)，对于空间复杂度，如果我们不考虑函数调用的递归栈的大小，那么 O(1)否则 O(h)，其中 h 是树的高度。这个程序类似于树的遍历空间和时间复杂度将与树遍历相同更多信息请参见我们的[树遍历](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)帖子了解详情。

**方法 2(迭代)**

这个想法是做基于队列的级别顺序遍历。遍历时，交换每个节点的左右子节点。

## C++

```
// Iterative CPP program to convert a Binary
// Tree to its mirror
#include<bits/stdc++.h>
using namespace std;

/* A binary tree node has data, pointer to
   left child and a pointer to right child */
struct Node
{
    int data;
    struct Node* left;
    struct Node* right;
};

/* Helper function that allocates a new node
   with the given data and NULL left and right
   pointers. */
struct Node* newNode(int data)

{
    struct Node* node = new Node;
    node->data = data;
    node->left = node->right = NULL;
    return(node);
}

/* Change a tree so that the roles of the  left and
    right pointers are swapped at every node.
 So the tree...
       4
      / \
     2   5
    / \
   1   3

 is changed to...
       4
      / \
     5   2
        / \
       3   1
*/
void mirror(Node* root)
{
    if (root == NULL)
        return;

    queue<Node*> q;
    q.push(root);

    // Do BFS. While doing BFS, keep swapping
    // left and right children
    while (!q.empty())
    {
        // pop top node from queue
        Node* curr = q.front();
        q.pop();

        // swap left child with right child
        swap(curr->left, curr->right);

        // push left and right children
        if (curr->left)
            q.push(curr->left);
        if (curr->right)
            q.push(curr->right);
    }
}

/* Helper function to print Inorder traversal.*/
void inOrder(struct Node* node)
{
    if (node == NULL)
        return;
    inOrder(node->left);
    cout << node->data << " ";
    inOrder(node->right);
}

/* Driver program to test mirror() */
int main()
{
    struct Node *root = newNode(1);
    root->left        = newNode(2);
    root->right       = newNode(3);
    root->left->left  = newNode(4);
    root->left->right = newNode(5);

    /* Print inorder traversal of the input tree */
    cout << "\n Inorder traversal of the"
            " constructed tree is \n";
    inOrder(root);

    /* Convert tree to its mirror */
    mirror(root);

    /* Print inorder traversal of the mirror tree */
    cout << "\n Inorder traversal of the "
           "mirror tree is \n";
    inOrder(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Iterative Java program to convert a Binary
// Tree to its mirror
import java.util.*;

class GFG
{

/* A binary tree node has data, pointer to
left child and a pointer to right child */
static class Node
{
    int data;
    Node left;
    Node right;
};

/* Helper function that allocates a new node
with the given data and null left and right
pointers. */
static Node newNode(int data)

{
    Node node = new Node();
    node.data = data;
    node.left = node.right = null;
    return(node);
}

/* Change a tree so that the roles of the left and
    right pointers are swapped at every node.
So the tree...
    4
    / \
    2 5
    / \
1 3

is changed to...
    4
    / \
    5 2
        / \
    3 1
*/
static void mirror(Node root)
{
    if (root == null)
        return;

    Queue<Node> q = new LinkedList<>();
    q.add(root);

    // Do BFS. While doing BFS, keep swapping
    // left and right children
    while (q.size() > 0)
    {
        // pop top node from queue
        Node curr = q.peek();
        q.remove();

        // swap left child with right child
        Node temp = curr.left;
        curr.left = curr.right;
        curr.right = temp;;

        // push left and right children
        if (curr.left != null)
            q.add(curr.left);
        if (curr.right != null)
            q.add(curr.right);
    }
}

/* Helper function to print Inorder traversal.*/
static void inOrder( Node node)
{
    if (node == null)
        return;
    inOrder(node.left);
    System.out.print( node.data + " ");
    inOrder(node.right);
}

/* Driver code */
public static void main(String args[])
{
    Node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);

    /* Print inorder traversal of the input tree */
    System.out.print( "\n Inorder traversal of the"
            +" coned tree is \n");
    inOrder(root);

    /* Convert tree to its mirror */
    mirror(root);

    /* Print inorder traversal of the mirror tree */
    System.out.print( "\n Inorder traversal of the "+
        "mirror tree is \n");
    inOrder(root);
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to convert a Binary
# Tree to its mirror

# A binary tree node has data, pointer to
# left child and a pointer to right child
# Helper function that allocates a new node
# with the given data and None left and
# right pointers
class newNode:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

''' Change a tree so that the roles of the left
    and right pointers are swapped at every node.
    So the tree...
        4
        / \
        2 5
        / \
    1 3

    is changed to...
        4
        / \
        5 2
            / \
        3 1
    '''

def mirror( root):

    if (root == None):
        return

    q = []
    q.append(root)

    # Do BFS. While doing BFS, keep swapping
    # left and right children
    while (len(q)):

        # pop top node from queue
        curr = q[0]
        q.pop(0)

        # swap left child with right child
        curr.left, curr.right = curr.right, curr.left

        # append left and right children
        if (curr.left):
            q.append(curr.left)
        if (curr.right):
            q.append(curr.right)

""" Helper function to print Inorder traversal."""
def inOrder( node):
    if (node == None):
        return
    inOrder(node.left)
    print(node.data, end = " ")
    inOrder(node.right)

# Driver code
root = newNode(1)
root.left = newNode(2)
root.right = newNode(3)
root.left.left = newNode(4)
root.left.right = newNode(5)

""" Print inorder traversal of the input tree """
print("Inorder traversal of the constructed tree is")
inOrder(root)

""" Convert tree to its mirror """
mirror(root)

""" Print inorder traversal of the mirror tree """
print("\nInorder traversal of the mirror tree is")
inOrder(root)

# This code is contributed by SHUBHAMSINGH10
```

## C#

```
// C# Iterative Java program to convert a Binary
// Tree to its mirror
using System.Collections.Generic;
using System;

class GFG
{

/* A binary tree node has data, pointer to
left child and a pointer to right child */
public class Node
{
    public int data;
    public Node left;
    public Node right;
};

/* Helper function that allocates a new node
with the given data and null left and right
pointers. */
static Node newNode(int data)

{
    Node node = new Node();
    node.data = data;
    node.left = node.right = null;
    return(node);
}

/* Change a tree so that the roles of the left and
    right pointers are swapped at every node.
So the tree...
    4
    / \
    2 5
    / \
1 3

is changed to...
    4
    / \
    5 2
        / \
    3 1
*/
static void mirror(Node root)
{
    if (root == null)
        return;

    Queue<Node> q = new Queue<Node>();
    q.Enqueue(root);

    // Do BFS. While doing BFS, keep swapping
    // left and right children
    while (q.Count > 0)
    {
        // pop top node from queue
        Node curr = q.Peek();
        q.Dequeue();

        // swap left child with right child
        Node temp = curr.left;
        curr.left = curr.right;
        curr.right = temp;;

        // push left and right children
        if (curr.left != null)
            q.Enqueue(curr.left);
        if (curr.right != null)
            q.Enqueue(curr.right);
    }
}

/* Helper function to print Inorder traversal.*/
static void inOrder( Node node)
{
    if (node == null)
        return;
    inOrder(node.left);
    Console.Write( node.data + " ");
    inOrder(node.right);
}

/* Driver code */
public static void Main(String []args)
{
    Node root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);

    /* Print inorder traversal of the input tree */
    Console.Write( "\n Inorder traversal of the"
            +" coned tree is \n");
    inOrder(root);

    /* Convert tree to its mirror */
    mirror(root);

    /* Print inorder traversal of the mirror tree */
    Console.Write( "\n Inorder traversal of the "+
        "mirror tree is \n");
    inOrder(root);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
    // Iterative Javascript program to convert a Binary
    // Tree to its mirror

    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    /* Helper function that allocates a new node
    with the given data and null left and right
    pointers. */
    function newNode(data)

    {
        let node = new Node(data);
        return(node);
    }

    /* Change a tree so that the roles of the left and
        right pointers are swapped at every node.
    So the tree...
        4
        / \
        2 5
        / \
    1 3

    is changed to...
        4
        / \
        5 2
            / \
        3 1
    */
    function mirror(root)
    {
        if (root == null)
            return;

        let q = [];
        q.push(root);

        // Do BFS. While doing BFS, keep swapping
        // left and right children
        while (q.length > 0)
        {
            // pop top node from queue
            let curr = q[0];
            q.shift();

            // swap left child with right child
            let temp = curr.left;
            curr.left = curr.right;
            curr.right = temp;;

            // push left and right children
            if (curr.left != null)
                q.push(curr.left);
            if (curr.right != null)
                q.push(curr.right);
        }
    }

    /* Helper function to print Inorder traversal.*/
    function inOrder(node)
    {
        if (node == null)
            return;
        inOrder(node.left);
        document.write( node.data + " ");
        inOrder(node.right);
    }

    let root = newNode(1);
    root.left = newNode(2);
    root.right = newNode(3);
    root.left.left = newNode(4);
    root.left.right = newNode(5);

    /* Print inorder traversal of the input tree */
    document.write(" Inorder traversal of the"
            +" constructed tree is " + "</br>");
    inOrder(root);

    /* Convert tree to its mirror */
    mirror(root);

    /* Print inorder traversal of the mirror tree */
    document.write("</br>" + " Inorder traversal of the "+
        "mirror tree is " + "</br>");
    inOrder(root);

</script>
```

**输出:**

```
 Inorder traversal of the constructed tree is 
4 2 5 1 3 
 Inorder traversal of the mirror tree is 
3 1 5 2 4 
```