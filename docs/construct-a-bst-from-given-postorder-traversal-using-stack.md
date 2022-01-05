# 使用堆栈

根据给定的后序遍历构建一个 BST

> 原文:[https://www . geesforgeks . org/construct-a-BST-from-给定-后置-遍历-使用-stack/](https://www.geeksforgeeks.org/construct-a-bst-from-given-postorder-traversal-using-stack/)

给定二叉查找树的后序遍历，构造 BST。
例如
1。如果给定的遍历是{1，7，5，50，40，10}，那么应该构造下面的树，并返回树的根。

```
     10
   /   \
  5     40
 /  \      \
1    7      50
```

> 输入:1 7 5 50 40 10
> 输出:
> 为了遍历构造的树:
> 1 5 7 10 40 50
> 如果给定的遍历是{2，6，4，9，13，11，7}，那么应该构造下面的树并返回树的根。
> 
> ```
>        7
>      /   \
>     4     11
>    / \    /  \
>   2   6  9    13
> ```
> 
> 输入:2 6 4 9 13 11 7
> 输出:
> 为了遍历构建的树:
> 2 4 6 7 9 11 13

让我们先看看工作[后序遍历](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)。

```
Left
Right 
Root
Hence last node of post order will be root of tree, create it and push to stack.
If next element(i-1) is greater then it should be in right subtree.
If next element(i-1) is less then it should be in left subtree.
```

**算法:**

*   将 BST 的根推入堆栈，即数组的最后一个元素。
*   开始反向遍历数组，如果下一个元素>堆栈顶部的元素，则
    将该元素设置为堆栈顶部元素的右子元素，并将其推入堆栈。
*   否则，如果下一个元素是< the element at the top of the stack then, 
    ，开始弹出堆栈中的所有元素，直到堆栈为空或者当前元素变成>堆栈顶部的元素。
*   使该元素成为最后弹出的节点的左子元素，并重复上述步骤，直到数组被完全遍历。

下面是上述算法的实现。

## C++

```
// C++ implementation of the algorithm
/* A binary tree node has data,
pointer to left child and a pointer
to right child */
#include<bits/stdc++.h>
using namespace std;

// Class Node has data and references
// to the left and the right child.
class Node
{
    public:
    int data;
    Node* left, *right;

    Node(int data)
    {
        this->data = data;
        left = right = NULL;
    }
};

// Function that creates the tree
Node* constructTreeUtil(int post[], int n)
{
    // Last node is root
    Node* root = new Node(post[n - 1]);
    stack<Node*> s;
    s.push(root);

    // Traverse from second last node
    for (int i = n - 2; i >= 0; --i)
    {
        Node* x = new Node(post[i]);

        // Keep popping nodes while top()
        // of stack is greater.
        Node* temp = NULL;
        while (s.size() &&
               post[i] < s.top()->data)
            temp = s.top(), s.pop();    

        // Make x as left child of temp
        if (temp != NULL)
            temp->left = x;    

        // Else make x as right of top    
        else
            s.top()->right = x;
        s.push(x);
    }
    return root;
}

// Function that calls the method
// which contructs the tree
Node* constructTree(int post[], int size)
{
    return constructTreeUtil(post, size);
}

// A utility function to print
// inorder traversal of a Binary Tree
void printInorder(Node* node)
{
    if (node == NULL)
        return;
    printInorder(node->left);
    cout << node->data << " ";
    printInorder(node->right);
}

// Driver Code
int main()
{
    int post[] = { 1, 7, 5, 50, 40, 10 };
    int size = sizeof(post)/sizeof(int);

    Node* root = constructTree(post, size);

    cout << "Inorder traversal of "
         << "the constructed tree:\n";
    printInorder(root);
}

// This code is contributed by Arnab Kundu
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the algorithm
/* A binary tree node has data, pointer to left child
and a pointer to right child */
import java.util.*;

// Class Node has data and references to the left
// and the right child.
class Node {
    int data;
    Node left, right;

    Node(int data)
    {
        this.data = data;
        left = right = null;
    }
}

class BinaryTree {

    // Function that creates the tree
    Node constructTreeUtil(int post[], int n)
    {
        // Last node is root
        Node root = new Node(post[n - 1]);
        Stack<Node> s = new Stack<>();
        s.push(root);

        // Traverse from second last node
        for (int i = n - 2; i >= 0; --i) {

            Node x = new Node(post[i]);

            // Keep popping nodes while top() of stack
            // is greater.
            Node temp = null;
            while (!s.isEmpty() && post[i] < s.peek().data)
                temp = s.pop();     

            // Make x as left child of temp  
            if (temp != null)
                temp.left = x;     

            // Else make x as right of top     
            else
                s.peek().right = x;
            s.push(x);
        }
        return root;
    }

    // Function that calls the method which contructs the tree
    Node constructTree(int post[], int size)
    {
        return constructTreeUtil(post, size);
    }

    // A utility function to print inorder traversal
    // of a Binary Tree
    void printInorder(Node node)
    {
        if (node == null)
            return;
        printInorder(node.left);
        System.out.print(node.data + " ");
        printInorder(node.right);
    }

    // Driver program to test above functions
    public static void main(String[] args)
    {
        BinaryTree tree = new BinaryTree();
        int post[] = new int[] { 1, 7, 5, 50, 40, 10 };
        int size = post.length;

        Node root = tree.constructTree(post, size);

        System.out.println("Inorder traversal of the constructed tree:");
        tree.printInorder(root);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the algorithm
# A binary tree node has data,
# pointer to left child and a pointer
# to right child

# Class Node has data and references
# to the left and the right child.
class Node:
    def __init__(self, data = 0):
        self.data = data
        self.left = None
        self.right = None

# Function that creates the tree
def constructTreeUtil(post , n):

    # Last node is root
    root = Node(post[n - 1])
    s = []
    s.append(root)
    i = n - 2

    # Traverse from second last node
    while ( i >= 0):
        x = Node(post[i])

        # Keep popping nodes while top()
        # of stack is greater.
        temp = None
        while (len(s) > 0 and post[i] < s[-1].data) :
            temp = s[-1]
            s.pop()    

        # Make x as left child of temp
        if (temp != None):
            temp.left = x    

        # Else make x as right of top    
        else:
            s[-1].right = x
        s.append(x)
        i = i - 1

    return root

# Function that calls the method
# which contructs the tree
def constructTree( post, size):
    return constructTreeUtil(post, size)

# A utility function to print
# inorder traversal of a Binary Tree
def printInorder( node):
    if (node == None):
        return
    printInorder(node.left)
    print( node.data, end = " ")
    printInorder(node.right)

# Driver Code
post = [1, 7, 5, 50, 40, 10]
size = len(post)

root = constructTree(post, size)

print( "Inorder traversal of the constructed tree:")
printInorder(root)

# This code is contributed by Arnab Kundu
```

## C#

```
// C# implementation of the algorithm

/* A binary tree node has data,
pointer to left child
and a pointer to right child */
using System;
using System.Collections.Generic;

// Class Node has data and references 
// to the left and the right child.
public class Node
{
    public int data;
    public Node left, right;

    public Node(int data)
    {
        this.data = data;
        left = right = null;
    }
}

public class BinaryTree
{

    // Function that creates the tree
    Node constructTreeUtil(int []post, int n)
    {
        // Last node is root
        Node root = new Node(post[n - 1]);
        Stack<Node> s = new Stack<Node>();
        s.Push(root);

        // Traverse from second last node
        for (int i = n - 2; i >= 0; --i)
        {

            Node x = new Node(post[i]);

            // Keep popping nodes while top() of stack
            // is greater.
            Node temp = null;
            while (s.Count!=0 && post[i] < s.Peek().data)
                temp = s.Pop();    

            // Make x as left child of temp
            if (temp != null)
                temp.left = x;    

            // Else make x as right of top    
            else
                s.Peek().right = x;
            s.Push(x);
        }
        return root;
    }

    // Function that calls the
    // method which contructs the tree
    Node constructTree(int []post, int size)
    {
        return constructTreeUtil(post, size);
    }

    // A utility function to print 
    // inorder traversal of a Binary Tree
    void printInorder(Node node)
    {
        if (node == null)
            return;
        printInorder(node.left);
        Console.Write(node.data + " ");
        printInorder(node.right);
    }

    // Driver code
    public static void Main()
    {
        BinaryTree tree = new BinaryTree();
        int []post = new int[] { 1, 7, 5, 50, 40, 10 };
        int size = post.Length;

        Node root = tree.constructTree(post, size);

        Console.WriteLine("Inorder traversal of the constructed tree:");
        tree.printInorder(root);
    }
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// JavaScript implementation of the algorithm

/* A binary tree node has data,
pointer to left child
and a pointer to right child */

// Class Node has data and references 
// to the left and the right child.
class Node
{
    constructor(data)
    {
        this.data = data;
        this.left = null;
        this.right = null;
    }
}

// Function that creates the tree
function constructTreeUtil(post, n)
{
    // Last node is root
    var root = new Node(post[n - 1]);
    var s = [];
    s.push(root);
    // Traverse from second last node
    for (var i = n - 2; i >= 0; --i)
    {

        var x = new Node(post[i]);
        // Keep popping nodes while top() of stack
        // is greater.
        var temp = null;
        while (s.length!=0 && post[i] < s[s.length-1].data)
            temp = s.pop();    
        // Make x as left child of temp
        if (temp != null)
            temp.left = x;    
        // Else make x as right of top    
        else
            s[s.length-1].right = x;
        s.push(x);
    }
    return root;
}
// Function that calls the
// method which contructs the tree
function constructTree(post, size)
{
    return constructTreeUtil(post, size);
}
// A utility function to print 
// inorder traversal of a Binary Tree
function printInorder(node)
{
    if (node == null)
        return;
    printInorder(node.left);
    document.write(node.data + " ");
    printInorder(node.right);
}
// Driver code
var post = [1, 7, 5, 50, 40, 10];
var size = post.length;
var root = constructTree(post, size);
document.write("Inorder traversal of the constructed tree:<br>");
printInorder(root);

</script>
```

**Output:** 

```
Inorder traversal of the constructed tree:
1 5 7 10 40 50
```