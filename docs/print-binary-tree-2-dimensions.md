# 二维打印二叉树

> 原文:[https://www . geesforgeks . org/print-binary-tree-2-dimensions/](https://www.geeksforgeeks.org/print-binary-tree-2-dimensions/)

给定一棵二叉树，用二维打印它。
**例:**

```
Input : Pointer to root of below tree
             1
            /  \
           2    3 
          / \   / \
         4   5  6  7 

Output :
                    7

          3

                    6

1

                    5

          2

                    4
```

**我们强烈建议你尽量减少浏览器，先自己试试这个。**
如果我们仔细观察这个模式，我们可以注意到以下几点。
1)最右边的节点打印在第一行，最左边的节点打印在最后一行。
2)每个等级的空间计数增加固定的数量。
所以我们进行反向有序遍历(右-根-左)并打印树节点。我们在每一级都以固定的数量增加空间。
下面是实现。

## C++

```
// C++ Program to print binary tree in 2D
#include<bits/stdc++.h>

using namespace std;
#define COUNT 10

// A binary tree node
class Node
{
    public:
    int data;
    Node* left, *right;

    /* Constructor that allocates a new node with the
    given data and NULL left and right pointers. */
    Node(int data){
        this->data = data;
        this->left = NULL;
        this->right = NULL;
    }
};

// Function to print binary tree in 2D
// It does reverse inorder traversal
void print2DUtil(Node *root, int space)
{
    // Base case
    if (root == NULL)
        return;

    // Increase distance between levels
    space += COUNT;

    // Process right child first
    print2DUtil(root->right, space);

    // Print current node after space
    // count
    cout<<endl;
    for (int i = COUNT; i < space; i++)
        cout<<" ";
    cout<<root->data<<"\n";

    // Process left child
    print2DUtil(root->left, space);
}

// Wrapper over print2DUtil()
void print2D(Node *root)
{
    // Pass initial space count as 0
    print2DUtil(root, 0);
}

// Driver code
int main()
{
    Node *root = new Node(1);
    root->left = new Node(2);
    root->right = new Node(3);

    root->left->left = new Node(4);
    root->left->right = new Node(5);
    root->right->left = new Node(6);
    root->right->right = new Node(7);

    root->left->left->left = new Node(8);
    root->left->left->right = new Node(9);
    root->left->right->left = new Node(10);
    root->left->right->right = new Node(11);
    root->right->left->left = new Node(12);
    root->right->left->right = new Node(13);
    root->right->right->left = new Node(14);
    root->right->right->right = new Node(15);

    print2D(root);

    return 0;
}

// This code is contributed by rathbhupendra
```

## C

