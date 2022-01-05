# 连续树

> 原文:[https://www.geeksforgeeks.org/continuous-tree/](https://www.geeksforgeeks.org/continuous-tree/)

如果在每个根到叶路径中，两个相邻的键之间的绝对差是 1，则树是连续树。给我们一棵二叉树，我们需要检查树是否连续。

示例:

```
Input :              3
                    / \
                   2   4
                  / \   \
                 1   3   5
Output: "Yes"

// 3->2->1 every two adjacent node's absolute difference is 1
// 3->2->3 every two adjacent node's absolute difference is 1
// 3->4->5 every two adjacent node's absolute difference is 1

Input :              7
                    / \
                   5   8
                  / \   \
                 6   4   10
Output: "No"

// 7->5->6 here absolute difference of 7 and 5 is not 1.
// 7->5->4 here absolute difference of 7 and 5 is not 1.
// 7->8->10 here absolute difference of 8 and 10 is not 1.
```

解决方案需要遍历树。要检查的重要事情是确保所有角落的案件都得到处理。拐角情况包括空树、单节点树、只有左子节点的节点和只有右子节点的节点。
在树遍历中，我们递归检查左右子树是否连续。我们还检查当前节点的键与其子键之间的键差是否为 1。下面是这个想法的实现。

## C++

```
// C++ program to check if a tree is continuous or not
#include<bits/stdc++.h>
using namespace std;

/* A binary tree node has data, pointer to left child
   and a pointer to right child */
struct Node
{
    int data;
    struct Node* left, * right;
};

/* Helper function that allocates a new node with the
   given data and NULL left and right pointers. */
struct Node* newNode(int data)
{
    struct Node* node = new Node;
    node->data = data;
    node->left = node->right = NULL;
    return(node);
}

// Function to check tree is continuous or not
bool treeContinuous(struct Node *ptr)
{
    // if next node is empty then return true
    if (ptr == NULL)
        return true;

    // if current node is leaf node then return true
    // because it is end of root to leaf path
    if (ptr->left == NULL && ptr->right == NULL)
        return true;

    // If left subtree is empty, then only check right
    if (ptr->left == NULL)
       return (abs(ptr->data - ptr->right->data) == 1) &&
              treeContinuous(ptr->right);

    // If right subtree is empty, then only check left
    if (ptr->right == NULL)
       return (abs(ptr->data - ptr->left->data) == 1) &&
              treeContinuous(ptr->left);

    // If both left and right subtrees are not empty, check
    // everything
    return  abs(ptr->data - ptr->left->data)==1 &&
            abs(ptr->data - ptr->right->data)==1 &&
            treeContinuous(ptr->left) &&
            treeContinuous(ptr->right);
}

/* Driver program to test mirror() */
int main()
{
    struct Node *root = newNode(3);
    root->left        = newNode(2);
    root->right       = newNode(4);
    root->left->left  = newNode(1);
    root->left->right = newNode(3);
    root->right->right = newNode(5);
    treeContinuous(root)?  cout << "Yes" : cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a tree is continuous or not
import java.util.*;

class solution
{

/* A binary tree node has data, pointer to left child
and a pointer to right child */
static class Node
{
    int data;
    Node left, right;
};

/* Helper function that allocates a new node with the
given data and null left and right pointers. */

static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = node.right = null;
    return(node);
}

// Function to check tree is continuous or not

static boolean treeContinuous( Node ptr)
{
    // if next node is empty then return true
    if (ptr == null)
        return true;

    // if current node is leaf node then return true
    // because it is end of root to leaf path
    if (ptr.left == null && ptr.right == null)
        return true;

    // If left subtree is empty, then only check right
    if (ptr.left == null)
    return (Math.abs(ptr.data - ptr.right.data) == 1) &&
            treeContinuous(ptr.right);

    // If right subtree is empty, then only check left
    if (ptr.right == null)
    return (Math.abs(ptr.data - ptr.left.data) == 1) &&
            treeContinuous(ptr.left);

    // If both left and right subtrees are not empty, check
    // everything
    return Math.abs(ptr.data - ptr.left.data)==1 &&
            Math.abs(ptr.data - ptr.right.data)==1 &&
            treeContinuous(ptr.left) &&
            treeContinuous(ptr.right);
}

/* Driver program to test mirror() */
public static void main(String args[])
{
    Node root = newNode(3);
    root.left     = newNode(2);
    root.right     = newNode(4);
    root.left.left = newNode(1);
    root.left.right = newNode(3);
    root.right.right = newNode(5);
    if(treeContinuous(root))
    System.out.println( "Yes") ;
    else
    System.out.println( "No");
}
}
//contributed by Arnab Kundu
```

## C#

```
// C# program to check if a tree is continuous or not
using System;

class solution
{

/* A binary tree node has data, pointer to left child
and a pointer to right child */
class Node
{
    public int data;
    public Node left, right;
};

/* Helper function that allocates a new node with the
given data and null left and right pointers. */

static Node newNode(int data)
{
    Node node = new Node();
    node.data = data;
    node.left = node.right = null;
    return(node);
}

// Function to check tree is continuous or not

static Boolean treeContinuous( Node ptr)
{
    // if next node is empty then return true
    if (ptr == null)
        return true;

    // if current node is leaf node then return true
    // because it is end of root to leaf path
    if (ptr.left == null && ptr.right == null)
        return true;

    // If left subtree is empty, then only check right
    if (ptr.left == null)
    return (Math.Abs(ptr.data - ptr.right.data) == 1) &&
            treeContinuous(ptr.right);

    // If right subtree is empty, then only check left
    if (ptr.right == null)
    return (Math.Abs(ptr.data - ptr.left.data) == 1) &&
            treeContinuous(ptr.left);

    // If both left and right subtrees are not empty, check
    // everything
    return Math.Abs(ptr.data - ptr.left.data)==1 &&
            Math.Abs(ptr.data - ptr.right.data)==1 &&
            treeContinuous(ptr.left) &&
            treeContinuous(ptr.right);
}

/* Driver program to test mirror() */
static public void Main(String []args)
{
    Node root = newNode(3);
    root.left     = newNode(2);
    root.right     = newNode(4);
    root.left.left = newNode(1);
    root.left.right = newNode(3);
    root.right.right = newNode(5);
    if(treeContinuous(root))
    Console.WriteLine( "Yes") ;
    else
    Console.WriteLine( "No");
}
}
//contributed by Arnab Kundu
```

## java 描述语言

```
<script>

// JavaScript program to check if a tree is continuous or not

/* A binary tree node has data, pointer to left child
and a pointer to right child */
class Node
{
    constructor()
    {
        this.data=0;
        this.left = null;
        this.right = null;
    }
};

/* Helper function that allocates a new node with the
given data and null left and right pointers. */

function newNode(data)
{
    var node = new Node();
    node.data = data;
    node.left = node.right = null;
    return(node);
}

// Function to check tree is continuous or not
function treeContinuous( ptr)
{
    // if next node is empty then return true
    if (ptr == null)
        return true;

    // if current node is leaf node then return true
    // because it is end of root to leaf path
    if (ptr.left == null && ptr.right == null)
        return true;

    // If left subtree is empty, then only check right
    if (ptr.left == null)
    return (Math.abs(ptr.data - ptr.right.data) == 1) &&
            treeContinuous(ptr.right);

    // If right subtree is empty, then only check left
    if (ptr.right == null)
    return (Math.abs(ptr.data - ptr.left.data) == 1) &&
            treeContinuous(ptr.left);

    // If both left and right subtrees are not empty, check
    // everything
    return Math.abs(ptr.data - ptr.left.data)==1 &&
            Math.abs(ptr.data - ptr.right.data)==1 &&
            treeContinuous(ptr.left) &&
            treeContinuous(ptr.right);
}

/* Driver program to test mirror() */
var root = newNode(3);
root.left     = newNode(2);
root.right     = newNode(4);
root.left.left = newNode(1);
root.left.right = newNode(3);
root.right.right = newNode(5);
if(treeContinuous(root))
    document.write( "Yes") ;
else
    document.write( "No");

</script>
```

**输出:**

```
Yes
```

本文由 [**沙莎克·米什拉(古卢)**](https://www.facebook.com/shashank.mishra.92167) 供稿。

**另一种方法(使用 BFS(队列))**

**说明:**

我们将简单地逐层遍历每个节点，检查父节点和子节点之间的差异是否为 1，如果所有节点都为真，那么我们将返回**真**否则我们将返回**假**。

## C++14

```
// CPP Code to check if the tree is continuous or not
#include <bits/stdc++.h>
using namespace std;

// Node structure
struct node {
    int val;
    node* left;
    node* right;
    node()
        : val(0)
        , left(nullptr)
        , right(nullptr)
    {
    }
    node(int x)
        : val(x)
        , left(nullptr)
        , right(nullptr)
    {
    }
    node(int x, node* left, node* right)
        : val(x)
        , left(left)
        , right(right)
    {
    }
};

// Function to check if the tree is continuous or not
bool continuous(struct node* root)
{

    // If root is Null then tree isn't Continuous
    if (root == NULL)
        return false;

    int flag = 1;
    queue<struct node*> Q;
    Q.push(root);
    node* temp;

    // BFS Traversal
    while (!Q.empty()) {
        temp = Q.front();
        Q.pop();

        // Move to left child
        if (temp->left) {

            // if difference between parent and child is
            // equal to 1 then do continue otherwise make
            // flag = 0 and break
            if (abs(temp->left->val - temp->val) == 1)
                Q.push(temp->left);
            else {
                flag = 0;
                break;
            }
        }

        // Move to right child
        if (temp->right) {

            // if difference between parent and child is
            // equal to 1 then do continue otherwise make
            // flag = 0 and break
            if (abs(temp->right->val - temp->val) == 1)
                Q.push(temp->right);
            else {
                flag = 0;
                break;
            }
        }
    }
    if (flag)
        return true;
    else
        return false;
}

// Driver Code
int main()
{
    // Constructing the Tree
    struct node* root = new node(3);
    root->left = new node(2);
    root->right = new node(4);
    root->left->left = new node(1);
    root->left->right = new node(3);
    root->right->right = new node(5);

    // Function Call
    if (continuous(root))
        cout << "True\n";
    else
        cout << "False\n";

    return 0;
}

// This code is contributed by Sanjeev Yadav.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA Code to check if the tree is continuous or not
import java.util.*;
class GFG
{

// Node structure
static class node
{
    int val;
    node left;
    node right;
    node()
    {
        this.val = 0;
        this.left = null;
        this.right= null;

    }
    node(int x)
    {
        this.val = x;
        this.left = null;
        this.right= null;

    }
    node(int x, node left, node right)
    {
        this.val = x;
        this.left = left;
        this.right= right;   
    }
};

// Function to check if the tree is continuous or not
static boolean continuous(node root)
{

    // If root is Null then tree isn't Continuous
    if (root == null)
        return false;

    int flag = 1;
    Queue<node> Q = new LinkedList<>();
    Q.add(root);
    node temp;

    // BFS Traversal
    while (!Q.isEmpty())
    {
        temp = Q.peek();
        Q.remove();

        // Move to left child
        if (temp.left != null)
        {

            // if difference between parent and child is
            // equal to 1 then do continue otherwise make
            // flag = 0 and break
            if (Math.abs(temp.left.val - temp.val) == 1)
                Q.add(temp.left);
            else
            {
                flag = 0;
                break;
            }
        }

        // Move to right child
        if (temp.right != null)
        {

            // if difference between parent and child is
            // equal to 1 then do continue otherwise make
            // flag = 0 and break
            if (Math.abs(temp.right.val - temp.val) == 1)
                Q.add(temp.right);
            else           
            {
                flag = 0;
                break;
            }
        }
    }
    if (flag != 0)
        return true;
    else
        return false;
}

// Driver Code
public static void main(String[] args)
{

    // Constructing the Tree
    node root = new node(3);
    root.left = new node(2);
    root.right = new node(4);
    root.left.left = new node(1);
    root.left.right = new node(3);
    root.right.right = new node(5);

    // Function Call
    if (continuous(root))
        System.out.print("True\n");
    else
        System.out.print("False\n");
}
}

// This code is contributed by Rajput-Ji
```

## C#

```
// C# Code to check if the tree is continuous or not
using System;
using System.Collections.Generic;
class GFG
{

  // Node structure
  public
    class node
    {
      public
        int val;
      public
        node left;
      public
        node right;
      public node()
      {
        this.val = 0;
        this.left = null;
        this.right = null;  
      }
      public node(int x)
      {
        this.val = x;
        this.left = null;
        this.right = null;
      }
      public node(int x, node left, node right)
      {
        this.val = x;
        this.left = left;
        this.right = right;   
      }
    };

  // Function to check if the tree is continuous or not
  static bool continuous(node root)
  {

    // If root is Null then tree isn't Continuous
    if (root == null)
      return false;
    int flag = 1;
    Queue<node> Q = new Queue<node>();
    Q.Enqueue(root);
    node temp;

    // BFS Traversal
    while (Q.Count != 0)
    {
      temp = Q.Peek();
      Q.Dequeue();

      // Move to left child
      if (temp.left != null)
      {

        // if difference between parent and child is
        // equal to 1 then do continue otherwise make
        // flag = 0 and break
        if (Math.Abs(temp.left.val - temp.val) == 1)
          Q.Enqueue(temp.left);
        else
        {
          flag = 0;
          break;
        }
      }

      // Move to right child
      if (temp.right != null)
      {

        // if difference between parent and child is
        // equal to 1 then do continue otherwise make
        // flag = 0 and break
        if (Math.Abs(temp.right.val - temp.val) == 1)
          Q.Enqueue(temp.right);
        else           
        {
          flag = 0;
          break;
        }
      }
    }
    if (flag != 0)
      return true;
    else
      return false;
  }

  // Driver Code
  public static void Main(String[] args)
  {

    // Constructing the Tree
    node root = new node(3);
    root.left = new node(2);
    root.right = new node(4);
    root.left.left = new node(1);
    root.left.right = new node(3);
    root.right.right = new node(5);

    // Function Call
    if (continuous(root))
      Console.Write("True\n");
    else
      Console.Write("False\n");
  }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript Code to check if the tree is continuous or not

// Node structure
class Node
{ 
    constructor(x)
    {
        this.val = x;
        this.left = null;
        this.right= null;
    }
}

// Function to check if the tree is continuous or not
function continuous(root)
{

    // If root is Null then tree isn't Continuous
    if (root == null)
        return false;

    let flag = 1;
    let Q = [];
    Q.push(root);
    let temp;

    // BFS Traversal
    while (Q.length!=0)
    {
        temp = Q.shift();

        // Move to left child
        if (temp.left != null)
        {

            // if difference between parent and child is
            // equal to 1 then do continue otherwise make
            // flag = 0 and break
            if (Math.abs(temp.left.val - temp.val) == 1)
                Q.push(temp.left);
            else
            {
                flag = 0;
                break;
            }
        }

        // Move to right child
        if (temp.right != null)
        {

            // if difference between parent and child is
            // equal to 1 then do continue otherwise make
            // flag = 0 and break
            if (Math.abs(temp.right.val - temp.val) == 1)
                Q.push(temp.right);
            else          
            {
                flag = 0;
                break;
            }
        }
    }
    if (flag != 0)
        return true;
    else
        return false;
}

// Driver Code
// Constructing the Tree
let root = new Node(3);
root.left = new Node(2);
root.right = new Node(4);
root.left.left = new Node(1);
root.left.right = new Node(3);
root.right.right = new Node(5);

// Function Call
if (continuous(root))
    document.write("True<br>");
else
    document.write("False<br>");

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output**

```
True
```

**时间复杂度:** O(n)

如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。