# 使用恒定的额外空间连接同级节点

> 原文:[https://www . geesforgeks . org/connect-同层节点-带-o1-extra-space/](https://www.geeksforgeeks.org/connect-nodes-at-same-level-with-o1-extra-space/)

编写一个函数来连接二叉树中同一级别的所有相邻节点。给定二叉树节点的结构如下。

## C

```
struct node {
  int data;
  struct node* left;
  struct node* right;
  struct node* nextRight;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
static class node {
  int data;
  node left;
  node right;
  node nextRight;
}

// This code is contributed by umadevi9616
```

## 蟒蛇 3

```
class newnode:
    def __init__(self,data):
        self.data = data
        self.left = None
        self.right = None
        self.nextRight = None

# this code is contributed by shivanisinghss2110
```

## C#

```
public class Node
{
    public int data;
    public Node left;
    public Node right;
    public Node nextRight;
}

// this code is contributed by shivanisinghss2110
```

## java 描述语言

```
class node {

    constructor()
    {
       this.data = 0;
       this.left = null;
       this.right = null;
       this.nextRight = null;
    }
}

// This code is contributed by importantly.
```

最初，所有的 nextRight 指针都指向垃圾值。您的函数应该将这些指针设置为指向每个节点的下一个右边。您只能使用恒定的额外空间。
**例:**

```
Input Tree
       A
      / \
     B   C
    / \   \
   D   E   F

Output Tree
       A--->NULL
      / \
     B-->C-->NULL
    / \   \
   D-->E-->F-->NULL
```

在[之前的帖子](https://www.geeksforgeeks.org/connect-nodes-at-same-level/)中，我们讨论了两种不同的方法。这两种方法所需的辅助空间不是恒定的。此外，那里讨论的方法 2 只适用于完整的二叉树。
在这篇文章中，我们将首先修改方法 2，使其适用于所有种类的树。之后，我们将从这个方法中移除递归，以便额外的空间成为常数。
**递归解**
在前一篇文章的方法 2 中，我们以预先排序的方式遍历了节点。如果我们在左和右子节点(根，下一个右，左)之前遍历下一个右节点，而不是以预先排序的方式遍历(根，左，右)，那么我们可以确保 I 级的所有节点在 i+1 级节点之前都有下一个右集。让我们考虑以下示例(与[之前的帖子](https://www.geeksforgeeks.org/archives/8631)相同的示例)。对于节点 4 的右子节点，方法 2 失败。在这个方法中，在我们尝试将 nextRight 设置为 9 之前，我们确保 4 的级别(级别 2)上的所有节点都设置了 nextRight。因此，当我们将 nextRight 设置为 9 时，我们会在节点 4 的右侧搜索一个非叶节点(getNextRight()会为我们这样做)。

```
            1            -------------- Level 0
          /    \
        2        3       -------------- Level 1
       / \      /  \
      4   5    6    7    -------------- Level 2
     / \           / \
    8   9        10   11 -------------- Level 3
```

## C

```
// Recursive C program to connect nodes at same level
// using constant extra space
void connectRecur(struct node* p);
struct node *getNextRight(struct node *p);

// Sets the nextRight of root and calls connectRecur() for other nodes
void connect (struct node *p)
{
    // Set the nextRight for root
    p->nextRight = NULL;

    // Set the next right for rest of the nodes (other than root)
    connectRecur(p);
}

/* Set next right of all descendants of p. This function makes sure that
nextRight of nodes ar level i is set before level i+1 nodes. */
void connectRecur(struct node* p)
{
    // Base case
    if (!p)
       return;

    /* Before setting nextRight of left and right children, set nextRight
    of children of other nodes at same level (because we can access
    children of other nodes using p's nextRight only) */
    if (p->nextRight != NULL)
       connectRecur(p->nextRight);

    /* Set the nextRight pointer for p's left child */
    if (p->left)
    {
       if (p->right)
       {
           p->left->nextRight = p->right;
           p->right->nextRight = getNextRight(p);
       }
       else
           p->left->nextRight = getNextRight(p);

       /* Recursively call for next level nodes.  Note that we call only
       for left child. The call for left child will call for right child */
       connectRecur(p->left);
    }

    /* If left child is NULL then first node of next level will either be
      p->right or getNextRight(p) */
    else if (p->right)
    {
        p->right->nextRight = getNextRight(p);
        connectRecur(p->right);
    }
    else
       connectRecur(getNextRight(p));
}

/* This function returns the leftmost child of nodes at the same level as p.
   This function is used to getNExt right of p's right child
   If right child of p is NULL then this can also be used for the left child */
struct node *getNextRight(struct node *p)
{
    struct node *temp = p->nextRight;

    /* Traverse nodes at p's level and find and return
       the first node's first child */
    while(temp != NULL)
    {
        if(temp->left != NULL)
            return temp->left;
        if(temp->right != NULL)
            return temp->right;
        temp = temp->nextRight;
    }

    // If all the nodes at p's level are leaf nodes then return NULL
    return NULL;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Recursive Java program to connect nodes at same level
// using constant extra space

// A binary tree node
class Node
{
    int data;
    Node left, right, nextRight;

    Node(int item)
    {
        data = item;
        left = right = nextRight = null;
    }
}

class BinaryTree
{
    Node root;

    /* Set next right of all descendants of p. This function makes sure that
       nextRight of nodes ar level i is set before level i+1 nodes. */
    void connectRecur(Node p)
    {
        // Base case
        if (p == null)
            return;

        /* Before setting nextRight of left and right children, set nextRight
           of children of other nodes at same level (because we can access
           children of other nodes using p's nextRight only) */
        if (p.nextRight != null)
            connectRecur(p.nextRight);

        /* Set the nextRight pointer for p's left child */
        if (p.left != null)
        {
            if (p.right != null)
            {
                p.left.nextRight = p.right;
                p.right.nextRight = getNextRight(p);
            }
            else
                p.left.nextRight = getNextRight(p);

            /* Recursively call for next level nodes.  Note that we call only
             for left child. The call for left child will call for right child */
            connectRecur(p.left);
        }

        /* If left child is NULL then first node of next level will either be
         p->right or getNextRight(p) */
        else if (p.right != null)
        {
            p.right.nextRight = getNextRight(p);
            connectRecur(p.right);
        }
        else
            connectRecur(getNextRight(p));
    }

    /* This function returns the leftmost child of nodes at the same
       level as p. This function is used to getNExt right of p's right child
       If right child of p is NULL then this can also be used for
       the left child */
    Node getNextRight(Node p)
    {
        Node temp = p.nextRight;

        /* Traverse nodes at p's level and find and return
         the first node's first child */
        while (temp != null)
        {
            if (temp.left != null)
                return temp.left;
            if (temp.right != null)
                return temp.right;
            temp = temp.nextRight;
        }

        // If all the nodes at p's level are leaf nodes then return NULL
        return null;
    }

    /* Driver program to test the above functions */
    public static void main(String args[])
    {
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(10);
        tree.root.left = new Node(8);
        tree.root.right = new Node(2);
        tree.root.left.left = new Node(3);
        tree.root.right.right = new Node(90);

        // Populates nextRight pointer in all nodes
        tree.connectRecur(tree.root);

        // Let us check the values of nextRight pointers
        int a = tree.root.nextRight != null ?
                          tree.root.nextRight.data : -1;
        int b = tree.root.left.nextRight != null ?
                          tree.root.left.nextRight.data : -1;
        int c = tree.root.right.nextRight != null ?
                            tree.root.right.nextRight.data : -1;
        int d = tree.root.left.left.nextRight != null ?
                        tree.root.left.left.nextRight.data : -1;
        int e = tree.root.right.right.nextRight != null ?
                        tree.root.right.right.nextRight.data : -1;

        // Now lets print the values
        System.out.println("Following are populated nextRight pointers in "
                + " the tree(-1 is printed if there is no nextRight)");
        System.out.println("nextRight of " + tree.root.data + " is " + a);
        System.out.println("nextRight of " + tree.root.left.data + " is " + b);
        System.out.println("nextRight of " + tree.root.right.data + " is " + c);
        System.out.println("nextRight of " + tree.root.left.left.data +
                                                              " is " + d);
        System.out.println("nextRight of " + tree.root.right.right.data +
                                                              " is " + e);
    }
}

// This code has been contributed by Mayank Jaiswal
```

## C#

```
using System;

// Recursive C# program to connect nodes at same level
// using constant extra space

// A binary tree node
public class Node
{
    public int data;
    public Node left, right, nextRight;

    public Node(int item)
    {
        data = item;
        left = right = nextRight = null;
    }
}

public class BinaryTree
{
    public Node root;

    /* Set next right of all descendants of p. This function makes sure that
       nextRight of nodes ar level i is set before level i+1 nodes. */
    public virtual void connectRecur(Node p)
    {
        // Base case
        if (p == null)
        {
            return;
        }

        /* Before setting nextRight of left and right children, set nextRight
           of children of other nodes at same level (because we can access 
           children of other nodes using p's nextRight only) */
        if (p.nextRight != null)
        {
            connectRecur(p.nextRight);
        }

        /* Set the nextRight pointer for p's left child */
        if (p.left != null)
        {
            if (p.right != null)
            {
                p.left.nextRight = p.right;
                p.right.nextRight = getNextRight(p);
            }
            else
            {
                p.left.nextRight = getNextRight(p);
            }

            /* Recursively call for next level nodes.  Note that we call only
             for left child. The call for left child will call for right child */
            connectRecur(p.left);
        }

        /* If left child is NULL then first node of next level will either be
         p->right or getNextRight(p) */
        else if (p.right != null)
        {
            p.right.nextRight = getNextRight(p);
            connectRecur(p.right);
        }
        else
        {
            connectRecur(getNextRight(p));
        }
    }

    /* This function returns the leftmost child of nodes at the same
       level as p. This function is used to getNExt right of p's right child
       If right child of p is NULL then this can also be used for 
       the left child */
    public virtual Node getNextRight(Node p)
    {
        Node temp = p.nextRight;

        /* Traverse nodes at p's level and find and return
         the first node's first child */
        while (temp != null)
        {
            if (temp.left != null)
            {
                return temp.left;
            }
            if (temp.right != null)
            {
                return temp.right;
            }
            temp = temp.nextRight;
        }

        // If all the nodes at p's level are leaf nodes then return NULL
        return null;
    }

    /* Driver program to test the above functions */
    public static void Main(string[] args)
    {
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(10);
        tree.root.left = new Node(8);
        tree.root.right = new Node(2);
        tree.root.left.left = new Node(3);
        tree.root.right.right = new Node(90);

        // Populates nextRight pointer in all nodes
        tree.connectRecur(tree.root);

        // Let us check the values of nextRight pointers
        int a = tree.root.nextRight != null ? tree.root.nextRight.data : -1;
        int b = tree.root.left.nextRight != null ? tree.root.left.nextRight.data : -1;
        int c = tree.root.right.nextRight != null ? tree.root.right.nextRight.data : -1;
        int d = tree.root.left.left.nextRight != null ? tree.root.left.left.nextRight.data : -1;
        int e = tree.root.right.right.nextRight != null ? tree.root.right.right.nextRight.data : -1;

        // Now lets print the values
        Console.WriteLine("Following are populated nextRight pointers in the tree(-1 is printed if there is no nextRight)");
        Console.WriteLine("nextRight of " + tree.root.data + " is " + a);
        Console.WriteLine("nextRight of " + tree.root.left.data + " is " + b);
        Console.WriteLine("nextRight of " + tree.root.right.data + " is " + c);
        Console.WriteLine("nextRight of " + tree.root.left.left.data + " is " + d);
        Console.WriteLine("nextRight of " + tree.root.right.right.data + " is " + e);
    }
}

  // This code is contributed by Shrikant13
```

## java 描述语言

```
<script>
// Recursive javascript program to connect nodes at same level
// using constant extra space

// A binary tree node
class Node {
        constructor(val) {
            this.data = val;
            this.left = null;
            this.right = null;
            this.nextRight = null;
        }
    }

var root;

    /* Set next right of all descendants of p. This function makes sure that
       nextRight of nodes ar level i is set before level i+1 nodes. */
    function connectRecur(p)
    {
        // Base case
        if (p == null)
            return;

        /* Before setting nextRight of left and right children, set nextRight
           of children of other nodes at same level (because we can access
           children of other nodes using p's nextRight only) */
        if (p.nextRight != null)
            connectRecur(p.nextRight);

        /* Set the nextRight pointer for p's left child */
        if (p.left != null)
        {
            if (p.right != null)
            {
                p.left.nextRight = p.right;
                p.right.nextRight = getNextRight(p);
            }
            else
                p.left.nextRight = getNextRight(p);

            /* Recursively call for next level nodes.  Note that we call only
             for left child. The call for left child will call for right child */
            connectRecur(p.left);
        }

        /* If left child is NULL then first node of next level will either be
         p->right or getNextRight(p) */
        else if (p.right != null)
        {
            p.right.nextRight = getNextRight(p);
            connectRecur(p.right);
        }
        else
            connectRecur(getNextRight(p));
    }

    /* This function returns the leftmost child of nodes at the same
       level as p. This function is used to getNExt right of p's right child
       If right child of p is NULL then this can also be used for
       the left child */
    function getNextRight(p)
    {
        var temp = p.nextRight;

        /* Traverse nodes at p's level and find and return
         the first node's first child */
        while (temp != null)
        {
            if (temp.left != null)
                return temp.left;
            if (temp.right != null)
                return temp.right;
            temp = temp.nextRight;
        }

        // If all the nodes at p's level are leaf nodes then return NULL
        return null;
    }

    /* Driver program to test the above functions */

        var root = new Node(10);
        root.left = new Node(8);
        root.right = new Node(2);
        root.left.left = new Node(3);
        root.right.right = new Node(90);

        // Populates nextRight pointer in all nodes
        connectRecur(root);

        // Let us check the values of nextRight pointers
        var a = root.nextRight != null ?
                          root.nextRight.data : -1;
        var b = root.left.nextRight != null ?
                          root.left.nextRight.data : -1;
        var c = root.right.nextRight != null ?
                            root.right.nextRight.data : -1;
        var d = root.left.left.nextRight != null ?
                        root.left.left.nextRight.data : -1;
        var e = root.right.right.nextRight != null ?
                        root.right.right.nextRight.data : -1;

        // Now lets print the values
        document.write("Following are populated nextRight pointers in "
                + " the tree(-1 is printed if there is no nextRight)");
        document.write("<br/>nextRight of " + root.data + " is " + a);
        document.write("<br/>nextRight of " + root.left.data + " is " + b);
        document.write("<br/>nextRight of " + root.right.data + " is " + c);
        document.write("<br/>nextRight of " + root.left.left.data +
                                                              " is " + d);
        document.write("<br/>nextRight of " + root.right.right.data +
                                                              " is " + e);

// This code is contributed by umadevi9616
</script>
```

**输出:**

```
Following are populated nextRight pointers in the tree (-1 is printed if 
there is no nextRight)
nextRight of 10 is -1
nextRight of 8 is 2
nextRight of 2 is -1
nextRight of 3 is 90
nextRight of 90 is -1
```

**迭代解**
上面讨论的递归方法可以很容易地转换为迭代。在迭代版本中，我们使用嵌套循环。外环穿过所有层，内环穿过每个层的所有节点。该解决方案使用恒定空间。

## C++

```
// Iterative CPP program to connect
// nodes at same level using
// constant extra space
#include<bits/stdc++.h>
#include<bits/stdc++.h>
using namespace std;

class node
{
    public:
    int data;
    node* left;
    node* right;
    node *nextRight;

    /* Constructor that allocates a new node with the
    given data and NULL left and right pointers. */
    node(int data)
    {
        this->data = data;
        this->left = NULL;
        this->right = NULL;
        this->nextRight = NULL;
    }
};

/* This function returns the leftmost
child of nodes at the same level as p.
This function is used to getNExt right
of p's right child  If right child of
is NULL then this can also be used for
the left child */
node *getNextRight(node *p)
{
    node *temp = p->nextRight;

    /* Traverse nodes at p's level
    and find and return the first
    node's first child */
    while (temp != NULL)
    {
        if (temp->left != NULL)
            return temp->left;
        if (temp->right != NULL)
            return temp->right;
        temp = temp->nextRight;
    }

    // If all the nodes at p's level
    // are leaf nodes then return NULL
    return NULL;
}

/* Sets nextRight of all nodes
of a tree with root as p */
void connectRecur(node* p)
{
    node *temp;

    if (!p)
    return;

    // Set nextRight for root
    p->nextRight = NULL;

    // set nextRight of all levels one by one
    while (p != NULL)
    {
        node *q = p;

        /* Connect all children nodes of p and
        children nodes of all other nodes at
        same level as p */
        while (q != NULL)
        {
            // Set the nextRight pointer
            // for p's left child
            if (q->left)
            {
                // If q has right child, then
                // right child is nextRight of
                // p and we also need to set
                // nextRight of right child
                if (q->right)
                    q->left->nextRight = q->right;
                else
                    q->left->nextRight = getNextRight(q);
            }

            if (q->right)
                q->right->nextRight = getNextRight(q);

            // Set nextRight for other
            // nodes in pre order fashion
            q = q->nextRight;
        }

        // start from the first
        // node of next level
        if (p->left)
            p = p->left;
        else if (p->right)
            p = p->right;
        else
            p = getNextRight(p);
    }
}

/* Driver code*/
int main()
{

    /* Constructed binary tree is
            10
            / \
        8 2
        /     \
    3     90
    */
    node *root = new node(10);
    root->left = new node(8);
    root->right = new node(2);
    root->left->left = new node(3);
    root->right->right     = new node(90);

    // Populates nextRight pointer in all nodes
    connectRecur(root);

    // Let us check the values of nextRight pointers
    cout << "Following are populated nextRight pointers in the tree"
        " (-1 is printed if there is no nextRight) \n";
    cout << "nextRight of " << root->data << " is "
        << (root->nextRight? root->nextRight->data: -1) <<endl;
    cout << "nextRight of " << root->left->data << " is "
        << (root->left->nextRight? root->left->nextRight->data: -1) << endl;
    cout << "nextRight of " << root->right->data << " is "
        << (root->right->nextRight? root->right->nextRight->data: -1) << endl;
    cout << "nextRight of " << root->left->left->data<< " is "
        << (root->left->left->nextRight? root->left->left->nextRight->data: -1) << endl;
    cout << "nextRight of " << root->right->right->data << " is "
        << (root->right->right->nextRight? root->right->right->nextRight->data: -1) << endl;
    return 0;
}

// This code is contributed by rathbhupendra
```

## C

```
// Iterative C program to connect nodes at same level
// using constant extra space
#include <stdio.h>
#include <stdlib.h>

struct node
{
    int data;
    struct node *left;
    struct node *right;
    struct node *nextRight;
};

/* This function returns the leftmost child of nodes at the same level as p.
   This function is used to getNExt right of p's right child
   If right child of is NULL then this can also be used for the left child */
struct node *getNextRight(struct node *p)
{
    struct node *temp = p->nextRight;

    /* Traverse nodes at p's level and find and return
       the first node's first child */
    while (temp != NULL)
    {
        if (temp->left != NULL)
            return temp->left;
        if (temp->right != NULL)
            return temp->right;
        temp = temp->nextRight;
    }

    // If all the nodes at p's level are leaf nodes then return NULL
    return NULL;
}

/* Sets nextRight of all nodes of a tree with root as p */
void connect(struct node* p)
{
    struct node *temp;

    if (!p)
      return;

    // Set nextRight for root
    p->nextRight = NULL;

    // set nextRight of all levels one by one
    while (p != NULL)
    {
        struct node *q = p;

        /* Connect all children nodes of p and children nodes of all other nodes
          at same level as p */
        while (q != NULL)
        {
            // Set the nextRight pointer for p's left child
            if (q->left)
            {
                // If q has right child, then right child is nextRight of
                // p and we also need to set nextRight of right child
                if (q->right)
                    q->left->nextRight = q->right;
                else
                    q->left->nextRight = getNextRight(q);
            }

            if (q->right)
                q->right->nextRight = getNextRight(q);

            // Set nextRight for other nodes in pre order fashion
            q = q->nextRight;
        }

        // start from the first node of next level
        if (p->left)
           p = p->left;
        else if (p->right)
           p = p->right;
        else
           p = getNextRight(p);
    }
}

/* UTILITY FUNCTIONS */
/* Helper function that allocates a new node with the
   given data and NULL left and right pointers. */
struct node* newnode(int data)
{
    struct node* node = (struct node*)
                        malloc(sizeof(struct node));
    node->data = data;
    node->left = NULL;
    node->right = NULL;
    node->nextRight = NULL;

    return(node);
}

/* Driver program to test above functions*/
int main()
{

    /* Constructed binary tree is
              10
            /   \
          8      2
        /         \
      3            90
    */
    struct node *root = newnode(10);
    root->left        = newnode(8);
    root->right       = newnode(2);
    root->left->left  = newnode(3);
    root->right->right       = newnode(90);

    // Populates nextRight pointer in all nodes
    connect(root);

    // Let us check the values of nextRight pointers
    printf("Following are populated nextRight pointers in the tree "
           "(-1 is printed if there is no nextRight) \n");
    printf("nextRight of %d is %d \n", root->data,
           root->nextRight? root->nextRight->data: -1);
    printf("nextRight of %d is %d \n", root->left->data,
           root->left->nextRight? root->left->nextRight->data: -1);
    printf("nextRight of %d is %d \n", root->right->data,
           root->right->nextRight? root->right->nextRight->data: -1);
    printf("nextRight of %d is %d \n", root->left->left->data,
           root->left->left->nextRight? root->left->left->nextRight->data: -1);
    printf("nextRight of %d is %d \n", root->right->right->data,
           root->right->right->nextRight? root->right->right->nextRight->data: -1);

    getchar();
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Iterative Java program to connect nodes at same level
// using constant extra space

// A binary tree node
class Node
{
    int data;
    Node left, right, nextRight;

    Node(int item)
    {
        data = item;
        left = right = nextRight = null;
    }
}

class BinaryTree
{
    Node root;

    /* This function returns the leftmost child of nodes at the same level
       as p. This function is used to getNExt right of p's right child
       If right child of is NULL then this can also be used for the
       left child */
    Node getNextRight(Node p)
    {
        Node temp = p.nextRight;

        /* Traverse nodes at p's level and find and return
           the first node's first child */
        while (temp != null)
        {
            if (temp.left != null)
                return temp.left;
            if (temp.right != null)
                return temp.right;
            temp = temp.nextRight;
        }

        // If all the nodes at p's level are leaf nodes then return NULL
        return null;
    }

    /* Sets nextRight of all nodes of a tree with root as p */
    void connect(Node p) {
        Node temp = null;

        if (p == null)
            return;

        // Set nextRight for root
        p.nextRight = null;

        // set nextRight of all levels one by one
        while (p != null)
        {
            Node q = p;

            /* Connect all children nodes of p and children nodes of all other
               nodes at same level as p */
            while (q != null)
            {
                // Set the nextRight pointer for p's left child
                if (q.left != null)
                {

                    // If q has right child, then right child is nextRight of
                    // p and we also need to set nextRight of right child
                    if (q.right != null)
                        q.left.nextRight = q.right;
                    else
                        q.left.nextRight = getNextRight(q);
                }

                if (q.right != null)
                    q.right.nextRight = getNextRight(q);

                // Set nextRight for other nodes in pre order fashion
                q = q.nextRight;
            }

            // start from the first node of next level
            if (p.left != null)
                p = p.left;
            else if (p.right != null)
                p = p.right;
            else
                p = getNextRight(p);
        }
    }

    /* Driver program to test above functions */
    public static void main(String args[])
    {
         /* Constructed binary tree is
                 10
               /   \
             8      2
           /         \
         3            90
        */
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(10);
        tree.root.left = new Node(8);
        tree.root.right = new Node(2);
        tree.root.left.left = new Node(3);
        tree.root.right.right = new Node(90);

        // Populates nextRight pointer in all nodes
        tree.connect(tree.root);

        // Let us check the values of nextRight pointers
        int a = tree.root.nextRight != null ?
                                     tree.root.nextRight.data : -1;
        int b = tree.root.left.nextRight != null ?
                                 tree.root.left.nextRight.data : -1;
        int c = tree.root.right.nextRight != null ?
                                tree.root.right.nextRight.data : -1;
        int d = tree.root.left.left.nextRight != null ?
                                  tree.root.left.left.nextRight.data : -1;
        int e = tree.root.right.right.nextRight != null ?
                                   tree.root.right.right.nextRight.data : -1;

        // Now lets print the values
        System.out.println("Following are populated nextRight pointers in "
                + " the tree(-1 is printed if there is no nextRight)");
        System.out.println("nextRight of " + tree.root.data + " is " + a);
        System.out.println("nextRight of " + tree.root.left.data
                                                       + " is " + b);
        System.out.println("nextRight of " + tree.root.right.data +
                                                           " is " + c);
        System.out.println("nextRight of " + tree.root.left.left.data +
                                                            " is " + d);
        System.out.println("nextRight of " + tree.root.right.right.data +
                                                             " is " + e);
    }
}

// This code has been contributed by Mayank Jaiswal
```

## 蟒蛇 3

```
# Iterative Python program to connect nodes
# at same level using constant extra space

# Helper class that allocates a new node
# with the given data and None left and
# right pointers.
class newnode:
    def __init__(self,data):
        self.data = data
        self.left = None
        self.right = None
        self.nextRight = None

# This function returns the leftmost child of 
# nodes at the same level as p. This function
# is used to getNExt right of p's right child
# If right child of is None then this can also
# be used for the left child
def getNextRight(p):
    temp = p.nextRight

    # Traverse nodes at p's level and find
    # and return the first node's first child
    while (temp != None):
        if (temp.left != None):
            return temp.left
        if (temp.right != None):
            return temp.right
        temp = temp.nextRight

    # If all the nodes at p's level are
    # leaf nodes then return None
    return None

# Sets nextRight of all nodes of a tree
# with root as p
def connect(p):
    temp = None

    if (not p):
        return

    # Set nextRight for root
    p.nextRight = None

    # set nextRight of all levels one by one
    while (p != None):
        q = p

        # Connect all children nodes of p and
        # children nodes of all other nodes
        # at same level as p
        while (q != None):

            # Set the nextRight pointer for
            # p's left child
            if (q.left):

                # If q has right child, then right
                # child is nextRight of p and we
                # also need to set nextRight of
                # right child
                if (q.right):
                    q.left.nextRight = q.right
                else:
                    q.left.nextRight = getNextRight(q)

            if (q.right):
                q.right.nextRight = getNextRight(q)

            # Set nextRight for other nodes in
            # pre order fashion
            q = q.nextRight

        # start from the first node
        # of next level
        if (p.left):
            p = p.left
        elif (p.right):
            p = p.right
        else:
            p = getNextRight(p)

# Driver Code
if __name__ == '__main__':

    # Constructed binary tree is
    #         10
    #     / \
    #     8     2
    # /         \
    # 3         90
    root = newnode(10)
    root.left     = newnode(8)
    root.right     = newnode(2)
    root.left.left = newnode(3)
    root.right.right     = newnode(90)

    # Populates nextRight pointer in all nodes
    connect(root)

    # Let us check the values of nextRight pointers
    print("Following are populated nextRight "
          "pointers in the tree (-1 is printed "
          "if there is no nextRight) \n")
    print("nextRight of", root.data,
                    "is", end = " ")
    if root.nextRight:
        print(root.nextRight.data)
    else:
        print(-1)
    print("nextRight of", root.left.data,
                         "is", end = " ")
    if root.left.nextRight:
        print(root.left.nextRight.data)
    else:
        print(-1)
    print("nextRight of", root.right.data,
                          "is", end = " ")
    if root.right.nextRight:
        print(root.right.nextRight.data)
    else:
        print(-1)
    print("nextRight of", root.left.left.data,
                              "is", end = " ")
    if root.left.left.nextRight:
        print(root.left.left.nextRight.data)
    else:
        print(-1)
    print("nextRight of", root.right.right.data,
                                "is", end = " ")
    if root.right.right.nextRight:
        print(root.right.right.nextRight.data)
    else:
        print(-1)

# This code is contributed by PranchalK
```

## C#

```
using System;

// Iterative c# program to connect nodes at same level
// using constant extra space

// A binary tree node
public class Node
{
    public int data;
    public Node left, right, nextRight;

    public Node(int item)
    {
        data = item;
        left = right = nextRight = null;
    }
}

public class BinaryTree
{
    public Node root;

    /* This function returns the leftmost child of nodes at the same level
       as p. This function is used to getNExt right of p's right child
       If right child of is NULL then this can also be used for the 
       left child */
    public virtual Node getNextRight(Node p)
    {
        Node temp = p.nextRight;

        /* Traverse nodes at p's level and find and return
           the first node's first child */
        while (temp != null)
        {
            if (temp.left != null)
            {
                return temp.left;
            }
            if (temp.right != null)
            {
                return temp.right;
            }
            temp = temp.nextRight;
        }

        // If all the nodes at p's level are leaf nodes then return NULL
        return null;
    }

    /* Sets nextRight of all nodes of a tree with root as p */
    public virtual void connect(Node p)
    {
        Node temp = null;

        if (p == null)
        {
            return;
        }

        // Set nextRight for root
        p.nextRight = null;

        // set nextRight of all levels one by one
        while (p != null)
        {
            Node q = p;

            /* Connect all children nodes of p and children nodes of all other
               nodes at same level as p */
            while (q != null)
            {
                // Set the nextRight pointer for p's left child
                if (q.left != null)
                {

                    // If q has right child, then right child is nextRight of
                    // p and we also need to set nextRight of right child
                    if (q.right != null)
                    {
                        q.left.nextRight = q.right;
                    }
                    else
                    {
                        q.left.nextRight = getNextRight(q);
                    }
                }

                if (q.right != null)
                {
                    q.right.nextRight = getNextRight(q);
                }

                // Set nextRight for other nodes in pre order fashion
                q = q.nextRight;
            }

            // start from the first node of next level
            if (p.left != null)
            {
                p = p.left;
            }
            else if (p.right != null)
            {
                p = p.right;
            }
            else
            {
                p = getNextRight(p);
            }
        }
    }

    /* Driver program to test above functions */
    public static void Main(string[] args)
    {
         /* Constructed binary tree is
                 10
               /   \
             8      2
           /         \
         3            90
        */
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(10);
        tree.root.left = new Node(8);
        tree.root.right = new Node(2);
        tree.root.left.left = new Node(3);
        tree.root.right.right = new Node(90);

        // Populates nextRight pointer in all nodes
        tree.connect(tree.root);

        // Let us check the values of nextRight pointers
        int a = tree.root.nextRight != null ? tree.root.nextRight.data : -1;
        int b = tree.root.left.nextRight != null ? tree.root.left.nextRight.data : -1;
        int c = tree.root.right.nextRight != null ? tree.root.right.nextRight.data : -1;
        int d = tree.root.left.left.nextRight != null ? tree.root.left.left.nextRight.data : -1;
        int e = tree.root.right.right.nextRight != null ? tree.root.right.right.nextRight.data : -1;

        // Now lets print the values
        Console.WriteLine("Following are populated nextRight pointers in " + " the tree(-1 is printed if there is no nextRight)");
        Console.WriteLine("nextRight of " + tree.root.data + " is " + a);
        Console.WriteLine("nextRight of " + tree.root.left.data + " is " + b);
        Console.WriteLine("nextRight of " + tree.root.right.data + " is " + c);
        Console.WriteLine("nextRight of " + tree.root.left.left.data + " is " + d);
        Console.WriteLine("nextRight of " + tree.root.right.right.data + " is " + e);
    }
}

  // This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

    // Iterative Javascript program to connect nodes at same level
    // using constant extra space

    class Node
    {
        constructor(item) {
              this.data = item;
            this.left = null;
            this.right = null;
            this.nextRight = null;
        }
    }

    let root;

    /* This function returns the leftmost
    child of nodes at the same level
    as p. This function is used to getNExt right of p's right child
    If right child of is NULL then this can also be used for the
    left child */
    function getNextRight(p)
    {
        let temp = p.nextRight;

        /* Traverse nodes at p's level and find and return
           the first node's first child */
        while (temp != null)
        {
            if (temp.left != null)
                return temp.left;
            if (temp.right != null)
                return temp.right;
            temp = temp.nextRight;
        }

        // If all the nodes at p's level are
        // leaf nodes then return NULL
        return null;
    }

    /* Sets nextRight of all nodes of a tree with root as p */
    function connect(p) {
        let temp = null;

        if (p == null)
            return;

        // Set nextRight for root
        p.nextRight = null;

        // set nextRight of all levels one by one
        while (p != null)
        {
            let q = p;

            /* Connect all children nodes of p and
               children nodes of all other
               nodes at same level as p */
            while (q != null)
            {
                // Set the nextRight pointer for p's left child
                if (q.left != null)
                {

                    // If q has right child, then
                    // right child is nextRight of
                    // p and we also need to set
                    // nextRight of right child
                    if (q.right != null)
                        q.left.nextRight = q.right;
                    else
                        q.left.nextRight = getNextRight(q);
                }

                if (q.right != null)
                    q.right.nextRight = getNextRight(q);

                // Set nextRight for other nodes
                // in pre order fashion
                q = q.nextRight;
            }

            // start from the first node of next level
            if (p.left != null)
                p = p.left;
            else if (p.right != null)
                p = p.right;
            else
                p = getNextRight(p);
        }
    }

    /* Constructed binary tree is
                 10
               /   \
             8      2
           /         \
         3            90
        */
    root = new Node(10);
    root.left = new Node(8);
    root.right = new Node(2);
    root.left.left = new Node(3);
    root.right.right = new Node(90);

    // Populates nextRight pointer in all nodes
    connect(root);

    // Let us check the values of nextRight pointers
    let a = root.nextRight != null ?
      root.nextRight.data : -1;
    let b = root.left.nextRight != null ?
      root.left.nextRight.data : -1;
    let c = root.right.nextRight != null ?
      root.right.nextRight.data : -1;
    let d = root.left.left.nextRight != null ?
      root.left.left.nextRight.data : -1;
    let e = root.right.right.nextRight != null ?
      root.right.right.nextRight.data : -1;

    // Now lets print the values
    document.write("Following are populated nextRight pointers in "
            + " the tree(-1 is printed if there is no nextRight)" +
                   "</br>");
    document.write("nextRight of " + root.data + " is " + a +
                                  "</br>");
    document.write("nextRight of " + root.left.data
                       + " is " + b + "</br>");
    document.write("nextRight of " + root.right.data +
                       " is " + c + "</br>");
    document.write("nextRight of " + root.left.left.data +
                       " is " + d + "</br>");
    document.write("nextRight of " + root.right.right.data +
                       " is " + e + "</br>");

</script>
```

**输出:**

```
Following are populated nextRight pointers in the tree (-1 is printed if 
there is no nextRight)
nextRight of 10 is -1
nextRight of 8 is 2
nextRight of 2 is -1
nextRight of 3 is 90
nextRight of 90 is -1
```

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。