# 二叉树|集合 1(简介)

> 原文:[https://www . geesforgeks . org/二叉树-set-1-introduction/](https://www.geeksforgeeks.org/binary-tree-set-1-introduction/)

**树:**与数组、链表、栈和队列是线性数据结构不同，树是分层数据结构。
**树词汇:**最顶端的节点叫树根。直接位于元素下的元素称为其子元素。某物正上方的元素称为它的父元素。例如，“a”是“f”的子代，“f”是“a”的父代。最后，没有子元素的元素叫做叶子。

```
      tree
      ----
       j    <-- root
     /   \
    f      k  
  /   \      \
 a     h      z    <-- leaves
```

**为什么是树？**
**1。**使用树的一个原因可能是因为你想存储自然形成层次结构的信息。例如，计算机上的文件系统:

```
file system
-----------
     /    <-- root
  /      \
...       home
      /          \
   ugrad        course
    /       /      |     \
  ...      cs101  cs112  cs113
```

**2。**树(具有一些排序，例如 BST)提供适度的访问/搜索(比链表快，比数组慢)。
T3】3。树提供适度的插入/删除(比数组快，比无序链表慢)。
**4。**像链表和不像数组一样，树没有节点数量的上限，因为节点是用指针链接的。
**树木的主要应用包括:**
**1。**操纵分层数据。
**2。**使信息易于搜索(参见树遍历)。
**3。**处理排序后的数据列表。
T21【4】。作为合成数字图像以获得视觉效果的工作流程。
**5。**路由器算法
**6。**多阶段决策的形式(见商业棋局)。
**二叉树:**元素最多有 2 个子元素的树称为二叉树。由于二叉树中的每个元素只能有两个子元素，我们通常将它们命名为左右子元素。
**C 语言中的二叉树表示法:**树是由指向树中最顶端节点的指针来表示的。如果树为空，则根的值为空。
树节点包含以下部分。
1。数据
2。指针指向左子
3。在 C 语言中，我们可以用结构来表示一个树节点。下面是一个包含整数数据的树节点的示例。

## C++

```
struct node
{
    int data;
    struct node* left;
    struct node* right;
};
```

## 计算机编程语言

```
# A Python class that represents an individual node
# in a Binary Tree
class Node:
    def __init__(self,key):
        self.left = None
        self.right = None
        self.val = key
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Class containing left and right child of current
   node and key value*/
class Node
{
    int key;
    Node left, right;

    public Node(int item)
    {
        key = item;
        left = right = null;
    }
}
```

## C#

```
/* Class containing left and right child
of current node and key value*/
class Node
{
    int key;
    Node left, right;

    public Node(int item)
    {
        key = item;
        left = right = null;
    }
}
```

## java 描述语言

```
<script>
/* Class containing left and right child of current
   node and key value*/
class Node
{
    constructor(item)
    {
        this.key = item;
        this.left = this.right = null;
    }
}

// This code is contributed by umadevi9616
</script>
```

**C 中的第一棵简单树**
让我们在 C 中创建一棵具有 4 个节点的简单树。

```
      tree
      ----
       1    <-- root
     /   \
    2     3  
   /   
  4
```

## C++

```
#include <bits/stdc++.h>
using namespace std;

struct Node {
    int data;
    struct Node* left;
    struct Node* right;

    // val is the key or the value that
    // has to be added to the data part
    Node(int val)
    {
        data = val;

        // Left and right child for node
        // will be initialized to null
        left = NULL;
        right = NULL;
    }
};

int main()
{

    /*create root*/
    struct Node* root = new Node(1);
    /* following is the tree after above statement

             1
            / \
          NULL NULL
    */

    root->left = new Node(2);
    root->right = new Node(3);
    /* 2 and 3 become left and right children of 1
                    1
                  /    \
                 2       3
               /  \     /  \
            NULL NULL  NULL NULL
    */

    root->left->left = new Node(4);
    /* 4 becomes left child of 2
               1
            /     \
           2       3
          / \     / \
         4  NULL NULL NULL
        / \
     NULL NULL
    */

    return 0;
}
```

## C

```
#include <stdio.h>
#include <stdlib.h>
struct node {
    int data;
    struct node* left;
    struct node* right;
};

/* newNode() allocates a new node
with the given data and NULL left
and right pointers. */
struct node* newNode(int data)
{
    // Allocate memory for new node
    struct node* node
        = (struct node*)malloc(sizeof(struct node));

    // Assign data to this node
    node->data = data;

    // Initialize left and
    // right children as NULL
    node->left = NULL;
    node->right = NULL;
    return (node);
}

int main()
{
    /*create root*/
    struct node* root = newNode(1);
    /* following is the tree after above statement
         1
        / \
      NULL NULL
    */

    root->left = newNode(2);
    root->right = newNode(3);
    /* 2 and 3 become left and right children of 1
            1
         /    \
        2      3
      /  \    /  \
   NULL NULL NULL NULL
    */

    root->left->left = newNode(4);
    /* 4 becomes left child of 2
             1
         /    \
        2      3
      /  \    /  \
     4 NULL NULL NULL
    / \
 NULL NULL
    */

    getchar();
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Class containing left and right child of current
   node and key value*/
class Node
{
    int key;
    Node left, right;

    public Node(int item)
    {
        key = item;
        left = right = null;
    }
}

// A Java program to introduce Binary Tree
class BinaryTree
{
    // Root of Binary Tree
    Node root;

    // Constructors
    BinaryTree(int key)
    {
        root = new Node(key);
    }

    BinaryTree()
    {
        root = null;
    }

    public static void main(String[] args)
    {
        BinaryTree tree = new BinaryTree();

        /*create root*/
        tree.root = new Node(1);

        /* following is the tree after above statement

              1
            /   \
          null  null     */

        tree.root.left = new Node(2);
        tree.root.right = new Node(3);

        /* 2 and 3 become left and right children of 1
               1
            /     \
          2        3
        /   \     /  \
      null null null null  */

        tree.root.left.left = new Node(4);
        /* 4 becomes left child of 2
                    1
                /       \
               2          3
             /   \       /  \
            4    null  null  null
           /   \
          null null
         */
    }
}
```

## 计算机编程语言

```
# Python program to introduce Binary Tree

# A class that represents an individual node in a
# Binary Tree
class Node:
    def __init__(self,key):
        self.left = None
        self.right = None
        self.val = key

# create root
root = Node(1)
''' following is the tree after above statement
        1
      /   \
     None  None'''

root.left      = Node(2);
root.right     = Node(3);

''' 2 and 3 become left and right children of 1
           1
         /   \
        2      3
     /    \    /  \
   None None None None'''

root.left.left  = Node(4);
'''4 becomes left child of 2
           1
       /       \
      2          3
    /   \       /  \
   4    None  None  None
  /  \
None None'''
```

## C#

```
// A C# program to introduce Binary Tree
using System;

/* Class containing left and right child
of current node and key value*/
public class Node
{
    public int key;
    public Node left, right;

    public Node(int item)
    {
        key = item;
        left = right = null;
    }
}

public class BinaryTree
{
    // Root of Binary Tree
    Node root;

    // Constructors
    BinaryTree(int key)
    {
        root = new Node(key);
    }

    BinaryTree()
    {
        root = null;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        BinaryTree tree = new BinaryTree();

        /*create root*/
        tree.root = new Node(1);

        /* following is the tree after above statement

             1
            / \
         null null     */
        tree.root.left = new Node(2);
        tree.root.right = new Node(3);

        /* 2 and 3 become left and right children of 1
                1
             /     \
           2        3
         /  \     /   \
       null null null null */
        tree.root.left.left = new Node(4);

        /* 4 becomes left child of 2
                1
             /     \
           2        3
         /  \     /   \
         4 null null null
        / \
     null null
        */
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
/* Class containing left and right child of current
   node and key value*/
 class Node {
        constructor(val) {
            this.key = val;
            this.left = null;
            this.right = null;
        }
    }

// A javascript program to introduce Binary Tree

    // Root of Binary Tree
    var root = null;

        /*create root*/
        root = new Node(1);

        /* following is the tree after above statement

              1
            /   \
          null  null     */

        root.left = new Node(2);
        root.right = new Node(3);

        /* 2 and 3 become left and right children of 1
               1
            /     \
          2        3
        /   \     /  \
      null null null null  */     
      root.left.left = new Node(4);
        /* 4 becomes left child of 2
                    1
                /       \
               2          3
             /   \       /  \
            4    null  null  null
           /   \
          null null
         */

// This code contributed by umadevi9616
</script>
```

**总结:**树是一种分层的数据结构。树的主要用途包括维护分层数据，提供适度的访问和插入/删除操作。二叉树是树的特例，其中每个节点最多有两个子节点。
https://youtu.be/W6aZKAJcNJA
以下为本岗位第二套、第三套。
[二叉树的属性](https://www.geeksforgeeks.org/binary-tree-set-2-properties/)
[二叉树的类型](https://www.geeksforgeeks.org/binary-tree-set-3-types-of-binary-tree/)
如有不正确的地方请写评论，或者想分享更多以上讨论话题的信息。