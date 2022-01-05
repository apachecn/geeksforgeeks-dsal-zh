# 将所有更大的值添加到给定 BST 中的每个节点上

> 原文:[https://www . geesforgeks . org/add-greater-values-ever-node-given-BST/](https://www.geeksforgeeks.org/add-greater-values-every-node-given-bst/)

给定一个 **B** 二进制 **S** 搜索 **T** ree (BST)，修改它，以便给定 BST 中所有更大的值都被添加到每个节点。例如，考虑下面的 BST。

```
              50
           /      \
         30        70
        /   \      /  \
      20    40    60   80 

The above tree should be modified to following 

              260
           /      \
         330        150
        /   \       /  \
      350   300    210   80
```

解决这个问题的一个简单方法是找到每个节点所有更大值的总和。这种方法需要 O(n^2 时间。
本文讨论的方法使用了 BST 的反向有序树遍历技术，优化了单次遍历要解决的问题。
**方法:**在这个问题中，我们可以注意到最大的节点将保持不变。*第二大节点的值=最大值+第二大节点*的值。类似地，第 n 个最大节点的值将是修改后的第 n 个节点和第(n-1)个最大节点的值之和。因此，如果我们以降序遍历树，同时在每一步更新和值，同时将值添加到根节点，问题就会得到解决。
因此，为了以降序遍历 BST，我们使用 BST 的反向顺序遍历。这需要一个全局变量 sum，它在每个节点上更新，一旦到达根节点，它就被添加到根节点的值中，并且根节点的值被更新。

## C++

```
// C++ program to add all greater
// values in every node of BST
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

// Recursive function to add all
// greater values in every node
void modifyBSTUtil(Node* root, int* sum)
{
    // Base Case
    if (root == NULL)
        return;

    // Recur for right subtree
    modifyBSTUtil(root->right, sum);

    // Now *sum has sum of nodes
    // in right subtree, add
    // root->data to sum and
    // update root->data
    *sum = *sum + root->data;
    root->data = *sum;

    // Recur for left subtree
    modifyBSTUtil(root->left, sum);
}

// A wrapper over modifyBSTUtil()
void modifyBST(Node* root)
{
    int sum = 0;
    modifyBSTUtil(root, &sum);
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
            50
        / \
        30 70
        / \ / \
    20 40 60 80 */
    Node* root = NULL;
    root = insert(root, 50);
    insert(root, 30);
    insert(root, 20);
    insert(root, 40);
    insert(root, 70);
    insert(root, 60);
    insert(root, 80);

    modifyBST(root);

    // print inorder traversal of the modified BST
    inorder(root);

    return 0;
}

// This code is contributed by rathbhupendra
```

## C

```
// C program to add all greater
// values in every node of BST
#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node *left, *right;
};

// A utility function to create a new BST node
struct Node* newNode(int item)
{
    struct Node* temp
        = (struct Node*)malloc(
            sizeof(struct Node));
    temp->data = item;
    temp->left = temp->right = NULL;
    return temp;
}

// Recursive function to add
// all greater values in every node
void modifyBSTUtil(
    struct Node* root, int* sum)
{
    // Base Case
    if (root == NULL)
        return;

    // Recur for right subtree
    modifyBSTUtil(root->right, sum);

    // Now *sum has sum of nodes
    // in right subtree, add
    // root->data to sum and
    // update root->data
    *sum = *sum + root->data;
    root->data = *sum;

    // Recur for left subtree
    modifyBSTUtil(root->left, sum);
}

// A wrapper over modifyBSTUtil()
void modifyBST(struct Node* root)
{
    int sum = 0;
    modifyBSTUtil(root, &sum);
}

// A utility function to do
// inorder traversal of BST
void inorder(struct Node* root)
{
    if (root != NULL) {
        inorder(root->left);
        printf("%d ", root->data);
        inorder(root->right);
    }
}

/* A utility function to insert
a new node with given data in BST */
struct Node* insert(
    struct Node* node, int data)
{
    /* If the tree is empty, return a new node */
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

// Driver Program to test above functions
int main()
{
    /* Let us create following BST
              50
           /     \
          30      70
         /  \    /  \
       20   40  60   80 */
    struct Node* root = NULL;
    root = insert(root, 50);
    insert(root, 30);
    insert(root, 20);
    insert(root, 40);
    insert(root, 70);
    insert(root, 60);
    insert(root, 80);

    modifyBST(root);

    // print inorder traversal of the modified BST
    inorder(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to add all greater values to
// every node in a given BST

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
    BinarySearchTree()
    {
        root = null;
    }

    // Inorder traversal of the tree
    void inorder()
    {
        inorderUtil(this.root);
    }

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

    // This class initialises the value of sum to 0
    public class Sum {
        int sum = 0;
    }

    // Recursive function to add all greater values in
    // every node
    void modifyBSTUtil(Node node, Sum S)
    {
        // Base Case
        if (node == null)
            return;

        // Recur for right subtree
        this.modifyBSTUtil(node.right, S);

        // Now *sum has sum of nodes in right subtree, add
        // root->data to sum and update root->data
        S.sum = S.sum + node.data;
        node.data = S.sum;

        // Recur for left subtree
        this.modifyBSTUtil(node.left, S);
    }

    // A wrapper over modifyBSTUtil()
    void modifyBST(Node node)
    {
        Sum S = new Sum();
        this.modifyBSTUtil(node, S);
    }

    // Driver Function
    public static void main(String[] args)
    {
        BinarySearchTree tree = new BinarySearchTree();

        /* Let us create following BST
              50
           /     \
          30      70
         /  \    /  \
       20   40  60   80 */

        tree.insert(50);
        tree.insert(30);
        tree.insert(20);
        tree.insert(40);
        tree.insert(70);
        tree.insert(60);
        tree.insert(80);

        tree.modifyBST(tree.root);

        // print inorder traversal of the modified BST
        tree.inorder();
    }
}

// This code is contributed by Kamal Rawal
```

## 蟒蛇 3

```
# Python3 program to add all greater values
# in every node of BST

# A utility function to create a
# new BST node
class newNode:

    # Constructor to create a new node
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Recursive function to add all greater
# values in every node
def modifyBSTUtil(root, Sum):

    # Base Case
    if root == None:
        return

    # Recur for right subtree
    modifyBSTUtil(root.right, Sum)

    # Now Sum[0] has sum of nodes in right
    # subtree, add root.data to sum and
    # update root.data
    Sum[0] = Sum[0] + root.data
    root.data = Sum[0]

    # Recur for left subtree
    modifyBSTUtil(root.left, Sum)

# A wrapper over modifyBSTUtil()
def modifyBST(root):
    Sum = [0]
    modifyBSTUtil(root, Sum)

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
    # 50
    #     /     \
    # 30     70
    #     / \ / \
    # 20 40 60 80
    root = None
    root = insert(root, 50)
    insert(root, 30)
    insert(root, 20)
    insert(root, 40)
    insert(root, 70)
    insert(root, 60)
    insert(root, 80)

    modifyBST(root)

    # print inorder traversal of the
    # modified BST
    inorder(root)

# This code is contributed by PranchalK
```

## C#

```
using System;

// C# code to add all greater values to
// every node in a given BST

// A binary tree node
public class Node {

    public int data;
    public Node left, right;

    public Node(int d)
    {
        data = d;
        left = right = null;
    }
}

public class BinarySearchTree {

    // Root of BST
    public Node root;

    // Constructor
    public BinarySearchTree()
    {
        root = null;
    }

    // Inorder traversal of the tree
    public virtual void inorder()
    {
        inorderUtil(this.root);
    }

    // Utility function for inorder traversal of
    // the tree
    public virtual void inorderUtil(Node node)
    {
        if (node == null) {
            return;
        }

        inorderUtil(node.left);
        Console.Write(node.data + " ");
        inorderUtil(node.right);
    }

    // adding new node
    public virtual void insert(int data)
    {
        this.root = this.insertRec(this.root, data);
    }

    /* A utility function to insert a new node with 
    given data in BST */
    public virtual Node insertRec(Node node, int data)
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

    // This class initialises the value of sum to 0
    public class Sum {
        private readonly BinarySearchTree outerInstance;

        public Sum(BinarySearchTree outerInstance)
        {
            this.outerInstance = outerInstance;
        }

        public int sum = 0;
    }

    // Recursive function to add all greater values in
    // every node
    public virtual void modifyBSTUtil(Node node, Sum S)
    {
        // Base Case
        if (node == null) {
            return;
        }

        // Recur for right subtree
        this.modifyBSTUtil(node.right, S);

        // Now *sum has sum of nodes in right subtree, add
        // root->data to sum and update root->data
        S.sum = S.sum + node.data;
        node.data = S.sum;

        // Recur for left subtree
        this.modifyBSTUtil(node.left, S);
    }

    // A wrapper over modifyBSTUtil()
    public virtual void modifyBST(Node node)
    {
        Sum S = new Sum(this);
        this.modifyBSTUtil(node, S);
    }

    // Driver Function
    public static void Main(string[] args)
    {
        BinarySearchTree tree = new BinarySearchTree();

        /* Let us create following BST
              50
           /     \
          30      70
         /  \    /  \
       20   40  60   80 */

        tree.insert(50);
        tree.insert(30);
        tree.insert(20);
        tree.insert(40);
        tree.insert(70);
        tree.insert(60);
        tree.insert(80);

        tree.modifyBST(tree.root);

        // print inorder traversal of the modified BST
        tree.inorder();
    }
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

// JavaScript code to add all greater values to
// every node in a given BST

// A binary tree node
class Node {
    constructor(val) {
        this.data = val;
        this.left = null;
        this.right = null;
    }
}

    // Root of BST
    var root = null;

    // Inorder traversal of the tree
    function inorder()
    {
        inorderUtil(this.root);
    }

    // Utility function for inorder traversal of
    // the tree
    function inorderUtil(node)
    {
        if (node == null)
            return;

        inorderUtil(node.left);
        document.write(node.data + " ");
        inorderUtil(node.right);
    }

    // adding new node
     function insert(data)
    {
        this.root = this.insertRec(this.root, data);
    }

    /* A utility function to insert a new node with
    given data in BST */
    function insertRec(node , data)
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

    // This class initialises the value of sum to 0
     class Sum {
     constructor(){
        this.sum = 0;
        }
    }

    // Recursive function to add
    // all greater values in
    // every node
    function modifyBSTUtil(node,  S)
    {
        // Base Case
        if (node == null)
            return;

        // Recur for right subtree
        this.modifyBSTUtil(node.right, S);

        // Now *sum has sum of nodes
        // in right subtree, add
        // root->data to sum and update root->data
        S.sum = S.sum + node.data;
        node.data = S.sum;

        // Recur for left subtree
        this.modifyBSTUtil(node.left, S);
    }

    // A wrapper over modifyBSTUtil()
    function modifyBST(node)
    {
        var S = new Sum();
        this.modifyBSTUtil(node, S);
    }

    // Driver Function

        /* Let us create following BST
              50
           /     \
          30      70
         /  \    /  \
       20   40  60   80 */

        insert(50);
        insert(30);
        insert(20);
        insert(40);
        insert(70);
        insert(60);
        insert(80);

        modifyBST(root);

        // print inorder traversal of the modified BST
        inorder();

// This code contributed by gauravrajput1

</script>
```

**输出:**

```
350 330 300 260 210 150 80
```

**复杂度分析:**

*   **时间复杂度:** O(n)。
    由于这个问题使用了有序树遍历技术
*   **辅助空间:** O(1)。
    因为没有数据结构用于存储值。

顺便说一下，我们也可以使用反向 Inorder 遍历来找到 BST 中第 k 个最大的元素。
本文由 [**钱德拉·普拉卡什**](https://www.facebook.com/chandra.prakash.52643) 供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。