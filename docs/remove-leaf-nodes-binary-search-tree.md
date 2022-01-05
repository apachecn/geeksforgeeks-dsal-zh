# 从二叉查找树移除所有叶节点

> 原文:[https://www . geesforgeks . org/remove-leaf-nodes-binary-search-tree/](https://www.geeksforgeeks.org/remove-leaf-nodes-binary-search-tree/)

我们给出了一个二叉查找树，我们想从二叉查找树删除叶节点。
**例:**

```
Input : 20 10 5 15 30 25 35
Output : Inorder before Deleting the leaf node
         5 10 15 20 25 30 35
         Inorder after Deleting the leaf node
         10 20 30

        This is the binary search tree where we
        want to delete the leaf node.
              20
           /     \
          10      30
         /  \    /  \
       5     15 25   35 

      After deleting the leaf node the binary 
      search tree looks like
              20
           /     \
          10      30

```

我们以[的方式穿越给定的二叉查找树。在遍历过程中，我们检查当前节点是否是叶子，如果是，我们删除它。否则我们会为左右孩子重现。要记住的一件重要的事情是，如果子树的根有任何修改，我们必须分配新的左右子树。](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/) 

## C++

```
// C++ program to delete leaf Node from
// binary search tree.
#include <bits/stdc++.h>
using namespace std;

struct Node {
    int data;
    struct Node* left;
    struct Node* right;
};

// Create a newNode in binary search tree.
struct Node* newNode(int data)
{
    struct Node* temp = new Node;
    temp->data = data;
    temp->left = temp->right = NULL;
    return temp;
}

// Insert a Node in binary search tree.
struct Node* insert(struct Node* root, int data)
{
    if (root == NULL)
        return newNode(data);
    if (data < root->data)
        root->left = insert(root->left, data);
    else if (data > root->data)
        root->right = insert(root->right, data);
    return root;
}

// Function for inorder traversal in a BST.
void inorder(struct Node* root)
{
    if (root != NULL) {
        inorder(root->left);
        cout << root->data << " ";
        inorder(root->right);
    }
}

// Delete leaf nodes from binary search tree.
struct Node* leafDelete(struct Node* root)
{
    if (root == NULL)
        return NULL;
    if (root->left == NULL && root->right == NULL) {
        free(root);
        return NULL;
    }

    // Else recursively delete in left and right
    // subtrees.
    root->left = leafDelete(root->left);
    root->right = leafDelete(root->right);

    return root;
}

// Driver code
int main()
{
    struct Node* root = NULL;
    root = insert(root, 20);
    insert(root, 10);
    insert(root, 5);
    insert(root, 15);
    insert(root, 30);
    insert(root, 25);
    insert(root, 35);
    cout << "Inorder before Deleting the leaf Node." << endl;
    inorder(root);
    cout << endl;
    leafDelete(root);
    cout << "INorder after Deleting the leaf Node." << endl;
    inorder(root);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to delete leaf Node from
// binary search tree.
class GfG {

    static class Node {
        int data;
        Node left;
        Node right;
    }

    // Create a newNode in binary search tree.
    static Node newNode(int data)
    {
        Node temp = new Node();
        temp.data = data;
        temp.left = null;
        temp.right = null;
        return temp;
    }

    // Insert a Node in binary search tree.
    static Node insert(Node root, int data)
    {
        if (root == null)
            return newNode(data);
        if (data < root.data)
            root.left = insert(root.left, data);
        else if (data > root.data)
            root.right = insert(root.right, data);
        return root;
    }

    // Function for inorder traversal in a BST.
    static void inorder(Node root)
    {
        if (root != null) {
            inorder(root.left);
            System.out.print(root.data + " ");
            inorder(root.right);
        }
    }

    // Delete leaf nodes from binary search tree.
    static Node leafDelete(Node root)
    {
        if (root == null) {
            return null;
        }
        if (root.left == null && root.right == null) {
            return null;
        }

        // Else recursively delete in left and right
        // subtrees.
        root.left = leafDelete(root.left);
        root.right = leafDelete(root.right);

        return root;
    }

    // Driver code
    public static void main(String[] args)
    {
        Node root = null;
        root = insert(root, 20);
        insert(root, 10);
        insert(root, 5);
        insert(root, 15);
        insert(root, 30);
        insert(root, 25);
        insert(root, 35);
        System.out.println("Inorder before Deleting the leaf Node. ");
        inorder(root);
        System.out.println();
        leafDelete(root);
        System.out.println("INorder after Deleting the leaf Node. ");
        inorder(root);
    }
}
// This code is contributed by Prerna saini
```

## 蟒蛇 3

```
# Python 3 program to delete leaf
# Node from binary search tree.

# Create a newNode in binary search tree.
class newNode:

    # Constructor to create a new node
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Insert a Node in binary search tree.
def insert(root, data):
    if root == None:
        return newNode(data)
    if data < root.data:
        root.left = insert(root.left, data)
    elif data > root.data:
        root.right = insert(root.right, data)
    return root

# Function for inorder traversal in a BST.
def inorder(root):
    if root != None:
        inorder(root.left)
        print(root.data, end = " ")
        inorder(root.right)

# Delete leaf nodes from binary search tree.
def leafDelete(root):
    if root == None:
        return None
    if root.left == None and root.right == None:
        return None

    # Else recursively delete in left
    # and right subtrees.
    root.left = leafDelete(root.left)
    root.right = leafDelete(root.right)

    return root

# Driver code
if __name__ == '__main__':
    root = None
    root = insert(root, 20)
    insert(root, 10)
    insert(root, 5)
    insert(root, 15)
    insert(root, 30)
    insert(root, 25)
    insert(root, 35)
    print("Inorder before Deleting the leaf Node.")
    inorder(root)
    leafDelete(root)
    print()
    print("INorder after Deleting the leaf Node.")
    inorder(root)    

# This code is contributed by PranchalK
```

## C#

```
// C# program to delete leaf Node from
// binary search tree.
using System;

class GfG {

    class Node {
        public int data;
        public Node left;
        public Node right;
    }

    // Create a newNode in binary search tree.
    static Node newNode(int data)
    {
        Node temp = new Node();
        temp.data = data;
        temp.left = null;
        temp.right = null;
        return temp;
    }

    // Insert a Node in binary search tree.
    static Node insert(Node root, int data)
    {
        if (root == null)
            return newNode(data);
        if (data < root.data)
            root.left = insert(root.left, data);
        else if (data > root.data)
            root.right = insert(root.right, data);
        return root;
    }

    // Function for inorder traversal in a BST.
    static void inorder(Node root)
    {
        if (root != null) {
            inorder(root.left);
            Console.Write(root.data + " ");
            inorder(root.right);
        }
    }

    // Delete leaf nodes from binary search tree.
    static Node leafDelete(Node root)
    {
        if (root == null) {
            return null;
        }
        if (root.left == null && root.right == null) {
            return null;
        }

        // Else recursively delete in
        // left and right subtrees.
        root.left = leafDelete(root.left);
        root.right = leafDelete(root.right);

        return root;
    }

    // Driver code
    public static void Main(String[] args)
    {
        Node root = null;
        root = insert(root, 20);
        insert(root, 10);
        insert(root, 5);
        insert(root, 15);
        insert(root, 30);
        insert(root, 25);
        insert(root, 35);
        Console.WriteLine("Inorder before Deleting"
                          + "the leaf Node. ");
        inorder(root);
        Console.WriteLine();
        leafDelete(root);
        Console.WriteLine("INorder after Deleting"
                          + "the leaf Node. ");
        inorder(root);
    }
}

// This code has been contributed
// by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript program to delete leaf Node from
// binary search tree.
class Node {
    constructor() {
        this.data = 0;
        this.left = null;
        this.right = null;
    }
}

    // Create a newNode in binary search tree.
    function newNode(data) {
        var temp = new Node();
        temp.data = data;
        temp.left = null;
        temp.right = null;
        return temp;
    }

    // Insert a Node in binary search tree.
    function insert(root , data) {
        if (root == null)
            return newNode(data);
        if (data < root.data)
            root.left = insert(root.left, data);
        else if (data > root.data)
            root.right = insert(root.right, data);
        return root;
    }

    // Function for inorder traversal in a BST.
    function inorder(root) {
        if (root != null) {
            inorder(root.left);
            document.write(root.data + " ");
            inorder(root.right);
        }
    }

    // Delete leaf nodes from binary search tree.
    function leafDelete(root) {
        if (root == null) {
            return null;
        }
        if (root.left == null && root.right == null) {
            return null;
        }

        // Else recursively delete in left and right
        // subtrees.
        root.left = leafDelete(root.left);
        root.right = leafDelete(root.right);

        return root;
    }

    // Driver code

        var root = null;
        root = insert(root, 20);
        insert(root, 10);
        insert(root, 5);
        insert(root, 15);
        insert(root, 30);
        insert(root, 25);
        insert(root, 35);
        document.write(
        "Inorder before Deleting the leaf Node. <br/>"
        );
        inorder(root);
        document.write("<br/>");
        leafDelete(root);
        document.write(
        "INorder after Deleting the leaf Node. <br/>"
        );
        inorder(root);

// This code is contributed by todaysgaurav

</script>
```

**输出:**

```
Inorder before Deleting the leaf node.
5 10 15 20 25 30 35
INorder after Deleting the leaf node.
10 20 30
```

本文由**达曼德拉·库马尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。