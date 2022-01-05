# 检查二叉树中的子和属性

> 原文:[https://www . geesforgeks . org/check-for-children-sum-property-in-a-a-binary-tree/](https://www.geeksforgeeks.org/check-for-children-sum-property-in-a-binary-tree/)

给定一个二叉树，写一个函数，如果该树满足下面的属性，则返回 true。
对于每个节点，数据值必须等于左右子节点的数据值之和。对于空子代，将数据值视为 0。下图是一个例子

![](img/96129b447b7960af0fbcf094abbc046b.png)

**算法:**
遍历给定的二叉树。对于每个节点，检查(递归地)该节点及其两个子节点是否满足子总和属性，如果满足，则返回真，否则返回假。
**实施:**

## C++

```
/* Program to check children sum property */
#include <bits/stdc++.h>
using namespace std;

/* A binary tree node has data, left
child and right child */
struct node
{
    int data;
    struct node* left;
    struct node* right;
};

/* returns 1 if children sum property holds
for the given node and both of its children*/
int isSumProperty(struct node* node)
{
    /* left_data is left child data and
       right_data is for right child data*/
    int sum = 0;

    /* If node is NULL or it's a leaf node
    then return true */
    if(node == NULL ||
        (node->left == NULL &&
         node->right == NULL))
        return 1;
    else
    {
        /* If left child is not present then 0
        is used as data of left child */
        if(node->left != NULL)
        sum += node->left->data;

        /* If right child is not present then 0
        is used as data of right child */
        if(node->right != NULL)
        sum+ = node->right->data;

        /* if the node and both of its children
        satisfy the property return 1 else 0*/
        return ((node->data == sum)&&
            isSumProperty(node->left) &&
            isSumProperty(node->right))
    }
}

/*
Helper function that allocates a new node
with the given data and NULL left and right
pointers.
*/
struct node* newNode(int data)
{
    struct node* node =
        (struct node*)malloc(sizeof(struct node));
    node->data = data;
    node->left = NULL;
    node->right = NULL;
    return(node);
}

// Driver Code
int main()
{
    struct node *root = newNode(10);
    root->left     = newNode(8);
    root->right = newNode(2);
    root->left->left = newNode(3);
    root->left->right = newNode(5);
    root->right->right = newNode(2);
    if(isSumProperty(root))
        cout << "The given tree satisfies "
            << "the children sum property ";
    else
        cout << "The given tree does not satisfy "
            << "the children sum property ";

    getchar();
    return 0;
}
// This code is contributed by Akanksha Rai
```

## C

```
/* Program to check children sum property */
#include <stdio.h>
#include <stdlib.h>

/* A binary tree node has data, left child and right child */
struct node
{
    int data;
    struct node* left;
    struct node* right;
};

/* returns 1 if children sum property holds for the given
    node and both of its children*/
int isSumProperty(struct node* node)
{
  /* left_data is left child data and right_data is for right
     child data*/
  int left_data = 0,  right_data = 0;

  /* If node is NULL or it's a leaf node then
     return true */
  if(node == NULL ||
     (node->left == NULL && node->right == NULL))
    return 1;
  else
  {
    /* If left child is not present then 0 is used
       as data of left child */
    if(node->left != NULL)
      left_data = node->left->data;

    /* If right child is not present then 0 is used
      as data of right child */
    if(node->right != NULL)
      right_data = node->right->data;

    /* if the node and both of its children satisfy the
       property return 1 else 0*/
    if((node->data == left_data + right_data)&&
        isSumProperty(node->left) &&
        isSumProperty(node->right))
      return 1;
    else
      return 0;
  }
}

/*
 Helper function that allocates a new node
 with the given data and NULL left and right
 pointers.
*/
struct node* newNode(int data)
{
  struct node* node =
      (struct node*)malloc(sizeof(struct node));
  node->data = data;
  node->left = NULL;
  node->right = NULL;
  return(node);
}

/* Driver program to test above function */
int main()
{
  struct node *root  = newNode(10);
  root->left         = newNode(8);
  root->right        = newNode(2);
  root->left->left   = newNode(3);
  root->left->right  = newNode(5);
  root->right->right = newNode(2);
  if(isSumProperty(root))
    printf("The given tree satisfies the children sum property ");
  else
    printf("The given tree does not satisfy the children sum property ");

  getchar();
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check children sum property

/* A binary tree node has data, pointer to left child
   and a pointer to right child */
class Node
{
    int data;
    Node left, right;

    public Node(int d)
    {
        data = d;
        left = right = null;
    }
}

class BinaryTree
{
    Node root;

    /* returns 1 if children sum property holds for the given
    node and both of its children*/
    int isSumProperty(Node node)
    {

        /* left_data is left child data and right_data is for right
           child data*/
        int left_data = 0, right_data = 0;

        /* If node is NULL or it's a leaf node then
        return true */
        if (node == null
                || (node.left == null && node.right == null))
            return 1;
        else
        {

            /* If left child is not present then 0 is used
               as data of left child */
            if (node.left != null)
                left_data = node.left.data;

            /* If right child is not present then 0 is used
               as data of right child */
            if (node.right != null)
                right_data = node.right.data;

            /* if the node and both of its children satisfy the
               property return 1 else 0*/
            if ((node.data == left_data + right_data)
                    && (isSumProperty(node.left)!=0)
                    && isSumProperty(node.right)!=0)
                return 1;
            else
                return 0;
        }
    }

    /* driver program to test the above functions */
    public static void main(String[] args)
    {
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(10);
        tree.root.left = new Node(8);
        tree.root.right = new Node(2);
        tree.root.left.left = new Node(3);
        tree.root.left.right = new Node(5);
        tree.root.right.right = new Node(2);
        if (tree.isSumProperty(tree.root) != 0)
            System.out.println("The given tree satisfies children"
                    + " sum property");
        else
            System.out.println("The given tree does not satisfy children"
                    + " sum property");
    }
}
```

## 蟒蛇 3

```
# Python3 program to check children
# sum property

# Helper class that allocates a new
# node with the given data and None
# left and right pointers.
class newNode:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

# returns 1 if children sum property
# holds for the given node and both
# of its children
def isSumProperty(node):

    # left_data is left child data and
    # right_data is for right child data
    left_data = 0
    right_data = 0

    # If node is None or it's a leaf
    # node then return true
    if(node == None or (node.left == None and
                        node.right == None)):
        return 1
    else:

        # If left child is not present then
        # 0 is used as data of left child
        if(node.left != None):
            left_data = node.left.data

        # If right child is not present then
        # 0 is used as data of right child
        if(node.right != None):
            right_data = node.right.data

        # if the node and both of its children 
        # satisfy the property return 1 else 0
        if((node.data == left_data + right_data) and
                        isSumProperty(node.left) and
                        isSumProperty(node.right)):
            return 1
        else:
            return 0

# Driver Code
if __name__ == '__main__':
    root = newNode(10)
    root.left = newNode(8)
    root.right = newNode(2)
    root.left.left = newNode(3)
    root.left.right = newNode(5)
    root.right.right = newNode(2)
    if(isSumProperty(root)):
        print("The given tree satisfies the",
                    "children sum property ")
    else:
        print("The given tree does not satisfy",
                   "the children sum property ")

# This code is contributed by PranchalK
```

## C#

```
// C# program to check children sum property
using System;

/* A binary tree node has data, pointer
to left child and a pointer to right child */
public class Node
{
    public int data;
    public Node left, right;

    public Node(int d)
    {
        data = d;
        left = right = null;
    }
}

class GFG
{
public Node root;

/* returns 1 if children sum property holds
for the given node and both of its children*/
public virtual int isSumProperty(Node node)
{

    /* left_data is left child data and
    right_data is for right child data*/
    int left_data = 0, right_data = 0;

    /* If node is NULL or it's a leaf
    node then return true */
    if (node == null || (node.left == null &&
                         node.right == null))
    {
        return 1;
    }
    else
    {

        /* If left child is not present
        then 0 is used as data of left child */
        if (node.left != null)
        {
            left_data = node.left.data;
        }

        /* If right child is not present then
        0 is used as data of right child */
        if (node.right != null)
        {
            right_data = node.right.data;
        }

        /* if the node and both of its children
        satisfy the property return 1 else 0*/
        if ((node.data == left_data + right_data) &&
                  (isSumProperty(node.left) != 0) &&
                   isSumProperty(node.right) != 0)
        {
            return 1;
        }
        else
        {
            return 0;
        }
    }
}

// Driver Code
public static void Main(string[] args)
{
    GFG tree = new GFG();
    tree.root = new Node(10);
    tree.root.left = new Node(8);
    tree.root.right = new Node(2);
    tree.root.left.left = new Node(3);
    tree.root.left.right = new Node(5);
    tree.root.right.right = new Node(2);
    if (tree.isSumProperty(tree.root) != 0)
    {
        Console.WriteLine("The given tree satisfies" +
                            " children sum property");
    }
    else
    {
        Console.WriteLine("The given tree does not" +
                   " satisfy children sum property");
    }
}
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

      // JavaScript program to check children sum property

    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
        }
    }

    let root;

    /* returns 1 if children sum property holds for the given
    node and both of its children*/
    function isSumProperty(node)
    {

        /* left_data is left child data and right_data is for right
           child data*/
        let left_data = 0, right_data = 0;

        /* If node is NULL or it's a leaf node then
        return true */
        if (node == null
                || (node.left == null && node.right == null))
            return 1;
        else
        {

            /* If left child is not present then 0 is used
               as data of left child */
            if (node.left != null)
                left_data = node.left.data;

            /* If right child is not present then 0 is used
               as data of right child */
            if (node.right != null)
                right_data = node.right.data;

            /* if the node and both of its children satisfy the
               property return 1 else 0*/
            if ((node.data == left_data + right_data)
                    && (isSumProperty(node.left)!=0)
                    && isSumProperty(node.right)!=0)
                return 1;
            else
                return 0;
        }
    }

    root = new Node(10);
    root.left = new Node(8);
    root.right = new Node(2);
    root.left.left = new Node(3);
    root.left.right = new Node(5);
    root.right.right = new Node(2);
    if (isSumProperty(root) != 0)
      document.write("The given tree satisfies the children"
                         + " sum property");
    else
      document.write("The given tree does not satisfy children"
                         + " sum property");

</script>
```

**输出:**

```
The given tree satisfies the children sum property 
```

**时间复杂度:** O(n)，我们在做一个完整的树遍历。

作为练习，将上述问题扩展到 n 元树。
这个问题是谢哈尔问的。
如发现上述算法有 bug 或有更好的方法解决同样的问题，请写评论。