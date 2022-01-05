# 在二叉树中用深度替换节点

> 原文:[https://www . geesforgeks . org/用二叉树深度替换节点/](https://www.geeksforgeeks.org/replace-node-with-depth-in-a-binary-tree/)

给定一棵二叉树，用深度值替换每个节点。例如，考虑下面的树。根位于深度 0，将其值更改为 0，下一级节点位于深度 1，以此类推。

```
       3                       0
      /  \                    /   \
     2    5      == >;         1     1
   /   \                   /   \
  1     4                 2     2
```

想法是从根开始遍历树。以节点的通过深度为参数。我们可以跟踪深度，对根传递 0，对孩子传递 1 加当前深度。
下面是想法的实现。

## C++

```
// CPP program to replace every key value
// with its depth.
#include<bits/stdc++.h>
using namespace std;

/* A tree node structure */
struct Node
{
    int data;
    struct Node *left, *right;
};

/* Utility function to create a
   new Binary Tree node */
struct Node* newNode(int data)
{
    Node *temp = new Node;
    temp->data = data;
    temp->left = temp->right = NULL;   
    return temp;
}

// Helper function replaces the data with depth
// Note : Default value of level is 0 for root.
void replaceNode(struct Node *node, int level=0)
{
    // Base Case
    if (node == NULL)
        return;

    // Replace data with current depth
    node->data = level;

    replaceNode(node->left, level+1);
    replaceNode(node->right, level+1);
}

// A utility function to print inorder
// traversal of a Binary Tree
void printInorder(struct Node* node)
{
     if (node == NULL)
          return;
     printInorder(node->left);
     cout << node->data <<" ";
     printInorder(node->right);
}

/* Driver function to test above functions */
int main()
{
    struct Node *root = new struct Node;

    /* Constructing tree given in
       the above figure */
    root = newNode(3);
    root->left = newNode(2);
    root->right = newNode(5);
    root->left->left = newNode(1);
    root->left->right = newNode(4);

    cout << "Before Replacing Nodes\n";   
    printInorder(root);
    replaceNode(root); 
    cout << endl;

    cout << "After Replacing Nodes\n";
    printInorder(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to replace every key value
// with its depth.
class GfG {

/* A tree node structure */
static class Node
{
    int data;
    Node left, right;
}

/* Utility function to create a
new Binary Tree node */
static Node newNode(int data)
{
    Node temp = new Node();
    temp.data = data;
    temp.left = null;
    temp.right = null;    
    return temp;
}

// Helper function replaces the data with depth
// Note : Default value of level is 0 for root.
static void replaceNode(Node node, int level)
{
    // Base Case
    if (node == null)
        return;

    // Replace data with current depth
    node.data = level;

    replaceNode(node.left, level+1);
    replaceNode(node.right, level+1);
}

// A utility function to print inorder
// traversal of a Binary Tree
static void printInorder(Node node)
{
    if (node == null)
        return;
    printInorder(node.left);
    System.out.print(node.data + " ");
    printInorder(node.right);
}

/* Driver function to test above functions */
public static void main(String[] args)
{
    Node root = new Node();

    /* Constructing tree given in
    the above figure */
    root = newNode(3);
    root.left = newNode(2);
    root.right = newNode(5);
    root.left.left = newNode(1);
    root.left.right = newNode(4);

    System.out.println("Before Replacing Nodes");    
    printInorder(root);
    replaceNode(root, 0);
    System.out.println();

    System.out.println("After Replacing Nodes");
    printInorder(root);

}
}
```

## 蟒蛇 3

```
# Python3 program to replace every key
# value with its depth.

class newNode:
    def __init__(self, data):
        self.data = data
        self.left = self.right = None

# Helper function replaces the data with depth
# Note : Default value of level is 0 for root.
def replaceNode(node, level = 0):

    # Base Case
    if (node == None):
        return

    # Replace data with current depth
    node.data = level

    replaceNode(node.left, level + 1)
    replaceNode(node.right, level + 1)

# A utility function to prinorder
# traversal of a Binary Tree
def printInorder(node):
    if (node == None):
        return
    printInorder(node.left)
    print(node.data, end = " ")
    printInorder(node.right)

# Driver Code
if __name__ == '__main__':

    # Constructing tree given in
    # the above figure
    root = newNode(3)
    root.left = newNode(2)
    root.right = newNode(5)
    root.left.left = newNode(1)
    root.left.right = newNode(4)

    print("Before Replacing Nodes")    
    printInorder(root)
    replaceNode(root)

    print()
    print("After Replacing Nodes")
    printInorder(root)

# This code is contributed by PranchalK
```

## C#

```
// C# program to replace every key value
// with its depth.
using System;

public class GfG
{

    /* A tree node structure */
    public class Node
    {
        public int data;
        public Node left, right;
    }

    /* Utility function to create a
    new Binary Tree node */
    static Node newNode(int data)
    {
        Node temp = new Node();
        temp.data = data;
        temp.left = null;
        temp.right = null;    
        return temp;
    }

    // Helper function replaces the data with depth
    // Note : Default value of level is 0 for root.
    static void replaceNode(Node node, int level)
    {
        // Base Case
        if (node == null)
            return;

        // Replace data with current depth
        node.data = level;

        replaceNode(node.left, level + 1);
        replaceNode(node.right, level + 1);
    }

    // A utility function to print inorder
    // traversal of a Binary Tree
    static void printInorder(Node node)
    {
        if (node == null)
            return;
        printInorder(node.left);
        Console.Write(node.data + " ");
        printInorder(node.right);
    }

    /* Driver code*/
    public static void Main(String[] args)
    {
        Node root = new Node();

        /* Constructing tree given in
        the above figure */
        root = newNode(3);
        root.left = newNode(2);
        root.right = newNode(5);
        root.left.left = newNode(1);
        root.left.right = newNode(4);

        Console.WriteLine("Before Replacing Nodes");    
        printInorder(root);
        replaceNode(root, 0);
        Console.WriteLine();

        Console.WriteLine("After Replacing Nodes");
        printInorder(root);
    }
}

// This code is contributed Rajput-Ji
```

## java 描述语言

```
<script>

    // JavaScript program to replace every
    // key value with its depth.

    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }  

    /* Utility function to create a
    new Binary Tree node */
    function newNode(data)
    {
        let temp = new Node(data);
        return temp;
    }

    // Helper function replaces the data with depth
    // Note : Default value of level is 0 for root.
    function replaceNode(node, level)
    {
        // Base Case
        if (node == null)
            return;

        // Replace data with current depth
        node.data = level;

        replaceNode(node.left, level+1);
        replaceNode(node.right, level+1);
    }

    // A utility function to print inorder
    // traversal of a Binary Tree
    function printInorder(node)
    {
        if (node == null)
            return;
        printInorder(node.left);
        document.write(node.data + " ");
        printInorder(node.right);
    }

    let root = new Node();

    /* Constructing tree given in
    the above figure */
    root = newNode(3);
    root.left = newNode(2);
    root.right = newNode(5);
    root.left.left = newNode(1);
    root.left.right = newNode(4);

    document.write("Before Replacing Nodes" + "</br>");    
    printInorder(root);
    replaceNode(root, 0);
    document.write("</br>");
    document.write("</br>");

    document.write("After Replacing Nodes" + "</br>");
    printInorder(root);

</script>
```

**输出:**

```
Before Replacing Nodes
1 2 4 3 5 

After Replacing Nodes
2 1 2 0 1 
```

本文由 **Chhavi** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。