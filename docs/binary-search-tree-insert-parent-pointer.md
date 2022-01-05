# 带有父指针的二叉查找树插件

> 原文:[https://www . geesforgeks . org/binary-search-tree-insert-parent-pointer/](https://www.geeksforgeeks.org/binary-search-tree-insert-parent-pointer/)

我们已经讨论了[简单的 BST 插入](https://www.geeksforgeeks.org/binary-search-tree-set-1-search-and-insertion/)。如何在需要维护父指针的树中插入？父指针有助于快速找到一个节点的祖先、两个节点的 LCA、一个节点的后继等等。

在简单插入的递归调用中，我们返回在子树中创建的子树根的指针。所以这个想法是为左右子树存储这个指针。我们在递归调用之后设置这个返回指针的父指针。这确保在插入过程中设置了所有父指针。根的父级设置为空。我们通过默认将父节点指定为空来处理这个问题。

## C++

```
// C++ program to demonstrate insert operation
// in binary search tree with parent pointer
#include<bits/stdc++.h>

struct Node
{
    int key;
    struct Node *left, *right, *parent;
};

// A utility function to create a new BST Node
struct Node *newNode(int item)
{
    struct Node *temp =  new Node;
    temp->key = item;
    temp->left = temp->right = NULL;
    temp->parent = NULL;
    return temp;
}

// A utility function to do inorder traversal of BST
void inorder(struct Node *root)
{
    if (root != NULL)
    {
        inorder(root->left);
        printf("Node : %d, ", root->key);
        if (root->parent == NULL)
          printf("Parent : NULL \n");
        else
          printf("Parent : %d \n", root->parent->key);
        inorder(root->right);
    }
}

/* A utility function to insert a new Node with
   given key in BST */
struct Node* insert(struct Node* node, int key)
{
    /* If the tree is empty, return a new Node */
    if (node == NULL) return newNode(key);

    /* Otherwise, recur down the tree */
    if (key < node->key)
    {
        Node *lchild = insert(node->left, key);
        node->left  = lchild;

        // Set parent of root of left subtree
        lchild->parent = node;
    }
    else if (key > node->key)
    {
        Node *rchild = insert(node->right, key);
        node->right  = rchild;

        // Set parent of root of right subtree
        rchild->parent = node;
    }

    /* return the (unchanged) Node pointer */
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
    struct Node *root = NULL;
    root = insert(root, 50);
    insert(root, 30);
    insert(root, 20);
    insert(root, 40);
    insert(root, 70);
    insert(root, 60);
    insert(root, 80);

    // print inorder traversal of the BST
    inorder(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to demonstrate insert operation
// in binary search tree with parent pointer
class GfG {

static class Node
{
    int key;
    Node left, right, parent;
}

// A utility function to create a new BST Node
static Node newNode(int item)
{
    Node temp = new Node();
    temp.key = item;
    temp.left = null;
    temp.right = null;
    temp.parent = null;
    return temp;
}

// A utility function to do inorder traversal of BST
static void inorder(Node root)
{
    if (root != null)
    {
        inorder(root.left);
        System.out.print("Node : "+ root.key + " , ");
        if (root.parent == null)
        System.out.println("Parent : NULL");
        else
        System.out.println("Parent : " + root.parent.key);
        inorder(root.right);
    }
}

/* A utility function to insert a new Node with
given key in BST */
static Node insert(Node node, int key)
{
    /* If the tree is empty, return a new Node */
    if (node == null) return newNode(key);

    /* Otherwise, recur down the tree */
    if (key < node.key)
    {
        Node lchild = insert(node.left, key);
        node.left = lchild;

        // Set parent of root of left subtree
        lchild.parent = node;
    }
    else if (key > node.key)
    {
        Node rchild = insert(node.right, key);
        node.right = rchild;

        // Set parent of root of right subtree
        rchild.parent = node;
    }

    /* return the (unchanged) Node pointer */
    return node;
}

// Driver Program to test above functions
public static void main(String[] args)
{
    /* Let us create following BST
            50
        /     \
        30     70
        / \ / \
    20 40 60 80 */
    Node root = null;
    root = insert(root, 50);
    insert(root, 30);
    insert(root, 20);
    insert(root, 40);
    insert(root, 70);
    insert(root, 60);
    insert(root, 80);

    // print iNorder traversal of the BST
    inorder(root);
}
}
```

## 蟒蛇 3

```
# Python3 program to demonstrate insert operation
# in binary search tree with parent pointer

# A utility function to create a new BST Node
class newNode:
    def __init__(self, item):
        self.key = item
        self.left = self.right = None
        self.parent = None

# A utility function to do inorder
# traversal of BST
def inorder(root):
    if root != None:
        inorder(root.left)
        print("Node :", root.key, ", ", end = "")
        if root.parent == None:
            print("Parent : NULL")
        else:
            print("Parent : ", root.parent.key)
        inorder(root.right)

# A utility function to insert a new
# Node with given key in BST
def insert(node, key):

    # If the tree is empty, return a new Node
    if node == None:
        return newNode(key)

    # Otherwise, recur down the tree
    if key < node.key:
        lchild = insert(node.left, key)
        node.left = lchild

        # Set parent of root of left subtree
        lchild.parent = node
    elif key > node.key:
        rchild = insert(node.right, key)
        node.right = rchild

        # Set parent of root of right subtree
        rchild.parent = node

    # return the (unchanged) Node pointer
    return node

# Driver Code
if __name__ == '__main__':

    # Let us create following BST
    #         50
    #     /     \
    #     30     70
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

    # print iNorder traversal of the BST
    inorder(root)

# This code is contributed by PranchalK
```

## C#

```
// C# program to demonstrate insert operation
// in binary search tree with parent pointer
using System;

class GfG
{
    class Node
    {
        public int key;
        public Node left, right, parent;
    }

    // A utility function to create a new BST Node
    static Node newNode(int item)
    {
        Node temp = new Node();
        temp.key = item;
        temp.left = null;
        temp.right = null;
        temp.parent = null;
        return temp;
    }

    // A utility function to do
    // inorder traversal of BST
    static void inorder(Node root)
    {
        if (root != null)
        {
            inorder(root.left);
            Console.Write("Node : "+ root.key + " , ");
            if (root.parent == null)
            Console.WriteLine("Parent : NULL");
            else
            Console.WriteLine("Parent : " +
                                root.parent.key);
            inorder(root.right);
        }
    }

    /* A utility function to insert a new Node with
    given key in BST */
    static Node insert(Node node, int key)
    {
        /* If the tree is empty, return a new Node */
        if (node == null) return newNode(key);

        /* Otherwise, recur down the tree */
        if (key < node.key)
        {
            Node lchild = insert(node.left, key);
            node.left = lchild;

            // Set parent of root of left subtree
            lchild.parent = node;
        }
        else if (key > node.key)
        {
            Node rchild = insert(node.right, key);
            node.right = rchild;

            // Set parent of root of right subtree
            rchild.parent = node;
        }

        /* return the (unchanged) Node pointer */
        return node;
    }

    // Driver code
    public static void Main(String[] args)
    {
        /* Let us create following BST
                50
            / \
            30 70
            / \ / \
        20 40 60 80 */
        Node root = null;
        root = insert(root, 50);
        insert(root, 30);
        insert(root, 20);
        insert(root, 40);
        insert(root, 70);
        insert(root, 60);
        insert(root, 80);

        // print iNorder traversal of the BST
        inorder(root);
    }
}

// This code is contributed 29AjayKumar
```

## java 描述语言

```
<script>
// javascript program to demonstrate insert operation
// in binary search tree with parent pointer

     class Node {
            constructor() {
                this.key = 0;
                this.left = null;
                this.right = null;
                this.parent = null;
            }
        }

// A utility function to create a new BST Node
function newNode(item)
{
    var temp = new Node();
    temp.key = item;
    temp.left = null;
    temp.right = null;
    temp.parent = null;
    return temp;
}

// A utility function to do inorder traversal of BST
function inorder(root)
{
    if (root != null)
    {
        inorder(root.left);
        document.write("Node : "+ root.key + " , ");
        if (root.parent == null)
        document.write("Parent : NULL<br/>");
        else
        document.write("Parent : " + root.parent.key+"<br/>");
        inorder(root.right);
    }
}

/* A utility function to insert a new Node with
given key in BST */
function insert(node , key)
{
    /* If the tree is empty, return a new Node */
    if (node == null) return newNode(key);

    /* Otherwise, recur down the tree */
    if (key < node.key)
    {
        var lchild = insert(node.left, key);
        node.left = lchild;

        // Set parent of root of left subtree
        lchild.parent = node;
    }
    else if (key > node.key)
    {
        var rchild = insert(node.right, key);
        node.right = rchild;

        // Set parent of root of right subtree
        rchild.parent = node;
    }

    /* return the (unchanged) Node pointer */
    return node;
}

// Driver Program to test above functions

    /* Let us create following BST
            50
        /     \
        30     70
        / \ / \
    20 40 60 80 */
    var root = null;
    root = insert(root, 50);
    insert(root, 30);
    insert(root, 20);
    insert(root, 40);
    insert(root, 70);
    insert(root, 60);
    insert(root, 80);

    // print iNorder traversal of the BST
    inorder(root);

// This code contributed by umadevi9616
</script>
```

**输出:**

```
Node : 20, Parent : 30 
Node : 30, Parent : 50 
Node : 40, Parent : 30 
Node : 50, Parent : NULL 
Node : 60, Parent : 70 
Node : 70, Parent : 50 
Node : 80, Parent : 70 
```

**练习:**
删除时如何维护父指针。
本文由**舒巴姆·古普塔**供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息