# 连接同级节点

> 原文:[https://www.geeksforgeeks.org/connect-nodes-at-same-level/](https://www.geeksforgeeks.org/connect-nodes-at-same-level/)

编写一个函数来连接二叉树中同一级别的所有相邻节点。给定二叉树节点的结构如下。

## C++

```
struct node {
    int data;
    struct node* left;
    struct node* right;
    struct node* nextRight;
}
```

## C

```
struct node {
    int data;
    struct node* left;
    struct node* right;
    struct node* nextRight;
}
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

最初，所有的 nextRight 指针都指向垃圾值。您的函数应该将这些指针设置为指向每个节点的下一个右边。
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

**方法 1(扩展等级顺序遍历或 BFS)**
考虑[等级顺序遍历](https://www.geeksforgeeks.org/level-order-tree-traversal/)的方法 2。方法 2 可以很容易地扩展到连接相同级别的节点。我们可以增加队列条目来包含节点级别，根节点为 0，根的子节点为 1，依此类推。因此，队列节点现在将包含指向树节点的指针和整数级别。当我们对一个节点进行排队时，我们要确保在队列中为节点设置了正确的级别值。为了设置 nextRight，对于每个节点 N，我们将下一个节点从队列中出列，如果下一个节点的级别号相同，我们将 N 的 nextRight 设置为出列节点的地址，否则我们将 N 的 nextRight 设置为 NULL。
我们初始化一个指向前一个节点的节点 Prev。在遍历同一层的节点时，我们跟踪前一个节点，并在每次迭代中将 nextRight 指针指向当前节点。

## C++

```
/* Iterative program to connect all the adjacent nodes at the same level in a binary tree*/
#include <iostream>
#include<queue>
using namespace std;

// A Binary Tree Node
class node {
public:
    int data;
    node* left;
    node* right;
    node* nextRight;

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
// setting right pointer to next right node
/* 
             10 ----------> NULL
            /  \
          8 --->2 --------> NULL
         /
        3 ----------------> NULL
        */
void connect(node *root)
    {
       //Base condition
       if(root==NULL)
        return;
       // Create an empty queue like level order traversal
       queue<node*> q;
       q.push(root);
       while(!q.empty()){
         // size indicates no. of nodes at current level
           int size=q.size();
         // for keeping track of previous node
           node* prev=NULL;
           while(size--){
               node* temp=q.front();
               q.pop();

               if(temp->left)
                q.push(temp->left);

               if(temp->right)
                q.push(temp->right);

               if(prev!=NULL)
                prev->nextRight=temp;
               prev=temp;
           }
           prev->nextRight=NULL;
       }
    }

int main() {
      /* Constructed binary tree is
             10
            /  \
          8     2
         /
        3
        */
    // Let us create binary tree shown above
    node* root = new node(10);
    root->left = new node(8);
    root->right = new node(2);
    root->left->left = new node(3);
    connect(root);
    // Let us check the values
    // of nextRight pointers
    cout << "Following are populated nextRight pointers in the tree"
            " (-1 is printed if there is no nextRight)\n";
    cout << "nextRight of " << root->data << " is "
         << (root->nextRight ? root->nextRight->data : -1) << endl;
    cout << "nextRight of " << root->left->data << " is "
         << (root->left->nextRight ? root->left->nextRight->data : -1) << endl;
    cout << "nextRight of " << root->right->data << " is "
         << (root->right->nextRight ? root->right->nextRight->data : -1) << endl;
    cout << "nextRight of " << root->left->left->data << " is "
         << (root->left->left->nextRight ? root->left->left->nextRight->data : -1) << endl;
    return 0;
}
// this code is contributed by Kapil Poonia
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;
import java.io.*;
class Node {
    int data;
    Node left, right, nextRight;

    Node(int item)
    {
        data = item;
        left = right = nextRight = null;
    }
}

public class BinaryTree {
    Node root;
    void connect(Node p)
    {
        // initialize queue to hold nodes at same level 
        Queue<Node> q = new LinkedList<>();

        q.add(root); // adding nodes to tehe queue

        Node temp = null; // initializing prev to null
        while (!q.isEmpty()) {
            int n = q.size();
            for (int i = 0; i < n; i++) {
                Node prev = temp;
                temp = q.poll();

                // i > 0 because when i is 0 prev points
                // the last node of previous level, 
                // so we skip it
                if (i > 0)
                    prev.nextRight = temp; 

                if (temp.left != null)
                    q.add(temp.left);

                if (temp.right != null)
                    q.add(temp.right);
            }

            // pointing last node of the nth level to null
            temp.nextRight = null; 
        }
    }

    // Driver program to test above functions
    public static void main(String args[])
    {
        BinaryTree tree = new BinaryTree();

        /* Constructed binary tree is 
             10 
            /  \ 
          8     2 
         / 
        3 
        */
        tree.root = new Node(10);
        tree.root.left = new Node(8);
        tree.root.right = new Node(2);
        tree.root.left.left = new Node(3);

        // Populates nextRight pointer in all nodes
        tree.connect(tree.root);

        // Let us check the values of nextRight pointers
        System.out.println("Following are populated nextRight pointers in "
                           + "the tree"
                           + "(-1 is printed if there is no nextRight)");
        int a = tree.root.nextRight != null ? tree.root.nextRight.data : -1;
        System.out.println("nextRight of " + tree.root.data + " is "
                           + a);
        int b = tree.root.left.nextRight != null ? tree.root.left.nextRight.data : -1;
        System.out.println("nextRight of " + tree.root.left.data + " is "
                           + b);
        int c = tree.root.right.nextRight != null ? tree.root.right.nextRight.data : -1;
        System.out.println("nextRight of " + tree.root.right.data + " is "
                           + c);
        int d = tree.root.left.left.nextRight != null ? tree.root.left.left.nextRight.data : -1;
        System.out.println("nextRight of " + tree.root.left.left.data + " is "
                           + d);
    }
}
// This code has been contributed by Rahul Shakya
```

## C#

```
// C# program to connect nodes 
// at same level 
using System;
using System.Collections.Generic;

class Node
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
    Node root;
    void connect(Node p)
    {
        // initialize queue to hold nodes at same level 
        Queue<Node> q = new Queue<Node>();

        q.Enqueue(root); // adding nodes to tehe queue 

        Node temp = null; // initializing prev to null 
        while (q.Count > 0)
        {
            int n = q.Count;
            for (int i = 0; i < n; i++)
            {
                Node prev = temp;
                temp = q.Dequeue();

                // i > 0 because when i is 0 prev points 
                // the last node of previous level, 
                // so we skip it 
                if (i > 0)
                    prev.nextRight = temp;

                if (temp.left != null)
                    q.Enqueue(temp.left);

                if (temp.right != null)
                    q.Enqueue(temp.right);
            }

            // pointing last node of the nth level to null 
            temp.nextRight = null;
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        BinaryTree tree = new BinaryTree();

        /* Constructed binary tree is 
            10 
            / \ 
        8     2 
        / 
        3 
        */
        tree.root = new Node(10);
        tree.root.left = new Node(8);
        tree.root.right = new Node(2);
        tree.root.left.left = new Node(3);

        // Populates nextRight pointer in all nodes 
        tree.connect(tree.root);

        // Let us check the values of nextRight pointers 
        Console.WriteLine("Following are populated nextRight pointers in "
                        + "the tree"
                        + "(-1 is printed if there is no nextRight)");
        int a = tree.root.nextRight != null ? tree.root.nextRight.data : -1;
        Console.WriteLine("nextRight of " + tree.root.data + " is "
                        + a);
        int b = tree.root.left.nextRight != null ? tree.root.left.nextRight.data : -1;
        Console.WriteLine("nextRight of " + tree.root.left.data + " is "
                        + b);
        int c = tree.root.right.nextRight != null ? tree.root.right.nextRight.data : -1;
        Console.WriteLine("nextRight of " + tree.root.right.data + " is "
                        + c);
        int d = tree.root.left.left.nextRight != null ? tree.root.left.left.nextRight.data : -1;
        Console.WriteLine("nextRight of " + tree.root.left.left.data + " is "
                        + d);

        Console.ReadKey();
    }
}

// This code has been contributed by techno2mahi 
```

## java 描述语言

```
<script>

class Node 
{
    constructor(item)
    {
        this.data = item;
        this.left = this.right = this.nextRight = null;
    }
}

let root;

function connect(p)
{
    // initialize queue to hold nodes at same level
        let q = [];

        q.push(root); // adding nodes to tehe queue

        let temp = null; // initializing prev to null
        while (q.length!=0) {
            let n = q.length;
            for (let i = 0; i < n; i++) {
                let prev = temp;
                temp = q.shift();

                // i > 0 because when i is 0 prev points
                // the last node of previous level,
                // so we skip it
                if (i > 0)
                    prev.nextRight = temp;

                if (temp.left != null)
                    q.push(temp.left);

                if (temp.right != null)
                    q.push(temp.right);
            }

            // pointing last node of the nth level to null
            temp.nextRight = null;
        }
}

// Driver program to test above functions

/* Constructed binary tree is
             10
            /  \
          8     2
         /
        3
        */
root = new Node(10);
root.left = new Node(8);
root.right = new Node(2);
root.left.left = new Node(3);

// Populates nextRight pointer in all nodes
connect(root);

// Let us check the values of nextRight pointers
document.write("Following are populated nextRight pointers in "
                   + "the tree"
                   + "(-1 is printed if there is no nextRight)<br>");
let a = root.nextRight != null ? root.nextRight.data : -1;
document.write("nextRight of " + root.data + " is "
                   + a+"<br>");
let b = root.left.nextRight != null ? root.left.nextRight.data : -1;
document.write("nextRight of " + root.left.data + " is "
                   + b+"<br>");
let c = root.right.nextRight != null ? root.right.nextRight.data : -1;
document.write("nextRight of " + root.right.data + " is "
                   + c+"<br>");
let d = root.left.left.nextRight != null ? root.left.left.nextRight.data : -1;
document.write("nextRight of " + root.left.left.data + " is "
                   + d+"<br>");
// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
Following are populated nextRight pointers in the tree(-1 is printed if there is no nextRight)
nextRight of 10 is -1
nextRight of 8 is 2
nextRight of 2 is -1
nextRight of 3 is -1
```

实现请参考[连接同级节点(级序遍历)](https://www.geeksforgeeks.org/connect-nodes-level-level-order-traversal/)。
时间复杂度:O(n)
**方法 2(扩展预序遍历)**
这种方法只适用于[完全二叉树](http://en.wikipedia.org/wiki/Binary_tree#Types_of_binary_trees)。在这个方法中，我们以预先排序的方式设置下一个权限，以确保父级的下一个权限设置在其子级之前。当我们在节点 p 时，我们设置它的左右子节点的 nextRight。因为树是完全树，所以 p 的左子节点的 nextRight(p->left->next right)将始终是 p 的右子节点，p 的右子节点的 next right(p->right->next right)将始终是 p 的 next right 的左子节点(如果 p 不是其级别中最右边的节点)。如果 p 是最右边的节点，那么 p 的右子节点的 nextRight 将为空。

## C++

```
// CPP program to connect nodes
// at same level using extended
// pre-order traversal
#include <bits/stdc++.h>
#include <iostream>
using namespace std;

class node {
public:
    int data;
    node* left;
    node* right;
    node* nextRight;

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

void connectRecur(node* p);

// Sets the nextRight of
// root and calls connectRecur()
// for other nodes
void connect(node* p)
{
    // Set the nextRight for root
    p->nextRight = NULL;

    // Set the next right for rest of the nodes
    // (other than root)
    connectRecur(p);
}

/* Set next right of all descendants of p. 
Assumption: p is a complete binary tree */
void connectRecur(node* p)
{
    // Base case
    if (!p)
        return;

    // Set the nextRight pointer for p's left child
    if (p->left)
        p->left->nextRight = p->right;

    // Set the nextRight pointer
    // for p's right child p->nextRight
    // will be NULL if p is the right
    // most child at its level
    if (p->right)
        p->right->nextRight = (p->nextRight) ? p->nextRight->left : NULL;

    // Set nextRight for other
    // nodes in pre order fashion
    connectRecur(p->left);
    connectRecur(p->right);
}

/* Driver code*/
int main()
{

    /* Constructed binary tree is 
                10 
            / \ 
            8 2 
        / 
        3 
    */
    node* root = new node(10);
    root->left = new node(8);
    root->right = new node(2);
    root->left->left = new node(3);

    // Populates nextRight pointer in all nodes
    connect(root);

    // Let us check the values
    // of nextRight pointers
    cout << "Following are populated nextRight pointers in the tree"
            " (-1 is printed if there is no nextRight)\n";
    cout << "nextRight of " << root->data << " is "
         << (root->nextRight ? root->nextRight->data : -1) << endl;
    cout << "nextRight of " << root->left->data << " is "
         << (root->left->nextRight ? root->left->nextRight->data : -1) << endl;
    cout << "nextRight of " << root->right->data << " is "
         << (root->right->nextRight ? root->right->nextRight->data : -1) << endl;
    cout << "nextRight of " << root->left->left->data << " is "
         << (root->left->left->nextRight ? root->left->left->nextRight->data : -1) << endl;
    return 0;
}

// This code is contributed by rathbhupendra
```

## C

```
// C program to connect nodes at same level using extended
// pre-order traversal
#include <stdio.h>
#include <stdlib.h>

struct node {
    int data;
    struct node* left;
    struct node* right;
    struct node* nextRight;
};

void connectRecur(struct node* p);

// Sets the nextRight of root and calls connectRecur()
// for other nodes
void connect(struct node* p)
{
    // Set the nextRight for root
    p->nextRight = NULL;

    // Set the next right for rest of the nodes
    // (other than root)
    connectRecur(p);
}

/* Set next right of all descendants of p.
   Assumption:  p is a complete binary tree */
void connectRecur(struct node* p)
{
    // Base case
    if (!p)
        return;

    // Set the nextRight pointer for p's left child
    if (p->left)
        p->left->nextRight = p->right;

    // Set the nextRight pointer for p's right child
    // p->nextRight will be NULL if p is the right
    // most child at its level
    if (p->right)
        p->right->nextRight = (p->nextRight) ? p->nextRight->left : NULL;

    // Set nextRight for other nodes in pre order fashion
    connectRecur(p->left);
    connectRecur(p->right);
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

    return (node);
}

/* Driver program to test above functions*/
int main()
{

    /* Constructed binary tree is
            10
          /   \
        8      2
      /
    3
  */
    struct node* root = newnode(10);
    root->left = newnode(8);
    root->right = newnode(2);
    root->left->left = newnode(3);

    // Populates nextRight pointer in all nodes
    connect(root);

    // Let us check the values of nextRight pointers
    printf("Following are populated nextRight pointers in the tree "
           "(-1 is printed if there is no nextRight) \n");
    printf("nextRight of %d is %d \n", root->data,
           root->nextRight ? root->nextRight->data : -1);
    printf("nextRight of %d is %d \n", root->left->data,
           root->left->nextRight ? root->left->nextRight->data : -1);
    printf("nextRight of %d is %d \n", root->right->data,
           root->right->nextRight ? root->right->nextRight->data : -1);
    printf("nextRight of %d is %d \n", root->left->left->data,
           root->left->left->nextRight ? root->left->left->nextRight->data : -1);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to connect nodes
// at same level using extended
// pre-order traversal
import java.util.*;
class GFG {

    static class node {

        int data;
        node left;
        node right;
        node nextRight;

        /*
         * Constructor that allocates a new node with the given data and null left and
         * right pointers.
         */
        node(int data) {
            this.data = data;
            this.left = null;
            this.right = null;
            this.nextRight = null;
        }
    };

    // Sets the nextRight of
    // root and calls connectRecur()
    // for other nodes
    static void connect(node p) {
        // Set the nextRight for root
        p.nextRight = null;

        // Set the next right for rest of the nodes
        // (other than root)
        connectRecur(p);
    }

    /*
     * Set next right of all descendants of p. Assumption: p is a complete binary
     * tree
     */
    static void connectRecur(node p) {
        // Base case
        if (p == null)
            return;

        // Set the nextRight pointer for p's left child
        if (p.left != null)
            p.left.nextRight = p.right;

        // Set the nextRight pointer
        // for p's right child p.nextRight
        // will be null if p is the right
        // most child at its level
        if (p.right != null)
            p.right.nextRight = (p.nextRight) != null ? p.nextRight.left : null;

        // Set nextRight for other
        // nodes in pre order fashion
        connectRecur(p.left);
        connectRecur(p.right);
    }

    /* Driver code */
    public static void main(String[] args) {

        /*
         * Constructed binary tree is 10 / \ 8 2 / 3
         */
        node root = new node(10);
        root.left = new node(8);
        root.right = new node(2);
        root.left.left = new node(3);

        // Populates nextRight pointer in all nodes
        connect(root);

        // Let us check the values
        // of nextRight pointers
        System.out.print("Following are populated nextRight pointers in the tree"
                + " (-1 is printed if there is no nextRight)\n");
        System.out.print(
                "nextRight of " + root.data + " is " + (root.nextRight != null ? root.nextRight.data : -1) + "\n");
        System.out.print("nextRight of " + root.left.data + " is "
                + (root.left.nextRight != null ? root.left.nextRight.data : -1) + "\n");
        System.out.print("nextRight of " + root.right.data + " is "
                + (root.right.nextRight != null ? root.right.nextRight.data : -1) + "\n");
        System.out.print("nextRight of " + root.left.left.data + " is "
                + (root.left.left.nextRight != null ? root.left.left.nextRight.data : -1) + "\n");
    }
}

// This code is contributed by umadevi9616 
```

## 蟒蛇 3

```
# Python3 program to connect nodes at same 
# level using extended pre-order traversal 

class newnode:
    def __init__(self, data):
        self.data = data
        self.left = self.right = self.nextRight = None

# Sets the nextRight of root and calls 
# connectRecur() for other nodes 
def connect (p):

    # Set the nextRight for root 
    p.nextRight = None

    # Set the next right for rest of
    # the nodes (other than root) 
    connectRecur(p)

# Set next right of all descendants of p. 
# Assumption: p is a complete binary tree 
def connectRecur(p):

    # Base case 
    if (not p):
        return

    # Set the nextRight pointer for p's 
    # left child 
    if (p.left): 
        p.left.nextRight = p.right 

    # Set the nextRight pointer for p's right
    # child p.nextRight will be None if p is 
    # the right most child at its level 
    if (p.right):
        if p.nextRight:
            p.right.nextRight = p.nextRight.left
        else:
            p.right.nextRight = None

    # Set nextRight for other nodes in
    # pre order fashion 
    connectRecur(p.left) 
    connectRecur(p.right)

# Driver Code
if __name__ == '__main__':

    # Constructed binary tree is 
    # 10 
    #     / \ 
    # 8     2 
    # / 
    # 3 
    root = newnode(10) 
    root.left = newnode(8) 
    root.right = newnode(2) 
    root.left.left = newnode(3) 

    # Populates nextRight pointer in all nodes 
    connect(root) 

    # Let us check the values of nextRight pointers 
    print("Following are populated nextRight", 
          "pointers in the tree (-1 is printed",
                    "if there is no nextRight)")
    print("nextRight of", root.data, "is ", end = "")
    if root.nextRight:
        print(root.nextRight.data)
    else:
        print(-1)
    print("nextRight of", root.left.data, "is ", end = "") 
    if root.left.nextRight:
        print(root.left.nextRight.data)
    else:
        print(-1)
    print("nextRight of", root.right.data, "is ", end = "") 
    if root.right.nextRight:
        print(root.right.nextRight.data)
    else:
        print(-1)
    print("nextRight of", root.left.left.data, "is ", end = "") 
    if root.left.left.nextRight:
        print(root.left.left.nextRight.data)
    else:
        print(-1)

# This code is contributed by PranchalK
```

## C#

```
using System;

// C# program to connect nodes at same level using extended
// pre-order traversal

// A binary tree node
public class Node {
    public int data;
    public Node left, right, nextRight;

    public Node(int item)
    {
        data = item;
        left = right = nextRight = null;
    }
}

public class BinaryTree {
    public Node root;

    // Sets the nextRight of root and calls connectRecur()
    // for other nodes
    public virtual void connect(Node p)
    {

        // Set the nextRight for root
        p.nextRight = null;

        // Set the next right for rest of the nodes (other
        // than root)
        connectRecur(p);
    }

    /* Set next right of all descendants of p. 
       Assumption:  p is a complete binary tree */
    public virtual void connectRecur(Node p)
    {
        // Base case
        if (p == null) {
            return;
        }

        // Set the nextRight pointer for p's left child
        if (p.left != null) {
            p.left.nextRight = p.right;
        }

        // Set the nextRight pointer for p's right child
        // p->nextRight will be NULL if p is the right most child
        // at its level
        if (p.right != null) {
            p.right.nextRight = (p.nextRight != null) ? p.nextRight.left : null;
        }

        // Set nextRight for other nodes in pre order fashion
        connectRecur(p.left);
        connectRecur(p.right);
    }

    // Driver program to test above functions
    public static void Main(string[] args)
    {
        BinaryTree tree = new BinaryTree();

        /* Constructed binary tree is 
             10 
            /  \ 
          8     2 
         / 
        3 
        */
        tree.root = new Node(10);
        tree.root.left = new Node(8);
        tree.root.right = new Node(2);
        tree.root.left.left = new Node(3);

        // Populates nextRight pointer in all nodes
        tree.connect(tree.root);

        // Let us check the values of nextRight pointers
        Console.WriteLine("Following are populated nextRight pointers in "
                          + "the tree"
                          + "(-1 is printed if there is no nextRight)");
        int a = tree.root.nextRight != null ? tree.root.nextRight.data : -1;
        Console.WriteLine("nextRight of " + tree.root.data + " is " + a);
        int b = tree.root.left.nextRight != null ? tree.root.left.nextRight.data : -1;
        Console.WriteLine("nextRight of " + tree.root.left.data + " is " + b);
        int c = tree.root.right.nextRight != null ? tree.root.right.nextRight.data : -1;
        Console.WriteLine("nextRight of " + tree.root.right.data + " is " + c);
        int d = tree.root.left.left.nextRight != null ? tree.root.left.left.nextRight.data : -1;
        Console.WriteLine("nextRight of " + tree.root.left.left.data + " is " + d);
    }
}

// This code is contributed by Shrikant13
```

**Output:** 

```
Following are populated nextRight pointers in the tree (-1 is printed if there is no nextRight)
nextRight of 10 is -1
nextRight of 8 is 2
nextRight of 2 is -1
nextRight of 3 is -1
```

感谢丹雅提出这个方法。
**时间复杂度:** O(n)
***为什么方法 2 对不是完全二叉树的树不起作用？***
让我们考虑以下树为例。在方法 2 中，我们以预先排序的方式设置下一个右指针。当我们在节点 4 时，我们设置它的孩子的下一个权利是 8 和 9(4 的下一个权利已经被设置为节点 5)。8 的 nextRight 将被简单地设置为 9，但是 9 的 nextRight 将被设置为空，这是不正确的。我们无法设置正确的 nextRight，因为当我们将 nextRight 设置为 9 时，我们只有节点 4 的 nextRight 和节点 4 的祖先，在根的右子树中没有节点的 nextRight。

```
            1
          /    \
        2        3
       / \      /  \
      4   5    6    7
     / \           / \  
    8   9        10   11
```

更多解决方案参见 [**使用恒定额外空间**](https://www.geeksforgeeks.org/connect-nodes-at-same-level-with-o1-extra-space/) 连接同级节点。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。