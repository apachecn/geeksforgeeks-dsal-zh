# 检查两个二分搜索法树是否相同

> 原文:[https://www . geesforgeks . org/check-这两个二进制搜索树是否相同/](https://www.geeksforgeeks.org/check-whether-the-two-binary-search-trees-are-identical-or-not/)

给定两个二分搜索法树的根节点。如果两个二分搜索法树相同，任务是打印 1，否则打印 0。如果两棵树在结构上相同，并且节点具有相同的值，则它们是相同的。

Tree 1 Tree 2 

在上面的图像中，树 1 和树 2 是相同的。

为了确定两棵树是否相同，我们需要同时遍历这两棵树，并且在遍历时，我们需要比较数据和树的子树。
下面是检查两个 BST 是否相同的分步算法:

1.  如果两棵树都是空的，那么返回 1。
2.  否则如果两棵树都不是空的
    *   检查根节点的数据(tree1->data == tree2->data)
    *   递归检查左子树，即调用 sameTree(tree1->left_subtree，tree2->left_subtree)
    *   递归检查右子树，即调用 sameTree(tree1->right_subtree，tree2->right_subtree)
    *   如果以上三个步骤中返回的值为真，则返回 1。
3.  否则返回 0(一个是空的，另一个不是)。

以下是上述方法的实现:

## C++

```
// C++ program to check if two BSTs
// are identical

#include <iostream>
using namespace std;

// BST node
struct Node {
    int data;
    struct Node* left;
    struct Node* right;
};

// Utility function to create a new Node
struct Node* newNode(int data)
{
    struct Node* node = (struct Node*)
        malloc(sizeof(struct Node));
    node->data = data;
    node->left = NULL;
    node->right = NULL;

    return node;
}

// Function to perform inorder traversal
void inorder(Node* root)
{
    if (root == NULL)
        return;

    inorder(root->left);

    cout << root->data << " ";

    inorder(root->right);
}

// Function to check if two BSTs
// are identical
int isIdentical(Node* root1, Node* root2)
{
    // Check if both the trees are empty
    if (root1 == NULL && root2 == NULL)
        return 1;
    // If any one of the tree is non-empty
    // and other is empty, return false
    else if (root1 != NULL && root2 == NULL)
        return 0;
    else if (root1 == NULL && root2 != NULL)
        return 0;
    else { // Check if current data of both trees equal
        // and recursively check for left and right subtrees
        if (root1->data == root2->data && isIdentical(root1->left, root2->left)
            && isIdentical(root1->right, root2->right))
            return 1;
        else
            return 0;
    }
}

// Driver code
int main()
{
    struct Node* root1 = newNode(5);
    struct Node* root2 = newNode(5);
    root1->left = newNode(3);
    root1->right = newNode(8);
    root1->left->left = newNode(2);
    root1->left->right = newNode(4);

    root2->left = newNode(3);
    root2->right = newNode(8);
    root2->left->left = newNode(2);
    root2->left->right = newNode(4);

    if (isIdentical(root1, root2))
        cout << "Both BSTs are identical";
    else
        cout << "BSTs are not identical";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if two BSTs
// are identical
class GFG
{

// BST node
static class Node
{
    int data;
    Node left;
    Node right;
};

// Utility function to create a new Node
static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = null;
    node.right = null;

    return node;
}

// Function to perform inorder traversal
static void inorder(Node root)
{
    if (root == null)
        return;

    inorder(root.left);

    System.out.print(root.data + " ");

    inorder(root.right);
}

// Function to check if two BSTs
// are identical
static int isIdentical(Node root1,
                       Node root2)
{
    // Check if both the trees are empty
    if (root1 == null && root2 == null)
        return 1;

    // If any one of the tree is non-empty
    // and other is empty, return false
    else if (root1 != null &&
             root2 == null)
        return 0;
    else if (root1 == null &&
             root2 != null)
        return 0;
    else
    {
        // Check if current data of both trees equal
        // and recursively check for left and right subtrees
        if (root1.data == root2.data &&
            isIdentical(root1.left, root2.left) == 1 &&
            isIdentical(root1.right, root2.right) == 1)
            return 1;
        else
            return 0;
    }
}

// Driver code
public static void main(String[] args)
{
    Node root1 = newNode(5);
    Node root2 = newNode(5);
    root1.left = newNode(3);
    root1.right = newNode(8);
    root1.left.left = newNode(2);
    root1.left.right = newNode(4);

    root2.left = newNode(3);
    root2.right = newNode(8);
    root2.left.left = newNode(2);
    root2.left.right = newNode(4);

    if (isIdentical(root1, root2)==1)
        System.out.print("Both BSTs are identical");
    else
        System.out.print("BSTs are not identical");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to contrcut all unique
# BSTs for keys from 1 to n

# Binary Tree Node
""" A utility function to create a
new BST node """
class newNode:

    # Construct to create a newNode
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# Function to perform inorder traversal
def inorder(root) :

    if (root == None):
        return

    inorder(root.left)

    print(root.data, end = " ")

    inorder(root.right)

# Function to check if two BSTs
# are identical
def isIdentical(root1, root2) :

    # Check if both the trees are empty
    if (root1 == None and root2 == None) :
        return 1

    # If any one of the tree is non-empty
    # and other is empty, return false
    elif (root1 != None and root2 == None) :
        return 0
    elif (root1 == None and root2 != None) :
        return 0
    else: # Check if current data of both trees
          # equal and recursively check for left
          # and right subtrees
        if (root1.data == root2.data and
            isIdentical(root1.left, root2.left)
            and isIdentical(root1.right, root2.right)) :
            return 1
        else:
            return 0

# Driver Code
if __name__ == '__main__':

    root1 = newNode(5)
    root2 = newNode(5)
    root1.left = newNode(3)
    root1.right = newNode(8)
    root1.left.left = newNode(2)
    root1.left.right = newNode(4)

    root2.left = newNode(3)
    root2.right = newNode(8)
    root2.left.left = newNode(2)
    root2.left.right = newNode(4)

    if (isIdentical(root1, root2)):
        print("Both BSTs are identical")
    else:
        print("BSTs are not identical")

# This code is contributed by
# Shubham Singh(SHUBHAMSINGH10)
```

## C#

```
// C# program to check if two BSTs
// are identical
using System;

class GFG
{

// BST node
class Node
{
    public int data;
    public Node left;
    public Node right;
};

// Utility function to create a new Node
static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = null;
    node.right = null;

    return node;
}

// Function to perform inorder traversal
static void inorder(Node root)
{
    if (root == null)
        return;

    inorder(root.left);

    Console.Write(root.data + " ");

    inorder(root.right);
}

// Function to check if two BSTs
// are identical
static int isIdentical(Node root1,
                       Node root2)
{
    // Check if both the trees are empty
    if (root1 == null && root2 == null)
        return 1;

    // If any one of the tree is non-empty
    // and other is empty, return false
    else if (root1 != null &&
             root2 == null)
        return 0;
    else if (root1 == null &&
             root2 != null)
        return 0;
    else
    {
        // Check if current data of both trees equal
        // and recursively check for left and right subtrees
        if (root1.data == root2.data &&
            isIdentical(root1.left, root2.left) == 1 &&
            isIdentical(root1.right, root2.right) == 1)
            return 1;
        else
            return 0;
    }
}

// Driver code
public static void Main(String[] args)
{
    Node root1 = newNode(5);
    Node root2 = newNode(5);
    root1.left = newNode(3);
    root1.right = newNode(8);
    root1.left.left = newNode(2);
    root1.left.right = newNode(4);

    root2.left = newNode(3);
    root2.right = newNode(8);
    root2.left.left = newNode(2);
    root2.left.right = newNode(4);

    if (isIdentical(root1, root2) == 1)
        Console.Write("Both BSTs are identical");
    else
        Console.Write("BSTs are not identical");
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// Javascript program to check if two BSTs
// are identical

// BST node
class Node
{
    // Utility function to create a new Node
    constructor(data)
    {
        this.data = data;
        this.left = this.right = null;
    }
}

// Function to perform inorder traversal
function inorder(root)
{
    if (root == null)
        return;

    inorder(root.left);

    document.write(root.data + " ");

    inorder(root.right);
}

// Function to check if two BSTs
// are identical
function isIdentical(root1,root2)
{
    // Check if both the trees are empty
    if (root1 == null && root2 == null)
        return 1;

    // If any one of the tree is non-empty
    // and other is empty, return false
    else if (root1 != null &&
             root2 == null)
        return 0;
    else if (root1 == null &&
             root2 != null)
        return 0;
    else
    {
        // Check if current data of both trees equal
        // and recursively check for left and right subtrees
        if (root1.data == root2.data &&
            isIdentical(root1.left, root2.left) == 1 &&
            isIdentical(root1.right, root2.right) == 1)
            return 1;
        else
            return 0;
    }
}

// Driver code
let root1 = new Node(5);
    let root2 = new Node(5);
    root1.left = new Node(3);
    root1.right = new Node(8);
    root1.left.left = new Node(2);
    root1.left.right = new Node(4);

    root2.left = new Node(3);
    root2.right = new Node(8);
    root2.left.left = new Node(2);
    root2.left.right = new Node(4);

    if (isIdentical(root1, root2)==1)
        document.write("Both BSTs are identical");
    else
        document.write("BSTs are not identical");

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
Both BSTs are identical
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)