```
// Program to print binary tree in 2D
#include<stdio.h>
#include<malloc.h>
#define COUNT 10

// A binary tree node
struct Node
{
    int data;
    struct Node* left, *right;
};

// Helper function to allocates a new node
struct Node* newNode(int data)
{
    struct Node* node = malloc(sizeof(struct Node));
    node->data = data;
    node->left = node->right = NULL;
    return node;
}

// Function to print binary tree in 2D
// It does reverse inorder traversal
void print2DUtil(struct Node *root, int space)
{
    // Base case
    if (root == NULL)
        return;

    // Increase distance between levels
    space += COUNT;

    // Process right child first
    print2DUtil(root->right, space);

    // Print current node after space
    // count
    printf("\n");
    for (int i = COUNT; i < space; i++)
        printf(" ");
    printf("%d\n", root->data);

    // Process left child
    print2DUtil(root->left, space);
}

// Wrapper over print2DUtil()
void print2D(struct Node *root)
{
   // Pass initial space count as 0
   print2DUtil(root, 0);
}

// Driver program to test above functions
int main()
{
    struct Node *root   = newNode(1);
    root->left   = newNode(2);
    root->right  = newNode(3);

    root->left->left  = newNode(4);
    root->left->right = newNode(5);
    root->right->left  = newNode(6);
    root->right->right = newNode(7);

    root->left->left->left  = newNode(8);
    root->left->left->right  = newNode(9);
    root->left->right->left  = newNode(10);
    root->left->right->right  = newNode(11);
    root->right->left->left  = newNode(12);
    root->right->left->right  = newNode(13);
    root->right->right->left  = newNode(14);
    root->right->right->right  = newNode(15);

    print2D(root);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to print binary tree in 2D
class GFG
{

static final int COUNT = 10;

// A binary tree node
static class Node
{
    int data;
    Node left, right;

    /* Constructor that allocates a new node with the
    given data and null left and right pointers. */
    Node(int data)
    {
        this.data = data;
        this.left = null;
        this.right = null;
    }
};

// Function to print binary tree in 2D
// It does reverse inorder traversal
static void print2DUtil(Node root, int space)
{
    // Base case
    if (root == null)
        return;

    // Increase distance between levels
    space += COUNT;

    // Process right child first
    print2DUtil(root.right, space);

    // Print current node after space
    // count
    System.out.print("\n");
    for (int i = COUNT; i < space; i++)
        System.out.print(" ");
    System.out.print(root.data + "\n");

    // Process left child
    print2DUtil(root.left, space);
}

// Wrapper over print2DUtil()
static void print2D(Node root)
{
    // Pass initial space count as 0
    print2DUtil(root, 0);
}

// Driver code
public static void main(String args[])
{
    Node root = new Node(1);
    root.left = new Node(2);
    root.right = new Node(3);

    root.left.left = new Node(4);
    root.left.right = new Node(5);
    root.right.left = new Node(6);
    root.right.right = new Node(7);

    root.left.left.left = new Node(8);
    root.left.left.right = new Node(9);
    root.left.right.left = new Node(10);
    root.left.right.right = new Node(11);
    root.right.left.left = new Node(12);
    root.right.left.right = new Node(13);
    root.right.right.left = new Node(14);
    root.right.right.right = new Node(15);

    print2D(root);
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 Program to print binary tree in 2D
COUNT = [10]

# Binary Tree Node
""" utility that allocates a newNode
with the given key """
class newNode:

    # Construct to create a newNode
    def __init__(self, key):
        self.data = key
        self.left = None
        self.right = None

# Function to print binary tree in 2D
# It does reverse inorder traversal
def print2DUtil(root, space) :

    # Base case
    if (root == None) :
        return

    # Increase distance between levels
    space += COUNT[0]

    # Process right child first
    print2DUtil(root.right, space)

    # Print current node after space
    # count
    print()
    for i in range(COUNT[0], space):
        print(end = " ")
    print(root.data)

    # Process left child
    print2DUtil(root.left, space)

# Wrapper over print2DUtil()
def print2D(root) :

    # space=[0]
    # Pass initial space count as 0
    print2DUtil(root, 0)

# Driver Code
if __name__ == '__main__':

    root = newNode(1)
    root.left = newNode(2)
    root.right = newNode(3)

    root.left.left = newNode(4)
    root.left.right = newNode(5)
    root.right.left = newNode(6)
    root.right.right = newNode(7)

    root.left.left.left = newNode(8)
    root.left.left.right = newNode(9)
    root.left.right.left = newNode(10)
    root.left.right.right = newNode(11)
    root.right.left.left = newNode(12)
    root.right.left.right = newNode(13)
    root.right.right.left = newNode(14)
    root.right.right.right = newNode(15)

    print2D(root)

# This code is contributed by
# Shubham Singh(SHUBHAMSINGH10)
```

## C#

```
// C# Program to print binary tree in 2D
using System;

class GFG
{

static readonly int COUNT = 10;

// A binary tree node
public class Node
{
    public int data;
    public Node left, right;

    /* Constructor that allocates a new node with the
    given data and null left and right pointers. */
    public Node(int data)
    {
        this.data = data;
        this.left = null;
        this.right = null;
    }
};

// Function to print binary tree in 2D
// It does reverse inorder traversal
static void print2DUtil(Node root, int space)
{
    // Base case
    if (root == null)
        return;

    // Increase distance between levels
    space += COUNT;

    // Process right child first
    print2DUtil(root.right, space);

    // Print current node after space
    // count
    Console.Write("\n");
    for (int i = COUNT; i < space; i++)
        Console.Write(" ");
    Console.Write(root.data + "\n");

    // Process left child
    print2DUtil(root.left, space);
}

// Wrapper over print2DUtil()
static void print2D(Node root)
{
    // Pass initial space count as 0
    print2DUtil(root, 0);
}

// Driver code
public static void Main(String []args)
{
    Node root = new Node(1);
    root.left = new Node(2);
    root.right = new Node(3);

    root.left.left = new Node(4);
    root.left.right = new Node(5);
    root.right.left = new Node(6);
    root.right.right = new Node(7);

    root.left.left.left = new Node(8);
    root.left.left.right = new Node(9);
    root.left.right.left = new Node(10);
    root.left.right.right = new Node(11);
    root.right.left.left = new Node(12);
    root.right.left.right = new Node(13);
    root.right.right.left = new Node(14);
    root.right.right.right = new Node(15);

    print2D(root);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// JavaScript Program to print binary tree in 2D

let COUNT = 10;

// A binary tree node
class Node
{
    constructor(data)
    {
        this.data = data;
        this.left = null;
        this.right = null;
    }
}

// Function to print binary tree in 2D
// It does reverse inorder traversal
function print2DUtil(root,space)
{
    // Base case
    if (root == null)
        return;

    // Increase distance between levels
    space += COUNT;

    // Process right child first
    print2DUtil(root.right, space);

    // Print current node after space
    // count
    document.write("<br>");
    for (let i = COUNT; i < space; i++)
        document.write("  ");
    document.write(root.data + "\n");

    // Process left child
    print2DUtil(root.left, space);
}

// Wrapper over print2DUtil()
function print2D(root)
{
    // Pass initial space count as 0
    print2DUtil(root, 0);
}

// Driver code
let root = new Node(1);
root.left = new Node(2);
root.right = new Node(3);

root.left.left = new Node(4);
root.left.right = new Node(5);
root.right.left = new Node(6);
root.right.right = new Node(7);

root.left.left.left = new Node(8);
root.left.left.right = new Node(9);
root.left.right.left = new Node(10);
root.left.right.right = new Node(11);
root.right.left.left = new Node(12);
root.right.left.right = new Node(13);
root.right.right.left = new Node(14);
root.right.right.right = new Node(15);

print2D(root);

// This code is contributed by patel2127

</script>
```

