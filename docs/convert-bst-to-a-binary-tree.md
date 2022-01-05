# 将一个 BST 转换成一个二叉树，这样所有更大的键的总和被添加到每个键中

> 原文:[https://www.geeksforgeeks.org/convert-bst-to-a-binary-tree/](https://www.geeksforgeeks.org/convert-bst-to-a-binary-tree/)

给定一个二叉查找树(BST)，将其转换为二叉树，这样原始 BST 的每个键都被更改为键加上 BST 中所有较大键的和。
**例:**

```
Input: Root of following BST
              5
            /   \
           2     13

Output: The given BST is converted to following Binary Tree
              18
            /   \
          20     13
```

**方法一:**
**解:**做逆序遍历。记录到目前为止访问的节点总数。设这个和为*和*。对于当前正在访问的每个节点，首先将该节点的密钥添加到 *sum* 中，即 *sum* = *sum* + *节点- >密钥*。然后将当前节点的键改为*和*，即*节点- >键=和*。
当一个 BST 被反向遍历时，对于当前被访问的每个键，所有已经被访问的键都是更大的键。

## C++

```
// C++ Program to change a BST to Binary Tree
// such that key of a node becomes original
// key plus sum of all greater keys in BST
#include <bits/stdc++.h>
using namespace std;

/* A BST node has key, left child
   and right child */
struct node
{
    int key;
    struct node* left;
    struct node* right;
};

/* Helper function that allocates a new node
with the given key and NULL left and right pointers.*/
struct node* newNode(int key)
{
    struct node* node = (struct node*)malloc(sizeof(struct node));
    node->key = key;
    node->left = NULL;
    node->right = NULL;
    return (node);
}

// A recursive function that traverses the
// given BST in reverse inorder and for
// every key, adds all greater keys to it
void addGreaterUtil(struct node *root, int *sum_ptr)
{
    // Base Case
    if (root == NULL)
        return;

    // Recur for right subtree first so that sum
    // of all greater nodes is stored at sum_ptr
    addGreaterUtil(root->right, sum_ptr);

    // Update the value at sum_ptr
    *sum_ptr = *sum_ptr + root->key;

    // Update key of this node
    root->key = *sum_ptr;

    // Recur for left subtree so that the
    // updated sum is added to smaller nodes
    addGreaterUtil(root->left, sum_ptr);
}

// A wrapper over addGreaterUtil(). It initializes
// sum and calls addGreaterUtil() to recursively
// update and use value of sum
void addGreater(struct node *root)
{
    int sum = 0;
    addGreaterUtil(root, &sum);
}

// A utility function to print inorder
// traversal of Binary Tree
void printInorder(struct node* node)
{
    if (node == NULL)
        return;
    printInorder(node->left);
    cout << node->key << " " ;
    printInorder(node->right);
}

// Driver Code
int main()
{
    /* Create following BST
            5
            / \
        2 13 */
    node *root = newNode(5);
    root->left = newNode(2);
    root->right = newNode(13);

    cout << "Inorder traversal of the "
         << "given tree" << endl;
    printInorder(root);

    addGreater(root);
    cout << endl;
    cout << "Inorder traversal of the "
         << "modified tree" << endl;
    printInorder(root);

    return 0;
}

// This code is contributed by SHUBHAMSINGH10
```

## C

```
// Program to change a BST to Binary Tree such that key of a node becomes
// original key plus sum of all greater keys in BST
#include <stdio.h>
#include <stdlib.h>

/* A BST node has key, left child and right child */
struct node
{
    int key;
    struct node* left;
    struct node* right;
};

/* Helper function that allocates a new node with the given key and
   NULL left and right  pointers.*/
struct node* newNode(int key)
{
    struct node* node = (struct node*)malloc(sizeof(struct node));
    node->key = key;
    node->left = NULL;
    node->right = NULL;
    return (node);
}

// A recursive function that traverses the given BST in reverse inorder and
// for every key, adds all greater keys to it
void addGreaterUtil(struct node *root, int *sum_ptr)
{
    // Base Case
    if (root == NULL)
        return;

    // Recur for right subtree first so that sum of all greater
    // nodes is stored at sum_ptr
    addGreaterUtil(root->right, sum_ptr);

    // Update the value at sum_ptr
    *sum_ptr = *sum_ptr + root->key;

    // Update key of this node
    root->key = *sum_ptr;

    // Recur for left subtree so that the updated sum is added
    // to smaller nodes
    addGreaterUtil(root->left, sum_ptr);
}

// A wrapper over addGreaterUtil().  It initializes sum and calls
// addGreaterUtil() to recursivel upodate and use value of sum
void addGreater(struct node *root)
{
    int sum = 0;
    addGreaterUtil(root, &sum);
}

// A utility function to print inorder traversal of Binary Tree
void printInorder(struct node* node)
{
    if (node == NULL)
        return;
    printInorder(node->left);
    printf("%d ", node->key);
    printInorder(node->right);
}

// Driver program to test above function
int main()
{
    /* Create following BST
              5
            /   \
           2     13  */
    node *root = newNode(5);
    root->left = newNode(2);
    root->right = newNode(13);

    printf("Inorder traversal of the given tree\n");
    printInorder(root);

    addGreater(root);

    printf("\nInorder traversal of the modified tree\n");
    printInorder(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to convert BST to binary tree such that sum of
// all greater keys is added to every key

class Node {

    int data;
    Node left, right;

    Node(int d) {
        data = d;
        left = right = null;
    }
}

class Sum {

    int sum = 0;
}

class BinaryTree {

    static Node root;
    Sum summ = new Sum();

    // A recursive function that traverses the given BST in reverse inorder and
    // for every key, adds all greater keys to it
    void addGreaterUtil(Node node, Sum sum_ptr) {

        // Base Case
        if (node == null) {
            return;
        }

        // Recur for right subtree first so that sum of all greater
        // nodes is stored at sum_ptr
        addGreaterUtil(node.right, sum_ptr);

        // Update the value at sum_ptr
        sum_ptr.sum = sum_ptr.sum + node.data;

        // Update key of this node
        node.data = sum_ptr.sum;

        // Recur for left subtree so that the updated sum is added
        // to smaller nodes
        addGreaterUtil(node.left, sum_ptr);
    }

    // A wrapper over addGreaterUtil().  It initializes sum and calls
    // addGreaterUtil() to recursivel upodate and use value of sum
    Node addGreater(Node node) {
        addGreaterUtil(node, summ);
        return node;
    }

    // A utility function to print inorder traversal of Binary Tree
    void printInorder(Node node) {
        if (node == null) {
            return;
        }
        printInorder(node.left);
        System.out.print(node.data + " ");
        printInorder(node.right);
    }

    // Driver program to test the above functions
    public static void main(String[] args) {
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(5);
        tree.root.left = new Node(2);
        tree.root.right = new Node(13);

        System.out.println("Inorder traversal of given tree ");
        tree.printInorder(root);
        Node node = tree.addGreater(root);
        System.out.println("");
        System.out.println("Inorder traversal of modified tree ");
        tree.printInorder(node);
    }
}

// This code has been contributed by Mayank Jaiswal
```

## 蟒蛇 3

```
# Python3 Program to change a BST to
# Binary Tree such that key of a node
# becomes original key plus sum of all
# greater keys in BST

# A BST node has key, left child and
# right child */
class Node:

    # Constructor to create a new node
    def __init__(self, data):
        self.key = data
        self.left = None
        self.right = None

# A recursive function that traverses
# the given BST in reverse inorder and
# for every key, adds all greater keys to it
def addGreaterUtil(root, sum_ptr):

    # Base Case
    if root == None:
        return

    # Recur for right subtree first so that sum
    # of all greater nodes is stored at sum_ptr
    addGreaterUtil(root.right, sum_ptr)

    # Update the value at sum_ptr
    sum_ptr[0] = sum_ptr[0] + root.key

    # Update key of this node
    root.key = sum_ptr[0]

    # Recur for left subtree so that the
    # updated sum is added to smaller nodes
    addGreaterUtil(root.left, sum_ptr)

# A wrapper over addGreaterUtil(). It initializes
# sum and calls addGreaterUtil() to recursive
# update and use value of sum
def addGreater(root):
    Sum = [0]
    addGreaterUtil(root, Sum)

# A utility function to print inorder
# traversal of Binary Tree
def printInorder(node):
    if node == None:
        return
    printInorder(node.left)
    print(node.key, end = " ")
    printInorder(node.right)

# Driver Code
if __name__ == '__main__':

    # Create following BST
    #         5
    #     / \
    #     2     13
    root = Node(5)
    root.left = Node(2)
    root.right = Node(13)

    print("Inorder traversal of the given tree")
    printInorder(root)

    addGreater(root)
    print()
    print("Inorder traversal of the modified tree")
    printInorder(root)

# This code is contributed by PranchalK
```

## C#

```
using System;

// C# program to convert BST to binary tree such that sum of 
// all greater keys is added to every key

public class Node
{

    public int data;
    public Node left, right;

    public Node(int d)
    {
        data = d;
        left = right = null;
    }
}

public class Sum
{

    public int sum = 0;
}

public class BinaryTree
{

    public static Node root;
    public Sum summ = new Sum();

    // A recursive function that traverses the given BST in reverse inorder and
    // for every key, adds all greater keys to it
    public virtual void addGreaterUtil(Node node, Sum sum_ptr)
    {

        // Base Case
        if (node == null)
        {
            return;
        }

        // Recur for right subtree first so that sum of all greater
        // nodes is stored at sum_ptr
        addGreaterUtil(node.right, sum_ptr);

        // Update the value at sum_ptr
        sum_ptr.sum = sum_ptr.sum + node.data;

        // Update key of this node
        node.data = sum_ptr.sum;

        // Recur for left subtree so that the updated sum is added
        // to smaller nodes
        addGreaterUtil(node.left, sum_ptr);
    }

    // A wrapper over addGreaterUtil().  It initializes sum and calls
    // addGreaterUtil() to recursivel upodate and use value of sum
    public virtual Node addGreater(Node node)
    {
        addGreaterUtil(node, summ);
        return node;
    }

    // A utility function to print inorder traversal of Binary Tree
    public virtual void printInorder(Node node)
    {
        if (node == null)
        {
            return;
        }
        printInorder(node.left);
        Console.Write(node.data + " ");
        printInorder(node.right);
    }

    // Driver program to test the above functions
    public static void Main(string[] args)
    {
        BinaryTree tree = new BinaryTree();
        BinaryTree.root = new Node(5);
        BinaryTree.root.left = new Node(2);
        BinaryTree.root.right = new Node(13);

        Console.WriteLine("Inorder traversal of given tree ");
        tree.printInorder(root);
        Node node = tree.addGreater(root);
        Console.WriteLine("");
        Console.WriteLine("Inorder traversal of modified tree ");
        tree.printInorder(node);
    }
}

  // This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

// Javascript program to convert BST to binary tree such that sum of 
// all greater keys is added to every key
class Node
{
    constructor(d)
{
    this.data = d;
    this.left = null;
    this.right = null;
}
}

class Sum
{
    constructor()
    {
        this.sum = 0;
    }
}

var root = null;
var summ = new Sum();

// A recursive function that traverses the given BST in reverse inorder and
// for every key, adds all greater keys to it
function addGreaterUtil(node, sum_ptr)
{
    // Base Case
    if (node == null)
    {
        return;
    }

    // Recur for right subtree first so that sum of all greater
    // nodes is stored at sum_ptr
    addGreaterUtil(node.right, sum_ptr);

    // Update the value at sum_ptr
    sum_ptr.sum = sum_ptr.sum + node.data;

    // Update key of this node
    node.data = sum_ptr.sum;

    // Recur for left subtree so that the updated sum is added
    // to smaller nodes
    addGreaterUtil(node.left, sum_ptr);
}

// A wrapper over addGreaterUtil().  It initializes sum and calls
// addGreaterUtil() to recursivel upodate and use value of sum
function addGreater(node)
{
    addGreaterUtil(node, summ);
    return node;
}

// A utility function to print inorder traversal of Binary Tree
function printInorder(node)
{
    if (node == null)
    {
        return;
    }
    printInorder(node.left);
    document.write(node.data + " ");
    printInorder(node.right);
}

// Driver program to test the above functions
root = new Node(5);
root.left = new Node(2);
root.right = new Node(13);
document.write("Inorder traversal of given tree <br>");
printInorder(root);
var node = addGreater(root);
document.write("<br>");
document.write("Inorder traversal of modified tree <br>");
printInorder(node);

// This code is contributed by rrrtnx.
</script>
```

**输出:**

```
Inorder traversal of the given tree
2 5 13
Inorder traversal of the modified tree
20 18 13
```

**时间复杂度:** O(n)，其中 n 是给定二叉查找树中的节点数。

**方法二:**

下面的方法使用了堆栈迭代技术。

**进场:**

1.  首先，我们初始化一个空堆栈，并将当前节点设置为根。
2.  然后，只要堆栈中有未访问的节点，或者该节点没有指向 null，我们就将沿着最右边的叶子的路径的所有节点推到堆栈上。
3.  。接下来，我们访问堆栈顶部的节点，并考虑它的左子树。
4.  最终，我们的堆栈是空的，节点指向树的最小值节点的左边空子节点，因此循环终止。

下面是上述方法的实现:

## C

```
#include <stdio.h>
#include <stdlib.h>
#define bool int

/* A binary tree tNode has data, pointer to left child
and a pointer to right child */
struct tNode {
    int data;
    struct tNode* left;
    struct tNode* right;
};

/* Structure of a stack node. Linked List implementation is
used for stack. A stack node contains a pointer to tree node
and a pointer to next stack node */
struct sNode {
    struct tNode* t;
    struct sNode* next;
};

/* Stack related functions */
void push(struct sNode** top_ref, struct tNode* t);
struct tNode* pop(struct sNode** top_ref);
bool isEmpty(struct sNode* top);

/* Iterative function for inorder tree traversal */
void inOrder(struct tNode* root)
{
    /* set current to root of binary tree */
    struct tNode* current = root;
    struct sNode* s = NULL; /* Initialize stack s */
    bool done = 0;

    while (!done) {
        /* Reach the left most tNode of the current tNode */
        if (current != NULL) {
            /* place pointer to a tree node on the stack
               before traversing the node's left subtree */
            push(&s, current);
            current = current->left;
        }

        /* backtrack from the empty subtree and visit the
        tNode at the top of the stack; however, if the stack
        is empty, you are done */
        else {
            if (!isEmpty(s)) {
                current = pop(&s);
                printf("%d ", current->data);

                /* we have visited the node and its left
                subtree. Now, it's right subtree's turn */
                current = current->right;
            }
            else
                done = 1;
        }
    } /* end of while */
}

void Greater_BST(struct tNode* root)
{
    int sum = 0;
    struct sNode* st = NULL;
    struct tNode* node = root;

    while (!isEmpty(st) || node != NULL) {
        // push all nodes up to (and including) this
        // subtree's maximum on the stack

        while (node != NULL) {
            push(&st, node);
            node = node->right;
        }

        node = pop(&st);

        sum += node->data;
        node->data = sum;

        // all nodes with values between the current and its
        // parent lie in the left subtree.
        node = node->left;
    }
}

/* UTILITY FUNCTIONS */
/* Function to push an item to sNode*/
void push(struct sNode** top_ref, struct tNode* t)
{
    /* allocate tNode */
    struct sNode* new_tNode
        = (struct sNode*)malloc(sizeof(struct sNode));

    if (new_tNode == NULL) {
        printf("Stack Overflow \n");
        getchar();
        exit(0);
    }

    /* put in the data */
    new_tNode->t = t;

    /* link the old list off the new tNode */
    new_tNode->next = (*top_ref);

    /* move the head to point to the new tNode */
    (*top_ref) = new_tNode;
}

/* The function returns true if stack is empty, otherwise
 * false */
bool isEmpty(struct sNode* top)
{
    return (top == NULL) ? 1 : 0;
}

/* Function to pop an item from stack*/
struct tNode* pop(struct sNode** top_ref)
{
    struct tNode* res;
    struct sNode* top;

    top = *top_ref;
    res = top->t;
    *top_ref = top->next;
    free(top);
    return res;
}

/* Helper function that allocates a new tNode with the
given data and NULL left and right pointers. */
struct tNode* newtNode(int data)
{
    struct tNode* tNode
        = (struct tNode*)malloc(sizeof(struct tNode));
    tNode->data = data;
    tNode->left = NULL;
    tNode->right = NULL;

    return (tNode);
}

/* Driver program to test above functions*/
int main()
{

    /* Let us create following BST
                          8
                /     \
              5        12
             /  \      /  \
           2     7    9    15     */

    struct tNode* root = newtNode(8);
    root->left = newtNode(5);
    root->right = newtNode(12);
    root->left->left = newtNode(2);
    root->left->right = newtNode(7);
    root->right->left = newtNode(9);
    root->right->right = newtNode(15);

    Greater_BST(root);

    inOrder(root);

    getchar();
    return 0;
}
```

## C++

```
// C++ program to add all greater
// values in every node of BST through Iteration using Stack
#include <bits/stdc++.h>
using namespace std;

class Node {
public:
    int data;
    Node *left, *right;
};

// A utility function to create
// a new BST node
Node* newNode(int item)
{
    Node* temp = new Node();
    temp->data = item;
    temp->left = temp->right = NULL;
    return temp;
}

// Iterative function to add
// all greater values in every node
void Greater_BST(Node* root)
{
    int sum = 0;
        stack<Node*> st;
        Node* node = root;

        while(!st.empty() || node != NULL ){
        // push all nodes up to (and including) this subtree's maximum on the stack

            while(node != NULL){
                st.push(node);
                node = node->right;
            }

            node = st.top();
            st.pop();
            sum += node->data;
            node->data = sum;

   // all nodes with values between the current and its parent lie in the left subtree.
            node = node->left;
        }
}

// A utility function to do
// inorder traversal of BST
void inorder(Node* root)
{
    if (root != NULL) {
        inorder(root->left);
        cout << root->data << " ";
        inorder(root->right);
    }
}

/* A utility function to insert
a new node with given data in BST */
Node* insert(Node* node, int data)
{
    /* If the tree is empty,
    return a new node */
    if (node == NULL)
        return newNode(data);

    /* Otherwise, recur down the tree */
    if (data <= node->data)
        node->left = insert(node->left, data);
    else
        node->right = insert(node->right, data);

    /* return the (unchanged) node pointer */
    return node;
}

// Driver code
int main()
{
    /* Let us create following BST
              8
            /     \
          5        12
         /  \      /  \
       2     7    9    15 */

    Node* root = NULL;
    root = insert(root, 8);
    insert(root, 5);
    insert(root, 2);
    insert(root, 7);
    insert(root, 12);
    insert(root, 9);
    insert(root, 15);

    Greater_BST(root);

    // print inorder traversal of the Greater BST
    inorder(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to add all greater values to
// every node in a given BST

import java.util.*;

// A binary tree node
class Node {

    int data;
    Node left, right;

    Node(int d)
    {
        data = d;
        left = right = null;
    }
}

class BinarySearchTree {

    // Root of BST
    Node root;

    // Constructor
    BinarySearchTree() { root = null; }

    // Inorder traversal of the tree
    void inorder() { inorderUtil(this.root); }

    // Utility function for inorder traversal of
    // the tree
    void inorderUtil(Node node)
    {
        if (node == null)
            return;

        inorderUtil(node.left);
        System.out.print(node.data + " ");
        inorderUtil(node.right);
    }

    // adding new node
    public void insert(int data)
    {
        this.root = this.insertRec(this.root, data);
    }

    /* A utility function to insert a new node with
    given data in BST */
    Node insertRec(Node node, int data)
    {
        /* If the tree is empty, return a new node */
        if (node == null) {
            this.root = new Node(data);
            return this.root;
        }

        /* Otherwise, recur down the tree */
        if (data <= node.data) {
            node.left = this.insertRec(node.left, data);
        }
        else {
            node.right = this.insertRec(node.right, data);
        }
        return node;
    }

    // Iterative function to add
    // all greater values in every node
    void Greater_BST(Node root)
    {
        int sum = 0;
        Node node = root;
        Stack<Node> stack = new Stack<Node>();

        while (!stack.isEmpty() || node != null) {
            /* push all nodes up to (and including) this
             * subtree's maximum on the stack. */
            while (node != null) {
                stack.add(node);
                node = node.right;
            }

            node = stack.pop();
            sum += node.data;
            node.data = sum;

            /* all nodes with values between the current and
             * its parent lie in the left subtree. */
            node = node.left;
        }
    }

    // Driver Function
    public static void main(String[] args)
    {
        BinarySearchTree tree = new BinarySearchTree();

        /* Let us create following BST

           8
         /     \
   5     12
  / \   / \
 2   7 9   15   */

        tree.insert(8);
        tree.insert(5);
        tree.insert(2);
        tree.insert(7);
        tree.insert(12);
        tree.insert(9);
        tree.insert(15);

        tree.Greater_BST(tree.root);

        // print inorder traversal of the Greater BST
        tree.inorder();
    }
}
```

## 蟒蛇 3

```
# Python3 program to add all greater values
# in every node of BST through Iteration using Stack

# A utility function to create a
# new BST node
class newNode:

    # Constructor to create a new node
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Iterative function to add all greater
# values in every node 
def Greater_BST(root):
    total = 0

    node = root
    stack = []
    while stack or node is not None:

        # push all nodes up to (and including)
        # this subtree's maximum on
        # the stack.
        while node is not None:
            stack.append(node)
            node = node.right

        node = stack.pop()
        total += node.data
        node.data = total

        # all nodes with values between
        # the current and its parent lie in
        # the left subtree.
        node = node.left

# A utility function to do inorder
# traversal of BST
def inorder(root):
    if root != None:
        inorder(root.left)
        print(root.data, end =" ")
        inorder(root.right)

# A utility function to insert a new node
# with given data in BST
def insert(node, data):

    # If the tree is empty, return a new node
    if node == None:
        return newNode(data)

    # Otherwise, recur down the tree
    if data <= node.data:
        node.left = insert(node.left, data)
    else:
        node.right = insert(node.right, data)

    # return the (unchanged) node pointer
    return node

# Driver Code
if __name__ == '__main__':

    # Let us create following BST
    #        8
    #     /     \
    #   5     12
    #  / \   / \
    # 2   7 9   15
    root = None
    root = insert(root, 8)
    insert(root, 5)
    insert(root, 2)
    insert(root, 7)
    insert(root, 9)
    insert(root, 12)
    insert(root, 15)

    Greater_BST(root)

    # print inorder traversal of the
    # Greater BST
    inorder(root)

```

**输出:**

```
58 56 51 44 36 27 15 
```

**时间复杂度:** O(n)，n 为一个 BST 中的节点数。

**辅助空间:** O(n)。堆栈用于存储数据。

？list = plqm7 alhxfyshcxd 7 r1j 0k y9 ZG _ gbb1 dbk
如果发现有不正确的地方，请写评论，或者想分享更多关于上面讨论的主题的信息。