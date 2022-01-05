# 将任意二叉树转换为持有子和属性的树–集合 2

> 原文:[https://www . geesforgeks . org/convert-一个任意二叉树到一个保存子树的树-sum-property-set-2/](https://www.geeksforgeeks.org/convert-an-arbitrary-binary-tree-to-a-tree-that-holds-children-sum-property-set-2/)

**问题:** 给定任意二叉树，将其转换为持有 [<u>子和属性</u>](https://www.geeksforgeeks.org/check-for-children-sum-property-in-a-binary-tree/) 的二叉树。您只能增加任何节点中的数据值(您不能更改树的结构，也不能减少任何节点的值)。
比如下面的树没有持有孩子的 sum 属性，将其转换为持有该属性的树。

> 50
> 
> / \
> 
> / \
> 
>        7             2
> 
> / \ /\
> 
> / \ / \
> 
>   3        5      1      30

**天真方法:**天真方法在本文的[第 1 集中讨论。这里，我们正在讨论优化方法。](https://www.geeksforgeeks.org/convert-an-arbitrary-binary-tree-to-a-tree-that-holds-children-sum-property/)

**算法:**将子节点转换为最大可能值，因此在向后移动时，没有父节点的值超过子节点的值，因此不会有额外的函数来再次遍历该节点的子树。

*   如果子节点的总和小于当前节点，则用当前节点的值替换两个子节点的值。

> 如果(节点->左+节点->右< node->数据)
> 将节点- >数据值放在两个子项中

*   如果子节点的总和大于或等于当前节点，则用子节点的总和替换当前节点的值。

> 如果(节点->左->数据+节点->右->数据> =节点->数据)
> 将两个子数据值的总和放在节点- >数据中

*   在向后遍历时，用左右子数据的总和覆盖现有的节点值。

(注意:不会有节点的值大于其子节点的值之和的情况，因为我们已经给了它们最大可能的值)。

按照以下步骤解决问题:

*   如果**根**为**空**则返回。
*   将变量**子总和**初始化为 **0。**
*   如果**根**有子代，那么将它们的值添加到**子代总和中。**
*   如果**子总和**大于等于**根- >数据，**则将**根- >数据**设置为**子总和**。
*   否则，如果有**根的孩子，**则将他们孩子的数据设置为**根- >数据。**
*   对**根- >左**和**根- >右调用相同的[功能](https://www.geeksforgeeks.org/functions-in-c/)。**
*   将变量**初始化为 **0** 。**
*   如果**根**有子代，那么将它们的数据值添加到变量**totalsumto changepart 中。**
*   如果**根**有子级，则将**根**的值设置为 **totalSumToChangeParent。**

下面是上述方法的实现。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Structure of a node in a binary tree
struct Node {
    int data;
    Node* left;
    Node* right;
    Node(int x)
    {
        data = x;
        left = NULL;
        right = NULL;
    }
};

// Convert the tree such that it holds
// children sum property
void convertTree(Node* root)
{
    if (root == NULL)
        return;

    // Calculating the sum
    // of left and right child
    int childSum = 0;
    if (root->left)
        childSum += root->left->data;
    if (root->right)
        childSum += root->right->data;

    // If sum of child is greater
    // then change the node's
    // data else change the data
    // of left and right child to
    // make sure they will get
    // the maximum possible value
    if (childSum >= root->data)
        root->data = childSum;
    else {
        if (root->left)
            root->left->data = root->data;
        if (root->right)
            root->right->data = root->data;
    }

    // Recursive call for left child
    convertTree(root->left);

    // Recursive call for right child
    convertTree(root->right);

    // Overwriting the parent's data
    int totalSumToChangeParent = 0;
    if (root->left)
        totalSumToChangeParent
            += root->left->data;
    if (root->right)
        totalSumToChangeParent
            += root->right->data;
    if (root->left || root->right)
        root->data = totalSumToChangeParent;
}

void printInorder(Node* root)
{
    if (root == NULL)
        return;

    // Recursive call to left child
    printInorder(root->left);

    // Printing the node's data
    cout << root->data << " ";

    // Recursive call to right child
    printInorder(root->right);
}

// Driver Code
int main()
{

    Node* root = new Node(50);
    root->left = new Node(7);
    root->right = new Node(2);
    root->left->left = new Node(3);
    root->left->right = new Node(5);
    root->right->left = new Node(1);
    root->right->right = new Node(30);

    convertTree(root);

    printInorder(root);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Structure of a node in a binary tree
static class Node {
    int data;
    Node left;
    Node right;
    Node(int x)
    {
        data = x;
        left = null;
        right = null;
    }
};

// Convert the tree such that it holds
// children sum property
static void convertTree(Node root)
{
    if (root == null)
        return;

    // Calculating the sum
    // of left and right child
    int childSum = 0;
    if (root.left!=null)
        childSum += root.left.data;
    if (root.right!=null)
        childSum += root.right.data;

    // If sum of child is greater
    // then change the node's
    // data else change the data
    // of left and right child to
    // make sure they will get
    // the maximum possible value
    if (childSum >= root.data)
        root.data = childSum;
    else {
        if (root.left!=null)
            root.left.data = root.data;
        if (root.right!=null)
            root.right.data = root.data;
    }

    // Recursive call for left child
    convertTree(root.left);

    // Recursive call for right child
    convertTree(root.right);

    // Overwriting the parent's data
    int totalSumToChangeParent = 0;
    if (root.left != null)
        totalSumToChangeParent
            += root.left.data;
    if (root.right != null)
        totalSumToChangeParent
            += root.right.data;
    if (root.left != null || root.right != null)
        root.data = totalSumToChangeParent;
}

static void printInorder(Node root)
{
    if (root == null)
        return;

    // Recursive call to left child
    printInorder(root.left);

    // Printing the node's data
    System.out.print(root.data+ " ");

    // Recursive call to right child
    printInorder(root.right);
}

// Driver Code
public static void main(String[] args)
{

    Node root = new Node(50);
    root.left = new Node(7);
    root.right = new Node(2);
    root.left.left = new Node(3);
    root.left.right = new Node(5);
    root.right.left = new Node(1);
    root.right.right = new Node(30);

    convertTree(root);

    printInorder(root);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python code for the above approach

# Class of a node in a binary tree
class Node:

    def __init__(self, x):
        self.data = x
        self.left = None
        self.right = None

# Convert the tree such that it holds
# children sum property
def convertTree(root):
    if (root == None):
        return

    # Calculating the sum
    # of left and right child
    childSum = 0
    if (root.left):
        childSum += root.left.data
    if (root.right):
        childSum += root.right.data

    # If sum of child is greater
    # then change the node's
    # data else change the data
    # of left and right child to
    # make sure they will get
    # the maximum possible value
    if (childSum >= root.data):
        root.data = childSum
    else:
        if (root.left):
            root.left.data = root.data
        if (root.right):
            root.right.data = root.data

    # Recursive call for left child
    convertTree(root.left)

    # Recursive call for right child
    convertTree(root.right)

    # Overwriting the parent's data
    totalSumToChangeParent = 0
    if (root.left):
        totalSumToChangeParent += root.left.data
    if (root.right):
        totalSumToChangeParent += root.right.data
    if (root.left or root.right):
        root.data = totalSumToChangeParent

def printInorder(root):
    if (root == None):
        return

    # Recursive call to left child
    printInorder(root.left)

    # Printing the node's data
    print(root.data, end=" ")

    # Recursive call to right child
    printInorder(root.right)

# Driver Code
root = Node(50)
root.left = Node(7)
root.right = Node(2)
root.left.left = Node(3)
root.left.right = Node(5)
root.right.left = Node(1)
root.right.right = Node(30)

convertTree(root)

printInorder(root)

# self code is contributed by Saurabh Jaiswal
```

## C#

```
// C# program for the above approach
using System;
public class GFG{

// Structure of a node in a binary tree
class Node {
    public int data;
    public Node left;
    public Node right;
    public Node(int x)
    {
        data = x;
        left = null;
        right = null;
    }
};

// Convert the tree such that it holds
// children sum property
static void convertTree(Node root)
{
    if (root == null)
        return;

    // Calculating the sum
    // of left and right child
    int childSum = 0;
    if (root.left!=null)
        childSum += root.left.data;
    if (root.right!=null)
        childSum += root.right.data;

    // If sum of child is greater
    // then change the node's
    // data else change the data
    // of left and right child to
    // make sure they will get
    // the maximum possible value
    if (childSum >= root.data)
        root.data = childSum;
    else {
        if (root.left!=null)
            root.left.data = root.data;
        if (root.right!=null)
            root.right.data = root.data;
    }

    // Recursive call for left child
    convertTree(root.left);

    // Recursive call for right child
    convertTree(root.right);

    // Overwriting the parent's data
    int totalSumToChangeParent = 0;
    if (root.left != null)
        totalSumToChangeParent
            += root.left.data;
    if (root.right != null)
        totalSumToChangeParent
            += root.right.data;
    if (root.left != null || root.right != null)
        root.data = totalSumToChangeParent;
}

static void printInorder(Node root)
{
    if (root == null)
        return;

    // Recursive call to left child
    printInorder(root.left);

    // Printing the node's data
    Console.Write(root.data+ " ");

    // Recursive call to right child
    printInorder(root.right);
}

// Driver Code
public static void Main(String[] args)
{

    Node root = new Node(50);
    root.left = new Node(7);
    root.right = new Node(2);
    root.left.left = new Node(3);
    root.left.right = new Node(5);
    root.right.left = new Node(1);
    root.right.right = new Node(30);

    convertTree(root);

    printInorder(root);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
       // JavaScript code for the above approach

       // Class of a node in a binary tree
       class Node {

           constructor(x) {
               this.data = x;
               this.left = null;
               this.right = null;
           }
       };

       // Convert the tree such that it holds
       // children sum property
       function convertTree(root) {
           if (root == null)
               return;

           // Calculating the sum
           // of left and right child
           let childSum = 0;
           if (root.left)
               childSum += root.left.data;
           if (root.right)
               childSum += root.right.data;

           // If sum of child is greater
           // then change the node's
           // data else change the data
           // of left and right child to
           // make sure they will get
           // the maximum possible value
           if (childSum >= root.data)
               root.data = childSum;
           else {
               if (root.left)
                   root.left.data = root.data;
               if (root.right)
                   root.right.data = root.data;
           }

           // Recursive call for left child
           convertTree(root.left);

           // Recursive call for right child
           convertTree(root.right);

           // Overwriting the parent's data
           let totalSumToChangeParent = 0;
           if (root.left)
               totalSumToChangeParent
                   += root.left.data;
           if (root.right)
               totalSumToChangeParent
                   += root.right.data;
           if (root.left || root.right)
               root.data = totalSumToChangeParent;
       }

       function printInorder(root) {
           if (root == null)
               return;

           // Recursive call to left child
           printInorder(root.left);

           // Printing the node's data
           document.write(root.data + " ");

           // Recursive call to right child
           printInorder(root.right);
       }

       // Driver Code
       let root = new Node(50);
       root.left = new Node(7);
       root.right = new Node(2);
       root.left.left = new Node(3);
       root.left.right = new Node(5);
       root.right.left = new Node(1);
       root.right.right = new Node(30);

       convertTree(root);

       printInorder(root);

 // This code is contributed by Potta Lokesh
   </script>
```

**Output:** 

```
50 100 50 200 50 100 50
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)