**输出:**

```
                              15

                    7

                              14

          3

                              13

                    6

                              12

1

                              11

                    5

                              10

          2

                              9

                    4

                              8
```

**使用层级顺序遍历的另一种解决方案:**

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.LinkedList;

public class Tree1 {

    public static void main(String[] args) {

        Tree1.Node root = new Tree1.Node(1);
        Tree1.Node temp = null;
        temp = new Tree1.Node(2);
        root.left=temp;
        temp = new Tree1.Node(3);
        root.right=temp;

        temp = new Tree1.Node(4);
        root.left.left = temp;
        temp=new Tree1.Node(5);
        root.left.right =temp;
        temp=new Tree1.Node(6);
        root.right.left =temp;
        temp=new Tree1.Node(7);
        root.right.right = temp;

        temp = new Tree1.Node(8);
        root.left.left.left = temp;
        temp = new Tree1.Node(9);
        root.left.left.right = temp;
        temp=new Tree1.Node(10);
        root.left.right.left = temp;
        temp=new Tree1.Node(11);
        root.left.right.right = temp;
        temp=new Tree1.Node(12);
        root.right.left.left = temp;
        temp=new Tree1.Node(13);
        root.right.left.right = temp;
        temp=new Tree1.Node(14);
        root.right.right.left = temp;
        temp=new Tree1.Node(15);
        root.right.right.right = temp;

        printBinaryTree(root);

    }

public static class Node{

    public Node(int data){
        this.data = data;
    }
    int data;
    Node left;
    Node right;
}

    public static void printBinaryTree(Node root) {
        LinkedList<Node> treeLevel = new LinkedList<Node>();
        treeLevel.add(root);
        LinkedList<Node> temp = new LinkedList<Node>();
        int counter = 0;
        int height = heightOfTree(root)-1;
        //System.out.println(height);
        double numberOfElements = (Math.pow(2 , (height + 1)) - 1);
        //System.out.println(numberOfElements);
        while (counter <= height) {
            Node removed = treeLevel.removeFirst();
            if (temp.isEmpty()) {
                printSpace(numberOfElements / Math.pow(2 , counter + 1), removed);
            } else {
                printSpace(numberOfElements / Math.pow(2 , counter), removed);
            }
            if (removed == null) {
                temp.add(null);
                temp.add(null);
            } else {
                temp.add(removed.left);
                temp.add(removed.right);
            }

            if (treeLevel.isEmpty()) {
                System.out.println("");
                System.out.println("");
                treeLevel = temp;
                temp = new LinkedList<>();
                counter++;
            }

        }
    }

public static void printSpace(double n, Node removed){
    for(;n>0;n--) {
            System.out.print("\t");
    }
    if(removed == null){
        System.out.print(" ");
    }
    else {
        System.out.print(removed.data);
    }
}

public static int heightOfTree(Node root){
    if(root==null){
        return 0;
    }
     return 1+ Math.max(heightOfTree(root.left),heightOfTree(root.right));
}

}
```

**Output**

```
                                1

                2                                3

        4                5                6                7

    8        9        10        11        12        13        14        15
```

**输出:**

本文由**阿迪蒂亚·戈尔**供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如发现任何不正确的地方，请写评论，或者您想分享更多关于上述话题的信息