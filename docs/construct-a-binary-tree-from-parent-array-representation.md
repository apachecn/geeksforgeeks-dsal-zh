# 从给定的父数组表示中构建二叉树

> 原文:[https://www . geeksforgeeks . org/construct-a-二叉树-从父数组-表示法/](https://www.geeksforgeeks.org/construct-a-binary-tree-from-parent-array-representation/)

给定一个表示树的数组，数组索引是树节点中的值，数组值给出该特定索引(或节点)的父节点。根节点索引的值总是-1，因为根没有父节点。从这个给定的表示构造给定二叉树的标准链接表示。
**例:**

```
Input: parent[] = {1, 5, 5, 2, 2, -1, 3}
Output: root of below tree
          5
        /  \
       1    2
      /    / \
     0    3   4
         /
        6 
Explanation: 
Index of -1 is 5\.  So 5 is root.  
5 is present at indexes 1 and 2\.  So 1 and 2 are
children of 5\.  
1 is present at index 0, so 0 is child of 1.
2 is present at indexes 3 and 4\.  So 3 and 4 are
children of 2\.  
3 is present at index 6, so 6 is child of 3.

Input: parent[] = {-1, 0, 0, 1, 1, 3, 5};
Output: root of below tree
         0
       /   \
      1     2
     / \
    3   4
   /
  5 
 /
6
```

预期的时间复杂度是 O(n)，其中 n 是给定数组中的元素数量。

**强烈建议尽量减少浏览器，先自己试试这个。**
A **简单解**递归构造，首先搜索当前根，然后对找到的索引进行递归(最多可以有两个索引)，并使其成为根的左右子树。这个解决方案需要 O(n <sup>2</sup> ，因为我们必须线性搜索每个节点。
一个**高效解决方案**可以在 O(n)时间内解决上述问题。这个想法是利用额外的空间。创建了一个数组[0..n-1]用于跟踪创建的节点。
***createTree(parent[]，n)***

1.  创建一个指针数组，比如创建了[0..n-1]。如果没有创建索引 I 的节点，则 created[i]的值为 NULL，否则该值是指向已创建节点的指针。
2.  对给定数组的每个索引 I 执行以下操作
    createNode(父，I，已创建)

***createNode(父节点[]，I，created[])***

1.  如果创建的[i]不为空，则节点已经创建。所以回来吧。
2.  创建一个值为“I”的新节点。
3.  如果 parent[i]为-1 (i 为 root)，则将创建的节点设为 root 并返回。
4.  检查是否创建了“I”的父代(我们可以通过检查创建的[父代[i]]是否为空来检查这一点。
5.  如果未创建父级，则为父级重复，并首先创建父级。
6.  让指向父节点的指针为 p。如果 p->left 为空，那么将新节点作为左子节点。否则，将新节点作为父节点的右子节点。

以下是上述思想的 C++实现。

## C++

```
// C++ program to construct a Binary Tree from parent array
#include<bits/stdc++.h>
using namespace std;

// A tree node
struct Node
{
    int key;
    struct Node *left, *right;
};

// Utility function to create new Node
Node *newNode(int key)
{
    Node *temp = new Node;
    temp->key  = key;
    temp->left  = temp->right = NULL;
    return (temp);
}

// Creates a node with key as 'i'.  If i is root, then it changes
// root.  If parent of i is not created, then it creates parent first
void createNode(int parent[], int i, Node *created[], Node **root)
{
    // If this node is already created
    if (created[i] != NULL)
        return;

    // Create a new node and set created[i]
    created[i] = newNode(i);

    // If 'i' is root, change root pointer and return
    if (parent[i] == -1)
    {
        *root = created[i];
        return;
    }

    // If parent is not created, then create parent first
    if (created[parent[i]] == NULL)
        createNode(parent, parent[i], created, root);

    // Find parent pointer
    Node *p = created[parent[i]];

    // If this is first child of parent
    if (p->left == NULL)
        p->left = created[i];
    else // If second child
        p->right = created[i];
}

// Creates tree from parent[0..n-1] and returns root of the created tree
Node *createTree(int parent[], int n)
{
    // Create an array created[] to keep track
    // of created nodes, initialize all entries
    // as NULL
    Node *created[n];
    for (int i=0; i<n; i++)
        created[i] = NULL;

    Node *root = NULL;
    for (int i=0; i<n; i++)
        createNode(parent, i, created, &root);

    return root;
}

//For adding new line in a program
inline void newLine(){
    cout << "\n";
}

// Utility function to do inorder traversal
void inorder(Node *root)
{
    if (root != NULL)
    {
        inorder(root->left);
        cout << root->key << " ";
        inorder(root->right);
    }
}

// Driver method
int main()
{
    int parent[] =  {-1, 0, 0, 1, 1, 3, 5};
    int n = sizeof parent / sizeof parent[0];
    Node *root = createTree(parent, n);
    cout << "Inorder Traversal of constructed tree\n";
    inorder(root);
    newLine();
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to construct a binary tree from parent array

// A binary tree node
class Node
{
    int key;
    Node left, right;

    public Node(int key)
    {
        this.key = key;
        left = right = null;
    }
}

class BinaryTree
{
    Node root;

    // Creates a node with key as 'i'.  If i is root, then it changes
    // root.  If parent of i is not created, then it creates parent first
    void createNode(int parent[], int i, Node created[])
    {
        // If this node is already created
        if (created[i] != null)
            return;

        // Create a new node and set created[i]
        created[i] = new Node(i);

        // If 'i' is root, change root pointer and return
        if (parent[i] == -1)
        {
            root = created[i];
            return;
        }

        // If parent is not created, then create parent first
        if (created[parent[i]] == null)
            createNode(parent, parent[i], created);

        // Find parent pointer
        Node p = created[parent[i]];

        // If this is first child of parent
        if (p.left == null)
            p.left = created[i];
        else // If second child

            p.right = created[i];
    }

    /* Creates tree from parent[0..n-1] and returns root of
       the created tree */
    Node createTree(int parent[], int n)
    {   
        // Create an array created[] to keep track
        // of created nodes, initialize all entries
        // as NULL
        Node[] created = new Node[n];
        for (int i = 0; i < n; i++)
            created[i] = null;

        for (int i = 0; i < n; i++)
            createNode(parent, i, created);

        return root;
    }

    //For adding new line in a program
    void newLine()
    {
        System.out.println("");
    }

    // Utility function to do inorder traversal
    void inorder(Node node)
    {
        if (node != null)
        {
            inorder(node.left);
            System.out.print(node.key + " ");
            inorder(node.right);
        }
    }

    // Driver method
    public static void main(String[] args)
    {

        BinaryTree tree = new BinaryTree();
        int parent[] = new int[]{-1, 0, 0, 1, 1, 3, 5};
        int n = parent.length;
        Node node = tree.createTree(parent, n);
        System.out.println("Inorder traversal of constructed tree ");
        tree.inorder(node);
        tree.newLine();
    }
}

// This code has been contributed by Mayank Jaiswal(mayank_24)
```

## 计算机编程语言

```
# Python implementation to construct a Binary Tree from
# parent array

# A node structure
class Node:
    # A utility function to create a new node
    def __init__(self, key):
        self.key = key
        self.left = None
        self.right = None

""" Creates a node with key as 'i'. If i is root,then
    it changes root. If parent of i is not created, then
    it creates parent first
"""
def createNode(parent, i, created, root):

    # If this node is already created
    if created[i] is not None:
        return

    # Create a new node and set created[i]
    created[i] = Node(i)

    # If 'i' is root, change root pointer and return
    if parent[i] == -1:
        root[0] = created[i] # root[0] denotes root of the tree
        return

    # If parent is not created, then create parent first
    if created[parent[i]] is None:
        createNode(parent, parent[i], created, root )

    # Find parent pointer
    p = created[parent[i]]

    # If this is first child of parent
    if p.left is None:
        p.left = created[i]
    # If second child
    else:
        p.right = created[i]

# Creates tree from parent[0..n-1] and returns root of the
# created tree
def createTree(parent):
    n = len(parent)

    # Create and array created[] to keep track
    # of created nodes, initialize all entries as None
    created = [None for i in range(n+1)]

    root = [None]
    for i in range(n):
        createNode(parent, i, created, root)

    return root[0]

#Inorder traversal of tree
def inorder(root):
    if root is not None:
        inorder(root.left)
        print root.key,
        inorder(root.right)

# Driver Method
parent = [-1, 0, 0, 1, 1, 3, 5]
root = createTree(parent)
print "Inorder Traversal of constructed tree"
inorder(root)

# This code is contributed by Nikhil Kumar Singh(nickzuck_007)
```

## C#

```
// C# program to construct a binary
// tree from parent array
using System;

// A binary tree node
public class Node
{
    public int key;
    public Node left, right;

    public Node(int key)
    {
        this.key = key;
        left = right = null;
    }
}

class GFG
{
public Node root;

// Creates a node with key as 'i'.
// If i is root, then it changes
// root. If parent of i is not created,
// then it creates parent first
public virtual void createNode(int[] parent,
                               int i, Node[] created)
{
    // If this node is already created
    if (created[i] != null)
    {
        return;
    }

    // Create a new node and set created[i]
    created[i] = new Node(i);

    // If 'i' is root, change root
    // pointer and return
    if (parent[i] == -1)
    {
        root = created[i];
        return;
    }

    // If parent is not created, then
    // create parent first
    if (created[parent[i]] == null)
    {
        createNode(parent, parent[i], created);
    }

    // Find parent pointer
    Node p = created[parent[i]];

    // If this is first child of parent
    if (p.left == null)
    {
        p.left = created[i];
    }
    else // If second child
    {

        p.right = created[i];
    }
}

/* Creates tree from parent[0..n-1]
and returns root of the created tree */
public virtual Node createTree(int[] parent, int n)
{
    // Create an array created[] to
    // keep track of created nodes,
    // initialize all entries as NULL
    Node[] created = new Node[n];
    for (int i = 0; i < n; i++)
    {
        created[i] = null;
    }

    for (int i = 0; i < n; i++)
    {
        createNode(parent, i, created);
    }

    return root;
}

// For adding new line in a program
public virtual void newLine()
{
    Console.WriteLine("");
}

// Utility function to do inorder traversal
public virtual void inorder(Node node)
{
    if (node != null)
    {
        inorder(node.left);
        Console.Write(node.key + " ");
        inorder(node.right);
    }
}

// Driver Code
public static void Main(string[] args)
{
    GFG tree = new GFG();
    int[] parent = new int[]{-1, 0, 0, 1, 1, 3, 5};
    int n = parent.Length;
    Node node = tree.createTree(parent, n);
    Console.WriteLine("Inorder traversal of " +
                          "constructed tree ");
    tree.inorder(node);
    tree.newLine();
}
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

// Javascript program to construct a binary
// tree from parent array

// A binary tree node
class Node
{
  constructor(key)
  {
    this.key = key;
    this.left = null;
    this.right = null;
  }
}

var root = null;

// Creates a node with key as 'i'.
// If i is root, then it changes
// root. If parent of i is not created,
// then it creates parent first
function createNode(parent, i, created)
{
    // If this node is already created
    if (created[i] != null)
    {
        return;
    }

    // Create a new node and set created[i]
    created[i] = new Node(i);

    // If 'i' is root, change root
    // pointer and return
    if (parent[i] == -1)
    {
        root = created[i];
        return;
    }

    // If parent is not created, then
    // create parent first
    if (created[parent[i]] == null)
    {
        createNode(parent, parent[i], created);
    }

    // Find parent pointer
    var p = created[parent[i]];

    // If this is first child of parent
    if (p.left == null)
    {
        p.left = created[i];
    }
    else // If second child
    {

        p.right = created[i];
    }
}

/* Creates tree from parent[0..n-1]
and returns root of the created tree */
function createTree(parent, n)
{
    // Create an array created[] to
    // keep track of created nodes,
    // initialize all entries as NULL
    var created = Array(n);
    for (var i = 0; i < n; i++)
    {
        created[i] = null;
    }

    for (var i = 0; i < n; i++)
    {
        createNode(parent, i, created);
    }

    return root;
}

// For adding new line in a program
function newLine()
{
    document.write("");
}

// Utility function to do inorder traversal
function inorder(node)
{
    if (node != null)
    {
        inorder(node.left);
        document.write(node.key + " ");
        inorder(node.right);
    }
}

// Driver Code
var parent = [-1, 0, 0, 1, 1, 3, 5];
var n = parent.length;
var node = createTree(parent, n);
document.write("Inorder traversal of " +
                      "constructed tree<br>");
inorder(node);
newLine();

// This code is contributed by rrrtnx.

</script>
```

**输出:**

```
Inorder Traversal of constructed tree
6 5 3 1 4 0 2
```

类似问题:[查找父数组](https://www.geeksforgeeks.org/find-height-binary-tree-represented-parent-array/)
代表的二叉树的高度，如有不正确的地方请写评论，或者想分享更多以上讨论话题的信息